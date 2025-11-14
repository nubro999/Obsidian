
[[Project Review]]
[[Truffle Project01]]

기술 스택
: [[Truffle]] + [[Ganache]] + Vscode

빌드 및 실행 순서

1. truffle init으로 초기화
2. truffle-config.js 에 네트워크 설정

```js
networks: {

    development: {

      host: "127.0.0.1",     // Localhost (default: none)

      port: 8545,            // Standard Ethereum port (default: none)

      network_id: "*",       // Any network (default: none)

     },
```

1. contracts에 sol파일 작성
2. ganache 실행
3. migration폴더에 js파일로 컴파일 및 deploy 함수 작성![[Pasted image 20250718155438.png]]

4. ganache에 정보 확인
5. truffle migrate 실행
6. truffle console 실행
7. let instance = await DiaryDapp.deployed(); 으로 인스턴스 할당(const도 가능)
8. await instance.writeDiary("제목", "내용", 0, Math.floor(Date.now()/1000)); 으로 값전달
9. let diary = await instance.getDiaryByMood(1); 이런 식으로 함수호출
10. diary : 값 확인

![[Pasted image 20250718154541.png]]


from값을 바꾸고 싶을 때 : await instance.writeDiary("제목", "내용", 0, Math.floor(Date.now()/1000), {from: accounts[1]});


