# Termos de Uso e Política de Privacidade · PRISMA · AI

Este é o mesmo texto que aparece no instalador do programa. [← Voltar para o README](../README.md)

Versão do documento: 2.0 (setembro de 2026)

Titular do software: Studio BRT ("Studio BRT", "nós")

Contato e encarregado de dados: audiovisualbrt@gmail.com


## RESUMO EM LINGUAGEM SIMPLES

*(não substitui o texto completo abaixo)*

- Você recebe uma licença de USO pessoal. O software continua sendo do Studio BRT: não pode ser copiado, revendido nem redistribuído.

- A IA gera comandos para a sua grandMA2 e pode errar. Quem aprova e responde pelo que roda na mesa e no palco é o operador.

- Salve o show antes de usar. Teste antes de abrir para o público.

- O login é pela sua conta Google; o acesso é conferido na comunidade do Studio BRT no Patreon.

- Seus pedidos e um resumo técnico do show vão para o provedor de IA que VOCÊ escolheu (Google), com a SUA conta.

- Para melhorar os agentes, enviamos ao Studio BRT dados de uso (e-mail, nome do computador, pedidos, resultados e erros).

- NÃO enviamos ao Studio BRT: arquivos de show, sua chave de API, senhas nem outros arquivos do seu computador.

- Você pode pedir acesso, correção ou exclusão dos seus dados pelo e-mail acima (LGPD, art. 18).


## 1. DEFINIÇÕES

1.1 "Software": o programa PRISMA · AI (antes chamado BRT Studio mAi onPC), incluindo o aplicativo, o servidor local, os agentes de IA, os prompts, os plugins BRT AI v1 e v2 para a grandMA2, as atualizações e a documentação.

1.2 "Usuário" ou "você": a pessoa que instala ou usa o Software, ou a empresa em nome da qual ele é usado.

1.3 "Mesa": o console grandMA2 ou o grandMA2 onPC controlado pelo Software.

1.4 "Provedor de IA": o serviço de inteligência artificial de terceiro usado para gerar os comandos (Google Gemini pela chave de API do Usuário, ou Antigravity CLI pela conta Google do Usuário).

1.5 "Serviço de validação": o serviço em nuvem do Studio BRT (hospedado na Cloudflare) que confere o login, a inscrição e recebe a telemetria.

1.6 "Conteúdo do Usuário": shows, patch, presets, grupos, efeitos, macros, sequences e demais dados criados na Mesa.


## 2. ACEITE E CAPACIDADE

2.1 Ao clicar em "Eu Concordo", instalar ou usar o Software, você declara que leu e aceita estes Termos. Se não concordar, clique em "Cancelar" e não use o Software.

2.2 O Software é destinado a maiores de 18 anos e a uso profissional em iluminação cênica.

2.3 Se você aceitar em nome de uma empresa, declara ter poderes para obrigá-la a estes Termos.


## 3. LICENÇA DE USO

3.1 O Studio BRT concede a você uma licença pessoal, não exclusiva, intransferível, não sublicenciável e revogável para instalar e usar o Software em computadores sob seu controle, enquanto seu acesso estiver ativo.

3.2 Não é permitido, salvo autorização por escrito:
   - a) copiar, vender, alugar, emprestar, sublicenciar ou redistribuir o Software ou partes dele;
   - b) descompilar, desmontar ou fazer engenharia reversa, exceto nos limites expressamente permitidos pela Lei 9.609/1998;
   - c) extrair, copiar ou reutilizar os prompts, as regras dos agentes ou os plugins BRT AI em outro produto;
   - d) contornar o login, o controle de acesso ou as travas de segurança do Software;
   - e) remover avisos de autoria, marca ou licença;
   - f) usar o Software para fins ilícitos ou que coloquem pessoas em risco.

3.3 O descumprimento desta cláusula encerra a licença automaticamente, sem prejuízo das medidas legais cabíveis.


## 4. PROPRIEDADE INTELECTUAL

4.1 O Software é protegido pela Lei 9.609/1998 (Lei do Software) e pela Lei 9.610/1998 (Direitos Autorais). O código, a arquitetura, os agentes, os prompts, as bases de regras, os plugins e a marca "Studio BRT" pertencem ao Studio BRT.

4.2 O Conteúdo do Usuário é seu. O Software não adquire nenhum direito sobre os seus shows.

4.3 grandMA2 e grandMA2 onPC são marcas da MA Lighting Technology GmbH. O Studio BRT não é afiliado, patrocinado nem endossado pela MA Lighting. Google, Gemini, Antigravity, Patreon, Cloudflare e GitHub são marcas de seus titulares.

