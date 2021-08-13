install 
```bash
sudo pacman -S postgresql pgadmin4
```

switch to user `postgres`
```bash
sudo -iu postgres
```

INIT database
```bash
initdb -D /var/lib/postgres/data
```

start postgreSQL database
```bash
sudo systemctl start postgresql
sudo systemctl enable postgresql
```