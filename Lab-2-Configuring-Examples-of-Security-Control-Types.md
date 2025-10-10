# Lab 2: Configuring Examples of Security Control Types

## Objective
Demonstrate the configuration and testing of preventative, detective and corrective security controls, applying them 
within a Windows Server environment to strengthen organisational security posture.
This activity is designed to test your understanding of and ability to apply content examples in the following CompTIA 
Security+ objectives:
* 1.1 Compare and contrast various types of security controls


## Overview
I operated from PC10 (Windows Server 2019), serving as a client in the lab environment to perform and validate configurations of security controls. Each 
section demonstrated a real-world application of the control type and showed how to test the effectiveness of those 
controls through practical means


## Configure and test preventative controls
A preventative control is designed to prevent unwanted actions before they happen.

#### Steps taken
1. I logged into PC10 as Sam, a non-admin user
2. Navigated to ``\\10.1.16.1\TOOLS`` to test access to the directory
3. Sam was able to access the folder contents, this was not expected as Sam is not an administrator and should not have access
   <img width="1146" height="536" alt="image" src="https://github.com/user-attachments/assets/2d101217-b67a-40db-a3e2-b03fdced26bc" />
4. I then logged into DC10 as Administrator and navigated to Server Manager > File and Storage Services > Shares
<img width="1540" height="1094" alt="image" src="https://github.com/user-attachments/assets/82dfe344-5610-47c2-95eb-848327141ad5" />
5. Located the TOOLS share > Right-clicked > Properties > Permissions tab > Customised permissions

6. Removed the 'Users' group from the access control list (ACL) to restrict access to only ``Domain Admins`` and ``LocalAdmin`` 
<img width="1537" height="1094" alt="image" src="https://github.com/user-attachments/assets/3db76097-9c03-4fe4-9fa9-4424bb745c6c" />
<img width="1535" height="1094" alt="image" src="https://github.com/user-attachments/assets/5e1ee80c-4375-4a88-9752-d63e24c3a4b3" />

7. I went back to login as Sam and verified the control by reattempting to access teh directory. This time, access was denied, resulting in a network error message popping up.

Sam's unintended access to TOOLS was a vulnerability that could lead to unauthorised data exposure. The preventive control restricted this 
successfully.
In this situation, we’re looking at a security issue involving user access permissions, which is a critical part of following proper procedures within any cybersecurity framework (CSF) or broader information security practice.
What happened here is that Sam, a user in the system, was able to access a folder or file that he shouldn’t have had permission to see. The file was located in a shared network folder `\10.1.16.1\TOOLS`, and somehow the 
permissions were misconfigured, allowing Sam to view its contents under the ``TOOLS`` directory.

This kind of access, when not properly controlled, introduces a security vulnerability. From the perspective of a security analyst or system administrator, the goal in this task was to remove or restrict Sam’s access so he could no
longer see or interact with that file.
This scenario highlights how important it is to stay on top of access controls and ensure only authorized users have permission to view or modify sensitive data.
When I navigated to the TOOLS directory as Jaime, I was able to access it because Jaime is a member of the LocalAdmin security group.
<img width="799" height="309" alt="image" src="https://github.com/user-attachments/assets/335724a9-6c14-4350-b226-c7caada6f130" />


## Configure and test detective controls

#### Steps Taken
1. Logged in as Jamie (admin) and navigated to ``LABFILES`` > Deleted ``empty`` folder
2. Opened Event Viewer > Windows Logs > Security, used 'Find' to search for ``empty`` and no results were found. This goes to show that the
deletion was not being audited.
Through 'find' we're trying to verify the file we deleted is no longer present, since that's the goal for this part of the scenario.
Once we deleted that folder, it stopped showing up in the Event Logs to be audited. Now that it's been fully removed from the system, we're no longer
able to find it.
<img width="1540" height="1065" alt="image" src="https://github.com/user-attachments/assets/51e4cbf6-d1b2-40ec-b603-3533aa7221a8" />
3. Opened Local Security Policy > Audit Policy > Audit object access > Enabled Success and Failure audit logging

<img width="1175" height="844" alt="image" src="https://github.com/user-attachments/assets/fc949442-01fb-4bfa-8b7c-149d7708e335" />

After selecting the Success/Failure options, it gets reflected under the Security Setting column
<img width="1174" height="845" alt="image" src="https://github.com/user-attachments/assets/3b0fc8ec-8dff-4b7f-abba-4b4e561711dd" />

