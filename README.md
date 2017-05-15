# Traverse Email Documentation v1.1:

## Contents

  * [Overview](#overview)
  * [Getting started](#getting-started)
  * [Pixel Block](#pixel-block)
  * [CNAME](#cname)
  * [Hashes](#hashes)
  * [Example](#example)

## Overview

The Traverse Pixel Block allows you to license linkage data generated by your email campaigns.

## Getting started

To use the Pixel Block, [add it](#pixel-block) to your HTML email.

## Pixel Block

The Pixel Block is a set of at least 10 pixels, each of which redirects to a separate partner, passing the partner hashed versions of the recipient's email address and allowing the partner to set a cookie.

Each pixel has the following form:

```
<img border="0" width="1" height="1" src="https://{{cname}}/v1/{{clientId}}/{{index}}.gif?emailMd5Lower={{emailMd5Lower}}&emailSha1Lower={{emailSha1Lower}}&emailSha256Lower={{emailSha256Lower}}&domain={{domain}}"\>
```

| Parameter    | Description | Required |
| ------------ |------------ | -------- |
| `cname` | See [CNAME](#cname), below. | Yes |
| `clientId` | Your 36-character client ID (includes hyphens). | Yes |
| `index` | How many pixels *with this hash type* came before this one? | Yes |
| `emailMd5Lower` | MD5 hash of lowercased email address. | No<sup>*</sup> |
| `emailSha1Lower` | SHA1 hash of lowercased email address. | No<sup>*</sup> |
| `emailSha256Lower` | SHA256 hash of lowercased email address. | No<sup>*</sup> |
| `domain` | The recipient's domain. | No |

<sup>*</sup> __Note__: At least one of the hash types is required. Some partners expect an MD5 hash, but others expect SHA-1 or SHA-256. In order to maximize revenue, please provide all of `emailMd5Lower`, `emailSha1Lower`, and `emailSha256Lower`. If unable to provide all, it is important that you use the same hash parameters with each pixel.

*Please see the [example](#example), below.*

## Hashes

Email addresses must be white-space trimmed and converted to lowercase before hashing.

| Parameter    | Description |
| ------------ |------------ |
| `emailMd5Lower` | MD5 hash of lowercased email address. |
| `emailSha1Lower` | SHA1 hash of lowercased email address. |
| `emailSha256Lower` | SHA256 hash of lowercased email address. |

For example, if the email address is `foo@BAR.com`, then `emailMd5Lower` would be `f3ada405ce890b6f8204094deb12d8a8`.

## CNAME

Our pixels are hosted at `email.traversedlp.com`. However, in order to protect your deliverability, you should serve them from a domain you control, via a [CNAME record](https://en.wikipedia.org/wiki/CNAME_record).

For example, if your sending domain is `example.com`, you could create a CNAME record for `traverse.example.com` that resolves to `email.traversedlp.com`, and then use that subdomain in the [Pixel Block](#pixel-block).

## Example

Suppose you control `example.com`, have set up a [CNAME record](#domain) pointing `traverse.example.com` to `email.traversedlp.com`, and you're sending an email to `foo@BAR.com`.

Include at least 10 pixels with the same hashes provided. You can include one or more of `emailMd5Lower`, `emailSha1Lower`, and `emailSha256Lower` like so (*notice the changing `index`*):

```
<img border="0" width="1" height="1" src="https://traverse.example.com/v1/YOUR-CLIENT-ID-HERE/0.gif?emailMd5Lower=f3ada405ce890b6f8204094deb12d8a8&emailSha1Lower=823776525776c8f23a87176c59d25759da7a52c4&emailSha256Lower=0c7e6a405862e402eb76a70f8a26fc732d07c32931e9fae9ab1582911d2e8a3b&domain=bar.com"/>
<img border="0" width="1" height="1" src="https://traverse.example.com/v1/YOUR-CLIENT-ID-HERE/1.gif?emailMd5Lower=f3ada405ce890b6f8204094deb12d8a8&emailSha1Lower=823776525776c8f23a87176c59d25759da7a52c4&emailSha256Lower=0c7e6a405862e402eb76a70f8a26fc732d07c32931e9fae9ab1582911d2e8a3b&domain=bar.com"/>
<img border="0" width="1" height="1" src="https://traverse.example.com/v1/YOUR-CLIENT-ID-HERE/2.gif?emailMd5Lower=f3ada405ce890b6f8204094deb12d8a8&emailSha1Lower=823776525776c8f23a87176c59d25759da7a52c4&emailSha256Lower=0c7e6a405862e402eb76a70f8a26fc732d07c32931e9fae9ab1582911d2e8a3b&domain=bar.com"/>
<img border="0" width="1" height="1" src="https://traverse.example.com/v1/YOUR-CLIENT-ID-HERE/3.gif?emailMd5Lower=f3ada405ce890b6f8204094deb12d8a8&emailSha1Lower=823776525776c8f23a87176c59d25759da7a52c4&emailSha256Lower=0c7e6a405862e402eb76a70f8a26fc732d07c32931e9fae9ab1582911d2e8a3b&domain=bar.com"/>
<img border="0" width="1" height="1" src="https://traverse.example.com/v1/YOUR-CLIENT-ID-HERE/4.gif?emailMd5Lower=f3ada405ce890b6f8204094deb12d8a8&emailSha1Lower=823776525776c8f23a87176c59d25759da7a52c4&emailSha256Lower=0c7e6a405862e402eb76a70f8a26fc732d07c32931e9fae9ab1582911d2e8a3b&domain=bar.com"/>
<img border="0" width="1" height="1" src="https://traverse.example.com/v1/YOUR-CLIENT-ID-HERE/5.gif?emailMd5Lower=f3ada405ce890b6f8204094deb12d8a8&emailSha1Lower=823776525776c8f23a87176c59d25759da7a52c4&emailSha256Lower=0c7e6a405862e402eb76a70f8a26fc732d07c32931e9fae9ab1582911d2e8a3b&domain=bar.com"/>
<img border="0" width="1" height="1" src="https://traverse.example.com/v1/YOUR-CLIENT-ID-HERE/6.gif?emailMd5Lower=f3ada405ce890b6f8204094deb12d8a8&emailSha1Lower=823776525776c8f23a87176c59d25759da7a52c4&emailSha256Lower=0c7e6a405862e402eb76a70f8a26fc732d07c32931e9fae9ab1582911d2e8a3b&domain=bar.com"/>
<img border="0" width="1" height="1" src="https://traverse.example.com/v1/YOUR-CLIENT-ID-HERE/7.gif?emailMd5Lower=f3ada405ce890b6f8204094deb12d8a8&emailSha1Lower=823776525776c8f23a87176c59d25759da7a52c4&emailSha256Lower=0c7e6a405862e402eb76a70f8a26fc732d07c32931e9fae9ab1582911d2e8a3b&domain=bar.com"/>
<img border="0" width="1" height="1" src="https://traverse.example.com/v1/YOUR-CLIENT-ID-HERE/8.gif?emailMd5Lower=f3ada405ce890b6f8204094deb12d8a8&emailSha1Lower=823776525776c8f23a87176c59d25759da7a52c4&emailSha256Lower=0c7e6a405862e402eb76a70f8a26fc732d07c32931e9fae9ab1582911d2e8a3b&domain=bar.com"/>
<img border="0" width="1" height="1" src="https://traverse.example.com/v1/YOUR-CLIENT-ID-HERE/9.gif?emailMd5Lower=f3ada405ce890b6f8204094deb12d8a8&emailSha1Lower=823776525776c8f23a87176c59d25759da7a52c4&emailSha256Lower=0c7e6a405862e402eb76a70f8a26fc732d07c32931e9fae9ab1582911d2e8a3b&domain=bar.com"/>
```

__Note__: We continue to support supplying one hash per pixel and repeating indexes for each hash type. This is no longer the preferred method of integration. Providing all hashes available to each pixel allows Traverse to maximize your revenue. Example:
```
<img border="0" width="1" height="1" src="https://traverse.example.com/v1/YOUR-CLIENT-ID-HERE/0.gif?emailMd5Lower=f3ada405ce890b6f8204094deb12d8a8&domain=bar.com"/>
<img border="0" width="1" height="1" src="https://traverse.example.com/v1/YOUR-CLIENT-ID-HERE/1.gif?emailMd5Lower=f3ada405ce890b6f8204094deb12d8a8&domain=bar.com"/>
<img border="0" width="1" height="1" src="https://traverse.example.com/v1/YOUR-CLIENT-ID-HERE/2.gif?emailMd5Lower=f3ada405ce890b6f8204094deb12d8a8&domain=bar.com"/>
<img border="0" width="1" height="1" src="https://traverse.example.com/v1/YOUR-CLIENT-ID-HERE/3.gif?emailMd5Lower=f3ada405ce890b6f8204094deb12d8a8&domain=bar.com"/>
<img border="0" width="1" height="1" src="https://traverse.example.com/v1/YOUR-CLIENT-ID-HERE/4.gif?emailMd5Lower=f3ada405ce890b6f8204094deb12d8a8&domain=bar.com"/>
<img border="0" width="1" height="1" src="https://traverse.example.com/v1/YOUR-CLIENT-ID-HERE/0.gif?emailSha1Lower=823776525776c8f23a87176c59d25759da7a52c4&domain=bar.com"/>
<img border="0" width="1" height="1" src="https://traverse.example.com/v1/YOUR-CLIENT-ID-HERE/1.gif?emailSha1Lower=823776525776c8f23a87176c59d25759da7a52c4&domain=bar.com"/>
<img border="0" width="1" height="1" src="https://traverse.example.com/v1/YOUR-CLIENT-ID-HERE/2.gif?emailSha1Lower=823776525776c8f23a87176c59d25759da7a52c4&domain=bar.com"/>
<img border="0" width="1" height="1" src="https://traverse.example.com/v1/YOUR-CLIENT-ID-HERE/3.gif?emailSha1Lower=823776525776c8f23a87176c59d25759da7a52c4&domain=bar.com"/>
<img border="0" width="1" height="1" src="https://traverse.example.com/v1/YOUR-CLIENT-ID-HERE/4.gif?emailSha1Lower=823776525776c8f23a87176c59d25759da7a52c4&domain=bar.com"/>
```
