AWS 的数据传输类型大致有如下三类：

与 Internet 之间的数据传输
AWS 内部跨区域的数据传输
AWS 内部同一区域的数据传输
每个区域从 AWS 到 Internet 的数据传输费率都不一样，基本是 下行免费，上行收费，费率算总量

https://aws.amazon.com/cn/ec2/pricing/on-demand/ ---> 数据传输部分

EC2
传入/出至互联网
传入不收费
传出收费 <first 10TB/month>
us-east-1: 0.09 USD/GB
ap-northeast-1: 0.114 USD/GB
同一区域
同一可用区内之间传输数据免费，除非使用公网 IP 或者弹性 IP 地址传输数据，则上下行都需要收费，0.01 USD/GB
跨可用区 (A-Z)，上下行都需要收费，0.01 USD/GB
跨可用区 (A-Z)，ELB -> EC2 不收费，EC2 -> ELB 需要收费，0.01 USD/GB
使用 VPC 对等连接传输数据，上下行都需要收费，0.01 USD/GB
通过 PrivateLink 终端节点访问的 AWS 服务将产生标准 PrivateLink 费用
不同区域
传出收费
us-east-1: 基本上是 0.02 USD/GB，有部分美国东部区域不收费
ap-northeast-1: 0.09 USD/GB
CloudFront
AWS 服务 (EC2、S3 等) 传出到 CloudFront，AWS 服务不收费
CloudFront 传入 AWS 服务需要收费，只有 POST 和 PUT 请求，或者从客户端流向 WebSocket 服务器的 WebSocket 流量的需要收费
us-east-1: 0.02 USD/GB
ap-northeast-1: 0.06 USD/GB
CloudFront 传出的流量费用费用 (1TB 内免费)
us-east-1: 0.085 USD/GB
ap-northeast-1: 0.114 USD/GB
S3
S3 和其它 AWS 服务在同一区域 ( Region ) 进行数据传输不收费

不同账号
<待补充>

建议
尽量将所有工作负载保持在同一个 AWS 区域，如果需要使用其他区域，则选择价格最低的区域
尽量将你的所有工作负载保持在同一个 VPC 的可用区，并使用 Private IP 进行连接
避免使用 NAT 网关，因为它的出站流量需要另外收费，尽量使用互联网网关。
如果需要向用户发送数据，使用 CloudFront 与直接从 EC2 实例发送流量相比，它的速度更快，费用更低
尽量减少跨 AZ 数据复制
link
Overview of Data Transfer Costs for Common Architectures
AWS Data Transfer Costs
Amazon CloudFront 定价
