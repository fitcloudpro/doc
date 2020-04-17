#FitCloud2.0服务器接口文档

[TOC]

# 一、更新日志
See git history

# 二、通用说明

## 2.1 接口数据格式
本文档接口数据格式沿用旧服务器格式，采用HTTP **POST** 请求方式，返回数据格式统一为JSON。

返回数据例子如下：
基本数据类型：
```
{
    "errorCode": 0,
    "errorMsg": "提示信息",
    "data": 1
}
```

复合对象数据类型：
```
{
    "errorCode":0, 
    "errorMsg":"提示信息",
    "data":{ 
	    "id":1, 
	    "name":"王小二" 
    }
}
```

数组类型：
```
{
    "errorCode":0, 
    "errorMsg":"提示信息",
    "data":[
        { 
	        "id":1, 
	        "name":"王小二" 
        },
        { 
	        "id":2, 
	        "name":"王小三" 
        }
    ]
}
```

## 2.2 错误代码

    1001 系统错误
    1002 未授权
    1003 验证码不正确
    1004 用户已经存在
    1005 用户不存在
    1006 密码不正确
    1007 身份 ID 已经设置
    1008 用户在其他地方登录，token失效
    1009 Refresh Token失效
    
# 三、Token
## 3.1 获取token
用户登录后，将获得token，用于请求与用户关联的数据。
```
Token{
    String access_token;//token
    int expires_in;//access_token的超时时间，单位为秒
    String refresh_token;  //只能用于刷新 token，不能用于交互，过期时间较长
}
```

/public以及/auth开头的接口属于匿名接口，无需 token。 其他接口都与用户数据相关，需在 header 中带上 token。

Token在HTTP Header中。形式如下 （xxx 部分为 token 内容）：

> Authorization: Bearer xxxxxxxxxx


## 3.3 刷新token
接口名称：/auth/refreshToken  
接口作用：刷新token  
接口参数：
|参数|类型|必填|说明| 
|-|-|-|-|
|refreshToken|String|是|refresh_token|

返回值：
|返回字段|类型|说明|
|-|-|-|
|errorCode|int|错误码，0代表成功，其他数值代表失败。根据实际接口的错误类型决定失败数值，错误编码需要统一单独列出。|
|errorMsg|String|错误描述。errorCode为0时，此字段为空。|
|data|String|Token的JSON对象|


# 四、用户接口
## 4.1 注册
接口名称：/auth/register  
接口作用：用户注册。根据checkAuthCode参数，有需要验证码和不需要验证码两种注册方式。  
接口参数：
|参数|类型|必填|说明| 
|-|-|-|-|
|platform|int|是|所属平台，0安卓，1苹果，2后台|	 
|channelId|long|是|所属渠道ID|
|userName|String|是|手机号或者邮箱|
|password|String|是|密码|
|checkAuthCode|boolean|是|是否需要检验验证码|
|authCode|String|否|验证码|

返回值：
|返回字段|类型|说明|
|-|-|-|
|errorCode|int|错误码，0代表成功，其他数值代表失败。根据实际接口的错误类型决定失败数值。|
|errorMsg|String|错误描述。errorCode为0时，此字段为空。|
|data|String|Token的JSON对象|

## 4.2 获取验证码
接口名称：/auth/requestAuthCode  
接口作用：获取验证码，可以用于注册，找回密码，绑定手机等。  
接口参数：
|参数|类型|必填|说明| 
|-|-|-|-|
|userName|String|是|手机号或者邮箱|
|language|String|否|默认zh_CN中文，或其他 = 英文|

返回值：
|返回字段|类型|说明|
|-|-|-|
|errorCode|int|错误码，0代表成功，其他数值代表失败。根据实际接口的错误类型决定失败数值。|
|errorMsg|String|错误描述。errorCode为0时，此字段为空。|

## 4.3 检测用户是否存在
接口名称：/auth/checkExist  
接口作用：检测用户是否已经存在  
接口参数：
|参数|类型|必填|说明| 
|-|-|-|-|
|userName|String|是|手机号或者邮箱|
|channelId|long|是|所属渠道ID|

返回值：
|返回字段|类型|说明|
|-|-|-|
|errorCode|int|错误码，0代表成功，其他数值代表失败。根据实际接口的错误类型决定失败数值。|
|errorMsg|String|错误描述。errorCode为0时，此字段为空。|
|data|int|0表示不存在，1表示已存在。|
		
## 4.4 账号登录
接口名称：/auth/login  
接口作用：使用手机号或者邮箱登录  
接口参数：
|参数|类型|必填|说明| 
|-|-|-|-|
|platform|int|是|所属平台，0安卓，1苹果，2后台|	 
|channelId|long|是|所属渠道ID|
|userName|String|是|手机号或者邮箱|
|password|String|是|密码|

返回值：
|返回字段|类型|说明|
|-|-|-|
|errorCode|int|错误码，0代表成功，其他数值代表失败。根据实际接口的错误类型决定失败数值。|
|errorMsg|String|错误描述。errorCode为0时，此字段为空。|
|data|String|Token的JSON对象|

## 4.5 第三方平台登录
接口名称：/auth/login2  
接口作用：使用QQ，微信等第三方平台登录。如果是第一次使用该平台账号登录，自动完成注册功能。  
接口参数：
|参数|类型|必填|说明| 
|-|-|-|-|
|platform|int|是|所属平台，0安卓，1苹果，2后台|	 
|channelId|long|是|所属渠道ID|
|openAppName|String|是|第三方app名称,需要统一名称，QQ，WeChat,Facebook,Sina。目前只有这4个作为第三方平台登录|
|openAppId|String|是|第三方openId|

返回值：
|返回字段|类型|说明|
|-|-|-|
|errorCode|int|错误码，0代表成功，其他数值代表失败。根据实际接口的错误类型决定失败数值。|
|errorMsg|String|错误描述。errorCode为0时，此字段为空。|
|data|String|Token的JSON对象|

## 4.6 重新设置密码
接口名称：/auth/resetPassword  
接口作用：用于忘记密码时，重新设置密码。虽然邮箱注册时不需要验证码，但是邮箱找回密码时，需要验证码。  
接口参数：
|参数|类型|必填|说明| 
|-|-|-|-|
|userName|String|是|手机号或者邮箱|
|channelId|long|是|所属渠道ID|
|password|String|是|新密码|
|authCode|String|是|验证码|

返回值：
|返回字段|类型|说明|
|-|-|-|
|errorCode|int|错误码，0代表成功，其他数值代表失败。根据实际接口的错误类型决定失败数值。|
|errorMsg|String|错误描述。errorCode为0时，此字段为空。|

## 4.7 修改密码
接口名称：/user/changePassword  
接口作用：用于修改密码。  
接口参数：
|参数|类型|必填|说明| 
|-|-|-|-|
|oldPassword|String|是|旧密码|
|newPassword|String|是|新密码|

返回值：
|返回字段|类型|说明|
|-|-|-|
|errorCode|int|错误码，0代表成功，其他数值代表失败。根据实际接口的错误类型决定失败数值。|
|errorMsg|String|错误描述。errorCode为0时，此字段为空。|

## 4.8 户账号设置完成情况
接口名称：/user/profileStatus  
接口作用：判断用户账号资料设置情况  
接口参数：
|参数|类型|必填|说明| 
|-|-|-|-|
|无||||

返回值：
|返回字段|类型|说明|
|-|-|-|
|errorCode|int|错误码，0代表成功，其他数值代表失败。根据实际接口的错误类型决定失败数值。|
|errorMsg|String|错误描述。errorCode为0时，此字段为空。|
|data|如下结构体||

    {
        hasProfile  : 0,        //0，没有资料， 1，已经设置过。
        hasPassword : 0,        //0，没有密码， 1，已经设置过。
        hasIdentity : 0         //0，没有ID，   1，已经设置过。
    }

