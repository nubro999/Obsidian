## 1. **Keccak이란?**

- **Keccak**은 2012년에 발표된 해시 함수 패밀리입니다.
- **SHA-3** 표준의 기반이 되는 알고리즘입니다.
    - 즉, SHA-3 = Keccak의 표준화 버전입니다.
- **개발자:** Guido Bertoni, Joan Daemen, Michaël Peeters, Gilles Van Assche

---

## 2. **어디에 쓰이나요?**

- **데이터 무결성 검증** (파일 해시, 메시지 해시)
- **블록체인** (특히 이더리움에서 사용)
- **디지털 서명, 인증 등** 다양한 암호 프로토콜

---

## 3. **주요 특징**

|항목|설명|
|---|---|
|구조|Sponge construction(스펀지 구조)|
|출력 길이|가변적 (예: 224, 256, 384, 512비트 등)|
|속도|빠름|
|보안성|SHA-2와 비슷하거나 더 높음|
|표준화|Keccak → SHA-3(NIST 표준)|
|블록체인|이더리움은 Keccak-256을 기본 해시로 사용(SHA3-256과 다름)|

---

## 4. **동작 원리 (간단 설명)**

- **Sponge 구조**란?
    
    - 데이터를 “스펀지”처럼 빨아들였다가(흡수, absorb)
    - 내부 상태를 여러 번 섞은 뒤
    - 원하는 만큼 데이터를 짜내듯 출력(squeeze)하는 구조
- **Keccak의 주요 단계**
    
    1. **패딩(Padding):** 입력 메시지를 블록 단위로 맞춤
    2. **흡수(Absorb):** 메시지 블록을 내부 상태에 XOR로 합침
    3. **섞기(Permutation):** 내부 상태를 복잡하게 섞음
    4. **짜내기(Squeeze):** 해시 결과를 출력

---

## 5. **Keccak vs SHA-3 vs SHA-2**

- **Keccak**: 원본 알고리즘 이름 (NIST 표준화 전)
- **SHA-3**: Keccak을 바탕으로 NIST가 약간 수정해 표준화한 것 (2015년)
- **SHA-2**: 이전 세대 해시(SHA-256, SHA-512 등), 구조가 다름(Merkle–Damgård)

> **이더리움**은 Keccak-256(원본 Keccak)을 사용하며,  
> Python의 `hashlib.sha3_256()`은 표준 SHA-3-256(약간 다름)을 사용합니다.  
> (즉, 해시값이 다를 수 있으니 주의!)

---

## 6. **코드 예시 (Python)**

- **Keccak-256 (이더리움과 동일) 사용 예시:**

복사

`from Crypto.Hash import keccak  k = keccak.new(digest_bits=256) k.update(b"hello") print(k.hexdigest())`

- **SHA-3-256 (표준):**

복사

`import hashlib  h = hashlib.sha3_256() h.update(b"hello") print(h.hexdigest())`

---

## 7. **정리**

|구분|설명|
|---|---|
|Keccak|SHA-3 표준의 기반, Sponge 구조, 빠르고 안전|
|SHA-3|Keccak을 표준화한 것, 약간의 내부 파라미터 차이|
|이더리움|Keccak-256 사용 (SHA3-256과 해시값 다름)|
|용도|무결성, 블록체인, 디지털 서명, 인증 등|