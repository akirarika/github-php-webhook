```php

<?php

$secret = '5ce243d12b674100019726f5c15337b7';

$signature = "sha1=" . hash_hmac('sha1', file_get_contents("php://input"),  $secret);

if (strcmp($signature, $_SERVER['HTTP_X_HUB_SIGNATURE']) != 0) return http_response_code(404);

exec("bash " . __DIR__ . "/hook.sh ", $shell);

foreach($shell as $line) {
    echo $line . "\n";
}
```
