## 相关代码
```php
protected function request($method, $data)
{
    
    $cacert = __DIR__ . '/cacert.pem';
    $data = json_encode($data);
    $url = 'https://shdrqaapi.shanghaidisneyresort.com.cn/' . $method;
    $ssl = substr($url, 0, 8) == "https://" ? TRUE : FALSE;
    $ch = curl_init();
    curl_setopt($ch, CURLOPT_URL, $url);
    curl_setopt($ch, CURLOPT_RETURNTRANSFER, 1);
    curl_setopt($ch, CURLOPT_IPRESOLVE, CURL_IPRESOLVE_V4);
    curl_setopt($ch, CURLOPT_POST, 1);
    curl_setopt($ch, CURLOPT_TIMEOUT, 10);
    curl_setopt($ch, CURLOPT_POSTFIELDS, $data);
    //curl_setopt($ch, CURLOPT_HEADER, 1);
    if ($ssl) {
        curl_setopt($ch, CURLOPT_SSL_VERIFYPEER, true);   // 只信任CA颁布的证书  
        curl_setopt($ch, CURLOPT_CAINFO, $cacert); // CA根证书（用来验证的网站证书是否是CA颁布）  
        curl_setopt($ch, CURLOPT_SSL_VERIFYHOST, 0); // 检查证书中是否设置域名，并且是否与提供的主机名匹配  
    }
    
    $result = curl_exec($ch);
    curl_close($ch);
    return $result;
}
```
## 获取相关CA证书
```txt
从 http://curl.haxx.se/ca/cacert.pem 获取CA证书
```