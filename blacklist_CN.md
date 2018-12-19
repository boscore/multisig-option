## bos配置通过多签上链

### 1.bos上链的主要有三个名单

增加到了eosio.system合约中，系统合约的action名字是namelist，具体的执行的操作如下：
```
cleos push action eosio  namelist  '{"list":"actor_blacklist","action":"insert","names":[boscorebos14]}'  -p eosio
```
其中详细解释

- 需要操作什么类型的黑名单list:
```
actor_blacklist
contract_blacklist	
resource_greylist
```
- 需要进行的动作action:
```
insert
remove
```
- 需要添加的用户名names:

这个黑名单功能保留了原来的config文件配置，也可以通过多签的方式上链。

## 准备工作：

1）首先先把前30个bp的权限列出来，写到文件中bppermission.json
```
[{"actor":"produceraaaa","permission":"active"},
{"actor":"producerbbbb","permission":"active"},
{"actor":"producercccc","permission":"active"},
{"actor":"producerdddd","permission":"active"},
{"actor":"producereeee","permission":"active"},
{"actor":"producerffff","permission":"active"},
{"actor":"producergggg","permission":"active"},
{"actor":"producerhhhh","permission":"active"},
{"actor":"produceriiii","permission":"active"},
{"actor":"producerjjjj","permission":"active"},
{"actor":"producerkkkk","permission":"active"},
{"actor":"producerllll","permission":"active"},
{"actor":"producermmmm","permission":"active"},
{"actor":"producernnnn","permission":"active"},
{"actor":"produceroooo","permission":"active"},
{"actor":"producerpppp","permission":"active"},
{"actor":"producerqqqq","permission":"active"},
{"actor":"producerrrrr","permission":"active"},
{"actor":"producerssss","permission":"active"},
{"actor":"producertttt","permission":"active"},
{"actor":"produceruuuu","permission":"active"},
{"actor":"producervvvv","permission":"active"},
{"actor":"producerwwww","permission":"active"},
{"actor":"producerxxxx","permission":"active"},
{"actor":"produceryyyy","permission":"active"},
{"actor":"producerzzzz","permission":"active"}]
```
## 开始多签操作：
增加黑名单
```
1)cleos multisig propose addblack1  bppermission1.json '[{"actor": "eosio", "permission": "active"}]'  eosio  namelist  '{"list":"actor_blacklist","action":"insert","names":["boscoretest1"]}' produceraaaa  168
  #删除黑名单
  #cleos multisig propose rmblack2 bppermission.json '[{"actor": "eosio", "permission": "active"}]'  eosio  namelist  '{"list":"actor_blacklist","action":"remove","names":["boscoretest1"]}' produceraaaa  168

2)cleos multisig approve  produceraaaa addblack1 '{"actor":"produceraaaa","permission":"active"}' -p produceraaaa

3)cleos multisig exec boscorebos11 addblack1  -p produceraaaa@active
```

- 如果配置了producer_api_plugin插件可以通过api查看
```curl --request POST --url http://127.0.0.1:8888/v1/producer/get_whitelist_blacklist```


