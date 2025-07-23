# Administering Users in Linux

## Ticket
![Linux Ticket](https://github.com/Judeorabueze/Administering-Users-in-Linux/blob/main/Linux%20Ticket.PNG)

## Introduction
This project was carried out in direct response to Help Desk Ticket #4561290, which requested administrative action on a Linux system. The ticket required the creation of two new user accounts on an Ubuntu Linux host, configuration of secure password policies, and implementation of strict folder access controls.

As the assigned system administrator, I personally executed all required steps on a virtualized Ubuntu 22.04 LTS environment. The project aimed to demonstrate practical skills in user management, permission assignment, and securing sensitive directories in a multi-user environment. The actions performed ensured that only the specified users — Bertram and Erlich — had access to a newly created folder, while all other system users were restricted, fulfilling the principle of least privilege.

## Objectives
- Create two new user accounts: <b>Bertram</b> and <b>Erlich</b>
- Assign temporary passwords and enforce password change on first login
- Create a secure folder <b>Confidential</b> in the root directory
- Ensure root remains the folder owner with full rights
- Grant full access only to the two users
- Restrict all other system users from accessing the folder

## Tools and Technologies Used

| Tool/Command              | Purpose                                             |
| ------------------------- | ----------------------------------------------      |
| `adduser`, `passwd`       | User creation and password assignment               |
| `passwrd --expire`        | Expire password and force change at first login     |
| `su`                      | Switch user                                         |
| `ls`                      | List contents of a directory                        |
| `mkdir`, `chown`, `chmod` | Directory creation and ownership configuration      |
| `addgroup` , `chgrp`      | Add group , Change group                            |
| `usermod -a -G`           | Add user to a group                                 |  
| `sudo`                    | Privileged command execution                        |
| Ubuntu 22.04 LTS          | OS environment                                      |

## Project Approach

### 1. User Creation
- #### Add the Users Bertram and Erlich
  - I added the user <b>Bertram</b> using the command - `sudo adduser bertram`
  - The user <b>Erlich</b> was added using - `sudo adduser erlich`

    (For each user, I was prompted to enter a password. I set a temporary password for both users, knowing they would be required to change it upon their first login.

    During the process, I was asked to provide optional details such as Full Name, Room Number, etc. I chose to leave these fields blank by pressing Enter to skip them.)

![Bertram](https://github.com/Judeorabueze/Administering-Users-in-Linux/blob/main/bertram%202.PNG)

### 2. Enforce Password Change at First Login
- Expired Bertram's password using - `sudo passwd --expire bertram`
- Expired Erlich's password using - `sudo passwd --expire erlich`

![expire password](https://github.com/Judeorabueze/Administering-Users-in-Linux/blob/main/password%20expire.PNG)

#### To check if the above actions were successfull:
- I switched the users (Bertram and Erlich).
  - Entered `su bertram `to switch to user <b>bertram</b>
  - Entered `su erlich `to switch to user <b>erlich</b>
  
  ![su bertram](https://github.com/Judeorabueze/Administering-Users-in-Linux/blob/main/su%20bertram.PNG)

  From the screenshot above, the forced password change was sucessfully enforced

### 3. Create a Folder "Confidential' in the Root Directory
- Entered `sudo mkdir Confidential`
- Used `ls` to list the content of the root directory
  
![confidential](https://github.com/Judeorabueze/Administering-Users-in-Linux/blob/main/confidential%20directory.PNG)

(From the screenshot above, the folder <b>"Confidential"</b> was successfully created)

### 4. Check and Set Folder Ownership and Permissions
- Entered `ls -l` to display list of files, folders, and their respective ownerships and permissions

![ls -l](https://github.com/Judeorabueze/Administering-Users-in-Linux/blob/main/ls-l.PNG)

The screenshot above shows that:
  - <b>Confidential</b> file type is <b>directory</b> (see <b>d</b>rwx ...)
  - File ownership was <b>root</b> with <b>full permission</b> - read (r), write (w) and execute (x) permissions. (See the first set of permission - <b>rwx</b>)
  - Permissions set for <b>group (root)</b> - read (r) and execute (x) (See the second set of permissions - <b>r_x</b>). The group has no permission to <b>write</b> in the file.
  - Permission for everyone or others - read (r) and execute (x) (See the third set of permissions - <b>r_x</b>). <b>Others</b> have no permission to <b>write</b> in the file.

### 5 Fix Users (bertram and erlich) Permissions
- Added a new group named <b>"congroup"</b> using `sudo addgroup congroup`
- Added the users (bertram and erlich) to the <b>"congroup"</b>- `sudo usermod -a -G congroup bertram` and `sudo usermod -a -G erlich`
- Changed the file group from <b>"root"</b> to <b>"congroup"</b> - `sudo chgrp congroup Confidential`
- Used `ls -l` to check ownerships and permissions

![change group](https://github.com/Judeorabueze/Administering-Users-in-Linux/blob/main/change%20group.PNG)

From the screenshot above, the group was successfully changed to <b>congroup</b>.

- Set the group permissions such that both the file owner and the users (bertram and erlich) now in congroup group have full permissions while other have no permission
  - Enter `sudo chmod 770 Confidential`
  - And `ls -l` to confirm the updated permissions.
 
![final](https://github.com/Judeorabueze/Administering-Users-in-Linux/blob/main/Final.PNG)

From the above screenshot, the permissions have been successfully set and the ticket resolved.
