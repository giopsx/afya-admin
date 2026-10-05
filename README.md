# Afya Admin — Dashboard com Blazor WebAssembly e MudBlazor

## Identificação

| | |
|---|---|
| **Aluno(a)** | `PREENCHER` |
| **Matrícula** | `PREENCHER` |
| **Faculdade** | `PREENCHER` |
| **Curso** | `PREENCHER` |
| **Disciplina** | `PREENCHER` |
| **Professor(a)** | `PREENCHER` |
| **Semestre** | 2026.2 |

## Objetivo do projeto

`PREENCHER — 2 a 4 parágrafos`

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
![Inspeção do HTML no DevTools](docs/prints/devtools.png)

`PREENCHER — qual componente foi inspecionado, qual HTML ele gerou e quais classes apareceram`

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
│   ├── html-gerado.md                 HTML gerado pelos componentes
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

**1. Como uma aplicação Blazor WebAssembly inicia no navegador? Qual é o papel do `index.html`, da `<div id="app">` e do `Program.cs`?**

`PREENCHER`

**2. Qual é a diferença entre um Layout, uma Page e um Component neste projeto? Dê um exemplo de cada.**

`PREENCHER`

**3. O que é um `RenderFragment` e como o `DashboardCard` usa esse recurso para ser reutilizado por vários cards?**

`PREENCHER`

**4. Como funciona o `@bind-Valor` no `SeletorPeriodo`? Qual é o papel do `ValorChanged`?**

`PREENCHER`

**5. Por que os dados ficam na pasta `Data`, separados dos componentes? Que vantagem isso traz se, no futuro, os dados vierem de uma API?**

`PREENCHER`

**6. Como o `MudGrid` com `xs`, `sm` e `lg` faz os cards de KPI se reorganizarem em telas de tamanhos diferentes?**

`PREENCHER`

**7. Como foi possível estilizar a página inteira sem escrever CSS? Explique o papel do tema (`MudTheme`) e das classes utilitárias.**

`PREENCHER`

**8. Por que o namespace do projeto é `afya_admin` e não `afya-admin`?**

`PREENCHER`

## Dificuldades e soluções

`PREENCHER — pelo menos dois problemas e como foram resolvidos`

## Melhorias futuras (opcional)

`PREENCHER (opcional)`
