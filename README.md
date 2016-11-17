## wechat-jssdk-signature

微信JSSDK服务端生成签名认证，包含后端PHP与前端JS的实现，后端缓存access_token、jsapi_ticket。

### 配置开发者ID

打开 config.php 修改 CONF_APP_ID 与 CONF_APP_SECRET，不知道填什么？去你的公众平台去找吧！

```php
// 微信开发者ID
define('CONF_APP_ID', '****************');
define('CONF_APP_SECRET', '********************************');
```

打开 jssdk-config.js 修改 appId


```javascript
// 用户配置
var appId = '****************';
```

### 使用范例 

打开 jssdk_example.html 里面有一个定位的范例

### 范例讲解

范例里有引用3个js文件：
1. 第一个是jquery，如果你的项目有引用，可以去掉
2. 微信的jssdk的库，不能动
3. 我写好的jssdk配置文件，这样你就不需要每个页面去配置了

```javascript
<script type="text/javascript" src="http://lib.sinaapp.com/js/jquery/1.9.1/jquery-1.9.1.min.js"></script>
<script type="text/javascript" src="http://res.wx.qq.com/open/js/jweixin-1.0.0.js"></script>
<script type="text/javascript" src="/jssdk-config.js"></script>
```

接下来就是直接执行微信的js接口了，是不是很简单很方便

```javascript
<script type="text/javascript">

    // 配置成功后执行
    wx.ready(function(){

        // 获取地理位置
        wx.getLocation({
            type: 'wgs84',
            success: function (res) {
                console.log(res);
                var latitude = res.latitude;
                var longitude = res.longitude;
                var speed = res.speed;
                var accuracy = res.accuracy;
                alert("latitude:" + latitude + " / latitude:" + longitude);
            }
        });

    });

</script>
```

### 注意安全

因为 access_token、jsapi_ticket 做的是文件缓存，存放在 Cache 目录里，所以不要让别人知道你的url了，不然别人可以直接下载，我还是建议大家存到redis,memcache里去，修改下Core目录的Cache类就可以了，很简单的。