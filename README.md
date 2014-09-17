# updown.bz - Open API

This project is the API documentation of the updown.bz API. It'll show you available API calls and examples for different programing languages. If you like, commit your example codes, other changes or link in updown.bz related projects. The updown.bz APi includes everything you need to work with your files, upload, download, account, ... .
 
## Basics
The API is based on [JSON](http://en.wikipedia.org/wiki/JSON)-objects, which will be transfered with [HTTP-POST](http://en.wikipedia.org/wiki/POST_(HTTP), thus you'll need to set the _Content-Type_ to _application/json; charset=utf-8_. Because all our connections are secured via [SSL](http://en.wikipedia.org/wiki/Transport_Layer_Security) only use  [HTTPS](http://en.wikipedia.org/wiki/HTTP_Secure)-connections. Post all JSON-objects to _https://api.updown.bz_.

Each transmitted JSON object consists of a minimum of two properties _m (module)_ and _a (action)_. Optional properties are _i (request id)_, _d (data)_, _s (session token)_. The _request id_ could be any string or number, which you can use to keep track of all your requests. The API is just passing it through. _data_ will be used to append specified payload for the particular API call. If you use authenticated API calls, set the _session token_ property, which you got from a login API call (see below).

The easiest API call is the link checker call. Set the _data_-property _id_ to an array of updown.bz id's and it'll delivers you the file status. The JSON-object to transmit would be this:
```json
{
    "m": "chk",
    "a": "chkr",
    "d": {
        id: [
            "6qnfmXuiGt",
            "scUgCG3oQf",
            "Fxhb9KbLRF"
        ]
    }
}
```

For a quick test, use the following [PHP]() code, which uses [PHP-cURL](http://php.net/manual/en/book.curl.php) to transmit the JSON-object from above:

```php
<?php
// http://php.net/manual/en/book.curl.php

$api_url = 'https://api.updown.bz';
$user_agent = 'Mozilla/5.0 (X11; Linux x86_64; rv:28.0) Gecko/20100101 Firefox/28.0';
$query_id = rand(1024, 1024 * 1024 * 1024);

$query = array(
    'i' => $query_id,
    'm' => 'chkr',
    'a' => 'chk',
    'd' => array(
        'id' => array(
            '6qnfmXuiGt',
            'scUgCG3oQf',
            'Fxhb9KbLRF'
        )
    )
);

$json = json_encode($query);

$ch = curl_init();
curl_setopt($ch, CURLOPT_URL, $api_url);
curl_setopt($ch, CURLOPT_RETURNTRANSFER, 1);
curl_setopt($ch, CURLOPT_HTTPHEADER, array(
        'Content-Type: application/json; charset=UTF-8',
        'User-Agent: '.$user_agent
    ));
curl_setopt($ch, CURLOPT_POST, 1);
curl_setopt($ch, CURLOPT_POSTFIELDS, $json);
$result = curl_exec($ch);

var_dump($result);
```

That request leads to the following JSON-object, which all the file data you need:
```json
{
    "c": 1,
    "d": [{
        "id": "6qnfmXuiGt",
        "name": "image_one.jpg",
        "online": true,
        "size": 54286,
        "protected": false,
        "premium": false,
        "md5": "85316d1cd4b6da12d9a99c70ce0e9a53"
    }, {
        "id": "Fxhb9KbLRF",
        "name": "image_three.jpg",
        "online": true,
        "size": 113088,
        "protected": false,
        "premium": false,
        "md5": "0265213a0a9bbbe272d99b5dafb08c80"
    }, {
        "id": "scUgCG3oQf",
        "name": "image_two.jpg",
        "online": true,
        "size": 58901,
        "protected": false,
        "premium": false,
        "md5": "6bb3e62d21666c970deb924996119754"
    }],
    "t": 1410959460,
    "i": 956361669
}
```

> TODO: explain response

## Calls
write me

## Examples
write me

## Links
+ Login | Bash -> [My Gist](https://gist.github.com/elmoyak/fc88558bd4d18632bad0)
+ Login | PHP -> [My Gist](https://gist.github.com/elmoyak/cbd6973b4f27700fff00)
+ Login/Download | Java -> [jDownloader plugin](https://github.com/svn2github/jdownloader/blob/9e70773ac2d4b44ec7f93e41d97a6376d0c71c26/src/jd/plugins/hoster/UpDownBz.java)
+ Upload | Java -> [NeembuuUploader plugin](http://sourceforge.net/p/neembuuuploader/code/HEAD/tree/NeembuuUploader/src/neembuuuploader/uploaders/UpdownBz.java)