4.4 O Software inclui componentes de código aberto (por exemplo Electron, Node.js e as fontes Roboto, sob licença SIL OFL), regidos por suas próprias licenças.


## 5. ACESSO E CONTA

5.1 O acesso é feito com a sua conta Google. O Serviço de validação confere a conta e a sua inscrição (gratuita ou paga) na comunidade do Studio BRT no Patreon.

5.2 Após a validação, o Software cria uma sessão local, assinada com uma chave gerada no seu próprio computador.

5.3 Algumas funções podem depender do tipo de inscrição. Se a inscrição for encerrada, o acesso pode ser suspenso.

5.4 Você é responsável pela segurança da sua conta Google e do computador onde o Software está instalado.


## 6. COMO O SOFTWARE FUNCIONA (TRANSPARÊNCIA TÉCNICA)

6.1 Servidor local: o Software roda um servidor em 127.0.0.1, porta 3000, acessível somente pelo próprio computador.

6.2 Conexão com a Mesa: o Software conecta à Mesa por Telnet no endereço configurado (padrão 127.0.0.1, porta 30000) e faz login automaticamente com o usuário "Administrator" padrão do onPC. Se a sua Mesa usar outra senha ou usuário, ajuste antes.

6.3 Leitura do show: ao iniciar, o Software LÊ o patch, os pools (grupos, presets, macros, efeitos, sequences, layouts, executors) e os plugins. A leitura não altera o show.

6.4 Escrita no show: o Software só grava na Mesa ao executar comandos de um pedido. No plugin BRT AI v1 os comandos rodam direto; no BRT AI v2 o plano é mostrado e só roda após a sua aprovação.

6.5 Arquivos no computador: o Software copia os plugins BRT AI para a pasta de plugins da grandMA2 (ProgramData) quando eles faltam na Mesa, e lê a biblioteca de aparelhos da grandMA2 para obter valores de cor, gobo, lâmpada e reset.

6.6 Travas de segurança: antes de enviar, o Software bloqueia gravações no pool de plugins, atributos inexistentes no patch e presets vazios. Essas travas reduzem, mas não eliminam, o risco de comandos indesejados.

6.7 Atualizações: o Software procura versões novas no repositório público do Studio BRT no GitHub, baixa em segundo plano e instala quando você reinicia. Ele também pode baixar versões novas dos prompts dos agentes pelo Serviço de validação.


## 7. INTELIGÊNCIA ARTIFICIAL

7.1 Você escolhe o Provedor de IA: modo "Chave API" (Google Gemini, com a sua chave) ou modo "CLI" (Antigravity, com a sua conta Google). A relação com o Provedor de IA, incluindo cotas, limites, custos e termos de uso, é entre você e o Provedor.

7.2 Para gerar os comandos, o Software envia ao Provedor de IA: o texto do seu pedido, as instruções dos agentes e um resumo técnico do show (tipos e números de aparelhos, atributos, nomes e números de grupos, presets, macros, efeitos e sequences).

7.3 O tratamento feito pelo Provedor de IA segue as políticas dele. O Studio BRT não controla esse tratamento.

7.4 Respostas de IA são probabilísticas e podem conter erros, comandos inadequados ou resultados diferentes para o mesmo pedido. O Software não garante nenhum resultado específico.

7.5 Não coloque dados pessoais, senhas ou informações sigilosas de terceiros nos pedidos.


## 8. RESPONSABILIDADE DO OPERADOR E SEGURANÇA DE PALCO

8.1 O Software é uma ferramenta de assistência. A operação, a conferência dos comandos e a segurança do palco, do público, da equipe e dos equipamentos são de responsabilidade exclusiva do operador.

8.2 Antes de usar: salve o show, faça cópias de segurança e teste os resultados antes de qualquer apresentação.

8.3 Comandos de lâmpada, reset, movimento, intensidade, strobe e efeitos atuam em equipamentos reais. Nunca use o Software como único meio de controle ou de segurança, e cumpra as normas de segurança elétrica e de trabalho aplicáveis.


## 9. PRIVACIDADE E PROTEÇÃO DE DADOS (LGPD - LEI 13.709/2018)

9.1 Controlador: Studio BRT. Encarregado (contato para assuntos de dados pessoais): audiovisualbrt@gmail.com.

