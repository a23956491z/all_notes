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

### Download senstive file with **Poison Null Byte**

in `http://10.10.255.254/ftp` we want to download the `package.json.bak` file and we get the *403 Error: Only .md and .pdf files are allowed!*

We can use character bypass called **Poison Null Byte** looks like `%00` & we encode `%00` to URL encoded format which is `%2500`

adding this at the end & append the `.md` suffix like:
`http://10.10.255.254/ftp/package.json.bak%2500.md`

Poison Null byte is a **NULL terminator**

## Broken Access Control

Privilege Escalation
* Horizontal : different user same level of permission
* Vertical : Higher level of permission

In web developer -> debugger
we can find a javascript file `http://10.10.255.254/main-es2015.js`

Go to this file's source code
we can search for term`admin` and tring to find `path: administration`

and we found `path:"administration"` this hint towards a page called `/#/administration`

### change parameter
with intercept on , by click the view basket we found the api for basket is : `/rest/basket/NaN`

by change `Nan` to `2` we can see the basket of user 2

## XSS

### DOM XSS
we can use this payload this in search bar
```
<iframe src="javascript:alert(`xss`)"> 
```

and this type of XSS is also called XFS (Cross-Frame Scripting)

### Persistent XSS
in admin account
we can navigate the "Last Login IP" page for this attack
![](https://i.imgur.com/MBakVxN.png)

turn on the intercept to catch the **logout request**
and add this Header name:`True-Client-IP` value with the payload:
```
<iframe src="javascript:alert(`xss`)"> 
```

and when we back to "Last Login IP" page
it would show our payload, because this page will catch the header value : `True-Client-IP`

### Reflected XSS

in Order History -> Orders & Payment
clicking the **Truck** button would lead us to the order detail
`http://10.10.255.254/#/track-result?id=5267-b33bfac9d9e227c1`

and we can change the parameter id's value to our payload :
```
<iframe src="javascript:alert(`xss`)">
```

## More change 
in `/#/score-board/`