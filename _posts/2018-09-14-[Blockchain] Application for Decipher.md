---
layout: post
title: "[Blockchain] Application for Decipher"
description: ""
tags: [Blockchain]
redirect_from:
  - /2018/09/14/
---

# Application for Decipher

서울대학교 블록체인 학회 [Decipher](https://medium.com/decipher-media) 2기 신입 학회원을 모집하여 지원하게 되었다. 지원서 질문과 내가 답변한 내용을 본 포스트에 정리해 보았다. 서류 전형이 완료되어 업로드하였다.

## 질문 1. 현재 블록체인이 당면한 문제 중에서 관심 있는 주제가 무엇인지, 그리고 그것이 왜 해결되어야 하는 문제인지에 대해 작성해 주세요. (예시 : 합의 알고리즘, 확장성, 오라클, 프라이버시, 거버넌스 등)

### 합의 알고리즘 (Consensus algorithm)

비트코인(Bitcoin), 이더리움(Ethereum) 등과 같은 public blockchain에서 많이 사용 중인 합의 알고리즘인 PoW(Proof of Work)는 엄청난 컴퓨팅 파워를 요구하고 있기 때문에 좋은 컴퓨팅 자원을 갖추고 있는 피어(peer)들에게 유리하여 확률적으로 부의 쏠림 현상이 발생한다. 이는 블록체인의 탈중앙화(decentralized) 철학과 배치되는 결과를 초래한다.

블록을 생성하기 위해 많은 전기량을 소모시키지만 의미없이 자원을 낭비한다는 측면도 있다. 마이닝(mining)을 통해 가치를 얻을 수 있는 마이너(miner)는 block time 당 한 개의 노드(node)만 가능하기 때문에 마이닝에 참여하는 노드수가 N일 때, N - 1개의 노드는 전기 낭비만 할 뿐 아무런 이득을 얻지 못하게 된다.

PoW 환경에서는 블록체인을 finalize하지 못한다. 동일 블록이 2개 이상 생성되어 fork가 발생했을 때 우선권을 갖는 체인(chain)에 트랜잭션(transaction)이 담기지 못했을 경우 트랜잭션은 블록에 담겼던 것이 취소가 될 수 있어 불안정성을 내포하고 있다.

### 확장성 (Scalability)

블록체인은 확장성 이슈에 직면해 있다. 초당 트랜잭션 처리량을 비교했을 때 VISA는 24,000 TPS, paypal은 193 TPS인 반면, 이더리움은 20 TPS, 비트코인은 7 TPS이다. 실제로는 더 낮은 트랜잭션 처리량을 보인다. 트래픽(traffic)이 몰릴 경우 트랜잭션이 pending된 상태를 오랜 시간 동안 유지할 수 있다. 아무리 블록체인이 안정성이 뛰어나다고 할지라도 이처럼 성능이 낮을 경우 블록체인은 상용화도 못하는 의미없는 기술이 되어 버리고 만다.

### 프라이버시 (Privacy)

비트코인과 이더리움에서 말하는 익명성은 anonymous가 아니라 pseudonymous이다. 지갑의 해시(hash) 주소를 통해 트랜잭션을 송수신하기 때문에 이 부분은 익명성을 갖지만 지갑 주인만 알아내게 된다면 익명성이 깨지게 된다. 지갑으로 어떤 트랜잭션이 오고 갔는지 모두 추적할 수 있기 때문이다. 이는 상용화를 막는 장애물이다. 실제 서비스에서는 개인정보, 계약 내용 등 공개되어서는 안되는 데이터를 활용해야 하는데 이더리움 상에서 이러한 데이터를 사용할 경우 트랜잭션을 송수신하는 과정에서 모든 사람들에게 해당 데이터가 공개될 수밖에 없다.

## 질문 2.다음의 두 질문 중 한 가지를 선택하여 서술해 주시기 바랍니다. (택 1)

1. 질문 1에서 제시한 주제를 해결하기 위한 기존의 연구나 사례가 있다면 설명해 주세요.
2. 질문 1에서 제시한 주제에 관하여 자신이 생각하는 해결책이 있다면 설명해 주세요.

### 합의 알고리즘

이더리움의 경우 PoS (Proof of Stake) 기반 합의 알고리즘으로 전환하려고 한다. Casper FFG는 이더리움 차세대 합의 알고리즘으로 블록생성은 PoW를 사용하되 validator를 두어 PoS 기반으로 checkpoint마다 검증을 통해 finalize시키는 합의 알고리즘이다. Casper FFG가 도입될 경우 블록체인을 checkpoint 마다 finalize할 수 있기 때문에 검증된 checkpoint와 그 이전 블록들에 담긴 트랜잭션들은 최종 확정성을 보장받게 된다. 그리고 검증을 위한 전기 소모량이 줄어 들어 자원 낭비를 줄일 수 있다.

### 확장성

이더리움에서는 많은 확장성 솔루션이 제안되었고 개발 중이다. 확장성 솔루션을 크게 off-chain, on-chain 솔루션으로 나눌 수 있다. off-chain 솔루션으로는 라이덴 네트워크(Raiden Network)와 플라즈마(Plasma)가 있습니다. 라이덴 네트워크는 비트코인 라이트닝 네트워크(Lightning Network)의 이더리움 버전으로 결제 채널(Payment Channel)을 연결하여 off-chain 상에서도 안전한 거래를 보장한다. 결제 채널은 거래 당사자 간에 off-chain 상에서 채널을 열고 트랜잭션을 송수신한다. 채널 상에서 전송되는 트랜잭션들은 on-chain 상에 올리지 않고 결제 채널을 열 때의 시작 트랜잭션과 결제 채널을 닫을 때의 종료 트랜잭션만 on-chain 상에 올리게 된다. 따라서 on-chain 상에 전송되는 트랜잭션 수가 감소하여 이더리움 메인넷(mainnet)의 트래픽이 줄어들게 된다.

플라즈마는 이더리움 메인넷에 사이드 체인(Side Chain)들을 트리(tree) 구조로 연결하여 부모 체인(parent chain)이 자식 체인(child chain)의 블록 헤더(block header)의 해시값을 소유하게 하여 블록체인을 관리하는 기술이다. 플라즈마 블록체인 상에 dapp (decentralized application) 등을 올린 뒤 결과 트랜잭션만 해시값을 통해 이더리움 메인넷에 보낸다면 이더리움 메인넷의 트래픽이 감소하면서 많은 트랜잭션을 처리할 수 있게 된다.

on-chain 솔루션으로는 샤딩(Sharding)이 있다. 샤딩은 shared-nothing 컨셉의 클러스터링(clustering) 기술로서 원래 데이터베이스를 분산화할 때 사용하는 기술이다. 샤드(shard) 단위로 피어들을 나누어 동일한 샤드 내에 속한 피어들끼리는 동일한 데이터를 공유, 동기화, 검증하지만 다른 샤드끼리는 다른 데이터를 가지고 있다. 데이터를 분산화하여 저장하게 된다. 샤딩을 사용하면 TPS를 높일 수 있어서 성능 향상에 도움이 된다.

그러나 public blockchain에서 확장성 솔루션을 도입하더라도 근본적인 해결책이 될 수 없다. 상용화 관점에서는 public blockchain이 비현실적으로 보이기도 한다. 따라서 Hyperledger Fabric과 같은 permissioned blockchain이 blockchain을 현실에 접목시킬 수 있는 현실적인 방안 중 하나이다. Certificate Authority를 통해 증명서를 발급받은 당사자만 네트워크에 참여할 수 있어서 네트워크 트래픽을 관리하기가 public blockchain에 비해 용이하다. 그리고 트랜잭션의 라이프사이클(life cycle)이 보통의 블록체인의 경우 order 후 execute이지만, Hyperledger Fabric의 경우 execute, order, validate라는 실행 흐름을 따르기 때문에 트랜잭션 처리 속도도 더 빠르다.

### 프라이버시

비트코인이나 이더리움과 같은 블록체인에서 공개적으로 트랜잭션이 노출되는 것을 방지하기 위한 솔루션 중에 Zcash를 참고할 수 있다. Zcash는 permissionless blockchain으로 zero knowledge 증명인 zk-SNARK을 사용하여 트랜잭션 프라이버시를 보장해 준다. Permissioned blockchain인 Hyperledger Fabric에서는 채널에 속해 있는 피어들 간에만 데이터를 공유하게 된다. 동일 채널에 속하지 않은 피어들은 다른 채널의 데이터를 알 수 없기 때문에 개인정보, 계약 정보 등과 같이 보호해야할 데이터를 안전하게 관리할 수 있다.
