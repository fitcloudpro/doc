# Hft后台接口文档

**修改日志** 
**2018-1-8：**
1.增加找回密码发送验证码接口(54)

**2017-12-15：**
1.修改绑定接口(50)增加mac地址，修改Guest对象增加绑定的mac地址

**2017-11-30：**
1、修改运动目标设置和获取接口goalSet(27)，goalGet(28)

**2017-11-1：**
1、修改意见反馈接口，增加字段

**2017-09-26：**
1、修改LatLng
2、删除RunBean的isDevice字段

**2017-09-22：**
1、修改RunBean删除几个字段

**2017-09-19：**
1、修改RunBean增加是否是手表启动和经纬度列表字段

**2017-09-08：**
1、修改设置运动目标goalSet(27),获取运动目标goalGet(28),RunBean增加运动类型

**2017-08-28：**
1、修改更新用户信息接口updatePersonInfo(8)，增加私人参考模式开关

**2017-08-17：**
1、增加带验证码注册用户接口registUserWithCode(53)

**2017-07-14：**
1、修改心电更新接口updateEcg(34)
2、修改获取心电数据列表findEcgTotal(35)

**2017-06-06：**
1、增加国外天气接口overSeaWeather(52)

**2017-05-25：**
1、增加绑定版本新接口bindHardwareVersionNew(50)
2、增加更新版本新接口updateVersionNew(51)
3、修改Guest增加几个字段

**2017-05-24：**
1、增加意见反馈接口feedBack(49)

**2017-05-15：** 
1、增加获取某用户的二维码字符串接口getUserQrCode(37)
2、增加设置某用户的身份id接口setIdentityId(38)
3、增加搜索好友接口searchFriend(39)
4、增加添加好友请求接口addFriend(40)
5、增加修改好友备注名接口updateFriendRemark(41)
6、增加获取新好友请求接口getNewRequest(42)
7、增加接受好友请求接口acceptFriend(43)
8、增加拒绝好友请求接口urefuseFriend(44)
9、增加获取被拒绝好友请求的列表接口getRefuse(45)
10、增加删除好友或者取消关注接口cancelFriend(46)
11、增加获取我关注的好友列表接口getMyFocusList(47)
12、增加获取关注我的好友列表接口getFocusMeList(48)

**2017-05-12：** 
1、修改心电数据上传接口updateEcg(34),增加uuid,收缩压和舒张压
2、修改查询心电数据列表接口findEcgTotal(35)uuid，返回uuid
3、修改查询心电数据明细接口findEcgDetail(36)，ecgId为uuid

**2017-05-11：** 
1、修改心电数据上传接口updateEcg(34)
2、修改查询心电数据列表接口findEcgTotal(35)
3、增加查询心电数据明细接口findEcgDetail(36)

**2017-05-10：** 
1、增加心电数据上传接口updateEcg(34)
2、增加查询某天心电数据接口findEcg(35)

**2017-05-04：** 
1、修改uploadRun接口的RunDetail，增加isRestart字段(29)

**2017-02-21：** 
1、增加设置睡眠开始时间和结束时间接口(32)
2、增加获取睡眠开始时间和结束时间接口(33)

**2017-02-15：** 
1、增加获取跑步总数据接口(31)

**2017-01-19：** 
1、固件升级增加是否强制升级字段(16)
2、增加设置跑步目标接口(27)
3、增加获取跑步目标接口(28)
4、增加上传跑步数据接口(29)
5、增加获取某用户某段时间的跑步数据接口(30)

**2016-11-29：** 
1、第三方登录接口增加一个是否已注册的字段(2)

**2016-11-25：** 
1、增加获取使用帮助接口(26)

**2016-11-4：** 
1、增加微信获取二维码接口(25)

**2016-11-1：** 
1、修改硬件更新接口(16),修改返回的版本字段为一个

**2016-10-18：** 
1、修改硬件更新接口(16)添加了sdk版本，patch版本，os和对应app版本几个参数

**2016-09-14：** 
1、修改软硬件更新接口（16）添加一个参数

**2016-09-13：** 
1、修改实时天气接口（24）更新了2个参数

**2016-09-08：** 
1、添加实时天气接口（24）

**2016-09-05：** 
1、软硬件接口更新(16),更新了第2个参数（patchApp），为 软件号+flash号+版本号 的拼接

**2016-08-26：** 
1、修改更新用户资料接口(8),增加了3个参数（systolicNum，diastolicNum，wearLeftHand） 
2、修改更新用户数据接口（3），实体添加了bloodOxygenNum、highBloodNum、lowBloodNum、breathingRateNum这4个属性 
3、增加第18、19、20、21、22、23六个接口

**2016-07-20:** 
1、添加检测是否注册接口（17） 
2、修改更新用户数据接口（3），实体添加了kmNum和calorieNum这两个属性

**2016-06-28：** 
1、修改软硬件更新接口（16），添加了两个参数 
2、修改用户与硬件版本号绑定接口（7），修改了参数 
3、修改了用户个人实体，添加如下两个属性，去掉hardwareNum这个属性 
private String projectHardware;//项目号 
private String patchApp; //硬件版本号

**2016-06-20：** 
1、注册接口（5）和更新用户资料接口（8） 身高体重 Integer类型换成了Float 类型

##**一、通用说明**

后台地址：host =xxxx 
用户名: xx 
密码: xx

##**二、前台与后台交互API**

http请求get或者post;
数据格式统一为json;
数据结构例子; 
带数据返回： 
｛"msg":"提示信息","status"：0,"errCode":0, 
“user”:{ 
“id”:”1”, 
”name”:”王小二” 
}｝ 
不带数据返回： 
｛"msg":"提示信息","status"：0,"errCode":0｝ 
status： 0 表示请求失败 1表示请求成功 
errCode: 
0 参数为空 
1 系统繁忙 
2 该用户已经存在 
3 密码错误 
4 该用户不存在 
5 两次密码输入不一样 
6 验证码失效 
7 验证码输入错误 
8 短信发送失败 
9 邮件发送失败 
10 数据有误
11 获取token失败
12 无该城市信息
13 没有查询到天气信息
14 该ID已存在
15 请求添加的用户不存在
16 添加失败
17 该记录不存在
18 请求的用户已经是好友

---
##**1、邮件找回密码**

接口名称：sendMail 
接口作用：邮件找回密码 
接口参数：

|参数名|	类型|	说明|
| --------   | -----:  | :----:  |
|email|	String|	邮箱地址|
|language|	String|	语言(可选，不传或者zh-CN为中文，其他英文)|
返回值：