返回值：
|返回字段|类型|说明|
|-|-|-|
|errorCode|int|错误码，0代表成功，其他数值代表失败。根据实际接口的错误类型决定失败数值。|
|errorMsg|String|错误描述。errorCode为0时，此字段为空。|
|data|int|0，没有设置，1，已经设置。|

## 4.9 绑定/换绑手机号/邮箱
接口名称：/user/rebind  
接口作用：绑定手机号和邮箱，目前APP原型图上邮箱绑定时发送一个链接到用户邮箱，用户点击完成邮箱的绑定。这里还是全部改成验证码吧，统一一下方便点。  
接口参数：
|参数|类型|必填|说明| 
|-|-|-|-|
|userName|String|是|邮箱或者手机|
|authCode|String|是|验证码|
|password|String|否|新密码，如果之前用户没有密码，那么这个参数是必要的|

返回值：
|返回字段|类型|说明|
|-|-|-|
|errorCode|int|错误码，0代表成功，其他数值代表失败。根据实际接口的错误类型决定失败数值。|
|errorMsg|String|错误描述。errorCode为0时，此字段为空。|

## 4.10 设置用户身份标志
接口名称：/user/setIdentity  
接口作用：设置用户的身份ID，只允许设置一次。  
接口参数：
|参数|类型|必填|说明| 
|-|-|-|-|
|identityId|String|是|身份ID|

返回值：
|返回字段|类型|说明|
|-|-|-|
|errorCode|int|错误码，0代表成功，其他数值代表失败。根据实际接口的错误类型决定失败数值。|
|errorMsg|String|错误描述。errorCode为0时，此字段为空。|

## 4.11 同步用户资料
接口名称：/user/syncUserInfo  
接口作用：同步本地用户信息到服务器，服务器对比资料更新时间，在确定是否需要覆盖旧的数据。请求成功后，服务器其需要返回所有用户信息。  
接口参数：
|参数|类型|必填|说明| 
|-|-|-|-|
|nickName|String|否|用户昵称|
|sex|int|否|性别    0男，1女|
|birthday|String|否|出生日期，格式为yyyy/M，如1990/5|
|height|float|否|身高，单位cm|
|weight|float|否|体重，单位kg|
|avatar|String|否|头像URL地址|
|lastModifyTime|long|是|最后更新时间|

返回值：
|返回字段|类型|说明|
|-|-|-|
|errorCode|int|错误码，0代表成功，其他数值代表失败。根据实际接口的错误类型决定失败数值。|
|errorMsg|String|错误描述。errorCode为0时，此字段为空。|
|data|String|User的JSON数据|

```
User{
	long userId;//用户ID
	String phone;//手机号
	String email;//邮箱
	String openAppName;//第三方平台的名称
	String openAppId;//第三方平台的openId
	String nickName//用户昵称
	int sex;//性别    0男，1女
	String birthday;//出生日期，格式为yyyy/M，如1990/5
	float height;//身高，单位cm
	float weight;//体重，单位kg
	String avatar;//头像URL地址
	String identityId;//用户身份ID
	long lastModifyTime;//最后更新时间
}
```

## 4.12 同步用户单位配置
接口名称：/user/syncUnitConfig  
接口作用：同步用户的单位配置。  
接口参数：
|参数|类型|必填|说明| 
|-|-|-|-|
|lengthUnit|int|是|长度单位，0公制单位，1英制单位，默认为0|
|weightUnit|int|是|重量单位，0公制单位，1英制单位，默认为0|
|unitLastModifyTime|long|是|单位的最后更新时间|

返回值：
|返回字段|类型|说明|
|-|-|-|
|errorCode|int|错误码，0代表成功，其他数值代表失败。根据实际接口的错误类型决定失败数值。|
|errorMsg|String|错误描述。errorCode为0时，此字段为空。|
|data|String|UnitConfig的JSON对象|

```
UnitConfig{
    int lengthUnit;//长度单位，0公制单位，1英制单位，默认为0
    int weightUnit;//重量单位，0公制单位，1英制单位，默认为0
    long unitLastModifyTime;//单位的最后更新时间
}
```

## 4.13 同步用户运动目标配置
接口名称：/user/syncTargetConfig  
接口作用：同步用户每日步数目标的配置。  
接口参数：
|参数|类型|必填|说明| 
|-|-|-|-|
|stepTarget|int|是|每日步数目标，默认8000|
|targetLastModifyTime|long|是|单位的最后更新时间|
|distanceTarget|float|否|距离目标 默认5(单位公里)|
|calorieTarget|int|否|卡路里目标，默认250（单位千卡）|

返回值：
|返回字段|类型|说明|
|-|-|-|
|errorCode|int|错误码，0代表成功，其他数值代表失败。根据实际接口的错误类型决定失败数值。|
|errorMsg|String|错误描述。errorCode为0时，此字段为空。|
|data|String|StepTargetConfig的JSON对象|

```
StepTargetConfig{
    int stepTarget;//每日步数目标，默认8000
    long targetLastModifyTime;//单位的最后更新时间
    float distanceTarget;//距离目标，默认5(单位公里)
    int calorieTarget;//卡路里目标，默认250（单位千卡）
}
```

## 4.14 同步用户绑定设备的配置
接口名称：/user/syncBindDeviceConfig  
接口作用：同步用户绑定设备的配置。  
接口参数：
|参数|类型|必填|说明| 
|-|-|-|-|
|deviceAddress|String|是|用户绑定的设备地址|
|deviceName|String|是|用户绑定的设备名称|
|deviceHardwareInfo|String|是|用户绑定的设备版本信息|
|deviceBind|int|是|该设备是否解绑，0未解绑，1，已经解绑|
|deviceLastModifyTime|long|是|用户绑定设备的最后更新时间|

返回值：
|返回字段|类型|说明|
|-|-|-|
|errorCode|int|错误码，0代表成功，其他数值代表失败。根据实际接口的错误类型决定失败数值。|
|errorMsg|String|错误描述。errorCode为0时，此字段为空。|
|data|String|BindDeviceConfig的JSON对象|

```
BindDeviceConfig{
    String deviceAddress;//用户绑定的设备地址
    String deviceName;//设备名称
    String deviceHardwareInfo;//用户绑定的设备版本信息
    int deviceBind;//该设备是否解绑，0未解绑，1，已经解绑
    long deviceLastModifyTime;//用户绑定设备的最后更新时间
}
```

# 五、数据接口
## 5.1 步数接口
### 5.1.1 上传步数数据
接口名称：/step/upload  
接口作用：按日期划分，上传一组步数数据。  
接口参数：
|参数|类型|必填|说明| 
|-|-|-|-|
|data|String|是|StepRecord的JSON数组，服务器对比StepRecord中的lastModifyTime字段，如果上传数据的lastModifyTime大于服务器中的lastModifyTime，则更新这天的数据|

返回值：
|返回字段|类型|说明|
|-|-|-|
|errorCode|int|错误码，0代表成功，其他数值代表失败。根据实际接口的错误类型决定失败数值。|
|errorMsg|String|错误描述。errorCode为0时，此字段为空。|
|data|String|StepRecord的JSON数组。返回与上传数据日期对应的StepRecord|

```

/**
* 某天步数总数据
*/
StepRecord{
    String date;//该天的日期，yyyy-MM-dd
    String device;//改数据来源设备地址
    int step;//当天总步数值
    float distance;//当天总距离,单位km。保留3位小数
    float calorie;//当天总卡路里，单位千卡。保留3位小数
    long lastModifyTime;//数据最后更新时间
}

```

### 5.1.2 获取某段日期的步数数据
接口名称：/step/get  
接口作用：获取某段日期用户的步数总数据。如果startDate等于endDate，就相当于查询这一天的数据。  
接口参数：
|参数|类型|必填|说明| 
|-|-|-|-|
|startDate|String|是|起始日期，包含这个日期。格式为yyyy-MM-dd|
|endDate|String|是|结束日期，包含这个日期。格式为yyyy-MM-dd|

