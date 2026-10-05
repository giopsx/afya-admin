# Afya Admin — Dashboard com Blazor WebAssembly e MudBlazor

## Identificação

> ⚠️ **PREENCHER** — substitua cada campo abaixo pelos seus dados.

| | |
|---|---|
| **Aluno(a)** | *(seu nome completo)* |
| **Matrícula** | *(sua matrícula)* |
| **Faculdade** | *(nome da faculdade)* |
| **Curso** | *(nome do curso)* |
| **Disciplina** | *(nome da disciplina)* |
| **Professor(a)** | *(nome do professor)* |
| **Semestre** | 2026.2 |

## Objetivo do projeto

> ⚠️ **ESCREVER COM SUAS PALAVRAS** (2 a 4 parágrafos).
>
> Pontos que você pode usar como roteiro:
> - o que é o painel "Afya Pedagógico" e o que a página Dashboard mostra;
> - por que o projeto é um Blazor WebAssembly autônomo (não há backend; os dados são fictícios);
> - qual foi a restrição central do trabalho (nenhum CSS próprio) e o que ela obrigou a aprender;
> - como a página foi dividida em componentes em vez de um arquivo único.

## Tecnologias utilizadas

- .NET 10 / Blazor WebAssembly autônomo (standalone)
- MudBlazor 9 (componentes, tema e classes utilitárias)
- Template `mudblazorwasm` (pacote `MudBlazor.Templates`)
- Fonte Inter (Google Fonts)
- Git / GitHub

## Como executar

Pré-requisito: **.NET SDK 10** (verifique com `dotnet --version`, deve começar com `10.`).

Na primeira vez, instale os templates do MudBlazor:

```bash
dotnet new install MudBlazor.Templates
```

Depois, clone e execute:

```bash
git clone https://github.com/SEU-USUARIO/afya-admin.git
cd afya-admin
dotnet watch
```

A aplicação abre em `http://localhost:5074` (a porta está em `Properties/launchSettings.json`).

## Telas

### Tema claro
![Dashboard — tema claro](docs/prints/tema-claro.png)

### Tema escuro
![Dashboard — tema escuro](docs/prints/tema-escuro.png)

### Versão mobile
![Dashboard — celular](docs/prints/mobile.png)

No celular os KPIs ficam em uma coluna, o sidebar vira gaveta, a busca e o bloco de nome/e-mail
do usuário são ocultados, e a tabela de Projetos Recentes deixa de ser tabela e vira uma lista de
cards, com cada célula rotulada pelo `DataLabel`.

### HTML gerado (DevTools)

> ⚠️ **PRINT PENDENTE** — este é o único print que falta. Veja "Como tirar este print" logo abaixo.

![Inspeção do HTML no DevTools](docs/prints/devtools.png)

> ⚠️ **ESCREVER COM SUAS PALAVRAS**: explique em poucas linhas qual componente você inspecionou,
> qual HTML ele gerou e quais classes apareceram.
>
> O arquivo [`docs/html-gerado.md`](docs/html-gerado.md) tem o HTML real já extraído da aplicação
> (card de KPI, `MudStack`, `MudAvatar` e `MudButton`) para você conferir enquanto escreve.

**Como tirar este print:** rode `dotnet watch`, abra a página no Chrome ou Edge, pressione `F12`,
vá na aba **Elements**, clique no ícone de seleção (seta no canto superior esquerdo do DevTools) e
clique sobre o card "Receita". Deixe o painel Elements e o painel Styles visíveis e capture a tela
inteira. Salve como `docs/prints/devtools.png`.

## Estrutura do projeto

```
afya-admin/
├── Components/                        componentes visuais reutilizáveis do dashboard
│   ├── AtividadesRecentes.razor
│   ├── CabecalhoPagina.razor
│   ├── DashboardCard.razor
│   ├── GraficoDistribuicaoClientes.razor
│   ├── GraficoReceita.razor
│   ├── KpiCard.razor
│   ├── PerformanceProjetos.razor
│   ├── ProjetosRecentes.razor
│   ├── SeletorPeriodo.razor
│   └── Ui.cs                          funções auxiliares de apresentação
├── Data/
│   └── DashboardData.cs               modelos (records) e dados fictícios
├── Layout/
│   ├── MainLayout.razor               moldura da aplicação: tema, AppBar e sidebar
│   └── NavMenu.razor                  links do menu lateral
├── Pages/
│   ├── Dashboard.razor                página "/" — só monta os componentes
│   └── NotFound.razor                 página 404
├── Properties/
│   └── launchSettings.json            perfis de execução e porta
├── wwwroot/                           arquivos estáticos servidos ao navegador
│   ├── css/app.css                    CSS do template (não modificado)
│   ├── img/alex-morgan.jpg            foto fictícia do usuário
│   └── index.html                     a única página HTML real da aplicação
├── docs/
│   ├── html-gerado.md                 HTML gerado pelos componentes (apoio ao print do DevTools)
│   └── prints/                        imagens usadas neste README
├── App.razor                          roteador
├── Program.cs                         ponto de entrada
├── _Imports.razor                     @using globais
└── afya-admin.csproj                  definição do projeto
```

