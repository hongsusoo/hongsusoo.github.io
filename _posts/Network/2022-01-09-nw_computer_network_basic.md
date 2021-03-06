---
defaults:
  - scope:
      path: ""
      type: posts
    values:
      layout: single
      author_profile: true
      comments: true
      share: true
      related: true

title: "Computer Networking ๊ธฐ์ด ์ ๋ฆฌ"
excerpt: "about : Network Basic"
toc: true
toc_sticky: true
toc_label: "Label"
categories: 
  - Network Basic
tags:
  - [Computer Networking]
date: 2022-01-09
last_modified_at: 2022-01-09
---

<br>

# Computer Networking Overview

๐กyoutube "Networking Class"์ ๊ฐ์๋ฅผ ๋ณด๊ณ  ์ ๋ฆฌํจ [link](https://www.youtube.com/watch?v=v9IVz5m_SCs&list=PLQFHF6cwEgwPYzMqIzpczc8sYe3VOe6Si)

## ์ฉ์ด ๋ฐ ๊ฐ๋
### Nework ๊ตฌ์ฑ

1. Application : Youtube ๋ฑ ๋ฐ์ดํฐ๋ฅผ ์์ฑ, ์ฌ์ฉ, ์ฒ๋ฆฌ
2. Device
    - End Device : PC, Server, Smartphone, IoT๊ธฐ๊ธฐ ๋ฑ
    - Networking Device : ์ ์ก์ฅ๋น, Switch, AP, Router, L4/L7, Firewall, VPN..
3. Media : Wired or Wireless
4. Protocol
    - ํต์ ์ ์ํ ํ์ค, ๊ท์น(FTP, HTTP, UDP์ ๋ค์ด๊ฐ๋ P๊ฐ Protocol)

### Network ๋ฐฉ์

- Unicast(1๋1 ํต์ ), Multicast(1๋N), Broadcast(1๋์ ์ฒด)
    <img src="https://user-images.githubusercontent.com/77658029/148672296-7ccd9e15-5bce-4fd9-8f1f-cfd234a90d40.png"  width="50%" height="50%"/>
- Simplex(๋จ๋ฐฉํฅ ํต์ ), Duplex(์๋ฐฉํฅ ํต์ )
- Connection Oriented(TCP, ์ฐ๊ฒฐ ํ ๋ฐ์ดํฐ ์ ์ก) / Connectionless(UDP, ์ฐ๊ฒฐ ์์ด ๋ฐ์ดํฐ ์ ์ก)
- LAN(Local Area Network) / WAN(wide area network)
- ์ฐ๊ฒฐ๋ฐฉ์ : Point to Point,Mulit-Access
- ์ ๋ฌ๋ฐฉ์ : 
    - Circuit Switching : ํ๋์ ํ์ ์ ํ ๋น๋ฐ์ ๋ฐ์ดํฐ๋ฅผ ์ฃผ๊ณ  ๋ฐ์, ํต์ ์ด ์ฐ๊ฒฐ๋๋ฉด ๊ทธ ํ์ ์ ๋์ ํ์ฌ ์ฌ์ฉํ๊ธฐ ๋๋ฌธ์ ๋ค๋ฅธ ์ฌ๋๋ค์ด ๋ผ์ด๋ค ์ ์์, ํ์ง๋ง ์๋์ ์ฑ๋ฅ์ ์ผ์ ํ๊ฒ ์ ์งํ  ์ ์์, ํ์ ์ ์ชผ๊ฐ์ ์ฐ๋ ๋ฐฉ์์ผ๋ก TDM(time division multitasking), FDM(frequency division multitasking) ๋ฐฉ์์ด ์์
        <img src="https://user-images.githubusercontent.com/77658029/148672818-a404aff2-813f-444d-9a7b-65f92cca5383.png"  width="50%" height="50%"/>
    - Packet Switching : packet ๋จ์๋ก ์ชผ๊ฐ์ ์ ๋ฌ, Packet์ header์ ์ถ๋ฐ์ง์ ๋ชฉ์ ์ง์ ๋ํ ์ ๋ณด๊ฐ ์์ด์ ์ ๋ฌํด์ค, ๋ผ์ฐํ ์๊ณ ๋ฆฌ์ฆ์ ํ์ฉํ์ฌ ๊ฒฝ๋ก๋ฅผ ์ค์ ํ๊ณ  ๋ผ์ฐํฐ๋ค์ ํตํด ์ ๋ฌ์ด ์ด๋ค์ง, ๋ค์ ๋ผ์ฐํฐ๋ก ์ด๋ํ๊ธฐ ์ ์ ๋๊ธฐ(queueing)๋ฅผ ํ๋๋ฐ, ์ด๋ ์์ฉํ  ์ ์๋ ํ์ ๋ฒ์๋ฅผ ์ด๊ณผํ๋ฉฐ ์์ค์ด ์๊น
        <img src="https://user-images.githubusercontent.com/77658029/148672812-6c5cd7d5-343f-47d9-b5c9-ab47ace65dd1.png"  width="50%" height="50%"/>
- Newtork Topoplogy(๋คํธ์ํฌ ํ ํด๋ก์ง) : ๋ง๊ตฌ์ฑ๋ฐฉ์
    - Bus, Star, Ring, Hierarchical, Mesh, Hub&Spoke
        <img src="https://user-images.githubusercontent.com/77658029/148673170-eec1aa19-236f-4b2c-90e8-88c35c475cb9.png"  width="50%" height="50%"/>



**๐reference**
- [Unicast](https://ko.wikipedia.org/wiki/%EC%9C%A0%EB%8B%88%EC%BA%90%EC%8A%A4%ED%8A%B8)
- [์ ๋ฌ๋ฐฉ์](https://swalloow.tistory.com/55)
- [Newtork Topoplogy](https://ko.wikipedia.org/wiki/%EB%84%A4%ED%8A%B8%EC%9B%8C%ED%81%AC_%ED%86%A0%ED%8F%B4%EB%A1%9C%EC%A7%80)
<br>

```
๐ก ์์  ํ์ํ ๋ด์ฉ์ ๋๊ธ์ด๋ ๋ฉ์ผ๋ก ์๋ ค์ฃผ์๋ฉด ๊ฐ์ฌํ๊ฒ ์ต๋๋ค!๐ก 
```
