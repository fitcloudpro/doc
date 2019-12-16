#FitCloud2.0服务器数据下发接口文档

[TOC]

# 一、更新日志
See git history

# 二、用户接口


# 三、数据接口

## 3.1 步数数据分发
接口名称：/dispatch/step    
接口作用：按日期划分，分发步数数据。同一天的数据可能多次上传，对端接受此数据后，需要根据日期保存或覆盖旧的数据。    
接口参数：
|参数|类型|必填|说明| 
|-|-|-|-|
|data|String|是|StepRecord的JSON数组|

返回值：
|返回字段|类型|说明|
|-|-|-|
|errorCode|int|错误码，0代表成功，其他数值代表失败。根据实际接口的错误类型决定失败数值。|
|errorMsg|String|错误描述。errorCode为0时，此字段为空。|


```

/**
* 某天步数总数据
*/
StepRecord{
    String date;//该天的日期，yyyy-MM-dd
    String device;//该数据来源设备地址
    int step;//当天总步数值
    float distance;//当天总距离,单位km。保留3位小数
    float calorie;//当天总卡路里，单位千卡。保留3位小数
}

```

## 3.2 睡眠数据分发
接口名称：/dispatch/sleep  
接口作用：分发一组睡眠数据。同一天的数据可能多次上传，对端接受此数据后，需要根据日期保存或覆盖旧的数据。    
接口参数：
|参数|类型|必填|说明| 
|-|-|-|-|
|data|String|是|UploadSleepRecord的JSON数组|

返回值：
|返回字段|类型|说明|
|-|-|-|
|errorCode|int|错误码，0代表成功，其他数值代表失败。根据实际接口的错误类型决定失败数值。|
|errorMsg|String|错误描述。errorCode为0时，此字段为空。|

```
/**
* 上传的睡眠数据
*/
UploadSleepRecord{
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

## 3.3 心率数据分发
接口名称：/dispatch/heartrate  
接口作用：分发一组心率数据。同一天的心率数据，会分成多个节点数据HeartRateItem，并且可能分多次上传。对端接受此数据后，需要根据日期保存或覆盖旧的HeartRateItem数据。    
接口参数：
|参数|类型|必填|说明| 
|-|-|-|-|
|data|String|是|UploadHeartRateRecord的JSON数组|

返回值：
|返回字段|类型|说明|
|-|-|-|
|errorCode|int|错误码，0代表成功，其他数值代表失败。根据实际接口的错误类型决定失败数值。|
|errorMsg|String|错误描述。errorCode为0时，此字段为空。|

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

## 3.4 血压数据分发
接口名称：/dispatch/bloodpressure  
接口作用：分发一组心率数据。保存方式与心率相同。  
接口参数：
|参数|类型|必填|说明| 
|-|-|-|-|
|data|String|是|UploadBloodPressureRecord的JSON数组|

返回值：
|返回字段|类型|说明|
|-|-|-|
|errorCode|int|错误码，0代表成功，其他数值代表失败。根据实际接口的错误类型决定失败数值。|
|errorMsg|String|错误描述。errorCode为0时，此字段为空。|

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

## 3.5 血氧数据分发
接口名称：/dispatch/oxygen  
接口作用：分发一组血氧数据。保存方式与心率相同  
接口参数：
|参数|类型|必填|说明| 
|-|-|-|-|
|data|String|是|UploadOxygenRecord的JSON数组|

返回值：
|返回字段|类型|说明|
|-|-|-|
|errorCode|int|错误码，0代表成功，其他数值代表失败。根据实际接口的错误类型决定失败数值。|
|errorMsg|String|错误描述。errorCode为0时，此字段为空。|

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

## 3.6 心电数据分发
接口名称：/dispatch/ecg   
接口作用：分发一组用户的心电数据。对端接受此数据，根据UUID保存或覆盖旧的数据。   
接口参数：
|参数|类型|必填|说明| 
|-|-|-|-|
|data|String|是|UploadEcgRecord的JSON数组|

返回值：
|返回字段|类型|说明|
|-|-|-|
|errorCode|int|错误码，0代表成功，其他数值代表失败。根据实际接口的错误类型决定失败数值。|
|errorMsg|String|错误描述。errorCode为0时，此字段为空。|

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

## 3.7 运动数据分发
接口名称：/dispatch/sport  
接口作用：分发一组用户的运动数据。对端接受此数据，根据UUID保存或覆盖旧的数据。   
接口参数：
|参数|类型|必填|说明| 
|-|-|-|-|
|data|String|是|UploadSportRecord的JSON数组|

返回值：
|返回字段|类型|说明|
|-|-|-|
|errorCode|int|错误码，0代表成功，其他数值代表失败。根据实际接口的错误类型决定失败数值。|
|errorMsg|String|错误描述。errorCode为0时，此字段为空。|

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