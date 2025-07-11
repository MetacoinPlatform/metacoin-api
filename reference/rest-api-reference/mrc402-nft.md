---
description: MRC-402 is Token like NFT
---

# MRC402(NFT)

## Support mixed assets for NFT. <a href="#id-52d1" id="id-52d1"></a>

MRC402 supports the mixed assets and shares some portion of commission to a copyright holder or a profit share holder on Sales/Auction.

It supports to create Token/MRC402 and Mint and Burn by QR Code or Deeplink on MetaWallet webpage.

Here is the MRC402’s main features.

### Mixed Assets <a href="#id-2d69" id="id-2d69"></a>

You can create the NFT with combining several tokens not only one token.

* James set as 5 Metacoin and 10 JamesToken(MRC010) per one NFT as initial assets then create 100 JamesNFT.
* It’s withdrawn the 500 Metacoin(5MTC\*100), 1000 JamesToken(10 JamesToken \* 100) from creator’s wallet.
* It’s valued of 5 Metacoin, 10 JamesToken on 1 JamesNFT.
* If a user who has got JameNFT melt it or James who create the JamesNFT burn it, you can get the amount of melted or burned \* 5 Metacoin, 10 JemaesToken(MRC010).

### Copyright Information <a href="#id-63b5" id="id-63b5"></a>

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

### Transfer <a href="#id-1ac9" id="id-1ac9"></a>

MRC402 can send multiple NFTs on transaction not like MRC401.

### Melt <a href="#id-8734" id="id-8734"></a>

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

It helps you to be more creative.

{% openapi src="../../.gitbook/assets/api.yaml" path="/mrc402" method="post" %}
[api.yaml](../../.gitbook/assets/api.yaml)
{% endopenapi %}

{% openapi src="../../.gitbook/assets/api.yaml" path="/mrc402/{mrc402id}" method="get" %}
[api.yaml](../../.gitbook/assets/api.yaml)
{% endopenapi %}

{% openapi src="../../.gitbook/assets/api.yaml" path="/mrc402/transfer/{mrc402id}" method="post" %}
[api.yaml](../../.gitbook/assets/api.yaml)
{% endopenapi %}

{% openapi src="../../.gitbook/assets/api.yaml" path="/mrc402/sell" method="post" %}
[api.yaml](../../.gitbook/assets/api.yaml)
{% endopenapi %}

{% openapi src="../../.gitbook/assets/api.yaml" path="/mrc402/unsell" method="post" %}
[api.yaml](../../.gitbook/assets/api.yaml)
{% endopenapi %}

{% openapi src="../../.gitbook/assets/api.yaml" path="/mrc402/buy/{mrc402id}" method="post" %}
[api.yaml](../../.gitbook/assets/api.yaml)
{% endopenapi %}

{% openapi src="../../.gitbook/assets/api.yaml" path="/mrc402/melt/{mrc402id}" method="post" %}
[api.yaml](../../.gitbook/assets/api.yaml)
{% endopenapi %}

{% openapi src="../../.gitbook/assets/api.yaml" path="/mrc402/auction" method="post" %}
[api.yaml](../../.gitbook/assets/api.yaml)
{% endopenapi %}

{% openapi src="../../.gitbook/assets/api.yaml" path="/mrc402/unauction" method="post" %}
[api.yaml](../../.gitbook/assets/api.yaml)
{% endopenapi %}

{% openapi src="../../.gitbook/assets/api.yaml" path="/mrc402/bid/{mrc402id}" method="post" %}
[api.yaml](../../.gitbook/assets/api.yaml)
{% endopenapi %}

{% openapi src="../../.gitbook/assets/api.yaml" path="/mrc402/auctionfinish/{mrc402id}" method="get" %}
[api.yaml](../../.gitbook/assets/api.yaml)
{% endopenapi %}
