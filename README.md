<h1> Active Directory Password Change with Delegation</h1>

<h2>Description</h2>
This project exemplifies the utilization of delegation within Active Directory to reset a user password. Additionally, we employ PowerShell to force a password reset, prompting the user to create a new password upon logging in with the temporary password provided.


<h2>Tools and Languages Utilized</h2>
<ul>
  <li>Active directory </li><br>
  <li>PowerShell</li>
</ul>


<h2>Program walk-through:</h2>

In numerous organizations, the sheer volume of employees often prompts the engagement of IT companies to oversee network management. Routine tasks such as resource allocation, password adjustments, and account locking are typically handled by the IT team through Active Directory. One method employed for this purpose is known as <ins>Delegation.</ins> Delegation involves granting specific users elevated privileges within Active Directory to carry out designated tasks. Let's delve into this further.
<br>
<br>

<h3><ins>Step 1</h3>
  <ul>
<li>After accessing Active Directory, we are presented with a page resembling the one depicted below.</h5></li><br>

</ul>
<p align="center">
<img src="https://files.catbox.moe/cg25cg.png" height="80%" width="80%" alt="OU modification"/>
</p>
<h3><ins>Step 2</h3>
    <ul>
<li>On the left side, we find the Organizational Units (OUs), allowing us to choose the unit we wish to explore and view the users associated with it. In this case, we will focus on the IT OU and its corresponding users: Claire, Mary, and Phillip.</h5></li><br>
  </ul>
<p align="center">
<img src="https://files.catbox.moe/tzx9tl.png" height="80%" width="80%" alt="OU modification"/>
</p>
<h3><ins>Step 3</h3>
    <ul>
<li>As noted earlier, delegation can be assigned to any user within this OU. In this instance, we will grant Phillip delegation authority over the Sales OU. Put simply, this means we are endowing Phillip with the privilege to reset passwords for all individuals within the Sales department, who include the following:</h5></li><br>
  </ul>
<p align="center">
<img src="https://github.com/Salrocks/ActiveDirectoryPasswordChangewithDelegation/blob/main/3.png" height="80%" width="80%" alt="OU modification"/>
</p>
<h3><ins>Step 4</h3>
    <ul>
<li>Now, to grant Phillip this privilege, we will right-click on the Sales OU and select 'Delegate Control'."</li><br>
  </ul>
<p align="center">
<img src="https://github.com/Salrocks/ActiveDirectoryPasswordChangewithDelegation/blob/main/4.png" height="80%" width="80%" alt="OU modification"/>
</p>
<h3><ins>Step 5</h3>
    <ul>
<li>After clicking this, a new tab will be open which looks like this: </li><br>
  </ul>
<p align="center">
<img src="https://github.com/Salrocks/ActiveDirectoryPasswordChangewithDelegation/blob/main/5.png" height="80%" width="80%" alt="OU modification"/>
</p>
<h3><ins>Step 6</h3>
    <ul>
<li>After clicking 'Next', we will encounter a screen similar to the one below. Then, we'll proceed to click the 'Add' button to include Phillip in the designated box.</li><br>
  </ul>
<p align="center">
<img src="https://github.com/Salrocks/ActiveDirectoryPasswordChangewithDelegation/blob/main/6.png" height="80%" width="80%" alt="OU modification"/>
</p>
<h3><ins>Step 7</h3>
    <ul>
<li>After clicking 'Add', a tab similar to this will appear. In the lower box, we will type the name of the user to whom we want to grant delegation. Once the name is entered, it's crucial to CLICK 'Check Names' to prompt Active Directory to search for the specific user. This step helps prevent misspellings of the user's name. Once the desired user is located, we click 'OK'.</li><br>
  </ul>
<p align="center">
<img src="https://github.com/Salrocks/ActiveDirectoryPasswordChangewithDelegation/blob/main/7.png" height="80%" width="80%" alt="OU modification"/>
</p>
<h3><ins>Step 8</h3>
    <ul>
<li>We will then see the following screen, simply press “next”. </li><br>
  </ul>
<p align="center">
<img src="https://github.com/Salrocks/ActiveDirectoryPasswordChangewithDelegation/blob/main/8.png" height="80%" width="80%" alt="OU modification"/>
</p>
<h3><ins>Step 9</h3>
    <ul>
<li>Upon clicking 'Next', the following options will be displayed. As shown in the image below, various special privileges can be granted to Phillip. However, as we are solely providing him with the privilege to reset passwords, we will select the second box. After this selection, continue to press 'Next' until you are returned to the Active Directory screen.</li><br></ul>
<p align="center">
<img src="https://github.com/Salrocks/ActiveDirectoryPasswordChangewithDelegation/blob/main/9.png" height="80%" width="80%" alt="OU modification"/>
</p>
<h3><ins>Step 10</h3>
    <ul>
<li>Now that we have granted Phillip the necessary privileges, let's put it to the test using PowerShell. In this example, we will reset Sophie's password, who is a user in the Sales OU. To begin, open PowerShell and navigate to the user Phillip, as demonstrated below."</li><br></ul>
<p align="center">
<img src="https://github.com/Salrocks/ActiveDirectoryPasswordChangewithDelegation/blob/main/10.png" height="80%" width="80%" alt="OU modification"/>
</p>
<h3><ins>Step 11</h3>
    <ul>
<li>In power shell we will run the command: <br>
<br>
  
    Set-ADAccountPassword sophie -Reset -NewPassword (Read-Host -AsSecureString -Prompt 'New Password') -Verbose) 
  
as shown below. After running this command we will be prompted with a “ new password.” This new password will be the temporary password we will assign to Sophie. </li></ul>
<p align="center">
<img src="https://github.com/Salrocks/ActiveDirectoryPasswordChangewithDelegation/blob/main/11.png" height="80%" width="80%" alt="OU modification"/>
</p>
<h3><ins>Step 12</h3>
    <ul>
<li>After typing in the temporary password, we will run another command that will force reset the temporary password. In other words, after Sophie logs in with the temporary password we have provided, she will have to create a new password before continuing. To do this, we run the command: </li> <br></ul>

      Set-ADUser -ChangePasswordAtLogon $true -Identity sophie -Verbose <br>

<br>

<p align="center">
<img src="https://github.com/Salrocks/ActiveDirectoryPasswordChangewithDelegation/blob/main/12.png" height="80%" width="80%" alt="Delegations"/>
</p>
<h3><ins>Step 13</h3>
    <ul>
<li>After completing these steps, we can verify that Sophie will need to reset her password by attempting to log into her account. As illustrated below, upon using the temporary password, we are directed to the password reset page.</li><br></ul>
<p align="center">
<img src="https://github.com/Salrocks/ActiveDirectoryPasswordChangewithDelegation/blob/main/13.png" height="80%" width="80%" alt="OU modification"/>
</p>

</ul>