|返回字段	|类型	|说明|
| --------   | -----:  | :----:  |
|msg|	String|	请求信息|
|status|	int|	信息编码 1 请求成功 0 请求失败|
示例: http://demo.htimes.cn/open/sendMail.action?email=657044849@qq.com

##**2、第三方登陆**

接口名称：otherLogin 
接口作用：第三方登陆 
接口参数：

|参数名|	类型|	说明|
| --------   | -----:  | :----:  |
|openId	|String	|第三方唯一标识|
|nickName|	String|	第三方用户昵称|
|openAppName|	String|	第三方app名称|
返回值：

|返回字段|	类型|	说明|
| --------   | -----:  | :----:  |
|msg|	String	|请求信息|
|status|	int	|信息编码 1 请求成功 0 请求失败|
|isRegister|   int|是否已注册，1是已注册，0是未注册|
|object	|String	|json对象< Guest >|
示例: http://demo.htimes.cn/open/otherLogin.action?openId=657&nickName=test&openAppName=sina

##**3、更新用户数据**

接口名称：updateEnergy 
接口作用：更新用户数据 
接口参数：

|参数名	|类型|	说明|
| --------   | -----:  | :----:  |
|guestId|	Integer|	用户ID|
|energyInfo|	String|	json数组 List< Energy >|
返回值：

|返回字段	|类型|	说明|
| --------   | -----:  | :----:  |
|msg|	String|	请求信息|
|status	|int|	信息编码 1 请求成功 0 请求失败|
示例: http://demo.htimes.cn/open/updateEnergy.action?guestId=6&energyInfo=[{}]

Energy:

    /**
    * 自增id
    */
    private int id;
    /**
    * 紫外线数值
    */
    private int rays;
    /**
    * 步数
    */
    private int stepNum; 
    /**
    * 睡眠时间
    */
    private int sleepTime;
    /**
    * 深睡时间
    */
    private int deepTime;  
    /**
    * 浅睡时间
    */
    private int lightTime;
    /**
    * 心率平均值
    */
    private int heartNum;
    /**
    * 日期   单位 秒（s）
    */
    private long date;
    private int guestId;//所属用户
    /**
    * 公里数
    */
    private float kmNum;
    /**
    * 卡路里数
    */
    private float calorieNum;
    /**
    * 血氧
    */
    private int bloodOxygenNum;
    /**
    * 高血压值
    */
    private int highBloodNum;
    /**
    * 低血压值
    */
    private int lowBloodNum;
    /**
    * 呼吸频率(单位：分钟)
    */
    private int breathingRateNum;

##**4、获取用户近期一个月的数据**

接口名称：getEnergy 
接口作用：更新用户数据 
接口参数：

|参数名|	类型|	说明|
| --------   | -----:  | :----:  |
|guestId|	Integer	|用户ID|
返回值：

|返回字段|	类型|	说明|
| --------   | -----:  | :----:  |
|msg|	String	|请求信息|
|status	|int|	信息编码 1 请求成功 0 请求失败|
|object|	String|	json对象< Energy >|
示例: http://demo.htimes.cn/open/getEnergy.action?guestId=1

##**5、注册用户**

接口名称：registUser2 
接口作用：注册用户 
接口参数：

|参数名|	类型|	说明|
| --------   | -----:  | :----:  |
|userName|	String|	用户的名称 (必需)|
|password|	String|	用户密码 (必需)|
|nickName|	String	|用户昵称|
|flag|	Integer|	0 安卓 1 苹果|
|sex|	Integer|	0 男 1 女|
|birthDate|	String|	出生日期|
|weight	|Float|	体重 kg|
|height|	Float|	身高 cm|
|base64Str|	String|	头像base64字符串|
返回值：

|返回字段|	类型|	说明|
| --------   | -----:  | :----:  |
|msg|	String|	请求信息|
|status|	int	|信息编码 1 请求成功 0 请求失败|
|object|	String|	json对象< Guest >|
示例: http://demo.htimes.cn/open/registUser.action?userName=657044849@qq.com&password=123

##**6、用户登陆**

接口名称：loginUser2 
接口作用：用户登陆 
接口参数：

|参数名	|类型|	说明|
| --------   | -----:  | :----:  |
|userName|	String	|用户的名称|
|password|	String|	用户密码|
返回值：

|返回字段	|类型|	说明|
| --------   | -----:  | :----:  |
|msg|	String	|请求信息|
|status	|int	|信息编码 1 请求成功 0 请求失败|
|object	|String	|json对象< Guest >|
Guest:

    private int guestId;//用户的ID
    private String nickName;  //用户昵称
    private String name;//用户的名称
    private String password;//用户密码
    private String note;//用户备注
    private int flag; //0 安卓   1  苹果
    private int sex; // 0  男   1 女
    private String birthDate;  //出生日期
    private Float weight; //体重   kg
    private Float height;  // 身高 cm
    private Date createDate = new Date();//用户创建时间
    private String projectHardware;//项目号
    private String patchApp;   //硬件版本号
    private String openId;//第三方唯一标识
    private String openAppName;//第三方app名称
    private String phoneNums; //求救电话号码  用","隔开
    private String content;  //求救内容
    private String headImg; //头像
    private int systolicNum;  //收缩压
    private int diastolicNum; // 舒张压
    private int wearLeftHand; // 0 是左手  1是右手   
	private int type;//目标类型，0是未设置，1是设置距离，2是设置时长
	private double distance;//跑步距离目标
	private Integer runTime;//跑步时长目标
	private String identityId;//身份id
	private String hardwareInfo;//固件信息字符串(长度64)
	private long sleepStartTime;//睡眠开始时间
	private long sleepEndTime;//睡眠结束时间
	private int privacyTag;//私人参考模式
	private String macAddress;//绑定的mac地址
	
示例: http://demo.htimes.cn/open/loginUser2.action?userName=657044849@qq.com&password=123

##**7、用户与硬件版本号绑定**

接口名称：bindHardwareVersion 
接口作用：用户与硬件版本号绑定 
接口参数：

|参数名	|类型|	说明|
| --------   | -----:  | :----:  |
|guestId|	Integer	|用户ID|
|projectHardware|	String	|项目号|
|patchApp|	String|	硬件版本号|
返回值：

|返回字段|	类型|	说明|
| --------   | -----:  | :----:  |
|msg|	String	|请求信息|
|status	|int	|信息编码 1 请求成功 0 请求失败|
示例: http://demo.htimes.cn/open/bindHardwareVersion.action?guestId=6&projectHardware=123&patchApp=1321

