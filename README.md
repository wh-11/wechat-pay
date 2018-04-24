# wechat-pay
这里说的是微信公众号支付，主要是微信里面的多域名调用一个支付的问题
* 主要手段是通过一个跳转的中间页进行支付，中间页是在微信后台配置的正确的页面，但是这样存在一个问题就是，支付的时候需要跳转一个页面进行支付，这个暂时没有避免，可以优化体验，
* 当点击支付按钮的时候，调用自己的下单接口，拿到对应的金额跟订单号，进行拼接支付url，跳转支付


    var openid ='';
    var total_fee = 1; 
    var out_trade_no = '';
    var back_url = encodeURIComponent('http://baidu.com');
    var url = 'http://wxpay.com/example/jsapi.php?openid='+openid+'&total_fee='+total_fee+'&out_trade_no='+out_trade_no+'&back_url='+back_url;
	window.location.replace(url);
	
	
	
	
### 在支付页面的配置
* 获取传递过来的金额，价格，openid，紧接着就调用`callpay()` 进行支付，支付完成之后跳转回 `back_url`，用户中间就只有一个等待页面加载的操作，不会有别的差异


### 注
* 这里尽量用 `window.location.replace` 进行页面跳转，这样的话，用户返回，或者左滑右滑之类的操作不会进入到支付页面
* 如果登陆的微信平台跟支付的微信平台用的openid不一致的话，只能通过两次微信登陆，获取两个openid，


### 泛解析的项目在微信开发过程中问题
* 关于登陆，目前是通过跳转中间页面拿取code值的方式
* 关于微信分享，在微信后台设置主域名就可以保证所有的都可以正常分享
* 关于设置安全可信任的域名，设置主域名
