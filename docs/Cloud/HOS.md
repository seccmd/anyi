# Commando-VM

https://github.com/mandiant/commando-vm

## Pre-Install Procedures

You MUST disable Windows Defender for a smooth install. 

1. You MUST disable Windows Defender for a smooth install. The best way to accomplish this is through Group Policy

   在1909及更高版本的Windows中，添加了防篡改保护**必须禁用篡改保护，否则将忽略组策略设置**

   1. 打开 Windows 安全中心 （系统搜索栏输入 Windows Security）
   2. 点击病毒和威胁保护 > 病毒和威胁防护设置 > 管理设置
   3. 关闭 篡改防护（无需更改任何其他设置（“实时保护”等））

   > **重点：**更改组策略设置之前，必须禁用篡改保护。

   永久禁用实时保护

   1. 打开本地组策略编辑器（系统搜索栏输入 gpedit ）
   2. Computer Configuration > Administrative Templates > Windows Components > Microsoft Defender Antivirus > Real-time Protection
   3. 计算机配置 > 管理模板 > Windows 组件 > Microsoft Defender 防病毒 > 实时保护
   4. 打开 “关闭实时保护” 选型 ，选择 “已启用”，点击 “应用” 确定。
   5. **重启系统**

   > 执行以下操作前，必须重启

   永久禁用微软防病毒

   1. 打开本地组策略编辑器（系统搜索栏输入 gpedit ）
   2. 计算机配置 > 管理模板 > Windows 组件 > Microsoft Defender 防病毒
   3. 打开 “关闭 Microsoft Defender 防病毒” 选型 ，选择 “已启用”，点击 “应用” 确定。
   4. **重启系统**

## Standard install

1. Create and configure a new Windows Virtual Machine

> Ensure VM is updated completely. You may have to check for updates, reboot, and check again until no more remain

1. Take a snapshot of your machine!
2. Download and copy `install.ps1` on your newly configured machine.
3. Open PowerShell as an Administrator
4. Unblock the install file by running `Unblock-File .\install.ps1`
5. Enable script execution by running `Set-ExecutionPolicy Unrestricted -f`
6. Finally, execute the installer script as follows:

- `.\install.ps1`
- You can also pass your password as an argument: `.\install.ps1 -password <password>`

The script will set up the Boxstarter environment and proceed to download and install the Commando VM environment. You will be prompted for the administrator password in order to automate host restarts during installation. If you do not have a password set, hitting enter when prompted will also work.