##**8、更新用户资料**

接口名称：updatePersonInfo 
接口作用：更新用户资料 
接口参数：

|参数名	|类型|	说明|
| --------   | -----:  | :----:  |
|guestId|	Integer|	用户ID|
|nickName|	String|	用户昵称 （可选）|
|flag	|Integer|	0 安卓 1 苹果 （可选）|
|sex|	Integer	|0 男 1 女 （可选）|
|birthDate|	String|	出生日期 （可选）|
|weight	|Float	|体重 kg （可选）|
|height	|Float|	身高 cm （可选）|
|base64Str|	String	|头像base64字符串 （可选,url可直接传）|
|systolicNum|	Integer|	收缩压值 （可选）|
|diastolicNum|	Integer|	舒张压值 （可选）|
|wearLeftHand|	int|	手表所佩戴的部位 0 是左手 1是右手|
|privacyTag| int| 私人参考模式，0是关闭，1是开启|
返回值：

|返回字段	|类型|	说明|
| --------   | -----:  | :----:  |
|msg|	String	|请求信息|
|status|	int|	信息编码 1 请求成功 0 请求失败|
例如: http://demo.htimes.cn/open/updatePersonInfo.action?birthDate=123

##**9、发送验证码**

接口名称：sendCode 
接口作用：发送验证码 
接口参数：

|参数名	|类型|	说明|
| --------   | -----:  | :----:  |
|phoneNum|	String|	电话号码|
返回值：

|返回字段	|类型|	说明|
| --------   | -----:  | :----:  |
|msg|	String|	请求信息|
|status	|int|	信息编码 1 请求成功 0 请求失败|
例如: http://demo.htimes.cn/open/sendCode.action?phoneNum=123

##**10、找回密码(updateUserPwd)**

接口名称：updateUserPwd 
接口作用：找回密码 
接口参数：

|参数名	|类型|	说明|
| --------   | -----:  | :----:  |
|phoneNum|	String	|电话号码|
|code|	String	|验证码|
|newPwd	|String	|新密码|
返回值：

|返回字段|	类型	|说明|
| --------   | -----:  | :----:  |
|msg|	String|	请求信息|
|status	|int|信息编码 1 请求成功 0 请求失败|
例如: http://demo.htimes.cn/open/updateUserPwd.action?phoneNum=123&code=425574&newPwd=321343

##**11、发急救短信(firstAidSms)**

接口名称：firstAidSms 
接口作用：急救发短信 
接口参数：

|参数名	|类型	|说明|
| --------   | -----:  | :----:  |
|guestId|	String|	用户ID|
|address|	String|	地址（非必填）|
|longitude|	String	|经度（非必填）|
|latitude|	String|	纬度（非必填）|
返回值：

|返回字段|	类型|	说明|
| --------   | -----:  | :----:  |
|msg|	String|	请求信息|
|status	|int|	信息编码 1 请求成功 0 请求失败|
例如: http://demo.htimes.cn/open/firstAidSms.action?guestId =123

##**12、设置求救信息(bindAidPhones)**

接口名称：bindAidPhones 
接口作用：设置求救信息 
接口参数：

|参数名	|类型	|说明|
| --------   | -----:  | :----:  |
|guestId|	Integer|	用户ID|
|isOn|	Integer|	是否开启急救 1开启 0关闭|
|phoneNums|	String|	电话号码 多个可用","拼接|
|content|	String|	求救内容|
返回值：

|返回字段|	类型|	说明|
| --------   | -----:  | :----:  |
|msg|	String	|请求信息|
|status	|int|	信息编码 1 请求成功 0 请求失败|
例如: http://demo.htimes.cn/open/bindAidPhones.action?guestId=1&phoneNums=123,3245&content=sos&isOn=1

##**13、获取求救信息(findAidPhones)**

接口名称：findAidPhones 
接口作用：获取求救信息 
接口参数：

|参数名|	类型|	说明|
| --------   | -----:  | :----:  |
|guestId|	Integer	|用户ID|
返回值：

|返回字段|	类型|	说明|
| --------   | -----:  | :----:  |
|msg|	String|	请求信息|
|status|	int	|信息编码 1 请求成功 0 请求失败|
|object	|String	|json字符串对象(AidBean)|
例如: http://demo.htimes.cn/open/findAidPhones.action?guestId=1

AidBean:

    /**
    * 用户ID
    */
    private Integer guestId;
    /**
    * 电话号码
    */
    private String phoneNums;
    /**
    * 求救内容
    */
    private String content;
    /**
    * 是否开启
    */
    private Integer isOn;


##**14、更新心率数据内容(updateHeart)**

接口名称：updateHeart 
接口作用：更新心率数据内容 
接口参数：

|参数名|	类型|	说明|
| --------   | -----:  | :----:  |
|guestId|	int	|用户Id|
|heartInfo|	String	|心率数据 json对象(HeartBean)|
返回值：

|返回字段|	类型|	说明|
| --------   | -----:  | :----:  |
|msg|	String|	请求信息|
|status	|int|	信息编码 1 请求成功 0 请求失败|
例如: http://demo.htimes.cn/open/updateHeart.action?guestId=1&heartInfo={}

HeartBean：

    /**
    * 测试时间（当天0点时间）
    */
    private long date;
    private List<HeartRate> list = new ArrayList<HeartRate>();
    
HeartRate:

    /**
    * 心率ID
    */
    private int id;
    /**
    * 心跳次数
    */
    private Integer count;
    /**
    * 心率产生的日期 单位(秒)
    */
    private long date;
    /**
    * 创建时间
    */
    private Date createDate = new Date();


##**15、获取该测试下的心率信息(findHeartRate)**

接口名称：findHeartRate 
接口作用：获取该测试 下的心率信息 
接口参数：

|参数名	|类型|	说明|
| --------   | -----:  | :----:  |
|guestId|	int	|用户ID|
|date|	long|	时间|
返回值：

|返回字段|	类型|	说明|
| --------   | -----:  | :----:  |
|msg|	String|	请求信息|
|status	|int|	信息编码 1 请求成功 0 请求失败|
|object	|String|	json数组(listHeartRate)|
例如: http://demo.htimes.cn/open/findHeartRate.action?guestId=1&date=12312424

HeartRate:

    /**
    * 心率ID
    */
    private int id;
    /**
    * 心跳次数
    */
    private Integer count;
    /**
    * 心率产生的日期 单位(秒)
    */
    private long date;


