# User Management in Linux

## Project Description

In this project, I simulated a real-world IT administration workflow where a new employee, `researcher9`, joins an organization and must be properly onboarded, granted appropriate file access, assigned to additional teams, and eventually removed from the system upon departure.

By managing user accounts through the Linux command line, the organization can maintain stronger access control through the principle of least privilege — ensuring each user has exactly the access they need, no more and no less.

To complete this task, I performed the following activities:

- Added a new user to the Linux system
- Assigned the user to a primary group
- Transferred file ownership to the new user
- Added the user to a secondary group
- Deleted the user and cleaned up the associated group

---

# Task 1 — Add a New User

A new employee has joined the Research department. The first step is to add them to the system under the username `researcher9`, and then assign them to their primary group `research_team`.

## Step 1.1 — Create the User

The following command creates a new user account named `researcher9`:

```bash
sudo useradd researcher9
```

## Step 1.2 — Assign a Primary Group

After creating the user, I used `usermod` with the `-g` option to assign `research_team` as their primary group:

```bash
sudo usermod -g research_team researcher9
```

> **Note:** The `-g` option (lowercase) sets the **primary group**, which is the default group assigned to files the user creates.

The screenshot below confirms both commands were executed successfully:

![Image](https://github.com/Kimmus521/Linux-Fundamentals/blob/d9119d2d489d190f6d18621381664bb37747d4f5/Images/p2_screenshot-1.png)

---

# Task 2 — Assign File Ownership

The new employee, `researcher9`, will be taking responsibility for a specific project file. In this task, I transferred ownership of `project_r.txt` from the original owner (`researcher2`) to `researcher9`.

## Step 2.1 — Navigate to the Project Directory

I first navigated to the directory where the project file is located and confirmed the file exists using `ls`:

```bash
cd /home/researcher2/projects
ls
```

The output shows `project_r.txt` is present in that directory.

## Step 2.2 — Change File Ownership

I then used the `chown` command to transfer ownership:

```bash
sudo chown researcher9 /home/researcher2/projects/project_r.txt
```

> **Note:** `chown` stands for *change ownership*. It requires `sudo` because you are modifying ownership of a file that belongs to another user.

The screenshot below confirms the ownership transfer was completed:

![Assign File Ownership](images/screenshot_2.png)

---

# Task 3 — Add the User to a Secondary Group

Several months later, `researcher9`'s role has expanded — they are now working across both the Research and Sales departments. Their primary group remains `research_team`, but they must also be added to `sales_team` as a secondary (supplementary) group.

## Step 3.1 — Add to Supplementary Group

I used `usermod` with the `-a` and `-G` options to append the new group without removing the existing primary group:

```bash
sudo usermod -a -G sales_team researcher9
```

> **Important:** Always use `-a` (append) together with `-G` when adding a secondary group. Using `-G` alone **replaces** all current supplementary groups. The `-a` flag ensures the new group is **added** rather than substituted.
>
> Also note that Linux options are case-sensitive: `-a` is lowercase and `-G` is uppercase — they must be used exactly as shown.

The screenshot below confirms `researcher9` was successfully added to `sales_team`:

![Add Secondary Group](images/screenshot_3.png)

---

# Task 4 — Delete a User

After a year, `researcher9` has left the organization. In this task, I removed their account from the system and cleaned up the group that was automatically created when their account was added.

## Step 4.1 — Delete the User Account

The following command removes the user from the system:

```bash
sudo userdel researcher9
```

After running this command, the terminal displayed the following message:

```
userdel: group researcher9 not removed because it is not the primary group of user researcher9.
```

> **This message is expected behavior.** When a new user is created in Linux, the system automatically creates a group with the same name as the user. Since `researcher9`'s primary group was set to `research_team` (not `researcher9`), the auto-created group `researcher9` was not deleted automatically.

## Step 4.2 — Delete the Orphaned Group

As a best practice, empty or unused groups should be removed after a user deletion. I cleaned up the leftover group using:

```bash
sudo groupdel researcher9
```

The screenshot below shows both commands executed, including the system message from `userdel`:

![Delete User and Group](images/screenshot_4.png)

---

# Summary

In this project, I walked through the full lifecycle of a Linux user account — from creation to deletion — using core command-line tools. Each task reflected a realistic IT administration scenario that a system administrator or cloud engineer would encounter in a professional environment.

The workflow included:

1. Creating a new user with `useradd` and assigning a primary group with `usermod -g`
2. Transferring file ownership with `chown`
3. Appending a secondary group with `usermod -a -G`
4. Removing a user with `userdel` and cleaning up the empty group with `groupdel`

This project demonstrates practical Linux administration skills related to:

- User account management
- Group membership and access control
- File ownership management
- System cleanup and housekeeping
- Linux command-line operations

---

# What I Learned

## Linux Commands Practiced

### Create a New User
```bash
sudo useradd researcher9
```

### Modify User's Primary Group
```bash
sudo usermod -g research_team researcher9
```

### Change File Ownership
```bash
sudo chown researcher9 /home/researcher2/projects/project_r.txt
```

### Add User to a Secondary Group
```bash
sudo usermod -a -G sales_team researcher9
```

### Delete a User
```bash
sudo userdel researcher9
```

### Delete an Empty Group
```bash
sudo groupdel researcher9
```

---

## Key Concepts and Skills Developed

- Understanding the difference between **primary groups** (`-g`) and **secondary/supplementary groups** (`-G`)
- Applying the **principle of least privilege** by granting users only the access they need
- Using `chown` to manage **file ownership** across user accounts
- Recognizing that Linux automatically creates a **default group** for each new user, and that good practice includes cleaning it up after deletion
- Safely **appending** supplementary groups with `-a -G` to avoid accidental removal of existing memberships

---

# Technologies Used

- Linux
- Bash
- Linux Terminal
- User and Group Management (`useradd`, `usermod`, `userdel`, `groupdel`)
- File Ownership Management (`chown`)
- Command-Line Interface (CLI)

---

# Author

## Haeun Kim

Computing Infrastructure and Network Engineering Technology Student at Purdue University

Interested in:
- Cloud Engineering
- Linux Infrastructure
- Networking
- Cybersecurity
- DevOps