返回值：
|返回字段|类型|说明|
|-|-|-|
|errorCode|int|错误码，0代表成功，其他数值代表失败。根据实际接口的错误类型决定失败数值。|
|errorMsg|String|错误描述。errorCode为0时，此字段为空。|
|data|String|StepRecord的JSON数组|


## 5.2 睡眠接口
APP使用时，如果token没有过期，并且之前有从服务器获取过睡眠数据，那么不再从服务器查询睡眠数据。因为本地数据肯定是最新的。
如果token过期了，或者之前没有从服务器获取过睡眠数据，在上传完本地睡眠数据后，在从服务器拉取最新的睡眠数据，更新到本地，保证本地睡眠数据和服务器保持一致。

### 5.2.1 上传睡眠数据
接口名称：/sleep/upload  
接口作用：上传一组睡眠数据。  
接口参数：
|参数|类型|必填|说明| 
|-|-|-|-|
|data|String|是|UploadSleepRecord的JSON数组|

返回值：
|返回字段|类型|说明|
|-|-|-|
|errorCode|int|错误码，0代表成功，其他数值代表失败。根据实际接口的错误类型决定失败数值。|
|errorMsg|String|错误描述。errorCode为0时，此字段为空。|
|data|String|UpdateSleepRecord的JSON数组。返回上传数据中总数据发生变化的数据|

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

/**
* 某次的睡眠数据
*/
UpdateSleepRecord{
    String time;//该数据的日期，yyyy-MM-dd HH:mm:ss
    int	deepSleep;//深睡的总时长，单位为秒
    int	lightSleep;//浅睡的总时长，单位为秒
    int	soberSleep;//清醒时长，单位为秒
    long lastModifyTime;//最后一次更新时间
    
    long previousModifyTime;//上一次更新时间
}

```

### 5.2.2 获取某段日期的睡眠数据
接口名称：/sleep/get  
接口作用：获取某段日期用户的睡眠总数据。  
接口参数：
|参数|类型|必填|说明| 
|-|-|-|-|
|startTime|String|是|起始日期，包含这个日期。格式为yyyy-MM-dd HH:mm:ss|
|endTime|String|是|结束日期，包含这个日期。格式为yyyy-MM-dd HH:mm:ss|
|needDetail|boolean|否|SleepData中是否需要detail字段，不填时默认为false|

返回值：
|返回字段|类型|说明|
|-|-|-|
|errorCode|int|错误码，0代表成功，其他数值代表失败。根据实际接口的错误类型决定失败数值。|
|errorMsg|String|错误描述。errorCode为0时，此字段为空。|
|data|String|SleepRecord的JSON数组|

```
/**
* 某次的睡眠数据
*/
SleepRecord{
    String time;//该数据的日期，yyyy-MM-dd HH:mm:ss
    int	deepSleep;//深睡的总时长，单位为秒
    int	lightSleep;//浅睡的总时长，单位为秒
    int	soberSleep;//清醒时长，单位为秒
    List<SleepItem> detail;//睡眠详细数据
    long lastModifyTime;//最后一次更新时间
}
```

## 5.3 心率接口
### 5.3.1 上传心率数据
接口名称：/heartrate/upload  
接口作用：上传一组心率数据  
接口参数：
|参数|类型|必填|说明| 
|-|-|-|-|
|data|String|是|UploadHeartRateRecord的JSON数组|

返回值：
|返回字段|类型|说明|
|-|-|-|
|errorCode|int|错误码，0代表成功，其他数值代表失败。根据实际接口的错误类型决定失败数值。|
|errorMsg|String|错误描述。errorCode为0时，此字段为空。|
|data|String|UpdatedHeartRateRecord的JSON数组|

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

/**
* 此次更新天数据的信息
*/
UpdatedHeartRateRecord{
    String date;//该行数据的日期，yyyy-MM-dd日期格式
    int	avgHeartRate;//当天平均心率值
    long lastModifyTime;//最后一次更新时间

    long previousModifyTime;//上一次更新时间
}
```

### 5.3.2 获取某段日期的心率数据
接口名称：/heartrate/get  
接口作用：获取某段日期用户的心率数据。如果startDate等于endDate，就相当于查询这一天的数据。  
接口参数：
|参数|类型|必填|说明| 
|-|-|-|-|
|startDate|String|是|起始日期，包含这个日期。格式为yyyy-MM-dd|
|endDate|String|是|结束日期，包含这个日期。格式为yyyy-MM-dd|
|needDetail|boolean|否|是否需要包含详细数据，如果不填，默认为false|

返回值：
|返回字段|类型|说明|
|-|-|-|
|errorCode|int|错误码，0代表成功，其他数值代表失败。根据实际接口的错误类型决定失败数值。|
|errorMsg|String|错误描述。errorCode为0时，此字段为空。|
|data|String|HeartRateRecord的JSON数组|

```
/**
* 心率数据
*/
HeartRateRecord{
    String date;//该行数据的日期，yyyy-MM-dd日期格式
    int	avgHeartRate;//当天平均心率值
    List<HeartRateItem> detail;//包含的详细数据
    long lastModifyTime;//最后一次更新时间
}
```

## 5.4 血压接口
### 5.4.1 上传血压数据
接口名称：/bloodpressure/upload  
接口作用：上传一组心率数据  
接口参数：
|参数|类型|必填|说明| 
|-|-|-|-|
|data|String|是|UploadBloodPressureRecord的JSON数组|

返回值：
|返回字段|类型|说明|
|-|-|-|
|errorCode|int|错误码，0代表成功，其他数值代表失败。根据实际接口的错误类型决定失败数值。|
|errorMsg|String|错误描述。errorCode为0时，此字段为空。|
|data|String|UpdatedBloodPressureRecord的JSON数组|

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

/**
* 此次更新天数据的信息
*/
UpdatedBloodPressureRecord{
    String date;//该行数据的日期，yyyy-MM-dd日期格式
    int	avgSbp;//当天平均收缩压
    int	avgDbp;//当天平均舒张压
    long lastModifyTime;//最后一次更新时间

    long previousModifyTime;//上一次更新时间
}
```

### 5.4.2 获取某段日期的血压数据
接口名称：/bloodpressure/get  
接口作用：获取某段日期用户的心率数据。如果startDate等于endDate，就相当于查询这一天的数据。  
接口参数：
|参数|类型|必填|说明| 
|-|-|-|-|
|startDate|String|是|起始日期，包含这个日期。格式为yyyy-MM-dd|
|endDate|String|是|结束日期，包含这个日期。格式为yyyy-MM-dd|
|needDetail|boolean|否|是否需要包含详细数据，如果不填，默认为false|

返回值：
|返回字段|类型|说明|
|-|-|-|
|errorCode|int|错误码，0代表成功，其他数值代表失败。根据实际接口的错误类型决定失败数值。|
|errorMsg|String|错误描述。errorCode为0时，此字段为空。|
|data|String|BloodPressureRecord的JSON数组|

```
/**
* 心率数据
*/
BloodPressureRecord{
    String date;//该行数据的日期，yyyy-MM-dd日期格式
    int	avgSbp;//当天平均收缩压
    int	avgDbp;//当天平均舒张压
    List<BloodPressureItem> detail;//包含的详细数据
    long lastModifyTime;//最后一次更新时间
}
```

## 5.5 血氧接口

### 5.5.1 上传血氧数据
接口名称：/oxygen/upload  
接口作用：上传一组血氧数据  
接口参数：
|参数|类型|必填|说明| 
|-|-|-|-|
|data|String|是|UploadOxygenRecord的JSON数组|

返回值：
|返回字段|类型|说明|
|-|-|-|
|errorCode|int|错误码，0代表成功，其他数值代表失败。根据实际接口的错误类型决定失败数值。|
|errorMsg|String|错误描述。errorCode为0时，此字段为空。|
|data|String|UpdatedOxygenRecord的JSON数组|

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

/**
* 此次更新天数据的信息
*/
UpdatedOxygenRecord{
    String date;//该行数据的日期，yyyy-MM-dd日期格式
    int	avgOxygen;//当天平均血氧值
    long lastModifyTime;//最后一次更新时间

    long previousModifyTime;//上一次更新时间
}
```

