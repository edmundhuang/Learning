# CQRS - Command Query Responsibility Segregation，命令查询职责分离模式

1. [12 Things You Should Know About Event Sourcing](http://blog.leifbattermann.de/2017/04/21/12-things-you-should-know-about-event-sourcing/)
* An event is something that has happened in the past - 事件是发生在过去的事情。
* An event should be presented as a verb in past tense - 事件应该用过去式表达 
``` CS
class OnlineAccountCreated(int accountId){}
class DepositMade(int accountId, decimal depositAmount) {}
class MoneyWithdrawn(int accountId, decimal withdrawalAmount){}
``` 
* State is a first level derivative of the event stream - 状态是事件流的第一级派生对象  
This means that an object is persisted as a stream of events. There is no need anymore to map its structural model with all its properties to tables in a relational database.
这意味着一个对象被持久化为一系列事件。 不需要将其结构模型及所有属性映射到关系数据库中的表。  
* Every aggregate has its own event stream - 每个聚合都有自己的事件流
* The structure of an event and how to persist it - 事件的结构以及如何持久化
* Events are immutable - 事件是不可改变的
* Theres is no delete - 没有删除
* The `apply` function - 应用函数  
![Apply](./images/es-apply.svg)  
* 

2. [浅谈命令查询职责分离(CQRS)模式](https://www.cnblogs.com/yangecnu/p/Introduction-CQRS.html)
