# Perguntas frequentes · PRISMA · AI

[← Voltar para o README](../README.md) · [Manual de comandos](MANUAL.md) · [Guia do Painel](PAINEL.md) · [Plugins](PLUGINS.md)

---

## Instalação e acesso

### O Windows diz que protegeu o computador. É vírus?

Não. O aviso "O Windows protegeu o computador" (SmartScreen) aparece para todo programa novo que ainda não tem **assinatura digital paga** e poucos downloads. Clique em **Mais informações** → **Executar assim mesmo**. O navegador também pode dizer "normalmente não é baixado": no Edge, **···** → **Manter** → **Manter assim mesmo**; no Chrome, **Manter**.

Para ter certeza de que o arquivo é o original, confira o SHA-256 que aparece na página da versão:

```
certutil -hashfile PRISMA_AI_1.0_RC_rev041026_Setup.exe SHA256
```

Baixe só da página oficial: <https://github.com/BRT-STUDIO01/Prisma-ai/releases/latest>.

### Aparece "acesso negado" ao entrar

O e-mail do Patreon tem que ser o **mesmo** da conta Google que você usa no programa, e você precisa ser **membro** da página do [Studio BRT](https://www.patreon.com/c/StudioBRT) (o plano gratuito basta). Confira os dois e entre de novo. Continua? Escreva para **audiovisualbrt@gmail.com**.

### Quanto custa?

Nesta fase (1.0 RC) é **grátis por tempo limitado** para membros do Studio BRT no Patreon. O motor de IA usa a **sua** conta Google (chave Gemini ou Antigravity CLI). Quando a gratuidade mudar, o aviso sai antes no Patreon.

### Precisa de administrador para instalar?

Não. O programa é instalado só para o seu usuário.

---

## Conexão com a mesa

### Cliquei em INICIAR e não conecta

1. A grandMA2 onPC está aberta, com um show carregado?
2. O Telnet está ligado? **Setup → Console → Global Settings → Telnet = Login Enabled**.
3. Mesa em outro PC: rede **Privada**, porta 30000 liberada no firewall e o IP certo em **MESA → Endereço**.
4. Teste a porta: `Test-NetConnection <IP> -Port 30000` precisa dar `TcpTestSucceeded : True`.

### Conecta, mas nada funciona (Error #43 LOGIN NEEDED)

O programa entra na mesa como **Administrator** (senha `admin`, o padrão da MA2) e, se não der, tenta sem senha. Um show que veio de outro operador pode ter outra senha. O terminal mostra "NAO CONSEGUI ENTRAR NA MESA". Duas saídas:

- Na grandMA2, **Setup → Users**: confira ou volte a senha do Administrator para `admin`.
- Ou coloque o usuário e a senha desse show no `config.env` (`AppData\Roaming\BRT Studio\config.env`): `MA2_USUARIO=nome` e `MA2_SENHA=senha`. Depois clique em PARAR e INICIAR.

### O painel mostra "bridge parado" / "não lido"

O programa ainda não foi iniciado. Clique em **INICIAR**. Depois de mexer na mesa à mão, use **F1 · Reanalisar show** (ou peça `analise`).

### Mudei uma coisa no programa e nada mudou

**INICIAR/PARAR** só liga e desliga a conexão com a mesa. Depois de uma atualização, feche o programa por completo e abra de novo.

---

## Pedidos para a IA

### A IA criou coisa errada / no aparelho errado

- Use um **prefixo** (`cor:`, `efeito:`, `cena:`...) para escolher o especialista certo. Veja o [manual](MANUAL.md#2-como-pedir-prefixos).
- Diga **em quem**: nome do grupo ou `Fixture 11 Thru 20`.
- Prefira o **BRT AI v2**: ele mostra a lista antes de criar.
- Se mexeu no show à mão, peça `analise` antes.

### "Frente" saiu para trás nos movings

Grave a **REF FRENTE**: aponte os movings para a frente e `Store Preset 2.101 "REF FRENTE"`. A IA monta as outras posições a partir dela.

### A IA vai apagar o que eu já programei?

Não. Preset, sequence, executor, macro, efeito, grupo ou layout ocupado: o novo vai para o próximo número livre. A única exceção é o painel: pedir `cria o painel` de novo apaga o painel antigo (só o que é dele) e põe o novo no lugar. O Layout Clone faz backup do layout antes de gravar. Mesmo assim, **salve o show antes** de usar.

### Pedi laser/vídeo/facas e ele recusou

O programa recusa na hora o que o rig não tem no patch (sem laser, sem media server, sem shapers), sem gastar a IA.

### Pedido de timecode não funciona

O agente de timecode está **trancado** nesta versão (em desenvolvimento).

---

## Color picker e grupos

### Pedi "cria o color picker" e veio o Painel

É isso mesmo. Desde a 1.0.8 existe **um color picker só: o PRISMA Painel v2.8**. `cria o color picker`, `seletor de cores`, `super color picker`, `cria o painel` e `paleta de cores no layout` criam o mesmo Painel (seleção de grupos + cor, 2ª cor, fade, delay, FX e rate). `color picker dos grupos 101 e 111 na pagina 2` faz o Painel só com as linhas desses grupos, na página 2.

### Pedi o painel de novo, vai duplicar?

Não. Se o show já tem painel, `cria o painel` (ou `refaz o painel`, `recria o painel`, `atualiza o painel`, `cria o color picker`) apaga o antigo antes (macros, layouts "PRISMA Painel", sequences, presets e efeitos "PPN ..." e desliga os executores dele) e cria o novo no lugar. Painel v1.4 antigo, sem o mapa dos botões: layouts, sequences, efeitos e macros "PPN" escondidas saem, mas as macros de cor antigas ficam no pool; apague essas à mão.

### Tenho Color Picker v7/v8 e Painel v1.4 no pool de Plugins

Peça `instala os plugins` (ou `atualiza os plugins`). Ele apaga do pool todo "PRISMA Color Picker" e os Painel, Layout Clone e Channel Sets que não são a versão atual (Painel v2.8, Layout Clone v4, Channel Sets v3), instala o que faltar e responde "Removidos (versão velha): ...". Um color picker v8 já criado num show antigo continua funcionando, e os atalhos falados (`deixa tudo azul`) ainda usam ele se o show não tiver Painel.

### O CTO saiu verde ou o UV não acendeu

As versões antigas procuravam essas cores só na biblioteca "MA colors", que não tem CTO nem UV. O Painel procura em todas as bibliotecas de gelatina (Lee Full C.T. Orange e Congo Blue, ou laranja e violeta da MA colors). Peça `refaz o painel`.

### No Painel, o 2/2 não alterna um sim, um não

Dois aparelhos encostados no desenho entravam na mesma coluna e piscavam juntos (ex.: 10 strobos davam 6 × 4). Na 1.0.6, numa fila cada aparelho é uma coluna. Peça os grupos de seleção de novo e depois `refaz o painel`.

### Peço "movings azul" e o Painel não muda

O painel precisa ter sido criado na 1.0.6 ou depois: é ela que grava o mapa dos botões que a IA usa. Peça `refaz o painel` e reinicie o programa se ele estava aberto.

### Fechei e abri o show: o painel ainda funciona?

Sim. A MA salva dentro do show as variáveis do painel (SetVar), então os botões continuam marcando e acendendo depois de reabrir.

### O show tinha grupos antigos e o painel (ou a 2ª cor) saiu incompleto

O Painel usa os grupos ALL, ODD, EVEN, ESQ e DIR de cada tipo como botões de seleção. Num show sem grupos o PRISMA cria todos sozinho; se o show já tinha grupos antigos, peça `cria os grupos de seleção` (regrava pelos layouts) e depois `refaz o painel`.

### ODD/EVEN ou o delay saem fora de ordem

Os grupos seguem o desenho do layout, da esquerda para a direita, por **colunas** (aparelhos um em cima do outro num desenho em andares contam como uma coluna). Recrie os grupos de seleção **pelo layout** onde os aparelhos estão desenhados (`... pelos layouts 1 2 3`). Depois peça `refaz o painel`: ele guarda os aparelhos dos grupos na hora em que é criado.

### Os strobos de várias células ficaram longe demais no layout

Peça `clona o desenho do <modelo> para <outros> no layout <N>`. O clone aproxima os aparelhos até sobrar 1 quadrado de folga. Para manter o espaço original, acrescente `sem aproximar`.

---

## Página SOM do painel (música)

### Atualizei o PRISMA e o painel continua igual

O painel fica gravado no show. Depois de atualizar, clique em **INICIAR** (o plugin novo entra no pool sozinho) e peça `refaz o painel`: o antigo é apagado e o novo, com as três páginas (COR, FX e SOM), entra no lugar.

### A batida não acompanha a música / pega só metade

A BATIDA anda um passo a cada batida que a mesa **ouve** pelo Sound Input, e ela costuma pegar só o 1º e o 3º "tum". Aperte **RAPIDO x2** para andar no tempo da música (x4 = o dobro). Confira também se o som chega na mesa: na janela **Sound Input**, o medidor tem que mexer com a música.

### O NIVEL SOM acende tudo junto, o tempo todo

O **Snd In** (ganho do Sound Input) está alto: todas as faixas ficam no pico. Deixe baixo, uns 5 a 15%, e aumente aos poucos. Se a luz sobe e desce seco demais, suba o **Snd Fade** na mesma janela.

### Troquei de efeito e deu um "flash"

Escolha um tempo no **FADE IN** (0.5s, 1s ou 2s): o efeito novo entra com fade. Na BATIDA o fader do executor sobe nesse tempo.

### Com RAPIDO x2 ou x4 a batida passa para outros desenhos

Isso acontecia antes do Painel v2.4, quando todos os desenhos ficavam numa sequence só. Peça `refaz o painel`: no painel novo cada desenho tem a sua sequence.

### Quero a onda andando e subindo/descendo com o som

Use **BATIDA → SINE SOM**: a onda corre sem parar (como o SINE) e acende na batida: sobe a 100% com fade (0.25 s) e volta devagar a 30% (0.9 s) até a próxima batida. O **SINE** sozinho só corre pela fila (no BPM da música, sem acompanhar o volume). O **NIVEL SOM** (TUDO, GRAVE, MEDIO, AGUDO) acende todos os aparelhos do grupo juntos e desliga a BATIDA: os dois usam o mesmo dimmer, e a grandMA2 não mistura dois efeitos de intensidade de executores diferentes (vale o maior).

### O RESPIRA fica piscando sem parar

Painel v2.6 ou anterior: a volta da sequence não esperava a batida. Peça `refaz o painel` (v2.7 ou mais nova): ele sobe na batida e desce sozinho até 15%, e espera a próxima batida.

### Não sei qual botão está ligado na página SOM

O botão escolhido em cada linha mostra o nome entre `> <` (ex.: `> GRAVE <`) com borda verde. Painel antigo sem essa marca: peça `refaz o painel`.

## Stage 3D (Capture)

### Os aparelhos não entram no patch

Deixe aberta na mesa a janela **Setup → Patch & Fixture Schedule** enquanto o programa cria. Depois feche e responda **SIM**.

### As posições aparecem 0 0 0

Com o Patch aberto a MA2 mostra 0 0 0. Feche o Patch (SIM) e clique em ↻ para reler.

### "Nenhum tipo da biblioteca bate com os canais do Capture"

Clique em **CRIAR TIPO**: o programa monta o FixtureType a partir dos canais do Capture. Confira os canais marcados com **CONFIRA** e clique em **GRAVAR NA BIBLIOTECA**.

---

## Privacidade

### O que vai para a internet?

Seus pedidos e um resumo técnico do show vão para o provedor de IA que você escolheu (Google), com a sua conta. O Studio BRT recebe dados de uso (e-mail, nome do computador, pedidos, resultados e erros) para melhorar os agentes. **Não** são enviados arquivos de show, chave de API, senhas nem outros arquivos do computador. Pedidos de acesso, correção ou exclusão de dados: **audiovisualbrt@gmail.com** (LGPD, art. 18).

---

Não achou a resposta? **audiovisualbrt@gmail.com** · Vídeos: **[YouTube @BRTAPRESENTA](https://www.youtube.com/@BRTAPRESENTA)**
