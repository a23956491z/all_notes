1. we get the email of administrator

![](https://i.imgur.com/RipWFs6.png)

2. searching parameter is using `q`
![](https://i.imgur.com/awIaMRK.png)


## SQL injection

Scenario might be:
```
String query = "SELECT * FROM accounts WHERE custID='" + request.getParameter("id") + "'";
```
### TEST injection
1. Turn on intercept mode in Burp Suite
2. Login with any infor.
3. `Forward` in Burp and we can intercept the POST
![](https://i.imgur.com/0eMteVm.png)
4. modify the POST with `{"email":"' or 1=1--","password":"a"}`

explan the payload:
1. `'` close the brackets in SQL query
2. `or 1=1` will always return true, which means email is valid and log us into **user id 0**
3. `--` comment the rest query

### Login to sepecific account

payload : `{"email":"bender@juice-sh.op'--","password":"a"}`

## Brute Force 

1. Use **Intruder**
2. in **Position** tab click **Clear** button
3. add the value field of **password**
4. email with the admin email  we got `admin@juice-sh.op`
![](https://i.imgur.com/L27oOTl.png)

we use the payload list `best1050.txt` from Seclists
install Seclists : `sudo apt-get install seclists`

list position : `/usr/share/seclists/Passwords/Common-Credentials/best1050.txt`

successful request return **200 ok**
failed request return **401 Unauthorized**

## Sensitive Data Exposure

### Sensitive link
in About us page, we found the link of legal.md is `http://10.10.255.254/ftp/legal.md`, which Navigating to that `/ftp/` directory.

And we can directly use `http://10.10.255.254/ftp` to see the files in FTP server.
