<img width="877" alt="Screenshot 2025-03-16 at 12 45 29 AM" src="https://github.com/user-attachments/assets/752b4095-a906-4cb9-82dc-f389632bd3a7" /># Overview: Lab 14 Delegate Control and Account Lockout Management
This repository documents the setup and configuration of a home lab environment dedicated to studying "Delegate Control and Account Lockout Management." The focus of this lab is to explore best practices for managing user permissions and account lockout policies in an Active Directory (AD) environment.

## Objectives
- Delegate Control: Implementing and testing delegation of administrative privileges in an AD environment to different users or groups, ensuring least privilege access.
- Account Lockout Management: Configuring and testing account lockout policies to secure accounts from brute-force attacks while ensuring proper exception handling.

## Documentation
In this home lab, we will focus on understanding Delegation Control and Account Lockout. Delegation involves granting a user limited access through Active Directory. To begin, we will create a new user in Active Directory Users and Computers on our Windows Server 2022 VM.

<br> 

<img width="877" alt="Screenshot 2025-03-16 at 12 42 49 AM" src="https://github.com/user-attachments/assets/dbd499d4-3e8e-4d29-bed3-ac58dcc2cf39" />

<br> 

1.We will create a user named Andrew for both the First and Last Name, and his login username will also be Andrew.

<br> 
<img width="877" alt="Screenshot 2025-03-16 at 12 43 38 AM" src="https://github.com/user-attachments/assets/a9ca87fb-1d6f-47e6-ba20-8e2ca95b9f67" />
<br> 

2. After creating the user Andrew, we will create a new Organizational Unit (OU). Right-click on the domain tobifash.com, select New → Organizational Unit, and name it Consultants. Then, drag Andrew into the newly created Consultants OU and click Yes to confirm.

<br> 

<img width="877" alt="Screenshot 2025-03-16 at 12 45 29 AM" src="https://github.com/user-attachments/assets/2d846875-db87-41cb-bfc7-5e1acfd8d486" />
<br> 

3. Next right click on the domain SimoTech.com and select “Delegate Control”

<br> 

<img width="877" alt="Screenshot 2025-03-16 at 12 45 52 AM" src="https://github.com/user-attachments/assets/43281eec-c2fb-4b3b-bbd3-05f411d8626e" />

<br> 

4. Then add “Andrew”.

<br> 

<img width="877" alt="Screenshot 2025-03-16 at 12 46 09 AM" src="https://github.com/user-attachments/assets/d8b1bd2a-27b4-4848-87a3-a38b3df14894" />

<br>  

5. Will only give Andrew the permission to reset passwords for other users. Check mark “Reset user passwords and force password change at next logon”. Then select “Next” then “Finish”.

<br> 

