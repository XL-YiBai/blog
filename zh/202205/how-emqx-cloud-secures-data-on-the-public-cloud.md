数字时代，数据逐渐成为企业的核心价值和重要资产，数据安全对于每一个企业来说都举足轻重。在网络环境复杂的当下，企业急需重视企业数据的安全问题。

作为一款全托管的 [MQTT 5.0](https://www.emqx.com/zh/mqtt/mqtt5) 公有云服务，[EMQX Cloud](https://www.emqx.com/zh/cloud) 提供了一站式运维代管、独有隔离环境的 MQTT 消息服务。EMQ 十分重视用户的数据安全性，因此在 EMQX Cloud 的产品设计中也特别注意了对数据安全的保障。即使是部署在公有云上，用户也无需担心数据泄漏等风险。

本文将从基础架构、数据通信、认证鉴权、权限管理、隐私数据安全这 5 个方面来解读 EMQX Cloud 的数据安全保障机制。

## 安全可靠的基础架构

EMQX Cloud 专业版采用高冗余集群架构，以确保服务的高可用性。通过独有隔离环境保障您的数据安全与业务稳定性，每个部署集群都拥有自己的公共 IP、专用 VPC 网络、独立 EMQX 服务器与数据库服务器，更加安全可靠。

## 通信协议加密保障数据安全

作为基于现代密码学公钥算法的安全协议，TLS/SSL 能在计算机通讯网络上保证传输安全。EMQX Cloud 支持 TLS/SSL 加密认证，包括支持单/双向认证、X.509 证书等多种安全认证。

我们不会将您上传的证书用于产品以外的用途，并且您可以随时删除您的证书信息。删除证书会断开客户端到 8883 和 8084 的连接，删除证书前请确保这不会影响到您的业务。

1. 登录 EMQX Cloud 控制台 。
2. 进入部署详情，点击 TLS/SSL 配置部分的证书「删除」按钮。
3. 在对话框点击「确定」，完成删除。


![单向 TLS/SSL 认证原理](https://assets.emqx.com/images/800d703cf32d4d553cd6d77ff3778a31.png)

<center>单向 TLS/SSL 认证原理</center>

![双向 TLS/SSL 认证原理](https://assets.emqx.com/images/8e48d965a059d44db0b9458823464619.png)

<center>双向 TLS/SSL 认证原理</center>

SSL/TLS 可以带来以下安全优势：

- **强认证。** 用 TLS 建立连接的时候，通讯双方可以互相检查对方的身份。在实践中，很常见的一种身份检查方式是检查对方持有的 X.509 数字证书。这样的数字证书通常是由一个受信机构颁发的，不可伪造。
- **保证机密性**。TLS 通讯的每次会话都会由会话密钥加密，会话密钥由通讯双方协商产生。任何第三方都无法知晓通讯内容。即使一次会话的密钥泄露，并不影响其他会话的安全性。
- **完整性。** 加密通讯中的数据很难被篡改而不被发现。

## 客户端认证鉴权防止非法连接

身份认证又称「验证」、「鉴权」，是指通过一定的手段，完成对用户身份的确认。身份认证是大多数应用的重要组成部分，启用身份认证能有效阻止非法客户端的连接。EMQX Cloud 中的认证指的是当一个客户端连接到 EMQX Cloud 的时候，通过服务器端的配置来控制客户端连接服务器的权限。

EMQX Cloud 的认证支持包括两个层面：

1. MQTT 协议本身在 CONNECT 报文中指定用户名和密码
2. 在传输层上，TLS 可以保证使用客户端证书的客户端到服务器的身份验证，并确保服务器向客户端验证服务器证书。

EMQX Cloud 还支持 HTTP 自定义认证、MySQL、PostgreSQL 外部数据库认证，未来还将支持 Redis 自定义认证及授权，帮助用户实现更加复杂的认证鉴权逻辑和 ACL 校验逻辑。

## 多项目、多角色管理实现权限管理

对于企业应用软件来说，权限设计是一个非常重要的模块。各个企业千差万别的组织架构会产生不尽相同的业务流程，因此应用软件需要有完善的权限管理功能，可以实现不同用户登陆系统后，能看到不同的模块，操作不同的功能，看到不同范围的数据，防止数据泄露、权限混乱等情况发生。

针对这些问题，EMQX Cloud 设计了多项目管理部署及子账号管理权限功能。

例如：您可以将用于测试环境及生产环境的部署分别存放在测试项目和生产项目下管理，同时赋予开发人员和测试人员不同项目的只读/修改权限，这样一来，开发人员及测试人员登陆控制台只可执行被赋予权限的操作，预防了诸如因误操作修改生产环境部署数据影响正常业务运转这类的问题。

 
![多项目、多角色管理实现权限管理](https://assets.emqx.com/images/5ac188426bb70ad17b6006c5d9e10f05.png)


## 客户隐私数据安全保障

EMQX Cloud 拥有严格的用户隐私数据安全保障协议，不会有意收集、访问 、使用、存储、披露、转让或以其他方式处理任何您已识别或可识别个人相关的任何内容。在您创建部署前，您可以查阅我们的隐私协议具体了解。

在您使用 EMQX Cloud 的过程中，您的生产数据不会持久化储存在集群里，根据您的功能使用情况，可能存储在 EMQX Cloud 侧的用户隐私数据可能包含：设备连接证书，设备认证数据和 ACL 数据，数据集成配置等。在您停止服务后，我们会自动删除您的部署，同时清理这些数据，完全无需手动删除，避免数据泄漏的隐患。

## 结语

EMQX Cloud 通过以上五个方面组建了一整套完备的数据安全保障方案。无论是在设备数据的流转，还是业务数据的分角色处理，都拥有对应的措施来保证数据安全，助力用户构建高效、可靠、安全的物联网平台与应用。


<section class="promotion">
    <div>
        免费试用 EMQX Cloud
        <div class="is-size-14 is-text-normal has-text-weight-normal">无须绑定信用卡</div>
    </div>
    <a href="https://accounts-zh.emqx.com/signup?continue=https://cloud.emqx.com/console/deployments/0?oper=new" class="button is-gradient px-5">开始试用 →</a>
</section>
