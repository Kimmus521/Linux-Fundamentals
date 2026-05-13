# File Permissions in Linux

## Project Description

The research team in my organization needed to modify permissions for certain files in the `projects` directory. By adjusting permissions appropriately, the organization could maintain stronger file security through the principle of least privilege.

To complete this task, I performed the following activities:

- Checked existing file and directory permissions
- Interpreted Linux permission strings
- Modified file permissions using `chmod`
- Updated hidden file permissions
- Restricted directory access permissions

---

# Check File and Directory Details

The following command was used to determine the existing permissions for each file and directory.

```bash
ls -la
```

The command lists all files in the directory, including hidden files, along with detailed permission information. The output displays:

- A `drafts` directory
- A hidden `.project_x.txt` file
- Several project files

The 10-character string at the beginning of each line represents the permissions assigned to the file or directory.

![image alt](https://github.com/Kimmus521/Linux-Fundamentals/blob/228dfad113e04e72ae52cdcc3f50c50f4693a58b/Images/check_file_and_directory.png)

---

# Understanding the Permission String

The Linux permission string identifies:

- File type
- User permissions
- Group permissions
- Other permissions

## Permission Structure

| Position | Meaning |
|---|---|
| 1st Character | File type (`d` for directory, `-` for regular file) |
| 2nd–4th Characters | User permissions (`r`, `w`, `x`) |
| 5th–7th Characters | Group permissions (`r`, `w`, `x`) |
| 8th–10th Characters | Other permissions (`r`, `w`, `x`) |

If a hyphen (`-`) appears, that permission is not granted.

### Example

```text
-rw-rw-r--
```

This means:

- User: read and write
- Group: read and write
- Others: read only

No one has execute permissions.

---

# Change File Permissions

The organization decided that others should not have write access to any project files.

To remove write permissions for others, I used the following Linux command:

```bash
chmod o-w project_k.txt
```

After applying the permission change, I verified the update using:

```bash
ls -la
```

![image alt](https://github.com/Kimmus521/Linux-Fundamentals/blob/2bc4ed202cd1afcb0c320792ee1af04dbc7b0502/Images/change_file_permissions.png)

---

# Change Permissions on a Hidden File

The organization archived `.project_x.txt` and wanted:

- No write access for anyone
- Read access for both the user and group

To achieve this, I modified the permissions using:

```bash
chmod u-w,g-w,g+r .project_x.txt
```

Finally, I verified the updated permissions using:

```bash
ls -la
```

![image alt](https://github.com/Kimmus521/Linux-Fundamentals/blob/fe43f952a58a7e52ecfbc8ab348ad54d407d9ad8/Images/change_file_permissions_hidden.png)

---

# Change Directory Permissions

The organization required that only the `researcher2` user should have access to the `drafts` directory and its contents.

This meant that no other users should retain execute permissions.

I updated the directory permissions using `chmod` and verified the changes afterward.

![image alt](https://github.com/Kimmus521/Linux-Fundamentals/blob/a5ca7761913f1326c2c9d7445c0996b592bd7b27/Images/change_directory_permissions.png)

The output confirms that only `researcher2` has read, write, and execute permissions for the `drafts` directory.

---

# Summary

In this project, I modified Linux file and directory permissions to align with organizational security requirements.

The workflow included:

1. Using `ls -la` to inspect existing permissions
2. Using `chmod` to add or remove permissions
3. Verifying all changes after modification

This project demonstrates practical Linux administration skills related to:

- File security
- Permission management
- Access control
- Linux command-line operations

---

# What I Learned

## Linux Commands Practiced

### Check Permissions
```bash
ls -la
```

### Modify Permissions
```bash
chmod
```

---

## Key Skills Developed

- Understanding Linux permission structures
- Managing user, group, and other access levels
- Applying the principle of least privilege
- Using terminal commands for system administration
- Interpreting Linux directory listings

---

# Technologies Used

- Linux
- Bash
- Linux Terminal
- File Permission Management
- Command-Line Interface (CLI)

---

# Author

## Haeun Kim

Computing Infrastructure and Network Engineering Technology Student

Interested in:
- Cloud Engineering
- Linux Infrastructure
- Networking
- Cybersecurity
- DevOps
