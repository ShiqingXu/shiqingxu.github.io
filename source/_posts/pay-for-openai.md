---
title: openAI 付款记
date: 2023-06-17 11:58:11
tags: openai

---

这些年为了购买国外的服务，花了不少时间，不过大部分都不算折腾。Google Play 支持中国发行的银行卡，Apple 美区帐户支持绑定了中国银行卡的 Paypal 支付，其它区还可以购买 gift card。Netflix、Amazon、Spotify 等也都支持中国发行的银行卡。

唯独 openAI，铁了心不收中国人的钱。

<!--more-->

3 月份时为了能用上 openAI API key，申请了一张虚拟信用卡，当时还能成功绑定，应该也能支付，不过很快就听说那家虚拟信用卡的号段已经被 opanAI ban 掉了。

4月份我用的很少，最终5月中旬出账单时，显示已经支付了，但支付金额是0。此时已经知道卡不行了，所以进入6月之后一直很关心何时出账单，怕自己的帐号因为支付方式的原因被封。

等到6月17日，终于出账单了，果然因为支付方式的原因，没有成功扣款，收到了 openAI 的邮件：

> We were unable to process your last payment for $*.** using your mastercard ending in ****. Your card was declined.
>
> Please review your payment method, and update it if necessary to continue using the API uninterrupted.
>
> 
>
> We'll try to process your payment again in a few days. **If we aren't able to complete your payment by** **Jul 2, 2023 2:00 AM UTC**, your organization's API access will be suspended.

还好没有封号。除了绑定的银行卡，付款页面上还支持两外两种支付方式，于是赶紧尝试。

首先是使用 link.com 的支付服务，上面绑定了我的招行全币卡，支付失败。

然后尝试了 google pay，绑定的也是那张卡，支付失败。

最后尝试将美区 Paypal 添加到 google pay 里，通过 google pay 支付，终于支付成功。Paypal 里绑定的也是那张卡。

套了两层皮之后，openAI 终于获取不到原始信用卡信息了。

把 Paypal 添加到 google pay，也遭遇了一点小问题。从 google pay 跳转到 Paypal 进行认证时，需要验证手机号，而我的 google voice 不被支持，添加中国手机号则直接返回“不能确认是我本人”。解决方案也比较简单，先自行登录 Paypal，这时只会要求验证邮箱，登录之后再从 google pay 跳转过去就不需要登录验证了。大约是 Paypal 的风控策略，不同人遇到的情况可能会有所差别，我这次运气还可以。

最后，4月份的账单并没有被免除，而是添加到5月份里了。可能是因为每扣款一次，openAI 要向 strip 支付 0.3 刀手续费，消费金额太少的话就积攒一下一起扣款。

这个事件带来的互联网二等公民感尤为强烈。希望以后不要遇到这样的事情了。

