# Plugins na mesa · PRISMA · AI

O PRISMA · AI coloca estes plugins no **pool de Plugins** da grandMA2 onPC. Ele instala sozinho ao clicar em **INICIAR** (também com a mesa em outro PC da rede), e você pode pedir **`instala os plugins`** a qualquer momento: ele coloca só o que faltar, na versão certa, e tira do pool as versões velhas (Color Picker v7/v8, Painel v1.4...).

[← Voltar para o README](../README.md) · [Guia do Painel](PAINEL.md) · [Manual de comandos](MANUAL.md) · [Perguntas frequentes](FAQ.md)

![Plugins na mesa](../imagens/03-plugins-na-mesa.png)

| Nº típico | Plugin | Para que serve | Roda à mão? | A IA usa? |
|---|---|---|---|---|
| 2 | **BRT AI v1** | Pedido direto para a IA | Sim | É a porta de entrada |
| 3 | **BRT AI v2** | Pedido com conversa e aprovação | Sim | É a porta de entrada |
| 4 | **PRISMA Painel v2.8** | O color picker do PRISMA: seleção de grupos + cor + FX + efeitos que batem com a música | Sim | Sim (`cria o painel` ou `cria o color picker`, e depois troca cor e FX falando) |
| 5 | **PRISMA Layout Clone v4** | Copiar o desenho de um aparelho de várias células | Sim (com perguntas) | Sim (`clona o desenho do ...`) |
| 6 | **PRISMA Channel Sets v3** | Nomear cores/gobos da roda olhando o aparelho | Sim | Pela tela F6 · Atributos |

Todos os plugins são **ASCII puro** (a MA2 não aceita acento nem emoji dentro do Lua) e **nunca apagam** objetos do show: conferem os números livres antes de gravar.

---

## BRT AI v1 — modo direto

Você pede, a IA decide sozinha e executa. Sem perguntas e sem tela de aprovação.

- "presets nos movings": usa o Group dos movings se existir; senão, todos os aparelhos daquele tipo.
- "paleta de cor": escolhe uma paleta coerente sozinha.

**Como funciona por dentro:** o plugin manda `AI_REQUEST: [AUTO] <pedido>` no feedback da mesa. O `[AUTO]` diz ao programa: não perguntar, não pedir aprovação, executar. O plugin espera o programa escrever `$AI_STATUS = DONE` (ou `ERROR`) e mostra o resultado numa caixa.

**Uso:**

- Direto: rode o plugin e digite o pedido na caixa.
- Por macro: `SetVar $AI_PROMPT = "crie posicoes nos movings"` e depois `Plugin "BRT AI v1"`.

## BRT AI v2 — pergunta, plano e aprovação

Manda o pedido, recebe o plano de comandos, você lê e aprova (ou cancela) antes de qualquer coisa tocar no show.

```
plugin   -> programa : AI_REQUEST: <pedido>
programa -> plugin   : $AI_STATUS = "PLAN"  (e $AI_L1..N com o plano)
plugin   -> programa : AI_APPROVE: <id>
```

Respostas na caixa: `ok` (ou vazio) cria a lista mostrada; `tira a rosa`, `troca o verde por lima`, `acrescenta um lilas` refazem só com a mudança.

Os plugins usam **SetVar** (variável global do show), não SetUserVar: o Telnet do programa entra como Administrator e o plugin roda no perfil da tela; com SetVar os dois se enxergam. Macros antigas com `SetUserVar $AI_PROMPT` continuam funcionando.

---

## PRISMA Painel v2.8 — o color picker do PRISMA

Uma paleta só, e os **grupos viram botões de seleção**: você marca o grupo (ele fica verde) e aperta a cor ou o efeito, que vai só nele. São **três páginas** (três layouts): **COR**, **FX** (efeitos sem som) e **SOM** (efeitos que batem com a música). A seleção de grupos aparece igual nas três, e os botões embaixo dela viram a página.

Basta pedir **`cria o painel`** (executores na página 99, longe dos seus playbacks; `cria o painel na pagina 5` escolhe outra). `cria o color picker`, `seletor de cores`, `super color picker` e `paleta de cores no layout` criam o mesmo Painel; `color picker dos grupos 101 e 111 na pagina 2` cria o Painel só com as linhas desses grupos, na página 2.

