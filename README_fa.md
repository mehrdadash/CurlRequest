# CurlRequest
<div dir="rtl">
کلاس ساده برای صدا زدن api در زبان php ( لطفا برای اطلاعات بیشتر به http://php.net/curl مراجعه کنید)


## نصب

Click the `download` link above or `git clone git://github.com/shuber/curl.git`
</div>

## Usage

### Initialization

Simply require and initialize the `Curl` class like so:

	require_once 'curl.php';
	$curl = new Curl;


### Performing a Request

The Curl object supports 5 types of requests: HEAD, GET, POST, PUT, and DELETE.
You must specify a url to request and optionally specify an associative array or string of variables to send along with it.

	# The Curl object will append the array of $vars to the $url as a query string

	$response = $curl->head($url, $vars = array());   # initilize head request
	$response = $curl->get($url, $vars = array());    # initilize get request
	$response = $curl->post($url, $vars = array());   # initilize post request
	$response = $curl->put($url, $vars = array());    # initilize put request
	$response = $curl->delete($url, $vars = array()); # initilize delete request
	
To use a custom request methods, you can call the `request` method:

	$response = $curl->request('YOUR_CUSTOM_REQUEST_TYPE', $url, $vars = array());

All of the built in request methods like `put` and `get` simply wrap the `request` method. For example, the `post` method is implemented like:

	function post($url, $vars = array()) {
	    return $this->request('POST', $url, $vars);
	}

Examples:

	$response = $curl->get('domain.com?q=somedata');

	# The Curl object will append '&some_variable=some_value' to the url
	$response = $curl->get('google.com?q=test', array('some_variable' => 'some_value'));
	
	$response = $curl->post('test.com/posts', array('title' => 'sometitle', 'body' => 'something as body'));

All requests return a CurlResponse object (see below) or false if an error occurred. You can access the error string with the `$curl->error()` method.


### The CurlResponse Object

A normal CURL request will return the headers and the body in one response string. This class parses the two and places them into separate properties.

For example

	$response = $curl->get('google.com');
	echo $response;  or   # both will work
	echo $response->body; # A string containing everything in the response will echo, except for the headers
	print_r($response->headers); # An associative array containing the response headers

	example:	

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

### Cookie Sessions

By default, cookies will be stored in a file called `lib/curl_cookie.txt`. You can change this file's name by setting it like this

	$curl->cookie_file = 'some_other_filename';

This allows you to maintain a session across requests


### Basic Configuration Options

You can easily set the referer or user-agent

	$curl->referer = 'https://google.com';
	$curl->user_agent = 'some user agent string';

You can even set these headers manually :


### Setting Custom Headers

You can set custom headers to send with the request

	$curl->headers['Host'] = 12.345.678.90;
	$curl->headers['Some-Custom-Header'] = 'Some Custom Value';


### Setting Custom CURL request options

By default, the `Curl` object will follow redirects. You can disable this by setting:

	$curl->follow_redirects = false;

You can set or override many different options for CURL requests (see the [curl_setopt documentation](http://php.net/curl_setopt) for a list of them)

	# any of these will work
	$curl->options['AUTOREFERER'] = true;
	$curl->options['autoreferer'] = true;
	$curl->options['CURLOPT_AUTOREFERER'] = true;
	$curl->options['curlopt_autoreferer'] = true;

## Contact

keep in touch with me: [mehrdadashtari.ma@gmail.com](mailto:mehrdadashtari.ma@gmail.com)