| Pasta | Papel |
|---|---|
| `Components` | componentes de apresentação reutilizáveis; recebem tudo por parâmetro |
| `Data` | os dados fictícios e os `record` que os descrevem, separados da apresentação |
| `Layout` | a moldura comum a todas as páginas: tema, barra superior e menu lateral |
| `Pages` | os componentes roteáveis (`@page`), ou seja, as telas da aplicação |
| `wwwroot` | arquivos estáticos servidos a partir da raiz do site |

## Componentes criados

| Componente | Responsabilidade | Parâmetros que recebe |
|---|---|---|
| `CabecalhoPagina` | título e subtítulo da página, com área livre para botões à direita | `Titulo` (obrigatório), `Subtitulo`, `Acoes` (`RenderFragment`) |
| `SeletorPeriodo` | menu com cara de botão para escolher o período | `Opcoes` (obrigatório), `Valor`, `ValorChanged` (habilita `@bind-Valor`) |
| `DashboardCard` | card base reutilizado por 5 blocos: título, subtítulo, ações, menu "⋮" e conteúdo | `Titulo` (obrigatório), `Subtitulo`, `Acoes`, `Menu`, `ChildContent` |
| `KpiCard` | um indicador: ícone pastel, valor, variação e mini gráfico de tendência | `Kpi` (obrigatório, record `Kpi`) |
| `GraficoReceita` | gráfico de linha Receita × Meta, com legenda própria | `Meses`, `Receita`, `Meta` (todos obrigatórios) |
| `GraficoDistribuicaoClientes` | gráfico de rosca com o total no centro e legenda com percentuais | `Total`, `Segmentos` (ambos obrigatórios) |
| `PerformanceProjetos` | lista de projetos com barra de progresso e contagem de tarefas | `Projetos` (obrigatório) |
| `AtividadesRecentes` | feed de atividades com ícone da ação e avatar de iniciais | `Atividades` (obrigatório) |
| `ProjetosRecentes` | tabela de projetos, que vira lista de cards no celular | `Projetos` (obrigatório) |
| `Ui` (classe estática) | `FundoSuave(Color)` monta a classe `mud-{cor}-hover`; `Iniciais(nome)` devolve "MS" | — |

## O que aprendi

> ⚠️ **RESPONDER COM SUAS PRÓPRIAS PALAVRAS** — um parágrafo curto por pergunta.
>
> Esta seção vale 15% da nota e é zerada se as respostas forem copiadas ou genéricas.
> Cite sempre o **seu** projeto: nomes de arquivos, componentes e parâmetros que você usou.

**1. Como uma aplicação Blazor WebAssembly inicia no navegador? Qual é o papel do `index.html`, da `<div id="app">` e do `Program.cs`?**

*(sua resposta)*

**2. Qual é a diferença entre um Layout, uma Page e um Component neste projeto? Dê um exemplo de cada.**

*(sua resposta)*

**3. O que é um `RenderFragment` e como o `DashboardCard` usa esse recurso para ser reutilizado por vários cards?**

*(sua resposta)*

**4. Como funciona o `@bind-Valor` no `SeletorPeriodo`? Qual é o papel do `ValorChanged`?**

*(sua resposta)*

**5. Por que os dados ficam na pasta `Data`, separados dos componentes? Que vantagem isso traz se, no futuro, os dados vierem de uma API?**

*(sua resposta)*

**6. Como o `MudGrid` com `xs`, `sm` e `lg` faz os cards de KPI se reorganizarem em telas de tamanhos diferentes?**

*(sua resposta)*

**7. Como foi possível estilizar a página inteira sem escrever CSS? Explique o papel do tema (`MudTheme`) e das classes utilitárias.**

*(sua resposta)*

**8. Por que o namespace do projeto é `afya_admin` e não `afya-admin`?**

*(sua resposta)*

## Dificuldades e soluções

> ⚠️ **ESCREVER COM SUAS PALAVRAS** — pelo menos dois problemas reais e como foram resolvidos.
>
> Dois problemas que realmente aconteceram neste projeto e que você pode descrever:
>
> **a) O nome do usuário não sumia no celular.** O bloco com "Alex Morgan" e o e-mail estava num
> `<MudStack Class="d-none d-md-flex">`, exatamente como no tutorial, mas continuava visível em
> telas pequenas. Inspecionando no DevTools, o elemento tinha as classes
> `d-flex flex-column gap-0 d-none d-md-flex` ao mesmo tempo: o `MudStack` já emite a própria
> classe `d-flex`, e no `MudBlazor.min.css` a regra `.d-flex { display:flex !important }` vem
> depois de `.d-none { display:none !important }`. Com a mesma especificidade, quem vem por
> último vence, então o `d-none` nunca fazia efeito. A solução foi pôr o `d-none d-md-flex` num
> `<div>` externo (que não traz `d-flex` próprio) e deixar o `MudStack` dentro dele — a mesma
> técnica que o tutorial usa com o `MudPaper` da busca, e que também não exige CSS.
>
> **b)** *(descreva aqui um problema que **você** enfrentou ao digitar o código)*

## Melhorias futuras (opcional)

> Ideias da seção 20 do tutorial que ainda não foram implementadas:
> trocar a cor de destaque do tema, criar as demais páginas do menu com breadcrumb dinâmico,
> fazer o seletor de período alterar os valores dos KPIs, mover os dados para um JSON carregado
> via `HttpClient`, extrair um `IDashboardService`, fazer a busca filtrar a tabela e lembrar a
> preferência de tema no `localStorage`.
