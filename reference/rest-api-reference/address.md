---
description: Metacoin Address and balance
---

# Address

{% swagger src="../../.gitbook/assets/api.yaml" path="/address" method="post" %}
[api.yaml](../../.gitbook/assets/api.yaml)
{% endswagger %}

```php
<?php
// Create New Address example code


// Create new key pair
$new_key_pair = openssl_pkey_new(array(
    "private_key_type" => OPENSSL_KEYTYPE_EC,
    'curve_name' => 'secp384r1',
));
openssl_pkey_export($new_key_pair, $private_key_pem);
$details = openssl_pkey_get_details($new_key_pair);
$public_key_pem = $details['key'];

$param = array(
	'publickey' => $public_key_pem,
	'addinfo' => 'new address'
);

// HTTP Request
$curl = curl_init();
$opt = curl_setopt_array($curl, array(
	CURLOPT_URL => 'https://testnetrest.metacoin.network:20923/address',
	CURLOPT_RETURNTRANSFER => true,
	CURLOPT_CONNECTTIMEOUT => 5,
	CURLOPT_TIMEOUT => 20,
	CURLOPT_SSL_VERIFYPEER => false,
	CURLOPT_SSL_VERIFYHOST => false,
	CURLOPT_POST => false,
	CURLOPT_POSTFIELDS => http_build_query($param),
	CURLOPT_POST => true,
));
curl_setopt($curl, CURLOPT_HTTPHEADER, array('Content-Type: application/x-www-form-urlencoded'));

$body = curl_exec($curl);
if(curl_errno($curl)){
	$http_code = curl_getinfo($curl, CURLINFO_HTTP_CODE);
	printf("API Error [%d] %s", $http_code, $body);
	exit;
}

printf("New Address : %s\n", $body);
printf("Private Key : %s\n", $private_key_pem);
```

{% swagger src="../../.gitbook/assets/api.yaml" path="/address/{address}" method="get" %}
[api.yaml](../../.gitbook/assets/api.yaml)
{% endswagger %}

{% swagger src="../../.gitbook/assets/api.yaml" path="/address/bykey" method="post" %}
[api.yaml](../../.gitbook/assets/api.yaml)
{% endswagger %}

{% swagger src="../../.gitbook/assets/api.yaml" path="/nonce/{address}" method="get" %}
[api.yaml](../../.gitbook/assets/api.yaml)
{% endswagger %}

{% swagger src="../../.gitbook/assets/api.yaml" path="/balance/{address}" method="get" %}
[api.yaml](../../.gitbook/assets/api.yaml)
{% endswagger %}
