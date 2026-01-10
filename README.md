# check_linux_security updates

nagios check to show pending security udpates on assorted Linux distros

Tested on Debian, Ubuntu, Fedora, RHEL, Alma, Rocky, Oracle Linux

NOTE: CentOS Stream does not publish security-only fixes, so this check will report ALL available updates on CentOS Stream.

# Requirements
ssh key pair auth

# Configuration

Add a section similar to the following to the services.cfg file on the nagios server.

```
define service{
        use                             generic-service
        hostgroup_name                  all_linux
        service_description             security updates
        check_command                   check_by_ssh!"/usr/local/nagios/libexec/check_linux_security_updates"
        }
 ```

# Output

You will see output similar to the following:

```
OK 0 pending security updates
```
```
WARN 34 security updates pending: ALSA-2025:23306 ALSA-2025:23306 ALSA-2025:21931 ALSA-2025:22395 <output snipped>
```
```
WARN 1 security updates pending, use dnf updateinfo list --security for details: FEDORA-EPEL-2025-beeb62ad3c
```
```
WARN 211 updates available, but since CentOS does not classify updates as security or bugfix or enhancement, this represents all available updates. Try these commands to see all pending updates: dnf list updates ; dnf repoquery --changelogs --upgrades
```
```
WARN 140 security updates pending: libc-devtools libc6-dev libc-dev-bin linux-libc-dev <output snipped>
```
```
UNKNOWN 140 security updates pending: libc-devtools libc6-dev libc-dev-bin linux-libc-dev <output snipped>
```

