```php

<?php

// Github Webhook 中你填写的 Secret
$secret = '5ce243d12b674100019726f5c15337b7';

$signature = "sha1=" . hash_hmac('sha1', file_get_contents("php://input"),  $secret);

// 断言 Secret 若验证失败，则响应 404 结束运行
if (strcmp($signature, $_SERVER['HTTP_X_HUB_SIGNATURE']) != 0) return http_response_code(404);

// 此下面编写你的 Github Webhook 验证成功的罗辑..

// ..

// 如执行一个 bash 脚本..
exec("bash " . __DIR__ . "/hook.sh ", $shell);

// 在执行完毕后，将结果打印出来
foreach($shell as $line) {
    echo $line . "\n";
}
```
