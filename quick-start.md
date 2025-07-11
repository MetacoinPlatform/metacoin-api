# Quick Start

{% hint style="info" %}
**Good to know:** A quick start guide can be good to help folks get up and running with your API in a few steps. Some people prefer diving in with the basics rather than meticulously reading every page of documentation!
{% endhint %}

## Create address

{% tabs %}
{% tab title="Node" %}
{% code overflow="wrap" lineNumbers="true" %}
```javascript
const crypto = require('crypto');
const axios = require('axios');

// testnet
var hostname = "https://testnetrest.metacoin.network:20923";
// mainnet
// hostname = "https://rest.metacoin.network:20923";

var public_key = "-----BEGIN PUBLIC KEY-----\nMIGbMBAGByqGSM49AgEGBSuBBAAjA4GGAAQBBp5oHHFaATF1UIephJYgtW+u2+aT\nhZLxNgn5JZhgFXzvTUHlThZxb61eTXMMjyU/IloNznwtzRWuPq1oMDOMq9oBbT/t\nE4lgyPF5/QtzuhaaYRpr/ahZ4JSLyHOegkopXeic3UFUmkpb4mXuSGgu5mChuuUC\nktjfluGNtvXHOWYtqTU=\n-----END PUBLIC KEY-----";
// public_key = "MIGbMBAGByqGSM49AgEGBSuBBAAjA4GGAAQBBp5oHHFaATF1UIephJYgtW+u2+aThZLxNgn5JZhgFXzvTUHlThZxb61eTXMMjyU/IloNznwtzRWuPq1oMDOMq9oBbT/tE4lgyPF5/QtzuhaaYRpr/ahZ4JSLyHOegkopXeic3UFUmkpb4mXuSGgu5mChuuUCktjfluGNtvXHOWYtqTU=";

axios.post(hostname + '/address/bykey', {
    'publickey': public_key
}, {
    proxy: {
    host: '127.0.0.1',
    port: 8888
    }
})
    .then(function (response) {
    if (response.status != 200) {
        return Promise.reject("Metacoin server response error");
    } else {
        return Promise.resolve(response.data);
    }
    })
    .then(function (mtc_address) {
    // ["MT4FzIQCgRh0T1YD841OxjNd3dkfTJcEd41d17d3"]
    console.log(mtc_address);
    })
    .catch(function (error) {
    if (error.response.status == 404) {
        console.log("Address not found");
    } else {
        console.log(error);
    }
    });
```
{% endcode %}
{% endtab %}

{% tab title="PHP" %}
{% code overflow="wrap" lineNumbers="true" %}
```php
<?
// testnet
define('MTC_HOST', 'https://testnetrest.metacoin.network:20923');
// mainnet
// define('MTC_HOST', 'https://rest.metacoin.network:20923');
function mtc_post($uri, $param){
    $curl = curl_init();
    $opt = curl_setopt_array($curl, array(
        CURLOPT_URL => MTC_HOST . $uri,
        CURLOPT_RETURNTRANSFER => true,
        CURLOPT_CONNECTTIMEOUT => 5,
        CURLOPT_TIMEOUT => 20,
        CURLOPT_SSL_VERIFYPEER => false,
        CURLOPT_SSL_VERIFYHOST => false,
        CURLOPT_POSTFIELDS => http_build_query($param),
        CURLOPT_POST => true,
        CURLOPT_HTTPHEADER => array('Content-Type: application/x-www-form-urlencoded')
    ));
    $body = curl_exec($curl);

    $http_code = curl_getinfo($curl, CURLINFO_HTTP_CODE);
    $err_msg = '';
    $err_code = curl_errno($curl);
    if ($err_code) {
        $err_msg = curl_error($curl);
    }

    printf("Response Http Code: %s, msg: %s\n", $http_code, $body);
    if ($err_code) {
        printf("Response CurlCode: %s, msg: %s\n", $err_code, $body);
    }

    curl_close($curl);
    $curl = null;

    return $body;
}

$param = array(
    'publickey' => "-----BEGIN PUBLIC KEY-----\nMIGbMBAGByqGSM49AgEGBSuBBAAjA4GGAAQBBp5oHHFaATF1UIephJYgtW+u2+aT\nhZLxNgn5JZhgFXzvTUHlThZxb61eTXMMjyU/IloNznwtzRWuPq1oMDOMq9oBbT/t\nE4lgyPF5/QtzuhaaYRpr/ahZ4JSLyHOegkopXeic3UFUmkpb4mXuSGgu5mChuuUC\nktjfluGNtvXHOWYtqTU=\n-----END PUBLIC KEY-----");

$body = mtc_post('/address/bykey', $param);
printf("Address list : %s\n", $body);
```
{% endcode %}
{% endtab %}
{% endtabs %}

