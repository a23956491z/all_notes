`-p 80` scan port 80
`-p 1000-1500` scan ports from 1000 to 1500
`-p-` scan all ports

`-A` aggressive mode

`-sS` Syn scan 
`-sU` UDP scan
`-O` detect OS
`-sV` detect the version of services running

`-v` verbose
`-vv` more verbose

saving outputs:
`-oA` save to 3 major format at once
`-oN` normal format
`-oG` grepable format

timing:
`-T5` timing template to level 5

scripts:
`--script=vuln` activate all scripts in "vuln" category

TCP scan:
`-ST` connect scans
`-sS` SYN "half-open" scans
`-sN` TCP full scan
`-sF` TCP FIN scans
`-sX` TCP Xmas Scans