**Pedir de novo não duplica:** `cria o painel` (ou `refaz o painel`, `recria o painel`, `atualiza o painel`, `cria o color picker`) num show que já tem painel apaga o antigo antes (o bloco de macros, os layouts "PRISMA Painel", as sequences, presets e efeitos "PPN ..." e desliga os executores dele) e cria o novo no lugar. Painel v1.4 antigo, sem o mapa dos botões: os layouts, sequences, efeitos e macros "PPN" escondidas saem, mas as macros de cor antigas ficam no pool (apague à mão). Se o show ainda não tem os grupos de seleção, o PRISMA cria antes, sozinho: ele lê todos os layouts do show e cada tipo de aparelho usa o layout onde está desenhado (o layout dos strobos para os strobos, o dos movings para os movings). Sem nenhum layout com aparelhos, usa a posição 3D.

**Atualizou o PRISMA?** Peça `refaz o painel` para o show receber o painel novo (o plugin novo entra no pool sozinho ao clicar em INICIAR).

Cada quadrado explicado em detalhe (o que faz, para que serve e o que acontece na mesa): **[Guia do Painel](PAINEL.md)**.

### Seleção (nas três páginas)

| Botão | O que faz |
|---|---|
| **Linha de cada tipo** | `[TIPO] [ALL] [ODD] [EVEN] [ESQ] [DIR]`: um grupo marcado por tipo (verde). Clicar no nome do tipo marca o ALL. |
| **TODOS** · **LIMPA** | `TODOS` marca o ALL de todos os tipos; `LIMPA` desmarca tudo. |
| **COR · FX · SOM** | Viram a página. |

Tudo o que você aperta embaixo vale **só para os grupos marcados**.

### Página COR

![Painel: página COR](../imagens/22-painel-cor.png)

| Linha | O que faz |
|---|---|
| **COR** | 12 cores + OFF: White, Red, Amber, Yellow, Green, Cyan, Blue, Lavender, Magenta, Pink, CTO, UV. A cor escolhida fica acesa e com `> NOME <`. OFF solta a cor dos marcados. |
| **COR FX** · **OPOSTA** | A 2ª cor, usada pelos efeitos de cor (FX COR e COR BATIDA). **OPOSTA** põe a cor complementar da COR atual (vermelho → verde, âmbar → azul...). |
| **FADE** | OFF, 0.5, 1, 2, 3, 5 s na troca de cor |
| **DELAY** + **DIR** | OFF, 0.5, 1, 2, 3, 5 s · `>>` `<<` `><` (centro sai primeiro) `<>` (pontas saem primeiro). O delay corre pelas colunas do desenho e é gravado às cegas (não mexe no programmer). |

### Página FX (efeitos sem som)

![Painel: página FX](../imagens/23-painel-fx.png)

| Linha | O que faz |
|---|---|
| **FX DIM** | `>>>` `<<>>` `1/3` `2/2` `PULSO` `ONDA` `RANDOM` `OFF`: efeito de dimmer correndo pelas colunas |
| **FX COR** | `COR >>>` `COR 2/2` `COR ONDA` `OFF`: alterna a COR e a COR FX. Trocar a cor muda o efeito sem parar ele. |
| **MOVE** | `CIRCLE` `LEQUE` `ONDA` `SPREAD` `OFF` (só tipos com pan/tilt) |
| **RATE** · **BPM** | `1/4` `1/2` `1x` `2x` `4x` e **BPM** (pergunta o número: 60 = normal, 120 = o dobro), nos FX dos marcados |

### Página SOM (tudo que bate com a música)

![Painel: página SOM](../imagens/24-painel-som.png)

Usa o **Sound Input** da grandMA2 (a placa de som ou o microfone do PC). Na janela Sound Input, o **Snd In** é o ganho: deixe baixo (uns 5 a 15%). Alto demais, todas as faixas ficam no pico e tudo acende junto.