{% hint style="info" %}
**Good to know:** Using tabs to separate out different languages is a great way to present technical examples or code documentation without cramming your docs with extra sections or pages per language.
{% endhint %}

## Make your first request

To make your first request, send an token transfer

{% openapi src=".gitbook/assets/api.yaml" path="/transfer" method="post" %}
[api.yaml](.gitbook/assets/api.yaml)
{% endopenapi %}

{% tabs %}
{% tab title="PHP" %}
{% code overflow="wrap" lineNumbers="true" %}
```php
define('MTC_HOST', 'https://testnetrest.metacoin.network:20923');
// mainnet
// define('MTC_HOST', 'https://rest.metacoin.network:20923');


function mtc_get($uri){
    $curl = curl_init();
    $opt = curl_setopt_array($curl, array(
        CURLOPT_URL => MTC_HOST . $uri,
        CURLOPT_RETURNTRANSFER => true,
        CURLOPT_CONNECTTIMEOUT => 5,
        CURLOPT_TIMEOUT => 20,
        CURLOPT_SSL_VERIFYPEER => false,
        CURLOPT_SSL_VERIFYHOST => false,
        CURLOPT_POST => false,
        CURLOPT_CUSTOMREQUEST => 'GET',
    ));

    $body = curl_exec($curl);

    $http_code = curl_getinfo($curl, CURLINFO_HTTP_CODE);
    $err_msg = '';
    $err_code = curl_errno($curl);
    if ($err_code) {
        $err_msg = curl_error($curl);
    }

    printf("Response Http Code: %s, msg: %s\n", $http_code, $body);
    if ($err_code) {
        printf("Response CurlCode: %s, msg: %s\n", $err_code, $body);
    }

    curl_close($curl);
    $curl = null;

    return $body;
}

function mtc_post($uri, $param){
    $curl = curl_init();
    $opt = curl_setopt_array($curl, array(
        CURLOPT_URL => MTC_HOST . $uri,
        CURLOPT_RETURNTRANSFER => true,
        CURLOPT_CONNECTTIMEOUT => 5,
        CURLOPT_TIMEOUT => 20,
        CURLOPT_SSL_VERIFYPEER => false,
        CURLOPT_SSL_VERIFYHOST => false,
        CURLOPT_POSTFIELDS => http_build_query($param),
        CURLOPT_POST => true,
        CURLOPT_HTTPHEADER => array('Content-Type: application/x-www-form-urlencoded')
    ));
    $body = curl_exec($curl);

    $http_code = curl_getinfo($curl, CURLINFO_HTTP_CODE);
    $err_msg = '';
    $err_code = curl_errno($curl);
    if ($err_code) {
        $err_msg = curl_error($curl);
    }

    printf("Response Http Code: %s, msg: %s\n", $http_code, $body);
    if ($err_code) {
        printf("Response CurlCode: %s, msg: %s\n", $err_code, $body);
    }

    curl_close($curl);
    $curl = null;

    return $body;
}

// sender address
$from_addr = "MTW95PhgJaQCc7L4K9I9GrU94d2zSd8DLjkrQ2b5";

// example private key. this key is not working
$from_private_key = "-----BEGIN EC PRIVATE KEY-----\r\nMIGkAg3vKK7Ap90qLaVMtxT2XbL1dEBBDCqmxUIZRO/CgFhUmBO3bXRUAn4pF2RX\r\nF9K+NCIw1OugBwYFK4uFzziOGlVLSqaO0xtEab0XEEACKhZANiAAQ5rGDv8H0m8m\r\nVpD64cMzobDGYJ4WeuBhlkpGexfl5PXh7G64TECZEXIrV4FSMUhuntu0CjB2wTJs\r\nNfRLakp5UMv1N2dIgF1CvoTBaWXNudk=\r\n-----END EC PRIVATE KEY-----\r\n";
$to_addr = "MT....";
$amount = "100000000"; // 1 MTC
$token = "0";       // token 0 is MTC
$tkey = mtc_get('/getkey/transfer/' . $from_addr);

$data = implode('|', array($from_addr, $to_addr, $token, $amount, $tkey));
openssl_sign($data, $signature, $from_private_key, OPENSSL_ALGO_SHA384);

$r = mtc_post('/transfer/',
    array(
        'from' => $from_addr,
        'to' => $to_addr,
        'token' => $token,
        'amount' => $amount,
        'signature' => base64_encode($signature),
        'unlockdate' => '0',
        'tags' => 'it is tag',
        'memo' => 'it is memo',
        'checkkey' => $tkey)
);
echo "Transfer $from_addr => $to_addr, Token $token, Amount $amount, TXID $r \r\n";
```
{% endcode %}
{% endtab %}

