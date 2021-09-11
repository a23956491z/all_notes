Simple Mail Transfer Protocol

Ports : 25

1. SMTP handshake
2. Submits : sender, recipeint, body, attachments
3. SMTP server : Check domain name of recipient & sender is the same?
4. SMTP server : 

## Enumerating

SMTP internal commands
* VERY : confirming the name of valid user
* EXPN : reveal address of user & lists of emails

We can use Metasploit's *smtp_enum* module to enumerating
* it would feed to host a wordlist of usernames
* auxiliary/scanner/smtp/smtp_enum

Metasploit:
1. `msfconsole`
2. `search smtp_version`