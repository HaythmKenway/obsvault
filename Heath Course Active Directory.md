Active directory initial attack vectors

#### LLMNR Poisoning
used to indentify hosits when DNS fails 
it is known as NBT-NS
![[Pasted image 20230605094058.png]]

Mitigation
best way is to prevent LLMNR and NBT-NS 

adding network based authentication 
requiring strong username and password

### SMB RELAY

it is the process of relaying hashes to specific machine and gaining acess without cracking the passwords

smb sign must be disabled on target 


### IPV6 Attack
we are often using ipv4 for performing operations in the network and we forget we have an ipv6 address assigned to our machine and who is taking care of dns resolution for ipv6
its nobody
so we can use this to impersonate as 


---
### Token Impersonation Attack

what are tokens ?
They are temprorary keys that allws you to access a system or netwoek without having to provide credentials each time you access a file
it is like a cookie for a computer

Types of tokens 
Delegate- Created for logging in to a desktop aor using rdp
Impersonate token - attaching a network drive or domain logon script "non interactive"


This can be done by using metasploit meterpreter
we can simply use psexec to get a meterpreter shell and incognito

Mitigation
Limit user/group token creation permission
Account tiering
Local Admin Restriction

---
### Kerberoasting
![[Pasted image 20230611203341.png]]

We can use GetUserSpns.py to get the server principle names associated with the normal user account
since normal user accounts  temds to be shorter than machines account, so that the tgs will encrypt the ticket with the account the spn is running under ,
we can retrieve the krgb5 ticket and crack the password using hashcat
Mitigation :-
it is a feature so we need to setup a strong password and least privilage to users

----

### GPP Attack

Group policy prefference allows admins to create policies using embedded credentials
THese credentials were encrypted and placed in a cPassword

---
### Post exploitation
![[Pasted image 20230612002657.png]]



![[Pasted image 20230612002911.png]]
