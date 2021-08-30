## Google drive + Rclone

1. Get client_id
	1. Log into the [Google API Console](https://console.developers.google.com/) 
	2. Select a project or create a new project
	3. **ENABLE API AND SERVICE** enable **google drive API**
	4. Client Credentials on sidebar & Create Credentials (Not Create Credentials wizard) : Create OAuth Client ID
	5. **CONFIGURE CONSENT SCREEN** : External
	6. Enter app name("rclone")  select Support email enter Contact email & Save
	7. "+ CREATE CREDENTIALS" , OAuth client ID, Desktop APP
	8. Go to OAuth consent screen : **PUBLISH APP**

2. Create Config `rclone config`


## Alias
`g_transfer`
```bash
#!/bin/bash
TRANSFER_PATH="/home/enip/Downloads/gdrive/transfer"

mkdir -p $TRANSFER_PATH
rclone copy -P g_ndhu:transfer $TRANSFER_PATH
```