9.2 Dados tratados, finalidade e base legal:
   - a) Acesso: e-mail e identificador da conta Google e situação da inscrição no Patreon. Finalidade: autenticar e liberar o acesso. Base legal: execução de contrato (art. 7º, V).
   - b) Telemetria de uso: e-mail, nome do computador, data e hora, agente usado, texto do pedido, resultado, quantidade de comandos gerados, mensagens de erro e eventos de sessão. Finalidade: suporte, correção de falhas e melhoria dos agentes. Base legal: legítimo interesse (art. 7º, IX). Você pode se opor pelo e-mail do encarregado.
   - c) Dados que ficam SÓ no seu computador: configuração (modo de IA, chave de API, endereço da Mesa), chave da sessão, logs e uma cópia local da telemetria, em `AppData\Roaming\BRT Studio`, `AppData\Roaming\StudioBRT` e `AppData\Roaming\brt-studio-mai-onpc`.
   - d) Dados enviados ao Provedor de IA: conforme a cláusula 7.2, sob a sua conta com o Provedor.

9.3 O Studio BRT NÃO coleta: arquivos de show, sua chave de API, senhas, conteúdo de outras pastas do computador nem dados de pagamento (pagamentos são processados pelo Patreon).

9.4 Compartilhamento: para funcionar, o Software usa fornecedores que tratam dados em nome do Studio BRT ou de forma independente: Cloudflare (Serviço de validação), GitHub (armazenamento da telemetria e distribuição de atualizações), Google (login e IA) e Patreon (verificação da inscrição). O Studio BRT não vende dados pessoais.

9.5 Transferência internacional: esses fornecedores podem tratar dados fora do Brasil, com base nas hipóteses do art. 33 da LGPD e nas garantias contratuais oferecidas por eles.

9.6 Retenção: a telemetria é mantida pelo tempo necessário às finalidades acima, por no máximo 24 meses, e depois excluída ou anonimizada. Dados de acesso são mantidos enquanto a conta estiver ativa.

9.7 Seus direitos (art. 18): confirmação e acesso aos dados, correção, anonimização, bloqueio ou eliminação de dados desnecessários, portabilidade, informação sobre compartilhamento, revogação do consentimento quando aplicável e oposição ao tratamento. Peça pelo e-mail do encarregado. Você também pode reclamar à ANPD.

9.8 Segurança: a comunicação com os serviços em nuvem usa HTTPS; tokens de serviços do Studio BRT ficam no Serviço de validação, não no instalador; a chave da sessão é gerada em cada computador; o servidor local só aceita conexões do próprio computador.


## 10. DISPONIBILIDADE E ALTERAÇÕES DO SOFTWARE

10.1 Os serviços online (login, validação, IA, atualizações) podem ficar indisponíveis por manutenção, falhas de terceiros ou falta de internet. Não há garantia de disponibilidade contínua.

10.2 O Studio BRT pode alterar, incluir ou remover funções nas atualizações.


## 11. GARANTIAS E LIMITAÇÃO DE RESPONSABILIDADE

11.1 O Software é fornecido "no estado em que se encontra", sem garantia de que funcione sem erros ou atenda a uma finalidade específica.

11.2 Na máxima extensão permitida pela lei, o Studio BRT não responde por danos indiretos, lucros cessantes, perda de show, de dados ou de apresentação, nem por danos a equipamentos decorrentes de comandos executados na Mesa. Quando houver responsabilidade, ela fica limitada ao valor pago pelo Usuário ao Studio BRT nos 12 meses anteriores ao fato.

11.3 Nada nestes Termos afasta direitos garantidos ao consumidor pelo Código de Defesa do Consumidor, quando aplicável.


## 12. ENCERRAMENTO

12.1 Você pode deixar de usar o Software a qualquer momento, desinstalando-o pelo Windows. Os dados locais podem ser apagados removendo as pastas indicadas na cláusula 9.2(c).

12.2 O Studio BRT pode suspender ou encerrar o acesso em caso de violação destes Termos ou fim da inscrição.


## 13. ALTERAÇÕES DESTES TERMOS

Estes Termos podem ser atualizados. A versão vigente acompanha o

instalador e as atualizações do Software. Mudanças relevantes

sobre dados pessoais serão informadas antes de entrarem em vigor.


## 14. DISPOSIÇÕES GERAIS

14.1 Estes Termos são regidos pelas leis da República Federativa do Brasil.

14.2 Fica eleito o foro do domicílio do Usuário para resolver qualquer controvérsia.

14.3 Se alguma cláusula for considerada inválida, as demais continuam válidas. A tolerância com um descumprimento não significa renúncia ao direito.

Studio BRT - Dando forma ao futuro do entretenimento.
