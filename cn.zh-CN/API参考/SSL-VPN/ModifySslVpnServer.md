# ModifySslVpnServer {#doc_api_951832 .reference}

调用ModifySslVpnServer接口修改SSL-VPN服务端的配置信息。

## 调试 {#apiExplorer .section}

前往【[API Explorer](https://api.aliyun.com/#product=Vpc&api=ModifySslVpnServer)】在线调试，API Explorer 提供在线调用 API、动态生成 SDK Example 代码和快速检索接口等能力，能显著降低使用云 API 的难度，强烈推荐使用。

## 请求参数 {#parameters .section}

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|Action|String|是|ModifySslVpnServer|要执行的操作。

 取值： **ModifySslVpnServer**。

 |
|RegionId|String|是|cn-hangzhou|VPN网关所在的地域。

 您可以通过调用[DescribeRegions](~~36063~~)接口获取地域ID。

 |
|SslVpnServerId|String|是|vss-bp18q7hzj6largv4vk2fe|SSL-VPN服务端实例ID。

 |
|Cipher|String|否|AES-128-CBC|SSL-VPN使用的加密算法。取值： **AES-128-CBC（默认值） |AES-192-CBC | AES-256-CBC | none**

 |
|ClientIpPool|String|否|10.30.30.0/2|客户端IP地址池。

 |
|ClientToken|String|否|02fb3da4-130e-11e9-8e44-0016e04115b| 

 客户端token，用于保证请求的幂等性。

 由客户端生成该参数值，要保证在不同请求间唯一，最大不值过64个 ASCII 字符。

 |
|Compress|Boolean|否|false|指定是否对通信进行压缩。 取值：**true（默认值） | false**

 |
|LocalSubnet|String|否|10.20.20.0/24(多个网段使用逗号分隔，例如：192.168.0.0/24,172.16.0.0/24)|本地客户端的网段。

 |
|Name|String|否|test|SSL-VPN服务端的名称。 长度为 2-128个字符，必须以字母或中文开头，可包含数字，点号（.），下划线（\_）和短横线（-）。但不能以`http://` 或`https://`开头。

 |
|Port|Integer|否|1194|SSL-VPN服务端所使用的端口，默认值为1194。 不能用使用以下端口：

 22, 2222, 22222, 9000, 9001, 9002, 7505, 80, 443, 53, 68, 123, 4510, 4560, 500, 4500

 |
|Proto|String|否|UDP|SSL-VPN服务端所使用的协议。

 |

## 返回参数 {#resultMapping .section}

|名称|类型|示例值|描述|
|--|--|---|--|
|Cipher|String|AES-128-CBC|使用的加密算法。

 |
|ClientIpPool|String|10.30.30.0/24|客户端IP地址池。

 |
|Compress|Boolean|false|是否压缩通信。

 |
|Connections|Integer|0|当前连接数。

 |
|CreateTime|Long|1492753580000|SSL-VPN服务端的创建时间。

 |
|InternetIp|String|47.98.xx.xx|公网IP。

 |
|LocalSubnet|String|10.20.20.0/24|本地客户端地址段。

 |
|MaxConnections|Integer|5|最大连接数。

 |
|Name|String|test|SSL-VPN服务端的名称。

 |
|Port|Integer|1194|SSL-VPN服务端的端口。

 |
|Proto|String|UDP|SSL-VPN服务端使用的协议。

 |
|RegionId|String|cn-hangzhou|SSL-VPN服务端的地域。

 |
|RequestId|String|DF11D6F6-E35A-41C3-9B20-6FC8A901FE65|请求ID。

 |
|SslVpnServerId|String|vss-bp18q7hzj6largv4vk2fe|SSL-VPN服务端的ID。

 |
|VpnGatewayId|String|vpn-bp1q8bgx4xnkm2ogj0fiu|VPN网关实例ID。

 |

## 示例 {#demo .section}

请求示例

``` {#request_demo}

https://vpc.aliyuncs.com/?Action=ModifySslVpnServer
&RegionId=cn-hangzhou
&SslVpnServerId=vss-bp18q7hzj6largv4vk2fe
&<公共请求参数>

```

正常返回示例

`XML` 格式

``` {#xml_return_success_demo}
<ModifySslVpnServerResponse>
  <PageNumber>1</PageNumber>
  <TotalCount>1</TotalCount>
  <PageSize>10</PageSize>
  <SslVpnServers>
    <SslVpnServer>
      <RegionId>cn-hanghzou</RegionId>
      <SslVpnServerId>vss-bp18q7hzj6largv4vk2fe</SslVpnServerId>
      <VpnGatewayId>vpn-bp1q8bgx4xnkm2ogj0fiu</VpnGatewayId>
      <Name>test</Name>
      <CLientIpPool>10.30.30.0/24</CLientIpPool>
      <LocalSubnet>10.20.20.0/24</LocalSubnet>
      <Proto>UDP</Proto>
      <Port>1194</Port>
      <Cipher>AES-128-CBC</Cipher>
      <Compress>true</Compress>
      <CreateTime>1492753580000</CreateTime>
      <Connections>0</Connections>
      <MaxConnections>5</MaxConnections>
      <InternetIp>47.98.xx.xx</InternetIp>
    </SslVpnServer>
  </SslVpnServers>
  <RequestId>DF11D6F6-E35A-41C3-9B20-6FC8A901FE65</RequestId>
</ModifySslVpnServerResponse>

```

`JSON` 格式

``` {#json_return_success_demo}
{
	"PageNumber":"1",
	"TotalCount":"1",
	"SslVpnServers":{
		"SslVpnServer":{
			"VpnGatewayId":"vpn-bp1q8bgx4xnkm2ogj0fiu",
			"CLientIpPool":"10.30.30.0/24",
			"Proto":"UDP",
			"Cipher":"AES-128-CBC",
			"InternetIp":"47.98.xx.xx",
			"SslVpnServerId":"vss-bp18q7hzj6largv4vk2fe",
			"Name":"test",
			"Port":"1194",
			"MaxConnections":"5",
			"RegionId":"cn-hanghzou",
			"CreateTime":"1492753580000",
			"Compress":"true",
			"LocalSubnet":"10.20.20.0/24",
			"Connections":"0"
		}
	},
	"PageSize":"10",
	"RequestId":"DF11D6F6-E35A-41C3-9B20-6FC8A901FE65"
}
```

## 错误码 { .section}

|HttpCode|错误码|错误信息|描述|
|--------|---|----|--|
|403|Forbbiden.SubUser|User not authorized to operate on the specified resource as your account is created by another user.|您没有权限操作该资源，请您申请操作权限后再试。|
|403|Forbidden|User not authorized to operate on the specified resource.|您没有权限操作指定资源，请提交工单咨询。|
|400|InvalidName|The name is not valid|该名称格式不合法。|
|400|VpnGateway.Configuring|The specified service is configuring.|服务正在配置中，请您稍后再试。|
|400|VpnGateway.FinancialLocked|The specified service is financial locked.|该服务已欠费，请您先充值再操作。|

[查看本产品错误码](https://error-center.aliyun.com/status/product/Vpc)

