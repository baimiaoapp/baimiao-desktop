## 配置

在设置页面可以配置监听 `IP` 和端口，默认 `0.0.0.0:8888`

## 请求

|  -   | -  |
|  ----  | ----  |
| Method  | `POST` |
| URI  | `/ocr` |
| Body  | `form-data` |

### 请求参数

|  参数   |类型 |示例  | 描述 |
|  ----  | ----  | ----  | ----  |
| lang  |String |`zh-Hans` |可选，默认中英文识别<br>识别语言，可以是多个语言字符串组合（逗号隔开），但是**中文只能和英文组合识别**，参考下文|
| b64  | String |`iVBORw0KGg...` |可选，和`image`二选一<br>需要识别图片的 base64，不含`dataUrl`前缀的`data:image/...`|
| image  | File |`@test.png` |可选，和`b64`二选一<br>需要识别的图片文件|
| quick  | Boolean |`false` |可选，默认false<br>启用快速模式后，识别结果不包含语言信息和换行信息|

**注意：** 当`b64`和`image`同时存在时，`image`参数优先。

#### 识别语言支持的选项：

|key|name|
|--|--|
|zh-Hans|简体中文|
|zh-Hant|繁体中文|
|en-US|英文|
|fr-FR|法语|
|de-DE|德语|
|it-IT|意大利语|
|es-ES|西班牙语|
|pt-BR|葡萄牙语|


>If not otherwise specified, Vision biases its results toward English. To alter its default behavior, provide an array of supported languages in the request’s recognitionLanguages property. The order in which you provide the languages dictates their relative importance. To recognize traditional and simplified Chinese, specify zh-Hant and zh-Hans as the first elements in the request’s recognitionLanguages property. English is the only other language that you can pair with Chinese.

