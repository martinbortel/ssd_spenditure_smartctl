# ssd_spenditure_smartctl

Check, how much data is being written to Your SSD.

The solution works through crontab run smartctl statistic, picking out written bytes and storing the information into ~/disk.log.

## Setup
1/ create link from ./disk.log to ~/
```sh
ln -s $(pwd)/disk.log ~/
```
2/ crontab setup
```sh
sudo crontab -l | cat - ./sudo_crontab | sudo crontab -
```
3/ ssd to $PATH
e.g. /usr/local/sbin - make sure the path is in your env variable $PATH
```sh
ln -s $(pwd)/ssd /usr/local/sbin/
```

## Usage
Cron will gather written bytes every day at 3pm.
The ./ssd script can calculate medians from the ./disk.log raw smartctl data.
e.g.
```sh
ssd 2
```
The above will print something like below:
```sh
❯ ssd 3
 - ----------- ------ -- ----- --
 + 07-May-2023 d.incr     1609 GB
 - ----------- ------ -- ----- --
 | 09-May-2023     79 GB
 v 11-May-2023     63 GB  1.75 TB
 - ----------- ------ -- ----- --
```

Or one can call smartctl overall stats:
```sh
❯ ssd --stats
smartctl 7.3 2022-02-28 r5338 [Darwin 22.4.0 arm64] (local build)
Copyright (C) 2002-22, Bruce Allen, Christian Franke, www.smartmontools.org

=== START OF INFORMATION SECTION ===
Model Number:                       
Serial Number:                      
Firmware Version:                   
PCI Vendor/Subsystem ID:           
IEEE OUI Identifier:                
Controller ID:                      
NVMe Version:                       
Number of Namespaces:              
Local Time is:                     
Firmware Updates (0x02):           
Optional Admin Commands (0x0004):   
Optional NVM Commands (0x0004):     
Maximum Data Transfer Size:        

Supported Power States
St Op     Max   Active     Idle   RL RT WL WT  Ent_Lat  Ex_Lat
 0 +     0.00W       -        -    0  0  0  0        0       0

=== START OF SMART DATA SECTION ===
SMART overall-health self-assessment test result: PASSED

SMART/Health Information (NVMe Log -x--)
Critical Warning:                   -x--
Temperature:                        XX Celsius
Available Spare:                    XX%
Available Spare Threshold:          XX%
Percentage Used:                    XX%
Data Units Read:                    
Data Units Written:                 X,XXX,XXX [X.XX TB]
Host Read Commands:                 XX,XXX,XXX
Host Write Commands:                XX,XXX,XXX
Controller Busy Time:               X
Power Cycles:                       XXX
Power On Hours:                     XX
Unsafe Shutdowns:                   X
Media and Data Integrity Errors:    X
Error Information Log Entries:      X
..
```

## Contact
e: martin.bortel@gmail.com
