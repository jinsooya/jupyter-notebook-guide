# Jupyter Notebook 입문 가이드

## Jupyter Notebook이란?
코드, 텍스트, 수식, 시각화를 하나의 문서에서 실행하고 공유할 수 있는 인터랙티브 개발 환경이다.
데이터 분석, 머신러닝, AI 실습 등에서 표준 도구로 자리잡고 있다.

---

## 1. 설치 및 실행

### 설치
```bash
pip install notebook        # 클래식 Jupyter Notebook
pip install jupyterlab      # 최신 JupyterLab (권장)
```

### 실행
```bash
jupyter notebook            # 클래식 인터페이스
jupyter lab                 # JupyterLab 인터페이스
```

실행하면 브라우저가 자동으로 열리며 `http://localhost:8888`로 접속된다.

> 💡 **팁:** Google Colab을 사용하면 설치 없이 브라우저에서 바로 실행할 수 있다.

---

## 2. 인터페이스 구성

```
┌──────────────────────────────────────────┐
│  메뉴바  │  툴바  │  커널 상태            │
├──────────────────────────────────────────┤
│  [ In ]  셀 1 — 코드 입력 영역            │
│  [ Out ] 셀 1 — 실행 결과 출력            │
├──────────────────────────────────────────┤
│  [ ]     셀 2 — Markdown 텍스트           │
└──────────────────────────────────────────┘
```

노트북은 **셀(Cell)** 의 나열로 구성된다. 각 셀은 독립적으로 실행할 수 있다.

---

## 3. 셀 타입

| 타입 | 용도 | 실행 결과 |
|------|------|-----------|
| **Code** | Python 코드 작성 및 실행 | 코드 출력값 표시 |
| **Markdown** | 설명, 제목, 수식 작성 | 렌더링된 텍스트 표시 |
| **Raw** | 변환 없이 그대로 저장 | 출력 없음 |

---

## 4. 핵심 단축키

### 셀 실행

| 단축키 | 동작 |
|--------|------|
| `Shift + Enter` | 현재 셀 실행 -> 다음 셀로 이동 |
| `Ctrl + Enter` | 현재 셀 실행 (이동 없음) |
| `Alt + Enter` | 현재 셀 실행 -> 새 셀 삽입 |

### 편집 모드 vs. 명령 모드

노트북에는 두 가지 모드가 있다.

| 모드 | 진입 방법 | 셀 테두리 색 |
|------|-----------|-------------|
| **편집 모드** | `Enter` | 파란색 |
| **명령 모드** | `Esc` | 회색 |

### 명령 모드 단축키

| 단축키 | 동작 |
|--------|------|
| `A` | 위에 셀 추가 |
| `B` | 아래 셀 추가 |
| `D D` | 셀 삭제 |
| `M` | Markdown 셀로 변환 |
| `Y` | Code 셀로 변환 |
| `Z` | 셀 삭제 취소 |
| `Shift + Up/Down` | 여러 셀 선택 |

> 💡 **팁:** 단축키를 모를 때는 명령 모드에서 `H`를 누르면 전체 단축키 목록이 나온다.

---

## 5. 셀 실행 순서 주의

노트북의 가장 흔한 실수는 셀을 순서 없이 실행하는 것이다.

```python
# 셀 1
x = 10

# 셀 3 (셀 2보다 먼저 실행하면 오류)
print(x + y)   # NameError: name 'y' is not defined

# 셀 2
y = 20
```

셀 왼쪽의 `[ ]` 안 숫자가 실행 순서를 나타낸다. 번호가 뒤섞여 있으면 다시 정리가 필요하다.

---

## 6. Markdown 셀 작성법

```markdown
# 제목 1
## 제목 2
### 제목 3

**굵게**  *기울임*  `인라인 코드`

- 목록 항목 1
- 목록 항목 2

1. 순서 있는 목록

| 열1 | 열2 |
|-----|-----|
| A   | B   |

수식 (LaTeX): $E = mc^2$
블록 수식: $$\sum_{i=1}^{n} x_i$$
```

---

## 7. 패키지 설치

노트북 안에서 직접 패키지를 설치할 수 있다. 안전도 순으로 세 가지 방식이 있다.

