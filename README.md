# HUD Screen Image Builder --- Minecraft Bedrock

Ferramenta HTML para criar e organizar imagens para `hud_screen.json` do
Minecraft Bedrock.

A ideia é facilitar a criação de HUDs baseados em **ActionBar +
condições `visible`**, sem precisar escrever manualmente cada controle
de imagem.

------------------------------------------------------------------------

## ✨ O que esta ferramenta faz?

O **HUD Screen Image Builder** transforma imagens importadas pelo
usuário em controles `image` para um `hud_screen.json`.

Cada imagem pode receber:

-   um nome;
-   uma textura;
-   tamanho;
-   posição;
-   anchors;
-   camada;
-   texto ActionBar;
-   visibilidade;
-   alpha;
-   animação;
-   modo Full Screen.

A ferramenta também possui um sistema de **sequências**, permitindo
importar várias imagens de uma vez.

------------------------------------------------------------------------

# 🖼️ Adicionando imagens

## Uma imagem

Use:

**＋ Adicionar imagem**

Isso abre o seletor de arquivos e permite escolher uma imagem.

Formatos aceitos pelo editor:

``` text
PNG
JPG/JPEG
WEBP
```

------------------------------------------------------------------------

## Várias imagens

Use:

**＋ Várias imagens**

É possível selecionar vários arquivos de imagem de uma vez.

Cada arquivo é transformado em um item separado no projeto.

------------------------------------------------------------------------

## 📁 Pasta inteira

Use:

**📁 Importar pasta**

O navegador pode fornecer o caminho relativo dos arquivos selecionados.

Isso permite trabalhar com estruturas como:

``` text
frames/
├── 001.png
├── 002.png
├── 003.png
└── 004.png
```

ou:

``` text
frames/
├── idle/
│   ├── 001.png
│   └── 002.png
└── attack/
    ├── 001.png
    └── 002.png
```

O caminho relativo pode ser usado para montar automaticamente o caminho
da textura.

------------------------------------------------------------------------

# 📚 Sistema de sequência

A ferramenta possui configuração de sequência para organizar conjuntos
de imagens.

Você pode definir:

### Nome da sequência

Exemplo:

``` text
catnap_idle
```

### Número inicial

Exemplo:

``` text
1
```

### Quantidade de dígitos

Exemplo:

``` text
3
```

Assim os números podem ser organizados como:

``` text
001
002
003
004
```

O texto ActionBar correspondente pode seguir o padrão:

``` text
catnap_idle_001
catnap_idle_002
catnap_idle_003
catnap_idle_004
```

Isso facilita posteriormente a criação de animações com o **HUD
ActionBar Animation Player**.

------------------------------------------------------------------------

# ⚙️ Configuração padrão antes da importação

Antes de adicionar as imagens, é possível definir configurações que
serão aplicadas aos novos itens.

## 🖼️ Fit

Opções:

``` text
Fill
Contain
Cover
```

### Fill

Preenche a área definida.

### Contain

Mantém a imagem dentro da área sem ultrapassar seus limites.

### Cover

Preenche a área priorizando a cobertura completa.

> O modo Fit é usado pelo editor/preview para organizar a imagem. O
> arquivo Bedrock gerado deve ser testado no seu ambiente para confirmar
> quais propriedades de apresentação são suportadas pela versão de UI
> utilizada.

------------------------------------------------------------------------

## 🖥️ Tela inteira

Opções:

``` text
Off
On
```

Quando ativado para uma imagem, o gerador usa:

``` json
"size": [
    "100%",
    "100%"
]
```

Quando desativado, usa o tamanho configurado no editor.

------------------------------------------------------------------------

# 🎛️ Editor da imagem

Depois de adicionar uma imagem, ela pode ser selecionada e configurada
individualmente.

## 📏 Largura

Define a largura do controle:

``` text
size[0]
```

## 📐 Altura

Define a altura:

``` text
size[1]
```

## 📍 Posição X / Y

Define o deslocamento:

``` json
"offset": [
    0,
    0
]
```

## ⚓ Anchor From

Define:

``` json
"anchor_from": "center"
```

Podem ser utilizados os valores disponibilizados pelo editor.

## ⚓ Anchor To

Define:

``` json
"anchor_to": "center"
```

## 🔢 Layer

Define a camada do controle:

``` json
"layer": 999999
```

Uma camada maior pode colocar o controle acima de outros elementos,
dependendo da composição do HUD.

## 🌫️ Alpha