##**16、软件硬件更新接口（updateVersion）**

接口名称：updateVersion 
接口作用：软件硬件更新接口 
接口参数：无

|参数名|	类型|	说明|
| --------   | -----:  | :----:  |
|packageName|	String|	android应用包名（非必填）|
|projectHardware|	String|	项目号|
|patchApp|	String|	硬件版本号|
|matchAppVersion| String|匹配APP版本号|
|os|String|手机系统版本:传android或ios|
|sdkVersion|String|固件sdk版本号|
|patchVersion|String|固件patch版本号|
返回值：

| 返回字段| 	类型| 	说明| 
| --------   | -----:  | :----:  |
| msg| 	String| 	请求信息| 
| status| 	int| 	信息编码 1 请求成功 0 请求失败| 
| object| 	String| 	json对象(LastVersion)| 
例如: http://demo.htimes.cn/open/updateVersion.action

LastVersion:

    private String appNum;  //软件版本号
    private String appName;  //软件版本名称
    private String hardwareNum;  //硬件版本号
    private String hardwareName; //硬件版本名称
    private String appUrl;       //app版本下载地址
    private String hardwareUrl;  //硬件下载地址
    private String note;  //硬件版本备注
    private String compulsion_tag;//是否强制升级，1是，0否




##**17、检测用户是否已经注册（checkRegist）**

接口名称：checkRegist 
接口作用：检测用户是否已经注册 
接口参数：

|参数名|	类型|	说明|
| --------   | -----:  | :----:  |
|userName|	String|	用户名|
返回值：

|返回字段|	类型|	说明|
| --------   | -----:  | :----:  |
|msg|	String|	请求信息|
|status|	int|	信息编码 1 请求成功 0 请求失败|
|errCode|	int|	错误编码 2 该用户已经注册 4 该用户不存在|
例如: http://demo.htimes.cn/open/checkRegist.action?userName=1232154234

##**18、 更新血氧含量(updateOxygen)**

接口名称：updateOxygen 
接口作用：更新血氧含量 
接口参数：

|参数名|	类型|	说明|
| --------   | -----:  | :----:  |
|guestId|	int	|用户Id|
|messageInfo|	String	|心率数据 json对象(BloodOxygenBean)|
返回值：

|返回字段|	类型|	说明|
| --------   | -----:  | :----:  |
|msg|	String	|请求信息|
|status	|int|	信息编码 1 请求成功 0 请求失败|
例如: http://demo.htimes.cn/open/updateOxygen.action?guestId=1&messageInfo={}

BloodOxygenBean：

    /**
    * 测试时间（当天0点时间）
    */
    private long date;
    private List<BloodOxygen> list = new ArrayList<BloodOxygen>();
    
BloodOxygen: 

    private int id; 
    /** 
    * 血氧含量 
    / 
    private int num; 
    /* 
    * 心率产生的日期 单位(秒) 
    */ 
    private long date;

##**19、获取用户下某天的测试血氧信息(findBloodOxygen)**

接口名称：findBloodOxygen 
接口作用：获取用户下某天的测试血氧信息 
接口参数：

|参数名|	类型|	说明|
| --------   | -----:  | :----:  |
|guestId|	int|	用户ID|
|date|	long|	时间|
返回值：

|返回字段|	类型|	说明|
| --------   | -----:  | :----:  |
|msg|	String|	请求信息|
|status|	int	|信息编码 1 请求成功 0 请求失败|
|object	|String	|json数组(List< BloodOxygen >)|
例如: http://demo.htimes.cn/open/findBloodOxygen.action?guestId=1&date=12312424

##**20、 更新血压数据(updatePressure)**

接口名称：updatePressure 
接口作用：更新血压数据 
接口参数：

|参数名|	类型|	说明|
| --------   | -----:  | :----:  |
|guestId|	int	|用户Id|
|messageInfo|	String|	心率数据 json对象(BloodPressureBean)|
返回值：

|返回字段|	类型|	说明|
| --------   | -----:  | :----:  |
|msg|	String|	请求信息|
|status|	int|	信息编码 1 请求成功 0 请求失败|
例如: http://demo.htimes.cn/open/updatePressure.action?guestId=1&messageInfo={}

BloodPressureBean：

    /**
    * 测试时间（当天0点时间）
    */
    private long date;
    private List<BloodPressure> list = new ArrayList<BloodPressure>();
    
BloodPressure:

    private int id;
    /**
    * 高血压值
    */
    private int highNum;
    /**
    * 低血压值
    */
    private int lowNum;
    /**
    * 心率产生的日期 单位(秒)
    */
    private long date;


##**21、获取某用户某天的测试的血压数据(findBloodPressure)**

接口名称：findBloodPressure 
接口作用：获取某用户某天的测试的血压数据 
接口参数：

|参数名	|类型|	说明|
| --------   | -----:  | :----:  |
|guestId|	int|	用户ID|
|date|	long|	时间|
返回值：

|返回字段|	类型|	说明|
| --------   | -----:  | :----:  |
|msg|	String|	请求信息|
|status|	int	|信息编码 1 请求成功 0 请求失败|
|object|	String|	json数组(List< BloodPressure >)|
例如: http://demo.htimes.cn/open/findBloodPressure.action?guestId=1&date=12312424

##**22、 更新呼吸频率数据(updateBreathRate)**

接口名称：updateBreathRate 
接口作用：更新呼吸频率数据 
接口参数：

|参数名|	类型|	说明|
| --------   | -----:  | :----:  |
|guestId|	int	|用户Id|
|messageInfo|	String|	心率数据 json对象(BreathRateBean)|
返回值：

|返回字段|	类型|	说明|
| --------   | -----:  | :----:  |
|msg|	String|	请求信息|
|status|	int|	信息编码 1 请求成功 0 请求失败|
例如: http://demo.htimes.cn/open/updateBreathRate.action?guestId=1&messageInfo={}

BreathRateBean：

    /**
    * 测试时间（当天0点时间）
    */
    private long date;
    private List<BreathRate> list = new ArrayList<BreathRate>();
    
BreathRate:

    private int id;
    /**
    * 呼吸频率数据
    */
    private int num;
    /**
    * 呼吸频率的日期 单位(秒)
    */
    private long date;


##**23、获取某用户某天的测试的呼吸频率数据(findBreathRate)**

接口名称：findBreathRate 
接口作用：获取某用户某天的测试的呼吸频率数据 
接口参数：

|参数名	|类型	|说明|
| --------   | -----:  | :----:  |
|guestId|	int|	用户ID|
|date|	long|	时间|
返回值：

