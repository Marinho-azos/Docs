# 🚀 Implementação de Observabilidade via Datadog

> **Documento de Migração**: Transição da observabilidade do Sentry para o Datadog

---

## 📋 Visão Geral

Este documento detalha o processo de transição da observabilidade do **Sentry** para o **Datadog**, com o objetivo de otimizar o monitoramento e a coleta de logs em nossos sistemas. A implementação visa consolidar a responsabilidade de observabilidade na plataforma Datadog, proporcionando uma visão mais abrangente e integrada de nossos serviços.

---

## 🎯 Descrição da Task

A principal tarefa consiste em migrar a observabilidade de nossas aplicações do **Sentry** para o **Datadog**, removendo a dependência do Sentry para essa funcionalidade. Esta mudança permitirá uma centralização e padronização da coleta de dados de monitoramento, facilitando a identificação e resolução proativa de problemas.

---

## ✅ Tarefas Essenciais

Para a conclusão bem-sucedida desta iniciativa, as seguintes etapas devem ser **rigorosamente seguidas**:

### 1. 🔴 Remoção da Dependência do Sentry
- Eliminar a biblioteca `sentry-sdk` e quaisquer outras dependências relacionadas ao Sentry de todos os projetos afetados
- Esta etapa é **crucial** para garantir que a observabilidade seja completamente transferida para o Datadog

### 2. 🟢 Adição da Dependência do ddtrace
- Incorporar a biblioteca `ddtrace` (biblioteca de logs do Datadog) em todas as aplicações que necessitarão de monitoramento via Datadog

### 3. 🔄 Migração dos Logs do Sentry
- Reconfigurar a lógica de envio de logs para que, em vez de serem direcionados ao Sentry, passem a utilizar a nova biblioteca `ddtrace` para integração com o Datadog

### 4. 🔍 Verificação Abrangente de Logs
- Avaliar a necessidade de incluir outros logs existentes nos traces do Datadog para garantir uma cobertura completa da observabilidade
- Esta análise deve identificar logs que, embora não estivessem no Sentry, seriam benéficos para o monitoramento via Datadog

---

## 📊 Próximos Passos

| Projeto | Time | Status |
|---------|------|--------|
| **aggregation-account** | 🟢 ATIVAÇÃO | ⏳ ToDo |
| **bff-b2b** | 🟢 ATIVAÇÃO | ⏳ ToDo |
| **aggregation-b2c-dash** | 🟡 PÓS VENDAS | ⏳ ToDo |
| **broker-service** | 🟢 ATIVAÇÃO | ⏳ ToDo |
| **doc_signature_service** | 🟢 ATIVAÇÃO | ⏳ ToDo |
| **domain-account** | 🟢 ATIVAÇÃO | ⏳ ToDo |
| **domain-dps-service** | 🟢 ATIVAÇÃO | ⏳ ToDo |
| **domain-product-settings** | 🟢 ATIVAÇÃO | ⏳ ToDo |
| **domain-proposal** | 🟢 ATIVAÇÃO | ⏳ ToDo |
| **pdf-generator** | 🟢 ATIVAÇÃO | ⏳ ToDo |
| **user-status-monitor** | 🟢 ATIVAÇÃO | ⏳ ToDo |
| **web-backoffice** | 🟢 ATIVAÇÃO | ⏳ ToDo |
| **web-broker-subscription** | 🟢 ATIVAÇÃO | ⏳ ToDo |
| **web-file-upload** | 🟢 ATIVAÇÃO | ⏳ ToDo |
| **webapp-payments** | 🟢 ATIVAÇÃO | ⏳ ToDo |
| **widget-simulation** | 🟢 ATIVAÇÃO | ⏳ ToDo |
| **azos-cms** | 🟢🟡 ATIVAÇÃO/PÓS VENDAS | ⏳ ToDo |
| **b2c-webapps** | 🟢🟡 ATIVAÇÃO/PÓS VENDAS | ⏳ ToDo |
| **domain-user** | 🟢🟡 ATIVAÇÃO/PÓS VENDAS | ⏳ ToDo |
| **image-generator** | 🟢🟡 ATIVAÇÃO/PÓS VENDAS | ⏳ ToDo |
| **brokers_commission** | 🟡 PÓS VENDAS | ⏳ ToDo |
| **mongodb_hooks** | 🟢🟡 ATIVAÇÃO/PÓS VENDAS | ⏳ ToDo |
| **business-performance-broker** | 🟢 ATIVAÇÃO | ⏳ ToDo |
| **campaign_service** | 🟡 PÓS VENDAS | ⏳ ToDo |
| **aggregation-b2b-platform** | 🟡 PÓS VENDAS | ⏳ ToDo |
| **aggregation-campaign** | 🟡 PÓS VENDAS | ⏳ ToDo |
| **aggregation-crm-platform** | 🟡 PÓS VENDAS | ⏳ ToDo |
| **aggregation-customer-success** | 🟡 PÓS VENDAS | ⏳ ToDo |
| **aggregation-financial** | 🟡 PÓS VENDAS | ⏳ ToDo |
| **aggregation-gamefication-broker** | 🟡 PÓS VENDAS | ⏳ ToDo |
| **bff-b2c** | 🟢🟡 ATIVAÇÃO/PÓS VENDAS | ⏳ ToDo |
| **mobile-app** | 🟢🟡 ATIVAÇÃO/PÓS VENDAS | ⏳ ToDo |
| **mobile-app-broker** | 🟡 PÓS VENDAS | ⏳ ToDo |
| **bff-plataforma** | 🟡 PÓS VENDAS | ⏳ ToDo |
| **business-broker-retrospective** | 🟡 PÓS VENDAS | ⏳ ToDo |
| **business-commissions** | 🟡 PÓS VENDAS | ⏳ ToDo |
| **domain-broker** | 🟡 PÓS VENDAS | ⏳ ToDo |
| **domain-business-summary** | 🟡 PÓS VENDAS | ⏳ ToDo |
| **domain-campaign** | 🟡 PÓS VENDAS | ⏳ ToDo |
| **domain-campaign-service** | 🟡 PÓS VENDAS | ⏳ ToDo |
| **pipeline-commission** | 🟡 PÓS VENDAS | ⏳ ToDo |
| **domain-celebration-service** | 🟡 PÓS VENDAS | ⏳ ToDo |
| **domain-crm** | 🟡 PÓS VENDAS | ⏳ ToDo |
| **domain-extract-csv** | 🟡 PÓS VENDAS | ⏳ ToDo |
| **susep-broker-leads** | 🟡 PÓS VENDAS | ⏳ ToDo |
| **domain-rating** | 🟡 PÓS VENDAS | ⏳ ToDo |
| **domain-score-broker** | 🟡 PÓS VENDAS | ⏳ ToDo |
| **extract-ingestion-data** | 🟡 PÓS VENDAS | ⏳ ToDo |
| **guardian-service** | 🟡 PÓS VENDAS | ⏳ ToDo |
| **notification-center-app-b2b** | 🟡 PÓS VENDAS | ⏳ ToDo |
| **push-notification-service** | 🟡 PÓS VENDAS | ⏳ ToDo |
| **subscription-analytics** | 🟡 PÓS VENDAS | ⏳ ToDo |
| **user-dashboard-wizard** | 🟡 PÓS VENDAS | ⏳ ToDo |
| **web-plataforma** | 🟡 PÓS VENDAS | ⏳ ToDo |
| **excelsior-service** | 🟢 ATIVAÇÃO | 🔍 Review |