### 5.5.2 获取某段日期的血氧数据
接口名称：/oxygen/get  
接口作用：获取某段日期用户的血氧数据。如果startDate等于endDate，就相当于查询这一天的数据。  
接口参数：
|参数|类型|必填|说明| 
|-|-|-|-|
|startDate|String|是|起始日期，包含这个日期。格式为yyyy-MM-dd|
|endDate|String|是|结束日期，包含这个日期。格式为yyyy-MM-dd|
|needDetail|boolean|否|是否需要包含详细数据，如果不填，默认为false|

返回值：
|返回字段|类型|说明|
|-|-|-|
|errorCode|int|错误码，0代表成功，其他数值代表失败。根据实际接口的错误类型决定失败数值。|
|errorMsg|String|错误描述。errorCode为0时，此字段为空。|
|data|String|OxygenRecord的JSON数组|

```
/**
* 血氧数据
*/
OxygenRecord{
    String date;//该行数据的日期，yyyy-MM-dd日期格式
    int	avgOxygen;//当天平均血氧值
    List<OxygenItem> detail;//包含的详细数据
    long lastModifyTime;//最后一次更新时间
}
```


## 5.6 呼吸频率接口
APP与服务器交互类似睡眠数据。

### 5.6.1 上传呼吸频率数据
接口名称：/respiratoryrate/upload  
接口作用：上传一组呼吸频率数据  
接口参数：
|参数|类型|必填|说明| 
|-|-|-|-|
|data|String|是|RespiratoryRateItem的JSON数组|

返回值：
|返回字段|类型|说明|
|-|-|-|
|errorCode|int|错误码，0代表成功，其他数值代表失败。根据实际接口的错误类型决定失败数值。|
|errorMsg|String|错误描述。errorCode为0时，此字段为空。|

```
/**
* 呼吸频率数据
*/
RespiratoryRateItem{
    String time;//该行数据的时间，yyyy-MM-dd HH:mm:ss日期格式
    int	rate;//呼吸频率值
}
```

### 5.6.2 获取某段日期的呼吸频率数据
接口名称：/respiratoryrate/get  
接口作用：获取某段日期用户的呼吸频率数据。如果startDate等于endDate，就相当于查询这一天的数据。  
接口参数：
|参数|类型|必填|说明| 
|-|-|-|-|
|startDate|String|是|起始日期，包含这个日期。格式为yyyy-MM-dd|
|endDate|String|是|结束日期，包含这个日期。格式为yyyy-MM-dd|

返回值：
|返回字段|类型|说明|
|-|-|-|
|errorCode|int|错误码，0代表成功，其他数值代表失败。根据实际接口的错误类型决定失败数值。|
|errorMsg|String|错误描述。errorCode为0时，此字段为空。|
|data|String|RespiratoryRateItem的JSON数组|

## 5.7 心电接口
APP与服务器交互类似睡眠数据。

### 5.7.1 上传心电数据
接口名称：/ecg/upload   
接口作用：上传一组用户的心电数据   
接口参数：
|参数|类型|必填|说明| 
|-|-|-|-|
|data|String|是|UploadEcgRecord的JSON数组|

返回值：
|返回字段|类型|说明|
|-|-|-|
|errorCode|int|错误码，0代表成功，其他数值代表失败。根据实际接口的错误类型决定失败数值。|
|errorMsg|String|错误描述。errorCode为0时，此字段为空。|
|data|String|无|

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

### 5.7.2 获取某段日期的心电数据
接口名称：/ecg/get  
接口作用：获取某段日期用户的心电数据。如果startDate等于endDate，就相当于查询这一天的数据。因为心电详细数据非常大，所以这个接口不返回EcgRecord detail字段  
接口参数：
|参数|类型|必填|说明| 
|-|-|-|-|
|startTime|String|是|起始时间，包含这个时间。格式为yyyy-MM-dd HH:mm:ss|
|endTime|String|是|结束时间，包含这个时间。格式为yyyy-MM-dd HH:mm:ss|

返回值：
|返回字段|类型|说明|
|-|-|-|
|errorCode|int|错误码，0代表成功，其他数值代表失败。根据实际接口的错误类型决定失败数值。|
|errorMsg|String|错误描述。errorCode为0时，此字段为空。|
|data|String|EcgRecord的JSON数组，不包含detail字段|

```
/**
* 心电数据
*/
EcgRecord{
    UUID ecgId;//心电id
    String time;//该行数据的时间，yyyy-MM-dd HH:mm:ss日期格式
    List<Integer> detail;//心电值详情
    List<EcgReport> reports;//心电报告地址
    long lastModifyTime;//最后一次更新时间
}
/**
* 心电报告
*/
EcgRecord{
    String language;//语言，目前只有CH或者EN
    String url;//报告地址
}
```
### 5.7.3 获取某个心电的详细数据
接口名称：/ecg/getDetail  
接口作用：获取某个心点值的详细数据，需包含detail字段。  
接口参数：
|参数|类型|必填|说明| 
|-|-|-|-|
|ecgId|UUID|是|心电的id|

返回值：
|返回字段|类型|说明|
|-|-|-|
|errorCode|int|错误码，0代表成功，其他数值代表失败。根据实际接口的错误类型决定失败数值。|
|errorMsg|String|错误描述。errorCode为0时，此字段为空。|
|data|String|EcgRecord的JSON对象|

### 5.7.4  获取心电报告
接口名称：/ecg/getReport  
接口作用：获取某个心电的心电报告  
接口参数：
|参数|类型|必填|说明| 
|-|-|-|-|
|ecgId|UUID|是|心电的id|
|language|String|是|目前只有CH或者EN。服务器根据language查询该条心电是否请求过心电报告，如果没有请求，那么请求报告，并缓存到数据库。然后把所有的心电报告返回。|

返回值：
|返回字段|类型|说明|
|-|-|-|
|errorCode|int|错误码，0代表成功，其他数值代表失败。根据实际接口的错误类型决定失败数值。|
|errorMsg|String|错误描述。errorCode为0时，此字段为空。|
|data|String|EcgReport的JSON数组|

## 5.8 运动接口
APP与服务器交互类似睡眠数据。

### 5.8.1 同步运动目标
接口名称：/sport/syncGoal  
接口作用：设置运动目标  
接口参数：
|参数|类型|必填|说明| 
|-|-|-|-|
|data|String|是|SportGoal的JSON数组|

返回值：
|返回字段|类型|说明|
|-|-|-|
|errorCode|int|错误码，0代表成功，其他数值代表失败。根据实际接口的错误类型决定失败数值。|
|errorMsg|String|错误描述。errorCode为0时，此字段为空。|
|data|String|SportGoal的JSON数组|

```
SportGoal{
    int sportType;//运动类型(0是未设置，1是跑步，2是跑步机，3是骑行)
    int goalType;//运动目标类型(0是未设置，1是设置距离，2是设置时长)
    float goalDistance;//运动目标距离(goalType为1时必传，单位为千米)
    int goalTime;//运动目标时间(goalType为2时必传，单位为秒)
    long lastModifyTime;//目标最后的更新时间
}
```

### 5.8.2 上传运动数据
接口名称：/sport/upload  
接口作用：上传一组用户的运动数据  
接口参数：
|参数|类型|必填|说明| 
|-|-|-|-|
|data|String|是|UploadSportRecord的JSON数组|

