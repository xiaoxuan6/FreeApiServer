# 免费的 API 数据接口服务

文档、快速、免费的 API 接口服务。共收录了 35 个接口

感觉此项目不错的记得 `star`、`fork`、 `follow` 三连，后续 `科技与狠活` 能及时观看。

## 如何使用

这里提供的 `docker`
镜像 [xiaoxuan6/free_api_server](https://hub.docker.com/repository/docker/xiaoxuan6/free_api_server/general)
，只需下载下来直接运行即可。

默认端口：`10086`

```bash
docker run -d --name free -p 10086:10086 xiaoxuan6/free_api_server:latest
```

启动成功后就可以调用下面所有的免费接口，所有的请求都是 `get`

```bazaar
https://{host}:{port}/api/search
```

|名称|说明|
|:---|:---|
|host|docker 所在服务器的 ip|
|port|启动容器所对外开放的端口|

# 接口文档

因时间问题接口文档不全，持续更新...

## 目前不开放

### v1.1.0 新增

<details>
<summary><b>身份证查询</b></summary>

请求参数：

|名称|是否必填|类型|说明|
|:---|:---|:---|:---|
|type|是|string|类型：默认值 id_card（版本 v1.2.0 之前为 idCard）和下面参数保持一致|
|id_card|是|string|身份证号码|

响应参数：

|名称|类型|说明|
|:---|:---|:---|
|code|int|状态码 1:表示成功 其他表示失败|
|msg|string|返回 成功/失败 信息|
|data|object||
|data.idCardNum|string|身份证号码|
|data.address|string|身份证所属归属地|
|data.birthday|string|生日|
|data.sex|string|性别|

</details>
<details>
<summary><b>手机归属地</b></summary>

请求参数：

|名称|是否必填|类型|说明|
|:---|:---|:---|:---|
|type|是|string|类型：默认值 mobile_location|
|mobile|是|string|手机号|

响应参数：

|名称|类型|说明|
|:---|:---|:---|
|code|int|状态码 1:表示成功 其他表示失败|
|msg|string|返回 成功/失败 信息|
|data|object||
|data.mobile|string|目标手机号|
|data.province|string|归属地省份|
|data.carrier|string|归属地描述|

</details>
<details>
<summary><b>今日油价查询</b></summary>

请求参数：

|名称|是否必填|类型|说明|
|:---|:---|:---|:---|
|type|是|string|类型：默认值 oil|
|province|是|string|省份，合法值为：【安徽、北京、重庆、福建、甘肃、广东、广西、贵州、海南、河北、黑龙江、河南、湖北、湖南、江苏、江西、吉林、辽宁、内蒙古、宁夏、青海、陕西、上海、山东、山西、四川、天津、西藏、新疆、云南、浙江】|

响应参数：

|名称|类型|说明|
|:---|:---|:---|
|code|int|状态码 1:表示成功 其他表示失败|
|msg|string|返回 成功/失败 信息|
|data|object||
|data.province|string|当前查询的省份|
|data.t0|string|0号柴油油价|
|data.t89|string|89号汽油油价|
|data.t92|string|92号汽油油价|
|data.t95|string|95号汽油油价|
|data.t98|string|98号汽油油价|

</details>
<details>
<summary><b>历史上的今天</b></summary>

请求参数：

|名称|是否必填|类型|说明|
|:---|:---|:---|:---|
|type|是|string|类型：默认值 history_today|
|item|否|int|是否需要详情，0：不需要详情 1：需要详情 默认值 0 可不传|

响应参数：

|名称|类型|说明|
|:---|:---|:---|
|code|int|状态码 1:表示成功 其他表示失败|
|msg|string|返回 成功/失败 信息|
|data|object||
|data.*.picUrl|string|历史事件所对应的图片，可能为空|
|data.*.title|string|历史事件的名称|
|data.*.year|string|该历史事件发生所对应的年份|
|data.*.month|string|该历史事件发生所对应的月份|
|data.*.day|string|该历史事件发生所对应的日期|
|data.*.details|string|历史事件的详细介绍，如果type=1，则此字段有返回值，否则不返回|

</details>

## 免费接口

### v1.0.0

<details>
<summary><b>获取指定日期的节假日信息</b></summary>

请求参数：

|名称|是否必填|类型|说明|
|:---|:---|:---|:---|
|type|是|string|类型：默认值 date_info|
|date|是|string|指定日期的字符串，格式 ‘2018-02-23’。可以省略，则默认服务器的当前时间。|

响应参数：

|名称|类型|说明|
|:---|:---|:---|
|code|int|0服务正常。-1服务出错|
|type|object||
|type.type|int|节假日类型，分别表示 工作日、周末、节日、调休|
|type.name|string|节假日类型中文名，可能值为 周一 至 周日、假期的名字、某某调休|
|type.week|string|一周中的第几天。值为 1 - 7，分别表示 周一 至 周日|
|holiday|object|如果不是节假日，holiday字段为null|
|holiday.holiday|bool|true表示是节假日，false表示是调休|
|holiday.name|string|节假日的中文名。如果是调休，则是调休的中文名，例如'国庆前调休|
|holiday.wage|int|薪资倍数，1表示是1倍工资|
|holiday.after|bool|只在调休下有该字段。true表示放完假后调休，false表示先调休再放假|
|holiday.target|string|只在调休下有该字段。表示调休的节假日|

</details>

<details>
<summary><b>批量查询指定日期节假日信息</b></summary>

请求参数：

|名称|是否必填|类型|说明|
|:---|:---|:---|:---|
|type|是|string|类型：默认值 date_batch|
|date|是|string|指定日期的字符串，多个日期之间使用 ',' 连接。最大长度查询个数50。兼容旧的格式用逗号,隔开，但不建议。格式 ‘2018-02-23’|
|word|否|string|是否返回日期类型，默认不返回。可选值：’Y’ 返回，’N’ 不返回|

响应参数：

|名称|类型|说明|
|:---|:---|:---|
|code|int|0服务正常。-1服务出错|
|holiday|object|传过来的日期是什么。传多少个就有多少个。|
|holiday.*.holiday|bool|true表示是节假日，false表示是调休|
|holiday.*.name|string|节假日类型中文名，可能值为 周一 至 周日、假期的名字、某某调休|
|holiday.*.wage|string|薪资倍数，1表示是1倍工资|
|type|object|只有明确指定参数 word=Y 时才返回类型信息|
|type.*.type|int|节假日类型，分别表示 工作日、周末、节日、调休|
|type.*.name|string|节假日类型中文名，可能值为 周一 至 周日、假期的名字、某某调休|
|type.*.week|int|一周中的第几天。值为 1 - 7，分别表示 周一 至 周日|

</details>

<details>
<summary><b>获取指定日期的下一个节假日（如果在放假前有调休，也会返回）</b></summary>

请求参数：

|名称|是否必填|类型|说明|
|:---|:---|:---|:---|
|type|是|string|类型：默认值 date_next|
|date|是|string|指定日期的字符串，格式 ‘2018-02-23’。可以省略，则默认服务器的当前时间|
|word|否|string| 是否返回日期类型，默认不返回。可选值：’Y’ 返回，’N’ 不返回 |
|week|否|string| 节假日是否包含周末，默认不包含。可选值：’Y’ 包含周末，’N’ 不包含 |

响应参数：

|名称|类型|说明|
|:---|:---|:---|
|code|int|0服务正常。-1服务出错|
|holiday|object||
|holiday.name|string|节假日的中文名|
|holiday.wage|int| 薪资倍数，3表示是3倍工资|
|holiday.date|string| 节假日的日期|
|holiday.rest|int| 表示当前时间距离目标还有多少天。比如今天是 2018-09-28，距离 2018-10-01 还有3天|
|workday|object|如果节假日前没调休，则此字段为null|
|workday.name|string|调休的中文名|
|workday.wage|int| 薪资倍数，3表示是3倍工资|
|workday.after|bool| true表示放完假后调休，false表示先调休再放假|
|workday.target|string| 表示调休的节假日|
|workday.date|string| 表示要调休的日期|
|workday.rest|int| rest|

</details>

<details>
<summary><b>获取指定日期的下一个工作日（工作日包含正常工作日、调休）不包含当天</b></summary>

请求参数：

|名称|是否必填|类型|说明|
|:---|:---|:---|:---|
|type|是|string|类型：默认值 date_next_workday|
|date|是|string|指定日期的字符串，格式 ‘2020-01-20’。可以省略，则默认服务器的当前时间|

响应参数：

|名称|类型|说明|
|:---|:---|:---|
|code|int|0服务正常。-1服务出错|
|workday|string|如果没有查找到最近的工作日，则此字段为null。最大查找长度为30|
|workday.workday|int|节假日类型，分别表示 工作日、周末、节日、调休。此接口只会返回 0 和 3 的类型|
|workday.name|string|工作日类型中文名，可能值为 周一 至 周五、某某调休|
|workday.week|int|一周中的第几天。值为 1 - 7，分别表示 周一 至 周日|
|workday.date|string|表示要工作的日期|
|workday.rest|int|表示当前时间距离目标还有多少天|

</details>

<details>
<summary><b>获取指定年份或年月份的所有节假日信息。默认返回当前年份的所有信息</b></summary>

请求参数：

|名称|是否必填|类型|说明|
|:---|:---|:---|:---|
|type|是|string|类型：默认值 date_year|
|date|是|string|指定年份或年月份，格式 ‘2019-02’ ‘2019-2’ 或者 ‘2019’。可以省略，则默认服务器当前时间的年份|
|word|否|string|是否返回日期类型，默认不返回。可选值：’Y’ 返回，’N’ 不返回|
|week|否|string|节假日是否包含周末，默认不包含。可选值：’Y’ 包含周末，’N’ 不包含|

响应参数：

|名称|类型|说明|
|:---|:---|:---|
|code|int|0服务正常。-1服务出错|
|holiday|object||
|holiday.*.name|string|节假日的中文名|
|holiday.*.wage|int|薪资倍数，3表示是3倍工资|
|holiday.*.date|string|节假日的日期|
|type|object|只有明确指定参数 word=Y 时才返回类型信息|
|type.*.type|int|节假日类型，分别表示 工作日、周末、节日、调休|
|type.*.name|string|节假日类型中文名，可能值为 周一 至 周日、假期的名字、某某调休|
|type.*.week|int|一周中的第几天。值为 1 - 7，分别表示 周一 至 周日|

</details>

<details>
<summary><b>返回距离今天最近的一个放假安排。周六周末、调休、节假日都会考虑，比较全面的放假安排。</b></summary>

请求参数：

|名称|是否必填|类型|说明|
|:---|:---|:---|:---|
|type|是|string|类型：默认值 date_tts|

响应参数：

|名称|类型|说明|
|:---|:---|:---|
|code|int|0服务正常。-1服务出错|
|tts|string|返回字符串|

</details>

<details>
<summary><b>返回距离今天最近的一个节假日安排。只考虑节假日和调休。</b></summary>

请求参数：

|名称|是否必填|类型|说明|
|:---|:---|:---|:---|
|type|是|string|类型：默认值 date_tts_next|

响应参数：

|名称|类型|说明|
|:---|:---|:---|
|code|int|0服务正常。-1服务出错|
|tts|string|返回字符串|

</details>

<details>
<summary><b>随机图片</b></summary>

请求参数：

|名称|是否必填|类型|说明|
|:---|:---|:---|:---|
|type|是|string|类型：默认值 rand_image_uri|
|mode|否|string| 模式：vertical 竖向图片、transverse 横向图片、taobao 淘宝买家秀图片|
|sort|否|string| 选择输出分类[美女、二次元、腿控、汽车、背景、动漫]，为空随机输出|

响应参数：

|名称|类型|说明|
|:---|:---|:---|
|code|int|返回的状态码 1服务正常、其他服务出错|
| 	imgurl 	|string 	|返回图片地址|
|msg 	|string 	|返回错误提示信息！|

</details>

<details>
<summary><b>随机头像输出</b></summary>

请求参数：

|名称|是否必填|类型|说明|
|:---|:---|:---|:---|
|type|是|string|类型：默认值 avatar|
|sort|否|string|选择输出分类[男、女、动漫男、动漫女]，为空随机输出|

响应参数：

|名称|类型|说明|
|:---|:---|:---|
|code|int|返回的状态码 1服务正常、其他服务出错|
| 	imgurl 	|string 	|返回图片地址|
|msg 	|string 	|返回错误提示信息！|

</details>

<details>
<summary><b>土味情话</b></summary>

请求参数：

|名称|是否必填|类型|说明|
|:---|:---|:---|:---|
|type|是|string|类型：默认值 qinghua|

响应参数：

|名称|类型|说明|
|:---|:---|:---|
|code|int|返回的状态码 1服务正常、其他服务出错|
| content 	|string 	|返回文本信息|
|msg 	|string 	|返回错误提示信息！|

</details>

<details>
<summary><b>网易云音乐随机歌曲</b></summary>

请求参数：

|名称|是否必填|类型|说明|
|:---|:---|:---|:---|
|type|是|string|类型：默认值 music|
|sort|否|string|选择输出分类 热歌榜、新歌榜、飙升榜、抖音榜、电音榜 为空输出热歌榜|

响应参数：

|名称|类型|说明|
|:---|:---|:---|
|code|int|返回的状态码 1服务正常、其他服务出错|
| name 	|string 	|歌名|
| artistsname 	|string 	|歌手名|
| url 	|string 	|播放地址|
| picurl 	|string 	|封面图|

</details>

[comment]: <> (<details>)

[comment]: <> (<summary><b>网易云音乐热门评论</b></summary>)

[comment]: <> (请求参数：)

[comment]: <> (|名称|是否必填|类型|说明|)

[comment]: <> (|:---|:---|:---|:---|)

[comment]: <> (|type|是|string|类型：默认值 comments|)

[comment]: <> (响应参数：)

[comment]: <> (|名称|类型|说明|)

[comment]: <> (|:---|:---|:---|)

[comment]: <> (|code|int|返回的状态码 1服务正常、其他服务出错|)

[comment]: <> (| data 	|string 	|返回文本信息|)

[comment]: <> (|msg 	|string 	|返回错误提示信息！|)

[comment]: <> (</details>)

<details>
<summary><b>短网址生成</b></summary>

请求参数：

|名称|是否必填|类型|说明|
|:---|:---|:---|:---|
|type|是|string|类型：默认值 short_url|
|url|否|string|需要进行缩短的长网址|

响应参数：

|名称|类型|说明|
|:---|:---|:---|
|code|int|返回的状态码 1服务正常、其他服务出错|
| ae_url 	|string 	| 	返回缩短后的短网址|

</details>

<details>
<summary><b>查询域名是否被墙</b></summary>

请求参数：

|名称|是否必填|类型|说明|
|:---|:---|:---|:---|
|type|是|string|类型：默认值 ck|
|url|否|string|需要进行查询的域名|

响应参数：

|名称|类型|说明|
|:---|:---|:---|
|code|int|返回的状态码 1服务正常、其他服务出错|
| msg 	|string 	| 	返回信息|

</details>

<details>
<summary><b>ICP备案查询</b></summary>

请求参数：

|名称|是否必填|类型|说明|
|type|是|string|类型：默认值 icp|
|url|否|string|需要进行查询的域名|

响应参数：

|名称|类型|说明|
|:---|:---|:---|
|code|int|返回的状态码 1服务正常、其他服务出错|
|domain|string|返回查询的域名|
|icp|string|返回备案号|

</details>

<details>
<summary><b>二维码解码解析器</b></summary>

请求参数：

|名称|是否必填|类型|说明|
|:---|:---|:---|:---|
|||||

响应参数：

|名称|类型|说明|
|:---|:---|:---|
||||

</details>

<details>
<summary><b>搜狗收录量</b></summary>

请求参数：

|名称|是否必填|类型|说明|
|:---|:---|:---|:---|
|||||

响应参数：

|名称|类型|说明|
|:---|:---|:---|
||||

</details>

<details>
<summary><b>搜狗收录判断</b></summary>

请求参数：

|名称|是否必填|类型|说明|
|:---|:---|:---|:---|
|||||

响应参数：

|名称|类型|说明|
|:---|:---|:---|
||||

</details>

<details>
<summary><b>百度收录量</b></summary>

请求参数：

|名称|是否必填|类型|说明|
|:---|:---|:---|:---|
|||||

响应参数：

|名称|类型|说明|
|:---|:---|:---|
||||

</details>

<details>
<summary><b>百度收录判断</b></summary>

请求参数：

|名称|是否必填|类型|说明|
|:---|:---|:---|:---|
|||||

响应参数：

|名称|类型|说明|
|:---|:---|:---|
||||

</details>

<details>
<summary><b>好搜收录量</b></summary>

请求参数：

|名称|是否必填|类型|说明|
|:---|:---|:---|:---|
|||||

响应参数：

|名称|类型|说明|
|:---|:---|:---|
||||

</details>

<details>
<summary><b>好搜收录判断</b></summary>

请求参数：

|名称|是否必填|类型|说明|
|:---|:---|:---|:---|
|||||

响应参数：

|名称|类型|说明|
|:---|:---|:---|
||||

</details>

### v1.2.0 新增

<details>
<summary><b>抖音视频背景音提取</b></summary>

请求参数：

|名称|是否必填|类型|说明|
|:---|:---|:---|:---|
|type|是|string|类型：默认值 dy_music|
|url|是|string|抖音链接|

响应参数：

|名称|类型|说明|
|:---|:---|:---|
|code|int|状态码 200:表示成功 其他表示失败|
|msg|string|返回 成功/失败 信息|
|desc	|string|	返回标题|
|author_tx	|string|	返回头像|
|music_url|	string|	返回歌曲链接  |

</details>

<details>
<summary><b>60秒读懂世界</b></summary>

请求参数：

|名称|是否必填|类型|说明|
|:---|:---|:---|:---|
|type|是|string|类型：默认值 dm_60s|
|item|否|string|是否输出JSON|

响应参数：

|名称|类型|说明|
|:---|:---|:---|
|code|int|状态码 200:表示成功 其他表示失败|
|msg|string|返回 成功/失败 信息|

</details>

<details>
<summary><b>菜谱查询</b></summary>

请求参数：

|名称|是否必填|类型|说明|
|:---|:---|:---|:---|
|type|是|string|类型：默认值 caipu|
|word|是|string|	食材或菜名|

响应参数：

|名称|类型|说明|
|:---|:---|:---|
|code|int|状态码 200:表示成功 其他表示失败|
|msg|string|返回 成功/失败 信息|
|id|int|菜谱ID|
|type_id|int|类型ID|
|type_name|string|类型名称|
|cp_name|string|菜肴名称|
|zuofa|string|做法|
|texing|string|菜肴特性|
|tishi|string|提示|
|tiaoliao|string|调料|
|yuanliao|string|原料|

</details>

<details>
<summary><b>土味情话</b></summary>

请求参数：

|名称|是否必填|类型|说明|
|:---|:---|:---|:---|
|type|是|string|类型：默认值 say_love|

响应参数：

|名称|类型|说明|
|:---|:---|:---|
|code|int|状态码 200:表示成功 其他表示失败|
|msg|string|返回 成功/失败 信息|
|content|string|	情话内容|

</details>

[comment]: <> (<details>)

[comment]: <> (<summary><b>身份证归属地</b></summary>)

[comment]: <> (请求参数：)

[comment]: <> (|名称|是否必填|类型|说明|)

[comment]: <> (|:---|:---|:---|:---|)

[comment]: <> (|||||)

[comment]: <> (响应参数：)

[comment]: <> (|名称|类型|说明|)

[comment]: <> (|:---|:---|:---|)

[comment]: <> (||||)

[comment]: <> (</details>)

<details>
<summary><b>汇率查询</b></summary>

请求参数：

|名称|是否必填|类型|说明|
|:---|:---|:---|:---|
|type|是|string|类型：默认值 fxrate|
|tocoin|是|string|目标兑换货币，例如人民币CNY|
|fromcoin|是|string|来源货币，例如美元USD|
|money|是|string|兑换金额，单位元|

响应参数：

|名称|类型|说明|
|:---|:---|:---|
|code|int|状态码 200:表示成功 其他表示失败|
|msg|string|返回 成功/失败 信息|
|money|string|金额价格，单位元|

</details>

<details>
<summary><b>抖音热搜榜</b></summary>

请求参数：

|名称|是否必填|类型|说明|
|:---|:---|:---|:---|
|type|是|string|类型：默认值 dy_hot|

响应参数：

|名称|类型|说明|
|:---|:---|:---|
|code|int|状态码 200:表示成功 其他表示失败|
|msg|string|返回 成功/失败 信息|
|hotindex|int|热搜榜指数|
|label|int|标签类型，1新，2荐，3热|
|word|string|热点话题|

</details>

<details>
<summary><b>收货地址解析</b></summary>

请求参数：

|名称|是否必填|类型|说明|
|:---|:---|:---|:---|
|type|是|string|类型：默认值 address_parse|
|text|是|string|文本内容，ex:马云13800138000杭州市滨江区网商路699号|

响应参数：

|名称|类型|说明|
|:---|:---|:---|
|code|int|状态码 200:表示成功 其他表示失败|
|msg|string|返回 成功/失败 信息|
|mobile	|string|	移动电话号码|
|name|	string|	收货人姓名|
|province|	string|	省/特区/自治区/直辖市|
|city	|string	|城市|
|district|	string|	区县|
|postcode|	string|	邮编（文本中优先否则默认区县级）|
|detail	|string|	完整地址|

</details>

<details>
<summary><b>舔狗日记</b></summary>

请求参数：

|名称|是否必填|类型|说明|
|:---|:---|:---|:---|
|type|是|string|类型：默认值 tiaogou_log|

响应参数：

|名称|类型|说明|
|:---|:---|:---|
|code|int|状态码 200:表示成功 其他表示失败|
|msg|string|返回 成功/失败 信息|
|content|	string|	内容|

</details>

<details>
<summary><b>金额转大写</b></summary>

请求参数：

|名称|是否必填|类型|说明|
|:---|:---|:---|:---|
|type|是|string|类型：默认值 cnmoney|
|money|是 |string|金额阿拉伯数字|

响应参数：

|名称|类型|说明|
|:---|:---|:---|
|code|int|状态码 200:表示成功 其他表示失败|
|msg|string|返回 成功/失败 信息|
|cnresult	|string|	中文大写金额|
|fnresult	|string	|西式的三位分节法数字|
|enresult	|string	|英语大写金额|

</details>

<details>
<summary><b>车牌号归属地</b></summary>

请求参数：

|名称|是否必填|类型|说明|
|:---|:---|:---|:---|
|type|是|string|类型：默认值 chepai_retreat|
|word|是|string|车牌号|

响应参数：

|名称|类型|说明|
|:---|:---|:---|
|code|int|状态码 200:表示成功 其他表示失败|
|msg|string|返回 成功/失败 信息|
|code|	string	|车牌代码|
|city|	string	|所属城市|
|province|	string|	所属省份|
|citycode|	string|	城市行政代码|

</details>

### v1.3.0 新增计划

- [ ] 抖音短视频解析
- [ ] 驾驶识别
- [ ] 行驶证识别
- [ ] 增值发票识别
- [ ] 人脸口罩识别
- [ ] 智能鉴黄
- [ ] 银行卡识别
- [ ] 身份证识别
- [ ] 车牌号识别
- [ ] 快递查询
- [ ] 营业执照识别

# 捐赠

如果此项目对您有帮助，还希望您捐赠支持，让我能好好的一直坚持下去。金额不在于多少，一份心意就好！在此感谢所有的捐赠者，你们的鼓励是我最大的动力！

<div style="background:#e3e3e3; color:#FFF" align=center >
<img width="220" height="300" src="https://cdn.jsdelivr.net/gh/xiaoxuan6/static/images/202212102216540.png"/>&nbsp;&nbsp;&nbsp;&nbsp;<img width="200" height="300" src="https://cdn.jsdelivr.net/gh/xiaoxuan6/static/images/202212102216435.jpg"/></div>

# 版权声明

本站所对外提供的Api接口中，部分数据来源于网络，如有侵权，请联系我进行处理！

本站所提供的所有Api接口仅仅是秉承交流学习的思想，没有任何盈利的行为，用户在使用过程中造成的版权问题由使用者自行承担，与本站维护者无关，请知悉！