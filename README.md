UniFi Controller for RHEL (yum-based distros)
=============================================

Ansible Galaxy role for installing UniFi Controller software for Ubiquiti Access Points on RedHat/Centos/Amazon/Fedora and other yum-based distros.

**WARNING: This has only been tested on Amazon Linux so far, and may have issues in `/etc/yum.repos.d/mongodb-org-3.2.repo` for Fedora (probably need to use the /redhat/ mongo repo.) If you install this on any other distro besides Amazon Linux please comment with your experiences.**

Forked from https://github.com/fukawi2/unifi-controller-rhel and modified to be an includable role via Galaxy instead of a playbook.

Requirements
------------

- Ubiquiti's license does not allow redistribution of the software ZIP, so you must manually download the ZIP of the UniFi Controller software from the [Ubiquiti website](https://www.ubnt.com/download/unifi/) and save it to `files/UniFi.unix.zip`. The most recent tested version is "UniFi v5.0.6 Zip for DIY Unix/Linux" from 2016-06-01. If you are including this role via Galaxy, you may download this file to your playbook's `files` directory instead of this role's `files` directory; both will work.
- You may need the [EPEL Repository](https://fedoraproject.org/wiki/EPEL) from Fedora Project enabled for some packages, however Mongo is installed directly from mongo.org so try running without first.


Role Variables
--------------

- **unifi_controller_rhel_ntp_server** (optional) sets your preferred NTP server for the UniFi APs to use (default: `pool.ntp.org`)
- **unifi_controller_rhel_unifi_zip_file** (optional) sets the filename of the UniFi controller software on the Ansible system (default: `UniFi.unix.zip`)

Dependencies
------------

n/a

Example Playbook
----------------

First, install this role via Galaxy by typing `sudo ansible-galaxy install zyphlar.unifi_controller_rhel`

Then create and run an Ansible playbook like this:

    - hosts: your_unifi_controllers
      become: true
      roles:
        - zyphlar.unifi_controller_rhel

Or, if you want to override some variables:

    - hosts: your_unifi_controllers
      become: true
      roles:
        - some_other_role
        - role: zyphlar.unifi_controller_rhel
          unifi_controller_rhel_unifi_zip_file: UniFi.unix.5.0.6.zip

License
-------

BSD

Support
-------

There is none. Tested on CentOS 6 x86_64. Not tested on animals.

Your results may vary. Discontinue use and see a doctor if rash occurs.

Author Information
------------------

- [fukawi2](https://github.com/fukawi2) (Original)
- [zyphlar](https://github.com/zyphlar) (Ansible Galaxy version)

TODO
----

Possibly open up ports in iptables if it's enabled by default in some distros:

```
-A INPUT -m state --state NEW -m tcp -p tcp --dport 8081 -j ACCEPT
-A INPUT -m state --state NEW -m tcp -p tcp --dport 8080 -j ACCEPT
-A INPUT -m state --state NEW -m tcp -p tcp --dport 8443 -j ACCEPT
-A INPUT -m state --state NEW -m tcp -p tcp --dport 8843 -j ACCEPT
-A INPUT -m state --state NEW -m tcp -p tcp --dport 8880 -j ACCEPT
-A INPUT -m state --state NEW -m tcp -p tcp --dport 27117 -j ACCEPT

# service iptables restart
```