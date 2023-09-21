## Netis N3Mv2-V1.0.1.865 Router Blind Command Injection in Hostname Parameter in WAN Settings

## Description

A critical security vulnerability has been discovered in the Wake-On-LAN (WoL) functionality of the Netis N3Mv2-V1.0.1.865 router firmware. This vulnerability resides in the handling of the "wakeup_mac" parameter used for initiating WoL requests. An attacker can exploit this flaw to inject arbitrary OS commands via the "wakeup_mac" parameter, potentially leading to unauthorized access or other malicious actions on the router.

![Router](images/1.png)

## Firmware Information

- **Manufacturer's Address:** [https://www.netis-systems.com](https://www.netis-systems.com)
- **Firmware Download Address:** [https://www.netisru.com/Support/downloads/dd/1/img/865](https://www.netisru.com/Support/downloads/dd/1/img/865)

## Affected Version

- **Version: Netis N3Mv2-V1.0.1.865**

## Vulnerability Details

The vulnerability lies in the "wakeup_mac" parameter used for Wake-On-LAN functionality. Attackers can manipulate this parameter to perform blind command injection. By injecting malicious commands, malicious actors can potentially execute arbitrary OS commands on the router.


## POC Video

[![Watch the video](https://img.youtube.com/vi/in0x_a2kz-U/maxresdefault.jpg)](https://youtu.be/in0x_a2kz-U)