
# 语音回拨
用户应用调用该接口后，云呼你平台首先向第一个被叫方发起呼叫；
在第一方接听后，向二方放发起呼叫；第二方接听后，双方通话。


##下载Demo&SDK
[下载]

##Demo示例

###接口调用示例
{% codetabs name="Java", type="jsp" -%}

msg = "Hello World"
print msg

{%- language name="php", type="php" -%}
//引入sdk文件
include_once("../YunhuniSapiSdk/SapiSdk.php");
//应用标识
$appId = "8af4caa057750727015779672ffb004a";
//鉴权账号
$certId = "c1d2597d7d8ba80a4808d383d0b554f7";
//接口API
$apiUrl = "http://api.yunhuni.com/v1/account/c1d2597d7d8ba80a4808d383d0b554f7/";
//密钥
$secreKey = "03024da1808062cb290d83440ba541bc";
    
/**
 * 双向回拨
 * @param from1 第一方主叫号码 选填 如有绑定IVR号码，可填绑定号码,否则为空
 * @param to1 第一方被叫号码 必填 （手机号码前面加0）
 * @param from2 第二方主叫号码 选填 如有绑定IVR号码，可填绑定号码,否则为空
 * @param to2 第二方被叫号码 必填 （手机号码前面加0）
 * @param ring_tone 自定义回铃音 选填
 * @param ring_tone_mode 自定义回铃音播放模式 0：收到对端回铃后开始播放 1：拨号时即开始播放，收到对端回铃后停止播放 2：拨号时即开始播放，对端接听或者挂机后停止播放 选填
 * @param max_dial_duration 最大拨号等待时间（秒） 选填
 * @param max_call_duration 最大接通时间（秒） 选填
 * @param recording 是否录音 选填
 * @param record_mode 录音模式： 0: 双向接通后录音 1：开始呼叫第一方时启动录音 2: 开始呼叫第二方时启动录音 选填
 * @param userData 用户数据 选填
 * @return
 */
function duoCallback($from1, $to1, $from2, $to2, $ring_tone, $ring_tone_mode, $max_dial_duration, $max_call_duration, $recording, $record_mode, $user_data)
{
    global $appId, $certId, $apiUrl, $secreKey;
    $api = new SapiSdk($appId, $certId, $apiUrl, $secreKey);
    $result = $api->duoCallback($from1, $to1, $from2, $to2, $ring_tone, $ring_tone_mode, $max_dial_duration, $max_call_duration, $recording, $record_mode, $user_data);
    $res = json_decode($result, true);
    if ($res['code'] == '000000') {
        //TODO 添加成功处理逻辑
        echo "callback success!<br>";
    } else {
        //TODO 添加错误处理逻辑
        echo "callback fail!<br>";
    }
}
//duoCallback('第一方主叫号码','第一方被叫号码','第二方主叫号码','第二方被叫号码','自定义回铃音','自定义回铃音播放模式','最大拨号等待时间（秒）','最大接通时间（秒）','是否录音','录音模式','用户数据');
//Demo调用,参数填入正确后，放开注释可以调用
duoCallback(null, '第一方被叫号码', null, '第二方主叫号码', null, 0, 30, 3600, 0, 0, '用户数据');
{%- endcodetabs %}

##事件回调
{% codetabs name="Java", type="jsp" -%}

{%- language name="php", type="php" -%}
    //接收流数据
    $streamData = isset($GLOBALS['HTTP_RAW_POST_DATA']) ? $GLOBALS['HTTP_RAW_POST_DATA'] : '';
    if (empty($streamData)) {
        $streamData = file_get_contents('php://input');
    }
    file_put_contents('text.log',$streamData)
    
{%- endcodetabs %}

[更多详情](http://yunhuni.com/)