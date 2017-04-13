## 1. 接口描述
 
本接口（RegisterBatchIp）用于当指定内网IP所属子网已经加入黑石NAT网关时，将此内网IP加入黑石NAT网关中，否则，此内网IP不会加入黑石NAT网关。
接口请求域名：<font style="color:red">vpc.api.qcloud.com</font>



 

## 2. 输入参数
 以下请求参数列表仅列出了接口请求参数，正式调用时需要加上公共请求参数，见<a href="/doc/api/372/4153" title="公共请求参数">公共请求参数</a>页面。其中，此接口的Action字段为RegisterBatchIp。

| 参数名称 | 是否必选  | 类型 | 描述 |
|---------|---------|---------|---------|
| vpcId | 是 | String | 系统分配的私有网络ID，支持升级前的vpcId，也支持升级后的unVpcId。 |
| subnetId | 是 | String | 系统分配的私有网络子网ID，支持升级前的subnetId，也支持升级后的unSubnetId。 |
| ipList | 是 | Array | 申请IP数组，数组个数范围为1-20。 |


 

## 3. 输出参数

| 参数名称 | 类型 | 描述 |
|---------|---------|---------|
| code | Int | 公共错误码, 0表示成功，其他值表示失败。详见错误码页面的<a href="https://www.qcloud.com/doc/api/372/%E9%94%99%E8%AF%AF%E7%A0%81#1.E3.80.81.E5.85.AC.E5.85.B1.E9.94.99.E8.AF.AF.E7.A0.81" title="公共错误码">公共错误码</a>。|
| message | String | 模块错误信息描述，与接口相关。|
| count | Int | 注册成功的IP个数。|
| extramsg | String | 接口返回的提示信息。|
| data.n | Array | 注册成功的IP数组。|


  ## 4. 错误码表

 | 错误代码 |英文提示| 描述 |
|---------|---------|---------|
| -3047 |InvalidBmVpc.NotFound| 无效的VPC,VPC资源不存在，请再次核实您输入的资源信息是否正确。 |
| -3030  |InvalidBmSubnet.NotFound| 无效的子网,子网资源不存在，请再次核实您输入的资源信息是否正确。 |
| -3031 |AvailableIpUseUp| 没有可用的IP可以分配。 |
| -3001| InvalidInputParams|参数不合法

## 5. 示例
 
输入
```

  https://vpc.api.qcloud.com/v2/index.php?Action=RegisterBatchIp
	&<公共请求参数>
	&vpcId=vpc-2ari9m7h
	&subnetId=subnet-keqt3oty
	&ipList.0=10.1.1.2&ipList.1=10.1.1.300
```

输出
```

{
    "code": 0,
    "message": "",
    "codeDesc": "Success",
    "data": [
        "10.6.100.40"
    ],
    "extramsg":"10.1.1.300 is invalid ip."
    "count": 1
}

```

