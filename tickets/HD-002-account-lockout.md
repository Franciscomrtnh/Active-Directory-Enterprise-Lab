# HD-002 — Account locked after failed logins

**Scenario:** Miguel Santos (Sales) reports being unable to log in after entering an incorrect password repeatedly.

## Objective

Confirm the applicable domain lockout policy, reproduce the problem using a test account, unlock the user and validate login.

## Procedure

1. On HD-DC01, use `net accounts /domain` to confirm threshold **5**, duration **15 minutes**, observation window **15 minutes**.
2. On HD-PC01, intentionally enter an incorrect password for `HELPDESK\miguel.santos` up to the configured threshold.
3. On HD-DC01, check the user's **Account** tab in ADUC for lockout state. Optionally examine Windows Security Event ID **4740**.
4. Unlock the account in ADUC if still locked. The policy can unlock it automatically after 15 minutes.
5. Sign in again with the correct domain credentials and verify with `whoami`.

## Resolution / evidence

- Investigated a simulated authentication lockout and restored Miguel's account access.
- Distinguished a failed-password delay on Windows from confirmed AD lockout state.

**Security note:** Only use fictional test users; never intentionally lock out a privileged account.
