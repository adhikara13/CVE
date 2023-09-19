## Netis N3Mv2-V1.0.1.865 Router Diagnostic Tools (Ping and Traceroute) OS Command Injection Vulnerability with Bypassable Mitigations

## Description

A critical security vulnerability has been identified in the Netis N3Mv2-V1.0.1.865 router firmware, specifically within the diagnostic tools page for the ping and traceroute functions. This vulnerability allows an authenticated remote attacker to inject arbitrary OS commands via HTTP, bypass command injection mitigations, and execute commands as the root user, potentially leading to unauthorized access or other malicious actions on the router.

![image-1](images/1.png)

## Firmware Information

* Manufacturer's Address: [https://www.netis-systems.com](https://www.netis-systems.com)
* Firmware Download Address: [https://www.netisru.com/Suppory/downloads/dd/1/img/526](https://www.netisru.com/Suppory/downloads/dd/1/img/526)

## Affected Version

**Version: Netis N3Mv2-V1.0.1.865**

## Vulnerability Details

This is the vulnerable part of the code:

```
undefined4 FUN_0040bd60(undefined4 param_1,undefined4 param_2)

{
  int iVar1;
  char *pcVar2;
  char *__nptr;
  size_t sVar3;
  hostent *phVar4;
  uint local_a8;
  char acStack148 [136];
  
  memset(acStack148,0,0x80);
  iVar1 = access("/tmp/result",0);
  if (iVar1 != 0) {
    remove("/tmp/result");
  }
  pcVar2 = (char *)FUN_00404308(param_1,param_2);
  iVar1 = atoi(pcVar2);
  if (iVar1 != 0) {
    pcVar2 = (char *)FUN_00404308(param_1,"IpAddr");
    __nptr = (char *)FUN_00404308(param_1,&DAT_00416544);
    iVar1 = atoi(__nptr);
    for (local_a8 = 0; sVar3 = strlen(pcVar2), local_a8 < sVar3; local_a8 = local_a8 + 1) {
      if ((((pcVar2[local_a8] == ' ') || (pcVar2[local_a8] == '|')) || (pcVar2[local_a8] == ';')) ||
         (pcVar2[local_a8] == '&')) {
        RunSystemCmd("echo \'\' > %s &","/tmp/result");
        return 0x7e;
      }
    }
    if (iVar1 == 1) {
      sprintf(acStack148,"ping -c 4 -s 56 %s -W 1000 > %s &",pcVar2,"/tmp/result");
    }
    else if (iVar1 == 2) {
      sprintf(acStack148,"traceroute -I -m 20 %s > %s &",pcVar2,"/tmp/result");
      phVar4 = gethostbyname(pcVar2);
      if ((phVar4 != (hostent *)0x0) && (phVar4->h_addrtype == 10)) {
        sprintf(acStack148,"rltraceroute6 -I -m 20 %s > %s &",pcVar2,"/tmp/result");
      }
    }
    system(acStack148);
  }
  return 0x7e;
}
```
We can see that it already implements some kind of filter for space, |, ;, and &:
``` 
for (local_a8 = 0; sVar3 = strlen(pcVar2), local_a8 < sVar3; local_a8 = local_a8 + 1) {
      if ((((pcVar2[local_a8] == ' ') || (pcVar2[local_a8] == '|')) || (pcVar2[local_a8] == ';')) ||
         (pcVar2[local_a8] == '&')) {
        RunSystemCmd("echo \'\' > %s &","/tmp/result");
        return 0x7e;
      }
    }
```
However, the problem with this vulnerability is that it doesn't block backticks '`' and dollar signs '$', which can also be used for attacks, including command injection.

To enhance security, it's advisable to use a 'whitelisting' approach instead of 'blacklisting'. Whitelisting means specifying which characters or patterns are allowed, making it much harder for attackers to exploit vulnerabilities, including command injection.

## POC Video

[![Watch the video](https://img.youtube.com/vi/QX_-Fht7cQA/maxresdefault.jpg)](https://youtu.be/QX_-Fht7cQA)