## Buffer Overflow in "servDomain" Parameter Leads to Denial-of-Service (DoS) in Netis N3Mv2-V1.0.1.865 Router

## Description

A critical vulnerability has been discovered in the Netis N3Mv2-V1.0.1.865 router firmware, which results in a Denial-of-Service (DoS) condition due to a buffer overflow in the "servDomain" parameter. This flaw arises from improper handling of certain inputs in the "servDomain" field, allowing attackers to overflow the buffer and disrupt the router's functionality, leading to network disruptions.

![Router](images/1.png)

## Firmware Information

- **Manufacturer's Address:** [https://www.netis-systems.com](https://www.netis-systems.com)
- **Firmware Download Address:** [https://www.netisru.com/Support/downloads/dd/1/img/865](https://www.netisru.com/Support/downloads/dd/1/img/865)

## Affected Version

- **Version: Netis N3Mv2-V1.0.1.865**

## Vulnerability Details

The vulnerability is rooted in the "servDomain" parameter, where improper input handling leads to a buffer overflow. Attackers can craft malicious input for the "servDomain" field, causing a buffer overflow and triggering a DoS condition. As a result, the router becomes unresponsive, disrupting network services and causing network outages.


## POC Video

[![Watch the video](https://img.youtube.com/vi/in0x_a2kz-U/maxresdefault.jpg)](https://youtu.be/zKZpjrLzMF4)