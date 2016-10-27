Traverse Email Documentation
----------------------------

Contents
--------

  * [Overview](#overview)
  * [Getting started](#getting-started)
  * [Pixel Block](#pixel-block)
  * [CNAME](#cname)
  * [Hashes](#hashes)
  * [Example](#example)

Overview
--------

The Traverse Pixel Block allows you to license linkage data generated by your email campaigns.

Getting started
---------------

To use the Pixel Block, [add it](#pixel-block) to your HTML email.

Pixel Block
-----------

The Pixel Block is a set of 10 pixels, each of which redirects to a separate partner, passing them the recipient's hashed email address and allowing them to set a cookie.

Each pixel has the following form:
 
>\<img border="0" width="1" height="1" src="http://`cname`/v1/`clientId`/`index`.gif?`hashType`=`hashValue`&domain=`domain`"/\>

| Parameter    | Description | Required |
| ------------ |------------ | -------- |
| `cname` | See [CNAME](#cname), below. | Yes |
| `clientId` | Your 36-character client ID (includes hyphens). | Yes |
| `index` | How many pixels *with this hash type* came before this one? | Yes |
| `hashType` | The [hash](#hashes) type. | Yes |
| `hashValue` | The [hash](#hashes) value. | Yes |
| `domain` | The recipient's domain. | No |

*Please see the [example](#example), below.*

Hashes
------

Our match partners expect compute hashes using varying schemes. Most want the email address converted to lowercase before hashing; however, some want it hashed using MD5 whereas others want SHA-1.

The following `hashType`s are supported:

| Parameter    | Description | *Recommended* |
| ------------ |------------ | ------------- |
| `emailMd5Lower` | MD5 hash of lowercase email address. | Yes |
| `emailSha1Lower` | SHA1 hash of lowercase email address. | Yes |
| `emailMd5Upper` | MD5 hash of *uppercase* email address. | No |
| `emailSha1Upper` | SHA1 hash of *uppercase* email address. | No |

For example, if the email address is `foo@BAR.com`, then `emailMd5Upper` would be `6d881a14e8fb4886b2742f0b4aa10d30`.

CNAME
-----

Our pixels are hosted at `email.traversedlp.com`. However, in order to protect your deliverability, you should serve them from a domain you control, via a [CNAME record](https://en.wikipedia.org/wiki/CNAME_record).

For example, if your sending domain is `example.com`, you could create a CNAME record for `traverse.example.com` that resolves to `email.traversedlp.com`, and then use that subdomain in the [Pixel Block](#pixel-block).

Example
-------

Suppose you control `example.com`, have set up a [CNAME record](#domain) pointing `traverse.example.com` to `email.traversedlp.com`, and you're sending an email to `foo@BAR.com`.

Include at least 5 pixels with `emailMd5Lower`, and at least 5 more with `emailSha1Lower`, like so (*notice the changing `index`*):

```
<img border="0" width="1" height="1" src="http://traverse.example.com/v1/YOUR-CLIENT-ID-HERE/0.gif?emailMd5Lower=f3ada405ce890b6f8204094deb12d8a8&domain=gmail.com"/>
<img border="0" width="1" height="1" src="http://traverse.example.com/v1/YOUR-CLIENT-ID-HERE/1.gif?emailMd5Lower=f3ada405ce890b6f8204094deb12d8a8&domain=gmail.com"/>
<img border="0" width="1" height="1" src="http://traverse.example.com/v1/YOUR-CLIENT-ID-HERE/2.gif?emailMd5Lower=f3ada405ce890b6f8204094deb12d8a8&domain=gmail.com"/>
<img border="0" width="1" height="1" src="http://traverse.example.com/v1/YOUR-CLIENT-ID-HERE/3.gif?emailMd5Lower=f3ada405ce890b6f8204094deb12d8a8&domain=gmail.com"/>
<img border="0" width="1" height="1" src="http://traverse.example.com/v1/YOUR-CLIENT-ID-HERE/4.gif?emailMd5Lower=f3ada405ce890b6f8204094deb12d8a8&domain=gmail.com"/>
<img border="0" width="1" height="1" src="http://traverse.example.com/v1/YOUR-CLIENT-ID-HERE/0.gif?emailSha1Lower=823776525776c8f23a87176c59d25759da7a52c4&domain=gmail.com"/>
<img border="0" width="1" height="1" src="http://traverse.example.com/v1/YOUR-CLIENT-ID-HERE/1.gif?emailSha1Lower=823776525776c8f23a87176c59d25759da7a52c4&domain=gmail.com"/>
<img border="0" width="1" height="1" src="http://traverse.example.com/v1/YOUR-CLIENT-ID-HERE/2.gif?emailSha1Lower=823776525776c8f23a87176c59d25759da7a52c4&domain=gmail.com"/>
<img border="0" width="1" height="1" src="http://traverse.example.com/v1/YOUR-CLIENT-ID-HERE/3.gif?emailSha1Lower=823776525776c8f23a87176c59d25759da7a52c4&domain=gmail.com"/>
<img border="0" width="1" height="1" src="http://traverse.example.com/v1/YOUR-CLIENT-ID-HERE/4.gif?emailSha1Lower=823776525776c8f23a87176c59d25759da7a52c4&domain=gmail.com"/>
```
