npm : 无法加载文件 C:\Program Files\nodejs\npm.ps1，因为在此系统上禁止运行脚本。有关详细信息，请参阅 https:/go.microsoft.com/fwlink/?LinkID=135170 中的 about_Execution_Policies。  
所在位置 行:1 字符: 1
+ npm add -D vitepress@next
+ ~~~
    + CategoryInfo          : SecurityError: (:) []，PSSecurityException
    + FullyQualifiedErrorId : UnauthorizedAccess

Soluton：
这个错误是由于Windows PowerShell的执行策略限制导致的，默认设置为Restricted会阻止所有脚本运行

以下是几种解决方案：

以管理员身份修改执行策略
‌以管理员身份运行PowerShell‌：

在开始菜单搜索"PowerShell"
右键点击"Windows PowerShell"，选择"以管理员身份运行"

‌检查当前执行策略‌：

powershell
Copy Code
Get-ExecutionPolicy
‌修改执行策略‌（推荐使用RemoteSigned）

powershell
Copy Code
Set-ExecutionPolicy RemoteSigned
系统提示确认时输入Y并回车

其他解决方案
‌临时解决方案‌（仅当前会话有效）

powershell
Copy Code
Set-ExecutionPolicy -Scope Process -ExecutionPolicy Bypass
‌用户级修改‌（不影响其他用户）

powershell
Copy Code
Set-ExecutionPolicy RemoteSigned -Scope CurrentUser
‌替代方法‌：使用CMD命令提示符执行npm命令，CMD不受PowerShell执行策略限制

安全建议
修改执行策略时，建议选择RemoteSigned而非Unrestricted，因为RemoteSigned允许运行本地脚本，但对从互联网下载的脚本要求数字签名，在安全性和便利性之间取得较好平衡

操作完成后，可以运行Get-ExecutionPolicy验证策略是否已成功更改

  
Windows PowerShell
版权所有（C） Microsoft Corporation。保留所有权利。

安装最新的 PowerShell，了解新功能和改进！https://aka.ms/PSWindows

PS C:\WINDOWS\system32> Set-ExecutionPolicy RemoteSigned

执行策略更改
执行策略可帮助你防止执行不信任的脚本。更改执行策略可能会产生安全风险，如 https:/go.microsoft.com/fwlink/?LinkID=135170
中的 about_Execution_Policies 帮助主题所述。是否要更改执行策略?
[Y] 是(Y)  [A] 全是(A)  [N] 否(N)  [L] 全否(L)  [S] 暂停(S)  [?] 帮助 (默认值为“N”): y
PS C:\WINDOWS\system32> Get-ExecutionPolicy