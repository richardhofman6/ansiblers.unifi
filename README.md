# unifi-controller-rhel

## About

Anisble playbook for installing UniFi Controller software for Ubiquiti
Access Points on RHEL 6

## Requirements

You need the EPEL Repository from Fedora Project enabled to be able to
install the requirements (MongoDB etc).

## Usage

You must download the ZIP of the UniFi Controller software from the Ubiquiti
website and save it to the same folder as the playbook as "UniFi.zip"

Optionally, update the playbook variable 'ntp_server' to point to your
preferred NTP server for the AP's to use.

The playbook will run against the "unifi_controllers" group in your Ansible
inventory:

    ansible-playbook unifi.play

## Support

There is none. Tested on CentOS 6 x86_64. Not tested on animals.

Your results may vary. Discontinue use and see a doctor if rash occurs.
