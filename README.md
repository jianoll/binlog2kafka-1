#### binlog2kafka

---

**简述**

>   数据实时同步中间件（阿里canal到kafka）！

 本项目是打通canal、kafka的桥梁；  
 基本原理：  
 canal解析binlog的数据，由syncClient订阅，然后实时推送到kafka；如果kafka服务异常，syncClient会回滚操作；canal、kafka异常退出，都不会影响数据的传输；


改写自:[syncClient](https://github.com/sasou/syncClient)


---

**配置说明：**

#client  
debug=1           # 是否开始调试：1未开启，0为关闭（线上运行请关闭）  
ip=127.0.0.1      # canal 服务端 ip  
port=11111        # canal 服务端 端口：默认11111  
destination=one   # canal 服务端 项目  
username=         # canal 用户名：默认为空  
password=         # canal 密码：默认为空  
filter=           # canal 同步表设置，默认空使用canal配置；  

#kafka  
kafkaIp=          # kafka 服务端 ip  
kafkaPort=        # kafka 端口：默认9092；  

---

**使用场景(基于日志增量订阅&消费支持的业务)：**

数据库镜像  
数据库实时备份  
多级索引 (分库索引)  
search build  
业务cache刷新  
数据变化等重要业务消息  


---
**docker 使用**
```
docker run --name binlog2kafka ruoyuchen/binglog2kafka \
	-e "CANAL_SERVER_IP=127.0.0.1" \
        -e "CANAL_SERVER_PORT=11111" \
        -e "DESTINATION=example" \
        -e "FILTER=.*" \
	-e "KAFKA_SERVERS=localhost:9092"
	
```
