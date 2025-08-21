# Spike - DPS and Lifestyle Questionnaire Improvements

> **Documento de Investigação Técnica**: Análise das melhorias na subscrição de risco para produtos com aumento do limite de capital segurado

---

## 📋 Descrição

Realizar uma investigação técnica detalhada sobre as melhorias na subscrição de risco para produtos focando no aumento do limite de capital segurado de 2M para 3M para cobertura de morte (seguro de vida). O objetivo é implementar novas regras de validação baseadas em DPS (≤2) e EV (≤2) para expandir a aceitação de clientes e aumentar a competitividade no mercado.

---

## 🎯 Contexto

A empresa de seguros precisa fazer melhorias na subscrição de risco para manter a competitividade no mercado e melhorar a experiência dos clientes. Foi aprovada uma alteração para produtos que aumenta o limite de capital segurado de 2M para 3M para cobertura de morte (seguro de vida).

**Sistema atual:**
- **build_proponent** contém informações pessoais: peso, idade, DPS, EV, status de fumante
- **max_covered_capital** DPS é calculado por pesos
- **Regra atual**: Aceita clientes com pontuação < 4
- **Limite atual**: Capital máximo de 2M

**Nova regra proposta:**
- **Limite expandido**: Capital máximo de 3M
- **Critérios de aceitação**: DPS ≤ 2 e EV ≤ 2
- **Regras adicionais**: Não fumante, até 60 anos, IMC ≤ 30 kg/m²

---

## 🎯 Objetivos

- Analisar o sistema atual de cálculo de DPS e EV no build_proponent
- Identificar onde implementar as novas regras de validação
- Definir a lógica para expansão da aceitação até pontuação 2
- Implementar validação de capital máximo baseada em DPS e EV
- Garantir que demais coberturas não sejam impactadas
- Manter compatibilidade com regras existentes de idade e faixa salarial

---

## ✅ Critérios de aceitação

- Documentar impactos na geração de propostas e cotação
- Incluir casos de teste para validação das novas regras
- Garantir que apenas cobertura de morte seja afetada

---

## 📝 Notas e resultados

### 🔧 **Análise do Sistema Atual**

**Localização:** Repositório CORE
**Arquivo:** `core/src/quoters/death_coverage` (assumindo estrutura similar)
**Funcionalidade:** Cálculo de DPS, EV e max_covered_capital

**Componentes identificados:**
- **DPS (Declaração Pessoal de Saúde)**: Sistema de pontuação por peso
- **EV (Estilo de Vida)**: Questionário de hábitos e comportamentos
- **build_proponent**: Construção da proposta com validações
- **max_covered_capital**: Cálculo do capital máximo permitido

**Regras atuais:**
- Aceita clientes com pontuação < 4
- Capital máximo limitado a 2M
- Validações de idade e faixa salarial existentes

### 🔍 **Nova Regra de Validação a Implementar**

#### **Cenário 1: DPS ≤ 2 e EV ≤ 2 (Aceitação Expandida)**
- **Capital máximo**: 3M para cobertura de morte
- **Validações adicionais**:
  - Não fumante
  - Até 60 anos
  - IMC ≤ 30 kg/m²
- **Resultado**: Geração de proposta permitida

#### **Cenário 2: DPS > 2 ou EV > 2 (Não se aplica)**
- **Capital máximo**: 2M para cobertura de morte
- **Resultado**: Não se aplica

#### **Coberturas não afetadas**
- Todas as demais coberturas mantêm regras atuais
- Apenas cobertura de morte (seguro de vida) é impactada

### 📊 **Análise de Impacto**

#### **Opção 1: Modificação da Função Existente**
- **Esforço:** Baixo
- **Risco:** Médio (mudança em lógica de validação)
- **Complexidade:** Baixa
- **Manutenibilidade:** Média

#### **Opção 2: Nova Função de Validação**
- **Esforço:** Baixo
- **Risco:** Baixo (não afeta lógica existente)
- **Complexidade:** Baixa
- **Manutenibilidade:** Alta

### ⏱️ **Estimativa**

**Tempo previsto para implementação:** 4h
**Inclui**: Desenvolvimento, testes e validação das regras

### 🚧 **Próximos Passos**

1. **Análise do código atual** de cálculo de DPS e EV
2. **Identificar onde implementar** as novas regras de validação
3. **Implementar validação de capital máximo** baseada em pontuação
4. **Adicionar validações adicionais** (fumante, idade, IMC)
5. **Criar casos de teste** para os dois cenários
6. **Validar que demais coberturas** não são impactadas

### ⚠️ **Riscos Identificados**

- **Alteração em lógica de validação** pode impactar geração de propostas
- **Complexidade das regras** de validação múltiplas
- **Performance** com validações adicionais
- **Compatibilidade** com regras existentes de idade e salário

### 📈 **Métricas de Sucesso**

- **Aumento de vendas** com capital expandido para 3M
- **Taxa de aceitação** de clientes com DPS/EV ≤ 2
- **Redução de recusas** para clientes elegíveis
- **Manutenção da qualidade** do risco aceito

---

## 🏷️ Tags

`#spike` `#dps` `#lifestyle-questionnaire` `#life-insurance` `#risk-underwriting` `#capital-limits` `#swiss` `#excelsior`

---

*Documento criado para investigação técnica das melhorias na subscrição de risco*
