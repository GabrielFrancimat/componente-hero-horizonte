# Desafio HORIZONTE

Reproduzir uma capa de site em que um texto claro fica perfeitamente legível sobre uma fotografia clara e colorida.

![Resultado esperado](referencia.png)

A pegadinha está aí: **a foto original não é escura.** Abra `img/horizonte.jpg` e compare com a imagem acima. É o CSS que escurece a fotografia, com uma camada de sombra colocada entre a imagem e o texto. Descobrir como criar essa camada é o desafio.

---

## O que você recebe

```
img/horizonte.jpg    a fotografia original, sem nenhuma edição
referencia.png       o resultado que você deve alcançar
README.md            este arquivo
```

Não há nenhuma linha de HTML ou CSS neste repositório. Os dois arquivos você vai criar do zero.

## O que você deve entregar

```
index.html
style.css
img/horizonte.jpg
```

## Regras

1. Apenas HTML e CSS. **Nenhuma linha de JavaScript.**
2. CSS escrito à mão.
3. Não troque a foto por outra mais escura.
4. Nenhuma fonte serifada.
5. A capa ocupa a altura inteira da tela, sem barra de rolagem.
6. Precisa funcionar no celular. Estreite a janela do navegador até 375px de largura: nada pode ser cortado, estourar a tela ou ficar ilegível.

---

## Como fazer o fork

Fork é uma cópia deste repositório dentro da sua própria conta do GitHub. Você trabalha na sua cópia, sem mexer no original.