4. Configured object-level auditing
   * Right-clicked ``LABFILES`` > Properties > Security > Advanced > Auditing > Add
   * Set Principal to ``Everyone`` > Show advanced permissionis > Checked ``Delete subfolders and files`` and ``Delete``
<img width="1373" height="887" alt="image" src="https://github.com/user-attachments/assets/fef93ab0-2ff4-432e-9913-e7afb52c4d26" />

   * Applied to all child objects
5. Deleted the pcaps folder to trigger logging
6. Refreshed Event Viewer, searched for Event ID 4660 (object deletion) and 4663 (access details)


<img width="1253" height="986" alt="image" src="https://github.com/user-attachments/assets/99c48fae-4cff-4f0b-ba3d-200615f45353" />

When reviewing the Event Viewer, I searched for Event ID 4660, which is tied to object deletion. I had to refresh the logs a 
couple times before the event appeared. Once found, I noted the Record ID which gives detailed info about the specific event.
This confirmed that the file I had deleted earlier in the lab was properly logged. The event showed all relevant process detils, 
verifying that the deletion action was successfully recorded.

<img width="1539" height="1096" alt="image" src="https://github.com/user-attachments/assets/b8a4ee0d-b3df-4902-9578-2f37a9a3b365" />

Security tab
<img width="1533" height="1055" alt="image" src="https://github.com/user-attachments/assets/96e1dde8-1013-49b1-8e5c-8b39947f247a" />



<img width="1541" height="1000" alt="image" src="https://github.com/user-attachments/assets/e2ef2b98-3b9c-4848-9d03-836cf5e884d6" />
In the Event Record > Details pane, you get more specific information. This is useful because it shows what logs have been captured, 
even for previously deleted files, and helps you stay updated. Event Log Viewer is a great tool for this because it gives you the 
record that shows teh file was deleted and that the audit was successful.
This showcases exactly what kind of activity occurred with the file. At its core, the purpose of a detective control is to 
create a record of events and activities, just like we see in this scenario. When you're trying to find certain records, 
this helps maintain integrity and non-repudiation of the evidence.
<img width="926" height="680" alt="image" src="https://github.com/user-attachments/assets/89b112b0-c400-4f32-bd2a-a6bf7cce451a" />

## Configure and test directive controls

Directive controls guide user behaviour by outlining policies and acceptable use

#### Steps Taken:
1. Logged in as Jaime, opened PowerShell as admin
2. Entered a script to set a login banner containing Acceptable Use Policy (AUP) and legal warnings

<img width="1290" height="357" alt="image" src="https://github.com/user-attachments/assets/ea5a0b89-3a2d-4477-b34a-b5b3f4dc16b7" />
What is being done is writing a PowerShell script to display a disclaimer notice, basically part of the Acceptable Use Policy (AUP). What you see on the screen is the kind of 
message a company would show to users when they log in.
It lays out the rules of acceptable behaviour within an organisation, letting employees know what's allowed and what isn't, along with the 
consequences involved if someone chooses to break those rules. This kind of messaging is important, especially for larger instituional or 
business environments. It helps with business protection, but also supports accountability and legal liability in the event that something goes wrong.
This PowerShell script displays an "Authorised Use Only" message, reminding users they're expected to use the system resposibly. That 
banner is a key way companies inform employees and enforce compliance. It helps make sure the Acceptable Use Policy is clearly communicated and upheld 
across the organisation.

<img width="885" height="470" alt="image" src="https://github.com/user-attachments/assets/6818ceb5-f1c5-4750-bf5e-ab5bb177ad02" />


The goal of directive controls is making sure employees are compliant. Directive controls are to measure the complaince for business accountability
and legal frameworks to make sure people are held responsible for their actions. Negligence can lead to a massive threat, which can ultimately lead to long-term effects of failure. 

This banner functions as both a deterrent and legal safeguard, reinforcing organisational compliance and accountability

## Configure and test corrective controls
Corrective controls respond to incidents by restoring systems to a secure state

#### Steps taken:
1. Used Sysinternals > notmyfault64.eve to simulate a system crash via Code Overwrite, forcing a particular execution phase where
the computer enters a Blue Screen of Death where the computer is no longer going to be operated for a period of time

<img width="581" height="437" alt="image" src="https://github.com/user-attachments/assets/9ae81a73-13f1-41ab-9e06-e28b84aa672a" />