|返回字段|	类型|	说明|
| --------   | -----:  | :----:  |
|msg|	String	|请求信息|
|status|	int	|信息编码 1 请求成功 0 请求失败|
|object|	String|	json数组(List< BreathRate >)|
例如: http://demo.htimes.cn/open/findBreathRate.action?guestId=1&date=12312424

##**24、获取实时天气（findWeatherInfo）**

接口名称：findWeatherInfo 
接口作用：更新用户数据 
接口参数：

| 参数名	| 类型	| 说明 |
| --------   | -----:  | :----:  |
| cityName	| String|	城市名称（必填）|
| province	| String|	省名称（必填） |
| language	| String| 	语言 （非必填），默认中文简体| 
返回值：

| 返回字段 |  类型 |  说明  |
| --------   | -----:  | :----:  |
| msg	| String |	请求信息|
| status| 	int	| 信息编码 1 请求成功 0 请求失败|
|object	|String	|json对象< Energy >|
参考链接： http://www.thinkpage.cn/doc#now 天气实况 
示例: http://demo.htimes.cn/open/findWeatherInfo.action?guestId=1

##**25、获取微信二维码（getQrCode）**

接口名称：getQrCode 
接口作用：获取二维码
接口参数：

| 参数名	| 类型	| 说明 |
| --------   | -----:  | :----:  |
| guestId	| String|	用户id（必填）|
| macAddress	| String|	手环mac地址（必填） |
返回值：

| 返回字段 |  类型 |  说明  |
| --------   | -----:  | :----:  |
| qrticket	| String |	二维码地址|
| deviceid| 	String	| 设备id|
|authResult	|String	|硬件授权结果|
示例: http://demo.htimes.cn/open/getQrCode.action?guestId=1&macAddress=889900

##**26、获取使用帮助（teach）**

接口名称：teach 
接口作用：获取使用帮助
接口参数：

| 参数名	| 类型	| 说明 |
| --------   | -----:  | :----:  |
|language	| String|	语言（必填有zh-CN,en,zh-HK）|
返回值：

直接是一个网页

示例: http://demo.htimes.cn/open/teach.action?language=zh-CN

##**27、设置运动目标（goalSet）**

接口名称：goalSet 
接口作用：设置跑步目标
接口参数：

| 参数名	| 类型	| 说明 |
| --------   | -----:  | :----:  |
|guestId	| int|	用户id(必填)|
|sportType	| int|	运动类型(0是未设置，1是跑步，2是跑步机，3是骑行)|
|goalType	| int|	运动目标类型(0是未设置，1是设置距离，2是设置时长)|
|goalDistance	| double|	运动目标距离(goalType为1时必传，只传km的数据)|
|goalTime	| int|	运动目标时间(goalType为2时必传，传单位秒的数据)|
返回值：
| 返回字段 |  类型 |  说明  |
| --------   | -----:  | :----:  |
| msg	| String |	请求信息|
| status| 	int	| 信息编码 1 请求成功 0 请求失败|

示例: http://demo.htimes.cn/open/goalSet.action?sportType=1&goalDistance=100&goalType=1&goalDistance=102&guestId=2

##**28、获取运动目标（goalGet）**

接口名称：goalGet 
接口作用：获取跑步目标
接口参数：

| 参数名	| 类型	| 说明 |
| --------   | -----:  | :----:  |
|guestId	| int|	用户id(必填)|
|sportType	| int|	运动类型(必填)|

返回值：
| 返回字段 |  类型 |  说明  |
| --------   | -----:  | :----:  |
| msg	| String |	请求信息|
| status| 	int	| 信息编码 1 请求成功 0 请求失败|
| object | 	string	| json对象< Goal >|

示例: http://demo.htimes.cn/open/goalGet.action?guestId=24

Goal:
   /**
    * 运动目标数据
    */
    private int sportType;  //运动类型
	private int goalType;//目标类型
	private double goalDistance;  //目标距离
    private int goalTime;//目标时间

##**29、上传跑步数据（uploadRun）**

接口名称：uploadRun 
接口作用：上传跑步数据,每次跑步结束上传
接口参数：

|参数名|	类型|	说明|
| --------   | -----:  | :----:  |
|guestId|	int	|用户Id(必填)|
|runInfo|	String|	跑步数据 json对象(RunBean)数组|
返回值：

|返回字段|	类型|	说明|
| --------   | -----:  | :----:  |
|msg|	String|	请求信息|
|status|	int|	信息编码 1 请求成功 0 请求失败|
例如: http://demo.htimes.cn/open/uploadRun.action?guestId=1&runInfo=[{},{},{}]

RunBean：

    /**
    * 跑步数据
    */
    private long date;//跑步时间
	
	private double distance;//跑步距离
	
	private String pace;//配速
	
	private double calorie;//消耗卡路里
	
	private int time;//跑步总时长
	
	private int stepNum;//总步数
	
	private double climb;//爬升
	
	private int locationType;//定位类型0是国内，1是国外，默认0
	
	private int sportType;//运动类型，1是手环上骑行，2是APP上骑行，3是手环上室外跑，4是APP上室外跑，5是手环上室内跑，6是APP上室内跑
	
	private List<RunDetail> list = new ArrayList<RunDetail>();//跑步过程中详细数据
	
	private List<LatLng> latLngs = new ArrayList<LatLng>();//经纬度列表
    
RunDetail:

	private double distance;//跑步每两分钟取数据的距离
	private int time;//每两分钟取数据的时长
	private String pace;//每两分钟取数据的配速
	private double speed;//每两分钟取数据的速度
	private String longitude;//每两分钟取数据的经度
	private String latitude;//每两分钟取数据的纬度
	private long date;//每两分钟取数据的当前时间
	private int isRestart;//是否暂停后开始的第一个点，1为是，0为否
	private String macAddress;
	
LatLng:

	private int id;  //数据id
	private double lat; //纬度
	private double lng; //经度
	private Run run;  //属于哪个跑步数据
	private long date; //date
	private int isRestart; //是否为第一个点，1为是，0为否
	private String macAddress;

##**30、获取某用户某段时间的跑步数据(getRun)**

接口名称：getRun 
接口作用：获取某用户某段时间的跑步数据
接口参数：

|参数名	|类型	|说明|
| --------   | -----:  | :----:  |
|guestId|	int|	用户ID(必填)|
|startTime|	long|	开始时间(比如月初)|
|endTime|	long|	结束时间(比如月末)|
返回值：

