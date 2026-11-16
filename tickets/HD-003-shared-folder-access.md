# HD-003 — Department shared folder access

**Scenario:** HR needs a network folder that HR employees can edit but Sales employees cannot access.

## Objective

Apply role-based access with an AD security group and both SMB share and NTFS permissions.

## Procedure

1. Create `GG_HR_Shared_RW`, a **Global Security** group in the HR OU.
2. Add Sofia Costa, Mariana Lopes, and Carolina Sousa as members.
3. On HD-DC01, create `C:\Company Shares\HR` and a fictional `HR-Test.txt`.
4. Share the folder as `HR`: HR group **Change + Read**, Administrators **Full Control**; remove broad Everyone access to the share.
5. On the HR folder's NTFS ACL, grant HR group **Modify**, preserving **SYSTEM** and **Administrators** Full Control; remove unnecessary broad entries.
6. From HD-PC01, verify `\\HD-DC01\HR` opens and is editable when logged in as Sofia, and is denied to Miguel (Sales).

## Resolution / evidence

- Confirmed authorized HR read/write access and unauthorized Sales access denial.
- Tested both share and NTFS permission layers.

**Technical note:** Share and NTFS permissions combine to determine effective rights over the network. Avoid explicit Deny entries when group-based allow lists are sufficient.
