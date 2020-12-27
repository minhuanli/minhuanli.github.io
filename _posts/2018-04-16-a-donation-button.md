---
layout: post
title: A Metamask Donation Button
description: Cryptocurrency is cool! In this decade, pay me with cryptocurrencies will probably replace the old-fashioned buy me a coffee. In this post, I tried to embedded a donation button in the Jekyll blog page. If the user's browser accidentally has a MetaMask installed, he/she can tip me with a wei or an ether!
tags: ethereum web3js metamask cryptocurrency blog github-page
---


<style>
.tip-button {
  width: 297px;
  height: 49px;
  margin: 20px;
  background-size: 100%;
  background-image: url('/public/image/metamask-off.png');
  cursor: pointer;
}
.tip-button:hover {
  background-image: url('/public/image/metamask-over.png');
}
.tip-button:active {
  background-image: url('/public/image/metamask-off.png');
}
</style>


<style>
.highlight-left {margin-left: 0}
</style>




[Ethereum](https://www.ethereum.org/) is cool! 

**Tip me with ether** is better than **buy me a coffee** nowadays. 

The community around Ethereum is awesome. The [MetaMask]((https://metmask.io)) is a great browser plugin for the Ethereum blockchain, serving many Ðapps, like some collectable, breedable and adorable creatures. 

MetaMask can serve the tipping purpose easily. This post is largely adapted from their own demo: [TipButton](https://github.com/MetaMask/TipButton). This post demos how to embed such donation link in a Jekyll Github page, very straightforward.



## The Tip Button

Here we go:

<div class="tip-button"></div>

It is **SAFE** to click it. An additional window will prompt up **BEFORE** you actually send the 0.005 ether to me, which is equivalent to a coffee by today 2018-04-16.

If you don't have MetaMask installed, please consider visiting [MetaMask](https://metmask.io).

## What is it doing?

1. Metamask provides the [web3.js](https://github.com/ethereum/web3.js/) object for your browser that communicates with the blockchain in the air, manages your accounts, and most importantly protects (hopefully) your private keys.
2. When you initiate a transaction on the Ethereum blockchain, it prompts a window to ask for your permission to sign the transaction.
3. The tipping transaction is constructed in the embedded javascript code.
4. If you hit confirm it, I will get the 0.005 ether after this transaction is mined into the chain.
5. Thanks!

## The Embedded JavaScript

The script is very simple and straightforward:

{% highlight javascript %}
<script>
var tipButton = document.querySelector('.tip-button');
tipButton.addEventListener('click', function() {
  if (typeof web3 === 'undefined') {
    return alert('You need to install MetaMask to use this feature.')
  }
  var user_address = web3.eth.accounts[0];
  if (typeof user_address === 'undefined') {
    return alert('You need to log in MetaMask to use this feature.')
  }
  web3.eth.sendTransaction({
    to: "0x66454C561Cf137F53321945758b0E4645E9EEae8",
    from: user_address,
    value: web3.toWei('0.005', 'ether'),
  }, function (err, transactionHash) {
    if (err) return alert('Thanks for trying out!');
    alert('Thanks for the generosity!!');
  })
})
</script>
{% endhighlight %}{: .highlight-left }



Enjoy the blockchain! <img class="inline" src="/public/LQ144x144.png" alt="LQ" style="width:1.5rem;height:1.5rem;" />






<script>
var tipButton = document.querySelector('.tip-button');
tipButton.addEventListener('click', function() {
  if (typeof web3 === 'undefined') {
    return alert('You need to install MetaMask to use this feature.')
  }
  var user_address = web3.eth.accounts[0];
  if (typeof user_address === 'undefined') {
    return alert('You need to log in MetaMask to use this feature.')
  }
  web3.eth.sendTransaction({
    to: "0x66454C561Cf137F53321945758b0E4645E9EEae8",
    from: user_address,
    value: web3.toWei('0.005', 'ether'),
  }, function (err, transactionHash) {
    if (err) return alert('Thanks for trying out!');
    alert('Thanks for the generosity!!');
  })
})
</script>


