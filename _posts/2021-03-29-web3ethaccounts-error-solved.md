---
title: "트러플 솔리디티 web3.eth.accounts 0 문제 해결 (invalid argument undefined truffle)"

categories:
  - ethereum
tags: 
  - truffle
  - Error
last_modified_at: 2021-03-29
---

블록체인 프로젝트를 진행중인데 현재 쓰는 버전에 의해 명령어가 먹히지 않아 애를 먹었다.

혹시 나같은 사람이 있을까봐 메모해둔다.

## 먼저 알아둘 점

Truffle v5.2.5 를 기준으로 한다.

Solidity 언어는 address 자료형을 지원한다.

   * uint : 부호가 없는 정수형
   * int : 정수형
   * bool : 논리 자료형
   * string : UTF-8 인코딩 문자열
   * bytes : 바이트
   * address : 이더리움 주소 값 (0xaDc7192A0…)

여기서 address 자료형을 받는 매개변수 에 대하여 web3.eth.accounts[0] 을 인자로 넘길 때 생긴 오류다.

web3.eth.accounts[0]트러플 콘솔에서 사용하여 계정 세부 정보를 얻으려고 할 때 undefined 반환하며 유효하지 못한 값으로 인식하여 에러가 났다는 것 같다.

## Solidity 코드

   ```ruby
struct Voter{
  address voterAddress;
  bool right;
}

function addVoter (address _voter) public {
  voterList[voterCount] = Voter(_voter, true);
  voterCount++;
}
   ```

## Error: invalid address

   ```ruby
truffle(development)> i.addVoter(web3.eth.accounts[0]);

Uncaught:
Error: invalid address (argument="address", value=undefined, code=INVALID_ARGUMENT, version=address/5.0.5) (argument="_voter", value=undefined, code=INVALID_ARGUMENT, version=abi/5.0.0-beta.153)
    at evalmachine.<anonymous>:0:3
    at sigintHandlersWrap (vm.js:274:15)
    at Script.runInContext (vm.js:128:14)
    at runScript (C:\Users\jee00\AppData\Roaming\npm\node_modules\truffle\build\webpack:\packages\core\lib\console.js:265:1)
    at Console.interpret (C:\Users\jee00\AppData\Roaming\npm\node_modules\truffle\build\webpack:\packages\core\lib\console.js:280:1)
    at bound (domain.js:426:14)
    at REPLServer.runBound [as eval] (domain.js:439:12)
    at REPLServer.onLine (repl.js:760:10)
    at REPLServer.emit (events.js:315:20)
    at REPLServer.EventEmitter.emit (domain.js:482:12)
    at REPLServer.Interface._onLine (readline.js:329:10)
    at REPLServer.Interface._line (readline.js:658:8)
    at REPLServer.Interface._ttyWrite (readline.js:999:14)
    at REPLServer.self._ttyWrite (repl.js:851:9)
    at ReadStream.onkeypress (readline.js:205:10)
    at ReadStream.emit (events.js:315:20)
    at ReadStream.EventEmitter.emit (domain.js:482:12)
    at emitKeys (internal/readline/utils.js:335:14)
    at emitKeys.next (<anonymous>)
    at ReadStream.onData (readline.js:1133:36) {
  reason: 'invalid address (argument="address", value=undefined, code=INVALID_ARGUMENT, version=address/5.0.5)',
  code: 'INVALID_ARGUMENT',
  argument: '_voter',
  value: undefined,
  hijackedStack: 'Error: invalid address (argument="address", value=undefined, code=INVALID_ARGUMENT, version=address/5.0.5) (argument="_voter", value=undefined, code=INVALID_ARGUMENT, version=abi/5.0.0-beta.153)\n' +
    '    at Logger.makeError (C:\\Users\\jee00\\AppData\\Roaming\\npm\\node_modules\\truffle\\build\\webpack:\\node_modules\\@ethersproject\\logger\\lib.esm\\index.js:166:1)\n' +
    '    at Logger.throwError (C:\\Users\\jee00\\AppData\\Roaming\\npm\\node_modules\\truffle\\build\\webpack:\\node_modules\\@ethersproject\\logger\\lib.esm\\index.js:175:1)\n' +
    '    at Logger.throwArgumentError (C:\\Users\\jee00\\AppData\\Roaming\\npm\\node_modules\\truffle\\build\\webpack:\\node_modules\\@ethersproject\\logger\\lib.esm\\index.js:178:1)\n' +
    '    at AddressCoder._throwError (C:\\Users\\jee00\\AppData\\Roaming\\npm\\node_modules\\truffle\\build\\webpack:\\node_modules\\@ethersproject\\abi\\lib.esm\\coders\\abstract-coder.js:38:15)\n' +
    '    at AddressCoder.encode (C:\\Users\\jee00\\AppData\\Roaming\\npm\\node_modules\\truffle\\build\\webpack:\\node_modules\\@ethersproject\\abi\\lib.esm\\coders\\address.js:14:1)\n' +
    '    at C:\\Users\\jee00\\AppData\\Roaming\\npm\\node_modules\\truffle\\build\\webpack:\\node_modules\\@ethersproject\\abi\\lib.esm\\coders\\array.js:41:1\n' +
    '    at Array.forEach (<anonymous>)\n' +
    '    at pack (C:\\Users\\jee00\\AppData\\Roaming\\npm\\node_modules\\truffle\\build\\webpack:\\node_modules\\@ethersproject\\abi\\lib.esm\\coders\\array.js:27:1)\n' +
    '    at TupleCoder.encode (C:\\Users\\jee00\\AppData\\Roaming\\npm\\node_modules\\truffle\\build\\webpack:\\node_modules\\@ethersproject\\abi\\lib.esm\\coders\\tuple.js:19:16)\n' +
    '    at AbiCoder.encode (C:\\Users\\jee00\\AppData\\Roaming\\npm\\node_modules\\truffle\\build\\webpack:\\node_modules\\@ethersproject\\abi\\lib.esm\\abi-coder.js:82:1)\n' +
    '    at ABICoder.encodeParameters (C:\\Users\\jee00\\AppData\\Roaming\\npm\\node_modules\\truffle\\build\\webpack:\\node_modules\\web3-eth-abi\\src\\index.js:145:1)\n' +
    '    at C:\\Users\\jee00\\AppData\\Roaming\\npm\\node_modules\\truffle\\build\\webpack:\\node_modules\\web3-eth\\node_modules\\web3-eth-contract\\src\\index.js:531:1\n' +
    '    at Array.map (<anonymous>)\n' +
    '    at Object._encodeMethodABI (C:\\Users\\jee00\\AppData\\Roaming\\npm\\node_modules\\truffle\\build\\webpack:\\node_modules\\web3-eth\\node_modules\\web3-eth-contract\\src\\index.js:530:10)\n' +
    '    at C:\\Users\\jee00\\AppData\\Roaming\\npm\\node_modules\\truffle\\build\\webpack:\\packages\\contract\\lib\\execute.js:181:1\n' +
    '    at processTicksAndRejections (internal/process/task_queues.js:97:5)'
}
   ```

