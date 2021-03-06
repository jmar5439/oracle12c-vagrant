#Oracle 12c Vagrant

Updated for 12.1.0.1 with 12.1.0.1.5 October 14 2014 PSU

Patch 19121550: DATABASE PATCH SET UPDATE 12.1.0.1.5

Following these instructions will use an Oracle Linux 6.5 VirtualBox VM, Install Oracle 12cR1 software, Patch it, and then create a container database with one pluggable database.

## Prerequisites

### VirtualBox

http://www.virtualbox.org

### Vagrant

http://vagrantup.com

### Oracle Linux 6.5

1. Use Vagrant box "rchouinard/oracle-65-x64"


### Oracle 12cR1
#### Optional (this branch has patches disabled)

1. Download Database Install files (1 and 2) - http://www.oracle.com/technetwork/database/enterprise-edition/downloads/database12c-linux-download-1959253.html
2. Place the zip archives in database_installer/

### Oracle 12cR1 CPU Patches

http://support.oracle.com

1. Download Patch 19121550: DATABASE PATCH SET UPDATE 12.1.0.1.5
2. Download patch 6880880
3. Place 19121550 at patches/p19121550_121010_Linux-x86-64.zip
4. Place 6880880 at patches/p6880880_121010_Linux-x86-64.zip
5. Make patches archives readable by all

    $ cd {project root}
    $ cd patches
    $ chmod gou+r *.zip


## Run Vagrant Box

    $ cd {project root}
    $ vagrant up
    $ vagrant ssh

## Oracle options in these branch

charset : WE8ISO8859P15

## Run Oracle 12c Installation Script

    [vagrant@vagrant-ol6 ~]$ sudo /vagrant/scripts/oracle12c-install.sh

## Connect to Database

    $ vagrant ssh
    $ service oracle start
    
    $ su - oracle
    
    $ sqlplus / as sysdba
    
    SYS@cdb12c>alter system set local_listener='LISTENER_CDB12C' scope=both;
    
Modifiy state of pluggable database :

    https://yasinyazici.wordpress.com/2014/09/13/automatic-pdb-start-in-12c/
    
## Connect to PDB

    $ sqlplus system@pdb

  Default password for sys, system is vagrant - Port 1521 - service cdb12c (for container), pdb (for pluggable database)

