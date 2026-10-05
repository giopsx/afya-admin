# HTML gerado pelo Blazor (material para a inspeção no DevTools)

Trechos extraídos da aplicação rodando, para apoiar a análise do print `docs/prints/devtools.png`.

## 1. Card de KPI — `<MudPaper>`

Código Razor escrito em `Components/KpiCard.razor`:

```razor
<MudPaper Elevation="1" Class="pa-4" Height="100%">
```

HTML que o Blazor gerou:

```html
<div class="mud-paper mud-elevation-1 pa-4" style="height:100%;">
```

| O que foi escrito | O que apareceu no HTML |
|---|---|
| `<MudPaper>` | uma `<div>` com a classe `mud-paper` |
| `Elevation="1"` | a classe `mud-elevation-1` (a sombra do card) |
| `Class="pa-4"` | a classe utilitária `pa-4` passou direto, sem tradução |
| `Height="100%"` | um atributo `style="height:100%"` inline |

## 2. `<MudStack>` vira um container flex

```razor
<MudStack Row="true" Spacing="3" AlignItems="AlignItems.Center">
```

```html
<div role="group" class="d-flex flex-row align-center gap-3">
```

`Row="true"` virou `flex-row`, `AlignItems.Center` virou `align-center` e `Spacing="3"` virou `gap-3`.
Ou seja: os parâmetros do componente são traduzidos para as mesmas classes utilitárias do MudBlazor.

## 3. Avatar com fundo pastel — `Ui.FundoSuave`

```razor
<MudAvatar Size="Size.Large" Class="@Ui.FundoSuave(Kpi.Cor)">
    <MudIcon Icon="@Kpi.Icone" Color="@Kpi.Cor" />
</MudAvatar>
```

```html
<div class="mud-avatar mud-avatar-large mud-avatar-filled mud-avatar-filled-default mud-elevation-0 mud-success-hover">
  <svg class="mud-icon-root mud-svg-icon mud-success-text mud-icon-size-medium" viewBox="0 0 24 24" role="img">...</svg>
</div>
```

A string `"mud-success-hover"` montada em C# chegou ao HTML como classe. O ícone recebeu
`mud-success-text`, que é a cor "cheia" — daí o contraste entre o círculo claro e o ícone forte.

## 4. Botão — `<MudButton>`

```razor
<MudButton Variant="Variant.Filled" Color="Color.Primary" Size="Size.Large"
           StartIcon="@Icons.Material.Filled.Add">Novo Projeto</MudButton>
```

```html
<button class="mud-button-root mud-button mud-button-filled mud-button-filled-primary mud-button-filled-size-large mud-ripple" type="button">
  <span class="mud-button-label">
    <span class="mud-button-icon-start mud-button-icon-size-large">
      <svg class="mud-icon-root mud-svg-icon mud-icon-size-large" viewBox="0 0 24 24" role="img">
        <path d="M19 13h-6v6h-2v-6H5v-2h6V5h2v6h6v2z"></path>
      </svg>
    </span>
    Novo Projeto
  </span>
</button>
```

Cada parâmetro virou uma classe: `Variant.Filled` → `mud-button-filled`,
`Color.Primary` → `mud-button-filled-primary`, `Size.Large` → `mud-button-filled-size-large`.
O `StartIcon` virou um `<svg>` inline dentro de um `<span>`, e não uma imagem.

## 5. Os comentários `<!--!-->`

Aparecem por toda parte no HTML. São marcadores que o Blazor usa para delimitar os pedaços
que ele pode atualizar sozinho depois, sem redesenhar a página inteira.
