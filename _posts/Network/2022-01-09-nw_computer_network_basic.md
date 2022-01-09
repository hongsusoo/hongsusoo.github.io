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

title: "Computer Networking 기초 정리"
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

💡youtube "Networking Class"의 강의를 보고 정리함 [link](https://www.youtube.com/watch?v=v9IVz5m_SCs&list=PLQFHF6cwEgwPYzMqIzpczc8sYe3VOe6Si)

## 용어 및 개념
### Nework 구성

1. Application : Youtube 등 데이터를 생성, 사용, 처리
2. Device
    - End Device : PC, Server, Smartphone, IoT기기 등
    - Networking Device : 전송장비, Switch, AP, Router, L4/L7, Firewall, VPN..
3. Media : Wired or Wireless
4. Protocol
    - 통신을 위한 표준, 규칙(FTP, HTTP, UDP에 들어가는 P가 Protocol)

### Network 방식

- Unicast(1대1 통신), Multicast(1대N), Broadcast(1대전체)
    <img src="https://user-images.githubusercontent.com/77658029/148672296-7ccd9e15-5bce-4fd9-8f1f-cfd234a90d40.png"  width="50%" height="50%"/>
- Simplex(단방향 통신), Duplex(쌍방향 통신)
- Connection Oriented(TCP, 연결 후 데이터 전송) / Connectionless(UDP, 연결 없이 데이터 전송)
- LAN(Local Area Network) / WAN(wide area network)
- 연결방식 : Point to Point,Mulit-Access
- 전달방식 : 
    - Circuit Switching : 하나의 회선을 할당받아 데이터를 주고 받음, 통신이 연결되면 그 회선을 독점하여 사용하기 때문에 다른 사람들이 끼어들 수 없음, 하지만 속도와 성능을 일정하게 유지할 수 있음, 회선을 쪼개서 쓰는 방식으로 TDM(time division multitasking), FDM(frequency division multitasking) 방식이 있음
        <img src="https://user-images.githubusercontent.com/77658029/148672818-a404aff2-813f-444d-9a7b-65f92cca5383.png"  width="50%" height="50%"/>
    - Packet Switching : packet 단위로 쪼개서 전달, Packet의 header에 출발지와 목적지에 대한 정보가 있어서 전달해줌, 라우팅 알고리즘을 활용하여 경로를 설정하고 라우터들을 통해 전달이 이뤄짐, 다음 라우터로 이동하기 전에 대기(queueing)를 하는데, 이때 수용할 수 있는 큐의 범위를 초과하며 손실이 생김
        <img src="https://user-images.githubusercontent.com/77658029/148672812-6c5cd7d5-343f-47d9-b5c9-ab47ace65dd1.png"  width="50%" height="50%"/>
- Newtork Topoplogy(네트워크 토폴로지) : 망구성방식
    - Bus, Star, Ring, Hierarchical, Mesh, Hub&Spoke
        <img src="https://user-images.githubusercontent.com/77658029/148673170-eec1aa19-236f-4b2c-90e8-88c35c475cb9.png"  width="50%" height="50%"/>



**📌reference**
- [Unicast](https://ko.wikipedia.org/wiki/%EC%9C%A0%EB%8B%88%EC%BA%90%EC%8A%A4%ED%8A%B8)
- [전달방식](https://swalloow.tistory.com/55)
- [Newtork Topoplogy](https://ko.wikipedia.org/wiki/%EB%84%A4%ED%8A%B8%EC%9B%8C%ED%81%AC_%ED%86%A0%ED%8F%B4%EB%A1%9C%EC%A7%80)
<br>

```
💡 수정 필요한 내용은 댓글이나 메일로 알려주시면 감사하겠습니다!💡 
```