返回值：
|返回字段|类型|说明|
|-|-|-|
|errorCode|int|错误码，0代表成功，其他数值代表失败。根据实际接口的错误类型决定失败数值。|
|errorMsg|String|错误描述。errorCode为0时，此字段为空。|
|data|String|无|

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

### 5.8.3 获取运动数据
接口名称：/sport/get  
接口作用：获取运动数据，支持分页查询  
接口参数：
|参数|类型|必填|说明| 
|-|-|-|-|
|page|int|是|第几页数据|
|pageSize|int|是|每页大小|

返回值：
|返回字段|类型|说明|
|-|-|-|
|errorCode|int|错误码，0代表成功，其他数值代表失败。根据实际接口的错误类型决定失败数值。|
|errorMsg|String|错误描述。errorCode为0时，此字段为空。|
|data|String|SportRecord的JSON数组,不包含detail字段|

```
/**
* 跑步数据
*/
SportRecord{
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
    long lastModifyTime;//最后一次更新时间
}
```

### 5.8.4 获取运动详细
接口名称：/sport/getDetail  
接口作用：获取运动详细数据  
接口参数：
|参数|类型|必填|说明| 
|-|-|-|-|
|sportId|UUID|是|运动ID|

返回值：
|返回字段|类型|说明|
|-|-|-|
|errorCode|int|错误码，0代表成功，其他数值代表失败。根据实际接口的错误类型决定失败数值。|
|errorMsg|String|错误描述。errorCode为0时，此字段为空。|
|data|String|SportRecord的JSON对象|

### 5.8.5 获取运动统计数据
接口名称：/sport/getTotal  
接口作用：获取一年内运动的统计数据  
接口参数：
|参数|类型|必填|说明| 
|-|-|-|-|
|无||||

返回值：
|返回字段|类型|说明|
|-|-|-|
|errorCode|int|错误码，0代表成功，其他数值代表失败。根据实际接口的错误类型决定失败数值。|
|errorMsg|String|错误描述。errorCode为0时，此字段为空。|
|data|String|SportTotal的JSON对象|

```
/** 
* 跑步统计数据 
*/ 
SportTotal:{
    int count;//总次数 
    double distance;//总距离
}
```

## 5.9 温度接口
### 5.9.1 上传温度数据
接口名称：/temperature/upload  
接口作用：上传一组温度数据  
接口参数：
|参数|类型|必填|说明| 
|-|-|-|-|
|data|String|是|UploadTemperatureRecord的JSON数组|

返回值：
|返回字段|类型|说明|
|-|-|-|
|errorCode|int|错误码，0代表成功，其他数值代表失败。根据实际接口的错误类型决定失败数值。|
|errorMsg|String|错误描述。errorCode为0时，此字段为空。|
|data|String|UpdatedTemperatureRecord的JSON数组|

```
/**
* 上传的温度数据
*/
UploadTemperatureRecord{
    String date;//该行数据的日期，yyyy-MM-dd日期格式
    List<TemperatureItem> detail;//包含的详细数据
}

/**
* 温度数据
*/
TemperatureItem{
    String time;//该行数据的时间，yyyy-MM-dd HH:mm:ss日期格式
    float body;//体温，单位为摄氏度，保留2位小数
    float wrist;//腕温，单位为摄氏度，保留2位小数
}

/**
* 此次更新天数据的信息
*/
UpdatedTemperatureRecord{
    String date;//该行数据的日期，yyyy-MM-dd日期格式
    int	avgBody;//当天平均体温
    int	avgWrist;//当天平均腕温
    long lastModifyTime;//最后一次更新时间

    long previousModifyTime;//上一次更新时间
}
```

### 5.9.2 获取某段日期的温度数据
接口名称：/temperature/get  
接口作用：获取某段日期用户的温度数据。如果startDate等于endDate，就相当于查询这一天的数据。  
接口参数：
|参数|类型|必填|说明| 
|-|-|-|-|
|startDate|String|是|起始日期，包含这个日期。格式为yyyy-MM-dd|
|endDate|String|是|结束日期，包含这个日期。格式为yyyy-MM-dd|
|needDetail|boolean|否|是否需要包含详细数据，如果不填，默认为false|

返回值：
|返回字段|类型|说明|
|-|-|-|
|errorCode|int|错误码，0代表成功，其他数值代表失败。根据实际接口的错误类型决定失败数值。|
|errorMsg|String|错误描述。errorCode为0时，此字段为空。|
|data|String|TemperatureRecord的JSON数组|

```
/**
* 温度数据
*/
TemperatureRecord{
    String date;//该行数据的日期，yyyy-MM-dd日期格式
    int	avgBody;//当天平均体温
    int	avgWrist;//当天平均腕温
    List<TemperatureItem> detail;//包含的详细数据
    long lastModifyTime;//最后一次更新时间
}
```

# 六、好友接口
## 6.1 搜索用户
接口名称：/relation/search  
接口作用：根据输入的关键字，搜索好友。目前搜索只需要通过完全匹配identityId的方式搜索即可。  
接口参数：
|参数|类型|必填|说明| 
|-|-|-|-|
|content|String|是|搜索关键字|

返回值：
|返回字段|类型|说明|
|-|-|-|
|errorCode|int|错误码，0代表成功，其他数值代表失败。根据实际接口的错误类型决定失败数值。|
|errorMsg|String|错误描述。errorCode为0时，此字段为空。|
|data|String|User的JSON数组，目前结果可能为0个或者1个。以后可能扩展为多个|

```
User{
    long userId;//用户ID
    String nickName//用户昵称
    int sex;//性别    0男，1女
    String birthday;//出生日期，格式为yyyy/M，如1990/5
    float height;//身高，单位cm
    float weight;//体重，单位kg
    String avatar;//头像URL地址
    String identityId;//用户身份ID
}
```

## 6.2 检测用户是否已经为好友关系
接口名称：/relation/check  
接口作用：检测某个用户是否已经是好友。用于客户端界面展示逻辑，如果不是好友关系，显示添加好友界面，如果已经是好友关系，那么显示好友信息页面。  
接口参数：
|参数|类型|必填|说明| 
|-|-|-|-|
|userId|long|是|用户ID|

返回值：
|返回字段|类型|说明|
|-|-|-|
|errorCode|int|错误码，0代表成功，其他数值代表失败。根据实际接口的错误类型决定失败数值。|
|errorMsg|String|错误描述。errorCode为0时，此字段为空。|
|data|int|0表示不是好友关系，1表示已经是好友关系。|

## 6.3 发送好友申请
接口名称：/relation/send  
接口作用：申请好友。  
接口参数：
|参数|类型|必填|说明| 
|-|-|-|-|
|userId|long|是|用户ID|
|mark|String|是|和对方的关系备注|
|message|String|是|打招呼的信息|

返回值：
|返回字段|类型|说明|
|-|-|-|
|errorCode|int|错误码，0代表成功，其他数值代表失败。根据实际接口的错误类型决定失败数值。|
|errorMsg|String|错误描述。errorCode为0时，此字段为空。|

## 6.4 接受好友申请
接口名称：/relation/accept  
接口作用：接受好友申请。处理完后删除该条申请消息  
接口参数：
|参数|类型|必填|说明| 
|-|-|-|-|
|applyId|long|是|申请ID|

返回值：
|返回字段|类型|说明|
|-|-|-|
|errorCode|int|错误码，0代表成功，其他数值代表失败。根据实际接口的错误类型决定失败数值。|
|errorMsg|String|错误描述。errorCode为0时，此字段为空。|

## 6.5 拒绝好友申请
接口名称：/relation/reject  
接口作用：拒绝好友申请。处理完后删除该条申请消息  
接口参数：
|参数|类型|必填|说明| 
|-|-|-|-|
|applyId|long|是|申请ID|