```python
# 방법 1 — python -m pip 방식 (안전, 실용적)
!python -m pip install langchain

# 방법 2 — 완전 명시적 방식 (가장 안전)
# sys.executable로 현재 커널의 Python 경로를 직접 지정
import sys
!{sys.executable} -m pip install langchain

# 방법 3 — 간단한 방식 (편리하지만 환경 불일치 가능성 있음)
!pip install langchain
```

> ⚠️ **주의:** `!pip install`은 OS PATH의 pip을 사용하므로 현재 커널 Python과 다른 환경에 설치될 수 있다. 가상환경이 잘 정리된 경우에는 문제없지만, 방법 1~2를 기본으로 쓰는 것이 안전하다.

---

## 8. 커널(Kernel) 관리

커널은 코드를 실행하는 Python 프로세스다.

| 메뉴 / 단축키 | 동작 |
|--------------|------|
| **Kernel -> Restart** | 커널 재시작 (변수 초기화) |
| **Kernel -> Restart & Run All** | 재시작 후 전체 셀 순서대로 실행 |
| **Kernel -> Interrupt** | 실행 중인 셀 강제 중단 |
| `0 0` (명령 모드) | 커널 재시작 단축키 |

> 💡 **팁:** 제출 전에 항상 **Restart & Run All**로 전체 실행 순서를 검증한다.

---

## 9. 시각화

```python
from matplotlib import pyplot
import numpy

x = numpy.linspace(0, 2 * numpy.pi, 100)
pyplot.plot(x, numpy.sin(x))
pyplot.title('Sine Wave')
pyplot.show()
```

> 💡 **팁:** 그래프가 출력되지 않으면 셀 상단에 `%matplotlib inline`을 추가한다.

---

## 10. 매직 커맨드 (Magic Commands)

`%`로 시작하는 특수 명령어로, 셀에서 직접 실행할 수 있다.

### 자주 쓰는 라인 매직 (`%`)

```python
%timeit sum(range(1000))       # 실행 시간 측정
%who                           # 현재 정의된 변수 목록
%pwd                           # 현재 작업 디렉토리
%ls                            # 파일 목록 (Unix)
%matplotlib inline             # 그래프 인라인 출력
%load_ext autoreload           # 모듈 자동 리로드 활성화
%autoreload 2
```

### 셀 매직 (`%%`)

```python
%%time
# 셀 전체 실행 시간 측정
result = [i**2 for i in range(100000)]
```

```python
%%bash
# 셀 전체를 bash 명령으로 실행
echo "현재 경로: $(pwd)"
ls -la
```

---

## 11. 노트북 내보내기 (Export)

메뉴 **File -> Download as** 또는 커맨드라인에서 변환한다.

```bash
jupyter nbconvert --to html     notebook.ipynb
jupyter nbconvert --to pdf      notebook.ipynb
jupyter nbconvert --to script   notebook.ipynb   # .py 파일로 변환
jupyter nbconvert --to markdown notebook.ipynb
```

---

## 12. 자주 발생하는 오류

| 오류 | 원인 | 해결 방법 |
|------|------|-----------|
| `NameError` | 변수 미정의 또는 셀 미실행 | 해당 셀부터 순서대로 다시 실행 |
| `ModuleNotFoundError` | 패키지 미설치 | `!pip install <패키지명>` 후 커널 재시작 |
| `KeyboardInterrupt` | 셀 강제 중단됨 | 정상 종료 — 필요하면 다시 실행 |
| 셀이 `[*]`에서 안 끝남 | 무한루프 또는 장시간 연산 | **Kernel -> Interrupt** |
| 그래프 미출력 | `plt.show()` 누락 또는 인라인 미설정 | `%matplotlib inline` 추가 |

---

## 13. 사용 흐름 요약

```
1. jupyter lab 실행 (또는 Colab 접속)
2. 새 노트북 생성 (.ipynb)
3. 패키지 설치 셀 -> 실행
4. 코드 작성 -> Shift+Enter로 순서대로 실행
5. 오류 발생 시 -> 커널 재시작 후 전체 재실행
6. 완성 후 -> Restart & Run All 로 검증
7. 필요하면 HTML/PDF로 내보내기
```
