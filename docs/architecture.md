# Technical notes — Lab architecture

## Machines

- **HD-DC01:** Windows Server 2025 Standard Evaluation, AD DS domain controller and DNS server for `helpdesk.test`; internal IPv4 `192.168.50.10/24`.
- **HD-PC01:** Windows 11 Enterprise Evaluation, joined to the domain; internal IPv4 `192.168.50.20/24`.
- **Hypervisor:** Oracle VirtualBox on a Windows 11 host.
- **Network:** `HELPDESK-LAN` is the Internal Network shared by the two VMs; no default gateway is needed on the internal NIC. NAT was used separately during installation or for internet access.

## Domain structure

```text
helpdesk.test
└── Employees
    ├── IT
    ├── HR
    ├── Sales
    └── Finance
```

Ten fictional accounts are distributed across the OUs. The HR Global Security group, `GG_HR_Shared_RW`, contains Sofia Costa, Mariana Lopes and Carolina Sousa in the final working state.

## File access model

Network resource: `\\HD-DC01\HR` (folder under `C:\Company Shares\HR` in the lab).

- Share permissions: HR security group with Change and Read; Administrators with Full Control.
- NTFS: HR security group with Modify; SYSTEM and Administrators retain Full Control.
- Sales accounts have no access through the HR group.

The effective permission for a request over SMB depends on both share and NTFS controls. When users change AD groups, they usually need a fresh logon session to obtain a new security token.

## Known observations

- On some tests, default name resolution consulted an unexpected DNS server, but explicitly querying `192.168.50.10` successfully resolved the domain controller.
- The domain controller advertised a VirtualBox NAT-associated IPv6 address in an AAAA record at one stage. IPv4 domain resolution and SMB were validated; any final AAAA cleanup is a follow-up task.
- A missing reverse PTR record can produce `Server: Unknown` in `nslookup` while forward DNS lookups succeed.