| Linha | O que faz |
|---|---|
| **BATIDA** | `>>>` `<<<` `ONDA` `<<>>` `2/2` `1/3` `RANDOM` `FLASH` `SINE` `SINE SOM` `RESPIRA` `OFF`: o desenho anda **um passo por batida** da música, pelas colunas do layout. ONDA corre com rastro (100/45/15). **SINE** é uma onda lisa correndo pelas colunas no BPM da música. **SINE SOM**: a mesma onda correndo sem parar, que acende na batida com fade e volta devagar (sobe e desce com o som). **RESPIRA** sobe na batida e desce sozinho até 15%. Cada desenho é uma sequence própria no executor do grupo (99.1, 99.2...). Desliga o FX DIM do grupo (mesmo dimmer). |
| **SUAVE** | `SECO` `0.15s` `0.3s` `0.5s` `1s`: transição entre os passos da batida (começa em 0.3s) |
| **RAPIDO** | `x1` `x2` `x4`. **x1**: um passo a cada batida que a mesa pega. A mesa costuma pegar metade das batidas (o 1º e o 3º "tum"), então **x2** põe o desenho no tempo da música e **x4** no dobro: o executor vira um **chaser** no BPM da janela Sound Input (Special Master 3.16) com Speed Mul2/Mul4. No SINE: x1 = metade do BPM, x2 = BPM, x4 = o dobro. Vale para a BATIDA e para a COR BATIDA. |
| **COR BATIDA** | `TROCA` `COR >>>` `COR <<<` `COR 2/2` `OFF`: a COR e a COR FX trocam na batida. Desliga o FX COR. Junte com FX DIM (dimmer correndo) ou com a BATIDA. |
| **NIVEL SOM** | `TUDO` `GRAVE` `MEDIO` `AGUDO` `OFF`: o dimmer dos grupos marcados segue o **volume** dessa faixa da música (forma **Sound** da MA2: SndAll, SndBass, SndMed, SndHigh). Todos os aparelhos do grupo juntos. Liga no lugar da BATIDA (mesmo dimmer). Para a onda andar e bater com o som, use o **SINE SOM**. |
| **FADE IN** | `SECO` `0.5s` `1s` `2s`: tempo de entrada quando você troca de efeito na página SOM (sem "flash"). No NIVEL SOM e no FX DIM é o fade da troca; na BATIDA, o fader do executor sobe nesse tempo. |
| **MUSICA** | `AUDIO` põe os FX da página FX dos grupos marcados no BPM da janela **Sound Input** (Special Master 3.16 "BPM"); `LIVRE` volta cada um para o seu RATE |

O botão escolhido em cada linha fica com `> NOME <` e borda verde (os ícones cobrem a cor do botão, por isso a marca no nome).

**Dicas da página SOM**

- A batida não pega o ritmo? Toque a música mais alto no PC ou suba um pouco o **Snd In**; para andar no tempo real, use **RAPIDO x2**.
- Tudo acende junto o tempo todo? O **Snd In** está alto demais: baixe.
- A luz do NIVEL SOM sobe e desce seco demais? Suba o **Snd Fade** na janela Sound Input (ele suaviza a resposta ao som).

### Colunas: como o efeito e o delay correm

O efeito e o delay correm **pela ordem do desenho** do layout, da esquerda para a direita:

- Desenho em **andares** (ex.: LED em cima e embaixo, a maioria das colunas com 2 ou mais aparelhos): os aparelhos um em cima do outro formam **uma coluna** e acendem juntos.
- Desenho em **fila**: cada aparelho é uma coluna, mesmo que dois estejam encostados. No `2/2` fica um sim, um não.
- Aparelho de várias células (strobo cluster de 16 quadrados, barra): conta como **um** aparelho, no centro do desenho dele. O strobo inteiro pisca junto.

ODD/EVEN, ESQ/DIR e os grupos do painel seguem as mesmas colunas. Mudou o desenho? Peça os grupos de seleção de novo e depois `refaz o painel` (o antigo é apagado e o novo entra no lugar).

### Pela IA

`cria o painel` monta tudo sem perguntas. Com o painel no show, pedidos curtos viram os botões dele, sem gastar a IA:

- `movings vermelho com fade de 2s` · `strobo ímpar magenta` · `par led da esquerda verde` · `grupo 113 âmbar`
- `tudo uv com delay 2s do centro pra fora` · `delay de 1s da esquerda pra direita`
- `beam vermelho e segunda cor oposta` · `cor fx azul nos beams`

