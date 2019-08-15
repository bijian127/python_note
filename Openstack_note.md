# Open Stack通用技术
## 1.消息总线
>设计原则：
> - 项目之间通过 `TESTful API` 进行通信
> - 项目内部，不同的进程之间的通信必须通过消息总线。

- -->保证对外服务的接口被不同类型客户端支持
- -->项目内部通信接口可扩展和可靠性，支持大规模部署
### `消息总线` 定义
>一些服务向总线发送消息，其他服务从总线上获取消息

### 1.1 OpenStack消息总线项目内部通信实现方法
>（oslo.messaging）
- `RPC` (Remote Procedure Call,远程过程调用)
  - `call` 调用，同步
  - `cast` 调用，异步
- `Event Notification` （事件通知）
  - 所有对此类事件的服务进程都可以获取此通知并进一步处理
  - 处理结果不会返回发送者
  - 可项目内部，可跨项目
  - ceilometer以此进行计量和监控
#### 1.1.1 `AMQP` (Advanced Message Queuing Protocol,高级消息队列协议)
- 异步消息传递
- 开放的应用层协议
- 包括消息导向、队列、路由、可靠性及安全性
- Oslomessaging支持AMQP0.9.1&1.0
- `AMQP`架构


img1-1 AMQP架构
