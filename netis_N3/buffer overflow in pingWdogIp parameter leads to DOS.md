## Buffer Overflow in "pingWdogIp" Parameter Leads to Denial-of-Service (DoS) in Netis N3Mv2-V1.0.1.865 Router

## Description

A significant security vulnerability has been uncovered in the Netis N3Mv2-V1.0.1.865 router firmware. This vulnerability triggers a buffer overflow in the "pingWdogIp" parameter, potentially causing a Denial-of-Service (DoS) condition. Exploiting this flaw could result in the router becoming unresponsive or crashing, affecting its normal operation.

![Router](images/1.png)

## Firmware Information

- **Manufacturer's Address:** [https://www.netis-systems.com](https://www.netis-systems.com)
- **Firmware Download Address:** [https://www.netisru.com/Support/downloads/dd/1/img/865](https://www.netisru.com/Support/downloads/dd/1/img/865)

## Affected Version

- **Version: Netis N3Mv2-V1.0.1.865**

## Vulnerability Details

The vulnerability arises in the handling of the "pingWdogIp" parameter within the Netis N3Mv2-V1.0.1.865 router's settings. Attackers can craft malicious input for this parameter, triggering a buffer overflow condition. When exploited, this vulnerability can disrupt the router's operation and potentially render it inaccessible.


## POC Video

[![Watch the video](https://img.youtube.com/vi/in0x_a2kz-U/maxresdefault.jpg)](https://youtu.be/F8V4YgQxy60)