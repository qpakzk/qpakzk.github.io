---
layout: post
title: "[Blockchain] Building a blockchain with Javascript : Part 2 (KR)"
description: ""
tags: [Blockchain]
redirect_from:
  - /2018/02/10/
---

# Part 2 : Implementing Proof-Of-Work(POW) in Javascript

  해당 포스트는 [Savjee youtube](https://www.youtube.com/watch?v=HneatE69814&list=PLzvRQMJ9HDiTqZmbtFisdXFxul5k0F-Q4&index=2)를 참고하여 작성하였다.

  이번 포스트에서는 consensus algorithms 중 가장 대표적인 알고리즘인 Poof-Of-Work(POW)를 구현해보도록 하겠다. 블록체인에서는 블록을 생성하기 위해 마이닝 방식을 사용하는데 마이닝 방식을 위한 알고리즘으로 POW를 사용한다.

## Poof-Of-Work

  마이닝을 위한 함수를 구현해보도록 하겠다. POW에서는 difficulty를 이용하여 블록의 해쉬값에 채워질 0을 맞추는 방식으로 마이닝이 이루어진다. 예를 들면 difficulty가 3이라면 000으로 시작하는 해쉬값을 찾게 되면 마이닝을 성공하게 된다. Block 클래스에 mineBlock 함수를 추가해보도록 하겠다.

  ```js
  mineBlock(difficulty) {
      while(this.hash.substring(0, difficulty) != Array(difficulty + 1).join("0")) {
          this.nonce++;
          this.hash = this.calculateHash();
      }

      console.log("Block mined: " + this.hash);
  }
  ```

  nonce라는 변수를 증가시키며 값을 바꿔준다. 따라서 nonce를 Block
  클래스의 멤버변수로 추가해줘야 한다.

  ```js
  constructor(index, timestamp, data, previousHash = '') {
      this.index = index;
      this.timestamp = timestamp;
      this.data = data;
      this.previousHash = previousHash;
      this.hash = this.calculateHash();
      this.nonce = 0;
  }
  ```

  mineBlock 함수 추가 후 Block 클래스의 소스코드는 다음과 같다.

  ```js
  const SHA256 = require('crypto-js/sha256');

  class Block {
      constructor(index, timestamp, data, previousHash = '') {
          this.index = index;
          this.timestamp = timestamp;
          this.data = data;
          this.previousHash = previousHash;
          this.hash = this.calculateHash();
          this.nonce = 0;
      }

      calculateHash() {
          return SHA256(this.index + this.timestamp + JSON.stringify(this.data) + this.previousHash + this.nonce).toString();
      }

      mineBlock(difficulty) {
          while(this.hash.substring(0, difficulty) != Array(difficulty + 1).join("0")) {
              this.nonce++;
              this.hash = this.calculateHash();
          }

          console.log("Block mined: " + this.hash);
      }
  }
  ```

## Mining

  Blockchain 클래스에서는 새로운 블록의 해쉬값을 계산하는 방식을 mining 방식으로 변경시켜줘야 한다.

  ```js

  addBlock(newBlock) {
      newBlock.previousHash = this.getLatestBlock().hash;
      //newBlock.hash = newBlock.calculateHash();
      newBlock.mineBlock(this.difficulty);
      this.chain.push(newBlock);
  }
  ```

  그리고 difficulty도 변수로 추가해야 한다. 추가된 Blockchain 클래스의 소스코드는 다음과 같다.

  ```js
  class Blockchain {
      constructor() {
          this.chain = [this.createGenesisBlock()];
          this.difficulty = 2;
      }

      createGenesisBlock() {
          return new Block(0, "2018/01/01", "Genesis Block", "0");
      }

      getLatestBlock() {
          return this.chain[this.chain.length - 1];
      }

      addBlock(newBlock) {
          newBlock.previousHash = this.getLatestBlock().hash;
          newBlock.mineBlock(this.difficulty);
          this.chain.push(newBlock);
      }

      isCoinValid() {

          for(let i = 1; i < this.chain.length; i++) {
              let currentBlock = this.chain[i];
              let previousBlock = this.chain[i - 1];

              if(currentBlock.hash != currentBlock.calculateHash()) {
                  return false;
              }

              if(currentBlock.previousHash != previousBlock.hash) {
                  return false;
              }
          }

          return true;
      }
  }
  ```

## Mining Test

  ```js
  let coin = new Blockchain();

  console.log("Mining block 1...");
  coin.addBlock(new Block(1, "2018/01/02", { amount: 4 }));

  console.log("Mining block 2...")
  coin.addBlock(new Block(2, "2018/01/05", { amount: 10 }));
  ```

  ![]({{ site.baseurl }}/assets/images/js-blockchain/result6.png)

## Mining Time Test

  마이닝은 difficulty에 따라 소요 시간이 다르다. 이를 테스트해보기 위해 __node-tictoc__ 패키지를 다운로드 받고 import한다.

  ```sh
  $ npm install --save node-tictoc
  ```

  ```js
  const time = require('node-tictoc');
  ```

  다음과 같은 방식으로 테스한다.

  ```js
  time.tic();
  console.log("Mining block 1...");
  coin.addBlock(new Block(1, "2018/01/02", { amount: 4 }));

  console.log("Mining block 2...")
  coin.addBlock(new Block(2, "2018/01/05", { amount: 10 }));
  time.toc();
  ```

  difficulty = 2 일 때

  ![]({{ site.baseurl }}/assets/images/js-blockchain/result7.png)

  difficulty = 3 일 때

  ![]({{ site.baseurl }}/assets/images/js-blockchain/result8.png)

  difficulty = 4 일 때

  ![]({{ site.baseurl }}/assets/images/js-blockchain/result9.png)

  difficulty = 5 일 때

  ![]({{ site.baseurl }}/assets/images/js-blockchain/result10.png)

  difficulty가 커질수록 마이닝이 오래 걸린다는 것을 알 수 있다.

  이번 포스트에서 구현한 전체 소스코드는 [여기](https://github.com/qpakzk/JS-Blockchain/blob/master/part3/main.js)에서 확인할 수 있다.
