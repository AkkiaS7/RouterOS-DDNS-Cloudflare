# RouterOS-DDNS-Cloudflare_PrivateDEV  
RouterOS script for Cloudflare DDNS using API_Token as authorization.  

### 一. 环境准备  
1. 你需要将 `JParseFunctions` 导入至RouterOS的 `scripts` 中  
导入后在RouterOS终端运行以下命令  
`/system script run "JParseFunctions"; global JSONLoad; global JSONLoads; global JSONUnload`  
2. 从Cloudflare获取API_TOKENS  
注意本脚本并不需要你的API_KEY与邮箱  
仅需要拥有 `编辑区域DNS` 权限的 `API_TOKENS` 即可完成任务  
3. 将 `ros-ddns-sample` 导入至RouterOS的 `scripts` 中  
你可能想要重命名并复制这个文件，如果你需要创建多个DDNS记录  
### 二. 使用脚本  
1. 根据 `ros-ddns-sample` 文件中的提示修改对应键值  
你需要输入的是 `uniqueID` , `WANInterface` , `CFdomain` , `CFzone` , `TTL` , `CFproxied` , `CFapitoken`  
2. `uniqueID` 必须唯一，它用于记录 `zoneID` 与`domainID`  
为多个DDNS脚本设置相同的 `uniqueID` 会导致DNS记录错误更新  
3. `TTL` 单位为秒  
4. `CFproxied` 用于开关 `Cloudflare's DNS Proxy` 功能  （橙色云朵图标）  
5. `WANInterface` 填入获取ip的目标接口名  
(pppoe拨号则填pppoe接口名)  

### 三. 清理  
1. RouterOS终端中运行 `$JSONUnload`  
这将自动清除所有 `JParseFunctions`加载的全局变量  
2. RouterOS终端中运行 `set $CFarray`  
这将删除本脚本所加载的全局变量  

### 四. 异常解决  
1. 几乎所有异常均可以通过移除 `CFarray` 全局变量解决  
在RouterOS终端中运行 `set $CFarray`  
在这之后脚本将会在下次运行时重新获取 `zoneID` 与 `domainID`  
2. 其他问题欢迎在issue中提出  

# Thanks: 
https://github.com/Winand/mikrotik-json-parser  
https://github.com/kiss2u/ros-cloudflare-ddns  