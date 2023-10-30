---
title: 區塊鏈跨鏈橋簡介
description: 跨鏈橋讓使用者能在不同的區塊鏈之間轉移資金
lang: zh-tw
---

# 區塊鏈跨鏈橋 {#prerequisites}

_第三代網際網路已發展成由一層和二層網路擴容解決方案組成的生態系統，每個解決方案都有獨特的功能和取捨。 隨著區塊鏈協定數量的增加，[跨鏈移動資產的需求也隨之增加](<https://dune.xyz/eliasimos/Bridge-Away-(from-Ethereum)>)。  為了滿足此需求，我們需要跨鏈橋。_

<Divider />

## 什麼是跨鏈橋？ {#what-are-bridges}

區塊鏈跨鏈橋的作用，與現實世界中的橋樑，功用是一樣的。 就像現實橋樑連接兩地一樣，跨鏈橋連接的是兩個區塊鏈生態系統。 跨鏈橋透過傳送資訊和資產，來促進區塊鏈之間的通訊。

讓我們來看一個例子：

你來自美國，正計劃去歐洲旅行。 你有美元，但你需要歐元才能消費。 為了將你的美元兌換成歐元，你可以支付少量手續費來換匯。

但如果想換用不同的區塊鏈，要怎麼做？ 假設你想用以太坊主網上的以太幣兌換 [Arbitrum](https://arbitrum.io/) 上的以太幣。 就像我們為歐元進行貨幣換匯一樣，我們需要一種機制，將我們的以太幣從以太坊轉移到 Arbitrum。 跨鏈橋能實現這種交易。 在這個例子中，[Arbitrum 有一個原生的跨鏈橋](https://bridge.arbitrum.io/)，可以將以太幣從以太坊主網轉移到 Arbitrum。

## 為什麼我們需要跨鏈橋？ {#why-do-we-need-bridges}

所有區塊鏈都有局限性。 以太坊需要卷軸才能擴容及跟上需求。 或者，Solana 和 Avalanche 等一層網路，透過不同的設計來實現更高的吞吐量，但是犧牲了去中心化。

然而，所有的區塊鏈都是在獨立的環境中開發的，並具有不同的規則和共識機制。 這意味著其無法原生通訊，代幣也無法在區塊鏈之間自由移動。

跨鏈橋的存在就是為了連接區塊鏈，使彼此之間能傳送資訊和代幣。

跨鏈橋能實現以下幾點：

- 跨鏈傳送資產和資訊
- 使去中心化應用程式能取得多種區塊鏈的優勢，因此增強區塊鏈的能力（因為協定現在在設計上有更多的創新空間）。
- 能讓使用者存取新的平台，並徹底善用不同區塊鏈的優勢。
- 能讓來自不同區塊鏈生態系統的開發者相互合作，並為使用者建立新平台。

[如何通過跨鏈橋將代幣轉移至第二層網路](/guides/how-to-use-a-bridge/)

<Divider />

## 跨鏈橋使用案例 {#bridge-use-cases}

以下是一些可以使用跨鏈橋的場景：

### 降低交易費 {#transaction-fees}

假設你在以太坊主網上擁有以太幣，但想要以更便宜的交易費來探索不同的去中心化應用程式。 將你的以太幣從主網跨鏈傳送到以太坊二層網路卷軸，可以享有更低的交易費。

### 在其他區塊鏈上的去中心化應用程式 {#dapps-other-chains}

假設你一直在以太坊主網上使用 Aave 借出泰達幣，但在 Polygon 上使用 Aave 借出泰達幣的利率更高。

### 探索區塊鏈生態系統 {#explore-ecosystems}

如果你在以太坊主網上擁有以太幣，並想探索其他一層網路，以試試其原生的去中心化應用程式。 你可以使用跨鏈橋，將以太幣從以太坊主網轉移到其他一層網路。

### 擁有原生加密資產 {#own-native}

假設你想擁有原生比特幣 (BTC)，但你的資金只存在於以太坊主網上。 要在以太坊上獲得比特幣，你可以購買包裝比特幣 (WBTC)。 然而，WBTC 是以太坊網路原生的 ERC-20 代幣，這表示它是以太坊版本的比特幣，而不是比特幣區塊鏈上的原始資產。 要擁有原生比特幣，你必須使用跨鏈橋將資產從以太坊轉移到比特幣。 這將會橋接 WBTC 並轉換為原生比特幣。 或者，你可能擁有比特幣，並希望在以太坊去中心化金融協定中使用它。 這將需要以另一種方式橋接，從比特幣到 WBTC，然後可將 WBTC 作為以太坊上的資產。

<InfoBanner shouldCenter emoji=":bulb:">
  你也可以使用 <a href="/get-eth/">中央化交易所</a> 完成上述所有操作。 但是，除非你已有資金在交易所內，否則會涉及多個步驟，而你可能會覺得使用跨鏈橋比較好。
</InfoBanner>

<Divider />

## 跨鏈橋的類型 {#types-of-bridge}

跨鏈橋具有許多不同的設計類型和複雜度。 通常，跨鏈橋分為兩類，即受信任和去信任跨鏈橋。

| 受任跨鏈橋                                                                              | 去信任跨鏈橋                                               |
| --------------------------------------------------------------------------------------- | ---------------------------------------------------------- |
| 受信任跨鏈橋倚賴一個中心實體或系統來運作。                                              | 去信任跨鏈橋利用智慧型合約及演算法來運行。                 |
| 在資金監管及跨鏈橋的安全性方面，具有許多信任假設。 使用者大多有賴於跨鏈橋運營商的聲譽。 | 屬於去信任，即跨鏈橋的安全性與底層區塊鏈的安全性相同。     |
| 使用者需放棄對其加密資產的控制。                                                        | 透過智慧型合約，去信任跨鏈橋讓使用者能繼續控制他們的資金。 |

簡而言之，我們可以說受信任跨鏈橋具有信任假設，去信任跨鏈橋則是將信任最小化，不必在底層領域之外做出新的信任假設。 這些術語可做這樣的解釋：

- **去信任**：安全性等同於底層領域。 如 [Arjun Bhuptani 在本文中所述。](https://medium.com/connext/the-interoperability-trilemma-657c2cf69f17)
- **信任假設：**在系統中加入外部驗證者，擺脫底層領域的安全性，其加密經濟的安全性因此降低。

為了更加理解這兩種方法的主要區別，讓我們舉個例子：

想像你在機場的安檢站。 檢查站有兩種類型：

1. 人工檢查站－由安檢人員操作，其以人工方式檢查機票和身份的所有細節，完畢後才提供登機證。
2. 自助報到－由一台機器操作，你可以在其中輸入你的航班詳細資訊，一切檢查完畢後將會收到登機證。

人工檢查站類似於受信任模式，因為倚賴第三方來運作，即安檢人員。 使用此服務，你相信工作人員會做出正確的決定並正確使用你的私人資訊。

自助報到類似去信任模式，因為卸下了操作員的角色，並使用科技進行操作。 使用者始終可以控制他們的資料，且不必將私人資訊交託給第三方。

許多橋接解決方案採用的模式，介於這兩個極端之間，去信任程度不等。

<Divider />

## 使用跨鏈橋的風險 {#bridge-risk}

跨鏈橋仍在早期發展階段。 很可能尚未發現最佳的跨鏈橋設計。 與任何類型的跨鏈橋互動都有風險：

- **智慧型合約風險 —** 程式碼漏洞風險，這可能導致使用者資金流失
- **技術風險 —** 軟體故障、程式碼漏洞、人為錯誤、垃圾郵件和惡意攻擊可能會干擾使用者作業

此外，受信任跨鏈橋由於增加了信任假設，因此帶來額外的風險，例如：

- **審查風險 —** 跨鏈橋運營商理論上可以阻止使用者利用跨鏈橋來轉移資產
- **託管風險 —** 跨鏈橋運營商可以串通盜取使用者的資金

如果出現以下情況，使用者的資金將面臨風險：

- 智慧型合約中存在漏洞
- 使用者出錯
- 底層區塊鏈被駭客入侵
- 在某個受信任跨鏈橋中，跨鏈橋運營商心懷不軌
- 跨鏈橋被駭客入侵

最近一次駭客攻擊針對的是 Solana 的 Wormhole 跨鏈橋，[在駭客攻擊期間其被竊取了 12 萬包裝以太幣（3.25 億美元）](https://rekt.news/wormhole-rekt/)。 很多[最嚴重的區塊鏈駭客事件都與跨鏈橋有關](https://rekt.news/leaderboard/)。

跨鏈橋對於讓使用者加入以太坊二層網路至關重要，對於想要探索不同生態系統的使用者也是如此。 然而，與跨鏈橋互動涉及上述風險，使用者必須了解跨鏈橋做出了哪些權衡取捨。 這裡提供一些[跨鏈安全性策略](https://blog.debridge.finance/10-strategies-for-cross-chain-security-8ed5f5879946)。

<Divider />

## 延伸閱讀 {#further-reading}

- [EIP-5164：跨鏈執行](https://ethereum-magicians.org/t/eip-5164-cross-chain-execution/9658) _2022 年 6 月 18 日 - Brendan Asselstine_
- [二層網路跨鏈橋風險框架](https://gov.l2beat.com/t/l2bridge-risk-framework/31) _2022 年 7 月 5 日 - Bartek Kiepuszewski_
- [「為什麼未來會多鏈並存但不是跨鏈」](https://old.reddit.com/r/ethereum/comments/rwojtk/ama_we_are_the_efs_research_team_pt_7_07_january/hrngyk8/) _2022 年 1 月 8 日 - Vitalik Buterin_
- [什麼是區塊鏈跨鏈橋？如何予以分類？](https://blog.li.finance/what-are-blockchain-bridges-and-how-can-we-classify-them-560dc6ec05fa) _2021 年 2 月 18 日 - Arjun Chand_
- [什麼是跨鏈橋？](https://www.alchemy.com/overviews/cross-chain-bridges) _2020 年 5 月 10 日 - Alchemy_
- [區塊鏈跨鏈橋：建立加密網路的網路](https://medium.com/1kxnetwork/blockchain-bridges-5db6afac44f8) _2021 年 9 月 8 日 - Dmitriy Berenzon_
- [加密貨幣領域的跨鏈橋](https://medium.com/chainsafe-systems/bridges-in-crypto-space-12e158f5fd1e) _2021 年 8 月 23 日 - Ben Adar Hyman_
- [互操作性的三難困境](https://medium.com/connext/the-interoperability-trilemma-657c2cf69f17) _2021 年 10 月 1 日 - Arjun Bhuptani_
- [保護跨鏈橋：正確完成跨鏈通訊](https://medium.com/dragonfly-research/secure-the-bridge-cross-chain-communication-done-right-part-i-993f76ffed5d) _2021 年 8 月 23 日 - Celia Wan_