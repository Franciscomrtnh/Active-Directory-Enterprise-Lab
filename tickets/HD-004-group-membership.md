# HD-004 — HR user suddenly loses access

**Scenario:** Sofia Costa previously accessed the HR folder but is now denied access.

## Objective

Diagnose group membership as the root cause and restore permissions without granting excess privileges.

## Reproduction and diagnosis

1. Remove Sofia from `GG_HR_Shared_RW` on HD-DC01.
2. Fully sign Sofia out of HD-PC01, then sign in again to refresh her logon token.
3. Try `\\HD-DC01\HR` and observe access denied.
4. Run `whoami /groups` on HD-PC01 and confirm `GG_HR_Shared_RW` is absent from the current token.
5. Inspect group membership in ADUC to confirm the missing user.

## Resolution

1. Re-add Sofia to `GG_HR_Shared_RW` using ADUC.
2. Sign out and back in on HD-PC01 to refresh her token.
3. Confirm `whoami /groups` includes the HR group and that Sofia can open and edit `HR-Test.txt`.

**Outcome:** Reproduced and resolved the access issue by restoring the intended AD group membership. No administrative rights were granted to the employee.
