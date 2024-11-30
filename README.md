<h1>Overview: Lab 6 Common Active Directory Issues, CMD Commands, PC Offline</h1>

This section of my home lab documentation explores **common Active Directory issues**, troubleshooting with **CMD commands**, and resolving situations where a **PC is offline** in a domain environment. The project provides practical solutions for addressing common problems that administrators face when working with Active Directory, such as authentication failures, group policy application issues, and troubleshooting offline PCs.

<h2>Objectives</h2>

- Identify and resolve **common Active Directory issues**, such as login problems and account lockouts.
- Use **CMD commands** to troubleshoot and resolve issues related to domain connectivity, account authentication, and more.
- Handle scenarios where a **PC is offline** from the domain, including troubleshooting network connectivity and domain membership.
- Understand how to diagnose and repair issues using Active Directory logs, CMD commands, and network tools.



<h2>Documentation</h2>

In this home lab, we will explore common Active Directory issues users might encounter, then use CMD commands to resolve PC offline problems.

Let's begin with some CMD commands. On the local user account **Bob**, open **Command Prompt** and type `ping 12.1.10.2`. This is the IP address of our **Windows Server 2022** machine. This command will confirm that **Desktop2** can communicate with the server. Now, let's repeat the process on the **Server** by pinging **Desktop2** to verify the connection from the server side.




1. <p align="center">
   <img src="https://i.imgur.com/GyDA6gv.png" height="100%" width="100%" alt="Disk Sanitization Steps 1"/>
   <br />
   <br />
</p>

Now on our Windows Server 2022, when we ping 12.1.10.4 (local user Bob), we can see that the connection timed out. This is because the firewall on that account is preventing the ping, so we would need to disable it. To do that, open up Windows Defender Firewall → Turn off Windows Defender Firewall on or off.

2. <p align="center">
   <img src="https://i.imgur.com/NxcdWtd.png" height="100%" width="100%" alt="Disk Sanitization Steps 2"/>
   <br />
   <br />
</p>

Use the Helpdesk administrative login to access Windows Defender Firewall, then turn off all of the options. Afterward, select OK to apply the changes.

3. <p align="center">
   <img src="https://i.imgur.com/j3T0aXA.png" height="100%" width="100%" alt="Disk Sanitization Steps 3"/>
   <br />
   <br />
</p>

Now lets run the command line again on our Windows Server 2022. 

4. <p align="center">
   <img src="https://i.imgur.com/WKSaner.png" height="100%" width="100%" alt="Disk Sanitization Steps 4"/>
   <br />
   <br />
</p>

If we add the -t option to our ping command, such as ping 12.1.10.4 -t, it will continue running indefinitely until manually stopped. This allows us to monitor network connectivity and observe any changes in packet loss over time. The ping will automatically stop if the Desktop2 PC is shut down or restarted.

5. <p align="center">
   <img src="https://i.imgur.com/cKMGUl9.png" height="100%" width="100%" alt="Disk Sanitization Steps 5"/>
   <br />
   <br />
</p>

Next, on the local user Bob, run Command Prompt as an administrator using the Helpdesk administrative login. Then, type gpresult /r > c:\results.txt. This command will generate a group policy report for the PC and save it as a text file in the C: drive.


6. <p align="center">
   <img src="https://i.imgur.com/u2kRBAq.png" height="100%" width="100%" alt="Disk Sanitization Steps 6"/>
   <br />
   <br />
</p>

s

7. <p align="center">
   <img src="https://i.imgur.com/bpiKnH2.png" height="100%" width="100%" alt="Disk Sanitization Steps 7"/>
   <br />
   <br />
</p>

If we do not run it in administrative then the command line will deny us access.

8. <p align="center">
   <img src="https://i.imgur.com/2JOfirK.png" height="100%" width="100%" alt="Disk Sanitization Steps 8"/>
   <br />
   <br />
</p>

Some additional command lines such as gpupdate /help will provide a list of available options for the gpupdate command.


9. <p align="center">
   <img src="https://i.imgur.com/qRCCSik.png" height="100%" width="100%" alt="Disk Sanitization Steps 9"/>
   <br />
   <br />
</p>

Gpresult /? will display a list of available options for the command.

