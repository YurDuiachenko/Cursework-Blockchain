# Cursework-Blockchain
## Репозиторий для курсовой работы по Блокчейну.
## Ход работы:
![image](https://github.com/YurDuiachenko/Cursework-Blockchain/assets/72216941/70dba1f3-3275-4a91-9863-355747e2dc82)
![image](https://github.com/YurDuiachenko/Cursework-Blockchain/assets/72216941/08998a53-a98b-4db5-908c-dbf6f5c0273a)
![image](https://github.com/YurDuiachenko/Cursework-Blockchain/assets/72216941/3e3e1852-0066-45e8-8a71-7765503a1dd4)
![image](https://github.com/YurDuiachenko/Cursework-Blockchain/assets/72216941/802a0afc-7515-4f5d-b8a0-617828a0a6b0)
![image](https://github.com/YurDuiachenko/Cursework-Blockchain/assets/72216941/c8958a2f-d8c6-4d25-aa8d-26d79789b029)
![image](https://github.com/YurDuiachenko/Cursework-Blockchain/assets/72216941/9a683bfb-20a9-488a-87b2-85971b0ce0f3)
![image](https://github.com/YurDuiachenko/Cursework-Blockchain/assets/72216941/19632857-d6cb-43de-a20e-98aa4c9167fe)
![image](https://github.com/YurDuiachenko/Cursework-Blockchain/assets/72216941/3f0f59f1-f3bd-400f-ad69-79b0b2dc7f81)
![image](https://github.com/YurDuiachenko/Cursework-Blockchain/assets/72216941/4151b932-e36b-4d49-a28a-2a2d143e0558)

```html
[
    {
        "index": 0,
        "previousHash": "0",
        "timestamp": 1682839690,
        "data": "RUT-MIIT first block",
        "hash": "1686576309",
        "nonce": 0
    },
    {
        "index": 1,
        "previousHash": "1686576309",
        "timestamp": 1686569967.343,
        "data": "@Yu_Dio42",
        "hash": "3464.123498497171",
        "nonce": 258
    },
    {
        "index": 2,
        "previousHash": "3464.123498497171",
        "timestamp": 1686570077.997,
        "data": "Love MIIT",
        "hash": "1234.9779000343653",
        "nonce": 492
    }
]
```
![image](https://github.com/YurDuiachenko/Cursework-Blockchain/assets/72216941/968eb9e8-7d95-440d-a2b7-bb726137bb4c)

```html
[
    {
        "index": 0,
        "previousHash": "0",
        "timestamp": 1682839690,
        "data": "RUT-MIIT first block",
        "hash": "1686576309",
        "nonce": 0
    },
    {
        "index": 1,
        "previousHash": "1686576309",
        "timestamp": 1686569967.343,
        "data": "@Yu_Dio42",
        "hash": "3464.123498497171",
        "nonce": 258
    },
    {
        "index": 2,
        "previousHash": "3464.123498497171",
        "timestamp": 1686570077.997,
        "data": "Love MIIT",
        "hash": "1234.9779000343653",
        "nonce": 492
    }
]
```
Сигнатураной хэш функцией сделал сумма косинуса и кошинуса, а условие - чтобы с хэше встречалась комбинация "1234":
```html
var mineBlock = (blockData) => {
    var previousBlock = getLatestBlock();
    var nextIndex = previousBlock.index + 1;
    var nonce = 1;
    var nextTimestamp = new Date().getTime() / 1000;
    var nextHash = calculateHash(nextIndex, previousBlock.hash, nextTimestamp, blockData, nonce);
    while (nextHash.indexOf('1234') == -1){
        nonce++;
        nextTimestamp = new Date().getTime() / 1000;
        nextHash = calculateHash(nextIndex, previousBlock.hash, 
            nextTimestamp, blockData, nonce)
            console.log("\"index\":" + nextIndex 
            +",\"previousHash\":"+previousBlock.hash
            +",\"timestamp\":"+nextTimestamp
            +",\"data\":"+blockData
            +",\x1b[33mhash: " + nextHash 
            +" \x1b[33mnonce: " + nonce + " \x1b[0m ");
        }
    return new Block(nextIndex, previousBlock.hash, nextTimestamp, blockData, nextHash, nonce);
}


var calculateHash = (index, previousHash, timestamp, data, nonce) => {
    var sum = 0;
    for(var i = 0; i < data.length; i++){
        sum += data[i].charCodeAt()+i
    }
    for(var i = 0; i < previousHash.length; i++){
        sum += previousHash[i].charCodeAt()
    }
    var input = nonce + parseInt(sum)
    return (Math.cos(parseInt(input))*(Math.round(timestamp*1000)%10000)).toString();

};

```