|返回字段|	类型|	说明|
| --------   | -----:  | :----:  |
|msg|	String	|请求信息|
|status|	int	|信息编码 1 请求成功 0 请求失败|
|object|	String|	json数组(List< RunBean >)|
例如: http://demo.htimes.cn/open/getRun.action?guestId=24&startTime=1484728662&endTime=1484729339

##**31、获取跑步总数据(getRunTotal)**

接口名称：getRunTotal 
接口作用：获取跑步总数据
接口参数：

|参数名	|类型	|说明|
| --------   | -----:  | :----:  |
|guestId|	int|	用户ID(必填)|
返回值：

|返回字段|	类型|	说明|
| --------   | -----:  | :----:  |
|msg|	String	|请求信息|
|status|	int	|信息编码 1 请求成功 0 请求失败|
|count|	int|	总次数|
|distance|	double|	总距离(KM)|
|object | 	string	| json对象< RunTotal >|
例如: http://demo.htimes.cn/open/getRunTotal.action?guestId=24

RunTotal:
   /**
    * 跑步总数据
    */
	private int count;//总次数
	private double distance;//总距离

##**32、设置睡眠开始时间和结束时间（setSleepTime）**

接口名称：setSleepTime 
接口作用：设置睡眠开始时间和结束时间
接口参数：

| 参数名	| 类型	| 说明 |
| --------   | -----:  | :----:  |
|guestId	| int|	用户id(必填)|
|startTime	| long|	开始时间|
|endTime	| long|	结束时间|
返回值：
| 返回字段 |  类型 |  说明  |
| --------   | -----:  | :----:  |
| msg	| String |	请求信息|
| status| 	int	| 信息编码 1 请求成功 0 请求失败|

示例: http://demo.htimes.cn/open/setSleepTime.action?guestId=24&startTime=1484729339&endTime=1484729350

##**33、获取睡眠开始时间和结束时间（getSleepTime）**

接口名称：getSleepTime 
接口作用：获取睡眠开始时间和结束时间
接口参数：

| 参数名	| 类型	| 说明 |
| --------   | -----:  | :----:  |
|guestId	| int|	用户id(必填)|
返回值：
| 返回字段 |  类型 |  说明  |
| --------   | -----:  | :----:  |
| msg	| String |	请求信息|
| status| 	int	| 信息编码 1 请求成功 0 请求失败|
| startTime| 	long	| 睡眠开始时间|
| endTime| 	long	| 睡眠结束时间|

示例: http://demo.htimes.cn/open/setSleepTime.action?guestId=24

##**34、 更新心电数据(updateEcg)**

接口名称：updateEcg 
接口作用：更新心电数据 
接口参数：

|参数名|	类型|	说明|
| --------   | -----:  | :----:  |
|guestId|	int	|用户Id|
|messageInfo|	String|	心电数据 json数组(Ecg)|
返回值：

|返回字段|	类型|	说明|
| --------   | -----:  | :----:  |
|msg|	String|	请求信息|
|status|	int|	信息编码 1 请求成功 0 请求失败|
例如: http://demo.htimes.cn/open/updateEcg.action?guestId=1&messageInfo={}

Ecg:
  
    /**
	 * 心电值json
	 */
	private String ecgJson;
	/**
	 * 心电产生的日期 单位(秒)
	 */
	private long date;
	/**
	 * uuid
	 */
	private String uuid;
	/**
	 * 收缩压
	 */
	private int highPressure;
	/**
	 * 舒张压
	 */
	private int lowPressure;
	/**
	 * 心率最大值
	 */
	private int highHeartRate;
	/**
	 * 心率最小值
	 */
	private int lowHeartRate;
	/**
	 * 心率平均值
	 */
	private int averageHeartRate;

    private String macAddress;

messageInfo参考:

    [{"date":1484607602,  "ecgJson": [{"ecg" : 66, "date":1480046891    },    {"ecg":70, "date" : 1486507802   },    {"ecg":60,"date" : 1480047489    }], "uuid":"550E8400-E29B-11D4-A716-446655670000", "highPressure":100, "lowPressure":80,"highHeartRate":90,"lowHeartRate":60,"averageHeartRate":75}]是个数组



##**35、获取某用户测试的心电数据列表(findEcgTotal)**

接口名称：findEcgTotal 
接口作用：获取某用户测试的心电数据列表 
接口参数：

|参数名	|类型|	说明|
| --------   | -----:  | :----:  |
|guestId|	int|	用户ID|
返回值：

|返回字段|	类型|	说明|
| --------   | -----:  | :----:  |
|msg|	String|	请求信息|
|status|	int	|信息编码 1 请求成功 0 请求失败|
|object|	String|	json数组(List< Object >)|


object:

    private String uuid;//ecg数据对应的uuid
    private long date;//时间
	private int highPressure;//收缩压
	private int lowPressure;//舒张压
	private int highHeartRate;//心率最大值
	private int lowHeartRate;//心率最小值
	private int averageHeartRate;心率平均值



例如: http://demo.htimes.cn/open/findEcgTotal.action?guestId=1

##**36、获取某用户测试的心电数据明细(findEcgDetail)**

接口名称：findEcgDetail 
接口作用：获取某用户测试的心电数据明细 
接口参数：

|参数名	|类型|	说明|
| --------   | -----:  | :----:  |
|ecgId|	String|	ecg数据对应的UUID|
返回值：

|返回字段|	类型|	说明|
| --------   | -----:  | :----:  |
|msg|	String|	请求信息|
|status|	int	|信息编码 1 请求成功 0 请求失败|
|object|	String|	json对象(Ecg)|


Ecg:

    private int id;
	/**
	 * 心电值json
	 */
	private String ecgJson;
	/**
	 * 心电产生的日期 单位(秒)
	 */
	private long date;
	/**
	 * 所属用户
	 */
	private Guest guest;
	/**
	 * 创建时间
	 */
	private Date createDate = new Date(); 
	/**
	 * uuid
	 */
	private String uuid;
	/**
	 * 收缩压
	 */
	private int highPressure;
	/**
	 * 舒张压
	 */
	private int lowPressure;
	/**
	 * 心率最大值
	 */
	private int highHeartRate;
	/**
	 * 心率最小值
	 */
	private int lowHeartRate;
	/**
	 * 心率平均值
	 */
	private int averageHeartRate;
	
	private String macAddress;

ecgJson:

       [{"num" : 66, "date":1480046891    },    {"num":70, "date" : 1486507802   },    {"num":60,"date" : 1480047489    }]
   
