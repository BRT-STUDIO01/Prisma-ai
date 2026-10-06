# Perguntas frequentes · PRISMA · AI

[← Voltar para o README](../README.md) · [Manual de comandos](MANUAL.md) · [Plugins](PLUGINS.md)

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

Não. Preset, sequence, executor, macro, efeito, grupo ou layout ocupado: o novo vai para o próximo número livre. O Layout Clone faz backup do layout antes de gravar. Mesmo assim, **salve o show antes** de usar.

### Pedi laser/vídeo/facas e ele recusou

O programa recusa na hora o que o rig não tem no patch (sem laser, sem media server, sem shapers), sem gastar a IA.

### Pedido de timecode não funciona

O agente de timecode está **trancado** nesta versão (em desenvolvimento).

---

## Color picker e grupos

### O color picker veio gigante, uma linha para cada grupo

Desde a v7 o color picker usa **uma linha por tipo** (os grupos "… ALL"). Atualize os plugins (`instala os plugins`), apague o picker antigo e peça `cria o color picker` de novo.

### O color picker não tem a 2ª cor (SPLIT)

A 2ª cor usa os grupos EVEN, DIR e PONTAS de cada tipo. Peça antes `cria os grupos de seleção pelos layouts 1 2 3` (com os números dos seus layouts) e depois o color picker.

### ODD/EVEN ou o delay saem fora de ordem

Os grupos seguem o desenho do layout. Recrie os grupos de seleção **pelo layout** onde os aparelhos estão desenhados (`... pelos layouts 1 2 3`). Se o desenho tem várias fileiras (cobra, V, zigue-zague), numere os aparelhos acompanhando o desenho: o programa usa essa numeração. Depois recrie o color picker (ele guarda os aparelhos dos grupos na hora em que é criado).

### Os strobos de várias células ficaram longe demais no layout

Peça `clona o desenho do <modelo> para <outros> no layout <N>`. O clone aproxima os aparelhos até sobrar 1 quadrado de folga. Para manter o espaço original, acrescente `sem aproximar`.

---

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
