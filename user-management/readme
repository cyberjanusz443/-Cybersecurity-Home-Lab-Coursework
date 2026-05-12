# 02 — User Management & Access Control

Implemented role-based access control on both Linux and Windows
using the same scenario: a fictional company with three roles
(employee, manager, guest) and a shared directory structure.

## What I did
- **Linux (Ubuntu):** Created `/company/{employees,management,archive,public}`
  with three users and proper group membership. Set directory permissions
  using `chmod` and `chown` to enforce least privilege.
- **Windows 11:** Built the same `C:\company\` structure with NTFS ACLs
  configured via Properties → Security tab, demonstrating identical
  authorization logic across both operating systems.
- Verified that `employee` can write only to their own directory and `public`,
  `manager` has access to `management`, and `guest` is denied access to both.

## Key screenshots
- `strukturafolderowsenior.jpg` — Linux directory tree with `ls -la /company`
  showing distinct group ownership per folder
- `testdostepuemployee.jpg` — Successful access test as `employee` user
- `testbrakudostepuguest.jpg` — `Permission denied` for `guest` attempting
  to write to `/company/management`
- `strukturafolderowCcompany.jpg` — Windows NTFS permissions for the same
  structure with named users and Authenticated Users group

## Takeaway
The principle of least privilege is universal — only the implementation differs
between operating systems. Once you understand POSIX permissions, NTFS ACLs
become straightforward.
