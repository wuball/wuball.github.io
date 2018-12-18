#### 问题描述
使用 `Windows Server 2012 R2` 或 `Windows Server 2016`系统，发现在安装 `.net 3.5.1` 时报错，报错内容如下

<!-- ![](https://raw.githubusercontent.com/wuball/img/master/24256887952783693328925795283587.jpg) -->

#### 原因分析
找不到安装源文件。

#### 解决办法
可以通过如下 `PowerShell` 脚本进行安装

1. 从开始菜单中找到 `PowerShell`，右击选择 以管理员身份运行     
2. 输入如下脚本后回车执行               




```
Set-ItemProperty -Path 'HKLM:\SOFTWARE\Policies\Microsoft\Windows\WindowsUpdate\AU' -Name UseWUServer -Value 0

Restart-Service -Name wuauserv

Install-WindowsFeature Net-Framework-Core

Set-ItemProperty -Path 'HKLM:\SOFTWARE\Policies\Microsoft\Windows\WindowsUpdate\AU' -Name UseWUServer -Value 1

Restart-Service -Name wuauserv
```
未知意外
如果未顺利执行，请检查 “windows update 服务”是否能正常启动