## 해결법

   ```c
// i.addVoter(web3.eth.accounts[0]); 대신 사용

account = (await web3.eth.getAccounts())[0];
i.addVoter(account);
   ```

   ```ruby
D:\workspace\EVoting_workspace\voting>truffle console

truffle(development)> Voting.deployed().then(function(ins){i=ins;});
undefined
truffle(development)> account = (await web3.eth.getAccounts())[0];
undefined
truffle(development)> i.addVoter(account);
{
  tx: '0x951cdd1a079d33b693ea2bc96a350f8539bc10a9c36e6044f0ee60456db717d9',
  receipt: {
    transactionHash: '0x951cdd1a079d33b693ea2bc96a350f8539bc10a9c36e6044f0ee60456db717d9',
    transactionIndex: 0,
    blockHash: '0x21a9e2cdf599aead57ce87005ba137959cdb0fce53022ae5f85437069a31d71d',
    blockNumber: 5,
    from: '0xe02a119e59f4047eaffa1b9cb34822eb4ce656d9',
    to: '0xa4f79387a9dc8ed5f0761324868b1136865301fd',
    gasUsed: 67076,
    cumulativeGasUsed: 67076,
    contractAddress: null,
    logs: [],
    status: true,
    logsBloom: '0x00000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000',
    rawLogs: []
  },
  logs: []
}
truffle(development)> i.getVoter(0);
Result { '0': '0xE02a119e59f4047eAffA1B9cb34822Eb4CE656D9', '1': true }
   ```

<figure class="align-center">
  <a href="/assets/images/2021-03-29-web3ethaccounts-error-solved.PNG"><img src="/assets/images/2021-03-29-web3ethaccounts-error-solved.PNG"></a>
  <figcaption>제대로 출력된다!</figcaption>
</figure>

## 참고 사이트

[Retrieve specific account in truffle 5 console](https://ethereum.stackexchange.com/questions/64924/retrieve-specific-account-in-truffle-5-console)