**1. Crie sua conta**
Se ainda não tem, crie em [github.com/signup](https://github.com/signup).

**2. Faça o fork**
No topo desta página, clique no botão **Fork**, no canto direito. Na tela seguinte, deixe tudo como está e clique em **Create fork**.

Pronto: o repositório agora aparece na sua conta, e o endereço muda de
`github.com/PROFESSOR/desafio-horizonte` para
`github.com/SEU-USUARIO/desafio-horizonte`.

**3. Clone a SUA cópia**
Na *sua* cópia — confira que o endereço tem o seu usuário, não o meu — clique no botão verde **Code**, copie a URL e clone:

```
git clone https://github.com/SEU-USUARIO/desafio-horizonte.git
cd desafio-horizonte
```

Clonar o repositório original em vez do seu fork é o erro mais comum aqui. Se acontecer, você não vai conseguir dar push depois.

**4. Trabalhe**
Abra a pasta no VS Code. Crie o `index.html` e o `style.css`. Abra o `index.html` no navegador para acompanhar o resultado.

**5. Envie de volta para o GitHub**

```
git add .
git commit -m "capa finalizada"
git push
```

---

## O conteúdo do texto

Use exatamente este conteúdo, nesta ordem:

- **HORIZONTE** — o título
- Litoral | Serra | Sertão — as três palavras e as barras são uma única linha de texto, digitada assim mesmo. Um traço fino entra de cada lado, feito em CSS.
- Mostra de fotografia | Terceira edição
- 2026 — com um travessão de cada lado

## A fonte

**Figtree**, do Google Fonts: [fonts.google.com/specimen/Figtree](https://fonts.google.com/specimen/Figtree)

Você vai precisar dos pesos **300** (Light) e **400** (Regular). No site do Google Fonts, selecione esses dois pesos, abra o painel *Get font › Get embed code* e cole no seu HTML o código que ele fornecer. É a única coisa que você tem permissão para copiar pronto.

---

## Ficha técnica

Os valores exatos, para você chegar igual à referência. Os valores estão aqui; onde e como aplicá-los é o desafio.

### Cores

| | Valor | Onde |
|---|---|---|
| Preto base | `#121212` | fundo da página e cor da sombra |
| Branco | `#ffffff` | o título, sem transparência |
| Branco 88% | `#ffffffe0` | *Litoral \| Serra \| Sertão* |
| Branco 78% | `#ffffffc7` | *Mostra de fotografia \| Terceira edição* |
| Branco 55% | `#ffffff8c` | o ano |
| Branco 45% | `#ffffff73` | os traços finos das laterais |

Repare que os quatro textos têm quatro transparências diferentes. É isso que cria a hierarquia: quanto menos importante, mais apagado.

**Sobre os hexadecimais de oito dígitos:** os seis primeiros são a cor, como você já conhece. Os **dois últimos são a transparência** — `00` é invisível e `ff` é totalmente opaco. Então `#ffffffe0` é o branco `#ffffff` com 88% de opacidade. É a mesma cor escrita de forma mais curta.

### A sombra

Degradê **vertical**, de cima para baixo, do mesmo preto `#121212` em três transparências:

| Posição | Cor |
|---|---|---|
| 0% (topo) | `#121212d1` |
| 45% (meio) | `#1212128c` | 
| 100% (base) | `#121212e0` |

O degradê vertical de cima para baixo é o comportamento padrão, e as paradas de `0%` e `100%` também: na prática só a do meio precisa ser escrita.

Denso nas duas pontas, leve no meio — é ali que a fotografia respira. Se quiser entender o efeito, monte primeiro com uma opacidade só, para toda a área, e depois quebre nas três paradas: a diferença é grande e vale ser vista.

### Tipografia

Dois tamanhos para cada texto: um para desktop, outro para celular.

| Elemento | Desktop | Celular | Peso | Espaço entre letras | Caixa |
|---|---|---|---|---|---|
| **HORIZONTE** | `88px` | `44px` | 300 | `0.14em` → `0.08em` no celular | como escrito |
| Litoral \| Serra \| Sertão | `12px` | `10px` | 400 | `0.3em` | MAIÚSCULAS |
| Mostra de fotografia… | `16px` | `12px` | 400 | `0.2em` → `0.12em` no celular | MAIÚSCULAS |
| 2026 | `12px` | `10px` | 400 | `0.4em` | — |

O espaço entre letras fica em `em` de propósito: `em` é relativo ao tamanho da própria fonte, então o espaçamento acompanha sozinho quando o tamanho muda.

O título tem `line-height: 1` e precisa de `text-indent` para corrigir a centralização — sempre com o mesmo valor do espaço entre letras, ou seja `0.14em` no desktop e `0.08em` no celular. O motivo está explicado na etapa 7.

### Medidas

| | Desktop | Celular |
|---|---|---|
| Altura da capa | `100vh` | `80vh` |
| Respiro interno da capa | `40px` / `24px` | `32px` / `20px` |
| Espaço entre os quatro textos | `26px` | `18px` |
| Espaço entre o texto e os traços | `18px` | `10px` |
| Traços laterais | `110px` × `1px` | `40px` × `1px` |
| Largura máxima do bloco de texto | `900px` | — |

O respiro interno traz dois valores: o primeiro em cima e embaixo, o segundo nas laterais.

**A virada entre desktop e celular acontece em 720px.** Acima disso, valem os números da coluna Desktop; em `720px` ou menos, os do celular.

---

## Roteiro de estudo

### 1. A estrutura

Você precisa de bem poucas tags. Pense em qual delas descreve melhor cada pedaço do conteúdo antes de sair escrevendo `<div>` para tudo.

`<header>` · `<img>` · `<h1>` · `<p>` · `<div>`

Na `<img>`, preste atenção nos atributos `src` e `alt`. O `alt` não é opcional: descreva a fotografia para quem não pode vê-la.

### 2. Empilhar as camadas — o coração do desafio

São três camadas, uma sobre a outra, na mesma área da tela: **a foto**, **a sombra** e **o texto**. Nessa ordem, de baixo para cima.

Para empilhar elementos em CSS, estude:

- `position` — o valor `relative` no elemento de fora e o valor `absolute` nos elementos de dentro. Entenda **por que** o pai precisa de `relative`: sem isso, o filho `absolute` se solta e vai procurar outra referência.
- `top`, `right`, `bottom`, `left` e o atalho `inset`
- `z-index` — quem fica na frente de quem
- `overflow`

> **Aviso, porque quase todo mundo trava aqui:** entre dois elementos posicionados sem `z-index`, quem aparece na frente é o que vem **depois** no HTML. Se a sua sombra sumir atrás da foto, o problema é este. E se o `z-index` parecer não fazer efeito nenhum, verifique se o elemento tem alguma `position` declarada — sem ela, o `z-index` é simplesmente ignorado.

### 3. A foto cobrindo a tela

Uma imagem esticada para preencher uma área fica deformada — as montanhas ficam gordas. Existe uma propriedade que resolve isso recortando o excesso em vez de esticar:

`width` · `height` · `object-fit` · `object-position`

Pesquise a diferença entre os valores `cover` e `contain` do `object-fit`. Teste os dois e veja com os próprios olhos o que muda.

### 4. A sombra sobre a foto

Aqui está o pulo do gato: **essa camada não é uma tag no HTML.** Ela é criada só com CSS.

- `::before` e `::after` — os pseudo-elementos
- a propriedade `content` — sem ela o pseudo-elemento não existe na página, e essa é a pegadinha mais comum de todas
- `background` com `linear-gradient()`
- **hexadecimal de oito dígitos** — os seis primeiros dígitos são a cor de sempre, os dois últimos são a transparência: `00` invisível, `ff` opaco. É assim que você escreve um preto que deixa a foto aparecer por baixo.

Sobre o degradê: ele não precisa ser uniforme. Repare na imagem de referência — a sombra é mais densa em cima e embaixo, e mais leve no meio, onde a fotografia respira. Isso se faz com **três paradas de cor** em vez de duas, cada uma com sua própria opacidade e sua própria posição em porcentagem. Os três valores estão na ficha técnica.

Ajustar esses números é a parte mais importante do exercício, e vale brincar com eles antes de fixar nos valores da ficha: você está negociando legibilidade contra uma foto que ainda quer ser vista.

### 5. Centralizar o texto

`display: flex` · `flex-direction` · `align-items` · `justify-content` · `gap` · `text-align`

Entenda por que os dois eixos se controlam com propriedades diferentes, e o que acontece quando você troca o `flex-direction` — as duas propriedades de alinhamento trocam de lado junto. Use `gap` para o espaço entre os elementos, não `margin` em cada um.

### 6. A altura da tela

`min-height` e a unidade `vh`

Pesquise o que `100vh` significa e por que se usa `min-height` no lugar de `height` aqui.

### 7. A tipografia

É o que separa uma capa que parece profissional de uma que parece um trabalho de escola. Olhe a referência com atenção: o título é **enorme, fino e com as letras muito afastadas** umas das outras. Os valores exatos estão na ficha técnica.

`font-family` · `font-size` · `font-weight` · `letter-spacing` · `line-height` · `text-transform` · `color`

Duas observações:

- O `letter-spacing` acrescenta espaço **depois** da última letra também, o que empurra o texto centralizado alguns pixels para a direita. Existe uma propriedade que devolve esse espaço para a esquerda e conserta o alinhamento. Procure por `text-indent`.
- Repare que os quatro textos não têm o mesmo tom de branco. Os menos importantes são mais apagados. Isso se faz com a opacidade da cor, não trocando o branco por cinza.

### 8. O celular

A capa precisa funcionar em duas larguras: desktop e celular. A virada é em **720px**.

- `@media (max-width: 720px)` — escreva o CSS pensando primeiro no desktop, e dentro da media query coloque **só o que muda** no celular. Repetir tudo dentro dela é desperdício e vira dor de cabeça na hora de ajustar.
- `box-sizing: border-box` — aplique em tudo no começo do arquivo. Sem isso, o `padding` soma na largura do elemento e as contas param de fechar.

Teste estreitando a janela do navegador até 375px. Compare com os números da coluna Celular na ficha técnica.

---

## Os detalhes finos (opcionais)

Só depois que o resto estiver funcionando. Nenhum deles vale entregar o desafio pela metade.

- **Os traços finos** nos dois lados de *Litoral | Serra | Sertão*. Não são imagens nem caracteres de texto: são pseudo-elementos com `1px` de altura e uma largura definida, participando do mesmo flex da linha.
- **Os travessões ao redor do ano**, com `content` no `::before` e no `::after`.

--

**Fontes de consulta:** [MDN Web Docs](https://developer.mozilla.org/pt-BR/docs/Web/CSS) para tudo, [CSS Gradient](https://cssgradient.io/) para experimentar degradês.
