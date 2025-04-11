Azure Hub & Spoke 아키텍처를 활용한 Azure OpenAI Service Private Endpoint 호출 가이드 워크샵 
----------------------------------------------------------------------------

# 워크샵 개요 및 목적

본 워크샵은 Azure Hub & Spoke 네트워크 아키텍처를 기반으로, On-premise 환경에서 Azure OpenAI Service를 Private Endpoint를 통해 안전하게 호출하는 전체 과정을 단계별로 안내합니다. Azure Portal을 이용한 수동 구성 방법과 Azure CLI를 이용한 자동화 구성 방법을 병행하여 학습함으로써, Azure 네트워킹 및 서비스 구성에 대한 이해도를 높이는 것을 목표로 합니다.

### **주요 학습 내용:**

-   Azure Hub & Spoke 아키텍처 설계 및 구현
-   Site-to-Site VPN을 이용한 On-premise와 Azure 간 네트워크 연결
-   Azure Firewall을 이용한 네트워크 트래픽 제어
-   Private Endpoint를 이용한 Azure PaaS 서비스 (OpenAI, API Management) 보안 강화
-   Azure Key Vault를 이용한 비밀 관리 및 API Management 통합
-   Log Analytics를 이용한 API 요청 모니터링
-   Bastion을 이용한 안전한 VM 접속

### **워크샵 진행 방식:**

본 워크샵은 각 단계를 Azure Portal을 사용한 수동 구성과 AZ CLI를 사용한 자동 구성으로 나누어 설명합니다.

-   Portal 구성은 스크린샷을 텍스트로 대체하여 각 단계를 설명합니다.
-   AZ CLI를 사용한 구성은 모든 단계를 누락없이 자세히 설명합니다.
-   각 단계별로 jupyternotebook에서 바로 실행할 수 있도록 구성합니다.
-   quick_start/01_Secure_Network.ipynb -> hybrid network과 firewall 기반의 hub & spoke 네트워크 구성
-   quick_start/02_Secure_OpenAI.ipyng -> private endpoint기반의 apim과 azure openai 구성, 모니터링, 테스트

### **워크샵 전체 흐름:**

1.  **네트워크 인프라 구성:**
    -   On-premise VNET, Hub VNET, Spoke VNET 생성
    -   VNET Peering (Hub ↔ Spoke1, Spoke2)
    -   Site-to-Site VPN (On-premise ↔ Hub)
    -   Azure Firewall 및 라우팅 테이블 설정
2.  **Azure 서비스 구성:**
    -   Azure OpenAI Service 및 Private Endpoint 생성
    -   Azure API Management 및 Private Endpoint 생성
    -   Key Vault 생성 및 비밀 관리
    -   Private DNS Zone 생성 및 연결
    -   Log Analytics 생성 및 APIM 연동
3.  **테스트 환경 구성:**
    -   On-premise VNET에 VM 생성
    -   Bastion 생성 및 VM 연결
4.  **OpenAI API 호출 테스트:**
    -   On-premise VM에서 Private Endpoint를 통해 OpenAI API 호출

* * * *
