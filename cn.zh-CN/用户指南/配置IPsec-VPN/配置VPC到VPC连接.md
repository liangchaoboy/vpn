# 配置VPC到VPC连接 {#concept_c4h_slz_wdb .concept}

本文介绍如何使用VPN网关建立VPC到VPC连接，从而两个VPC内的资源可以互访。

![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/13352/15560136513319_zh-CN.png)

本操作以同一个账号下的两个VPC为例。如果是跨账号VPC互通，操作步骤和同账号VPC互通一样。只是在创建用户网关前，需要获取对方账号的VPN网关的公网IP地址，然后使用获取的对方账号的公网IP地址创建用户网关。

|VPC名称|VPC网段|VPC ID|ECS名称|
|:----|:----|:-----|:----|
|VPC1|172.16.0.0/12|vpc-xxxxz0|ECS1|
|VPC2|10.0.0.0/8|vpc-xxxxut|ECS2|

**说明：** VPN 网关是基于Internet建立加密隧道进行通信，通信质量依赖Internet。如果对通信质量要求高，可以使用高速通道。详细说明，请参见[同账号VPC互连](../../../../intl.zh-CN/快速入门/同账号VPC互连.md#)和[跨账号VPC互连](../../../../intl.zh-CN/快速入门/跨账号VPC互连.md#)。

## 开始之前 {#section_q3w_ylz_wdb .section}

确保两个VPC的私网IP地址不重叠。

## 步骤一 创建VPN网关 {#section_vfk_2mz_wdb .section}

1.  登录VPC管理控制台。
2.  在左侧导航栏，单击**VPN** \> **VPN网关** 。
3.  在VPN网关页面，单击**创建VPN网关**。
4.  在购买页面，配置VPN网关，完成支付。本操作中VPN网关的配置如下：
    -   **地域**：选择VPN网关的地域。本操作中选择**华东1（杭州）**。

**说明：** 确保VPC的地域和VPN网关的地域相同。

    -   **专有网络**： 选择要连接的VPC。

    -   **带宽规格**：选择一个带宽规格。带宽规格是VPN网关所具备的公网带宽。

    -   **IPsec-VPN**： 选择开启IPsec-VPN功能。

    -   **SSL-VPN**： 选择是否开启SSL-VPN功能。SSL-VPN功能允许您从任何位置的单台计算机连接到专有网络。

    -   **SSL并发连接数**： 选择您需要同时连接的客户端最大规格。

**说明：** 本选项只有在选择开启了SSL-VPN功能后才可配置。

        ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/13352/155601365144632_zh-CN.png)

5.  重复上述步骤，为另外一个VPC创建一个VPN网关。

    刚创建好的VPN网关的状态是准备中，约两分钟左右会变成正常状态。正常状态就表明VPN网关完成了初始化，可以正常使用了。VPN 网关创建后，系统会自动分配两个公网IP。

    **说明：** VPN网关的创建一般需要1-5分钟。

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/13352/15560136513320_zh-CN.png)

    本例中分配的公网IP地址为121.xxx.xx.143和118.xxx.xx.149，如下表所示。

    |VPC|VPN网关|IP地址|
    |:--|:----|:---|
    | 名称：VPC1

 ID：vpc-xxxxz0

 网段：172.16.0.0/12

 |vpn-xxxxxqwj|118.xxx.xx.149|
    | 名称：VPC2

 ID：vpc-xxxxut

 网段：10.0.0.0/8

 |vpn-xxxxxl5z|121.xxx.xx.143|


## 步骤二 创建用户网关 {#section_upz_wmz_wdb .section}

1.  在左侧导航栏，单击**VPN** \> **用户网关** 。
2.  选择华东1地域。
3.  在用户网关页面，单击**创建用户网关**。
4.  根据以下信息配置用户网关：
    -   **名称**：输入用户网关的名称。

    -   **IP地址**：输入对端VPC的VPN网关的公网IP地址。

    -   **描述**：输入用户网关的描述信息。

5.  重复上述步骤，使用另外一个IP地址再创建一个用户网关。

    本操作后，VPC与VPN网关、用户网关之间的对应关系如下表所示。

    |VPC|VPN网关|IP地址|用户网关|
    |:--|:----|:---|:---|
    | 名称：VPC1

 ID：vpc-xxxxz0

 网段：172.16.0.0/12

 |vpn-xxxxxqwj|121.xxx.xx.143|user\_VPC1|
    | 名称：VPC2

 ID：vpc-xxxxut

 网段：10.0.0.0/8

 |vpn-xxxxxl5z|118.xxx.xx.149|user\_VPC|


## 步骤三 创建IPsec连接 {#section_ty2_jnz_wdb .section}

创建好VPN网关和用户网关后，您需要分别创建两个IPsec连接建立VPN通道：

1.  在左侧导航栏，单击**VPN** \> **IPSec连接**。
2.  选择华东1地域。
3.  在IPsec连接页面，单击**创建IPsec连接**。
4.  根据以下信息配置IPsec连接，然后单击**确定**。
    -   **名称**：输入IPsec连接的名称。

    -   **VPN网关**： 选择已创建的VPN网关。本例先选择VPC1的VPN网关vpn-xxxxxqwj。

    -   **用户网关**：选择使用对端VPN网关的公网IP地址创建的用户网关。本例选择VPC2的用户网关user\_VPC2。

    -   **本端网段**：输入已选VPN网关所属VPC的网段，本例输入VPC1的网段172.16.0.0/12。也可单击**+添加 本端网段**添加多个本端网段。

        **说明：** 只有IKE V2版本下才可以配置多网段。

    -   **对端网段**：输入对端VPC的网段，本例输入VPC2的网段10.0.0.0/8。也可单击**+添加 对端网段**添加多个对端网段。

        **说明：** 只有IKE V2版本下才可以配置多网段。

    -   **是否立即生效**：选择是否删除当前已协商成功的IPsec隧道并重新发起协商。

-   是：配置完成后立即进行协商。
-   否：当有流量进入时进行协商。
    -   **同步到VPN路由表**：选择是否将兴趣流同步到VPN路由表，推荐选择是。

-   是：IPsec连接创建完成后，兴趣流同步到VPN路由表。
-   否：IPsec连接创建完成后，兴趣流未同步到VPN路由表，您还需前往VPN网关页面添加网关路由。详细说明，请参见[网关路由概述](intl.zh-CN/用户指南/管理VPN网关/配置VPN网关路由/网关路由概述.md#)。
    -   **预共享密钥**：输入一个共享密钥，本例输入1234567。两个IPsec连接的共享密钥必须相同。

    -   **健康检查**：开启健康检查并输入目的IP、源IP、重试间隔和重试次数。

5.  在弹出的对话框中单击**确定**。

6.  找到目标路由条目，单击**发布**，然后在弹出的对话框中单击**确定**。

7.  重复上述步骤，为另外一个VPC创建一个IPsec连接。

    本操作中，VPC1的IPsec连接配置如下图所示。

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/13352/15560136513321_zh-CN.png)

    本操作中，VPC2的IPsec连接配置如下图所示。

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/13352/15560136513322_zh-CN.png)


## 步骤四 测试私网通信 {#section_ojw_ylz_wdb .section}

在专有网络VPC1内的ECS1实例上ping ECS2 实例的私网IP，测试两个VPC的私网通信。

![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/13352/15560136533323_zh-CN.png)

