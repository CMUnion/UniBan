# UniBan
A universal Minecraft player management system.  
一个联合Minecraft玩家管理系统。

## What is UniBan? UniBan是什么？
UniBan is a universal cross-server Minecraft player management system. It can help server operators to accomplish cross-platfrom cross-server player management, and help establishing a better Minecraft gamming community together.  
UniBan是一个跨服务器的Minecraft联合玩家管理系统。它可为各服务器管理员实现跨平台跨服务器的玩家管理，并帮助一同建立更好的Minecraft游戏环境。

## Objective 目标
1. 根据玩家的credit自动封禁玩家
1. 傻瓜式操作，使用者只需要设置他能接受的ban_level和由UniBan分配的key，就可以自动化实现跨服ban和unban管理。只需要使用/ban和/unban指令。
1. 减少人工干预。ban操作不需要二次审核。
1. 根据服务器在线时间、信誉、采用正态分布，计算玩家的credit。
1. 抵抗恶意数据。
1. 多语言支持
1. BungeeCord+多服务器（多个分服）支持
1. 提供玩家申诉渠道（计划中）
1. 同时支持正版/离线服务器（计划中）

## Functions 实现
### 插件
1. 服务器管理员向UniBan平台申请key
1. 服务器安装UniBan插件后，将key填入配置文件，并设置可接受的玩家credit
1. 管理员只需要/ban，/unban和/banlist指令，没有什么/global ban这些多余的累赘  
    `/ban <玩家> <理由> <时长> <是否仅在本分服>`  
    `/unban <玩家>`  
    `/banlist`
1. 如果玩家/玩家的IP credit低于设定值，则显示提示（包括封禁理由关键词）并自动ban出本服，管理员可以使用/unban手动解除封禁
1. 离线服务器根据名字和IP/所在地域等判断玩家credit（计划中）
1. 未获取key的服务器可以使用UniBan API查询玩家credit
1. 服务器关闭后自动向API注销AccessToken
1. 允许服务器直接在后台使用指令（/uniban register <email>）注册并自动设置key（计划中）
1. 服务器本地缓存（计划中）
1. ...
### UniBan平台
1. 全站HTTPS
1. 服务器管理员注册后给予唯一key，并设定有效期。注册需要有效邮箱（非10分钟邮箱）并验证，以后可考虑实名制（手机验证）。
1. 玩家申诉渠道（计划中），人工审核（邀请制或）
1. 查询服务，服务器管理员可以方便地查询自己的每个（分）服务器都手动处理了哪些玩家，以及玩家搜索服务。
1. ...
### UniBan API
1. 强制HTTPS
1. 限制每个key可以应用的服务器数量，具体方法是，每次服务器启动的时候都需要向API申请具有一定有效期的AccessToken，服务器使用这个AccessToken访问API（提交封禁/解禁/查询等），并限制AccessToken数量。
1. 计算服务器的weight
1. 根据提交封禁的服务器在线时间、信誉（weight）、玩家在线时长等、采用正太分布，计算玩家的credit。（具体算法构思中）
1. 同时支持正版/离线服务器，根据IP和所在区域（计划中）
1. 提取封禁理由关键词（计划中）。a服务器/ban人的时候理由可以随便填而不是填什么“破坏代码”。然后API再提取关键词，最后check的时候显示这些关键词，这样b服务器就对这个被别人ban了的玩家有概念了
1. 允许注销AccessToken
1. check的时候记录这个玩家被check次数，用于计算credit。因安全原因（防止破解），此数据不建议对外公开。
1. ...
1. 具体请看[API wiki](https://github.com/CMUnion/UniBan-API/wiki)
