# MRC400(NFT)

## NFT(Non-fungible token) is a digital asset that has its own identifiers and unique such as game items or masterpiece and cannot be replaced by another. <a href="#6439" id="6439"></a>

* Each has a unique ID.
* This is like a ticket. Tickets to enter the show look the same, but have different seat numbers.
* If you are showing a movie in a theater and selling tickets,
* Create a "movie screening plan" using MRC400, and create an admission ticket using MRC401 under the created MRC400.

### Support single assets for NFT.

MRC400 supports the single assets and shares some portion of commission to a copyright holder or a profit share holder on Sales/Auction.

It supports to create Token/MRC401 and Mint and Burn by QR Code or Deeplink on MetaWallet webpage.

### Copyright Information <a href="#63b5" id="63b5"></a>

NFT is usually used in work of art.

However, there are so confused to users who want to own the NFT. because it is unclear which art is based on.

In MRC402, copyright information can be set only once when NFT is created.

It will ensure that those who wish to own the NFT recognize which work they have by reference this information.

### Burn <a href="#e969" id="e969"></a>

Burn will reduce the total issuance and it can do by an issuer only.

If there is an initial asset, it will be returned equal to the burned amount \* the initial asset.

### Mint <a href="#ac24" id="ac24"></a>

Mint will increase the total issuance and can only be issued by issuer.

If there is an initial asset, it will be reduced from the creator’s wallet by the amount of mint \* initial asset.

### Transfer <a href="#1ac9" id="1ac9"></a>

If you want to send multiple MRC401s, you need to send them one by one.

This is equivalent to transferring ownership of each of the multiple homes when you purchase them.

If the MRC400 ID is the same MRC401, ownership can be transferred up to 100 at a time.

### Melt

Users who has got NFT can do the Melting.

But, If you specify a date that Melting function can be executed on creating the NFT, you can not do Melting before that date.

* James sends 100 MTC to Mary with a lockup until January.01.2025.
* Mary can not give 100 MTC to someone until that date.
* But, If James send to Mary it after setting the initial asset as 100 MTC and melting point as January.01.2025 and issuing 1 MRC402 Mary can transfer to someone at any time and the user who has got it get 100 MTC with melting after January.01.2015.

It has the same effect as a lockup and can also be used as a transferable token.

### Support various media <a href="#edeb" id="edeb"></a>

It can publish the NFT by MP4 files as well as images.

It saves in zzal.io because the storing in blockchain consumes excessive traffic and capacity.

zzal.io is a service that stores with distributing images and videos.

### Support Platform <a href="#c55d" id="c55d"></a>

* We open a website “HotDeal.io” that supports NFT trading and provides a variety of information related trading NFT.
* It can be expected to get advertising and transaction fees.
* ADV can be carried out in various support methods.
* If you want to get the commission at a certain percentage on the transaction, sellers send the NFT to “HotDeal.io”,
* “HotDeal.io” send to the seller with deducted the commission after getting the transaction amount from buyers.
* After all, it becomes subordinate to a web service called “HotDeal.io” not a decentralized transaction.

If it sell/auction in Metacoin Network after fill out the platform name, commission rate and receiver’s address for commission on registering MRC402,

Trading is made on the Metacoin Network. The fee is distributed according to the information.

### Support ShareHolder <a href="#cacc" id="cacc"></a>

You can enter the copyright holder on creating NFT or a user who receive the commission on trading.

We called it “ShareHolder”.

ShareHolder can put the address and commission rate up to 5 addresses.

It’s set up at the time of initial creation and can not be changed.

It supports multiple copyright holders and give stable profits on the Metacoin Network.

It helps you to be more creative.\


{% swagger src="../../.gitbook/assets/api.yaml" path="/mrc400" method="post" %}
[api.yaml](../../.gitbook/assets/api.yaml)
{% endswagger %}

