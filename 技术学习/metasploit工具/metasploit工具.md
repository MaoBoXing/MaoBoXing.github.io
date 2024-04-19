# Metasploit简介

## 版本

Metsploit pro		 :  商业化，有图形化界面

Metasploit Framework : 开源版本，kali中安装此版本

## 组成

Msfconsole  	   :  主要的命令行界面

Modules（模块）  :   漏洞利用, 扫描器, 有效载荷等模块

Tools（工具）	:   **msfvenom**、pattern_create 和 pattern_offset等。

> 其中pattern_create 和 pattern_offset是漏洞利用开发总有用的工具。

##  Mesploit 模块

在深入研究模块之前，澄清一些反复出现的概念会很有帮助：exploit、vulnerability和payload。

- exploit：使用目标系统上存在的漏洞的一段代码

- vulnerability : 影响目标系统的设计、编码或者逻辑缺陷。

  > 此漏洞可导致机密信息泄露或允许攻击者在目标系统上执行代码。

- payload：漏洞利用时，如果我们希望漏洞利用能够获得想要的结果，就需要使用有效载荷。有效载荷就是将在目标机器上运行的代码。

### Auxiliary模块

任何用于支持的模块的可以在这里找到，比如scanners（扫描器）、crawlers（爬虫）、fuzzers（模糊测试）

```shell
root@:root#cd /opt/metasploit-framework/embedded/framework/modules/
root@:/opt/metasploit-framework/embedded/framework/modules# tree -L 1 auxiliary/
├── admin
├── analyze
├── bnat
├── client
├── cloud
├── crawler
├── docx
├── dos
├── example.py
├── example.rb
├── fileformat
├── fuzzers
├── gather
├── parser
├── pdf
├── scanner
├── server
├── sniffer
├── spoof
├── sqli
├── voip
└── vsploit

20 directories, 2 files
```

### Encoders模块

encoders模块允许对漏洞和payload进行编码，用于绕过基于签名的防病毒解决方案。

> 基于签名的防病毒软件具有已知威胁的数据库。通过将可疑文件与此数据库文件进行算法比对来检测威胁，匹配度较高时发出警报，因此Encoders模块的成功率可能有限，因为防病毒解决方案可以执行额外的检查。

```shell
root@root:/opt/metasploit-framework/embedded/framework/modules# tree -L 1 encoders/
encoders/
├── cmd
├── generic
├── mipsbe
├── mipsle
├── php
├── ppc
├── ruby
├── sparc
├── x64
└── x86
```

### Evasion模块

虽然encoders模块将对payload进行编码，但不应将其视为直接尝试逃避防病毒软件。使用规避模块，也许能成功。

```shell
root@root:/opt/metasploit-framework/embedded/framework/modules# tree -L 2 evasion/
evasion/
└── windows
    ├── applocker_evasion_install_util.rb
    ├── applocker_evasion_msbuild.rb
    ├── applocker_evasion_presentationhost.rb
    ├── applocker_evasion_regasm_regsvcs.rb
    ├── applocker_evasion_workflow_compiler.rb
    ├── process_herpaderping.rb
    ├── syscall_inject.rb
    ├── windows_defender_exe.rb
    └── windows_defender_js_hta.rb

1 directory, 9 files
```

### Exploit模块

漏洞利用，按目标组织攻击。

```shell
root@root:/opt/metasploit-framework/embedded/framework/modules# tree -L 1 exploits/
exploits/
├── aix
├── android
├── apple_ios
├── bsd
├── bsdi
├── dialup
├── example_linux_priv_esc.rb
├── example.py
├── example.rb
├── example_webapp.rb
├── firefox
├── freebsd
├── hpux
├── irix
├── linux
├── mainframe
├── multi
├── netware
├── openbsd
├── osx
├── qnx
├── solaris
├── unix
└── windows

20 directories, 4 files
```

NOPs（NOPs）

NOP是什么也不做。他们用0x90表示，cpu在一个周期内不会执行任何操作。它们通常用作缓冲区，以实现一致的有效负载大小。

```shell
root@root:/opt/metasploit-framework/embedded/framework/modules# tree -L 1 nops/
nops/
├── aarch64
├── armle
├── cmd
├── mipsbe
├── php
├── ppc
├── sparc
├── tty
├── x64
└── x86

10 directories, 0 files
```

### Payloads模块

payloads是即将在目标系统上运行的代码。

```shell
root@root:/opt/metasploit-framework/embedded/framework/modules# tree -L 1 payloads/
payloads/
├── adapters
├── singles
├── stagers
└── stages

4 directories, 0 files
```

payloads中存在四个文件夹，adapters、singles、stagers、stages

adapters：可以将payloads转换为不同的格式。例如，可以将一个普通payload加载到Powershell adapters中，将生成一个可以执行payloads的Powershell命令

