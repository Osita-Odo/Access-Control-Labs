# Onboarding a User to Passwordless Sign-in with a Temporary Access Pass and Passkey

**Microsoft Entra ID · Temporary Access Pass (TAP) and passkey registration · TerraCyb Consulting**

## Project Summary

This project demonstrates how to onboard a user to passwordless authentication in Microsoft Entra ID by issuing a Temporary Access Pass (TAP) and using it to register a passkey. Working as an administrator in the Microsoft Entra admin centre, a time-limited, one-time access code is generated for a user (Chucks Eze) so that he can sign in for the first time without a password. He then uses that code at the Microsoft security information portal to authenticate and set up a passkey as his ongoing sign-in method.

The walkthrough covers the full lifecycle. On the administrator side, it locates the user and their authentication methods in the admin centre, adds a Temporary Access Pass with a set duration (one hour) and one-time use, and shares the generated code with the user. On the user side, it follows Chucks as he signs in with his user principal name (ending in the TerraCyb Consulting domain) and the provided code, selects a passkey option, verifies device ownership, names the passkey, and finally signs in with a device-specific passkey PIN. The result is a user who can sign in securely with a passkey rather than a password. If the session times out before setup is complete, a fresh code must be issued by the administrator.

## Tools Used

- Microsoft Entra ID (the identity and access management service, formerly Azure Active Directory).
- Microsoft Entra admin centre, used to manage the user and add authentication methods.
- Microsoft security information portal ([https://aka.ms/mysecurityinfo](https://aka.ms/mysecurityinfo)), used by the end user to sign in and register a passkey.
- Temporary Access Pass (TAP), a time-limited, one-time passcode for first sign-in.
- Passkey (FIDO2) authentication as the ongoing passwordless sign-in method.
- A web browser (Microsoft Edge and Google Chrome) and Google Password Manager for storing the passkey on the device.
- Windows Security (Windows Hello) PIN and a mobile device screen lock for identity verification.

---

## Part 1 (Administrator): Generate a Temporary Access Pass

**Open the user in the Entra admin centre:** Signed in as an administrator, go to Entra ID > Users > All users. Find the user, Chucks Eze, and click on the user's name rather than ticking the box beside it. This opens the user's own page.

<img width="850" height="470" alt="image" src="https://github.com/user-attachments/assets/acd41885-9f99-4459-86fa-6572b3a833d1" />


**Open the user's authentication methods:** On Chucks Eze's page, select Authentication methods from the menu on the lower left.

<img width="847" height="475" alt="image" src="https://github.com/user-attachments/assets/f2ef8790-94d7-42a0-9306-e4f55fc93b73" />


**Add an authentication method:** On the Authentication methods page, select Add authentication method from the top.

<img width="841" height="475" alt="image" src="https://github.com/user-attachments/assets/b72f4ef8-f2c5-4818-abb9-fe0dc1bb3679" />


**Choose Temporary Access Pass:** In the Add authentication method panel that appears, choose Temporary Access Pass from the Choose method list.

<img width="847" height="465" alt="image" src="https://github.com/user-attachments/assets/9568e3ac-97dc-4b6f-8d7e-66d65d441bd2" />


**Set the duration and create the pass:** Set the activation duration, one hour in this case. One-time use is already set to Yes. Then select Add.

<img width="855" height="461" alt="image" src="https://github.com/user-attachments/assets/08b2002b-cbac-4872-90ff-fe6614c05006" />


**Copy the generated pass:** A Temporary Access Pass is generated so that Chucks can sign in. The code is `DWDG$*cn` and the sign-in website is [https://aka.ms/mysecurityinfo](https://aka.ms/mysecurityinfo). This code is given to Chucks to sign in.

<img width="847" height="475" alt="image" src="https://github.com/user-attachments/assets/b04d4569-96fb-457a-839b-a38d99858b5d" />


---

## Part 2 (User): Sign in with the Temporary Access Pass

**Find the user principal name:** Chucks needs his user principal name, which ends with the TerraCyb Consulting domain. It can be copied from the Users list.

<img width="846" height="471" alt="image" src="https://github.com/user-attachments/assets/fece26ad-2e63-44ab-a332-6a6dc37dc721" />


**Start the sign-in:** Going to [https://aka.ms/mysecurityinfo](https://aka.ms/mysecurityinfo), Chucks is prompted to sign in and enters his user principal name.

<img width="835" height="470" alt="image" src="https://github.com/user-attachments/assets/f212563e-e0c1-49e7-b164-98ae1aab1969" />


**Enter the Temporary Access Pass:** On the next page, Chucks enters the Temporary Access Pass provided by the administrator: `DWDG$*cn`.

<img width="835" height="453" alt="image" src="https://github.com/user-attachments/assets/8f1c8523-f598-4719-95e0-c26f7d65ab03" />


**Skip saving the password and staying signed in:** After signing in, the browser may offer to save the login details, but this is not necessary. Chucks can also choose not to stay signed in.

<img width="838" height="465" alt="image" src="https://github.com/user-attachments/assets/fa47b6e3-943d-46fc-a01e-4890c6829ff3" />


---

## Part 3 (User): Register a passkey

**Add a sign-in method:** On the Security info page, Chucks can now set up a permanent sign-in method, since the provided code was for one-time use. Select Add sign-in method. Note: if the process ends because of a session time-out (the page left open for a long time without activity), the administrator must generate another code.

<img width="840" height="472" alt="image" src="https://github.com/user-attachments/assets/7e2167f5-df5e-471e-abad-097fe177ac6c" />


**Choose the passkey option:** Two sign-in options are shown. The second option, Passkey, is selected here, because the Microsoft Authenticator app is not being used.

<img width="837" height="421" alt="image" src="https://github.com/user-attachments/assets/a8d63a31-ae0b-45ed-b7c0-76bc52366e50" />


**Continue past the prompt:** Follow the prompt to sign in faster with your face, fingerprint or PIN, and select Next.

<img width="835" height="447" alt="image" src="https://github.com/user-attachments/assets/41235264-4d62-43a5-84c6-05a3307e8572" />


**Verify device ownership:** Verify that you are the owner of the device you are using to sign in. Here the passkey is saved to Google Password Manager, so Chucks confirms it is him.

<img width="837" height="471" alt="image" src="https://github.com/user-attachments/assets/ea155c97-21bb-44b9-b869-d8ec28aa53b6" />

**Enter the device screen lock:** Enter the screen lock for the selected device to access the encrypted data and confirm your identity.

<img width="848" height="467" alt="image" src="https://github.com/user-attachments/assets/ccea50f2-b7cc-44e6-9688-40519ef271d2" />


**Name the passkey:** After verification, you are prompted to name the passkey to help identify it later, for example "Chucks work account".

<img width="835" height="466" alt="image" src="https://github.com/user-attachments/assets/8d03be06-4990-4d09-a204-60bb2bb8a2e0" />


**Passkey created:** The passkey is now set and can be used by Chucks to sign in next time.

<img width="832" height="470" alt="image" src="https://github.com/user-attachments/assets/06cff9f9-fd44-44aa-ac06-393ed168e776" />


---

## Part 4 (User): Sign in with the passkey

**Choose passkey sign-in:** If Chucks signs out after setting up the passkey, he is prompted to sign in with his account details, [eze@terracybconsulting.onmicrosoft.com](mailto:eze@terracybconsulting.onmicrosoft.com). Instead of a password, he selects "Use your face, fingerprint, PIN or security key instead".

<img width="837" height="476" alt="image" src="https://github.com/user-attachments/assets/be1d8117-099e-4206-9ffe-95665371c3f6" />


**Enter the passkey PIN:** Chucks is then required to enter the passkey PIN for the specific device he is using, which completes the passwordless sign-in.

<img width="833" height="481" alt="image" src="https://github.com/user-attachments/assets/b22d7ee3-a419-4472-9b84-3ca3289ab2ef" />


---

## Outcome

The user is onboarded to passwordless sign-in. A one-time Temporary Access Pass allowed a secure first sign-in without a password, and from that session a passkey was registered as the ongoing method. Chucks can now sign in with a passkey protected by a device PIN, and the administrator retains control by issuing a new pass if setup does not complete in time.