例如: http://demo.htimes.cn/open/findEcgDetail.action?ecgId=1

##**37、获取某用户的二维码字符串(getUserQrCode)**
接口名称：getUserQrCode 
接口作用：获取某用户的二维码字符串 
接口参数：

|参数名	|类型|	说明|
| --------   | -----:  | :----:  |
|guestId|	String|	用户id|
返回值：

|返回字段|	类型|	说明|
| --------   | -----:  | :----:  |
|msg|	String|	请求信息|
|status|	int	|信息编码 1 请求成功 0 请求失败|
|object|	String|	json二维码对象|

object:

      private String qrCode;//二维码
   
   例如: http://demo.htimes.cn/open/getUserQrCode.action?guestId=1
   
##**38、设置某用户的身份id(setIdentityId)**
接口名称：setIdentityId 
接口作用：设置某用户的身份id 
接口参数：

|参数名	|类型|	说明|
| --------   | -----:  | :----:  |
|guestId|	String|	用户id|
|identityId| String|身份id|
返回值：

|返回字段|	类型|	说明|
| --------   | -----:  | :----:  |
|msg|	String|	请求信息|
|status|	int	|信息编码 1 请求成功 0 请求失败|

例如: http://demo.htimes.cn/open/setIdentityId.action?guestId=1&identityId=780

##**39、搜索好友(searchFriend)**
接口名称：searchFriend 
接口作用：搜索好友
接口参数：

|参数名	|类型|	说明|
| --------   | -----:  | :----:  |
|searchContent|	String|	搜索内容|
返回值：

|返回字段|	类型|	说明|
| --------   | -----:  | :----:  |
|msg|	String|	请求信息|
|status|	int	|信息编码 1 请求成功 0 请求失败|
|object|	String|	list对象(Guest)|

例如: http://demo.htimes.cn/open/searchFriend.action?searchContent=张三

##**40、添加好友请求(addFriend)**

接口名称：addFriend 
接口作用：添加好友请求
接口参数：

|参数名	|类型|	说明|
| --------   | -----:  | :----:  |
|guestId|	String|	发起请求的用户id|
|acceptUserId|	String|	被请求的用户id|
返回值：

|返回字段|	类型|	说明|
| --------   | -----:  | :----:  |
|msg|	String|	请求信息|
|status|	int	|信息编码 1 请求成功 0 请求失败|

例如: http://demo.htimes.cn/open/addFriend.action?guestId=1&acceptUserId=2

##**41、修改好友备注名(updateFriendRemark)**

接口名称：updateFriendRemark 
接口作用：修改好友备注名
接口参数：

|参数名	|类型|	说明|
| --------   | -----:  | :----:  |
|guestId|	String|	发起请求的用户id|
|acceptUserId|	String|	被请求的用户id(被备注的用户)|
|remark|	String|	备注名|
返回值：

|返回字段|	类型|	说明|
| --------   | -----:  | :----:  |
|msg|	String|	请求信息|
|status|	int	|信息编码 1 请求成功 0 请求失败|

例如: http://demo.htimes.cn/open/updateFriendRemark.action?guestId=1&acceptUserId=2&remark=xx

##**42、获取新好友请求(getNewRequest)**

接口名称：getNewRequest 
接口作用：获取新好友请求
接口参数：

|参数名	|类型|	说明|
| --------   | -----:  | :----:  |
|acceptUserId|	String|	被请求的用户id|

返回值：

|返回字段|	类型|	说明|
| --------   | -----:  | :----:  |
|msg|	String|	请求信息|
|status|	int	|信息编码 1 请求成功 0 请求失败|
|object|	String	|好友请求list(Friend)|

Friend:

    private int id;//好友请求记录id
	private Guest guestRequest; //发起请求的用户
	private Guest guestAccept; //被请求的用户
	private String acceptRemark; //被请求用户的备注名
	private String requestRemark; //发起请求用户的备注名
	private int tag; //请求接受状态,0是请求还未接受，1是已接受,2是拒绝
	private Date createDate = new Date();
	private int focus; //关注状态，0是只关注我，1是互相关注
	private long lastEcgDate; //最后心电更新时间

例如: http://demo.htimes.cn/open/getNewRequest.action?acceptUserId=2

##**43、接受好友请求(acceptFriend)**

接口名称：acceptFriend 
接口作用：接受好友请求
接口参数：

|参数名	|类型|	说明|
| --------   | -----:  | :----:  |
|guestId|	String|	发起请求的用户id|
|acceptUserId|	String|	被请求的用户id|

返回值：

|返回字段|	类型|	说明|
| --------   | -----:  | :----:  |
|msg|	String|	请求信息|
|status|	int	|信息编码 1 请求成功 0 请求失败|

例如: http://demo.htimes.cn/open/acceptFriend.action?guestId=1&acceptUserId=2

##**44、拒绝好友请求(refuseFriend)**

接口名称：refuseFriend 
接口作用：拒绝好友请求
接口参数：

|参数名	|类型|	说明|
| --------   | -----:  | :----:  |
|guestId|	String|	发起请求的用户id|
|acceptUserId|	String|	被请求的用户id|

返回值：

|返回字段|	类型|	说明|
| --------   | -----:  | :----:  |
|msg|	String|	请求信息|
|status|	int	|信息编码 1 请求成功 0 请求失败|

例如: http://demo.htimes.cn/open/refuseFriend.action?guestId=1&acceptUserId=2

##**45、获取被拒绝好友请求的列表(getRefuse)**

接口名称：getRefuse 
接口作用：获取被拒绝好友请求的列表
接口参数：

|参数名	|类型|	说明|
| --------   | -----:  | :----:  |
|guestId|	String|	发起请求的用户id|

返回值：

|返回字段|	类型|	说明|
| --------   | -----:  | :----:  |
|msg|	String|	请求信息|
|status|	int	|信息编码 1 请求成功 0 请求失败|
|object|	String	|好友请求list(Friend)|

例如: http://demo.htimes.cn/open/getRefuse.action?guestId=1

##**46、删除好友或者取消关注(cancelFriend)**

接口名称：cancelFriend 
接口作用：删除好友或者取消关注
接口参数：

|参数名	|类型|	说明|
| --------   | -----:  | :----:  |
|guestId|	String|	发起请求的用户id|
|acceptUserId|	String|	被请求的用户id|

返回值：

|返回字段|	类型|	说明|
| --------   | -----:  | :----:  |
|msg|	String|	请求信息|
|status|	int	|信息编码 1 请求成功 0 请求失败|