## Verifying Patch was Installed

    $ su - oracle

    [oracle@oracle12c ~]$ /u01/app/oracle/product/12.1.0/db_1/OPatch/opatch lsinventory

    Oracle Interim Patch Installer version 12.1.0.1.0
    Copyright (c) 2012, Oracle Corporation.  All rights reserved.


    Oracle Home       : /u01/app/oracle/product/12.1.0/db_1
    Central Inventory : /u01/app/oraInventory
       from           : /u01/app/oracle/product/12.1.0/db_1/oraInst.loc
    OPatch version    : 12.1.0.1.0
    OUI version       : 12.1.0.1.0
    Log file location : /u01/app/oracle/product/12.1.0/db_1/cfgtoollogs/opatch/opatch2014-10-15_04-11-23AM_1.log

    Lsinventory Output file location : /u01/app/oracle/product/12.1.0/db_1/cfgtoollogs/opatch/lsinv/lsinventory2014-10-15_04-11-23AM.txt

    --------------------------------------------------------------------------------
    Installed Top-level Products (1):

    Oracle Database 12c                                                  12.1.0.1.0
    There are 1 products installed in this Oracle Home.


    Interim patches (1) :

    Patch  19121550     : applied on Wed Oct 15 04:06:35 UTC 2014
    Unique Patch ID:  17919353
    Patch description:  "Database Patch Set Update : 12.1.0.1.5 (19121550)"
       Created on 6 Oct 2014, 17:22:53 hrs PST8PDT
       Bugs fixed:
         17716305, 17257820, 17034172, 16694728, 16042673, 18096714, 17439871
         16320173, 14664684, 17762256, 18002100, 18436307, 16450169, 17006570
         17753428, 17552800, 15994107, 17441661, 17305959, 18362376, 17997255
         17710315, 14506328, 17806676, 17443596, 17040764, 16849982, 16837842
         14010183, 18393024, 16845022, 16228604, 17446564, 17042658, 14536110
         17579911, 18262334, 17311728, 17391312, 17244462, 16935643, 17039360
         14355775, 18155703, 16672859, 18229326, 17080436, 17912217, 16788832
         16039096, 16570023, 18099539, 14123213, 17174391, 17405549, 17830435
         17249820, 16946990, 16589507, 16924879, 16874123, 17750832, 16784143
         15987992, 17346196, 16901482, 16859937, 17898041, 17068536, 16910001
         17946998, 16527374, 17394724, 17572720, 16703112, 17490498, 16433869
         16186165, 16170787, 16524968, 17032726, 16543323, 17349104, 18355572
         17888553, 16575931, 18061914, 16070351, 17088068, 16888264, 16448848
         16863422, 17443671, 18308576, 16911800, 16517900, 16825779, 17019974
         16707927, 17551812, 14576755, 17263661, 17325413, 17446849, 16465149
         17184677, 16689109, 16705020, 18889652, 17828499, 16964279, 15953721
         17205719, 18603606, 18121501, 16757934, 16864562, 16782193, 17436936
         15996344, 17037526, 17260090, 19556045, 17216406, 17659488, 16485876
         16709437, 17898730, 17174582, 16796277, 17421502, 17534365, 16921340
         16784167, 18292893, 16660558, 16793174, 16371304, 17570606, 16943711
         16674666, 16697600, 17848854, 18522516, 17797837, 17716565, 16456371
         16347068, 16181570, 19121550, 17516005, 16275522, 16475788, 16683859
         17491753, 16427054, 16227068, 17753514, 16479182, 18554871, 17051636
         16263492, 16551086, 18856947, 16406802, 16433745, 16681689, 17614134
         17364702, 17171530, 17298973, 16212405, 19049453, 18189497, 16443657
         16855202, 18078926, 18244962, 17462687, 16087650, 16313881, 16992075
         17082983, 17359546, 14595800, 16715647, 19554106, 17362796, 17777061
         16392068, 17761775, 16977973, 17158214, 14197853, 16712618, 12911115
         17922172, 16524071, 16856570, 17050888, 16410570, 17210416, 13866822
         18513099, 16372203, 17867137, 16101465, 15914210, 16459685, 16802693
         16195633, 16978185, 17983206, 16787973, 16850996, 16178562, 16838328
         16503473, 18126350, 13782826, 18439152, 17537657, 17721717, 17489214
         16362358, 16994576, 17600719, 17461374, 16969016, 17571945, 16444683
         16928832, 16929165, 16710753, 16864359, 16679874, 18031528, 16585173
         15986012, 17467075, 17735933, 14852021, 16191248, 19692901, 16173738
         17797453, 17343514, 16495802, 17324822, 16619249, 19297295, 16590848
         15921906, 16986421, 17316776, 16576250, 16730813, 16433540, 16663303
         18420490, 16619979, 17897716, 17016479, 16457621, 16675739, 17341326
         17981677, 17005047, 17442449, 16795944, 16668226, 16698577, 16621274
         17330580, 18348157, 17393683, 17817656, 16634384, 16465158, 16816103
         16910734, 16584684, 16936008, 16347904, 16512817, 17273253, 16902138
         17179261, 17810688, 16864048, 17468141, 17226980, 17883081, 16682595
         16473934, 16762985, 16864864, 16721594, 16946613, 16972213, 16855292
         17026503, 16964686, 17860549, 16674842, 13771513, 16061921, 17235750
         16842274, 16913149, 16769019, 17000176, 15931910, 17572525, 17478145
         14237793, 19248799, 17976046, 17289787, 16919176, 16613964, 17217040
         16462834, 18092561, 16617325, 17308691, 16733884, 16483559, 16057129
         16286774, 16822629, 17596344, 19289642, 17954431, 18423374, 16993424
         17605522, 17280117, 8352043, 18973907, 16772060, 16790307, 16991789
         17608025, 18082092, 16603924, 18148383, 17182200, 16784901, 16912439
         13521413, 17767676, 17478811, 16836849, 16007562, 16851772, 16663465
         17786278, 17027533, 16675710, 17437634, 19458377, 17610418, 17465741
         15905421, 17892268, 16523150, 16741246, 16930325, 17982838, 17390431, 17974104



    --------------------------------------------------------------------------------

    OPatch succeeded.
    
    
Check listener issues
https://gemsofprogramming.wordpress.com/2013/10/05/listen-oracle-12c-or-the-chapter-of-letting-the-listener-listen-on-a-non-default-port/
