# Private Hosted Channels with Poncho
This is a draft guide regarding a system of testing [Hosted Channels](https://fanismichalakis.fr/posts/what-are-hosted-channels/) (HC) offered by [Poncho](https://github.com/nbd-wtf/poncho) (plugin for CLN) in a private manner. Later this scenario can be extended to a public offer of HC.

## Introduction

The idea is to use the already existing liquidity pool from a RoF to offer private channels using the technology of Hosted Channels. This idea was based on [my article guide about Private LN banks that can be offered for private users](https://darthcoin.substack.com/p/bitcoin-private-banks-over-lightning), this time testing with a RoF as LSP source and see how can be scaled for a broader audience.

We want to see how these hosted channels can be used at a large scale, linked to a RoF and can offer good routes to private users using private nodes on their mobiles (OBW).

I think Poncho and Cliche, OBW are really underestimated LN tools. Especially for "privacy advocates", they don't know the real potential of these and also could help a lot in regards of  LN issues with liquidity, channel jamming, path finding, fees etc.

### The test will have 2 phases:
- 1st phase - using a central Poncho node with various OBW HC clients, making some testing payments, out of the RoF but also between clients, nodes etc, testing all kind of possible payments. So no need for all RoF members to run a Poncho! Just one for all OBW testers.
- 2nd phase - adding 1-2 new Poncho nodes to the RoF testing group. OBW have by default MPP, that means we can test even further payments taking multi-parts and routes and see how is going.
- Optional (3rd phase), using [Cliche](https://github.com/nbd-wtf/cliche) as liquidity client of Poncho for any other node. Right now LNbits and LNTXBOT are using it as liquidity client. Act the same as OBW but in this case for a normal desktop node.

![image](https://user-images.githubusercontent.com/56997124/210340892-0f3c4fd7-e5a2-4835-9692-4aa681a9facf.png)
Simple network scheme using HC for private mobile nodes

### What will be used in this testing phase:
- An existing RoF, it doesn't matter the size, amount of liquidity or number of channels. Can be anyone, but at least with some basic knowledge managing LN channels, using LN mobile wallet OBW and offering detailed feeedback about payments using HC.
- A "master of ceremony", a node runner with advanced knowledge in installing apps, plugins, in command line and managing hosted channels.
- A node that will be used as main HCP (hosted channels provider), with Poncho installed. It can be also a LND node, but next to this LND must run a CLN. Or can be separate nodes, it doesn't matter. The idea is to have for this Poncho node the gate to the ring group that offers routes. If is already a CLN node in the RoF is better so we don't have to add a big channel between CLN+Poncho and LND gate to RoF. Is up to you how you find the better scheme.
- HC Clients using OBW connected to this central Poncho node.
- For the testing purposes is prefered a clearnet Poncho node.

### Links:
- [Poncho](https://github.com/nbd-wtf/poncho) to be installed in a CLN node
- [OBW mobile app](https://github.com/nbd-wtf/obw) (only Android) to be installed on various devices. You can find it also on Play Store, but is better to use github repositories directly (see [releases](https://github.com/nbd-wtf/obw/releases)).
- [OBW Manual guide](https://darthcoin.substack.com/p/obw-open-bitcoin-wallet) - detailed description and guide how to use OBW, already translated in other 3 languages.
- [Cliche](https://github.com/nbd-wtf/cliche) - Poncho client for other nodes
- [Hosted Channels TG group](https://t.me/hostedchannels) - in case we need to inform Fiatjaf about possible issues.
- [OBW TG group](https://t.me/openbitcoinwallet) - in case we need to inform Fiatjaf about possible issues with OBW
- [The discussion section of this repository](https://github.com/Darth-Coin/Poncho-OBW-testing/discussions) - where we can post all tests we've done, issues encountered etc.


## Description
Many people are afraid of hosted channels because 1st thing they think is "ohh... are custodial" but the perce3ption is wrong. You are custoding your OWN hosted channels, for your own private use and for your friends and family (that can't run their own LN nodes).

OBW is per se a mobile LN node, using Immortan implementation. Is also like a decoy for your own node because HC will not reveal their nodeID. 

There's a huge potential for using this decoy for small merchants that want to add a bit more privacy in receiving.

Imagine a small merchant using [Cliche](https://github.com/nbd-wtf/cliche) (as client for Poncho) for his own node or simple OBW to receive payments. The HCP (Poncho node) can act as a decoy not revealing the last destination of the payment, because is behind a HC.

And that OBW or node client (with Cliche) can any time, close the HC and start a new identity. Will be NO WAY to trace such payment.

If you want even more privacy... add more layers like these.

Then is the LSP aspect.

Right now we have many node runners, but they are moving mostly sats between routing nodes. They ignore totally the private mobile nodes like OBW, Blixt, Breez, Phoenix, Electrum. And these mobile nodes need good liquidity that RoF can offer with private channels and HC. Mobile users are the biggest movers of sats.

Yes, we already built a large network of public channels, now is time to take care of private channels, mobile users, offering them those good routes.

## Objectives
After we finish this testing, if the results are satisfactory it can be extended to a larger audience and the node runners offering these kind of HC could have an incentive.
- HCP (hosted channels providers) could be listed (if they want) in OBW app for public access
- HCP can choose also their own audience with a selected list of private clients
- HCP could earn fees from routing these payments of mobile users
- HCP could offer private banks services with these HC
- HCP also could offer inbound channels liquidity, listed in OBW, also as normal channels peers, but will have to be well selected based on their ranking.
- Mobile users could have good peers and liquidity for their mobile private channels usage
- LN could increase its usage for a broader audience and use cases.

## Installation and testing steps
- If we do not have already a CLN node in the testing group, we can install one. Many bundle nodes could run LND + CLN on same machine. Or if is preffered a separate machine, also could be like that.
- [Install Poncho](https://github.com/nbd-wtf/poncho) onto that CLN machine. Poncho for the moment works only with CLN. Maybe some good coder could adapt it for LND later. Define the parameters indicated in the installation instructions and assign the amount of HC you want to offer for each client.
- Open a big channel, like min 10M sats to the LND node assigned to be the gate to the RoF. So practically this CLN node is using a single pipe to the RoF, could be even a private channel. If you want to use multiple channels, is up to you. But the is important that this pipe to be well linked to a pool of liquidity from a RoF, so can route well all the payments from multiple OBW clients, in and out.
- Is not important to be balanced this channel pipe between Poncho and RoF. The Poncho operator can give sats as credit base to any of his HC clients and they can start right away to send sats using that channel. So the testing will start practically by sending out sats from OBW, having most of liquidity on the Poncho side. It can be indeed also used a double liquidity, one channel out and one in so the Poncho node could have liquidity in both directions.
- In 2-3-4-5 OBW clients, open a private HC by scanning the QR nodeURI of the Poncho node and add it as hosted channel, NOT as normal channel. Will popup the option in OBW. Could be the same node operators from RoF or their family members, normal users testing payments with OBW. Important is that can communicate clearly all testing steps and with most of the details.
- Start making payments with OBW in and out and monitor all the routes. Do all kind of payments, stress test at maximum.
- Please use [this repository disscusion section](https://github.com/Darth-Coin/Poncho-OBW-testing/discussions/categories/tests) to post all testing steps and issues encountered. If users do not want to post their node / personal data, we can strikeout that and leave only what is important to debug. Or they can just post their findings / feedback in the TG group we created especially for testing group.
- Please use this format as example to post your testing, as [I used in the testing for Blixt mobile wallet](https://github.com/hsjoberg/blixt-wallet/issues/1065).
Indicate in details, what kind of payments you did, amounts, fees, time taken, routes / hops (if possible), destinations etc. So we can have a better understanding of the tests.

This is an ongoing testing ground, so is not really necessary to be done in a certain time frame. These tests need time and we want to see how respond in various situations. So take your time, do them whenever you can or want, choosing specific timing as you want. Important is the feedback.
