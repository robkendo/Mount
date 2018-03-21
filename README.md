# Mount
Mount cmds

Mount USB drive and copy files in CentOS

Place the usb drive into a usb port on the server.
From the cli run lsblk and look for your flash drive size
You should see something like this as the output
ROOT@rediscacheproxy-1-018.live.niso1.las1:~ 
$ lsblk
NAME   MAJ:MIN RM   SIZE RO TYPE MOUNTPOINT
sda      8:0    0 931.5G  0 disk 
├─sda1   8:1    0   200M  0 part /boot/efi
├─sda2   8:2    0   500M  0 part /boot
└─sda3   8:3    0 930.8G  0 part /
sdb      8:16   1   7.5G  0 disk 
└─sdb1   8:17   1   7.5G  0 part   (my flash drive)


 
 
Once you verify your usb drive in the caption above run this command
sudo mkdir /media/flash

Now mount the drive with the following command.  Note that your string might be different because the server might have a different name for the usb.
sudo mount /dev/sdb1 /media/flash

Once the drive has been mounted you can browse it by typing…
cd /media/flash

For copying files from the server you would use this command.
sudo cp -r /home/yourusername/* /media/flash





Here is a example done from one of our servers


mkuhlman@corpmz.com@las1-1-002.idm:~
$ ssh_as_root graphite-1-002.shared.adm.las1.mz-inc.com
****************************************************************************
* This system is property of Machine Zone, Inc. It is for authorized use   *
* only as detailed in the IT Accountability Policy. This system is subject *
* to monitoring to ensure security and proper functionality.               *
*                                                                          *
* Any unauthorized use that reveals criminal activity or policy violation  *
* may be provided to law enforcement officials or management for           *
* disciplinary action. By continuing, you are agreeing to these terms.     *
****************************************************************************
Last login: Fri Feb 10 18:37:48 2017 from las1-1-002.idm.mz-inc.com
****************************************************************************
* This system is property of Machine Zone, Inc. It is for authorized use   *
* only as detailed in the IT Accountability Policy. This system is subject *
* to monitoring to ensure security and proper functionality.               *
*                                                                          *
* Any unauthorized use that reveals criminal activity or policy violation  *
* may be provided to law enforcement officials or management for           *
* disciplinary action. By continuing, you are agreeing to these terms.     *
****************************************************************************
-------------------------------------------------------------------------------------
Welcome to graphite-1-002.shared.adm.las1.mz-inc.com!
Hostgroup: production/graphite.shared
Owner: Site Reliability Engineering (SRE)
Contacts: email: techops-sre@mz.com, slack: #ops---live
Purpose:
LOM IP: 10.193.3.77
Rack: 31
Port: 2
Hardware SKU: Database001
Switch SKU: Cisco001
VLAN: SHARED (504)
-------------------------------------------------------------------------------------
ROOT@graphite-1-002.shared.adm.las1:~
$ df -h
Filesystem      Size  Used Avail Use% Mounted on
/dev/sda3       112G  9.4G  102G   9% /
devtmpfs        126G     0  126G   0% /dev
tmpfs           126G   12K  126G   1% /dev/shm
tmpfs           126G   18M  126G   1% /run
tmpfs           126G     0  126G   0% /sys/fs/cgroup
/dev/sda2       492M  114M  379M  24% /boot
/dev/sda1       200M  9.8M  191M   5% /boot/efi
ROOT@graphite-1-002.shared.adm.las1:~
$ lsblk
NAME   MAJ:MIN RM   SIZE RO TYPE MOUNTPOINT
sda      8:0    0 111.8G  0 disk
├─sda1   8:1    0   200M  0 part /boot/efi
├─sda2   8:2    0   500M  0 part /boot
└─sda3   8:3    0 111.1G  0 part /
sdb      8:16   1   7.5G  0 disk
└─sdb1   8:17   1   7.5G  0 part
ROOT@graphite-1-002.shared.adm.las1:~
$ sudo mkdir /media/flash
ROOT@graphite-1-002.shared.adm.las1:~
$ cd /media/flash
ROOT@graphite-1-002.shared.adm.las1:/media/flash
$ ls -a
.  ..
ROOT@graphite-1-002.shared.adm.las1:/media/flash
$ cd ..
ROOT@graphite-1-002.shared.adm.las1:/media
$ cd ..
ROOT@graphite-1-002.shared.adm.las1:/
$ cd /tmp
ROOT@graphite-1-002.shared.adm.las1:/tmp
$ ls -a
.                                             puppet20170210-10719-yiusuh
..                                            sensu_client_loaded_files
fio-bugreport-20170210.183903-UQoSS0.tar.bz2  systemd-private-pqo0FS
.font-unix                                    systemd-private-xfAklh
hsperfdata_root                               tcollector.procstat.prev
.ICE-unix                                     .Test-unix
logstash-config-checksum                      .X11-unix
pip_build_root                                .XIM-unix
puppet20170210-10719-1pcxzys
ROOT@graphite-1-002.shared.adm.las1:/tmp
$ cd /var/tmp
ROOT@graphite-1-002.shared.adm.las1:/var/tmp
$ ls -a
.
..
abrt
sosreport-mkuhlman.2102017-20170210184819.tar.xz
sosreport-mkuhlman.2102017-20170210184819.tar.xz.md5
systemd-private-3j3bb5
systemd-private-N6GQKJ
ROOT@graphite-1-002.shared.adm.las1:/var/tmp
$ sudo cp -r /home/yourusername/* /media/flash
cp: cannot stat ‘/home/yourusername/*’: No such file or directory
ROOT@graphite-1-002.shared.adm.las1:/var/tmp
$ cd /tmp
ROOT@graphite-1-002.shared.adm.las1:/tmp
$ cd /var/tmp
ROOT@graphite-1-002.shared.adm.las1:/var/tmp
$ sudo cp -r sosreport-mkuhlman.2102017-20170210184819.tar.xz /media/flash/
ROOT@graphite-1-002.shared.adm.las1:/var/tmp
$ cd /media/flash
ROOT@graphite-1-002.shared.adm.las1:/media/flash
$ ls -a
.  ..  sosreport-mkuhlman.2102017-20170210184819.tar.xz
ROOT@graphite-1-002.shared.adm.las1:/media/flash
$ cd /tmp
ROOT@graphite-1-002.shared.adm.las1:/tmp
$ ls -a
.                                             puppet20170210-10719-yiusuh
..                                            sensu_client_loaded_files
fio-bugreport-20170210.183903-UQoSS0.tar.bz2  systemd-private-pqo0FS
.font-unix                                    systemd-private-xfAklh
hsperfdata_root                               tcollector.procstat.prev
.ICE-unix                                     .Test-unix
logstash-config-checksum                      .X11-unix
pip_build_root                                .XIM-unix
puppet20170210-10719-1pcxzys
ROOT@graphite-1-002.shared.adm.las1:/tmp
$ sudo cp -r fio-bugreport-20170210.183903-UQoSS0.tar.bz2  /media/flash
ROOT@graphite-1-002.shared.adm.las1:/tmp
$ cd /media/flash/
ROOT@graphite-1-002.shared.adm.las1:/media/flash
$ ls -a
.   fio-bugreport-20170210.183903-UQoSS0.tar.bz2
..  sosreport-mkuhlman.2102017-20170210184819.tar.xz
ROOT@graphite-1-002.shared.adm.las1:/media/flash
$

 
 
 
 

