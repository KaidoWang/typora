![xu'y](work.assets/数据库E-R图.png)

需要启动的应用类：

![image-20210719105954491](work.assets/image-20210719105954491.png)



报表的数据定义：

ReportTable类对应整个报表表格======》![image-20210719095408715](work.assets/image-20210719095408715.png)

```
t_business_vcard_detail
```

784279041

### 平台账号密码

WebCatEE:	 账号：wangkaidong
					    密码：123Vxiao



![image-20210727115321422](work.assets/image-20210727115321422.png)

```
// 2.调用消息中心能力 创建消息
if(!Objects.isNull(message)){
    // 创建消息
    msgExtDTO.setCreateParentType(createParentType.get(message.getType())==null?"0":createParentType.get(message.getType()));
    message = messageCenterService.create(msgExtDTO);
}
```

这段代码的判断是否出现错误？在第一部已经用应用的业务类创建完消息，这个判断是不是应该取消掉感叹号。



### 消息组件流程

```java
MessageController——》MessageHandler-》MessageComponentFacade-》具体业务实现类
```

### 报表组件流程

```java
ReportController--》ReportHandler--》具体业务实现类
```





fix:报表组件:S5报表组件接入  791027271

### 消费重构方案

vposConsume方法：

涉及的实体类：传入VcardDetail类 ----》 （TransactionDetailDTO类  ----》TransactionDetail类）  ----》返回TransactionResultDTO类

对应的数据库：



### 业务数据同步到大数据数据

#### 第一种：发送mq

​	1:在原有的业务类修改完数据发送mq![image-20210813105306494](work.assets/image-20210813105306494.png)

​	2:注入队列的消费者

![image-20210813105413057](work.assets/image-20210813105413057.png)

​	3:建立监听器，根据Apptype进行具体业务分类监听

![image-20210813105453555](work.assets/image-20210813105453555.png)

4:具体业务的监听器

![image-20210813105656906](work.assets/image-20210813105656906.png)

5：服务类实现

![image-20210813105803600](work.assets/image-20210813105803600.png)

