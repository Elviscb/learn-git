||||||
|---|----|---|----|----|
| 接口名称 | Token申请API |
| 传输协议 | Http(get方式) |
| 接口URL  | http://xxxxx.xxxxx.xxx/admonitor/token/get |
| 接口参数 | 参数名 | 数据类型 | 描述 | 示例 |
|          | campId | long | campaign标识 | 123 |
|          | appKey | string | 第三方标识密钥串(32位) | …1dcb95a… |
|          | startDate | string | 有效期开始日(格式yyyyMMdd) | 20160201 |
|          | endDate | string | 有效期结束日(格式yyyyMMdd) | 20160401 |
|          | deviceType | string | 投放平台类型标识(1pc;2移动) | 1 |
| 接口输出 | {"retCode":0, "token": "swrafafwfafwfqawfaf32safasf", "campId":123} |
|          | retCode | token | campid |
|          | 0:成功;其他:失败 | 长度64-128 | Token对应的campId |
| Api Demo | http://xxxxx.xxxxx.xxx/admonitor/token_get?campId=123&appKey=…1dcb95a…& startDate=20160201& endDate=20160401& deviceType=1 |
| IP限制   | 第三方提供访问API的出口IP,数平侧作为访问源安全校验手段之一 |
| 唯一性原则 | Token针对campId保持唯一性映射。同一个campId多次申请token,皆返回同一个token。 |
| 访频限制 | 访问频率限制,上限300/min。 |

### 关于endDate有效期变动
> 延期处理方案: 由第三方在用户设定的结束时间基础上,自动延期30天。数平侧不额外处理。
> 有效期校验: 数平侧进行计算时,基于startDate-endDate进行token有效期校验。若不符合有效期规范,则作为非正常数据处理。

### 关于平台类型标识参数
> 经第三方,业务侧讨论,结论为“第三方campaign只会投放在单一平台类型(即不存在同时投放移动和PC)“。
> 故在申请token时,指定平台参数;以此减少后续透传数据量并规范数平侧平台类型参数。