10. <p align="center">
   <img src="https://i.imgur.com/xjxgdeP.png" height="100%" width="100%" alt="Disk Sanitization Steps 10"/>
   <br />
   <br />
</p>

Gpresult /r  displays the result of the Group Policy for the current user and computer.

11. <p align="center">
   <img src="https://i.imgur.com/iPLZw4m.png" height="100%" width="100%" alt="Disk Sanitization Steps 11"/>
   <br />
   <br />
</p>

Next, let's explore some common issues that Helpdesk teams may encounter when assisting users, such as when a user account becomes locked out. To test this, we will sign out of Bob and purposely lock his account by putting the incorrect password. 

12. <p align="center">
   <img src="https://i.imgur.com/XvmmuIM.png" height="100%" width="100%" alt="Disk Sanitization Steps 12"/>
   <br />
   <br />
</p>

In this scenario when a user is locked out and is calling the helpdesk or admins for help, typically they would access the Active Directory Users and Computers → search for the user then unlock it from there. Lets try this out on our Helpdesk account. Open up Active Directory Users and Computers  → right-click on the domain SimoTech.com and search up Bob, make sure that the entire directory is selected. Once Bob is found, double click on his name and select “Account” then select “Unlock Account”. then press “Apply” then “OK”. Now Bob can log into his account successfully.

13. <p align="center">
   <img src="https://i.imgur.com/R1zDz6i.png" height="100%" width="100%" alt="Disk Sanitization Steps 13"/>
   <br />
   <br />
</p>

Bob should be able to log in now once his account is unlocked. 

14. <p align="center">
   <img src="https://i.imgur.com/O9yPw8c.png" height="100%" width="100%" alt="Disk Sanitization Steps 14"/>
   <br />
   <br />
</p>

Now let’s create an issue where Bob’s account is disabled for some reason and that he forgot his password. Let’s intentionally disable Bob’s account by clicking on his account again in Active Directory Users and Computers on the Helpdesk machine.

15. <p align="center">
   <img src="https://i.imgur.com/tDYHsWR.png" height="100%" width="100%" alt="Disk Sanitization Steps 15"/>
   <br />
   <br />
</p>

Now let’s imagine a scenario where Bob’s account is disabled for some reason, and he does not remember his password. As a helpdesk, we can look up Bob’s user in Active Directory Users and Computers using the Find command on the domain → select Entire Directory and search for Bob → right-click on his name and select Enable Account.

16. <p align="center">
   <img src="https://i.imgur.com/x8v60sL.png" height="100%" width="100%" alt="Disk Sanitization Steps 16"/>
   <br />
   <br />
</p>



17. <p align="center">
   <img src="https://i.imgur.com/FJAhP7t.png" height="100%" width="100%" alt="Disk Sanitization Steps 17"/>
   <br />
   <br />
</p>

Since Bob has forgotten his password, we can provide him with a temporary password that will allow him to log in and change it to his own password upon his next login. To do this, right-click on Bob and select Reset Password. Ensure that the User must change password at next logon option is enabled.

18. <p align="center">
   <img src="https://i.imgur.com/xuU9c8i.png" height="100%" width="100%" alt="Disk Sanitization Steps 18"/>
   <br />
   <br />
</p>



19. <p align="center">
   <img src="https://i.imgur.com/PBrCVjS.png" height="100%" width="100%" alt="Disk Sanitization Steps 19"/>
   <br />
   <br />
</p>



20. <p align="center">
   <img src="https://i.imgur.com/Xib53H2.png" height="100%" width="100%" alt="Disk Sanitization Steps 20"/>
   <br />
   <br />
</p>

Now, let’s create a scenario where **Bob’s** account is expired due to inactivity or because an administrator has set an expiration date for the account. To do this:

1. Select **Bob** in **Active Directory Users and Computers**.
2. Click on the **Account** tab.
3. Under **Account expires**, select **End of** and choose a date that has already passed.

21. <p align="center">
   <img src="https://i.imgur.com/BF9AT1Q.png" height="100%" width="100%" alt="Disk Sanitization Steps 21"/>
   <br />
   <br />
</p>


