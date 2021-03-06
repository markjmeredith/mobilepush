---

copyright:
 years: 2015, 2017

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen:.screen}
{:codeblock:.codeblock}

# Push Notifications REST API
{: #push-api-rest}
上次更新时间：2017 年 5 月 22 日
{: .last-updated}

您可以将 REST（具象状态传输）API（应用程序编程接口）用于 {{site.data.keyword.mobilepushshort}}。您还可以使用 SDK 和 [Push API ![外部链接图标](../../icons/launch-glyph.svg "外部链接图标")](https://imfpush.{DomainName}/imfpush/){: new_window} 来进一步开发您的客户机应用程序。

通过 Push REST API，后端服务器应用程序和客户机可以访问 {{site.data.keyword.mobilepushshort}} 功能。

- 设备注册
- 注册
- 消息
- 预订
- 标记
- Webhook

要获取 REST API 的基本 URL，请完成以下步骤：

1. 通过选择 MobileFirst Services Starter，在 IBM Cloud®“目录”的“样板”部分中创建后端应用程序。这可将 {{site.data.keyword.mobilepushshort}} 服务绑定到应用程序。您还可以创建 Push 的服务实例，并保留其为未绑定状态。 
1. 在 IBM Cloud“目录”的主页中，转至**应用程序**区域，然后选择您的应用程序。
3. 单击**移动选项**。路径和应用程序 GUID 值会显示在应用程序的详细信息页面顶部。“显示凭证”屏幕将显示有关 appSecret 的信息。您可以从“移动选项”获取应用程序私钥，也可以获取一些 API 的客户机私钥。

您还可以使用命令行来获取服务凭证：

```
 cf create-service-key {push_instance_name} {key_name}

 cf service-key {push_instance_name} {key_name}
```
	{: codeblock}

## 接受语言头
{: #push-api-rest-accept}

“Accept-Language”头指定要将哪种语言用于 [Push REST API ![外部链接图标](../../icons/launch-glyph.svg "外部链接图标")](https://imfpush.{DomainName}/imfpush/){: new_window} 输出的错误消息。支持的错误消息语言如下：简体中文、繁体中文、英语（美国）、德语、法语、意大利语、日语、韩语、葡萄牙语和西班牙语。


## Push REST API 过滤器
{: #push-api-rest-filters}

过滤器定义搜索条件，该条件用于限制从 {{site.data.keyword.mobilepushshort}} 的 GET API 返回的数据。针对要过滤的 GET 操作结果应用过滤器。过滤器会限制结果中包含的条目数。例如，可以使用过滤器来搜索以“test”开头的标记。 

使用以下语法，可生成过滤器：

**名称**：应用过滤器的字段名称。

**运算符**：可以为 ==（完全匹配）或 =@（包含子字符串），用于描述要使用的过滤匹配。

**表达式**：要包含在结果中的值。

如果表达式中出现逗号和反斜杠，必须用反斜杠将它们转义。

使用多个过滤器时，可以使用 AND 和 OR 逻辑来组合这些过滤器。

- 对于 AND 逻辑，在查询中使用多个过滤器。
- 对于 OR 逻辑，在过滤表达式内部使用逗号 (,)。
- 对于 AND 和 OR 逻辑，单个查询可以同时包含 AND 和 OR 逻辑。使用 AND 表达式组合多个过滤器时，会先对每个过滤器单独求值，然后再执行 AND 运算。

对于设备 GET API，将支持以下组合：
-名称为 platform 字段。
- 运算符可以为 == 或 =@，但 platform 除外
- 对于 platform，运算符必须是 ==。如果使用运算符 =@，那么值可以为子字符串。
- 如果使用 ==，那么值必须为完全匹配的字符串。

对于预订 GET API，将支持以下组合：

- 名称可以是以下某个字段：tagName 或 deviceId
- 运算符可以为 == 或 =@，但 platform 除外
- 对于 platform，运算符必须是 ==
- 如果使用 =@ 运算符，那么值可以为子字符串。如果使用 == 运算符，那么值必须为完全匹配的字符串。
- 对于标记 GET API，将支持以下组合：
- 名称可以是以下某个字段：“name”或“description”
- 如果使用运算符 =@，那么值可以为子字符串。
- 如果使用 ==，那么值必须为完全匹配的字符串。


## Push Notifications 服务响应代码
{: #push-api-response-codes}

状态：405 不允许的方法 - 应使用适当的方法。
