# Linux Fundamentals for Security Analysts: Package Management, Filesystem, Permissions & User Administration

## Objective

This project brought together a series of hands-on labs covering the practical Linux skills required in cybersecurity roles. Working in a Debian-based virtual machine through the Bash shell, the labs progressed from installing and managing network security software with APT (Suricata, tcpdump), through navigating the Linux filesystem and reading file contents, to filtering log data with `grep` and piping, creating and modifying files and directories, and finally managing permissions, ownership, and user accounts in line with the principle of least privilege. These are the day-to-day skills a security analyst relies on when investigating incidents remotely via a shell without a graphical interface, such as navigating to and reading a user access report during an unauthorized-access investigation.

**Lab recordings:**
* **Linux File Recording:** [Open Google Drive folder](https://drive.google.com/drive/folders/10l66EblVzahm8ITEd6dWs4Mu5Msj2hZW?usp=sharing)
* **Log Analysis Recording:** [Open Google Drive folder](https://drive.google.com/drive/folders/1LEuEFPwyLwPDtSlDcxy4lxlzR5OIPVR4?usp=sharing)

## Skills Learned

* Installing, removing, and reinstalling applications with the APT package manager (`sudo apt install`, `sudo apt remove`, `apt list --installed`).
* Examining input and output in the Bash shell (`echo`, `expr`, `clear`) and redirecting output with `>`, `>>`, and pipes (`|`).
* Navigating the Linux filesystem (`pwd`, `ls`, `cd`) and understanding the Filesystem Hierarchy Standard (`/home`, `/bin`, `/etc`, `/tmp`, `/mnt`), including why `/tmp` is commonly abused by attackers.
* Reading file content with `cat`, `head`, `tail`, and `less`, including using `tail` to read the most recent entries in a log file.
* Filtering and searching log data with `grep`, piping, and `find` (with `-name`, `-iname`, `-mtime`, `-mmin`, and wildcards).
* Creating and modifying files and directories (`mkdir`, `rmdir`, `touch`, `rm`, `mv`, `cp`, `nano`).
* Analyzing and changing file permissions with `ls -l` / `ls -la` and `chmod` (symbolic notation: `u`/`g`/`o`, `+`/`-`/`=`), applying the principle of least privilege.
* Managing users and ownership with `useradd`, `usermod` (`-g`, `-a -G`, `-d`, `-l`, `-L`), `userdel`, `chown`, and `groupdel`.
* Using built-in help resources (`man`, `whatis`, `apropos`) to work independently in unfamiliar situations.

## Tools Used

* Linux Bash shell on a Debian-based virtual machine (Qwiklabs environment).
* APT (Advanced Package Tool) for package management.
* Suricata and tcpdump as example network security applications for capture and analysis of network traffic.
* Core Linux utilities: `grep`, `find`, `nano`, `chmod`, `chown`, `useradd`/`usermod`/`userdel`, `man`/`whatis`/`apropos`.

---

## Lab 1: Install and Manage Applications with APT

*Scenario: Your role as a security analyst requires the Suricata and tcpdump network security applications on your system. You must install, uninstall, and reinstall these applications in the Bash shell and confirm each state: first verifying APT is present, then installing Suricata, removing it, installing tcpdump, listing installed applications, and finally reinstalling Suricata so both tools are available.*

**Commands used:**
```bash
sudo apt install suricata
suricata
sudo apt remove suricata
sudo apt install tcpdump
tcpdump
apt list --installed
```

*Ref 1: Confirming installed applications with APT*

<img width="600" height="300" alt="apt list --installed output confirming Suricata and tcpdump" src="https://github.com/user-attachments/assets/b63e7d21-b288-4b24-a431-ea25505bf216" />

Output of the install/remove/reinstall cycle, with `apt list --installed` confirming that both Suricata and tcpdump are present on the system. Running each application by name after installation verified it was correctly installed.

📹 **Video recording:** https://screenrec.com/share/NkeE5ihLmR

---

## Lab 2: Examine Input and Output in the Shell

Used the `echo` command to examine how input is received and output is returned in the shell, performed basic calculations, and cleared the terminal.

**Commands used:**
```bash
echo osita
echo "osita"
expr 3 + 4
clear
```

Both quoted and unquoted strings return the same output with `echo`; `expr` evaluates the arithmetic expression and returns `7`; `clear` resets the shell window.

---

## Lab 3: Navigate the Filesystem and Read File Content

**Core navigation commands:** `pwd` (absolute path of the current working directory), `whoami` (current username), `ls` (list), `cd` (change directory), `cat` (display full file contents), `head` (first 10 lines by default, or e.g. `head -n 5 updates.txt` for the first five).

*Ref 2: Filesystem Hierarchy Standard*

<img width="600" height="300" alt="Filesystem Hierarchy Standard diagram" src="https://github.com/user-attachments/assets/610023bd-f8fc-4a09-8967-405f5e90943d" />

Key directories from a security perspective:
* **`/` (root directory)**: the top of the hierarchy; every file path starts here.
* **`/home`**: each user's personal directory.
* **`/bin`**: binaries and executables.
* **`/etc`**: system configuration files.
* **`/tmp`**: temporary files; commonly used by attackers because anyone on the system can modify data here.
* **`/mnt`**: mount point for media such as USB and hard drives.

**Reading file content:** `cat` (entire file), `head` (start of file), `tail` (last 10 lines by default: a practical way to read the most recent entries in a log file), and `less` (one page at a time, navigating with Space, `b`, arrow keys, and `q` to quit).

*Ref 3: Navigating the file structure and locating files*

<img width="600" height="300" alt="Navigating directories and locating files in the lab" src="https://github.com/user-attachments/assets/c6ec7b2c-a6c0-4ed1-a30e-76b6d6152dd6" />

*Ref 4: Reading file contents to answer investigation questions*

<img width="600" height="300" alt="Reading file contents with cat and head" src="https://github.com/user-attachments/assets/f38ef45b-523f-4846-ba2d-7c0e52a18d67" />

Navigated the Linux file structure, located files, and read their contents: the same workflow an analyst uses when reviewing a user access report during an unauthorized-access investigation.

---

## Lab 4: Filter Content in Linux

*Scenario: You need to obtain information contained in server log and user data files, and find files with specific names. First, navigate to the logs directory and return the error messages in `server_logs.txt`. Next, navigate to the users directory and search for files containing a specific string in their names. Finally, search for information contained inside user files.*

**Key concepts:**
* `grep` searches a file and returns all lines containing a specified string: e.g. `grep error time_logs.txt`.
* **Piping (`|`)** sends the standard output of one command as input to another: e.g. `ls /home/analyst/reports | grep users`.
* `find` locates files and directories matching criteria: `-name` (case-sensitive) / `-iname` (case-insensitive) with `*` as a wildcard, and `-mtime` for modification time (`-mtime -3` = modified within the past three days; `-mmin` for minutes).

**Commands used:**
```bash
# Task 1: Navigate to logs and find error messages
cd /home/analyst/logs
grep error server_logs.txt

# Task 2: Find files by name in the users reports
cd /home/analyst/reports/users
ls | grep Q1
ls | grep access

# Task 3: Search inside user files
ls
grep jhill Q2_deleted_users.txt
grep "Human Resources" Q4_added_users.txt
```

*Ref 5: Filtering logs and user files with grep and piping*

<img width="600" height="300" alt="grep and piping used to filter server logs and user files" src="https://github.com/user-attachments/assets/349f6a4d-5fcf-4eb5-898a-78dcfbb2e6a6" />

📹 **Solution recording:** https://screenrec.com/share/J52VAg0ySB

---

## Lab 5: Create and Modify Directories and Files

**Key commands:** `mkdir` (create directory), `rmdir` (remove empty directory: fails if the directory contains files or subdirectories), `touch` (create file), `rm` (remove file), `mv` (move/rename), `cp` (copy without deleting the original), and `nano` (command-line editor: `Ctrl+O` to save, `Ctrl+X` to exit; Vim and Emacs are common alternatives).

**Output redirection:** `>` overwrites a file's contents while `>>` appends to it: both create the file if it doesn't exist. `>` should be used carefully, since overwritten files are not easy to recover. Example: `echo "last updated date" >> permissions.txt` appends the string; a subsequent `echo "time" > permissions.txt` would overwrite the entire file.

**Commands used:**
```bash
cd /home/analyst
mkdir logs
ls
rmdir temp
ls
cd notes
mv Q3patches.txt /home/analyst/reports/
ls /home/analyst/reports
rm tempnotes.txt
ls
touch tasks.txt
ls
nano tasks.txt
clear
cat tasks.txt
```

*Ref 6: Creating and removing directories*

<img width="600" height="300" alt="mkdir and rmdir operations" src="https://github.com/user-attachments/assets/036570a3-cd88-48b3-b6f1-df9f0a38651c" />

*Ref 7: Moving and removing files*

<img width="600" height="300" alt="Moving Q3patches.txt and removing tempnotes.txt" src="https://github.com/user-attachments/assets/75d28327-5ac6-4fde-a274-843df7525eb7" />

*Ref 8: Creating and editing tasks.txt with nano*

<img width="600" height="400" alt="Creating tasks.txt with touch and editing it in nano" src="https://github.com/user-attachments/assets/3f099c6d-1acc-4852-a92c-d706868eba9d" />

## Lab 6: File Permissions and the Principle of Least Privilege

**Inspecting permissions:** `ls -l` displays permissions plus owner, group, file size, and last modification time; `ls -a` includes hidden files; `ls -la` combines both.

**Changing permissions with `chmod` (symbolic notation):**

| Character | Description |
|-----------|-------------|
| `u` | changes user (owner) permissions |
| `g` | changes group permissions |
| `o` | changes other permissions |
| `+` | adds permissions |
| `-` | removes permissions |
| `=` | assigns permissions exactly as specified |

Examples: `chmod u+rwx,g+rwx,o+rwx login_sessions.txt` grants all permissions; `chmod u-rwx,g-rwx,o-rwx login_sessions.txt` removes them all; `chmod u=r,g=r,o=r login_sessions.txt` sets read-only for everyone. Changes for multiple owner types are separated by commas with no spaces.

**Least privilege in action:** a confidential `bonuses.txt` file owned by `hrrep1` showed permissions `-rw-rw----`: the group had read and write access it didn't need. Running `chmod g-rw bonuses.txt` restricted access to only the user whose job requires it.

**Commands used:**
```bash
cd /home/researcher2/projects
ls -l
ls -la
chmod o-w project_k.txt
ls -l
chmod g-r project_m.txt
ls -la
chmod u-w,g-w,g+r .project_x.txt
ls -l
chmod g-x drafts
```

*Ref 9: Inspecting permissions with ls -l and ls -la*

<img width="600" height="300" alt="Inspecting file permissions including hidden files" src="https://github.com/user-attachments/assets/f83c879c-6fac-4621-a013-a4f6644cca26" />

*Ref 10: Applying least privilege with chmod, including a hidden file and a directory*

<img width="600" height="300" alt="chmod changes on project files, hidden file, and drafts directory" src="https://github.com/user-attachments/assets/c75782c5-d08e-4623-ae17-ca554ae98745" />

📄 **Lab documentation:** [Google Doc link](https://docs.google.com/document/d/1_Q_kvpvsM3_3I_7wUoIm-hGY-Z-ubaTtlArWlz-0bqE/edit?usp=sharing)


## Lab 7: Add, Modify, and Delete Users

**Key concepts:**
* The **root user** (superuser) holds special privileges; `sudo` provides controlled access to root-level actions.
* `useradd` creates users: `-g` sets the primary group (e.g. `sudo useradd -g security fgarcia`), `-G` adds supplemental groups (e.g. `sudo useradd -G finance,admin fgarcia`).
* `usermod` modifies existing users: `-g` changes the primary group; `-a -G` appends supplemental groups (omitting `-a` would *replace* existing supplemental groups). Other options: `-d` (home directory), `-l` (login name), `-L` (lock account).
* `chown` changes ownership: `sudo chown fgarcia access.txt` for the user owner, `sudo chown :security access.txt` for the group owner (note the colon).
* `userdel` deletes a user; `groupdel` deletes a group.

**Commands used:**
```bash
sudo useradd researcher9
sudo usermod -g research_team researcher9
sudo chown researcher9 /home/researcher2/projects/project_r.txt
sudo usermod -a -G sales_team researcher9
sudo userdel researcher9
sudo groupdel researcher9
```

*Ref 11: Full user lifecycle: create, assign groups, transfer ownership, delete*

<img width="600" height="300" alt="User administration lifecycle with useradd, usermod, chown, userdel" src="https://github.com/user-attachments/assets/db5d9ac4-acdd-4a37-ad03-e7d22afdf400" />


## Lab 8: Get Help in the Shell

**Resources:** `man` displays the manual ("man page") for a command; `whatis` gives a one-line description (e.g. `whatis tail`); `apropos` searches man pages by keyword when you don't know which command to look up: `-a` narrows results to entries matching all keywords (e.g. `apropos -a create new group`).

**Commands used:**
```bash
whatis cat
man cat
apropos -a first part file
man useradd
whatis rm
whatis rmdir
apropos -a create new group
```

*Ref 12: Using whatis and man to look up commands*

<img width="600" height="300" alt="whatis and man output for core commands" src="https://github.com/user-attachments/assets/ac0eeeca-7b6a-415f-b3ce-b20e3fd7812a" />

*Ref 13: Discovering commands by keyword with apropos*

<img width="600" height="300" alt="apropos keyword search results" src="https://github.com/user-attachments/assets/2ff45c3a-423f-456c-be0b-8ee5752c7f53" />


## Conclusion

* Package managers like APT make installing security tooling repeatable and verifiable: always confirm state with `apt list --installed` or by invoking the tool.
* `grep`, piping, and `find` turn raw log directories into answerable questions: the foundation of log analysis before any SIEM is involved.
* `>` vs `>>` is a small distinction with big consequences: one careless `>` can destroy a log or config file.
* Permissions review (`ls -la`) plus targeted `chmod` changes is the practical, command-line application of the principle of least privilege.
* `usermod -a -G` versus `usermod -G` is a classic pitfall: forgetting `-a` silently strips a user's existing supplemental groups.
