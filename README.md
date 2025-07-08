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