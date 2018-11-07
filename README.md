# JSNAPy Basics

[![Build Status](https://travis-ci.org/tplisson/ansible-basics.svg?branch=master)](https://travis-ci.org/tplisson/jsnapy-basics)

## Documentation Structure

[**1. Quick Ansible Demo**](README.md#-1.-Quick-JSNAPY-Demo)

[**2. More Advanced Stuff**](README.md#-2.-More-Advanced-Stuff)


# 1. Quick JSNAPy Demo
This is a short demo on the Juniper JSNAPy tool

More on JSNAPy here:
 - https://junos-ansible-modules.readthedocs.io
 - https://github.com/Juniper/jsnapy
 

---
## 1.1 Start a Docker container for the Ansible environment
Using a Docker container greatly simplifies the environment setup and it also keeps things clean and contained

```
docker pull juniper/jsnapy
docker run -it --rm -v $(pwd):/scripts juniper/jsnapy
```

Check the JSNAPy version
```
jsnapy --version
```

See Docker Hub for more info:
- https://hub.docker.com/r/juniper/jsnapy/

If you need access to some Junos devices for lab / testing purposes, you can run vSRX or vQFX vagrant images:

- vSRX image on Vagrant Cloud:
    - https://app.vagrantup.com/juniper/boxes/ffp-12.1X47-D15.4-packetmode
- vQFX image on Vagrant Cloud:
    - https://app.vagrantup.com/juniper/boxes/vqfx10k-re
- Examples of multi VMs topologies:
    - https://github.com/Juniper/vqfx10k-vagrant



## 1.2 Setup the Environment

Inventory "hosts" file located in my project directory
```ini
[mx]
mx1
mx2
```

Credentials for the default Junos devices username and password can be stored under:
- group_vars/all.yml
```ini
---
# Default username and password
device_user: lab
device_pass: lab123
```

## 1.3 First JSNAPy script
Let's create a simple script to verify the status of the interfaces

JSNAPy Configuration file in YAML format called "check_intf.yml":
```yaml
---
hosts:
  - device: mx1
    username : lab
    passwd: lab123
tests:
  - test_intf_no_diff.yml
```
JSNAPy Test file in YAML format called "test_intf_no_diff.yml":
```yaml
---
test_command_version:
  - command: show interfaces terse * 
  - iterate:
      xpath: physical-interface
      id: './name'
      tests:
        - no-diff: oper-status       # element in which test is performed
          err: "Test Failed!! oper-status  got changed, before it was <{{pre['oper-status']}}>, now it is <{{post['oper-status']}}>"
          info: "Test Passed!! oper-status is same, before it is <{{pre['oper-status']}}> now it is <{{post['oper-status']}}>"
```

Create a PRE snapshot
```
jsnapy --snap pre -f check_intf.yml
```

Create a POST snapshot
```
jsnapy --snap pre -f check_intf.yml
```

Compare the two snapshots
```
jsnapy --check pre post -f check_intf.yml
```


# 2. More Advanced Stuff
text

```
cli
```
## 2.1 subtitle
text

```
cli
```
## 2.2 subtitle
text

```
cli
```
## 2.3 subtitle
text

```
cli
```
## 2. subtitle
text

```
cli
```
## 2. subtitle
text

```
cli
```
## 2. subtitle
text

```
cli
```
## 2. subtitle
text

```
cli
```
## 2. subtitle
text

```
cli
```
## 2. subtitle
text

```
cli
```
## 2. subtitle
text

```
cli
```