Controla a opacidade visual no editor.

## 👁️ Visibilidade

Permite controlar se o elemento está ativo no projeto.

## ✨ Animação

O editor pode adicionar a referência de animação configurada pelo
sistema.

------------------------------------------------------------------------

# 📝 ActionBar

Cada imagem possui um texto ActionBar.

Exemplo:

``` text
test_0001
```

O controle gerado utiliza uma condição semelhante a:

``` json
"$gde_actionbar_text": "$actionbar_text",
"visible": "($gde_actionbar_text = 'test_0001')"
```

Isso significa que o HUD pode usar o texto ActionBar como identificador
do frame.

Por exemplo:

``` text
/title @a actionbar test_0001
```

pode ativar a imagem cuja condição usa `test_0001`.

------------------------------------------------------------------------

# 🧩 Como o HUD é montado

Para cada imagem, o gerador cria um controle parecido com:

``` json
{
    "type": "image",
    "texture": "textures/ui/minha_imagem",
    "size": [
        128,
        128
    ],
    "anchor_from": "center",
    "anchor_to": "center",
    "offset": [
        0,
        0
    ],
    "layer": 999999,
    "$gde_actionbar_text": "$actionbar_text",
    "visible": "($gde_actionbar_text = 'test_0001')"
}
```

O caminho da textura é montado a partir do arquivo importado.

------------------------------------------------------------------------

# 📦 `_ui_defs.json`

O `_ui_defs.json` é o arquivo que registra o HUD para o sistema de UI.

No fluxo utilizado pelo seu projeto, ele deve apontar para:

``` text
ui/hud_screen.json
```

Formato:

``` json
{
    "ui_defs": [
        "ui/hud_screen.json"
    ]
}
```

Portanto:

``` text
_ui_defs.json
       ↓
ui/hud_screen.json
```

O `hud_screen.json` contém os controles.

O `_ui_defs.json` faz o registro do arquivo de UI.

------------------------------------------------------------------------

# 📤 Exportação

A ferramenta disponibiliza:

``` text
hud_screen.json
_ui_defs.json
README.txt
```

O botão de exportação pode gerar os arquivos diretamente pelo navegador.

------------------------------------------------------------------------

# 📱 Compatibilidade

A interface foi feita em HTML/CSS/JavaScript e pode ser usada em:

-   computador;
-   tablet;
-   celular.

Em telas menores, o editor usa painéis adaptados para navegação móvel.

------------------------------------------------------------------------

# 🔄 Fluxo recomendado

``` text
IMAGENS
   ↓
Adicionar uma imagem,
várias imagens ou uma pasta
   ↓
Criar sequência
   ↓
Configurar Fill / Contain / Cover
   ↓
Configurar Full Screen
   ↓
Editar tamanho, posição, layer,
anchors, ActionBar e animação
   ↓
Exportar
   ↓
hud_screen.json
+
_ui_defs.json
```

------------------------------------------------------------------------

# 📁 Estrutura recomendada

Um Resource Pack pode ser organizado assim:

``` text
resource_pack/
├── ui/
│   ├── hud_screen.json
│   └── _ui_defs.json
│
└── textures/
    └── ui/
        ├── 001.png
        ├── 002.png
        └── 003.png
```

O caminho usado no `texture` precisa corresponder à textura disponível
no Resource Pack.

------------------------------------------------------------------------

# 🔗 Uso com o Animation Player

Depois de criar o HUD, o projeto pode ser usado junto com o:

**HUD ActionBar Animation Player**

O fluxo fica:

``` text
HUD Screen Image Builder
        ↓
hud_screen.json
        ↓
ActionBar Animation Player
        ↓
main.js
        ↓
/title <seletor> actionbar <texto>
        ↓
visible do HUD
        ↓
imagem correspondente
```

------------------------------------------------------------------------

# ⚠️ Observações

Esta ferramenta gera os arquivos de UI; ela não instala automaticamente
o Resource Pack no Minecraft.

Depois de exportar:

1.  coloque `hud_screen.json` no diretório `ui/`;
2.  coloque `_ui_defs.json` no local utilizado pelo seu sistema de UI;
3.  coloque as texturas no diretório correspondente;
4.  teste o Resource Pack no Bedrock.

A sintaxe final de UI deve ser testada na versão de Bedrock que você
está utilizando.

------------------------------------------------------------------------

# 📜 Licença

Adicione aqui a licença escolhida para o seu projeto GitHub.

Exemplo:

``` text
MIT License
```