返回值：
|返回字段|类型|说明|
|-|-|-|
|errorCode|int|错误码，0代表成功，其他数值代表失败。根据实际接口的错误类型决定失败数值。|
|errorMsg|String|错误描述。errorCode为0时，此字段为空。|

## 6.6 删除好友
接口名称：/relation/remove  
接口作用：删除好友。  
接口参数：
|参数|类型|必填|说明| 
|-|-|-|-|
|userId|long|是|用户ID|

返回值：
|返回字段|类型|说明|
|-|-|-|
|errorCode|int|错误码，0代表成功，其他数值代表失败。根据实际接口的错误类型决定失败数值。|
|errorMsg|String|错误描述。errorCode为0时，此字段为空。|

## 6.7 修改备注名
接口名称：/relation/rename  
接口作用：修改好友备注名。  
接口参数：
|参数|类型|必填|说明| 
|-|-|-|-|
|userId|long|是|用户ID|
|mark|String|是|新的备注名|

返回值：
|返回字段|类型|说明|
|-|-|-|
|errorCode|int|错误码，0代表成功，其他数值代表失败。根据实际接口的错误类型决定失败数值。|
|errorMsg|String|错误描述。errorCode为0时，此字段为空。|


## 6.8 好友列表
接口名称：/relation/list  
接口作用：查看好友列表。  
接口参数：
|参数|类型|必填|说明| 
|-|-|-|-|
|token|String|是|user_token|

返回值：
|返回字段|类型|说明|
|-|-|-|
|errorCode|int|错误码，0代表成功，其他数值代表失败。根据实际接口的错误类型决定失败数值。|
|errorMsg|String|错误描述。errorCode为0时，此字段为空。|
|data|String|Friend的JSON数组|

## 6.9 好友信息
接口名称：/relation/info  
接口作用：查看好友列表。  
接口参数：
|参数|类型|必填|说明| 
|-|-|-|-|
|userId|long|是|用户ID|

返回值：
|返回字段|类型|说明|
|-|-|-|
|errorCode|int|错误码，0代表成功，其他数值代表失败。根据实际接口的错误类型决定失败数值。|
|errorMsg|String|错误描述。errorCode为0时，此字段为空。|
|data|String|Friend的JSON对象|
```
Friend{
    long userId;//用户ID
    String nickName//用户昵称
    int sex;//性别    0男，1女
    String birthday;//出生日期，格式为yyyy/M，如1990/5
    float height;//身高，单位cm
    float weight;//体重，单位kg
    String avatar;//头像URL地址
    String identityId;//用户身份ID
    String mark;//备注名
    long lastUpdateTime;//用户数据最后更新时间
}
```

## 6.10 获取申请消息列表
接口名称：/relation/msg  
接口作用：获取申请消息列表。  
接口参数：
|参数|类型|必填|说明| 
|-|-|-|-|

返回值：
|返回字段|类型|说明|
|-|-|-|
|errorCode|int|错误码，0代表成功，其他数值代表失败。根据实际接口的错误类型决定失败数值。|
|errorMsg|String|错误描述。errorCode为0时，此字段为空。|
|data|String|Friend的JSON对象|

```
ApplyMsg{
    long applyId; //好友申请ID
    long userId;//用户Id
    String nickName//用户昵称
    String avatar;//头像URL地址
    long time;//申请时间
    int read;//是否已读。0未读，1已读
    String message;//打招呼信息
}
```

## 6.11 将某个时间点之前的消息设置为已读
接口名称：/relation/readMsg  
接口作用：将某个时间点之前的消息设置为已读。因为app要显示有多少条未读消息，所以需要这个接口  
接口参数：
|参数|类型|必填|说明| 
|-|-|-|-|
|time|long|是|时间点|

返回值：
|返回字段|类型|说明|
|-|-|-|
|errorCode|int|错误码，0代表成功，其他数值代表失败。根据实际接口的错误类型决定失败数值。|
|errorMsg|String|错误描述。errorCode为0时，此字段为空。|

## 6.12 获取好友总数据
接口名称：/relation/totalData  
接口作用：获取好友的总数据。   
接口参数：
|参数|类型|必填|说明| 
|-|-|-|-|
|userId|long|是|好友的ID|

返回值：
|返回字段|类型|说明|
|-|-|-|
|errorCode|int|错误码，0代表成功，其他数值代表失败。根据实际接口的错误类型决定失败数值。|
|errorMsg|String|错误描述。errorCode为0时，此字段为空。|
|data|String|FriendTotalData的JSON对象|

```
FriendTotalData{
    long lastUpdateTime;//好友数据最后更新时间。这个更新时间是用户步数，睡眠，心率，血压，血氧，心电这六种数据最后一次的上传时，服务器保存的时间。
    String deviceHardwareInfo;//好友绑定的设备版本信息。‘4.14 同步用户绑定设备的配置’接口用户设置的版本信息
    StepRecord step;//好友30天之内最后一天的步数数据。
    SleepRecord sleep;//好友30天之内最后一天的睡眠数据。不需要包含详细数据。
    HeartRateRecord heartRate;//好友30天之内最后一天的心率数据。不需要包含详细数据。
    BloodPressureRecord bloodPressure;//好友30天之内最后一天的血压数据。不需要包含详细数据。
    OxygenRecord oxygen;//好友30天之内最后一天的血氧数据。不需要包含详细数据。
    EcgRecord ecg;//好友30天之内最后一条心电数据。不需要包含详细数据。
}
```

## 6.13 获取好友心率数据
参考‘5.3.2 获取某段日期的心率数据’接口。参数需要在加上好友friendId 
另外如果参数startDate和endDate为null，就查询最近30天的数据

## 6.14 获取好友血压数据
参考‘5.4.2 获取某段日期的血压数据’。其他参数同上。

## 6.15 获取好友血氧数据
参考‘5.5.2 获取某段日期的血氧数据’。其他参数同上。

## 6.16 获取好友心电列表
参考‘5.7.2 获取某段日期的心电数据’。其他参数同上。

## 6.17 获取好友某个心电的详细数据
参考‘5.7.3 获取某个心电的详细数据’。其他参数同上。

## 6.18 获取好友心电报告
参考‘5.7.4 获取心电报告’。其他参数同上。


# 七、项目接口
## 7.1 版本检测
接口名称：/public/checkVersion  
接口作用：检测是否用版本更新  
接口参数：
|参数|类型|必填|说明| 
|-|-|-|-|
|package|String|否|android应用包名|
|hardwareInfo|String|否|固件信息字符串|

返回值：
|返回字段|类型|说明|
|-|-|-|
|errorCode|int|错误码，0代表成功，其他数值代表失败。根据实际接口的错误类型决定失败数值。|
|errorMsg|String|错误描述。errorCode为0时，此字段为空。|
|data|String|Version的JSON对象|

```
Version{
    String appVersion;  //app版本号
    String appRemark;  //app版本信息
    String appUrl;  //app下载地址
    String hardwareInfo; //固件信息字符串
    String hardwareRemark;  //硬件版本信息
    String hardwareUrl;  //硬件下载地址
}

```

# 八、其他接口

## 8.1 意见反馈
接口名称：/public/feedback  
接口作用：提交意见反馈  
接口参数：
|参数|类型|必填|说明| 
|-|-|-|-|
|contact|String|否|联系方式|
|text|String|否|反馈文字内容|
|images|String|否|`List<String>`的JSON对象，最多包含4张图片的URL|
|files|String|否|`List<String>`的JSON对象，文件URL|
|osInfo|String|否|手机系统,'Android 7.0.1'|
|phoneModel|String|否|手机型号，如'HuaWei-P10'|
|appVersion|String|否|app版本,如'1.0.0'|
|hardwareInfo|String|否|固件信息|

