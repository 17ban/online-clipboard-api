# API

## 存入

### 描述

存入文本到服务器。

### 请求 URL

`https://cb.17ban.icu/api/text`

### 请求方法

`POST`

### 请求体类型

`application/json`

### 请求体参数

| 参数名  | 必选 | 类型   | 默认值 | 说明                                                         |
| ------- | ---- | ------ | ------ | ------------------------------------------------------------ |
| text    | 是   | string |        | 要存入服务器的文本。文本字符数量不能超过 1 万。              |
| timeout | 否   | number | 600000 | 存入文本的有效时长。单位：毫秒。最大值为 10 分钟，即 600000 。 |

### 响应体类型

`application/json`

### 响应字段

| 字段名 | 必选 | 类型   | 说明                                                         |
| ------ | ---- | ------ | ------------------------------------------------------------ |
| status | 是   | string | 请求的状态。仅存在这三个取值："OK", "ERROR", "REJECT" 。请求成功时为"OK" 。 |
| msg    | 是   | string | 与请求相关的信息。请求失败时描述失败的原因。                 |
| key    | 否   | string | 存入的文本的提取码。只有请求成功时此字段才存在。             |
| exp    | 否   | number | 存入的文本的失效时间戳。如 1611252171677 表示此文本将于北京时间 2021-01-22 02:02:51 失效。只有请求成功时此字段才存在。 |

### 请求示例

请求体：

```json
{
	"text": "Hello, Online ClipBoard!",
	"timeout": 500000
}
```

### 响应示例

响应体：

```json
{
	"status": "OK",
	"msg": "Succeed.",
    "key": "B17A",
	"exp": 1611252171677
}
```



## 取出

### 描述

从服务器取出文本。

### 请求 URL

`https://cb.17ban.icu/api/text`

### 响应体类型

`application/json`

### 请求方法

`GET`

### 请求 URL 参数

| 参数名 | 必选 | 类型   | 说明                         |
| ------ | ---- | ------ | ---------------------------- |
| key    | 是   | string | 文本的提取码。不区分大小写。 |

### 响应字段

| 字段名 | 必选 | 类型   | 说明                                                         |
| ------ | ---- | ------ | ------------------------------------------------------------ |
| status | 是   | string | 请求的状态。仅存在这三个取值："OK", "REJECT", "ERROR" 。请求成功时为"OK "。 |
| msg    | 是   | string | 与请求相关的信息。请求失败时描述失败的原因。                 |
| text   | 否   | string | 取出的文本。只有请求成功时才存在此字段。                     |

### 请求示例

URL：

```
https://cb.17ban.icu/api/text?key=B17A
```

### 响应示例

响应体：

```json
{
	"status": "OK",
	"msg": "Succeed.",
	"text": "Hello, web surfer."
}
```
