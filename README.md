# multiple_text_documents_chatbot 🤖

## 프로젝트 설명
**multiple_text_documents_chatbot**은 다수의 텍스트 파일을 업로드하고, 랭체인과 벡터DB(ChromaDB)를 활용하여 질의한 것에 대해 가장 유사한 문장을 찾아내고 그 문장을 바탕으로 추론 및 답변을 생성해주는 챗봇 프로젝트입니다. 
OpenAI의 GPT 모델과 ChromaDB를 결합하여 사용자의 질문에 적합한 텍스트를 추출하고, 해당 정보를 바탕으로 ChatGPT 모델을 통해 답변을 제공합니다.

<br>

## 설치 및 실행 방법
### 1. 필수 패키지 설치
다음 명령어로 필요한 라이브러리를 설치합니다:
```bash
pip install langchain openai tiktoken chromadb
```

### 2. OpenAI API Key 설정
```bash
export OPENAI_API_KEY='YOUR_OPENAI_API_KEY'
```

### 3. Flask 애플리케이션 실행
프로젝트 디렉터리에서 다음 명령어를 실행하여 챗봇을 시작합니다:
```bash
python multi_document_chatbot.py
```

### 4. 텍스트 파일 업로드 및 처리
프로젝트 디렉터리에 다수의 텍스트 파일을 업로드한 후, 각 문서를 1000글자씩 분할하고 벡터 데이터베이스(ChromaDB)에 저장한 후 질의응답 시스템을 통해 질문을 처리합니다.

<br>

## 중요 함수 및 코드 설명

### `process_llm_response`
```python
def process_llm_response(llm_response):
    print(llm_response['result'])
    print('\n\nSources:')
    for source in llm_response["source_documents"]:
        print(source.metadata['source'])
```
- LLM이 생성한 답변을 출력하고, 사용된 문서의 출처를 함께 출력하는 함수입니다.

### `qa_chain`
```python
qa_chain = RetrievalQA.from_chain_type(
    llm=OpenAI(),
    chain_type="stuff",
    retriever=retriever,
    return_source_documents=True
)
```
- OpenAI의 언어 모델을 사용하여 답변을 생성하는 Retrieval QA 객체입니다. 검색된 문서를 바탕으로 답변을 생성하고, 그 출처도 반환합니다.

<br>

## 기술 스택
- **LangChain**: 언어 모델과 벡터 검색을 결합하여 질문에 대한 답변을 생성하는 프레임워크.
- **ChromaDB**: 벡터 데이터를 저장하고 검색할 수 있는 벡터 데이터베이스.
- **OpenAI**: ChatGPT 모델을 통해 자연어 처리 및 답변 생성.
- **Tiktoken**: 토큰화 라이브러리로, 문서 텍스트를 처리하는 데 사용됩니다.
- **Flask**: 간단한 웹 애플리케이션을 구축하기 위한 마이크로 프레임워크.

<br>

## 프로젝트 참여자
- kks0507

## 코드
프로젝트 전체 코드는 GitHub에서 확인하실 수 있습니다: https://github.com/kks0507/multiple_text_documents_chatbot.git
