# FitCloud2.0服务器数据传输接口

[TOC]

# 一、说明
本文档接口数据格式沿用旧服务器格式，采用HTTP **POST** 请求方式，返回数据格式统一为JSON。

返回数据例子如下：
```json
{
    "errorCode": 0,
    "errorMsg": "",
    "data": {
        "total": 31099,         // 总数据条数
        "pageNo": 1,            // 当前页码
        "pageSize": 100,        // 每页默认100
        "results": []           // 结果数组
    }
}
```

# 二、数据接口

接口名称：/transfer/data  
接口作用：获取用户上报数据  
接口参数：  
|参数|类型|必填|说明| 
|-|-|-|-|
|accessToken|String|是|fitcloud提供|
|timeFrom|String|是|时间范围开始, 格式yyyy-MM-dd HH:mm:ss|
|timeTo|String|是|时间范围结束, 格式yyyy-MM-dd HH:mm:ss|
|page|String|否|页码，从1开始, 默认1|


返回值：  
|返回字段|类型|说明|
|-|-|-|
|errorCode|int|错误码，0代表成功，其他数值代表失败。根据实际接口的错误类型决定失败数值。|
|errorMsg|String|错误描述。errorCode为0时，此字段为空。|
|data|String| 数据包结构体 |

```json
data: {
    "total": 31099,
    "pageNo": 1,
    "pageSize": 100,
    "results": [
        {
            "ts": "2020-03-07 10:09:01",    //该笔数据上传时间
            "uid": 107270,                  // 用户id
            "type": "step",                 // 数据类型，取值有：step, heartrate, bloodpressure, oxygen, ecg, sleep, sport,
            "payload": []                   // 数据列表，每个payload对应的数据结构见说明
        },
        {
            "ts": "2020-03-07 10:09:01",
            "uid": 107270,
            "type": "heartrate",
            "payload": []
        },

        {
            "ts": "2020-03-07 10:09:01",
            "uid": 107270,
            "type": "bloodpressure",
            "payload": []
        }
    ]
}
```

Payload数据结构:  

1. type = `step`

```
/**
* 某天步数总数据
*/
{
    String date;//该天的日期，yyyy-MM-dd
    String device;//该数据来源设备地址
    int step;//当天总步数值
    float distance;//当天总距离,单位km。保留3位小数
    float calorie;//当天总卡路里，单位千卡。保留3位小数
}
```

2. type = `sleep`

```
/**
* 上传的睡眠数据
*/
{
    String time;//该数据的日期，yyyy-MM-dd HH:mm:ss
    int	deepSleep;//深睡的总时长，单位为秒
    int	lightSleep;//浅睡的总时长，单位为秒
    int	soberSleep;//清醒时长，单位为秒
    List<SleepItem> detail;//睡眠详细数据
}

/**
* 单条睡眠状态的时间段
*/
SleepItem{
	int status;// 该时间段睡眠状态，1深睡，2浅睡，3清醒
	String startTime;//该时间段的起始时间，yyyy-MM-dd HH:mm:ss日期格式
	String endTime;//该时间段的结束时间，yyyy-MM-dd HH:mm:ss日期格式
}

```

3. type = `heartrate`

```
/**
* 上传的心率数据
*/
UploadHeartRateRecord{
    String date;//该行数据的日期，yyyy-MM-dd日期格式
    List<HeartRateItem> detail;//包含的详细数据
}

/**
* 心率数据
*/
HeartRateItem{
    String time;//该行数据的时间，yyyy-MM-dd HH:mm:ss日期格式
    int	heartRate;//心率值
}

```

4. type = `bloodpressure`

```
/**
* 上传的血压数据
*/
UploadBloodPressureRecord{
    String date;//该行数据的日期，yyyy-MM-dd日期格式
    List<BloodPressureItem> detail;//包含的详细数据
}

/**
* 血压数据
*/
BloodPressureItem{
    String time;//该行数据的时间，yyyy-MM-dd HH:mm:ss日期格式
    int	sbp;//收缩压
    int	dbp;//舒张压
}
```

5. type = `oxygen`

```
/**
* 上传的血氧数据
*/
UploadOxygenRecord{
    String date;//该行数据的日期，yyyy-MM-dd日期格式
    List<OxygenItem> detail;//包含的详细数据
}

/**
* 血氧数据
*/
OxygenItem{
    String time;//该行数据的时间，yyyy-MM-dd HH:mm:ss日期格式
    int	oxygen;//血氧值
}

```

6. type = `ecg`

```
/**
 * 心电数据
 */
UploadEcgRecord{
    UUID ecgId;//心电id
    String time;//该行数据的时间，yyyy-MM-dd HH:mm:ss日期格式
    List<Integer> detail;//心电值详情
    String deviceAddress;//产生此数据的设备地址
    int scaleValue;//幅度转换比
    int sampleBase;//采样率
}

```

7. type = `sport`

```
/**
 * 上传运动数据
 */
UploadSportRecord{
    UUID sportId;//运动ID
    String time;//该行数据的时间，yyyy-MM-dd HH:mm:ss日期格式
    int duration;//跑步持续时间
    double distance;//跑步距离
    double calorie;//消耗卡路里
    int step;//总步数
    double climb;//爬升
    int locationType;//定位类型0是国内，1是国外，默认0
    int sportType;//运动类型，1是手环上骑行，2是APP上骑行，3是手环上室外跑，4是APP上室外跑，5是手环上室内跑，6是APP上室内跑
    List<SportLatLng> latLngs;//运动过程中的定位信息
}

SportLatLng{
    double lat;//纬度
    double lng;//经度
    long timestamp;//产生此经纬度的时间戳
    int duration;//产生此经纬度的跑步进行时间
    int isRestart; //是否为第一个点，1为是，0为否
}
```