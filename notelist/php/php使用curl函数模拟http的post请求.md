## php使用curl函数模拟http的post请求

```php
<?php

$data='mobile=18612244109&timestamp=1471414353000';

$ch = curl_init();
curl_setopt($ch, CURLOPT_DNS_USE_GLOBAL_CACHE, false);
curl_setopt($ch, CURLOPT_HTTPHEADER, array("Content-Type:application/x-www-form-urlencoded", "User-Agent:Moziral"));
curl_setopt($ch,CURLOPT_URL,"http://www.baidu.com");
curl_setopt($ch, CURLOPT_POST, 1);
curl_setopt($ch, CURLOPT_POSTFIELDS, $data);

$server_output = curl_exec ($ch);
curl_close ($ch);

echo "result is:".$server_output;

?>
```
