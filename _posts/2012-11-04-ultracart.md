---
layout: post
title: UltraCart
categories: integrations
author: Eric Fung
summary: UltraCart provides an integration option with KISSmetrics. Here's what you need to know.
---
UltraCart provides an integration option with KISSmetrics. Please refer to the administrative panel for where to insert your KISSmetrics API key. [Where is this key given? If it's to be built as noted below, this should be clearere. There are many places in the documentation that refer to an API. And saying that it is not to be confused with the URL API is not much help.]

## What's Included

Doing so will place our [JavaScript library][js] on the checkout pages. Additionally, UltraCart has set up to pass these events without any further setup on your end:

{% highlight js%}
_kmq.push(['record', 'Added Item to Cart': {'Product': THE_PRODUCT_CODE  }]);
_kmq.push(['record', 'Completed Purchase', {'Purchase Amount' : REVENUE_AMOUNT }]);
{% endhighlight %}

## What To Do

However, because users are going from your website/domain to UltraCart's domain `secure.ultracart.com`, we have to make sure that we recognize it's the same person going through the entire checkout funnel, from beginning to end. You can refer to our [article on using the JavaScript library on more than one domain][domains] for more details.

### Example

Here's an ***example*** of JavaScript you would add to modify your Add to Cart buttons:

{% highlight html %}
<script type="text/javascript">
// This block would go below the main JavaScript code we provide in kissmetrics.com/settings

_kmq.push(function()
  { document.getElementById("frm1").action = 'http://secure.ultracart.com/cgi-bin/UCEditor?MerchantID=foo&kmi=' + encodeURIComponent(KM.i());
  } );
</script>
{% endhighlight %}

This looks for the `<form >` element with `id="frm1"` and updates its action when someone submits. *Please refer to your own UltraCart setup; you may have set up the Add to Cart forms differently.* Additionally, please update the `MerchantID` parameter to use your own UltraCart merchant ID.

Thanks to [BCOSkins][bco] for helping with testing this.

[js]: /apis/javascript
[domains]: /apis/javascript/tracking-multiple-domains
[bco]: http://www.bcoskins.com

[live]: http://support.kissmetrics.com/tools/live
