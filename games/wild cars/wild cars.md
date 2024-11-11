basic game flow & rpc functions

rpc原则
自己本地要不要执行？
是发送输入给服务器还是说直接同步状态给所有人？
## client
- 选择职业并且连接大厅 - 是否需要登录功能？加入没有登录，那么信息需要带上玩家名字？
- 进入房间。
- 获取组队信息以及其他玩家信息 (server call, client do)
- 开始游戏 (server call, client do)
- 接受自己、别人车的位置 (server call, client do)
### driver
- 发送自己车子位置、方向 (client call, server do, 但自己不执行.这个有点没想明白，需不需要server再发一个rpc，还是直接server do就会转发给其他所有clients)(这个要不要单独给partner发一个ordered？会不会性能好点？其他的发个unordered?)
- 接受guider的指路信息 (client call, rpc_id(partner))
### guider
- 发送指路信息

## server
### 大厅server （websocket？）
- 接受玩家连接
- 接受玩家职业以及名字
- 拉起房间server,并且告知client连接大厅server
- 可能需要注册啥的(option)

### 房间server
- 接受玩家连接
- 接受玩家职业以及名字
- 给玩家分组，并将结果告知玩家。
- 接受玩家地图加载完成信息
- 发送game start
