# RAGAS를 활용한 문서 기반 RAG 챗봇 구축 프로젝트

## 📋 프로젝트 개요

사용자 회사에서 활용하는 업무 매뉴얼, 상담 매뉴얼은 일반적으로 FAQ 형식이 아니어서 이해하는데 많은 노력이 필요합니다. 반면 LLM (RAGAS 프레임워크)을 활용해서 생성된 FAQ 형태의 문서는 Vector Search에 용이한 구조를 가집니다.

본 프로젝트는 **RAGAS**를 활용하여 사용자의 문서를 질문/답변의 형태로 변환하고, 이를 벡터 데이터베이스에 저장하여 RAG(Retrieval-Augmented Generation) 시스템을 구성하고, 이를 통해 챗봇을 만들어 더욱 범용적인 AI 상담 애플리케이션 제작을 목적으로 합니다.

## 🎯 주요 기능

- **문서 업로드**: PDF, TXT, CSV 파일 지원
- **자동 Q&A 생성**: RAGAS를 활용한 문서 기반 질문-답변 쌍 생성
- **벡터 데이터베이스**: Chroma DB를 활용한 효율적인 검색
- **대화형 챗봇**: Gradio 기반 사용자 친화적 인터페이스

## 🏗️ 프로젝트 구조

```
homework-llm-skt/
├── data/                          # 데이터 파일들
│   ├── qa_dataset.csv            # 생성된 Q&A 데이터셋
│   ├── labor_law.pdf             # 예시 문서
│   ├── SKB_Settop_Box_User_Guide_2503.pdf
│   └── ...
├── chroma_db/                     # 벡터 데이터베이스
├── chroma_qa/                     # Q&A 벡터 저장소
├── csvsave.ipynb                  # 문서 처리 및 Q&A 생성 노트북
├── chatbot.ipynb                  # 챗봇 구현 노트북
└── README.md
```

## 🚀 사용 방법

### 1단계: 문서 업로드 및 처리 (`csvsave.ipynb`)

1. **Gradio 인터페이스 실행**
   - PDF, TXT, CSV 파일 업로드 지원
   - 문서 미리보기 기능

2. **문서 분할 및 벡터화**
   - RecursiveCharacterTextSplitter를 사용한 청크 분할
   - OpenAI Embeddings를 활용한 벡터 변환
   - Chroma DB에 저장

3. **RAGAS를 활용한 Q&A 생성**
   - 다양한 페르소나 기반 질문 생성
   - 고령 고객, 기술자 관점에서의 질문
   - 50개의 테스트셋 생성

### 2단계: 챗봇 구축 (`chatbot.ipynb`)

1. **Q&A 데이터 벡터화**
   - 생성된 CSV 파일을 벡터 데이터베이스에 저장
   - 질문과 답변을 메타데이터로 포함

2. **RAG 챗봇 구현**
   - 유사도 검색을 통한 관련 컨텍스트 검색
   - GPT-4.1-mini를 활용한 답변 생성
   - Gradio 기반 대화형 인터페이스

## 🛠️ 기술 스택

### 핵심 라이브러리
- **RAGAS**: 문서 기반 Q&A 데이터셋 생성
- **LangChain**: 문서 처리 및 RAG 파이프라인
- **Chroma**: 벡터 데이터베이스
- **Gradio**: 웹 인터페이스
- **OpenAI**: 임베딩 및 LLM

### 주요 기능
- **문서 로더**: PyPDFLoader, TextLoader, CSVLoader
- **텍스트 분할**: RecursiveCharacterTextSplitter
- **임베딩**: OpenAI text-embedding-3-small
- **LLM**: GPT-4.1-mini
- **벡터 검색**: 유사도 기반 검색

## 📊 생성된 데이터

- **문서 청크**: 472개 (SKB 세트탑 박스 사용자 가이드 기준)
- **Q&A 쌍**: 50개 (다양한 페르소나 기반)
- **벡터 저장소**: 3개 (문서, Q&A, SKB Q&A)

## 🎨 페르소나 설정

### 고령 고객 (elderly_customer)
- 기술에 대한 이해도가 낮은 일반 사용자
- 엉뚱한 질문을 많이 하는 특성
- 한국어 사용

### 기술자 (technician)
- SKB 세트탑 박스 설치 및 관리 담당
- 기능과 사용법에 대한 높은 이해도
- 한국어 사용

## 🔧 환경 설정

```bash
# 가상환경 생성 및 활성화
python -m venv .venv
source .venv/bin/activate  # macOS/Linux
# .venv\Scripts\activate   # Windows

# 의존성 설치
pip install -r requirements.txt
```

## 📝 라이선스

이 프로젝트는 교육 및 연구 목적으로 제작되었습니다.

## 🤝 기여하기

프로젝트 개선을 위한 제안이나 버그 리포트는 언제든 환영합니다!