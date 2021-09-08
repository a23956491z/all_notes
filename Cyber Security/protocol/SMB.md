 Server Message Block Protocol
 
 response-request 
 Clients connect to servers using TCP/IP
 
 * Samba (for UNIX)
 * printer

## SMB command
smbclient:
`smbclient //[IP]/[SHARE]`
* `-U <user>`
* `-p <port>`


* `get <file>` download file


get the info of file:
```bash
$ smbcacls //10.10.199.57/profiles .ssh/id_rsa
```
## Enumerating

1. Port scanning
* SMB running on which port?
2. Enum4Linux
* workgroup ?
* name of machine?
* version of OS



Enum4Linux:
-U             get userlist  
-M             get machine list  
-N             get namelist dump (different from -U and-M)  
-S             get sharelist  
-P             get password policy information  
-G             get group and member list

-A             all of the above (full basic enumeration)