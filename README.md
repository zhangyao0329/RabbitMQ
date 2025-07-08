```Shell
docker run \
 -e RABBITMQ_DEFAULT_USER=itheima \
 -e RABBITMQ_DEFAULT_PASS=123321 \
 -v mq-plugins:/plugins \
 --name mq \
 --hostname mq \
 -p 15672:15672 \
 -p 5672:5672 \
 --network hm-net\
 -d \
 rabbitmq:3.8-management
```

```http
http://192.168.152.128:15672/#/
```

# mq

![](https://github.com/zhangyao0329/tuchuang-blog/raw/main/tuchuang-blog/2025/07/08-7c3631ef4ea6a0e937c3d6f1db1544d4-image-20250708185741019.png)

![](https://github.com/zhangyao0329/tuchuang-blog/raw/main/tuchuang-blog/2025/07/08-8f63475a9b5e9507e1e9ca9aecc9b54c-image-20250708190007339.png)



## Spring-AMQP 如何收发消息？

![](https://github.com/zhangyao0329/tuchuang-blog/raw/main/tuchuang-blog/2025/07/08-13389a61a8604f0e9778677252f433d8-image-20250708190813833.png)

![](https://github.com/zhangyao0329/tuchuang-blog/raw/main/tuchuang-blog/2025/07/08-bf87fd25a23017370e21927b19168d3d-image-20250708190849989.png)

![](https://github.com/zhangyao0329/tuchuang-blog/raw/main/tuchuang-blog/2025/07/08-425e18871842a31b3b916af56bf9adf3-image-20250708191257748.png)

![](https://github.com/zhangyao0329/tuchuang-blog/raw/main/tuchuang-blog/2025/07/08-b08457081627debe76de02a4a46145fe-image-20250708220537800.png)

![总结](https://github.com/zhangyao0329/tuchuang-blog/raw/main/tuchuang-blog/2025/07/08-6c6a1f1ce3fff687275b7b5d79ddc639-image-20250708220603081.png)



## WorkQueues模型

![](https://github.com/zhangyao0329/tuchuang-blog/raw/main/tuchuang-blog/2025/07/08-c2418f8feaf604aef21d35cc57e29678-image-20250708220755671.png)

![](https://github.com/zhangyao0329/tuchuang-blog/raw/main/tuchuang-blog/2025/07/08-579f7fb957373a06ec94266b8d5ea46e-image-20250708220844654.png)





## 交换机

![](https://github.com/zhangyao0329/tuchuang-blog/raw/main/tuchuang-blog/2025/07/08-57005ee0de990e041207026ac011bffe-image-20250708220913000.png)

![](https://github.com/zhangyao0329/tuchuang-blog/raw/main/tuchuang-blog/2025/07/08-af1a607ac1ed05f7907e239f7732d114-image-20250708220940144.png)

![](https://github.com/zhangyao0329/tuchuang-blog/raw/main/tuchuang-blog/2025/07/08-d920532df94eb56da35178a39a24073b-image-20250708220956034.png)



![](https://github.com/zhangyao0329/tuchuang-blog/raw/main/tuchuang-blog/2025/07/08-5e35da12736af6cca4ecb018925fda19-image-20250708221012415.png)

![](https://github.com/zhangyao0329/tuchuang-blog/raw/main/tuchuang-blog/2025/07/08-f606e756cc75b40d9f92e6e815f8a5b5-image-20250708221037725.png)

![](https://github.com/zhangyao0329/tuchuang-blog/raw/main/tuchuang-blog/2025/07/08-e8983c1d12f3dfc6b96f1c905afa0992-image-20250708221118708.png)



## 消息可靠性

### 发送者重连

![](https://github.com/zhangyao0329/tuchuang-blog/raw/main/tuchuang-blog/2025/07/08-27bee5c5ee11ec72b481c2147d45b3d5-image-20250708231601635.png)

### 发送者确认

![](https://github.com/zhangyao0329/tuchuang-blog/raw/main/tuchuang-blog/2025/07/08-e90593f2347756f184621400f346c827-image-20250708232041058.png)

![](https://github.com/zhangyao0329/tuchuang-blog/raw/main/tuchuang-blog/2025/07/08-37294a082ceda0a842360eb7ea97d19d-image-20250708232140973.png)

![](https://github.com/zhangyao0329/tuchuang-blog/raw/main/tuchuang-blog/2025/07/08-a5f1ca010584623d5dba8fb591b5fe00-image-20250708232444358.png)

![](https://github.com/zhangyao0329/tuchuang-blog/raw/main/tuchuang-blog/2025/07/08-fe6af19b4d647688a4aac117373054e3-image-20250708232921190.png)

```Java
@Test
void testPublisherConfirm() {
    // 1.创建CorrelationData
    CorrelationData cd = new CorrelationData();
    // 2.给Future添加ConfirmCallback
    cd.getFuture().addCallback(new ListenableFutureCallback<CorrelationData.Confirm>() {
        @Override
        public void onFailure(Throwable ex) {
            // 2.1.Future发生异常时的处理逻辑，基本不会触发
            log.error("send message fail", ex);
        }
        @Override
        public void onSuccess(CorrelationData.Confirm result) {
            // 2.2.Future接收到回执的处理逻辑，参数中的result就是回执内容
            if(result.isAck()){ // result.isAck()，boolean类型，true代表ack回执，false 代表 nack回执
                log.debug("发送消息成功，收到 ack!");
            }else{ // result.getReason()，String类型，返回nack时的异常描述
                log.error("发送消息失败，收到 nack, reason : {}", result.getReason());
            }
        }
    });
    // 3.发送消息
    rabbitTemplate.convertAndSend("hmall.direct", "q", "hello", cd);
}
```

### MQ数据持久化

![](https://github.com/zhangyao0329/tuchuang-blog/raw/main/tuchuang-blog/2025/07/08-4b09d55eaaf41273a8235d65fcadbe7f-image-20250708234836679.png)

- 交换机持久化
- 队列持久化
- 消息持久化

![](https://github.com/zhangyao0329/tuchuang-blog/raw/main/tuchuang-blog/2025/07/08-9dab863b94fa89656a6bf10fce46b526-image-20250708235456565.png)

![](https://github.com/zhangyao0329/tuchuang-blog/raw/main/tuchuang-blog/2025/07/08-65c9d3bb2cad8fd8442fe41f72aa6406-image-20250708235525375.png)

![](https://github.com/zhangyao0329/tuchuang-blog/raw/main/tuchuang-blog/2025/07/08-9a5331b969da82d6172572d11526dd92-image-20250708235633169.png)

消费者确认

![](https://github.com/zhangyao0329/tuchuang-blog/raw/main/tuchuang-blog/2025/07/09-7a6961c9c114ba29dc209c226be95a47-image-20250709000159818.png)

![](https://github.com/zhangyao0329/tuchuang-blog/raw/main/tuchuang-blog/2025/07/09-3606f03cda5ed2c29f3eef655588b1b3-image-20250709000303677.png)

![](https://github.com/zhangyao0329/tuchuang-blog/raw/main/tuchuang-blog/2025/07/09-c912bc93ef898f6cb624019bd84216c2-image-20250709000540812.png)

![](https://github.com/zhangyao0329/tuchuang-blog/raw/main/tuchuang-blog/2025/07/09-a429475066e59c644aa40823a2bed774-image-20250709000847092.png)