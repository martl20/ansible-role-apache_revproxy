[![Build Status](https://drone.element-networks.nl/api/badges/Ansible/role-apache_revproxy/status.svg)](https://drone.element-networks.nl/Ansible/role-apache_revproxy)

# Ansible role to configure Apache as reverse proxy
This role provides a means to configure Apache as a reverse proxy on RedHat/CentOS systems.

It will install apache and provide a template for generic reverse proxy configurations.

Check [defaults/main.yml](the defaults file) for an example setup.

## Kerberos with IPA
When using Kerberos with IPA, this role can create the Kerberos principal in IPA, this requires
a user with administrative privileges for the desired host.

If you are using HBAC rules in IPA, you can limit access to the proxied application by setting ```hbac_service```,
this will limit access to the entire app to users that match the HBAC rule. The role will configure the required
steps in PAM (creating the authentication policy file and setting up SELinux when required).

If you require more fine-grained access control, you'll need to make a custom template.

## PAM authentication (with local users)
To make Apache authenticate local users via PAM requires a little extra work

Then fix some permissions and set up SELinux:
```
groupadd shadow
chown root:shadow /etc/shadow /usr/sbin/unix_chkpwd
chmod 6755 /usr/sbin/unix_chkpwd
chmod 0040 /etc/shadow
```

Note that this will probably break when you install updates!