---

## 🔧 Compatibilidade com ddtrace

### ✅ **BIBLIOTECAS COMPATÍVEIS COM DDTRACE**

#### 🌐 **Web Framework & HTTP**
- `fastapi==0.95.2`
- `starlette==0.27.0`
- `uvicorn==0.20.0`
- `gunicorn==20.1.0`
- `h11==0.14.0`

#### 🗄️ **Database & Storage**
- `motor==3.7.0`
- `pymongo==4.11.1`

#### 🌍 **HTTP Clients & Networking**
- `requests==2.32.3`
- `httpx==0.23.3`
- `urllib3==2.3.0`
- `anyio==4.8.0`

#### ☁️ **Cloud Services & gRPC**
- `google-cloud-pubsub==2.28.0`
- `google-api-core[grpc]==2.24.1`
- `grpcio==1.70.0`
- `grpcio-status==1.70.0`
- `grpc-google-iam-v1==0.14.0`

#### 📦 **Protocol Buffers**
- `proto-plus==1.26.0`
- `protobuf==5.29.3`

---

### ❌ **BIBLIOTECAS NÃO COMPATÍVEIS COM DDTRACE**

#### 📊 **Data Processing & Validation**
- `pydantic==1.10.21`
- `python-dateutil==2.9.0.post0`
- `pytz==2024.2`

#### 🔐 **Authentication & Security**
- `google-auth==2.38.0`
- `rsa==4.9`
- `pyasn1==0.6.1`
- `pyasn1-modules==0.4.1`

#### 🛠️ **Utilities & Helpers**
- `pyyaml==6.0.2`
- `certifi==2022.12.7`
- `charset-normalizer==2.1.1`
- `idna==3.10`
- `six==1.17.0`
- `wrapt==1.17.2`

#### ⚙️ **Dependency Injection & Configuration**
- `dependency-injector[yaml]==4.45.0`

#### 🧪 **Development & Testing**
- `click==8.1.8`
- `cachetools==5.5.1`
- `importlib-metadata==8.5.0`
- `setuptools==75.8.0`
- `zipp==3.21.0`

#### ⚠️ **Observability (Conflito)**
- `opentelemetry-api==1.30.0`
- `opentelemetry-sdk==1.30.0`
- `opentelemetry-semantic-conventions==0.51b0`

---

## 📝 Notas Importantes

> **⚠️ Atenção**: Verificar possibilidade de utilizar o `patch_all` do ddtrace (auto instrumentação) para bibliotecas compatíveis.

---

## 🏷️ Tags

`#observabilidade` `#datadog` `#migração` `#sentry` `#ddtrace` `#monitoramento` `#logs`

---

*Documento criado para acompanhamento da implementação de observabilidade via Datadog*
