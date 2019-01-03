---
layout: post
title: "[Blockchain] Building a blockchain with Javascript : Part 1"
description: ""
tags: [Blockchain]
redirect_from:
  - /2018/02/10/
---

# Part 1 : Creating a blockchain with Javascript

  해당 포스트는 [Savjee youtube](https://www.youtube.com/watch?v=zVqczFZr124&index=1&list=PLzvRQMJ9HDiTqZmbtFisdXFxul5k0F-Q4)를 참고하여 작성하였다.

  Javascript로 미니 블록체인을 개발해보고자 한다. 이번 포스트에서는 가장 기본적인 간단한 블록체인을 구현한다.

## Block

  먼저 블록(Block)을 구현해보자. 블록에는 블록 번호(index), 날짜(timestamp), 데이터(data), 이전 블록 해쉬값(previousHash), 현재 블록 해쉬값(hash)이 필요하다. 블록 클래스와 생성자를 다음과 같이 구성한다.

  ```js
  class Block {
    constructor(index, timestamp, data, previousHash = '') {
        this.index = index;
        this.timestamp = timestamp;
        this.data = data;
        this.previousHash = previousHash;
        this.hash = "";
    }
  }
  ```
  해쉬값을 구하는 함수를 구현해보자. 해쉬값을 구현하기 위해서는 해쉬 함수가 필요하다. 따라서 __crypto-js__ 패키지를 다운받도록 하자.

  ```sh
  $ npm install --save crypto-js
  ```

  crypto-js의 sha256 해쉬 함수를 import한다.

  ```js
  const SHA256 = require('crypto-js/sha256');
  ```

  sha256 해쉬 함수로 블록의 해쉬값을 계산한다.

  ```js
  calculateHash() {
        return SHA256(this.index + this.timestamp + JSON.stringify(this.data) + this.previousHash).toString();
  }
  ```

  calculateHash 함수를 이용하여 생성자에서의 현재 블록 해쉬값을 구한다.

  ```js
  this.hash = this.calculateHash();
  ```

  다음은 현재까지 Block 클래스를 구현한 소스코드이다.

  ```js

  const SHA256 = require('crypto-js/sha256');

  class Block {
      constructor(index, timestamp, data, previousHash = '') {
          this.index = index;
          this.timestamp = timestamp;
          this.data = data;
          this.previousHash = previousHash;
          this.hash = this.calculateHash();
      }

      calculateHash() {
          return SHA256(this.index + this.timestamp + JSON.stringify(this.data) + this.previousHash).toString();
      }
  }
  ```

## Blockchain

  다음으로 블록"체인"을 구현해보도록 하자. 블록체인에서 시작 블록인 Genesis Block을 생성하는 함수를 구현하고 Genesis Block을 체인에 저장한다.

  ```js
  class Blockchain {
    constructor() {
        this.chain = [this.createGenesisBlock()];
    }

    createGenesisBlock() {
        return new Block(0, "2018/01/01", "Genesis Block", "0");
    }
  }
  ```

  블록체인에 가장 최근에 연결된 블록을 알려주는 함수를 구현한다.

  ```js
  getLatestBlock() {
        return this.chain[this.chain.length - 1];
  }
  ```

  블록체인에 새로운 블록을 추가하는 함수를 구현한다. 블록체인에 새로운 블록을 연결하기 위해 새로운 블록에 이전 블록의 해쉬값을 저장한다.

  ```js
  addBlock(newBlock) {
        newBlock.previousHash = this.getLatestBlock().hash;
        newBlock.hash = newBlock.calculateHash();
        this.chain.push(newBlock);
  }
  ```

  지금까지 구현한 Blockchain 클래스의 소스코드는 다음과 같다.

  ```js
  class Blockchain {
      constructor() {
          this.chain = [this.createGenesisBlock()];
      }

      createGenesisBlock() {
          return new Block(0, "2018/01/01", "Genesis Block", "0");
      }

      getLatestBlock() {
          return this.chain[this.chain.length - 1];
      }

      addBlock(newBlock) {
          newBlock.previousHash = this.getLatestBlock().hash;
          newBlock.hash = newBlock.calculateHash();
          this.chain.push(newBlock);
      }
  }
  ```

## Blockchain Test

  이제 블록체인을 생성해보는 테스트를 해보도록 하겠다.
  Genesis Block(0 번째 블록)을 생성한 후 첫 번째 블록과 두 번째 블록을 생성해보도록 하겠다.

  ```js
  let coin = new Blockchain();
  coin.addBlock(new Block(1, "2018/01/02", { amount: 4 }));
  coin.addBlock(new Block(2, "2018/01/05", { amount: 10 }));

  console.log(JSON.stringify(coin, null, 4));
  ```

  다음은 블록체인에 저장된 블록들의 데이터를 JSON 형식으로 출력한 결과이다.

  ![]({{ site.baseurl }}/assets/images/js-blockchain/result1.png)

## Validity

  블록체인에 블록들이 유효한 블록들인지 테스트해볼 필요가 있다. 따라서 유효한 블록인지 테스트하는 isCoinValid 함수를 구현한다.

  ```js
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
  ```

  isCoinValid 함수를 포함한 Blockchain 클래스 소스코드는 다음과 같다.

  ```js
  class Blockchain {
    constructor() {
        this.chain = [this.createGenesisBlock()];
    }

    createGenesisBlock() {
        return new Block(0, "2018/01/01", "Genesis Block", "0");
    }

    getLatestBlock() {
        return this.chain[this.chain.length - 1];
    }

    addBlock(newBlock) {
        newBlock.previousHash = this.getLatestBlock().hash;
        newBlock.hash = newBlock.calculateHash();
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

  isCoinValid 함수를 통해 블록의 유효성을 테스트해보자.

  ```js
  let coin = new Blockchain();
  coin.addBlock(new Block(1, "2018/01/02", { amount: 4 }));
  coin.addBlock(new Block(2, "2018/01/05", { amount: 10 }));

  console.log("Is a blockchain valid? " + coin.isCoinValid());
  ```

  올바른 블록체인이라는 결과가 나온다.

  ![]({{ site.baseurl }}/assets/images/js-blockchain/result2.png)

  첫 번째 블록의 data를 수정해보고 테스트해보도록 하자.

  ```js
  let coin = new Blockchain();
  coin.addBlock(new Block(1, "2018/01/02", { amount: 4 }));
  coin.addBlock(new Block(2, "2018/01/05", { amount: 10 }));
  console.log("Is a blockchain valid? " + coin.isCoinValid());

  coin.chain[1].data = { amount : 100 };
  console.log("Is a blockchain valid? " + coin.isCoinValid());
  ```

  올바르지 않은 블록체인이라는 결과가 나온다.

  ![]({{ site.baseurl }}/assets/images/js-blockchain/result3.png)

  만약 첫 번째 블록의 해쉬값을 다시 계산하여 저장한다면 어떤 결과가 나올까?

  ```js
  let coin = new Blockchain();
  coin.addBlock(new Block(1, "2018/01/02", { amount: 4 }));
  coin.addBlock(new Block(2, "2018/01/05", { amount: 10 }));
  console.log("Is a blockchain valid? " + coin.isCoinValid());

  coin.chain[1].data = { amount : 100 };
  coin.chain[1].hash = coin.chain[1].calculateHash();
  console.log("Is a blockchain valid? " + coin.isCoinValid());
  ```

  올바르지 않은 블록체인이라는 결과가 나온다.

  ![]({{ site.baseurl }}/assets/imagesjs-blockchain/result4.png)

  첫 번째 블록의 데이터가 수정되는 순간 다음 블록과의 관계가 깨져버려서 유효하지 않은 블록체인이 되었다. 만약에 첫 번째 블록의 데이터 수정 후에도 유효한 블록체인이 되기 위해서는 어떻게 해야 할까?

  ```js
  let coin = new Blockchain();
  coin.addBlock(new Block(1, "2018/01/02", { amount: 4 }));
  coin.addBlock(new Block(2, "2018/01/05", { amount: 10 }));
  console.log("Is a blockchain valid? " + coin.isCoinValid());

  coin.chain[1].data = { amount : 100 };
  coin.chain[1].hash = coin.chain[1].calculateHash();
  coin.chain[2].previousHash = coin.chain[1].hash;
  coin.chain[2].hash = coin.chain[2].calculateHash();
  console.log("Is a blockchain valid? " + coin.isCoinValid());
  ```

  ![]({{ site.baseurl }}/assets/images/js-blockchain/result5.png)

  두 번째 블록의 previousHash를 수정된 첫 번째 블록의 해쉬값으로 수정해줘야 하고 두 번째 블록의 previousHash가 수정되었기 때문에 두 번째 블록의 해쉬값도 다시 계산해야 한다.

   정리해보면, N 번째 블록이 가장 최근에 블록체인에 연결된 블록이라고 할 때 K(0 $$0 \leq K \leq N$$) 블록의 데이터를 수정하면 K 블록부터 N 블록까지의 해쉬값을 전부 다시 계산해야 하며 이전 블록 해쉬값을 다시 업데이트해줘야 한다. 이번 테스트를 통해 블록체인에서 데이터를 수정하는 것이 어렵다는 것을 알 수 있었다.

   이번 포스트에서 구현한 전체 소스코드는 [여기](https://github.com/qpakzk/JS-Blockchain/blob/master/part1/main.js)에서 확인할 수 있다.