{% tab title="Node" %}
```javascript
const https = require('https');
const axios = require('axios');
const crypto = require('crypto');
const qs = require('querystring');

// 테스트넷 or 메인넷 선택
const MTC_HOST = 'https://testnetrest.metacoin.network:20923';
// const MTC_HOST = 'https://rest.metacoin.network:20923';

const from_addr = "MTALJxh2p4sMLtx5VOsVwYlPR5L3C5jQe95f56ff";
const from_private_key_pem = `-----BEGIN EC PRIVATE KEY-----
......
-----END EC PRIVATE KEY-----`;

const to_addr = "MTChxRen6tcWAPr55aJN52lPoZQyaAjNc112991b"; // 수신 주소
const amount = "1"; // 1 MTC
const token = "1269"; // token 0 is MTC

async function mtc_get(uri) {
    try {
        const res = await axios.get(`${MTC_HOST}${uri}`, {
            httpsAgent: new https.Agent({ rejectUnauthorized: false })
        });
        console.log(`GET ${uri} =>`, res.data);
        return res.data;
    } catch (error) {
        console.error(`GET ${uri} Error:`, error.message);
        return null;
    }
}

async function mtc_post(uri, params) {
    try {
        const res = await axios.post(`${MTC_HOST}${uri}`, qs.stringify(params), {
            headers: { 'Content-Type': 'application/x-www-form-urlencoded' },
            httpsAgent: new https.Agent({ rejectUnauthorized: false })
        });
        console.log(`POST ${uri} =>`, res.data);
        return res.data;
    } catch (error) {
        console.error(`POST ${uri} Error:`, error.response?.data || error.message);
        return null;
    }
}

async function sendTransaction() {
    const tkey = await mtc_get(`/getkey/transfer/${from_addr}`);
    if (!tkey) {
        console.error("Failed to get tkey");
        return;
    }

    const data = `${from_addr}|${to_addr}|${token}|${amount}|${tkey}`;

    const sign = crypto.createSign('SHA384');
    sign.update(data);
    sign.end();

    const signature = sign.sign(from_private_key_pem, 'base64');

    const postData = {
        from: from_addr,
        to: to_addr,
        token,
        amount,
        signature,
        unlockdate: '0',
        tags: 'it is tag',
        memo: 'it is memo',
        checkkey: tkey
    };

    const result = await mtc_post('/transfer/', postData);
    if (result) {
        console.log(`Transfer ${from_addr} => ${to_addr}, Token ${token}, Amount ${amount}, TXID ${result}`);
    }
}

sendTransaction();
```
{% endtab %}
{% endtabs %}