参考：[Recognizing Text in Images | Apple Developer Documentation](https://developer.apple.com/documentation/vision/recognizing_text_in_images/)


### 请求示例

使用图片文件识别：

```bash
curl --location --request POST '127.0.0.1:8888/ocr' \
--form 'lang="zh-Hans,zh-Hant,en-US"' \
--form 'image=@"/Users/afa/Downloads/test.png"'
```

使用图片 base64 识别：

```bash
curl --location --request POST '127.0.0.1:8888/ocr' \
--form 'lang="zh-Hans,zh-Hant,en-US"' \
--form 'b64="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"'
```

## 响应

### 响应结果

|  参数   |类型 |示例  | 描述 |
|  ----  | ----  | ----  | ----  |
| code  |Integer |1 |1:成功, 0:失败|
| msg  | String |`success`|失败原因等描述信息|
| data  | Null \| Object | - |失败时为 `null`，成功时为结果数据对象|

**Data 数据结构：**

|  参数   | 描述 |
|  ----  |  ----  |
| lines  |每一行识别数据的列表|
| boundingBox |文字的边界框（不一定是最小边框）<br>第一组是边框左上角坐标: [x, y]<br>第二组是边框的宽高: [width, height]|
| confidence  |置信度|
| lang  |语言类型，参照 [Whatlang](https://github.com/greyblake/whatlang-rs/blob/master/SUPPORTED_LANGUAGES.md), 可能为 `null`|
| lineFeed  |当前行结束后，是否换行|
| text  |文本文字|
|  -  |  -  |
| size  |图片的宽高|
|  -  |  -  |
| text_all  |所有文字|


### 响应示例：

**失败:**
```json
{
    "code": 0,
    "data": null,
    "msg": "Error parse image data"
}
```

**成功:**
```json
{
    "code": 1,
    "data": {
        "lines": [
            {
                "boundingBox": [
                    [
                        33.25416666666667,
                        27.506276150627627
                    ],
                    [
                        1309.924999710192,
                        49.221757311903765
                    ]
                ],
                "confidence": 1.0,
                "lang": "cmn",
                "lineFeed": false,
                "text": "7月31日，中华人民共和国国防部在北京人民大会堂举行盛大招待会，热烈庆祝中"
            },
            {
                "boundingBox": [
                    [
                        35.72893049036557,
                        91.36438518976071
                    ],
                    [
                        1310.4909645532666,
                        42.69343240212974
                    ]
                ],
                "confidence": 1.0,
                "lang": "cmn",
                "lineFeed": false,
                "text": "国人民解放军建军95周年。中共中央总书记、国家主席、中央军委主席习近平和李"
            },
            {
                "boundingBox": [
                    [
                        34.743248251675,
                        150.50466757717652
                    ],
                    [
                        1305.3986972111777,
                        43.99969595798124
                    ]
                ],
                "confidence": 1.0,
                "lang": "cmn",
                "lineFeed": false,
                "text": "克强、栗战书、汪洋、王沪宁、赵乐际、韩正、王岐山等党和国家领导人出席招待"
            },
            {
                "boundingBox": [
                    [
                        36.67290761589023,
                        212.33927111975464
                    ],
                    [
                        389.6482156712812,
                        41.770893839468734
                    ]
                ],
                "confidence": 0.5,
                "lang": "cmn",
                "lineFeed": true,
                "text": "会。新华社记者 燕雁摄"
            },
            {
                "boundingBox": [
                    [
                        35.7361317295745,
                        308.23304792974517
                    ],
                    [
                        1307.4678013427863,
                        55.42469389284821
                    ]
                ],
                "confidence": 1.0,
                "lang": "cmn",
                "lineFeed": false,
                "text": "人民大会堂宴会厅灯火璀瑑，洋溢着热烈喜庆的节日气氛。主席台上方悬挂着庄严"
            },
            {
                "boundingBox": [
                    [
                        29.59347385712237,
                        375.85938857939885
                    ],
                    [
                        1305.625844978858,
                        49.335162798211634
                    ]
                ],
                "confidence": 1.0,
                "lang": "cmn",
                "lineFeed": false,
                "text": "的“八一”军徽，“1927—2022”的大字年号在红旗映衬下格外醒目，昭示着中国人民"
            },
            {
                "boundingBox": [
                    [
                        36.56902395236287,
                        439.3261741846744
                    ],
                    [
                        459.45913738553855,
                        41.41991518729137
                    ]
                ],
                "confidence": 1.0,
                "lang": "cmn",
                "lineFeed": true,
                "text": "解放军走过95年的光辉历程。"
            },
            {
                "boundingBox": [
                    [
                        33.15547013755131,
                        542.8647125128256
                    ],
                    [
                        1324.5983679359967,
                        57.27652681573208
                    ]
                ],
                "confidence": 1.0,
                "lang": "cmn",
                "lineFeed": false,
                "text": "18时许，在欢快的《迎宾曲》中，习近平等觉和国家领导人步入宴会大厅，与中外"
            },
            {
                "boundingBox": [
                    [
                        38.75037247624422,
                        607.852805912474
                    ],
                    [
                        566.0624100855854,
                        41.54301729450085
                    ]
                ],
                "confidence": 1.0,
                "lang": "cmn",
                "lineFeed": true,
                "text": "来宾欢聚一堂，全场响起热烈掌声。"
            }
        ],
        "size": {
            "height": 692,
            "width": 1388
        },
        "text_all": "7月31日，中华人民共和国国防部在北京人民大会堂举行盛大招待会，热烈庆祝中国人民解放军建军95周年。中共中央总书记、国家主席、中央军委主席习近平和李克强、栗战书、汪洋、王沪宁、赵乐际、韩正、王岐山等党和国家领导人出席招待会。新华社记者 燕雁摄\n人民大会堂宴会厅灯火璀瑑，洋溢着热烈喜庆的节日气氛。主席台上方悬挂着庄严的“八一”军徽，“1927—2022”的大字年号在红旗映衬下格外醒目，昭示着中国人民解放军走过95年的光辉历程。\n18时许，在欢快的《迎宾曲》中，习近平等觉和国家领导人步入宴会大厅，与中外来宾欢聚一堂，全场响起热烈掌声。\n"
    },
    "msg": "success"
}
```


### 数据处理示例：

```javascript
let s = ""
let lastLF = true
for (line of resp.data.lines) {
  const lf = line.lineFeed ? "\n" : ""
  let conn = ""
  if (!lastLF) {
    conn = ["cmn", "kor", "jpn"].includes(line.lang) ? "" : " "
  }
  s = s + conn + line.text + lf
  lastLF = line.lineFeed
}
console.log(s)
```

