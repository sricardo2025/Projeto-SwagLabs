# Plano de Teste manual — SauceDemo (Swag Labs)

**Testador**: Sergio Ricardo <br>
**Plataforma**: windowns 10 <br>
**Navegador**: Brave atualizado

> **Versão:** 1.0 <br>
> **Data:** 20/11/2026 <br>
> **Ambiente de Teste:** [https://www.saucedemo.com](https://www.saucedemo.com)

---

## 🎯 1. Escopo do Teste

### ✅ Dentro do Escopo

| Módulo                                  | Funcionalidades                                                                                           |
| --------------------------------------- | --------------------------------------------------------------------------------------------------------- |
| **Login / Autenticação**                | Login com usuários válidos, usuário bloqueado, credenciais inválidas, campos vazios                       |
| **Catálogo de Produtos**                | Visualização da lista, contagem de itens, ordenação (A-Z, Z-A, preço crescente/decrescente)               |
| **Carrinho de Compras**                 | Adicionar itens, remover itens, contador do carrinho, persistência entre páginas                          |
| **Checkout / Compra**                   | Formulário de dados do cliente, validação de campos obrigatórios, resumo do pedido, finalização da compra |
| **Navegação e Logout**                  | Menu lateral, navegação entre páginas, encerramento de sessão, proteção de rotas após logout              |
| **Comportamento por perfil de usuário** | Validação com todos os 6 perfis disponíveis                                                               |

### ❌ Fora do Escopo

- Testes de API / backend
- Testes de performance e carga
- Testes de segurança (injeção, vulnerabilidades)
- Responsividade em dispositivos móveis
- Testes de acessibilidade

---

## 👤 2. Perfis de Usuário Disponíveis

| Usuário                   | Comportamento esperado                                         |
| ------------------------- | -------------------------------------------------------------- |
| `standard_user`           | Funcionamento normal — usuário principal de teste              |
| `locked_out_user`         | Conta bloqueada — não permite login                            |
| `problem_user`            | Apresenta problemas de funcionalidade (imagens, botões, links) |
| `performance_glitch_user` | Resposta lenta / atrasos no carregamento                       |
| `error_user`              | Erros em operações de formulário                               |
| `visual_user`             | Problemas de layout e elementos visuais                        |
| **Senha para todos:**     | `secret_sauce`                                                 |

---

## ⚠️ 3. Riscos e Mitigações

| #    | Risco                                                                                              | Impacto | Probabilidade | Mitigação                                                                      |
| ---- | -------------------------------------------------------------------------------------------------- | ------- | ------------- | ------------------------------------------------------------------------------ |
| R-01 | Ambiente externo pode estar instável ou indisponível                                               | Alto    | Baixo         | Verificar disponibilidade antes de iniciar; manter página de referência salva  |
| R-02 | Comportamento diferente entre navegadores                                                          | Médio   | Médio         | Definir navegador padrão (Chrome); registrar navegador utilizado em cada teste |
| R-03 | Dados de produto/preço podem ser alterados no ambiente remoto                                      | Médio   | Baixo         | Capturar valores como referência no início da execução                         |
| R-04 | `problem_user` e `performance_glitch_user` apresentam falhas conhecidas — não são bugs do ambiente | Baixo   | Certo         | Documentar comportamento esperado para cada perfil; não registrar como defeito |

---

## 📥 4. Critérios de Entrada

Antes de iniciar os testes, devem estar satisfeitos os requisitos abaixo:

- ✅ Acesso à internet e navegador atualizado (Chrome recomendado)
- ✅ Site **[https://www.saucedemo.com](https://www.saucedemo.com)** está acessível e carregando corretamente
- ✅ Lista de usuários e senha confirmada e disponível
- ✅ Acesso a ferramentas para registro de evidências (prints, planilha ou ferramenta de gestão de testes)
- ✅ Ambiente livre de interrupções para a execução

## 📤 Critérios de Saída

O ciclo de teste será considerado concluído quando:

- ✅ 100% dos casos de teste planejados forem executados
- ✅ Resultados registrados (Passou / Falhou / Bloqueado)
- ✅ Defeitos encontrados devidamente documentados com passos de reprodução e evidências
- ✅ Relatório final consolidado com taxa de aprovação e observações por perfil de usuário
- ✅ Funcionalidades críticas (login, fluxo completo de compra) validadas com `standard_user`

---

## 📝 5. Casos de Teste

### 🟦 S01 — Login e Autenticação

| ID         | Caso de Teste                 | Precondições                                                   | Passos                                                                   | Resultado Esperado                                                                     |
| ---------- | ----------------------------- | -------------------------------------------------------------- | ------------------------------------------------------------------------ | -------------------------------------------------------------------------------------- |
| **TC-001** | Login com credenciais válidas | Acessar [https://www.saucedemo.com](https://www.saucedemo.com) | 1. Usuário: `standard_user`2. Senha: `secret_sauce`3. Clicar em Login    | ✅ Acesso concedido → redireciona para página de inventário                            |
| **TC-002** | Login com usuário bloqueado   | Página de login aberta                                         | 1. Usuário: `locked_out_user`2. Senha: `secret_sauce`3. Clicar em Login  | ❌ Erro: _"Epic sadface: Sorry, this user has been locked out."_                       |
| **TC-003** | Login com usuário inexistente | Página de login aberta                                         | 1. Usuário: `usuario_invalido`2. Senha: `secret_sauce`3. Clicar em Login | ❌ Erro: _"Epic sadface: Username and password do not match any user in this service"_ |
| **TC-004** | Campo usuário vazio           | Página de login aberta                                         | 1. Manter usuário em branco2. Senha: `secret_sauce`3. Clicar em Login    | ❌ Erro: _"Epic sadface: Username is required"_                                        |
| **TC-005** | Campo senha vazio             | Página de login aberta                                         | 1. Usuário: `standard_user`2. Senha em branco3. Clicar em Login          | ❌ Erro: _"Epic sadface: Password is required"_                                        |

### 🟩 S02 — Catálogo de Produtos

| ID         | Caso de Teste                     | Precondições                        | Passos                                                      | Resultado Esperado                                           |
| ---------- | --------------------------------- | ----------------------------------- | ----------------------------------------------------------- | ------------------------------------------------------------ |
| **TC-006** | Visualização da lista de produtos | Login com `standard_user` realizado | 1. Verificar página de inventário                           | ✅ Exibir **6 produtos** com nome, descrição, preço e imagem |
| **TC-007** | Ordenação por Nome (A-Z)          | Lista de produtos visível           | 1. Clicar no menu de ordenação2. Selecionar "Name (A to Z)" | ✅ Produtos ordenados alfabeticamente crescente              |
| **TC-008** | Ordenação por Nome (Z-A)          | Lista de produtos visível           | 1. Selecionar "Name (Z to A)"                               | ✅ Produtos ordenados alfabeticamente decrescente            |
| **TC-009** | Ordenação por Preço — Crescente   | Lista de produtos visível           | 1. Selecionar "Price (low to high)"                         | ✅ Produtos do menor para o maior preço                      |
| **TC-010** | Ordenação por Preço — Decrescente | Lista de produtos visível           | 1. Selecionar "Price (high to low)"                         | ✅ Produtos do maior para o menor preço                      |

### 🟨 S03 — Carrinho de Compras

| ID         | Caso de Teste              | Precondições       | Passos                                              | Resultado Esperado                                                                 |
| ---------- | -------------------------- | ------------------ | --------------------------------------------------- | ---------------------------------------------------------------------------------- |
| **TC-011** | Adicionar item ao carrinho | Produtos visíveis  | 1. Clicar em "Add to cart" em um produto            | ✅ Botão muda para "Remove"✅ Ícone do carrinho mostra **1** item                  |
| **TC-012** | Remover item do carrinho   | Item já adicionado | 1. Clicar em "Remove"                               | ✅ Botão volta para "Add to cart"✅ Contador do carrinho é zerado                  |
| **TC-013** | Adicionar múltiplos itens  | Produtos visíveis  | 1. Adicionar 2 ou mais produtos                     | ✅ Contador mostra quantidade correta✅ Todos itens aparecem na página do carrinho |
| **TC-014** | Persistência do carrinho   | Itens adicionados  | 1. Navegar entre Inventário → Carrinho → Inventário | ✅ Itens permanecem no carrinho ao retornar                                        |

### 🟧 S04 — Fluxo de Checkout

| ID         | Caso de Teste                       | Precondições                               | Passos                                                                                            | Resultado Esperado                                                      |
| ---------- | ----------------------------------- | ------------------------------------------ | ------------------------------------------------------------------------------------------------- | ----------------------------------------------------------------------- |
| **TC-015** | Acessar carrinho e iniciar checkout | Pelo menos 1 item no carrinho              | 1. Clicar no ícone do carrinho2. Clicar em "Checkout"                                             | ✅ Formulário de dados do cliente é exibido                             |
| **TC-016** | Continuar sem preencher dados       | Página "Checkout: Your Information" aberta | 1. Clicar em "Continue" sem preencher                                                             | ❌ Erro: Campo obrigatório (First Name)                                 |
| **TC-017** | Continuar com dados incompletos     | Formulário aberto                          | 1. Preencher: Nome e Sobrenome2. Deixar CEP vazio3. Clicar em "Continue"                          | ❌ Erro: Postal Code é obrigatório                                      |
| **TC-018** | Informações válidas de entrega      | Formulário aberto                          | 1. First Name: `Maria`2. Last Name: `Silva`3. Zip/Postal Code: `58000-000`4. Clicar em "Continue" | ✅ Avança para página de resumo do pedido                               |
| **TC-019** | Resumo do pedido — valores corretos | Página de resumo aberta                    | 1. Verificar Subtotal, Imposto e Total                                                            | ✅ Subtotal = soma dos preços✅ Imposto e Total calculados corretamente |
| **TC-020** | Finalizar compra com sucesso        | Resumo do pedido visível                   | 1. Clicar em "Finish"                                                                             | ✅ Mensagem: *"Thank you for your order!"*✅ Número do pedido gerado    |
| **TC-021** | Cancelar compra durante o fluxo     | No passo de dados ou resumo                | 1. Clicar em "Cancel"                                                                             | ✅ Retorna para página de inventário sem concluir compra                |

### 🟪 S05 — Navegação e Logout

| ID         | Caso de Teste                             | Precondições     | Passos                                                             | Resultado Esperado                                                   |
| ---------- | ----------------------------------------- | ---------------- | ------------------------------------------------------------------ | -------------------------------------------------------------------- |
| **TC-022** | Realizar Logout                           | Usuário logado   | 1. Clicar no menu superior esquerdo2. Selecionar "Logout"          | ✅ Retorna para página de login                                      |
| **TC-023** | Acesso direto a rota protegida sem sessão | Sessão encerrada | 1. Digitar diretamente: `https://www.saucedemo.com/inventory.html` | ✅ Redireciona para login com mensagem de sessão expirada            |
| **TC-024** | Voltar no navegador após logout           | Logout realizado | 1. Clicar no botão ← do navegador                                  | ✅ Não deve retornar à página interna — permanece na página de login |

### 🟫 S06 — Comportamento de Perfis Alternativos

| ID         | Caso de Teste                                 | Precondições            | Passos                              | Resultado Esperado                                                                         |
| ---------- | --------------------------------------------- | ----------------------- | ----------------------------------- | ------------------------------------------------------------------------------------------ |
| **TC-025** | `problem_user` — comportamento conhecido      | Página de login         | Login com `problem_user`            | ✅ Login realizado, mas esperar anomalias conhecidas (imagens quebradas, botões com falha) |
| **TC-026** | `performance_glitch_user` — tempo de resposta | Página de login         | Login com `performance_glitch_user` | ✅ Login realizado, porém com tempo de resposta aumentado                                  |
| **TC-027** | `error_user` — operações de formulário        | Login com `error_user`  | Tentar fluxo completo de checkout   | ✅ Esperar erros em validações e salvamento de dados                                       |
| **TC-028** | `visual_user` — elementos visuais             | Login com `visual_user` | Navegar pelas páginas               | ✅ Esperar desalinhamentos e problemas de exibição                                         |

---

## 📊 6. Critérios de Avaliação

- **Sucesso:** Funcionalidades críticas (login, fluxo completo de compra) passam 100% com `standard_user`
- **Aceitável:** ≥ 90% dos casos de teste aprovados; defeitos registrados e classificados por severidade
- **Bloqueante:** Falha no login ou impossibilidade de concluir fluxo completo com usuário padrão

<style>
  body, p, h1, h2, h3, h4, h5, h6, li, td, th {
    font-family: 'albert sans', sans-serif !important;
  }
</style>