例如: http://demo.htimes.cn/open/cancelFriend.action?guestId=1&acceptUserId=2

##**47、获取我关注的好友列表(getMyFocusList)**

接口名称：getMyFocusList 
接口作用：获取我关注的好友列表
接口参数：

|参数名	|类型|	说明|
| --------   | -----:  | :----:  |
|guestId|	String|	发起请求的用户id|

返回值：

|返回字段|	类型|	说明|
| --------   | -----:  | :----:  |
|msg|	String|	请求信息|
|status|	int	|信息编码 1 请求成功 0 请求失败|
|object|	String	|好友请求list(Friend)|

例如: http://demo.htimes.cn/open/getMyFocusList.action?guestId=1

##**48、获取关注我的好友列表(getFocusMeList)**

接口名称：getFocusMeList 
接口作用：获取关注我的好友列表
接口参数：

|参数名	|类型|	说明|
| --------   | -----:  | :----:  |
|acceptUserId|	String|	被请求的用户id|

返回值：

|返回字段|	类型|	说明|
| --------   | -----:  | :----:  |
|msg|	String|	请求信息|
|status|	int	|信息编码 1 请求成功 0 请求失败|
|object|	String	|好友请求list(Friend)|

例如: http://demo.htimes.cn/open/getFocusMeList.action?acceptUserId=2

##**49、意见反馈(feedBack)**
接口名称：feedBack 
接口作用：意见反馈
接口参数：

|参数名	|类型|	说明|
| --------   | -----:  | :----:  |
|guestId|	String|	用户id(可选)|
|content|	String|	反馈内容|
|contact|	String|	联系方式|
|imgBase64str1|	String|	图片1 base64编码(可不传)|
|imgBase64str2|	String|	图片2 base64编码(可不传)|
|imgBase64str3|	String|	图片3 base64编码(可不传)|
|imgBase64str4|	String|	图片4 base64编码(可不传)|
|phoneModel|String|手机型号|
|os|String|手机系统|
|osVersion|String|系统版本|
|appVersion|String|app版本|
|hardwareInfo|String|固件版本|


返回值：

|返回字段|	类型|	说明|
| --------   | -----:  | :----:  |
|msg|	String|	请求信息|
|status|	int	|信息编码 1 请求成功 0 请求失败|

例如: http://demo.htimes.cn/open/feedBack.action?guestId=2&content=xx&contact=xx

##**50、用户与硬件版本号绑定新接口**

接口名称：bindHardwareVersionNew 
接口作用：用户与硬件版本号绑定新接口 
接口参数：

|参数名	|类型|	说明|
| --------   | -----:  | :----:  |
|guestId|	Integer	|用户ID|
|hardwareInfo|	String	|固件信息字符串|
|macAddress| String|固件mac地址(可选)|
返回值：

|返回字段|	类型|	说明|
| --------   | -----:  | :----:  |
|msg|	String	|请求信息|
|status	|int	|信息编码 1 请求成功 0 请求失败|
示例: http://demo.htimes.cn/open/bindHardwareVersionNew.action?guestId=6&hardwareInfo=xxx

##**51、软件硬件更新新接口（updateVersionNew）**

接口名称：updateVersionNew 
接口作用：软件硬件更新新接口 
接口参数：无

|参数名|	类型|	说明|
| --------   | -----:  | :----:  |
|packageName|	String|	android应用包名（非必填）|
|matchAppVersion| String|匹配APP版本号|
|os|String|手机系统版本:传android或ios|
|hardwareInfo|String|固件信息字符串|
返回值：

| 返回字段| 	类型| 	说明| 
| --------   | -----:  | :----:  |
| msg| 	String| 	请求信息| 
| status| 	int| 	信息编码 1 请求成功 0 请求失败| 
| object| 	String| 	json对象(LastVersion)| 
例如: http://demo.htimes.cn/open/updateVersionNew.action

LastVersion:

    private String appNum;  //软件版本号
    private String appName;  //软件版本名称
    private String hardwareName; //硬件版本名称
    private String appUrl;       //app版本下载地址
    private String hardwareUrl;  //硬件下载地址
    private String note;  //硬件版本备注
    private String compulsion_tag;//是否强制升级，1是，0否
    private String hardwareInfo;//固件信息字符串
    
##**52、国外天气接口（overSeaWeather）**

接口名称：overSeaWeather 
接口作用：国外天气接口
接口参数：无

|参数名|	类型|	说明|
| --------   | -----:  | :----:  |
|cityName|	String|	城市名称如new york|
返回值：

| 返回字段| 	类型| 	说明| 
| --------   | -----:  | :----:  |
| msg| 	String| 	请求信息| 
| status| 	int| 	信息编码 1 请求成功 0 请求失败| 
| object| 	String| 	json对象(weather)| 
例如: http://demo.htimes.cn/open/overSeaWeather.action

weather:

    private String text;//天气
	private int code;//天气代码
	private String temperature;//温度
	private String updateTime;//更新时间
	
##**53、带验证码注册用户**

接口名称：registUserWithCode 
接口作用：带验证码注册用户 
接口参数：

|参数名|	类型|	说明|
| --------   | -----:  | :----:  |
|userName|	String|	用户的名称 (必需)|
|password|	String|	用户密码 (必需)|
|validateCode| String | 验证码(必需)|
|nickName|	String	|用户昵称|
|flag|	Integer|	0 安卓 1 苹果|
|sex|	Integer|	0 男 1 女|
|birthDate|	String|	出生日期|
|weight	|Float|	体重 kg|
|height|	Float|	身高 cm|
|base64Str|	String|	头像base64字符串|
返回值：

|返回字段|	类型|	说明|
| --------   | -----:  | :----:  |
|msg|	String|	请求信息|
|status|	int	|信息编码 1 请求成功 0 请求失败|
|object|	String|	json对象< Guest >|
示例: http://demo.htimes.cn/open/registUserWithCode.action?userName=657044849@qq.com&password=123&validateCode=123

##**54、找回密码发送验证码**

接口名称：findPwdCode 
接口作用：找回密码发送验证码 
接口参数：

|参数名	|类型|	说明|
| --------   | -----:  | :----:  |
|phoneNum|	String|	电话号码|
返回值：

|返回字段	|类型|	说明|
| --------   | -----:  | :----:  |
|msg|	String|	请求信息|
|status	|int|	信息编码 1 请求成功 0 请求失败|
例如: http://demo.htimes.cn/open/findPwdCode.action?phoneNum=123