```php
<?php
define('MTC_HOST', 'https://testnetrest.metacoin.network:20923');

// change it !!!
$from_addr = "MTPBF7OHamYp0luagfi2RcleKFyQf2qU9d530ee2";
$from_key = "-----BEGIN EC PRIVATE KEY-----\r\nMIGkAgEBBDAbXEsjPkxq54dEOS+KXquoNrJ+VK9+ukXqNLlCUCyZqcVWGxUmF9r1\r\nEURYodDy/f6gBwYFK4EEACKhZANiAARLba/Xyzdbsyq5XigDD8HhhhN0OGk87OSQ\r\n401nZISt5y8wX625P/0N+51jX8ohHks2A9di7GrMBREZKizVuM50pVUmlULRgeKU\r\nLYuguhRSvtxBIoGx5JX++Sk8SdZoRcI=\r\n-----END EC PRIVATE KEY-----\r\n";

$curl = curl_init();
curl_setopt_array($curl, array(
	CURLOPT_URL => MTC_HOST . '/nonce/' . $from_addr,
	CURLOPT_RETURNTRANSFER => true,
	CURLOPT_CONNECTTIMEOUT => 5,
	CURLOPT_TIMEOUT => 20,
	CURLOPT_SSL_VERIFYPEER => false,
	CURLOPT_SSL_VERIFYHOST => false,
	CURLOPT_POST => false,
	CURLOPT_CUSTOMREQUEST => 'GET',
));

$body = curl_exec($curl);
$err_code = curl_errno($curl);
if ($err_code) {
	$err_msg = curl_error($curl);
	throw new Exception($err_msg, $http_code);
}

$http_code = curl_getinfo($curl, CURLINFO_HTTP_CODE);
if ($http_code != '200') {
	throw new Exception($body, $http_code);
}
curl_close($curl);
$curl = null;
$tkey = $body;

$data = array(
	'owner' => $from_addr,
	'name' => 'MRC400 Project',
	'url' => 'http://mrc400-project.domain.com',
	'imageurl' => 'http://mrc400-project.domain.com/image/project.png',
	'allowtoken' => "0",                // or token id
	'category' => 'game',
	'description' => 'Metacoin MRC110 Project',
	'itemurl' => 'https://mrc400-project.domain.com/item/{id}',
	'itemimageurl' => 'https://mrc400-project.domain.com/image/item/{id}',
	'data' => 'project data',
	'socialmedia' => "",    // json_encode(array('twitter' => 'http://twitter.com/'))
	'partner' => "",        // json_encode(array($addr[1][0] => 'partner')),
	'tkey' => $tkey,
);

$sign_data = implode('|', array(
	$data['owner'], $data['name'], $data['url'], $data['imageurl'], $data['category'],
	$data['itemurl'], $data['itemimageurl'], $data['partner'], $data['data'], $tkey
));
openssl_sign($sign_data, $signature, $from_key, OPENSSL_ALGO_SHA384);
printf("Sign : [%s]\n", base64_encode($signature));

$data['signature'] = base64_encode($signature);

$curl = curl_init();
curl_setopt_array($curl, array(
	CURLOPT_URL => MTC_HOST . '/mrc400',
	CURLOPT_RETURNTRANSFER => true,
	CURLOPT_CONNECTTIMEOUT => 5,
	CURLOPT_TIMEOUT => 20,
	CURLOPT_SSL_VERIFYPEER => false,
	CURLOPT_SSL_VERIFYHOST => false,
	CURLOPT_POSTFIELDS => http_build_query($data),
	CURLOPT_POST => true,
	CURLOPT_HTTPHEADER => array('Content-Type: application/x-www-form-urlencoded')
));

$body = curl_exec($curl);
$err_code = curl_errno($curl);
if ($err_code) {
	$err_msg = curl_error($curl);
	throw new Exception($err_msg, $http_code);
}

$http_code = curl_getinfo($curl, CURLINFO_HTTP_CODE);
if ($http_code != '200') {
	throw new Exception($body, $http_code);
}
curl_close($curl);
$curl = null;


$r = json_decode($body, true);
printf("TXID : %s, MRC400 ID : %s\r\n", $r['txid'], $r['mrc400id']);
```

{% swagger src="../../.gitbook/assets/api.yaml" path="/mrc400/{mrc400id}" method="put" %}
[api.yaml](../../.gitbook/assets/api.yaml)
{% endswagger %}

{% swagger src="../../.gitbook/assets/api.yaml" path="/mrc400/{mrc400id}" method="get" %}
[api.yaml](../../.gitbook/assets/api.yaml)
{% endswagger %}

{% swagger src="../../.gitbook/assets/api.yaml" path="/mrc401/{mrc400id}" method="post" %}
[api.yaml](../../.gitbook/assets/api.yaml)
{% endswagger %}

{% swagger src="../../.gitbook/assets/api.yaml" path="/mrc401/{mrc401id}" method="get" %}
[api.yaml](../../.gitbook/assets/api.yaml)
{% endswagger %}

{% swagger src="../../.gitbook/assets/api.yaml" path="/mrc401/transfer/{mrc401id}" method="post" %}
[api.yaml](../../.gitbook/assets/api.yaml)
{% endswagger %}

{% swagger src="../../.gitbook/assets/api.yaml" path="/mrc401/sell" method="post" %}
[api.yaml](../../.gitbook/assets/api.yaml)
{% endswagger %}

{% swagger src="../../.gitbook/assets/api.yaml" path="/mrc401/unsell" method="post" %}
[api.yaml](../../.gitbook/assets/api.yaml)
{% endswagger %}

{% swagger src="../../.gitbook/assets/api.yaml" path="/mrc401/buy/{mrc401id}" method="post" %}
[api.yaml](../../.gitbook/assets/api.yaml)
{% endswagger %}

{% swagger src="../../.gitbook/assets/api.yaml" path="/mrc401/melt/{mrc401id}" method="post" %}
[api.yaml](../../.gitbook/assets/api.yaml)
{% endswagger %}

{% swagger src="../../.gitbook/assets/api.yaml" path="/mrc401/auction" method="post" %}
[api.yaml](../../.gitbook/assets/api.yaml)
{% endswagger %}

{% swagger src="../../.gitbook/assets/api.yaml" path="/mrc401/unauction" method="post" %}
[api.yaml](../../.gitbook/assets/api.yaml)
{% endswagger %}

{% swagger src="../../.gitbook/assets/api.yaml" path="/mrc401/bid/{mrc401id}" method="post" %}
[api.yaml](../../.gitbook/assets/api.yaml)
{% endswagger %}

{% swagger src="../../.gitbook/assets/api.yaml" path="/mrc401/auctionfinish/{mrc401id}" method="get" %}
[api.yaml](../../.gitbook/assets/api.yaml)
{% endswagger %}