<img width="519" height="672" alt="image" src="https://github.com/user-attachments/assets/7224fbc2-6e0c-4a20-87cd-e4bff92d1047" />

<img width="1508" height="719" alt="image" src="https://github.com/user-attachments/assets/94f77a08-b318-463f-89c8-e7caa7e181ec" />

2. Demonstrated Windows' built-in corrective mechanism to maintain execution integrity

**Creation of a corrective control**
* Opened PowerShell > Created a file ``notes.txt`` containing the phrase "This is important"
* Generated a SHA256 hash of the file and saved it in ``hash.txt``
* Verified file hash integrity
* Simulated tampering: ``echo blah >> notes.txt``
* Verified mismatch triggered corrective action
* Restored original content and verified hash match again

<img width="1284" height="639" alt="image" src="https://github.com/user-attachments/assets/ef862a9a-c3d2-4887-92d8-eef50845c6d1" />

3. Automation Scripts
   * Created ``calchash.ps1`` to recalculate hash
   * Created ``check.ps1`` to monitor file changes and restore contents if altered
   * Validated script execution, content restoration, and integrity check


Notepad: calchash.ps1 
<img width="1279" height="284" alt="image" src="https://github.com/user-attachments/assets/6ba9fe17-98a8-4546-a766-faa897708b99" />

Creation of a new file
<img width="644" height="499" alt="image" src="https://github.com/user-attachments/assets/9080f764-02ac-4ba6-ac0d-57a5cf471f2a" />

Dual purpose of corrective controls:
* Return the system to a normal and generally secure condition
* Address an unwanted or less secure state or event

They’re not just about fixing software problems, they’re about recognizing when something has gone wrong and stepping in to fix it.
That could be anything from a vulnerable application to a configuration that leaves the system exposed.
The key idea is responsibility. If you’re not regularly checking for vulnerabilities, you’re leaving the door open for attackers to exploit weaknesses. 
Once a system has been compromised, it’s much harder to regain control. That’s where corrective controls step in to reduce the damage and restore order.

### TROUBLESHOOTING
I had encountered an issue where upon checking my progress I received a note saying that task was incomplete, my files were not saving in the correct directory. I realised that I was in the wrong directory and that 
the files were meant to be written under Jaime's. 
<img width="614" height="398" alt="image" src="https://github.com/user-attachments/assets/5dc1ca2c-1415-4bc3-8c0e-85fcdcd4a366" />

I still chose to proceed to avoid time loss on the VM and later manually copied the files into Jaime's directory to align with the task requirements
<img width="657" height="112" alt="image" src="https://github.com/user-attachments/assets/a134be21-cb95-44bd-80a4-ed44384ac173" />

I checked my score again after fixing the file paths and the tasks validated correctly this time around.

<img width="631" height="419" alt="image" src="https://github.com/user-attachments/assets/860606cb-92fa-4a84-9cb2-c40cf965d670" />

<img width="622" height="546" alt="image" src="https://github.com/user-attachments/assets/38f994d5-d119-4224-ac70-0a988b1ac2c8" />

<img width="314" height="151" alt="image" src="https://github.com/user-attachments/assets/5d631c54-5e71-480f-848c-b8d98294a4e4" />

<img width="615" height="299" alt="image" src="https://github.com/user-attachments/assets/f8f75bb3-0213-4c7f-9c5b-55335506ae37" />

## LAB RESULTS
<img width="1418" height="391" alt="image" src="https://github.com/user-attachments/assets/76ad9040-c849-4fb0-b68f-480daf916e55" />

## My Final Thoughts
This lab was structured in a really great way that allowed for the reinforcing of the practical application of layered
security control types. Each control type, whether blocking access, logging activity, instructing users, or remediating threats plays a 
vital role in protecting systems. The combination of manual and automated configurations built a strong foundation for understanding 
how to security an enterprise environment.

## Key Takeaways

* **Preventive Controls** stop unauthorized access before it happens.
* **Detective Controls** log critical actions to support audits and investigations.
* **Directive Controls** inform users of responsibilities and compliance expectations.
* **Corrective Controls** return the system to a secure state post-incident.
* **Hashing** is a reliable way to monitor and validate file integrity.
* Attention to detail, like correct directory targeting, is essential in scripting and validation.
* Event Viewer, PowerShell, and auditing configurations are core tools for system hardening and incident response.
