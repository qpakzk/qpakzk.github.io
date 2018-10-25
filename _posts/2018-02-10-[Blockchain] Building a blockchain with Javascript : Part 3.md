---
layout: post
title: "[Blockchain] Building a blockchain with Javascript : Part 3 (KR)"
description: ""
tags: [Blockchain]
redirect_from:
  - /2018/02/10/
---

# Part 3 : Miner Rewards & transaction - Blockchain in Javascript

  해당 포스트는 [Savjee youtube](https://www.youtube.com/watch?v=fRV6cGXVQ4I&index=3&list=PLzvRQMJ9HDiTqZmbtFisdXFxul5k0F-Q4)를 참고하여 작성하였다.

  이번 포스트에서는 miner reward와 tranaction을 구현해보도록 하겠다.

## Transaction

  Block 클래스의 멤버 변수 data를 transaction으로 수정하고 멤버 변수 index는 불필요하므로 제거한다. Blockchain 클래스에서 Genesis Block을 생성하는 createGenesisBlock 함수에서도 멤버 변수 index에게 넘겨주는 값 0을 제거한다. 다음은 수정 후의 소스코드이다.

  ```js
  class Block {
    constructor(timestamp, transactions, previousHash = '') {
        this.timestamp = timestamp;
        this.transactions = transactions;
        this.previousHash = previousHash;
        this.hash = this.calculateHash();
        this.nonce = 0;
    }

    calculateHash() {
        return SHA256(this.timestamp + JSON.stringify(this.transactions) + this.previousHash + this.nonce).toString();
    }

    mineBlock(difficulty) {
        while(this.hash.substring(0, difficulty) != Array(difficulty + 1).join("0")) {
            this.nonce++;
            this.hash = this.calculateHash();
        }

        console.log("Block mined: " + this.hash);
    }
  }

  class Blockchain {
    constructor() {
        this.chain = [this.createGenesisBlock()];
        this.difficulty = 2;
    }

    createGenesisBlock() {
        return new Block("2018/01/01", "Genesis Block", "0");
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

  Transaction 클래스를 생성한다. Transaction 클래스에는 보내는 주소(fromAddress), 받는 주소(toAddress), 금액(amount)가 존재한다.

  ```js
  class Transaction {
    constructor(fromAddress, toAddress, amount) {
        this.fromAddress = fromAddress;
        this.toAddress = toAddress;
        this.amount = amount;
    }
  }
  ```

## Rewards

  Blockchain 클래스에서는 트랜젝션을 저장하는 pendingTransactions과 마이너에게 제공되는 보상인 miningReward가 추가된다.

  ```js
  constructor() {
    this.chain = [this.createGenesisBlock()];
    this.difficulty = 2;
    this.pendingTransactions = [];
    this.miningReward = 100;
  }
  ```

  Blockchain 클래스에서 addBlock 함수를 제거하고 minePendingTransactions 함수로 대체한다. 기존 addBlock 함수에서 체인에 블록을 추가하는 기능에 마이너에게 제공되는 초기 보상이 포함된 트랜젝션을 추가하는 기능이 추가되었다.

  ```js
  minePendingTransactions(miningRewardAddress) {
        this.pendingTransactions = [
            new Transaction(null, miningRewardAddress, this.miningReward)
        ];

        let block = new Block(Date.now(), this.pendingTransactions);
        block.mineBlock(this.difficulty);

        console.log("Block successfully mind!");
        this.chain.push(block);
  }
  ```

  Blockchain 클래스에서 트랜젝션을 추가하는 함수와 잔돈을 계산하는 함수를 구현한다.

  ```js
  createTransaction(transaction) {
      this.pendingTransactions.push(transaction);
  }

  getBalanceOfAddress(address) {
      let balance = 0;

      for(const block of this.chain) {
          for(const trans of block.transactions) {
              if(trans.fromAddress == address) {
                  balance -= trans.amount;
              }

              if(trans.toAddress == address) {
                  balance += trans.amount;
              }
          }
      }

      return balance;
  }
  ```

  지금까지 완성한 소스코드는 다음과 같다.

  ```js
  const SHA256 = require('crypto-js/sha256');

  class Transaction {
      constructor(fromAddress, toAddress, amount) {
          this.fromAddress = fromAddress;
          this.toAddress = toAddress;
          this.amount = amount;
      }
  }

  class Block {
      constructor(timestamp, transactions, previousHash = '') {
          this.timestamp = timestamp;
          this.transactions = transactions;
          this.previousHash = previousHash;
          this.hash = this.calculateHash();
          this.nonce = 0;
      }

      calculateHash() {
          return SHA256(this.timestamp + JSON.stringify(this.transactions) + this.previousHash + this.nonce).toString();
      }

      mineBlock(difficulty) {
          while(this.hash.substring(0, difficulty) != Array(difficulty + 1).join("0")) {
              this.nonce++;
              this.hash = this.calculateHash();
          }

          console.log("Block mined: " + this.hash);
      }
  }

  class Blockchain {
      constructor() {
          this.chain = [this.createGenesisBlock()];
          this.difficulty = 2;
          this.pendingTransactions = [];
          this.miningReward = 100;
      }

      createGenesisBlock() {
          return new Block("2018/01/01", "Genesis Block", "0");
      }

      getLatestBlock() {
          return this.chain[this.chain.length - 1];
      }

      minePendingTransactions(miningRewardAddress) {
        this.pendingTransactions = [
            new Transaction(null, miningRewardAddress, this.miningReward)
        ];

        let block = new Block(Date.now(), this.pendingTransactions);
        block.mineBlock(this.difficulty);

        console.log("Block successfully mind!");
        this.chain.push(block);
      }

      createTransaction(transaction) {
          this.pendingTransactions.push(transaction);
      }

      getBalanceOfAddress(address) {
          let balance = 0;

          for(const block of this.chain) {
              for(const trans of block.transactions) {
                  if(trans.fromAddress == address) {
                      balance -= trans.amount;
                  }

                  if(trans.toAddress == address) {
                      balance += trans.amount;
                  }
              }
          }

          return balance;
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

## Test

  ```js
  let coin = new Blockchain();

  console.log("\n Start the miner...");
  coin.minePendingTransactions('frodo-address');

  console.log("Balance of frodo is " + coin.getBalanceOfAddress('frodo-address'));

  console.log("\n Start the miner again...");
  coin.minePendingTransactions('frodo-address');

  console.log("Balance of frodo is " + coin.getBalanceOfAddress('frodo-address'));

  console.log("\n Start the miner again...");
  coin.minePendingTransactions('frodo-address');

  console.log("Balance of frodo is " + coin.getBalanceOfAddress('frodo-address'));

  console.log("\n Sending Transactions...");
  coin.createTransaction(new Transaction("frodo-address", "anna-address", 100));
  coin.createTransaction(new Transaction("anna-address", "bob-address", 50));

  console.log("Balance of frodo is " + coin.getBalanceOfAddress('frodo-address'));
  console.log("Balance of anna is " + coin.getBalanceOfAddress('anna-address'));
  console.log("Balance of bob is " + coin.getBalanceOfAddress('bob-address'));
  ```

  ![]({{ site.baseurl }}/assets/images/js-blockchain/result11.png)

  이번 포스트에서 구현한 전체 소스코드는 [여기](https://github.com/qpakzk/JS-Blockchain/blob/master/part3/main.js)에서 확인할 수 있다.
