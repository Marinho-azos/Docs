# Spike - Capital Limit Calculation Logic

> **Documento de Investigação Técnica**: Análise da lógica de cálculo de limite de capital para coberturas de seguro com período de vigência

---

## 📋 Descrição

Realizar uma investigação técnica detalhada sobre a função `calculate_capital_limit` no repositório CORE, focando na implementação de uma regra de validação que **libera contratação apenas para coberturas específicas** e **proíbe para todas as demais**. O objetivo é adicionar uma validação que permita contratação imediata apenas para coberturas com capital de transição (DG13, DG30, IPT, IPTA, CIR) e bloqueie para todas as outras coberturas até o final da vigência.

---

## 🎯 Contexto

A empresa de seguros enfrenta um problema crítico na validação de capital segurado máximo. Atualmente, quando um cliente solicita redução/exclusão de capital de qualquer cobertura, a contratação é liberada sem considerar o período de vigência, permitindo que o cliente contrate capital excedente ao permitido.

**Exemplos de falhas identificadas:**
- `688a899a9892d99956845b16`
- `688aa945f8a2a31016845c65`
- `6883990936fe4a474531171d`
- `6880edf7afe46a116c8d5302`
- `6880f3b5afe46a116c8d5339`
- `6848a77f7aa463c86f7b4670`

**Coberturas críticas que precisam de validação rigorosa:**
- RIT, AFF, AFI, MORTE (seguro de vida), MAC, DIH
- Estas coberturas devem aguardar o final da vigência para liberar nova contratação

**Coberturas com capital de transição (liberação imediata):**
- DG13, DG30, IPT, IPTA, CIR
- Estas podem liberar contratação imediatamente após processamento da exclusão/redução

---

## 🎯 Objetivos

- Analisar a função `calculate_capital_limit` atual e identificar onde adicionar a nova regra
- Implementar regra que **libera contratação imediata** para coberturas DG13, DG30, IPT, IPTA, CIR
- Implementar regra que **proíbe contratação** para todas as outras coberturas até final da vigência
- Identificar como validar período de vigência para coberturas bloqueadas
- Definir estrutura de dados necessária para implementação da regra de liberação/bloqueio

---

## ✅ Critérios de aceitação

- Entregar relatório técnico com análise detalhada da função atual
- Apresentar proposta de implementação com nova lógica de validação
- Documentar riscos e impactos da mudança na função existente
- Fornecer recomendação fundamentada para a equipe de desenvolvimento
- Incluir exemplos de casos de teste para validação da nova lógica

---

## 📝 Notas e resultados

### 🔧 **Análise da Função Atual**

**Localização:** Repositório CORE

**Arquivo:** `core/src/services/validate_proposal/validate_proposal.py`

**Função:** `calculate_capital_limit` (class method)

**Código atual:**
```python
@classmethod
def calculate_capital_limit(
    cls,
    code: str,
    max_capital: int,
    all_coverages: List,
) -> int:
    """calculate capital limit by checking all coverages"""
    current_insured_capital_sum = 0
    for coverage in all_coverages:
        for data in coverage["data"]:
            coverage_code = cls._get_coverage_code(data["code"])
            if code in coverage_code:
                current_insured_capital_sum += data["insured_capital"]
    if current_insured_capital_sum >= max_capital:
        return 0
    left_over = max_capital - current_insured_capital_sum
    if code == "2007":
        return cls.round_down_to_10(left_over)
    return cls.round(left_over)
```

**Limitações identificadas:**
- Não valida período de vigência das coberturas
- Libera contratação para todas as coberturas sem restrições

### 🔍 **Regra de Validação a Implementar**

#### **Coberturas com Liberação Imediata (Capital de Transição)**
- **DG13, DG30, IPT, IPTA, CIR**: Contratação liberada imediatamente após processamento da exclusão/redução
- **Lógica**: Não aguardar final da vigência, permitir contratação instantânea

#### **Coberturas com Bloqueio até Final da Vigência**
- **RIT, AFF, AFI, MORTE, MAC, DIH**: Contratação bloqueada até final da vigência da cobertura
- **Lógica**: Aguardar final da vigência para liberar nova contratação

#### **Verificações Necessárias**
- Tipo de cobertura para determinar regra aplicável
- Data de vigência das coberturas bloqueadas

#### **Estrutura de Dados Requerida**
- Informações de vigência das coberturas
- Status das propostas e apólices
- Classificação de tipos de cobertura

### 📊 **Análise de Impacto**

#### **Opção 1: Modificação da Função Existente**
- **Esforço:** Baixo
- **Risco:** Médio
- **Complexidade:** Baixa
- **Manutenibilidade:** Média

#### **Opção 2: Criação de Nova Função de Validação (recomendada)**
- **Esforço:** Baixo
- **Risco:** Médio
- **Complexidade:** Baixa
- **Manutenibilidade:** Baixa

### ⏱️ **Estimativa**

**Tempo previsto para Opção 1:** 2-3 h
**Tempo previsto para Opção 2:** 2-3 h

### 🚧 **Próximos Passos**

1. **Identificar códigos de coberturas** e.g. (RIT, AFF, AFI, MORTE, MAC, DIH)
2. **Identificar onde adicionar a regra** na função `calculate_capital_limit`
3. **Implementar validação por tipo de cobertura** (liberação vs. bloqueio)
4. **Adicionar verificação de vigência** para coberturas bloqueadas
5. **Criar casos de teste** para validar as duas regras
6. **Testar cenários** de liberação imediata e bloqueio

### ⚠️ **Riscos Identificados**

- **Alteração em função crítica** pode impactar outros módulos
- **Complexidade da lógica** de validação de vigência
- **Performance** com validações adicionais
- **Compatibilidade** com funcionalidades existentes

---

## 🏷️ Tags

`#spike` `#capital-limit` `#insurance` `#coverage-validation` `#core-repository` `#business-logic`

---

*Documento criado para investigação técnica da lógica de cálculo de limite de capital*