返回值：
|返回字段|类型|说明|
|-|-|-|
|errorCode|int|错误码，0代表成功，其他数值代表失败。根据实际接口的错误类型决定失败数值。|
|errorMsg|String|错误描述。errorCode为0时，此字段为空。|

## 8.2 上传文件
接口名称：/public/uploadFile  
接口作用：用户上传文件，这里只列出需要的参数数据。这个功能是否用ftp或者其他的方式做更好，开发者自行评估。  
接口参数：
|参数|类型|必填|说明| 
|-|-|-|-|
|fileType|int|是|文件类型，0头像图片，1日志图片，2日志文件|
|file|MultipartFile|是|文件MultipartFile数据|

返回值：
|返回字段|类型|说明|
|-|-|-|
|errorCode|int|错误码，0代表成功，其他数值代表失败。根据实际接口的错误类型决定失败数值。|
|errorMsg|String|错误描述。errorCode为0时，此字段为空。|
|data|String|文件url|

## 8.3 天气查询
接口名称：/public/getWeather  
接口作用：查询对应地区的天气。  
接口参数：
|参数|类型|必填|说明| 
|-|-|-|-|
|country|String|是|国家|
|province|String|是|省份|
|city|String|是|城市|

返回值：
|返回字段|类型|说明|
|-|-|-|
|errorCode|int|错误码，0代表成功，其他数值代表失败。根据实际接口的错误类型决定失败数值。|
|errorMsg|String|错误描述。errorCode为0时，此字段为空。|
|data|String|Weather的JSON对象|

```
Weather{
    String text;//天气
    int code;//天气代码
    String temperature;//温度
    String updateTime;//更新时间
}
```

## 8.4 国外天气查询
接口名称：/public/overSeaWeather  
接口作用：查询对应地区的天气。  
接口参数：
|参数|类型|必填|说明| 
|-|-|-|-|
|cityName|String|是|城市|

返回值：
|返回字段|类型|说明|
|-|-|-|
|errorCode|int|错误码，0代表成功，其他数值代表失败。根据实际接口的错误类型决定失败数值。|
|errorMsg|String|错误描述。errorCode为0时，此字段为空。|
|data|String|Weather的JSON对象|

```
Weather{
    String text;//天气
    int code;//天气代码
    String temperature;//温度
    String updateTime;//更新时间
}
```

## 8.5 微信运动
接口名称：/wxsport/getQrCode  
接口作用：绑定微信运动接口。  
接口参数：
|参数|类型|必填|说明| 
|-|-|-|-|
|macAddress|String|是|设备地址|

返回值：
|返回字段|类型|说明|
|-|-|-|
|errorCode|int|错误码，0代表成功，其他数值代表失败。根据实际接口的错误类型决定失败数值。|
|errorMsg|String|错误描述。errorCode为0时，此字段为空。|
|data|String|微信运动绑定的JSON对象|

```
{
  "deviceid": "gh_46aec1fa828f_d89a400019c7b773",
  "qrticket": "http://we.qq.com/d/AQDmZSnSdQ27qeUoyFGlHeGl7MCGW16o1cScaQpW",
}
```

## 8.6 表盘UI样式

接口名称：/public/style/list  
接口作用：查询当前版本支持的表盘样式  
接口参数：

|参数|类型|必填|说明| 
|-|-|-|-|
|hardwareInfo|String|是|硬件字符串|
|uiNum|String|是|UI编号|
|uiSerial|String|是|UI序号|

返回值：
|返回字段|类型|说明|
|-|-|-|
|errorCode|int|错误码，0代表成功，其他数值代表失败。根据实际接口的错误类型决定失败数值。|
|errorMsg|String|错误描述。errorCode为0时，此字段为空。|
|data|String|UIVersion的JSON对象|

```
UIVersion {
    String appNum;
    String appUrl;
    String appRemark;
    List<UIStyle> styles;
}    
```

## 8.7 事件批量上报

接口名称：/public/event/upload  
接口作用：批量上报事件  
接口参数：

|参数|类型|必填|说明| 
|-|-|-|-|
|data|String|是|Event的JSON数组|

返回值：
|返回字段|类型|说明|
|-|-|-|
|errorCode|int|错误码，0代表成功，其他数值代表失败。根据实际接口的错误类型决定失败数值。|
|errorMsg|String|错误描述。errorCode为0时，此字段为空。|

```
Event {
    String eventName;//事件名
    long eventTime;//事件时间
    String phoneModel;//手机型号
    String osInfo;//系统版本
    String appVersion;//app版本
    String hardwareInfo;//硬件字符串
}    
```

## 8.8 新版天气查询

接口名称：/public/getHeCity    
接口作用：根据IP或者经纬度查询城市ID    
接口参数：

|参数|类型|必填|说明| 
|-|-|-|-|
|location|String|否|不填: 服务器自动获取IP并返回城市ID<br>经纬度：经度在前纬度在后，英文,分隔，服务器根据经纬度返回城市ID|


返回值：
|返回字段|类型|说明|
|-|-|-|
|errorCode|int|错误码，0代表成功，其他数值代表失败。根据实际接口的错误类型决定失败数值。|
|errorMsg|String|错误描述。errorCode为0时，此字段为空。|
|data|String|cityInfo的JSON对象|

```
cityInfo {
    cid: "CN101010100",         //城市ID，用来查询天气
    location: "北京",            //城市描述
    parent_city: "北京",         //上级城市
    admin_area: "北京",          //行政区域
    cnty: "中国",                //国家
    lat: "39.90498734",         //纬度
    lon: "116.4052887",         //精度
    tz: "+8.00"                 //时区
}
```

接口名称：/public/getHeWeather  
接口作用：根据城市ID获取天气信息  
接口参数：  

|参数|类型|必填|说明| 
|-|-|-|-|
|cid|String|是|城市ID|

返回值：
|返回字段|类型|说明|
|-|-|-|
|errorCode|int|错误码，0代表成功，其他数值代表失败。根据实际接口的错误类型决定失败数值。|
|errorMsg|String|错误描述。errorCode为0时，此字段为空。|
|data|String|weatherInfo的JSON对象|

```
weatherInfo {
    cond_code: "104",       //天气状态代码, 参见天气代码对应表
    cond_txt: "阴",         //天气状态描述
    tmp: "23",              //温度，默认单位：摄氏度
    fl: "24",                //体感温度，默认单位：摄氏度
    hum: "56",              //相对湿度
    pcpn: "0.0",            //降水量
    pres: "1005",           //大气压强 
    vis: "8",               //能见度，默认单位：公里
    wind_deg: "73",         //风向360角度
    wind_dir: "东北风",      //风向
    wind_sc: "1",           //风力
    wind_spd: "4"           //风速，公里/小时
    cloud: "91",            //云量
}
```

天气代码对应表

