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

- $\color{orange}{\textsf{Response}}$

```json
{
}
```

$\color{lime}{\textsf{Request}}$ -> API요청시 JSON예시.<br>
$\color{orange}{\textsf{Response}}$ -> RestAPI의 응답 JSON<br>

## 1. */api/Create_LLM_instance*<br>
LLM대화 인스턴스 발급받기<br>
$\color{magenta}{\textsf{인스턴스 생성 시, "Agent체인"와 "일반 대화 체인" LLM이 한번에 생성됩니다.}}$
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
- $\color{orange}{\textsf{Response}}$

```json
# 성공 시
{
    "status": "success",
    "message": "성공적으로 LLM대화 인스턴스 생성되었습니다."
    "Response_Data": {
        "Conversation_ID": "zxczxczxc..." # 핵심
    }
}

# 실패 시
{
    "status": "fail",
    "message": "인스턴스 생성 실패" # 또는 "잘못된 입력입니다. 정보를 다시 입력해주세요"
    "Response_Data": null
}
```

<br><br>

## 2. */api/Update_LLM*<br>
LLM 설정변경 ( 프롬프트 변경 )<br>
$\color{magenta}{\textsf{"일반 대화": system프롬프트 변경가능(덮어쓰기).}}$<br>
$\color{magenta}{\textsf{"Agent": 함수 호출방식 추가가능.}}$
- $\color{lime}{\textsf{Request}}$

```json
# 일반 대화용 
{
    "Request_Data": {
        "Conversation_Type": "Default", # Default는 "일반 대화"
        "Conversation_ID": "zxczxczxc...",
        "Update_Data": {
            "System_Message": "당신은 훌륭한 챗봇입니다." # 중요
        }
    }
}


# Agent 대화용
{
    "Request_Data": {
        "Conversation_Type": "Agent",
        "Conversation_ID": "ConversationID",  // 실제 ConversationID 값을 대체해야 함
        "Update_Data": {
            "Add_Tool": [
                {
                    "Tool_Name": "Agent_Tool_name",  // 고유하게 함수를 식별하기 위한 Tool 이름 문자열
                    "Tool_Prompt": "..." //이 부분은 꽤나 복잡함.
                }
            ]
        }
    }
}


```

- $\color{orange}{\textsf{Response}}$

```json
# 성공 시
{
    "status": "success",
    "message": "성공적으로 LLM업데이트 요청되었습니다."
    "Response_Data": {
        "Update_status":"success"
    }
}

# 실패 시
{
    "status": "fail",
    "message": "잘못된 입력입니다. 정보를 다시 입력해주세요"
    "Response_Data": null
}
```

<br><br>

## 3. */api/Start_Conversation*<br>
LLM대화하기
- $\color{lime}{\textsf{Request}}$

```json
# 일반 대화용
{
    "Request_Data": {
        "Conversation_Type": "Default", # 무조건 일반 대화형임
        "Conversation_ID": "zxczxczxc...",
        "Input_Text": 안녕하세요~ 넌 누구니?
    }
}

# Agent 대화용
{
    "Request_Data": {
        "Conversation_Type": "Agent", # 무조건 일반 대화형임
        "Conversation_ID": "zxczxczxc...",
        "Input_Text": 안녕하세요~ 웹페이지를 이동해주세요
    }
}
```

- $\color{orange}{\textsf{Response}}$

```json
{
}
```


