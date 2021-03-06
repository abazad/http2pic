# http2pic

## Introduction
http2pic is an Open Source website renderer. It uses the [wkhtmltox](https://github.com/wkhtmltopdf/wkhtmltopdf) to render websites with various options.

Live demo on https://http2pic.haschek.at/

## Dependencies
- [wkhtmltox](http://wkhtmltopdf.org/downloads.html)
- curl extension for PHP ```apt-get install php5-curl```
- Make sure the server has the "timeout" command ```apt-get install coreutils```

## Install
- Download [this repo](https://github.com/chrisiaut/http2pic/archive/master.zip) and extract it somewhere on your webserver

### With WKHTMLToImage
- Install [wkhtmltox](http://wkhtmltopdf.org/downloads.html) on your server
- Make /usr/sbin/wkhtmltoimage executable for the user that runs the webserver. For Apache it's the ```www-data``` user. Or use sudo

### With PhantomJS
- Install PhantomJS. eg via ```npm install -g phantomjs```
- Make /usr/bin/phantomjs executable for the user that runs the webserver. For Apache it's the ```www-data``` user. Or use sudo


## Upgrade

Whenever you come to this page you can just [download](https://github.com/chrisiaut/http2pic/archive/master.zip) the repo again and overwrite the existing files. Should work out of the box

## Usage

After you extracted the contents of this repo to your webserver and can access the page and it will tell you how to use the API.

But it's as simple as:

```
https://your-url-and.path/api.php?[OPTIONS]&url=[WEBSITE_URL]
```

The requested page will render as image (not provide a link). So you can use the path to your api.php file like so:

```html
<img src="https://your-url-and.path/api.php?url=http://xkcd.com" title="screenshot of xkcd.com" />
```

### Example php script to proxy an image to the local server

```php
<?php
    $targeturl = 'http://www.xkcd.com';
    $url = 'https://http2pic.haschek.at/api.php?url='.rawurlencode($targeturl);
	    
    $ch = curl_init($url);
    $fp = fopen('xkcd.jpg', 'wb');
    curl_setopt($ch, CURLOPT_FILE, $fp);
    curl_setopt($ch, CURLOPT_HEADER, 0);
    curl_exec($ch);
    curl_close($ch);
    fclose($fp);
?>
```

---

This is a [HASCHEK SOLUTIONS](https://haschek.solutions) project

[![HS logo](https://http2pic.haschek.at/img/hs_logo.png)](https://haschek.solutions)