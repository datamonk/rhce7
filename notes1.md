## Building a basic RPM package

```bash
yum install rpmdevtools
# as non-root user:
rpmdev-setuptree
mkdir example-1.0
echo "Here is some text." > example-1.0/example-file.txt
tar czf example-1.0.tar.gz example-1.0
cp example-1.0.tar.gz rpmbuild/SOURCES
rpmdev-newspec rpmbuild/SPECS/example.spec
# edit rpmbuild/SPECS/example.spec accordingly
# see: example.spec
rpmbuild -ba rpmbuild/SPECS/example.spec
```

## Recovering root login

* Reboot the host, enter edit mode in bootloader.
* Append rd.break to the end of the line that starts with linux16. Restart with Ctrl+X
* Remount /sysroot as read-write. 

```bash
switch_root:/# mount -oremount,rw /sysroot
```

* Switch into a chroot jail, where /sysroot is treated as the root of the file system tree.

```bash
chroot /sysroot
```

* Set a new root password

```bash
passwd root
```

* Ensure all unlabeled files (including /etc/shadow) get relabeled at boot. 

```bash
touch /.autorelabel
```

```bash
exit && exit
```

## Change the local hostname
A static host name may be specified in the /etc/hostname file. The hostnamectl command is used to modify this file and may be used to view of the systems FQDN.

```bash
hostnamectl status
hostnamectl set-hostname <new_hostname>
```

## Systemctl operations
```bash
systemctl status|stop|start|restart <UNIT>
```
```bash
systemctl reload <UNIT>
```
```bash
systemctl mask|unmask <UNIT>
```
```bash
systemctl enable|disable <UNIT>
```
```bash
systemctl list-dependencies <UNIT>
```
Change the system target at runtime: 
```bash
systemctl isolate <TARGET>
```
List default system target
```bash
systemctl get-default
```
Set the default target (None runtime)
```bash
systemctl set-default <new_target>

## Managing IPv6 Networking

### Commands
List names of available connections:
```bash
nmcli con show
```
Adding a new connection profile
```bash
nmcli con add con-name <NAME> type <TYPE> ifname <INTERFACE_NAME>
```
Modifying existing connections
```bash
nmcli con mod <con-name> ..
```
Deleting a network connection
```bash
nmcli con del <con-name>
```
Deactivate and disconnect the current connection on the network interface dev
```bash
nmcli dev dis <dev-name>
```

## Setup Teaming

## Setup Bridging

## Port Security