22. <p align="center">
   <img src="https://i.imgur.com/XgfSsWg.png" height="100%" width="100%" alt="Disk Sanitization Steps 22"/>
   <br />
   <br />
</p>

To resolve this, the Helpdesk account would need to go to Active Directory Users and Computers → search for Bob using the Find function in the domain → select Entire Directory → open Bob’s account → go to the Account tab, then select Never under Account expires.

23. <p align="center">
   <img src="https://i.imgur.com/3ZuYaxf.png" height="100%" width="100%" alt="Disk Sanitization Steps 23"/>
   <br />
   <br />
</p>

To make sure Bob’s account is valid, open Command Prompt on the Helpdesk account and type net user Bob /domain. This will verify that the account is active and should allow Bob to log in.


24. <p align="center">
   <img src="https://i.imgur.com/4L8kN16.png" height="100%" width="100%" alt="Disk Sanitization Steps 24"/>
   <br />
   <br />
</p>

Let’s create an issue where the computer has fallen off the domain. On the Helpdesk account in Active Directory Users and Computers → select Computers → right-click on the computer and select Disable Account.

25. <p align="center">
   <img src="https://i.imgur.com/LZ6Q49u.png" height="100%" width="100%" alt="Disk Sanitization Steps 25"/>
   <br />
   <br />
</p>

Lets use our Helpdesk account to login into desktop2. It should give us an error.

26. <p align="center">
   <img src="https://i.imgur.com/pRtJS91.png" height="100%" width="100%" alt="Disk Sanitization Steps 26"/>
   <br />
   <br />
</p>

When a computer is fallen off from a domain, we can sometimes fix it by going to Active Directory Users and Computers and selecting that computer (Desktop2) and enabling it. We can log in back into our accounts now.

27. <p align="center">
   <img src="https://i.imgur.com/sGlybnU.png" height="100%" width="100%" alt="Disk Sanitization Steps 27"/>
   <br />
   <br />
</p>


Now let’s try a different way of making the computer fall off the domain. We will delete **Desktop2** from the domain. In **Active Directory Users and Computers** on the **Helpdesk** account, select **Computers**, then right-click and delete **Desktop2**.

Next, let’s create a new user: go to **Users**, right-click, and select **New** → **User**. Use **First/Last Name** and set the **User logon** as **Test**, then click **Finish**.

Now, attempt to log in to **Desktop2** using the **Test** account. An error should appear indicating that the computer is no longer part of the domain.

28. <p align="center">
   <img src="https://i.imgur.com/bQMMvZu.png" height="100%" width="100%" alt="Disk Sanitization Steps 28"/>
   <br />
   <br />
</p>

To add Desktop2 back into our Computers domain, we need to log into our domain as administrator to do that type “.\administrator” and enter your password.

29. <p align="center">
   <img src="https://i.imgur.com/WtiZlzL.png" height="100%" width="100%" alt="Disk Sanitization Steps 29"/>
   <br />
   <br />
</p>

Next, go into File Explorer → right-click on This PC → select Properties → click on Rename this PC (Advanced) → select Change → under Member of, change it to Workgroup. Then, restart the computer.


30. <p align="center">
   <img src="https://i.imgur.com/4hyOaRk.png" height="100%" width="100%" alt="Disk Sanitization Steps 30"/>
   <br />
   <br />
</p>

Log in as **Administrator** and repeat the process to add the computer back to the domain. Go to **File Explorer** → right-click on **This PC** → select **Properties** → click on **Rename this PC (Advanced)** → select **Change**, then add it back to the domain as **SimoTech.com**. Proceed with a restart.

Now, go back to the **Helpdesk** account in **Active Directory Users and Computers**, and under **Computers**, you should see **Desktop2** is back in the domain.


31. <p align="center">
   <img src="https://i.imgur.com/vyZyjxH.png" height="100%" width="100%" alt="Disk Sanitization Steps 31"/>
   <br />
   <br />
</p>


Congratulations! We have successfully addressed several common Active Directory issues, utilized CMD commands effectively, and resolved PC offline scenarios. 

 👉 [Next Lab 7 : Security Groups, Mapped Drives, Personal Drives](https://github.com/melvinensahsl/Security-Groups-Mapped-Drives-Personal-Drives)