O programa marca os grupos (as variáveis do painel) e aperta os botões, e o layout acende igual. Pedidos de efeito e outros mais complexos vão para a IA, que recebe o mapa do painel e usa os mesmos botões.

- `fx no ritmo da musica` (ou `fx no bpm`) · `fx no bpm livre`: põe os FX do painel no BPM da janela Sound Input e volta, sem gastar a IA.
- Pedidos de efeito, como `batida 2/2 nos strobos` ou `nivel som grave nos leds`, vão para a IA; ela recebe o mapa com todos os botões do painel (das três páginas).

```
SetVar $PPN_AUTO = "1"
SetVar $PPN_MAP  = "101,102,103,104,105,M,303,1/111,112,113,114,115,D,305,16"
                   (por tipo: ALL,ODD,EVEN,ESQ,DIR ; M = tem pan/tilt ; ícone ; células)
SetVar $PPN_PAGE = "99"
Plugin "PRISMA Painel v2.8"   -> feedback "PPN_OK ..." ou "PPN_ERRO ..."
```

O plugin grava `importexport/ppn_mapa.txt` com o número de cada botão; é ele que deixa a IA usar o painel. As variáveis do painel (SetVar) ficam salvas dentro do show: fechou e abriu o show, o painel continua funcionando.

**Atenção:** a criação usa `ClearAll`; não deixe nada importante no programmer. Os botões de DELAY/DIR gravam o delay **às cegas** (BlindEdit) e não mexem no programmer.

---

## Color picker (aposentado)

O plugin **PRISMA Color Picker v8** saiu do PRISMA (versão 1.0.8). Agora existe **um color picker só: o Painel v2.8** (acima). `cria o color picker`, `seletor de cores`, `super color picker`, `cria o painel` ou `paleta de cores no layout` criam o mesmo Painel.

- **Versões velhas no pool:** peça `instala os plugins` (ou `atualiza os plugins`). Ele apaga do pool de Plugins todo "PRISMA Color Picker" (v7, v8...) e os Painel, Layout Clone e Channel Sets que não são a versão atual, e responde "Removidos (versão velha): ...".
- **Show com um color picker v8 já criado:** continua funcionando, e os atalhos falados (`deixa tudo azul`, `vermelho com fade de 2s`) ainda apertam os botões dele se o show não tiver Painel. Só não se cria mais picker novo.

**Gelatinas** (Painel): cada cor procura a gelatina pelo nome em **todas** as bibliotecas da mesa. CTO e UV não existem na "MA colors": usa a Lee (Full C.T. Orange, Congo Blue) se ela estiver na mesa; senão, laranja e violeta da MA colors.

---

## PRISMA Layout Clone v4

Você arruma **um** aparelho no layout (ex.: o strobo 21, células 21.1 a 21.16, em cruz). O plugin copia esse desenho para os outros aparelhos.

![Resultado do Layout Clone](../imagens/21-layout-clone.png)

| Modo | O que faz |
|---|---|
| **1 · No lugar, aproximado** (padrão) | Cada aparelho recebe o desenho centrado onde já está e o conjunto é aproximado até sobrar **1 quadrado de folga** entre um desenho e outro, mantendo o arranjo e o centro do grupo |
| **2 · Grade** | O modelo na 1ª casa e os outros ao lado, 5 por linha |
| **3 · No lugar, sem aproximar** | Mantém o espaço que já estava |

Aparelho que ainda não está no layout vai para a grade.

**Pela IA:** `clona o desenho do 21 para 22 a 30 no layout 1` (acrescente `em grade` ou `sem aproximar`; `e salva no layout 5` grava em outro layout).

```
SetVar $PLC_AUTO = "1"         SetVar $PLC_MODEL = "21"
SetVar $PLC_TARGETS = "22 thru 30"   SetVar $PLC_SRC = "1"
SetVar $PLC_DST = "1"          SetVar $PLC_MODE = "1"
Plugin "PRISMA Layout Clone v4"   -> feedback "PLC_OK ..." ou "PLC_ERRO ..."
```

**À mão:** rode o plugin e responda: ID do modelo, IDs que recebem a cópia, layout onde o modelo está, layout para salvar.

**Segurança:** antes de gravar, o layout original é salvo em `importexport/pcl_backup_layout<N>.xml`. Para voltar: `Import "pcl_backup_layout<N>" At Layout <N>`.

