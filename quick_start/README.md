Azure Hub & Spoke 아키텍처를 활용한 Azure OpenAI Service Private Endpoint 호출 가이드 워크샵
----------------------------------------------------------------------------

### 소개

본 워크샵은 Azure Hub & Spoke 네트워크 아키텍처를 기반으로, On-premise 환경에서 Azure OpenAI Service를 Private Endpoint를 통해 안전하게 호출하는 전체 과정을 단계별로 안내합니다. Azure Portal을 이용한 수동 구성 방법과 Azure CLI를 이용한 자동화 구성 방법을 병행하여 학습함으로써, Azure 네트워킹 및 서비스 구성에 대한 이해도를 높이는 것을 목표로 합니다.

### 목표

-   Azure Hub & Spoke 아키텍처 설계 및 구현 능력을 향상시킵니다.
-   Site-to-Site VPN을 이용하여 On-premise와 Azure 간 네트워크 연결을 구성합니다.
-   Azure Firewall을 이용하여 네트워크 트래픽을 제어하고 보안 정책을 적용합니다.
-   Private Endpoint를 이용하여 Azure PaaS 서비스 (OpenAI, API Management)의 보안을 강화합니다.
-   Azure Key Vault를 이용하여 비밀(API 키 등)을 안전하게 관리하고, API Management와 통합합니다.
-   Log Analytics를 이용하여 API 요청을 모니터링하고 분석합니다.
-   Bastion을 이용하여 안전하게 VM에 접속하고 관리합니다.
-   Azure Portal과 Azure CLI를 모두 사용하여 리소스를 구성하는 방법을 익힙니다.

### 다루는 기술

-   **Azure Virtual Network:** Hub & Spoke 네트워크 토폴로지를 구성합니다.
-   **Site-to-Site VPN:** On-premise 네트워크와 Azure VNET 간 보안 연결을 구성합니다.
-   **Azure Firewall:** 중앙 집중식 네트워크 보안 정책을 적용하고 트래픽을 제어합니다.
-   **Azure OpenAI Service:** Private Endpoint를 통해 안전하게 OpenAI API를 호출합니다.
-   **Azure API Management:** OpenAI API 호출을 관리하고, 인증, 로깅, 모니터링 기능을 제공합니다.
-   **Azure Key Vault:** API 키와 같은 중요 정보를 안전하게 저장하고 관리합니다.
-   **Azure Log Analytics:** API 호출 로그를 수집, 분석하고 시각화합니다.
-   **Azure Bastion:** 가상 머신에 대한 안전한 RDP/SSH 연결을 제공합니다.
-   **Private DNS Zone**: Private Endpoint 사용 시 필요한 사설 DNS 레코드를 관리합니다.

### 워크샵 구성

본 워크샵은 다음 단계로 구성됩니다.

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
    -   On-premise VM에서 Private Endpoint를 통해 OpenAI API 호출 (curl 등 이용)

각 단계는 Azure Portal을 이용한 수동 구성과 Azure CLI를 이용한 자동화 구성 방법으로 상세히 설명됩니다.

### 진행 방식

-   각 단계별로 Azure Portal을 사용한 구성 방법과 Azure CLI를 사용한 구성 방법을 병행하여 설명합니다.
-   Azure Portal 구성 단계는 스크린샷을 텍스트로 대체하여 설명합니다.
-   Azure CLI 명령어는 Jupyter Notebook에서 바로 실행할 수 있도록 제공됩니다.
-   실습은 Azure 환경에서 진행되며, On-premise 환경은 Azure Virtual Machine으로 모사합니다.

### 사전 준비 사항

-   Azure 구독 (Subscription)
-   (선택 사항) Azure Portal 및 Azure CLI 사용 경험

### 참고 자료

-   [Azure Hub-Spoke 네트워크 토폴로지](https://learn.microsoft.com/ko-kr/azure/architecture/reference-architectures/hybrid-networking/hub-spoke)
-   [Azure OpenAI Service](https://learn.microsoft.com/ko-kr/azure/ai-services/openai/overview)
-   [Azure API Management](https://learn.microsoft.com/ko-kr/azure/api-management/api-management-key-concepts)
-   [Azure Key Vault](https://learn.microsoft.com/ko-kr/azure/key-vault/general/overview)
-   [Azure Log Analytics](https://learn.microsoft.com/ko-kr/azure/azure-monitor/logs/log-analytics-overview)
-   [Azure Bastion](https://learn.microsoft.com/ko-kr/azure/bastion/bastion-overview)
-   [APIM과 OpenAI 연결 및 Log Analytics 설정](https://github.com/Azure-Samples/openai-python-enterprise-logging/blob/main/README.md)
-   [vpn으로 연결되어 있는 onprem-vnet에서 private dns zone을 사용할 수 있도록 dns zone forwarder를 구성](https://learn.microsoft.com/ko-kr/azure/dns/private-resolver-hybrid-dns)

### 라이선스

MIT License