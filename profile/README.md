# 🚀 Guia de Boas Práticas de Desenvolvimento - NEMPA

Bem-vindo(a) ao guia de desenvolvimento para os projetos de matemática computacional do NEMPA!

Este documento estabelece um fluxo de trabalho padrão para garantir que nossa colaboração seja organizada, eficiente e que a qualidade do nosso código seja sempre a mais alta possível. Seguir estas diretrizes é fundamental para o sucesso dos nossos projetos.

## 1. Papéis e Responsabilidades

Temos papéis bem definidos para manter a organização:

* **Project Manager (Prof. Roberto):**
    * Define o escopo e os objetivos dos projetos.
    * Cria os repositórios e a estrutura inicial.
    * Cria e prioriza as `Issues` (tarefas).
    * Realiza a revisão final e o merge de Pull Requests críticos.
    * Responsável por integrar `develop` na `main` para criar uma versão estável.

* **Maintainer(s) (Alunos mais experientes):**
    * Ajudam na revisão técnica dos Pull Requests (Code Review).
    * Orientam os novos contribuidores.
    * Podem ter permissão para fazer o merge de Pull Requests de funcionalidades na branch `develop`.

* **Contributor(s) (Todos os membros):**
    * Desenvolvem as funcionalidades e corrigem bugs.
    * São os principais criadores de branches de features e Pull Requests.
    * Participam ativamente das revisões de código dos colegas.

## 2. O Modelo de Branches: A Espinha Dorsal

Utilizamos um modelo simplificado baseado no GitFlow. Cada repositório terá **duas branches permanentes** com propósitos muito claros:

### 🌿 `main`
* **Propósito:** Versão estável e consolidada do projeto. Pense nela como a "versão de produção" ou o artigo final publicado.
* **Regras:**
    * **Ninguém** pode fazer push diretamente para a `main`.
    * Todo o código na `main` deve vir exclusivamente da branch `develop`, através de um Pull Request aprovado pelo Project Manager.

### 🔬 `develop`
* **Propósito:** Branch de integração contínua. Ela reflete o estado mais atual do desenvolvimento, contendo todas as funcionalidades já finalizadas e revisadas. É o "canteiro de obras".
* **Regras:**
    * **Ninguém** pode fazer push diretamente para a `develop`.
    * Todo código novo entra na `develop` através de um Pull Request a partir de uma branch de feature.

### ✨ `feature/<nome-da-feature>`
* **Propósito:** Branch temporária para desenvolver uma nova funcionalidade ou tarefa específica. É a sua "oficina particular".
* **Regras:**
    * Sempre criada a partir da `develop`.
    * O nome deve ser descritivo, geralmente incluindo o número da `Issue`. Ex: `feature/15-implementar-metodo-newton`.
    * Após o merge do seu Pull Request em `develop`, esta branch **deve ser deletada**.

## 3. Padrão de Commits

Para mantermos um histórico de commits limpo e legível, adotamos o padrão **Conventional Commits**. A estrutura é:

`<tipo>: <descrição>`

**Tipos mais comuns:**
* `feat`: Uma nova funcionalidade (feature).
* `fix`: Uma correção de bug.
* `docs`: Mudanças apenas na documentação (`README.md`, comentários no código).
* `style`: Mudanças de formatação que não afetam a lógica (ponto e vírgula, espaços, etc.).
* `refactor`: Refatoração de código que não corrige um bug nem adiciona uma funcionalidade.
* `test`: Adição ou correção de testes.
* `chore`: Mudanças em arquivos de build, configuração, etc. (Ex: `.gitignore`).

**Exemplos de bons commits:**
* `feat: Adiciona função para calcular o determinante de uma matriz`
* `fix: Corrige divisão por zero no método da bisseção`
* `docs: Atualiza README com instruções de instalação`
* `refactor: Simplifica o loop de renderização da cena Manim`

## 4. O Fluxo de Trabalho Completo: Passo a Passo

Vamos a um exemplo prático.

**Cenário:** Projeto `simulador-caos`. O Prof. Roberto criou a `Issue #7`: "Implementar o atrator de Lorenz". O aluno Ikaro será o responsável.

#### **Passo 1: Começando a Tarefa**

1.  **Aceite a `Issue`:** Ikaro vai até a `Issue #7` no GitHub e se atribui (`assign`) a ela, ou comenta "Estou trabalhando nisso".
2.  **Sincronize o ambiente local:** Antes de tudo, Ikaro garante que sua `develop` local está atualizada com a do repositório remoto.
    ```bash
    git checkout develop
    git pull origin develop
    ```
3.  **Crie a sua branch de feature:** A partir da `develop` atualizada, ele cria sua branch de trabalho.
    ```bash
    git checkout -b feature/7-atrator-lorenz
    ```

#### **Passo 2: Desenvolvimento e Commits**

1.  **Codifique:** Ikaro implementa o código para gerar o atrator de Lorenz.
2.  **Faça commits atômicos:** Ele faz commits pequenos e lógicos usando o padrão que definimos.
    ```bash
    git add .
    git commit -m "feat: Adiciona classe base para o atrator de Lorenz"
    # ... trabalha mais um pouco ...
    git add .
    git commit -m "feat: Implementa a integração de Runge-Kutta para as equações"
    ```
3.  **Envie para o repositório remoto:**
    ```bash
    git push origin feature/7-atrator-lorenz
    ```

#### **Passo 3: Pedindo a Integração (Pull Request)**

1.  **Abra o Pull Request (PR):** No GitHub, Ikaro abre um PR da sua branch `feature/7-atrator-lorenz` para a branch `develop`.
2.  **Preencha o template do PR:** Ele descreve o que foi feito, como testar, e o mais importante, **conecta o PR à Issue** digitando `Closes #7` no corpo da descrição.

#### **Passo 4: Revisão de Código (Code Review)**

1.  **Análise:** Enzo e Felipe são notificados. Eles analisam o código, a lógica matemática e o estilo.
2.  **Feedback:** Felipe deixa um comentário: "A constante `sigma` está com o valor `100` ao invés de `10`. Poderia corrigir?".
3.  **Ajuste:** Ikaro vê o feedback, corrige o valor na sua branch, e faz um novo commit.
    ```bash
    git add .
    git commit -m "fix: Corrige valor da constante sigma no atrator de Lorenz"
    git push origin feature/7-atrator-lorenz
    ```
    O Pull Request é atualizado automaticamente com o novo commit.

#### **Passo 5: Merge e Limpeza**

1.  **Aprovação:** O código agora está correto. Enzo e Felipe aprovam o PR.
2.  **Merge:** O Prof. Roberto (ou um Maintainer) vê as aprovações e clica no botão "Merge pull request". O código agora faz parte da `develop`. A `Issue #7` é fechada automaticamente.
3.  **Limpeza:** Após o merge, a branch `feature/7-atrator-lorenz` não é mais necessária e pode ser deletada pelo botão no GitHub ou localmente.

## 5. Estrutura e Padrões de Repositórios

Para manter a consistência entre os projetos:

1.  **`README.md` é Obrigatório:** Todo repositório **DEVE** ter um `README.md` na raiz, explicando o que o projeto faz, como instalá-lo e como usá-lo.
2.  **Roteiro para Animações Manim:** Projetos que envolvem a criação de animações com `manim` **DEVEM** incluir um arquivo `roteiro.md` na raiz. Este arquivo deve ser a "fonte da verdade" sobre o conteúdo visual e narrativo do vídeo. A versão final e aprovada do roteiro deve estar na branch `main`.
