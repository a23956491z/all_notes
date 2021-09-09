Network file system
share directory and files with others

Client request to **mount** a directory form remote host 

access a file using NFS, RPC call placed to NFS deamon on server:
* file handle
* name of file
* user ID
* group ID

file handle : address on file and directory
```bash
sudo mount  -t nfs <IP>:share /tmp/mount -nolock
```

* -t nfs : type is NFS
* IP:share : NFS server's name is share
* -nolock : not to use NLM locking


## escalate privileges
root_suqash: root squashing is enabled by default. So no one can connecting to NFS with root access.

if root_squash is disable, it can allow the creation of SUID files. allowing remote user root access.

1. Copy bash file to NFS share
2. Change bash file's owner to root
3. Grant SUID permission to bash
4. SSH into normal user
5. Use the SUID bash file(`./bash -p`) and we granted ROOT PRIVILEGE
