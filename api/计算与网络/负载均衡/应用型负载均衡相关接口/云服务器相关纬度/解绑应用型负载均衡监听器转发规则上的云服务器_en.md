## 1. API Description
 API DeregisterInstancesFromForwardLB is used to unbind one or more CVMs from the forwarding rules of forwarding cloud load balancer.
 
Domain for API access: lb.api.qcloud.com


## 2. Request Parameters
 
   The following request parameter list only provides API request parameters. Common request parameters need to be added when the API is called. For more information, refer to [Common Request Parameters](/doc/api/244/4183). The Action field for this API is DeregisterInstancesFromForwardLB.

| Parameter Name | Required | Type | Description |
|-|-|-|-|
| loadBalancerId | Yes | String | Uniform ID of cloud load balancer instance, i.e. unLoadBalancerId. It can be queried by entering 1 or -1 in input parameter "forward" field of API <a href="https://www.qcloud.com/doc/api/244/%E6%9F%A5%E8%AF%A2%E8%B4%9F%E8%BD%BD%E5%9D%87%E8%A1%A1%E5%AE%9E%E4%BE%8B%E5%88%97%E8%A1%A8" title="DescribeLoadBalancers">DescribeLoadBalancers</a>. |
| listenerId | Yes | String | ID of application-based cloud load balancer listener. It can be queried through API DescribeForwardLBListeners. |
| locationIds.n | No | String | ID of specified forwarding rule. If this is not specified, the CVM will be unbound from the entire listener. |
| domain | No | String | Domain of forwarding rule of the listener to be bound. |
| url | No | String | Path of forwarding rule of the listener to be bound. |
| backends.n.instanceId | Yes | String| Unique ID of CVM. It can be acquired from the response field unInstanceId of API <a href="http://www.qcloud.com/doc/api/229/%E6%9F%A5%E7%9C%8B%E5%AE%9E%E4%BE%8B%E5%88%97%E8%A1%A8" title="DescribeInstances">DescribeInstances</a>.<br> This API allows entering instance IDs of multiple CVMs. For example, if you want to enter IDs of two CVMs, the entry is: backends.1.instanceId&backends.2.instanceId. |
| backends.n.port | Yes | Int | Listening port of the backend CVM of cloud load balancer listener. Value range: 1-65535. If this is not specified, all the ports of the you may unbind all the ports of the CVM will be unbound. |



## 3. Response Parameters
| Parameter Name | Type | Description |
|-------|---|---------------|
| code | Int | Common error code; 0: Succeeded; other values: Failed. For more information, please refer to [Common Error Code](/doc/api/244/1530) in the Error Code page. |
| message | String | Module error message description depending on API. |
| codeDesc | String | Error code. For a successful operation, "Success" will be returned. For a failed operation, a message describing the failure will be returned. |
| requestId | Int | Request task ID. The operation status can be queried through API [DescribeLoadBalancersTaskResult](/doc/api/244/4007). |

 

## 4. Example
 
Input
```
https://lb.api.qcloud.com/v2/index.php?Action=RegisterInstancesWithForwardLBSeventhListener
&<Common request parameters>
&loadBalancerId=lb-abcdefgh
&listenerId=lbl-abcdefgh
&locationIds.0=loc-aaaadfa
&backends.0.instanceId=ins-1234test
&backends.0.port=80
&backends.1.instanceId=ins-5678test
&backends.1.port=6
```
Output
```
{
  "code" : 0,
  "message" : "",
  "requestId" : 1234
}
```


