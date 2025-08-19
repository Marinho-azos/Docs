# 🚀 Task Rate Limiter

> **Documento de Implementação**: Sistema de controle de taxa de requisições para APIs

---

## 📋 Visão Geral

Este documento detalha a implementação e configuração do sistema de rate limiting para controlar o fluxo de requisições às APIs, garantindo estabilidade e performance dos serviços. O projeto inclui verificação de configurações na GCP, revisão de variáveis de ambiente e migração para APIs corretas.

---

## 🎯 Objetivo

- Verificar se cada repositório está usando a URL correta (`api.azos.com.br`)

---

## ✅ Tarefa Principal

### 🔍 **Verificação de URLs**
- Verificar se cada repositório está usando a URL correta (`api.azos.com.br`)
- Identificar repositórios que precisam de correção
- Marcar como concluído após verificação

---

## 📊 Status dos Repositórios

### 🔴 **Pendentes de Verificação**

| Repositório | Projeto | URL Correta | Status |
|-------------|---------|-------------|---------|
| **aggregation-account** | 🟢 Account | ❌ FALSE | ⏳ ToDo |
| **bff-b2b** | 🟢 BFF | 🔍 Pendente | ⏳ ToDo |
| **aggregation-b2c-dash** | ⚪ (Sem Projeto) | 🔍 Pendente | ⏳ ToDo |
| **broker-service** | 🟢 Account | ❌ FALSE | ⏳ ToDo |
| **doc_signature_service** | ⚪ (Sem Projeto) | 🔍 Pendente | ⏳ ToDo |
| **domain-account** | 🟢 Account | ✅ TRUE | ✅ Done |
| **domain-dps-service** | 🟡 Product | 🔍 Pendente | ⏳ ToDo |
| **domain-product-settings** | 🟡 Product | 🔍 Pendente | ⏳ ToDo |
| **domain-proposal** | 🔵 Subscription | ❌ FALSE | ⏳ ToDo |
| **pdf-generator** | 🟣 CORP | ❌ FALSE | ⏳ ToDo |
| **user-status-monitor** | 🔴 Monitoring | 🔍 Pendente | ⏳ ToDo |
| **web-backoffice** | 🟣 CORP | ❌ FALSE | ⏳ ToDo |
| **web-broker-subscription** | 🔵 Subscription | ❌ FALSE | ⏳ ToDo |
| **web-file-upload** | ⚪ (Sem Projeto) | 🔍 Pendente | ⏳ ToDo |
| **webapp-payments** | 🟠 Billing | 🔍 Pendente | ⏳ ToDo |
| **widget-simulation** | 🔵 Subscription | 🔍 Pendente | ⏳ ToDo |
| **azos-cms** | 🟣 CORP | ❌ FALSE | ⏳ ToDo |
| **b2c-webapps** | 🔵 Subscription | 🔍 Pendente | ⏳ ToDo |
| **domain-user** | 🟢 Account | ❌ FALSE | ⏳ ToDo |
| **image-generator** | 🟠 Marketing | 🔍 Pendente | ⏳ ToDo |
| **mongodb_hooks** | ⚪ (Sem Projeto) | 🔍 Pendente | ⏳ ToDo |
| **business-performance-broker** | ⚪ (Sem Projeto) | 🔍 Pendente | ⏳ ToDo |

---

### ✅ **Já Verificados**

| Repositório | Status |
|-------------|--------|
| **aggregation-b2b-platform** | ✅ Done |
| **azos-bff-app-main** | ✅ Done |
| **azos-bff-b2b-main** | ✅ Done |
| **azos-bff-b2c-main** | ✅ Done |
| **azos-bff-dashboard-main** | ✅ Done |
| **aggregation-financial** | ✅ Done |
| **aggregation-campaign** | ✅ Done |
| **bff-readjustment-calculator** | ✅ Done |
| **subscription-analytics** | ✅ Done |
| **bff-widget** | ✅ Done |

---

## 🔧 Informações Técnicas

### 🌐 **URL Alvo**
- **URL Correta**: `api.azos.com.br`
- **Objetivo**: Verificar se todos os repositórios estão usando esta URL

---

## 📝 Notas Importantes

> **⚠️ Atenção**: Alguns serviços não chamam `core-url` e precisam de verificação especial.

> **🔍 Observação**: Repositórios sem projeto definido precisam de classificação adequada.

> **✅ Concluído**: `domain-account` já foi verificado e está usando a URL correta.

---

## 🏷️ Tags

`#rate-limiter` `#gcp` `#cloud-run` `#api` `#performance` `#monitoring` `#infrastructure`

---

*Documento criado para acompanhamento da implementação do Task Rate Limiter*