---

## PRISMA Channel Sets v3

Dá nome às posições da roda de **cor** ou de **gobo** de um aparelho (os ChannelSets do FixtureType), olhando o aparelho aceso. É o motor da tela **F6 · Atributos**.

1. Pergunta o ID do aparelho (ex.: 201).
2. Pergunta o canal: 1 = Cor, 2 = Gobo, ou o nome do atributo. Se o aparelho tem COLOR1 e COLOR2 (ou GOBO1 e GOBO2), faz os dois.
3. Manda o DMX no canal e pergunta o que apareceu: primeiro de 1 em 1 até medir uma faixa inteira; depois pula de faixa em faixa e pergunta uma vez por faixa.
4. Grava um **FixtureType novo** (modo "<modo> PRISMA") com os nomes. Depois é só trocar o tipo dos aparelhos no Patch.

| Resposta na caixa | Faz |
|---|---|
| nome da cor/gobo (português ou inglês: vermelho = Red, estrela = Star) | dá o nome à faixa |
| Enter (vazio) | igual ao anterior |
| `giro` | começa o giro (devagar→rápido, para, outro lado): o plugin acha sozinho |
| `nome*` | esse nome vai até o fim do canal (ex.: `strobe*`) |
| `fino` | o tamanho das faixas mudou: reaprende dali, de 1 em 1 |
| `volta` | desfaz a última resposta |
| `fim` | grava o que já foi |
| X / Cancelar | cancela tudo, nada é gravado |

**Segurança:** o FixtureType original **não** é alterado. O export original fica em `prisma_cs_backup_<tipo>.xml` e o tipo novo em `prisma_cs_<tipo>.xml`.

---

## Ícones PRISMA (Image pool)

Não é plugin, é um pacote de imagens que o programa importa no **Image pool** (`importa os ícones do prisma`):

- **Aparelhos** (a partir de 301): Moving Spot, Moving Wash, Moving Beam, Spot Perfil, LED Par, Wash Flood, Ripa LED, Strobe, Blinder, Laser, Aparelho genérico.
- **Funções** (a partir de 1200): cores, shutter, prisma, FX.

Usa um bloco livre e reusa o mesmo bloco se o pacote já estiver na mesa; nunca grava por cima de imagens do show. O layout dos tipos (`cria o layout dos tipos com ícones`) e o Painel apontam para esses ícones.

---

## Problemas com plugins

| Sintoma | Solução |
|---|---|
| Aparecem duas cópias do mesmo plugin (ex.: Color Picker v7 e v8, Painel v2.0 e v2.8) | Peça `instala os plugins`: ele remove do pool as versões velhas e o Color Picker inteiro. O programa sempre procura a versão do nome (Painel v2.8, Layout Clone v4, Channel Sets v3). |
| "O plugin não entrou no Plugin pool" | Peça `instala os plugins`. Se continuar, importe à mão o `.xml` da pasta `lua-plugin` do programa. |
| Pedi o painel de novo, vai ficar duplicado? | Não: `cria o painel` (ou `refaz o painel`) apaga o painel antigo e cria o novo no lugar. Painel v1.4 antigo deixa as macros de cor no pool; apague à mão. |
| Pedi o color picker e a 2ª cor ou a seleção de grupos saiu incompleta | O show tinha grupos antigos sem os ALL/ODD/EVEN/ESQ/DIR que o Painel usa. Peça `cria os grupos de seleção` (regrava pelos layouts) e depois `refaz o painel`. |
| Efeito ou delay correndo fora de ordem | `reordena os grupos pelo layout N` ou recrie os grupos de seleção pelo layout. |
| No Painel, o `2/2` não alterna um sim, um não | Os grupos foram criados antes da versão 1.0.6 (dois aparelhos encostados viravam uma coluna). Peça os grupos de seleção de novo e depois `refaz o painel`. |
| O Painel não troca de cor quando peço falando | Peça `refaz o painel`: o painel novo grava o mapa dos botões para a IA (painéis feitos antes da 1.0.6 não têm). |
| O plugin não respondeu em 2 minutos | Feche caixas abertas na mesa e tente de novo. Com a mesa em rede, confira o Telnet. |

Mais em [Perguntas frequentes](FAQ.md).
