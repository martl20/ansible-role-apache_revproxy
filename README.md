[![Build Status](https://drone.element-networks.nl/api/badges/Ansible/role-apache_revproxy/status.svg)](https://drone.element-networks.nl/Ansible/role-apache_revproxy)

# Ansible role to configure Apache as reverse proxy
This role provides a means to configure Apache as a reverse proxy on RedHat/CentOS systems.

It will install apache and provide a template for generic reverse proxy configurations.

Check [defaults/main.yml](the defaults file) for an example setup.

## Kerberos with IPA
When using Kerberos with IPA, this role can create the Kerberos principal in IPA, this requires
a user with administrative privileges for the desired host.

## PAM authentication
To make Apache authenticate users over PAM requires a little extra work (this role does not do it for you, yet)

First of all, make sure that you have ```mod_authnz_pam``` installed on your system

Then fix some permissions and set up SELinux:
```
setsebool -P httpd_mod_auth_pam 1
groupadd shadow
chown root:shadow /etc/shadow /usr/sbin/unix_chkpwd
chmod 6755 /usr/sbin/unix_chkpwd
chmod 0040 /etc/shadow
```

Note that this will probably break when you install updates!
