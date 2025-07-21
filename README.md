# Administering Users in Linux

## Ticket
![Linux Ticket](https://github.com/Judeorabueze/Administering-Users-in-Linux/blob/main/Linux%20Ticket.PNG)

## Introduction
This project was carried out in direct response to Help Desk Ticket #4561290, which requested administrative action on a Linux system. The ticket required the creation of two new user accounts on an Ubuntu Linux host, configuration of secure password policies, and implementation of strict folder access controls.

As the assigned system administrator, I personally executed all required steps on a virtualized Ubuntu 22.04 LTS environment. The project aimed to demonstrate practical skills in user management, permission assignment, and securing sensitive directories in a multi-user environment. The actions performed ensured that only the specified users — Bertram and Erlich — had access to a newly created folder, while all other system users were restricted, fulfilling the principle of least privilege.

## Objectives
- Create two new user accounts: <b>bertram</b> and <b>erlich</b>
- Assign temporary passwords and enforce password change on first login
- Create a secure folder <b>Confidential</b> in the root directory
- Ensure root remains the folder owner with full rights
- Grant full access only to the two users
- Restrict all other system users from accessing the folder

## Tools and Technologies Used

| Tool/Command              | Purpose                                        |
| ------------------------- | ---------------------------------------------- |
| `useradd`, `passwd`       | User creation and password assignment          |
| `chage`                   | Force password change at first login           |
| `mkdir`, `chown`, `chmod` | Directory creation and ownership configuration |
| `setfacl`, `getfacl`      | Fine-grained access control                    |
| `sudo`                    | Privileged command execution                   |
| Ubuntu 22.04 LTS          | OS environment                                 |
