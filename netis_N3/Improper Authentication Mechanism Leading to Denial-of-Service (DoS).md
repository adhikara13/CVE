## Netis N3Mv2-V1.0.1.865 Router Improper Authentication Mechanism Leading to Denial-of-Service (DoS)

## Description

A critical security vulnerability has been identified in the Netis N3Mv2-V1.0.1.865 router firmware. This vulnerability is attributed to an improper authentication mechanism in the handling of the 'Authorization' header.

![Router](images/1.png)

## Firmware Information

- **Manufacturer's Address:** [https://www.netis-systems.com](https://www.netis-systems.com)
- **Firmware Download Address:** [https://www.netisru.com/Support/downloads/dd/1/img/865](https://www.netisru.com/Support/downloads/dd/1/img/865)

## Affected Version

- **Version: Netis N3Mv2-V1.0.1.865**

## Vulnerability Details

The vulnerability is rooted in the way the authorization header is processed. A standard 'Authorization' header should contain parameters like 'Authorization: Digest username="", realm="", nonce="", uri="", response=""'. However, if, for instance, only 'Digest username="test"' is sent in the header, the server would cease to function (resulting in a denial of service). The issue likely stems from how the Boa web server handles HTTP headers.

## POC Video

[![Watch the video](https://img.youtube.com/vi/in0x_a2kz-U/maxresdefault.jpg)](https://youtu.be/5NHkUqSjvbY)