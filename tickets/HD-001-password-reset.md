# HD-001 — Forgotten domain password

**Scenario:** Sofia Costa (HR) cannot sign in after forgetting her domain password.

## Objective

Restore access using Active Directory Users and Computers (ADUC), while ensuring the employee changes the temporary password at next sign-in.

## Procedure

1. In a real service desk, verify the employee's identity according to policy. In this lab, identity verification is simulated.
2. On HD-DC01, open ADUC → `helpdesk.test/Employees/HR` → Sofia Costa.
3. Right-click **Reset Password**, set a temporary lab password and select **User must change password at next logon**.
4. On HD-PC01, sign in using `HELPDESK\sofia.costa`, complete the password-change prompt, then check `whoami`.

## Resolution / evidence

- Domain account password was reset.
- A mandatory password change was configured.
- Domain sign-in was later practiced on the Windows 11 workstation.

**Security notes:** Do not store the password in the ticket, README, or screenshots. Share a temporary password only through an approved private channel in a real organization.
