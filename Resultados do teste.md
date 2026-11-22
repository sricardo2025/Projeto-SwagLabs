# 📋 Relatório de Resultados de Teste

---

## 📌 Informações Gerais

| Campo                    | Detalhe                                    |
| ------------------------ | ------------------------------------------ |
| **Projeto:**             | Swag Labes                                 |
| **Módulo/Sistema:**      | Carrinho de vendas                         |
| **Versão:**              | 1.0                                        |
| **Período de Execução:** | [20/11/2026] a [21/11/2026]                |
| **Ambiente de Teste:**   | ☐ Desenvolvimento ☐ Homologação ☑ Produção |
| **Responsável:**         | Sergio Ricardo                             |
| **Data do Relatório:**   | 21/11/2026                                 |

---

## 📊 Resumo Executivo

> **Objetivo:** Validar logins, checkout e estabilidade do site.

| Status                          | Quantidade | Porcentagem |
| ------------------------------- | ---------- | ----------- |
| ✅ **Aprovados**                | 26         | 92,5%       |
| ❌ **Falhados**                 | 2          | 7,1%        |
| ⏳ **Em Análise**               | 1          | 3,5%        |
| ⏭️ **Ignorados/Não Executados** | 0          | 0%          |
| **Total**                       | **28**     | **100%**    |

> **Status Geral:** 🟢 **Aprovado** | 🟡 **Parcialmente Aprovado** | 🔴 **Não Aprovado**
>
> **Comentário:** O sistema está pronto para liberação com 2 ajustes pendentes e análise de um erro fora do escopo.

---

## 🐛 Lista de Defeitos Encontrados

Tabela

| ID Defeito | Título do Problema                                                                       | Severidade | Situação                       | Prioridade |
| ---------- | ---------------------------------------------------------------------------------------- | ---------- | ------------------------------ | ---------- |
| BUG-001    | Mesmo logando em várias contas, carrinho continua com produtos dentro.                   | 🔴 Crítica | ☐ Aberto ☐ Resolvido ☐ Fechado | Urgente    |
| BUG-001    | Teste CT-18 pagina deslogou na 1 tentativa.                                              | 🔴 Crítica | ☐ Aberto ☐ Resolvido ☐ Fechado | Urgente    |
| BUG-002    | Na página de carrinho não consta botão para adicionar maior quantidade do mesmo produto. | 🟡 Média   | ☐ Aberto ☐ Resolvido ☐ Fechado | Alta       |

---

## ✅ Itens Verificados

- Funcionalidades principais
- Fluxos críticos de negócio
- Validações de campos e regras
- Performance/resposta dentro do esperado
- Compatibilidade — Navegadores e windonws 10

---

## ⚠️ Riscos e Pendências

- **Pendência 1:** Adicionar contador de adição de mesmo item
- **Risco:** Carrinho não deleta item colocados em um usuiário após outro login feito.
- **Ação sugerida:** Rever código da pagina do carrinho.

---

## 📝 Conclusão e Recomendação

> **Conclusão:** Dos 28 cenários testados, 26 passaram com sucesso. Os 2 defeitos encontrados não bloqueiam o uso principal, mas devem ser corrigidos na próxima versão.
>
> **Recomendação:** ❌ Aguardar correções

---

<br>
<br>
<br>

**Assinatura/Responsável:** ****\*\*\*\*****\_****\*\*\*\***** | **Data:** \_**\_ /\_\_\_** /**\_\_**

<style>
  body, p, h1, h2, h3, h4, h5, h6, li, td, th {
    font-family: 'albert sans', sans-serif !important;
  }
</style>
