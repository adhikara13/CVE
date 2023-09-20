## Blind Command Injection in Netis N3Mv2-V1.0.1.865 Router's Changing Username and Password Feature

## Description

A critical security vulnerability has been identified in the Netis N3Mv2-V1.0.1.865 router firmware, specifically within the "Changing Username and Password" feature. This vulnerability allows an attacker to execute arbitrary commands on the router, potentially gaining unauthorized access and control over the device.

![image-1](images/1.png)

## Firmware Information

* Manufacturer's Address: [https://www.netis-systems.com](https://www.netis-systems.com)
* Firmware Download Address: [https://www.netisru.com/Suppory/downloads/dd/1/img/526](https://www.netisru.com/Suppory/downloads/dd/1/img/526)

## Affected Version

**Version: Netis N3Mv2-V1.0.1.865**

## Vulnerability Details

The vulnerable portion of the code resides in the "Changing Username and Password" feature:

```
void FUN_00408dd0(void)

{
  undefined auStack1160 [64];
  undefined auStack1096 [64];
  undefined auStack1032 [1024];
  
  memset(auStack1032,0,0x400);
  memset(auStack1160,0,0x40);
  memset(auStack1096,0,0x40);
  apmib_get(0x15d,auStack1160);
  apmib_get(0x15e,auStack1096);
  RunSystemCmd("echo \"root::0:0:root:/:/bin/sh\" > /var/passwd");
  RunSystemCmd("echo \"nobody:x:0:0:nobody:/:/dev/null\" >> /var/passwd");
  RunSystemCmd("echo \"%s::0:0:guest:/:/bin/sh\" >> /var/passwd",auStack1160);
  RunSystemCmd("echo %s:%s | chpasswd -m",auStack1160,auStack1096);
  RunSystemCmd("echo root:%s | chpasswd -m",auStack1096);
  RunSystemCmd("echo \"root:x:0:root\" > /var/group");
  RunSystemCmd("echo \"nobody:x:0:nobody\" >> /var/group");
  RunSystemCmd("echo \"%s:x:0:guest\" >> /var/group",auStack1160);
  RunSystemCmd("chmod 755 /var/passwd");
  RunSystemCmd("chmod 755 /var/group");
  fwrite("Changed Username and Password ...........\n",1,0x2a,stderr);
  return;
}
```
The code accepts user input for new usernames and passwords. Unfortunately, this input is not adequately validated, leading to a command injection vulnerability. An attacker can craft malicious usernames or passwords, such as ls, to execute arbitrary commands on the router, including downloading files through wget for out-of-band exploitation.


## POC Video

[![Watch the video](https://img.youtube.com/vi/pGxg0RLarSc/maxresdefault.jpg)](https://youtu.be/pGxg0RLarSc)