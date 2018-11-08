# CurlRequest
<p dir="rtl">
کلاس ساده برای صدا زدن api در زبان php ( لطفا برای اطلاعات بیشتر به http://php.net/curl مراجعه کنید)


## نصب

بر روی `download` کلیک کنید یا با نوشتن این دستور در ترمینال `git clone git://github.com/shuber/curl.git` کد را به پروژه خودتان اضافه کنید.


## استفاده

### مداردهی اولیه

به سادگی کلاس  `Curl` را به کدتان اضافه کنید و آبجکت جدیدی از آن بسازید. مانند نمونه:
</p>
	require_once 'curl.php';
	$curl = new Curl;

<p dir="rtl">
### انجام یک درخواست

آبجکت Curl از 5 نوع درخواست پشتیبانی می کند: HEAD، GET، POST، PUT و DELETE.
شما باید یک آدرس url برای درخواست و به صورت اختیاری یک آرایه یا رشته ای از متغیرها برای ارسال همراه با آن مشخص کنید.

	# آبجکت Curl، آرایه ای از vars را به url به عنوان یک رشته اضافه می کند
</p>
	$response = $curl->head($url, $vars = array());   # initilize head request
	$response = $curl->get($url, $vars = array());    # initilize get request
	$response = $curl->post($url, $vars = array());   # initilize post request
	$response = $curl->put($url, $vars = array());    # initilize put request
	$response = $curl->delete($url, $vars = array()); # initilize delete request
<p dir="rtl">
برای ارسال درخواست سفارشی میتوانید از متد `request` استفاده کنید:
</p>
	$response = $curl->request('YOUR_CUSTOM_REQUEST_TYPE', $url, $vars = array());
<p dir="rtl">
تمام متدهای درخواست ساخته شده مانند `put` و` get` به سادگی متد `request` را پوشش میدهند. به عنوان مثال، روش `post` به صورت زیر اجرا می شود:
</p>
	function post($url, $vars = array()) {
	    return $this->request('POST', $url, $vars);
	}
<p dir="rtl">
مثال:
</p>
	$response = $curl->get('domain.com?q=somedata');

	# The Curl object will append '&some_variable=some_value' to the url
	$response = $curl->get('google.com?q=test', array('some_variable' => 'some_value'));
	
	$response = $curl->post('test.com/posts', array('title' => 'sometitle', 'body' => 'something as body'));
<p dir="rtl">
تمام درخواستها آبجکت CurlResponse را به عنوان خروجی ذخیره میکنند:


###  پاسخ درخواست CurlResponse 


یک درخواست عادی CURL هدر و بادی را در یک رشته پاسخ باز می گرداند. این کلاس این دو را تجزیه می کند و آنها را به خواص جداگانه تبدیل می کند.

برای مثال:
</p>
	$response = $curl->get('google.com');
	echo $response;  or   # هر دو مورد جواب میدهند
	echo $response->body; # A string containing everything in the response will echo, except for the headers
	print_r($response->headers); # An associative array containing the response headers
<p dir="rtl">
	مثال:	
</p>
	Array
	(
	    [Http-Version] => 1.0
	    [Status-Code] => 200
	    [Status] => 200 OK
	    [Cache-Control] => private
	    [Content-Type] => text/html; charset=ISO-8859-1
	    [Date] => Wed, 07 May 2008 21:43:48 GMT
	    [Server] => gws
	    [Connection] => close
	)
<p dir="rtl">
### کوکی Sessions

به صورت پیش فرض، کوکی ها در یک فایل به نام `lib / curl_cookie.txt` ذخیره می شوند. شما می توانید نام این فایل را از طریق تنظیم این متغیر تغییر دهید:
</p>
	$curl->cookie_file = 'some_other_filename';
<p dir="rtl">
این به شما اجازه می دهد یک session را در طول درخواست ها حفظ کنید.

### تنظیمات اولیه پیکربندی


شما می توانید به راحتی referer یا user-agent را تنظیم کنید:
</p>
	$curl->referer = 'https://google.com';
	$curl->user_agent = 'some user agent string';

<p dir="rtl">
### تنظیم  هدر های سفارشی

شما حتی می توانید این هدر ها را به صورت دستی تنظیم کنید:
</p>
	$curl->headers['Host'] = 12.345.678.90;
	$curl->headers['Some-Custom-Header'] = 'Some Custom Value';

<p dir="rtl">
### تنظیم گزینه های سفارشی برای ارسال درخواست CURL

به طور پیش فرض، آبجکت `Curl` از تغییر مسیر پیروی می کند. شما می توانید به صورت زیر غیر فعال کنید:
</p>
	$curl->follow_redirects = false;
<p dir="rtl">
شما می توانید بسیاری از گزینه های مختلف برای ارسال درخواست های CURL را تنظیم کنید یا آنها را لغو کنید (برای مشاهده لیست آنها به [curl_setopt documentation] (http://php.net/curl_setopt) مراجعه کنید)

	# همه ی موارد زیر میتوانند مورد استفاده قرار بگیرند.
</p>
	$curl->options['AUTOREFERER'] = true;
	$curl->options['autoreferer'] = true;
	$curl->options['CURLOPT_AUTOREFERER'] = true;
	$curl->options['curlopt_autoreferer'] = true;
<p dir="rtl">
## تماس

شما میتوانید از طریق ایمیل روبرو با من در تماس باشید: [mehrdadashtari.ma@gmail.com](mailto:mehrdadashtari.ma@gmail.com)

</p>