![image](https://github.com/user-attachments/assets/bdcd7c09-0f4b-4fe0-bed8-cb05c69dbaae)
<br> 

6. Now that the setup is complete, let's log in as Andrew on our Windows 10 VM. Open Active Directory Users and Computers. To verify the actions available to Andrew, search for the user Bob, right-click on his account, and select Properties. Then, go to the Account tab. Under Account options, you'll notice that everything is grayed out except for the option User must change password at next logon.

<br> 

![Screenshot 2025-03-16 at 12 57 38 AM](https://github.com/user-attachments/assets/5b431ee8-61a9-41c7-9377-54d7f03739f5)

<br> 

7. To verify further, let's right-click on Bob and select Reset Password. This will prompt us to reset Bob's password.

Next, let's lock out Andrew's account. Use the Input button at the top of the VM, select Keyboard → Insert Alt + Ctrl + Del, then choose Lock. This will intentionally lock Andrew's account.


<br> 

![image](https://github.com/user-attachments/assets/d8c99a23-6185-4a14-89e4-a8e097193ef5)

<br> 

8. To investigate a user account that has been locked out, we can use a tool from Microsoft called the Account Lockout and Management Tools. We can download it from Microsoft’s website at this [link](https://www.microsoft.com/en-ca/download/details.aspx?id=18465). After downloading, we’ll move the file into our SimoTech Lab folder, which is shared with our Windows Server 2022 VM.

<br> 

<img width="990" alt="Screenshot 2025-03-16 at 1 09 38 AM" src="https://github.com/user-attachments/assets/481ef0b7-7848-4b3a-b3c5-28daa903ae7f" />

<br> 

9. Next, we need to enable shared folders on our Windows Server 2022 VM. Right-click on the folder icon at the bottom and select Share Folder Settings. For the Folder Path, locate the SimoTech Lab folder in our Downloads directory. Check the box for Auto-mount and click OK.

<br> 

<img width="990" alt="Screenshot 2025-03-16 at 1 11 34 AM" src="https://github.com/user-attachments/assets/72f3f692-bc0f-4e3c-8e16-b8f7d4525ea0" />

<br> 

10. The Tobifash Lab folder should now appear as our Z: drive. Open the Z: drive, then locate and open the Account Lockout and Management Tools application. Run the tool to begin the investigation.

<br> 

<img width="855" alt="Screenshot 2025-03-16 at 1 13 16 AM" src="https://github.com/user-attachments/assets/6c51b0ce-9a8c-42c0-a82d-84f4ea60db4c" />

<br> 

11. For extraction location, choose the Documents and select “OK”.

<br>

<img width="855" alt="Screenshot 2025-03-16 at 1 14 41 AM" src="https://github.com/user-attachments/assets/99ef41ba-e31b-405b-a8de-bfc8a6983c60" />

<br> 

12. In Documents, open the LockoutStatus application. This tool is designed to analyze and manage account lockouts in Active Directory environments. It's especially useful in large or complex networks where account lockouts may be caused by issues such as misconfigured applications, password synchronization problems, or unauthorized access attempts.

<br> 

![image](https://github.com/user-attachments/assets/65f39eb4-7199-4125-ba3a-dc0875f4bb22)

<br> 

13. Navigate to File in the top-left corner and select Select Target. Enter Andrew as the target user and click OK. This will display the User State, which shows that the account is currently locked due to 4 bad password attempts. It also provides key details, including the time of the last password attempt, the date the password was last set, the domain or origin of the lockout, and the lockout timestamp.

<br> 

![image](https://github.com/user-attachments/assets/f320b61d-b5db-409f-a3e4-f8ebb7f633b8)

<br> 

14. ![image](https://github.com/user-attachments/assets/ecedf05e-f70c-4615-bc79-0425c91140b9)

<br> 

15. Now that we’ve confirmed Andrew’s account is locked, we can fix it by following these steps:

  1. Open Active Directory Users and Computers.

  2. Search for Andrew in the Consultants organizational unit (OU).

  3. Right-click on Andrew and select Properties.

  4. Go to the Account tab and check the box for Unlock account.

  5. Click Apply to unlock the account.

  <br> 
<img width="748" alt="Screenshot 2025-03-16 at 1 35 24 AM" src="https://github.com/user-attachments/assets/ffef2c42-b151-4373-84fb-dcc9be45f10e" />

<br> 

16. Now we can have Andrew sign back into his account.

<br> 

![image](https://github.com/user-attachments/assets/8ad634ec-a9a1-419a-83ad-2dee58af0489)

<br> 

17. ![image](https://github.com/user-attachments/assets/a9071c0d-0379-4179-aa35-d0a66ce3957a)

<br> 

18. If we run the Bobby application again and search for Andrew, the results will show that the account is no longer locked.

<br> 

![image](https://github.com/user-attachments/assets/b6c12a68-a9ef-4cc0-9cb3-6342fd402812)

19. Congratulations! We have successfully completed the final home lab, gaining a thorough understanding of Delegation Control and how to investigate an account lockout using Microsoft’s Account Lockout and Management Tools.

