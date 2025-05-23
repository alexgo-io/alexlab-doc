---
description: ALEX DAMM introduces discrete liquidity bins, improved LP mechanics, and advanced swap types. Built for precision.
layout:
  title:
    visible: true
  description:
    visible: true
  tableOfContents:
    visible: true
  outline:
    visible: true
  pagination:
    visible: false
---

# ⚡ DAMM: Discrete Automated Market Maker

**DAMM** (Discrete Automated Market Maker) is the next-generation liquidity engine on ALEX DEX. It brings **concentrated liquidity** to Stacks by introducing **price bins** and **virtual balances**, giving liquidity providers (LPs) tighter control over how their funds are deployed.

Unlike traditional AMMs, DAMM allows users to provide liquidity to specific price ranges (bins), concentrating capital where it’s most likely to be used. This improves capital efficiency and gives LPs more control over their positions.

To learn about the math and architecture behind DAMM, check out the detailed breakdown on [our Medium post](https://medium.com/alexgobtc/damm-alex-amm-v3-discrete-automated-market-maker-fa6b2926a69b).

## ✅ What Can You Do with DAMM?

**🔸 Discrete Liquidity Bins**  
LPs no longer need to spread their liquidity across the entire price curve. Instead, they can choose specific “bins” (price ranges where they expect trading to occur). This lets them use their capital more efficiently by focusing it where it's most likely to be used.

**🔸 Virtual Balances (Smoother Price Curves)**  
Even when liquidity is focused in specific bins, virtual balances help smooth out price changes. This means more stable prices for traders and a better overall experience without affecting how LPs manage their positions.

**🔸 Improved Position Management**  
LPs can update their positions at any time by adding or removing a portion of their liquidity. They can also choose which price bins to use, making it easier to stay active and adjust to the market without needing to withdraw everything.

**🔸 Flexible Fee Structure with LP Incentives**  
Each pool on DAMM can set its own trading fees when it’s created. A portion of those fees can be given back to LPs as rewards, helping attract and keep liquidity in a more sustainable way.

**🔸 Advanced Swap Mechanics (IOC/FOK Orders and More)**  
DAMM lets traders use smart swap options like Immediate-or-Cancel (IOC), and soon Fill-or-Kill (FOK). These features help make trades more precise, reducing slippage and improving how orders get filled.
 
## ▶️ Get Started Now

Head to the [DAMM Pools section](https://app.alexlab.co/pool) on ALEX DEX to try it out!

## Support

For assistance, please reach out to our Community Managers on [Discord](https://discord.com/invite/alexlab) or [Telegram](https://t.me/AlexCommunity).
