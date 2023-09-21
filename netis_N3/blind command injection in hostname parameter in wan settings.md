## Netis N3Mv2-V1.0.1.865 Router Blind Command Injection in Hostname Parameter in WAN Settings

## Description

A critical security vulnerability has been identified in the Netis N3Mv2-V1.0.1.865 router firmware, specifically within the WAN settings where the "Hostname" parameter is susceptible to blind command injection. This vulnerability allows an attacker to inject arbitrary OS commands via the "Hostname" parameter, potentially leading to unauthorized access or other malicious actions on the router.

![Router](images/1.png)

## Firmware Information

- **Manufacturer's Address:** [https://www.netis-systems.com](https://www.netis-systems.com)
- **Firmware Download Address:** [https://www.netisru.com/Support/downloads/dd/1/img/865](https://www.netisru.com/Support/downloads/dd/1/img/865)

## Affected Version

- **Version: Netis N3Mv2-V1.0.1.865**

## Vulnerability Details

The vulnerable aspect of the firmware lies in the handling of the "Hostname" parameter within WAN settings. Attackers can craft malicious input for the "Hostname" field, leading to blind command injection. This allows malicious actors to execute arbitrary OS commands on the router.

## POC Video

[![Watch the video](https://img.youtube.com/vi/IxfQg_3SV9o/maxresdefault.jpg)](https://youtu.be/IxfQg_3SV9o)