|代码|中文|英文|图标|
|--- |--- |--- |--- |
|100|晴|Sunny/Clear|[100.png](https://cdn.heweather.com/cond_icon/100.png)|
|101|多云|Cloudy|[101.png](https://cdn.heweather.com/cond_icon/101.png)|
|102|少云|Few Clouds|[102.png](https://cdn.heweather.com/cond_icon/102.png)|
|103|晴间多云|Partly Cloudy|[103.png](https://cdn.heweather.com/cond_icon/103.png)|
|104|阴|Overcast|[104.png](https://cdn.heweather.com/cond_icon/104.png)|
|200|有风|Windy|[200.png](https://cdn.heweather.com/cond_icon/200.png)|
|201|平静|Calm|[201.png](https://cdn.heweather.com/cond_icon/201.png)|
|202|微风|Light Breeze|[202.png](https://cdn.heweather.com/cond_icon/202.png)|
|203|和风|Moderate/Gentle Breeze|[203.png](https://cdn.heweather.com/cond_icon/203.png)|
|204|清风|Fresh Breeze|[204.png](https://cdn.heweather.com/cond_icon/204.png)|
|205|强风/劲风|Strong Breeze|[205.png](https://cdn.heweather.com/cond_icon/205.png)|
|206|疾风|High Wind, Near Gale|[206.png](https://cdn.heweather.com/cond_icon/206.png)|
|207|大风|Gale|[207.png](https://cdn.heweather.com/cond_icon/207.png)|
|208|烈风|Strong Gale|[208.png](https://cdn.heweather.com/cond_icon/208.png)|
|209|风暴|Storm|[209.png](https://cdn.heweather.com/cond_icon/209.png)|
|210|狂爆风|Violent Storm|[210.png](https://cdn.heweather.com/cond_icon/210.png)|
|211|飓风|Hurricane|[211.png](https://cdn.heweather.com/cond_icon/211.png)|
|212|龙卷风|Tornado|[212.png](https://cdn.heweather.com/cond_icon/212.png)|
|213|热带风暴|Tropical Storm|[213.png](https://cdn.heweather.com/cond_icon/213.png)|
|300|阵雨|Shower Rain|[300.png](https://cdn.heweather.com/cond_icon/300.png)|
|301|强阵雨|Heavy Shower Rain|[301.png](https://cdn.heweather.com/cond_icon/301.png)|
|302|雷阵雨|Thundershower|[302.png](https://cdn.heweather.com/cond_icon/302.png)|
|303|强雷阵雨|Heavy Thunderstorm|[303.png](https://cdn.heweather.com/cond_icon/303.png)|
|304|雷阵雨伴有冰雹|Thundershower with hail|[304.png](https://cdn.heweather.com/cond_icon/304.png)|
|305|小雨|Light Rain|[305.png](https://cdn.heweather.com/cond_icon/305.png)|
|306|中雨|Moderate Rain|[306.png](https://cdn.heweather.com/cond_icon/306.png)|
|307|大雨|Heavy Rain|[307.png](https://cdn.heweather.com/cond_icon/307.png)|
|308|极端降雨|Extreme Rain|[308.png](https://cdn.heweather.com/cond_icon/308.png)|
|309|毛毛雨/细雨|Drizzle Rain|[309.png](https://cdn.heweather.com/cond_icon/309.png)|
|310|暴雨|Storm|[310.png](https://cdn.heweather.com/cond_icon/310.png)|
|311|大暴雨|Heavy Storm|[311.png](https://cdn.heweather.com/cond_icon/311.png)|
|312|特大暴雨|Severe Storm|[312.png](https://cdn.heweather.com/cond_icon/312.png)|
|313|冻雨|Freezing Rain|[313.png](https://cdn.heweather.com/cond_icon/313.png)|
|314|小到中雨|Light to moderate rain|[314.png](https://cdn.heweather.com/cond_icon/314.png)|
|315|中到大雨|Moderate to heavy rain|[315.png](https://cdn.heweather.com/cond_icon/315.png)|
|316|大到暴雨|Heavy rain to storm|[316.png](https://cdn.heweather.com/cond_icon/316.png)|
|317|暴雨到大暴雨|Storm to heavy storm|[317.png](https://cdn.heweather.com/cond_icon/317.png)|
|318|大暴雨到特大暴雨|Heavy to severe storm|[318.png](https://cdn.heweather.com/cond_icon/318.png)|
|399|雨|Rain|[399.png](https://cdn.heweather.com/cond_icon/399.png)|
|400|小雪|Light Snow|[400.png](https://cdn.heweather.com/cond_icon/400.png)|
|401|中雪|Moderate Snow|[401.png](https://cdn.heweather.com/cond_icon/401.png)|
|402|大雪|Heavy Snow|[402.png](https://cdn.heweather.com/cond_icon/402.png)|
|403|暴雪|Snowstorm|[403.png](https://cdn.heweather.com/cond_icon/403.png)|
|404|雨夹雪|Sleet|[404.png](https://cdn.heweather.com/cond_icon/404.png)|
|405|雨雪天气|Rain And Snow|[405.png](https://cdn.heweather.com/cond_icon/405.png)|
|406|阵雨夹雪|Shower Snow|[406.png](https://cdn.heweather.com/cond_icon/406.png)|
|407|阵雪|Snow Flurry|[407.png](https://cdn.heweather.com/cond_icon/407.png)|
|408|小到中雪|Light to moderate snow|[408.png](https://cdn.heweather.com/cond_icon/408.png)|
|409|中到大雪|Moderate to heavy snow|[409.png](https://cdn.heweather.com/cond_icon/409.png)|
|410|大到暴雪|Heavy snow to snowstorm|[410.png](https://cdn.heweather.com/cond_icon/410.png)|
|499|雪|Snow|[499.png](https://cdn.heweather.com/cond_icon/499.png)|
|500|薄雾|Mist|[500.png](https://cdn.heweather.com/cond_icon/500.png)|
|501|雾|Foggy|[501.png](https://cdn.heweather.com/cond_icon/501.png)|
|502|霾|Haze|[502.png](https://cdn.heweather.com/cond_icon/502.png)|
|503|扬沙|Sand|[503.png](https://cdn.heweather.com/cond_icon/503.png)|
|504|浮尘|Dust|[504.png](https://cdn.heweather.com/cond_icon/504.png)|
|507|沙尘暴|Duststorm|[507.png](https://cdn.heweather.com/cond_icon/507.png)|
|508|强沙尘暴|Sandstorm|[508.png](https://cdn.heweather.com/cond_icon/508.png)|
|509|浓雾|Dense fog|[509.png](https://cdn.heweather.com/cond_icon/509.png)|
|510|强浓雾|Strong fog|[510.png](https://cdn.heweather.com/cond_icon/510.png)|
|511|中度霾|Moderate haze|[511.png](https://cdn.heweather.com/cond_icon/511.png)|
|512|重度霾|Heavy haze|[512.png](https://cdn.heweather.com/cond_icon/512.png)|
|513|严重霾|Severe haze|[513.png](https://cdn.heweather.com/cond_icon/513.png)|
|514|大雾|Heavy fog|[514.png](https://cdn.heweather.com/cond_icon/514.png)|
|515|特强浓雾|Extra heavy fog|[515.png](https://cdn.heweather.com/cond_icon/515.png)|
|900|热|Hot|[900.png](https://cdn.heweather.com/cond_icon/900.png)|
|901|冷|Cold|[901.png](https://cdn.heweather.com/cond_icon/901.png)|
|999|未知|Unknown|[999.png](https://cdn.heweather.com/cond_icon/999.png)|


## 8.9 新表盘列表

接口名称：/public/dial/list  
接口作用：查询符合的表盘列表  
接口参数：

|参数|类型|必填|说明| 
|-|-|-|-|
|hardwareInfo|String|是|硬件字符串|
|lcd|int|是|表盘LCD分辨率尺寸的ID值|
|toolVersion|String|是|表盘工具版本|

返回值：
|返回字段|类型|说明|
|-|-|-|
|errorCode|int|错误码，0代表成功，其他数值代表失败。根据实际接口的错误类型决定失败数值。|
|errorMsg|String|错误描述。errorCode为0时，此字段为空。|
|data|List|Dial的JSON列表|

```
Dial {
    int dialNum;
    int lcd;
    String toolVersion;
    String binUrl;
    int binVersion;
    String imgUrl;
    String deviceImgUrl;
    String name;
    int downloadCount;
}    
```

## 8.10 设备外壳

接口名称：/public/device/shell  
接口作用：查询设备外壳的图片  
接口参数：

|参数|类型|必填|说明| 
|-|-|-|-|
|hardwareInfo|String|是|硬件字符串|

返回值：
|返回字段|类型|说明|
|-|-|-|
|errorCode|int|错误码，0代表成功，其他数值代表失败。根据实际接口的错误类型决定失败数值。|
|errorMsg|String|错误描述。errorCode为0时，此字段为空。|
|data|String|手环外壳url|
