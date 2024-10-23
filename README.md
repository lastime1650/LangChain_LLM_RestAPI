# LangChain_LLM_RestAPI
LangChain기반으로 구현된 LLM기능을 RestAPI ( FastAPI )으로 사용할 수 있도록 구현하였습니다. 

---

# LLM RestAPI 무슨 일을 하는가?
이 LLM RestAPI는 랭체인의 Agent기능과 일반 대화를 수행할 수 있으며, "LLM대화 인스턴스"를 먼저 생성하였을 때, 대화 서비스가 가능합니다. 

### 1. *LLM대화 인스턴스?*<br>
이 인스턴스는 RestAPI를 통해 의사소통을 하기 전에 "/api/Create_LLM_instance" 호출해서 "Conversation_ID"를 발급받아야합니다.<br>
## "Conversation_ID"의 존재이유<br>
이 ID는 "독립적인 LLM대화세션"을 구현하기 위함입니다. 

---
# 어떤 API 호출이 가능한가?


$\color{lime}{\textsf{Request}}$ -> API요청시 JSON예시.<br>
$\color{orange}{\textsf{Response}}$ -> RestAPI의 응답 JSON<br>

1. */api/Create_LLM_instance*<br>
LLM대화 인스턴스 발급받기
- $\color{lime}{\textsf{Request}}$<br>
```json
{
    "Request_Type": "Create_Conversation", # 필수 문자열
    "Request_Data": {
        "LLM_MODEL": "Default", #또는 "gpt-4o-mini"가능. # LLM 서버에서 지원가능한 str이여야함
        "API_KEY": "xxxxxxx" # 옵션이긴한데, 사용자가 'LLM_MODEL'키의 값이 Default로 설정하지 않으면 API_KEY가 필요하니까 일단 넣는다.
    }
}
```

<br>
- $\color{orange}{\textsf{Response}}$<br>
```json
```


<br><br>

3. */api/Start_Conversation*<br>
LLM대화하기

<br><br>

4. */api/Update_LLM*<br>
LLM 설정변경

