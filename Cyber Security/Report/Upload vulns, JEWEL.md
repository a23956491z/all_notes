headers:
* X-Powered-By: Express
* Server: nginx/1.17.6

## Naming
gobuster result with **direcotry-list-medium**:
* /content
* /modules
* /admin
* /assets

HINT: the uploaded file are gived a random name in `/`

## Client-side filter

filter js:
```javascript
HTTP/1.1 200 OK
Server: nginx/1.17.6
Date: Sat, 25 Sep 2021 07:38:02 GMT
Content-Type: application/javascript; charset=UTF-8
Content-Length: 1579
Connection: close
X-Powered-By: Express
Access-Control-Allow-Origin: *
Accept-Ranges: bytes
Cache-Control: public, max-age=0
Last-Modified: Fri, 03 Jul 2020 22:16:52 GMT
ETag: W/"62b-17316c0f820"

$(document).ready(function(){let errorTimeout;const fadeSpeed=1000;function setResponseMsg(responseTxt,colour){$("#responseMsg").text(responseTxt);if(!$("#responseMsg").is(":visible")){$("#responseMsg").css({"color":colour}).fadeIn(fadeSpeed)}else{$("#responseMsg").animate({color:colour},fadeSpeed)}clearTimeout(errorTimeout);errorTimeout=setTimeout(()=>{$("#responseMsg").fadeOut(fadeSpeed)},5000)}$("#uploadBtn").click(function(){$("#fileSelect").click()});$("#fileSelect").change(function(){const fileBox=document.getElementById("fileSelect").files[0];const reader=new FileReader();reader.readAsDataURL(fileBox);reader.onload=function(event){

			//Check File Size
			if (event.target.result.length > 50 * 8 * 1024){
				setResponseMsg("File too big", "red");			
				return;
			}
			//Check Magic Number
			if (atob(event.target.result.split(",")[1]).slice(0,3) != "???"){
				setResponseMsg("Invalid file format", "red");
				return;	
			}
			//Check File Extension
			const extension = fileBox.name.split(".")[1].toLowerCase();
			if (extension != "jpg" && extension != "jpeg"){
				setResponseMsg("Invalid file format", "red");
				return;
			}


const text={success:"File successfully uploaded",failure:"No file selected",invalid:"Invalid file type"};$.ajax("/",{data:JSON.stringify({name:fileBox.name,type:fileBox.type,file:event.target.result}),contentType:"application/json",type:"POST",success:function(data){let colour="";switch(data){case "success":colour="green";break;case "failure":case "invalid":colour="red";break}setResponseMsg(text[data],colour)}})}})});

```

we can found the client-side filter's error message is :`Invalid file format`
after we remove the client-side filter, the error message changed to `Invalid file type`

## Server-side
### Magic number?
modified the `.jpg` file's magic number to `4D 5A` (`.exe`)
and uploads works

the server-side filter **is not** using magic number.

### Whitelist or Blacklist
it says the upload type is wrong
maybe we can try change the MIME from `.php` file to `image/jpg` -> ~~still get `invalid file type`~~ , we need to use `image/jpeg`!!!!, and it works
or upload innocent with MIME from `image/jpg` to `php`? -> also `invalid file tpye`

**the server is also using MIME checking**

we can successfully upload some files after change the MIME type to `image/jpeg`

## Admin page
after we 