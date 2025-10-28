| Command                          | Description                                                            |
| -------------------------------- | ---------------------------------------------------------------------- |
| `useradd <user>`                 | Add a new user (non-interactive, low-level).                           |
| `adduser <user>`                 | Add a new user interactively (Debian/Ubuntu wrapper around `useradd`). |
| `usermod -l <newname> <oldname>` | Rename a user account.                                                 |
| `usermod -d /new/home <user>`    | Change the user’s home directory.                                      |
| `usermod -s /bin/bash <user>`    | Change the user’s default shell.                                       |
| `usermod -aG <group> <user>`     | Add a user to a supplementary group.                                   |
| `usermod -L <user>`              | Lock a user account (disable login).                                   |
| `usermod -U <user>`              | Unlock a user account.                                                 |
| `userdel <user>`                 | Delete a user account (keeps home directory by default).               |
| `userdel -r <user>`              | Delete a user **and** remove their home directory & mail spool.        |
| `passwd <user>`                  | Set or change a user’s password.                                       |
| `passwd -l <user>`               | Lock the user’s password (disable password login).                     |
| `passwd -u <user>`               | Unlock the user’s password.                                            |
| `chage -l <user>`                | Show password aging info (expiry date, etc.).                          |
| `chage -E <date> <user>`         | Set account expiration date.                                           |
| `chfn <user>`                    | Change user’s full name or finger information.                         |
| `id <user>`                      | Display user ID (UID), group ID (GID), and groups.                     |
| `whoami`                         | Show the current logged-in username.                                   |
| `su - <user>`                    | Switch to another user account (load environment).                     |
| `sudo -i -u <user>`              | Start an interactive shell as another user.                            |
| `last`                           | Show last login history.                                               |

Group Management Commands
| Command                             | Description                                                     |
| ----------------------------------- | --------------------------------------------------------------- |
| `groupadd <group>`                  | Create a new group.                                             |
| `addgroup <group>`                  | Interactive group creation (Debian/Ubuntu wrapper).             |
| `groupdel <group>`                  | Delete a group.                                                 |
| `groupmod -n <newgroup> <oldgroup>` | Rename a group.                                                 |
| `groups <user>`                     | Show the groups a user belongs to.                              |
| `gpasswd -a <user> <group>`         | Add a user to a group.                                          |
| `gpasswd -d <user> <group>`         | Remove a user from a group.                                     |
| `gpasswd <group>`                   | Set or change group password / manage group admins.             |
| `newgrp <group>`                    | Switch to a different group temporarily in the current session. |
| `getent group`                      | Display all groups (from `/etc/group` or directory service).    |

System Files Related to User & Group Management
| File              | Description                                             |
| ----------------- | ------------------------------------------------------- |
| `/etc/passwd`     | Stores user account info (UID, GID, home, shell, etc.). |
| `/etc/shadow`     | Stores encrypted passwords and password aging info.     |
| `/etc/group`      | Stores group info and group memberships.                |
| `/etc/gshadow`    | Stores secure group account information.                |
| `/etc/skel/`      | Default files copied to a new user’s home directory.    |
| `/etc/login.defs` | Default user and password configuration.                |

Bonus Utilities
| Command         | Description                                   |
| --------------- | --------------------------------------------- |
| `finger <user>` | Display detailed user info (if installed).    |
| `who`           | Show who is currently logged in.              |
| `w`             | Show logged-in users and what they are doing. |
| `lastlog`       | Show last login for all users.                |
| `getent passwd` | Display all system users.                     |
| `getent group`  | Display all system groups.                    |




# User Management in Linux

## Introduction to User Management in Linux
Linux is a multi-user operating system, meaning multiple users can operate on a system simultaneously. Proper user management ensures security, controlled access, and system integrity. 

Key files involved in user management:
- `/etc/passwd` – Stores user account details.
- `/etc/shadow` – Stores encrypted user passwords.
- `/etc/group` – Stores group information.
- `/etc/gshadow` – Stores secure group details.

## Creating Users in Linux
To create a new user in Linux, use:

### `useradd` Command (For most Linux distributions)
```bash
useradd username
```
This creates a user without a home directory.

To create a user with a home directory:
```bash
useradd -m username
```

To specify a shell:
```bash
useradd -s /bin/bash username
```

### `adduser` Command (For Debian-based systems)
```bash
adduser username
```
This is an interactive command that asks for a password and additional details.

## Managing User Passwords
To set or change a user’s password:
```bash
passwd username
```

### Enforcing Password Policies
- **Password expiration**: Set password expiry days
  ```bash
  chage -M 90 username
  ```
- **Lock a user account**
  ```bash
  passwd -l username
  ```
- **Unlock a user account**
  ```bash
  passwd -u username
  ```

## Modifying Users
Modify an existing user with `usermod`:
- Change the username:
  ```bash
  usermod -l new_username old_username
  ```
- Change the home directory:
  ```bash
  usermod -d /new/home/directory -m username
  ```
- Change the default shell:
  ```bash
  usermod -s /bin/zsh username
  ```

## Deleting Users
To remove a user but keep their home directory:
```bash
userdel username
```
To remove a user and their home directory:
```bash
userdel -r username
```

## Working with Groups
### Creating Groups
```bash
groupadd groupname
```

### Adding Users to Groups
```bash
usermod -aG groupname username
```

### Viewing Group Memberships
```bash
groups username
```

### Changing Primary Group
```bash
usermod -g new_primary_group username
```

## Sudo Access and Privilege Escalation
### Adding a User to Sudo Group
On Debian-based systems:
```bash
usermod -aG sudo username
```
On RHEL-based systems:
```bash
usermod -aG wheel username
```

### Granting Specific Commands with Sudo
Edit the sudoers file:
```bash
visudo
```
Then add:
```bash
username ALL=(ALL) NOPASSWD: /path/to/command
```
