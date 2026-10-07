# Manual de comandos · PRISMA · AI

**O que funciona de verdade na grandMA2 onPC 3.9**, conferido em show real. Este é o mesmo manual que abre dentro do programa na tecla **F4**.

[← Voltar para o README](../README.md) · [Plugins](PLUGINS.md) · [Perguntas frequentes](FAQ.md)

---

## Sumário

1. [Onde pedir](#1-onde-pedir)
2. [Como pedir: prefixos](#2-como-pedir-prefixos)
3. [Pedidos prontos do PRISMA Control](#3-pedidos-prontos-do-prisma-control)
4. [Plugins BRT AI v1 e v2](#4-plugins-brt-ai-v1-e-v2)
5. [Ribaltas e barras (aparelho com várias cabeças)](#5-ribaltas-e-barras-aparelho-com-várias-cabeças)
6. [Seleção e grupos](#6-seleção-e-grupos)
7. [Presets](#7-presets)
8. [Posição REF FRENTE](#8-posição-ref-frente)
9. [Efeitos](#9-efeitos)
10. [Cenas, cues e tempo](#10-cenas-cues-e-tempo)
11. [Executor, botão e chase](#11-executor-botão-e-chase)
12. [Macros](#12-macros)
13. [Vários comandos numa linha](#13-vários-comandos-numa-linha)
14. [Stage 3D (Capture) e Layout](#14-stage-3d-capture-e-layout)
15. [Mesa em outro PC](#15-mesa-em-outro-pc)
16. [Erros da mesa](#16-erros-da-mesa)
17. [Ajustes (config.env)](#17-ajustes-configenv)

---

## 1. Onde pedir

| Onde | Como |
|---|---|
| **Na mesa, plugin BRT AI v1** | Pool de Plugins → **BRT AI v1** → digite o pedido. Faz direto. |
| **Na mesa, plugin BRT AI v2** | Pool de Plugins → **BRT AI v2** → digite o pedido. Pergunta o que falta e mostra o plano. |
| **Por macro da mesa** | `SetVar $AI_PROMPT = "cor: paleta fria"` e depois `Plugin "BRT AI v1"` (ou `"BRT AI v2"`) |
| **No programa** | Linha `[Channel]>` no rodapé: manda **comandos da MA2** direto (não é pedido para a IA). `help` mostra a ajuda; `/layout`, `/atributos`, `/criar`, `/mvr`, `/manual` abrem as ferramentas. |

> Antes do primeiro pedido, clique em **INICIAR** no programa com o show aberto na mesa. O programa lê o show e instala os plugins que faltarem.

---

## 2. Como pedir: prefixos

Comece o pedido com o assunto e dois pontos. O prefixo escolhe o especialista certo e evita que a IA adivinhe. Sem prefixo também funciona: o programa escolhe pelo assunto.

| Prefixo | O que faz | Exemplo |
|---|---|---|
| `dimmer:` | Presets de dimmer (pool 1) | `dimmer: crie níveis 0, 25, 50, 75 e 100 para todos` |
| `posicao:` | Presets de posição (pool 2) | `posicao: crie um leque abrindo e um fechando nos pointes` |
| `gobo:` | Presets de gobo (pool 3) | `gobo: crie presets com os gobos dos pointes` |
| `cor:` | Paleta de cor (pool 4): roda, RGB ou scroller, conforme o aparelho | `cor: paleta de cores quentes para os pointes` |
| `beam:` `focus:` | Pools 5 e 6 (prisma, frost, zoom, foco) | `beam: zoom aberto e fechado nos pointes` |
| `preset control:` | Pool 7 (lamp, reset) | `preset control: lamp on, lamp off e reset` |
| `preset all:` | Pool 0 (vários atributos juntos) | `preset all: abertura: centro, azul, gobo aberto, dimmer 100` |
| `efeito:` | Efeito de movimento, dimmer ou cor | `efeito: círculo espelhado nos pointes, lento` |
| `cena:` `cue:` | Sequence com várias cues, tempos e executor | `cena: 4 etapas crescendo nas ribaltas, no executor 1.120` |
| `chase:` | Sequence em modo chaser com velocidade | `chase: 6 cores no led, 128 bpm, executor 1.122` |
| `cria:` | Cena/sequence genérica (só com os dois pontos; "cria ..." sozinho é só o verbo) | `cria: blackout geral no executor 1.130` |
| `macro:` | Macros novas (as suas não são apagadas) | `macro: botão que salva o show` |
| `grupo:` | Grupos de aparelhos | `grupo: um grupo para cada tipo de aparelho` |
| `layout:` | Layout 2D | `layout: pointes em linha` |
| `laser:` | Laser com ClipSelect (só se tiver laser no patch) | `laser: 4 cues com clips diferentes` |
| `patch:` | Só responde sobre o rig, não cria nada | `patch: quais aparelhos têm cor e quais têm gobo` |
| `ajuda:` | Não cria nada. Explica a MA2 **e monta pedidos prontos** com os aparelhos, grupos e presets do seu show | `ajuda: como peço uma abertura de show?` |
| `analise` | Relê o show inteiro (depois de mexer na mesa à mão). Igual à tecla F1. | `analise` |
| `timecode:` | Trancado nesta versão (em desenvolvimento) | — |

Pergunta sem verbo de ação (termina com "?" ou começa com "como", "o que", "qual") vai para a **ajuda** e não cria nada.

Pedido impossível no seu rig (facas, vídeo, laser sem o aparelho no patch) é recusado na hora, sem gastar a IA.

### Um pedido bom tem 4 partes

**O que** criar + **em quem** (grupo ou fixtures) + **quantos** + **clima ou velocidade**.

```
chase: 6 cores nas ribaltas, 120 bpm, no executor 1.122
posicao: leque abrindo e fechando nos pointes (Fixture 11 Thru 20)
efeito: dimmer correndo por cabeca nas ribaltas, lento
```

Sem ideia de como pedir? Mande `ajuda: como peço ...`: a ajuda devolve 2 a 4 pedidos prontos para copiar, já com os números do seu show.

---

## 3. Pedidos prontos do PRISMA Control

Estes pedidos montam estruturas inteiras de uma vez, **sem caixas de pergunta** e sem gastar a IA para gerar comando por comando. Funcionam igual no v1 e no v2.

### Ordem recomendada num show novo

| Passo | Pedido | Resultado |
|---|---|---|
| 1 | (F2 Layout Designer ou F3 Stage 3D) | Aparelhos desenhados num Layout |
| 2 | `clona o desenho do 21 para 22 a 30 no layout 1` | Desenho do aparelho de várias células copiado para os outros |
| 3 | `cria os grupos de seleção pelos layouts 1 2 3` | 8 grupos por tipo, na ordem do palco |
| 4 | `cria o painel` | PRISMA Painel: seleção de grupos + cor, 2ª cor, fade, delay, FX de dimmer, cor e movimento |
| 4b | `cria o color picker` (opcional) | Color picker simples no Layout, uma linha por tipo |
| 5 | `cria os efeitos base` · `cria os presets de beam` | Efeitos e presets de feixe prontos |

### Tabela completa

| Pedido (exemplos que funcionam) | O que faz |
|---|---|
| `instala os plugins` · `atualiza os plugins` | Coloca no pool de Plugins tudo o que o PRISMA usa (BRT AI v1/v2, Color Picker, Painel, Layout Clone, Channel Sets), só o que faltar. |
| `cria os grupos de seleção` | 8 grupos por tipo de aparelho (ALL, ODD, EVEN, ESQ, DIR, CENTRO, PONTAS, IN-OUT) pela posição 3D. Números a partir de 101, um bloco de 10 por tipo. |
| `cria os grupos de seleção pelos layouts 1 2 3` | Igual, pela ordem do desenho nos Layouts citados (cada tipo usa o layout onde está). Pedir de novo regrava nos mesmos números. |
| `reordena os grupos pelo layout 1` · `arruma a ordem dos grupos 1 a 8 pelo palco` | Regrava os grupos existentes com os mesmos aparelhos, só na ordem física. Conserta efeito/delay correndo fora de ordem. |
| `cria o painel` · `cria o super color picker` | PRISMA Painel v1.5: os grupos de seleção viram botões (marca e fica marcado) e cor, 2ª cor, fade, delay, FX de dimmer, FX de cor, movimento e rate vão só nos marcados. Dois layouts (COR e FX), executores na página 99. Precisa dos grupos de seleção. |
| `cria o painel na pagina 5` | O mesmo, com os executores na página 5. |
| `movings vermelho com fade de 2s` · `strobo ímpar magenta` · `tudo uv com delay 2s do centro pra fora` · `beam vermelho e segunda cor oposta` | Com o painel no show: marca os grupos e aperta os botões do painel. Não cria nada. |
| `cria o color picker` | Color picker simples (plugin PRISMA Color Picker v8): uma linha por tipo (grupos "… ALL") + ALL, 2ª cor, fade, delay e direção. |
| `color picker dos grupos 101 e 111 na pagina 2` | Color picker só com esses grupos, executores na página 2. |
| `deixa tudo azul` · `vermelho com fade de 2s` · `âmbar da esquerda pra direita com delay de 1s` | Com o color picker já criado (e sem painel): aperta os botões do picker (cor, fade, delay, direção). Não cria nada. |
| `clona o desenho do 21 para 22 a 30 no layout 1` | Layout Clone: copia o desenho do aparelho 21 (todas as células) para 22 a 30, no lugar de cada um, aproximando com 1 quadrado de folga. |
| `clona o desenho do 21 para 22 a 30 no layout 1 em grade` | Mesma cópia, mas em grade (5 por linha). |
| `clona o desenho do 21 para 22 a 30 no layout 1 sem aproximar` | No lugar, mantendo o espaço original. |
| `clona o desenho do 1 para 2 a 12 no layout 3 e salva no layout 5` | Lê o modelo no layout 3 e grava o resultado no layout 5. |
| `cria o layout dos tipos com ícones` · `prisma tipos` | Layout com um botão por tipo de aparelho, com o ícone do tipo; clicou, seleciona o tipo. |
| `importa os ícones do prisma` | Ícones de aparelho (Image pool a partir de 301) e de função (a partir de 1200). Usa bloco livre e não duplica. |
| `cria os efeitos base` | Efeitos a partir do 901: Circle, Tilt Leque, Pan Wave, Spread (wings 2), Dim Chase, Dim Onda e Dim+Pos. Movimento só se o show tem movings. |
| `cria os presets de beam` | Pool 5 a partir do 101: Zoom Fechado/Médio/Aberto, Íris Aberta/Fechada, Frost Off/Full, só nos aparelhos que têm o atributo. |

> **Ordem física (colunas):** os grupos de seleção seguem o desenho do layout, da esquerda para a direita. Num desenho em **andares** (a maioria das colunas com 2 ou mais aparelhos, ex.: LED em cima e embaixo), os aparelhos um em cima do outro formam uma coluna: acendem juntos no efeito e no delay, e ODD/EVEN contam por coluna. Numa **fila**, cada aparelho é uma coluna, mesmo que dois estejam encostados. Aparelho de várias células (strobo cluster) conta pelo centro do desenho dele. O `reordena os grupos` continua usando a numeração quando o desenho é cobra, V ou zigue-zague.

### Usando o color picker na mesa

| Linha | O que faz |
|---|---|
| **<tipo>** (ex.: `BS960 Strobosc`) | 12 cores para aquele tipo: White, Red, Amber, Yellow, Green, Cyan, Blue, Lavender, Magenta, Pink, CTO, UV |
| **SPLIT** (embaixo de cada tipo) | 2ª cor: escolha a cor e o padrão **1x1** (alternado, grupo EVEN), **MET** (metades, grupo DIR) ou **PNT** (pontas, grupo PONTAS). **OFF** solta a 2ª cor. |
| **ALL** | A mesma cor para todos os tipos |
| **FADE** | OFF, 0.5, 1, 2, 3, 5 s para todas as linhas |
| **DELAY** | OFF, 0.5, 1, 2, 3, 5 s |
| **DIR** | Direção do delay: esquerda→direita, direita→esquerda, centro→fora, fora→centro |

O quadrado cheio mostra a cor ativa. A 2ª cor fica num executor próprio com prioridade **HIGH**: trocar a cor principal não apaga o split.

### Usando o PRISMA Painel na mesa

| Linha | O que faz |
|---|---|
| **Seleção** | Uma linha por tipo: `[TIPO] [ALL] [ODD] [EVEN] [ESQ] [DIR]`, um marcado por tipo (verde). `TODOS` marca o ALL de todos, `LIMPA` desmarca. Tudo abaixo vale só para os marcados. |
| **COR** / **OFF** | 12 cores (a escolhida aparece como `> NOME <`). OFF solta a cor dos marcados. |
| **COR FX** / **OPOSTA** | 2ª cor dos efeitos de cor. OPOSTA = cor complementar da COR atual. |
| **FADE** · **DELAY** · **DIR** | Tempo da troca de cor e delay entre aparelhos, por coluna: `>>` `<<` `><` `<>`. O delay é gravado às cegas (não mexe no programmer). |
| **FX DIM** | `>>>` `<<>>` `1/3` `2/2` `PULSO` `ONDA` `RANDOM` `OFF` |
| **FX COR** | `COR >>>` `COR 2/2` `COR ONDA` `OFF` (alterna COR e COR FX; trocar a cor não para o efeito) |
| **MOVE** | `CIRCLE` `LEQUE` `ONDA` `SPREAD` `OFF` (tipos com pan/tilt) |
| **RATE** · **BPM** | `1/4` a `4x` e BPM digitado (60 = normal) nos FX dos marcados |

Mudou o desenho ou os grupos? Peça os grupos de seleção de novo, apague o painel antigo (os números aparecem no retorno do `cria o painel`) e crie outro: as fases e os delays ficam gravados nas cues.

---

## 4. Plugins BRT AI v1 e v2

| | BRT AI v1 (direto) | BRT AI v2 (conversa) |
|---|---|---|
| Pergunta? | Nunca. Escolhe sozinho: usa o Group do tipo pedido; sem grupo, todos os aparelhos daquele tipo. | Pergunta o que falta (quais aparelhos, tonalidade, quantas etapas) ou mostra a lista do que vai criar. |
| Aprovação | Não. Executa e mostra o resultado. | Mostra o plano e espera você aprovar. |
| Quando usar | Pedido claro, correria de show. | Quando você quer escolher os detalhes. |

### Respondendo a lista do v2

Quando aparecer `Vou criar 8 presets de Color (RED, GREEN, ...) para as Fixtures 201 Thru 218.`, responda:

- `ok` (ou vazio): cria exatamente aquela lista, sem chamar a IA de novo
- `tira a rosa` / `troca o verde por lima` / `acrescenta um lilas`: refaz só com a mudança

Mais detalhes em [PLUGINS.md](PLUGINS.md).

---

## 5. Ribaltas e barras (aparelho com várias cabeças)

Ao ler o show, o sistema conta as cabeças de cada tipo (ex.: DTW Bar = 12, de 1.1 a 1.12; strobo BS960 = 16, de 21.1 a 21.16).

```
Fixture 1                                  (as 12 cabeças juntas)
Fixture 1.3                                (só a 3ª cabeça)
Fixture 1.1 Thru 1.12                      (uma a uma, em ordem)
Fixture 1.1 Thru 1.12 + 2.1 Thru 2.12      (cabeças de duas ribaltas, em ordem)
```

**NÃO:** `Fixture 1.1 Thru 10.12`: a mesa recusa o Thru de uma ribalta para outra.

Escreva **por cabeça** no pedido (chase, efeito, cor alternada) para a IA trabalhar cabeça a cabeça. No layout, cada cabeça vira um quadrado em linha; use o **Layout Clone** para copiar um desenho (cruz, círculo) de um aparelho para os outros.

---

## 6. Seleção e grupos

```
ClearAll
Fixture 101 Thru 112
Fixture 1 Thru 10 + 101 Thru 112
Fixture 14 + 12 + 10 Thru 8          (a ordem escrita é a ordem da seleção)
Group 4
Store Group 5 "POINTES"
Store Group 5 /o /nc                 (regrava por cima, sem perguntar)
```

**NÃO:** `Group 21 Thru 40` seleciona grupos, não aparelhos (Error #72).

A ordem da seleção gravada no grupo é a ordem em que efeito, fase e delay correm. Por isso os grupos de seleção do PRISMA são gravados na ordem do palco.

---

## 7. Presets

| Pool | Tipo | Pool | Tipo |
|---|---|---|---|
| 0 | All | 5 | Beam |
| 1 | Dimmer | 6 | Focus |
| 2 | Position | 7 | Control |
| 3 | Gobo | 8 | Shapers |
| 4 | Color | 9 | Video |

```
ClearAll ; Fixture 101 Thru 112 ; Attribute "Pan" At 0 ; Attribute "Tilt" At 20 ; Store Preset 2.9 "CENTRO" ; ClearAll
ClearAll ; Fixture 201 Thru 218 ; Attribute "Dim" At 60 ; Store Preset 1.6 "RIBALTA 60" ; ClearAll
```

- `Store Preset 2.9 "NOME"` grava e dá nome num comando só.
- Use o atributo que o aparelho tem: moving de roda usa `COLOR1`, LED e ribalta usam `ColorRGB1..3`, scroller usa `SCROLLER`.
- **Cor com LED + moving de disco:** o LED entra em todas as cores. O moving só entra no preset cuja cor existe no disco dele. Pedindo 30 cores com um disco de 8, o moving fica só nos que batem. Nunca valor entre duas cores do disco.
- O sistema troca sozinho para o próximo ID livre se o pedido cair em cima de um preset seu.

---

## 8. Posição REF FRENTE

A IA não sabe como cada moving está montado: `Tilt At -30` pode ser frente num e fundo no outro. Por isso existe a posição de referência.

1. Aponte os movings para a **frente do palco**.
2. Grave no slot **101** da pool Position (não no 1): `Store Preset 2.101 "REF FRENTE"`
3. Pronto. Antes de cada pedido de posição, cena ou efeito o sistema relê a pool 2; não precisa reanalisar o show.

```
ClearAll ; Fixture 101 Thru 112 ; Preset 2.101 ; Attribute "Tilt" At + 15 ; Store Preset 2.9 "PLATEIA" ; ClearAll
```

Com a REF gravada, a IA monta as posições a partir dela com ajuste relativo (`At + 15`), nunca com valor absoluto. "Frente" é a própria REF. O programa mostra um aviso enquanto houver aparelhos com pan/tilt e a REF não estiver gravada (tecla **F5** confere).

---

## 9. Efeitos

### Receita testada

```
ClearAll
Fixture 101 Thru 112
MAtricksWings 2
Attribute "Pan" At EffectForm 8
Attribute "Pan" At EffectPhase 0 Thru 360
Attribute "Tilt" At EffectForm 9
Attribute "Tilt" At EffectPhase 0 Thru 360
Attribute "Pan" At EffectBPM 20
Attribute "Tilt" At EffectBPM 20
Store Effect 14 /nc
Label Effect 14 "CIRCULO"
MAtricksReset
ClearAll
```

### Formas (número desta mesa)

| N | Forma | Uso | N | Forma | Uso |
|---|---|---|---|---|---|
| 1 | Stomp | batida (não é seno!) | 10 | Ramp Plus | sobe e reseta |
| 3 | Random | aleatório | 11 | Ramp Minus | cai e reseta, cascata |
| 4 | Pwm | liga/desliga, chase de dimmer | 19 | Circle | círculo |
| 8 | Sin | onda, respiração | 22 | Wave | onda |
| 9 | Cos | seno adiantado 90 graus | 23 | Cross | cruzado |

- Toda camada com `Attribute "X"` na frente. `EffectPhase 0 Thru 360` sozinho cria uma linha extra (DIST) no efeito.
- Pan e Tilt são relativos: `EffectLow -20` / `EffectHigh 20` balança em volta da posição atual. Dimmer é absoluto: 0 a 100.
- Círculo: Pan 8 + Tilt 9, mesma fase e o mesmo BPM nos dois.
- Fase `0 Thru 360` faz a onda correr; fase 0 em todos = todo mundo junto.
- `MAtricksWings 2` espelha as metades, `MAtricksBlocks 2` anda em pares. Sempre termine com `MAtricksReset`.
- Efeito numa cue: `Group 101 ; At Effect 14 ; Store Sequence 50 Cue 1 /nc`.
- BPM depois de gravado: `Assign EffectBPM 140 Effect 14`.

**NÃO:** `Assign Effect 1 /wings=2` e `Assign Effect 1 /Attribute=...` não existem.

---

## 10. Cenas, cues e tempo

```
ClearAll ; Fixture 101 Thru 112 ; Preset 4.3 ; Preset 2.1 ; At 80
Store Sequence 120 Cue 1 "INTRO" Fade 3 /nc
Store Sequence 120 Cue 2 "PICO" Fade 0.5 Delay 1 /nc
Label Sequence 120 "ABERTURA"
```

- Sempre `Sequence N` na frente da cue. `Store Cue 120.2` vira a cue 120.2 da sequence selecionada, não a Sequence 120.
- Cue com número quebrado entra no meio: `Cue 2.5` fica entre a 2 e a 3.
- Cue chamando `Preset 4.3` em vez de valor solto: mudou o preset, todas as cues mudam junto.

**Leque de tempo (antes do Store):** `Fade 1 Thru 4` · `Delay 0 Thru 2`. Cada aparelho da seleção ganha um tempo diferente: a cor "escorre" pelo rack.

**Mudar o tempo de uma cue já gravada:**

```
Assign Sequence 120 Cue 2 /fade=4 /delay=0.5
Assign Sequence 120 Cue 2 /outfade=1 /outdelay=0
Assign Sequence 120 Cue 2 /info="entra com o bumbo"
```

**Cue que entra sozinha:**

```
Assign Sequence 120 Cue 2 /trig=follow
Assign Sequence 120 Cue 3 /trig=time /trigtime=3
```

`follow` = entra quando a anterior termina. `time` = entra N segundos depois. Conferir: `ChangeDest Sequence 120 Cue 2` e `List`.

---

## 11. Executor, botão e chase

```
Store Page 2 /nc
Assign Sequence 122 At Executor 1.122
Assign Flash Executor 1.122
Assign Executor 1.122 /chaser=on
Speed 128 Executor 1.122
Rate 2 Executor 1.122
```

| Função do botão | Faz |
|---|---|
| `Assign Go Executor P.E` | entra a cena e fica |
| `Assign Flash Executor P.E` | acende só enquanto aperta: ataque, blinder, golpe |
| `Assign Toggle Executor P.E` | liga e desliga no mesmo botão |

- Opções que a mesa aceitou: `/chaser=on` `/autofix=on` `/priority=htp` `/priority=high` `/autostart=on` `/autostop=on` `/ooo=on` `/restart="First Cue"`
- `Speed 128 Executor X` = velocidade do chase. `Rate 2 Executor X` = tudo no dobro da velocidade (efeito, fade); `Rate 1` volta ao normal.
- Pular para uma cue com o tempo dela: `Goto Executor 1.122 Cue 3`.

**NÃO:** `/speed=120` (Error #7), `/rate=` e `/swop=` (Error #66). Velocidade é com `Speed N Executor P.E`.
**NÃO:** `Go+ Executor 1.120` (Error #72). **OK:** `Go+ Sequence 120`, `Goto Sequence 120 Cue 3`, `Flash Sequence 120`.
**NÃO:** executor numa page que não existe = Error #14. Crie antes com `Store Page N /nc`.

---

## 12. Macros

```
CD Macro
Store 11 "SALVAR"
Store 11.1 "SaveShow /nc"
CD /
```

- Vários comandos numa linha de macro: `ClearAll ; Fixture 1 Thru 10 ; At 100`, com espaço dos dois lados do `;`. Sem o espaço, a mesa roda só o primeiro.
- Macros expandem variáveis: `Delay 0 Thru $PCP_DELAY`. O valor de um `SetVar` não pode ter `;`.
- O sistema nunca apaga macro sua: se o número estiver ocupado, grava no próximo livre.

---

## 13. Vários comandos numa linha

```
ClearAll ; Fixture 7 ; Move3D At -6.548 -0.97 7.11 ; Rotate3D At 0 0 -180 ; ClearAll
```

- A mesa aceita `a ; b ; c` e é bem mais rápido que um por vez. O sistema já manda assim, até ~1000 letras por linha (a mesa executa só ~1024 letras de cada linha do Telnet e descarta o resto em silêncio).
- Mexer na mesa (clicar num preset, abrir um plugin) enquanto uma linha longa roda faz a mesa largar o resto da linha. O sistema percebe e reenvia do ponto certo.
- Colar várias linhas de uma vez na linha de comando da MA2 dá **Error #3 ILLEGAL CHARACTER**: só a primeira roda. Junte tudo numa linha com ` ; `.
- Se um comando falha, a mesa abandona o resto da linha. O sistema percebe e manda o que faltou na linha seguinte.
- `Delete` sempre com `/nc`. Sem ele abre uma janela de confirmação e a conexão trava.
- `Echo` não existe na MA2 (Error #1).

---

## 14. Stage 3D (Capture) e Layout

**3 passos** na tela F3 (veja as imagens no [README](../README.md#stage-3d-do-capture-para-a-grandma2)):

1. **Projeto do Capture:** escolha a pasta do projeto. O arquivo mais novo abre sozinho (`.mvr` traz posição e patch; o `.c2p` traz o nome de cada canal).
2. **Conferir:** mapas de cima e de frente, o tipo da biblioteca MA2 de cada aparelho ("canais batem" = mesmos canais na mesma ordem; senão **CRIAR TIPO**) e os números. **Numerar** continua de onde a mesa parou e mantém os IDs digitados à mão. "Ajustar posição" corrige a origem e a escala.
3. **Enviar para a MA2:** Criar aparelhos, Posicionar no palco e Layout 2D.

### Criar aparelhos

- Deixe aberta na mesa a janela **Setup → Patch & Fixture Schedule**. Sem ela a MA2 ignora a camada. Depois feche e responda **SIM**.
- Cria uma camada por tipo ("CAPTURE Robin Pointe"...) com ID, endereço, posição e rotação. Endereço ocupado vai para o próximo livre.
- Se algum aparelho não entrar, o sistema manda de novo em partes pequenas (camadas extras "... +1", "+2") e lista quem faltou.
- Quem já está na mesa com o mesmo tipo é pulado: pode rodar de novo.

### Posicionar no Stage 3D

Compara a posição e a rotação da mesa com as do Capture e manda só o que falta. Com o Patch aberto a MA2 mostra 0 0 0 em todos: feche o Patch (SIM) e clique em ↻ antes de conferir.

**NÃO:** a ribalta de 11 partes (Beam Bar) recusa `Move3D` (Error #72). O sistema tenta uma, pula as outras do mesmo tipo e avisa. A posição dela vem da camada.

### Layout 2D

```
Store Layout 20 "CAPTURE" /o
ClearAll ; Fixture 101 ; Store Layout 20 /m /x=12.0 /y=-4.0
Label Layout 20 "CAPTURE"
```

- Aparelho com cabeças vai cabeça por cabeça, em linha (`Fixture 1.1 ; Store Layout 20 /m /x=0 /y=0 ...`). O layout é ampliado pelo número de cabeças da maior barra; use **Zoom Fit** na mesa.
- Depois use o **Layout Clone** para trocar a linha de células pelo desenho do aparelho.

**NÃO:** `Assign Fixture 1 At Layout 20`: a mesa aceita, mas o layout fica vazio. O sistema troca por `Store Layout /m` sozinho.

---

## 15. Mesa em outro PC

A grandMA2 onPC pode estar em outro computador da mesma rede. Tudo funciona igual: pedidos, leitura do show, plugins, Layout e Stage 3D.

**No PC da mesa:**

1. grandMA2: **Setup → Console → Global Settings → Telnet = Login Enabled**.
2. Windows: rede **Privada** (a Rede pública bloqueia tudo).
3. Firewall, no PowerShell como administrador:
   `New-NetFirewallRule -DisplayName "grandMA2 Telnet" -Direction Inbound -Protocol TCP -LocalPort 30000 -Action Allow`

**No PC do PRISMA:** com o programa parado, clique em **MESA → Endereço** no painel, digite o IP da mesa (ex.: `192.168.0.11`) e clique em **INICIAR**.

**Não conecta?** O ping costuma estar bloqueado pelo Windows e não prova nada. Teste a porta: `Test-NetConnection 192.168.0.11 -Port 30000` tem que dar `TcpTestSucceeded : True`. `arp -a` mostra se o PC da mesa aparece na rede.

---

## 16. Erros da mesa

| Erro | Quando aparece | O que fazer |
|---|---|---|
| #1 UNKNOWN COMMAND | palavra que a mesa não conhece (ex.: Echo) | confira o nome do comando |
| #3 ILLEGAL CHARACTER | várias linhas coladas de uma vez | junte numa linha com ` ; ` |
| #7 | `/speed=` no Assign Executor | use `Speed N Executor P.E` |
| #9 NUMBER TOO LARGE | `List Executor 1.1 Thru 1.999` | faixa menor (até .200) |
| #14 OBJECT DOES NOT EXIST | atributo que o aparelho não tem, page ou objeto inexistente | confira o patch / crie a page |
| #43 LOGIN NEEDED | conexão sem login | o programa faz o login sozinho (Administrator / admin, depois sem senha). Show com outra senha: `MA2_USUARIO` e `MA2_SENHA` no config.env |
| #66 | opção que o comando não aceita (`/rate=`, `/swop=`, `Assign Effect /Attribute=`) | use o comando próprio (`Rate N Executor`) |
| #72 COMMAND NOT EXECUTED | `Go+ Executor`, `Group X Thru Y`, `Move3D` na Beam Bar, comando enquanto a mesa importa uma camada | veja as seções acima; no Stage 3D espere o "criar aparelhos" terminar |

---

## 17. Ajustes (config.env)

| Variável | O que faz |
|---|---|
| `IA_PROVIDER=cli` / `api` | IA pelo Antigravity CLI (assinatura) ou pela chave Gemini |
| `AGY_EFFORT=low` | quanto o CLI pensa: low (rápido, padrão), medium, high |
| `AGY_MODEL=` | modelo do CLI (veja a lista com `agy models`) |
| `CLI_RESERVA=0` | desliga o agy que fica aberto esperando o próximo pedido |
| `MA2_LINHA_MAX=250` | tamanho máximo de cada linha mandada para a mesa |
| `PROMPTS_NUVEM=0` | não baixa prompts da nuvem ao iniciar |
| `AI_BRIDGE_LOG_LEVEL=verbose` | log da mesa pedaço a pedaço |
| `MA2_USUARIO=` · `MA2_SENHA=` | usuário e senha da mesa, quando o show não usa o Administrator padrão (senha "admin") |
| `PRISMA_FX_BASE=901` | primeiro número dos efeitos base |
| `PRISMA_ICON_BASE=301` · `PRISMA_ICON_FX_BASE=1200` | primeiro número dos ícones no Image pool |

---

Dúvidas: **audiovisualbrt@gmail.com** · Vídeos: **[YouTube @BRTAPRESENTA](https://www.youtube.com/@BRTAPRESENTA)**

grandMA2 é marca da MA Lighting Technology GmbH. O PRISMA · AI é um produto independente do Studio BRT.
