## Buffer Overflow in "hostname" Parameter Leads to Denial-of-Service (DoS) in Netis N3Mv2-V1.0.1.865 Router

## Description

A critical vulnerability has been discovered in the Netis N3Mv2-V1.0.1.865 router firmware, which results in a Denial-of-Service (DoS) condition due to a buffer overflow in the "hostName" parameter. This flaw arises from improper handling of certain inputs in the "hostName" field, allowing attackers to overflow the buffer and disrupt the router's functionality, leading to network disruptions.

![Router](images/1.png)

## Firmware Information

- **Manufacturer's Address:** [https://www.netis-systems.com](https://www.netis-systems.com)
- **Firmware Download Address:** [https://www.netisru.com/Support/downloads/dd/1/img/865](https://www.netisru.com/Support/downloads/dd/1/img/865)

## Affected Version

- **Version: Netis N3Mv2-V1.0.1.865**

## Vulnerability Details

The vulnerability is rooted in the "hostname" parameter, where improper input handling leads to a buffer overflow. Attackers can craft malicious input for the "hostName" field, causing a buffer overflow and triggering a DoS condition. As a result, the router becomes unresponsive, disrupting network services and causing network outages.

## Vulnerable function

```c
void FUN_0040dabc(undefined4 param_1,char **param_2)

{
  int iVar1;
  undefined4 local_30;
  char local_2c [36];
  
  local_30 = 0xffffffff;
  FUN_0040d480();
  iVar1 = atoi(*param_2);
  if (iVar1 == 2) {
    RunSystemCmd("flash reset");
  }
  FUN_0040d8b8();
  FUN_0040d950();
  apmib_get(0x158,local_2c);
  RunSystemCmd("hostname %s &",local_2c);   <----------
  apmib_get(0x159,local_2c);
  RunSystemCmd("echo \'%s\' > %s",local_2c,"/proc/rtl_dnstrap/domain_name");
  apmib_get(0x130,local_2c);
  if (local_2c[0] == '\0') {
    RunSystemCmd("flash gen-wsc-pin");
  }
  RunSystemCmd("rm /var/log/log_split > /dev/null 2>&1");
  RunSystemCmd("echo 7 > /var/log/log_split");
  RunSystemCmd("syslogd -L -s 8 -b 7 &");
  RunSystemCmd("klogd &");
  RunSystemCmd("watchdog 1000&");
  RunSystemCmd("NetisDaemon&");
  GetIPTVStatus();
  FUN_0040f450(param_1,param_2);
  FUN_00408dd0(param_1,param_2);
  FUN_00408f60(param_1,param_2);
  FUN_0040d0c0(param_1,param_2);
  FUN_0040fc00(param_1,param_2);
  RunSystemCmd(&DAT_0041cf28);
  FUN_004035e0(param_1,param_2);
  iVar1 = getWanPhyLink(&DAT_0041ce20);
  if ((iVar1 < 0) || (iVar1 = GetWANIP_Status(), iVar1 < 1)) {
    apmib_get(0x153,&local_30);
    StartupDnsMasqForDHCPserver();
  }
  RunSystemCmd("auto_update&");
  return;
}
```

The local_2c buffer is limited to 36, and it is vulnerable to buffer overflow because apmim_get does not check user input.
## POC Video

[![Watch the video](https://img.youtube.com/vi/in0x_a2kz-U/maxresdefault.jpg)](https://youtu.be/7QtOXkM-Kyw)