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

1. */api/Create_LLM_instance*<br>
LLM대화 인스턴스 발급받기

요청시 JSON예시:

<br><br>

3. */api/Start_Conversation*<br>
LLM대화하기

<br><br>

4. */api/Update_LLM*<br>
LLM 설정변경

