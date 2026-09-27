# D2 — Perímetro regulatório

> AVISO DE COBERTURA: neste run, `bcb.gov.br` (páginas institucionais/`exibenormativo`) respondeu como SPA vazia, e `planalto.gov.br` e `in.gov.br` falharam com erro de conexão (ECONNRESET / socket hang up) em todas as tentativas. A única via primária que funcionou foi o repositório de PDFs `normativos.bcb.gov.br`. Consequência: **o texto da Resolução BCB nº 80/2021 NÃO foi recuperado neste run** — capital mínimo por modalidade e limiares de volume ficam como lacuna declarada, não como afirmação. Tudo que segue como "Claim" tem texto normativo lido nesta sessão.

## Claims

- **A Resolução Conjunta nº 1, de 4/5/2020 (BCB + CMN), é a norma que implanta o Open Finance e se aplica a "instituições financeiras, instituições de pagamento e demais instituições autorizadas a funcionar pelo Banco Central do Brasil" (art. 1º) — ou seja, o universo de participantes é, por definição, o de entidades autorizadas pelo BCB.**
  - source: https://normativos.bcb.gov.br/Lists/Normativos/Attachments/51028/Res_Conj_0001_v4_P.pdf
  - publisher: Banco Central do Brasil / Conselho Monetário Nacional (repositório oficial de normativos)
  - pub_date: 2020-05-04 (texto consolidado; redação vigente do art. 1º dada pela Resolução Conjunta nº 4, de 24/3/2022, com efeitos a partir de 2/5/2022)
  - accessed: 2026-08-19
  - confidence: alta
  - class: regulatory

- **A Resolução Conjunta nº 1/2020 está VIGENTE e consolidada; a última alteração identificada no próprio texto é a Resolução Conjunta nº 4, de 24/3/2022 (efeitos a partir de 2/5/2022), que trocou "Open Banking" por "Open Finance" em todo o normativo; houve alteração anterior pela Resolução Conjunta nº 3, de 24/6/2021.**
  - source: https://normativos.bcb.gov.br/Lists/Normativos/Attachments/51028/Res_Conj_0001_v4_P.pdf
  - publisher: Banco Central do Brasil / CMN
  - pub_date: 2020-05-04 (consolidação "v4"; alterações marcadas até 2022-03-24)
  - accessed: 2026-08-19
  - confidence: média-alta (o arquivo consolidado lido é a versão "v4"; não consegui, dentro do orçamento, cruzar com a busca de normativos do BCB para descartar uma versão posterior a 2022)
  - class: regulatory

- **A Resolução Conjunta nº 1/2020 se apoia expressamente no art. 9º, caput e inciso II, da Lei nº 12.865, de 9/10/2013 (e no art. 4º, VIII, e art. 9º da Lei nº 4.595/1964) — confirmando que a competência do BCB sobre instituições de pagamento tem base na Lei 12.865/2013.**
  - source: https://normativos.bcb.gov.br/Lists/Normativos/Attachments/51028/Res_Conj_0001_v4_P.pdf (preâmbulo)
  - publisher: Banco Central do Brasil / CMN
  - pub_date: 2020-05-04
  - accessed: 2026-08-19
  - confidence: alta
  - class: regulatory

- **O ITP é definido no art. 2º, VI, da Resolução Conjunta nº 1/2020 como "instituição participante que presta serviço de iniciação de transação de pagamento SEM DETER EM MOMENTO ALGUM OS FUNDOS TRANSFERIDOS na prestação do serviço" — a não-custódia é elemento constitutivo da modalidade, não uma escolha de arquitetura.**
  - source: https://normativos.bcb.gov.br/Lists/Normativos/Attachments/51028/Res_Conj_0001_v4_P.pdf
  - publisher: Banco Central do Brasil / CMN
  - pub_date: 2020-05-04
  - accessed: 2026-08-19
  - confidence: alta
  - class: regulatory

- **O serviço de iniciação de transação de pagamento é definido (art. 2º, VII, redação da Res. Conj. nº 4/2022, vigente desde 2/5/2022) como o serviço que possibilita a iniciação da instrução de uma transação de pagamento, ordenado pelo cliente, relativamente a conta de depósitos ou de pagamento pré-paga, "comandada por instituição NÃO DETENTORA DA CONTA à instituição que a detém".**
  - source: https://normativos.bcb.gov.br/Lists/Normativos/Attachments/51028/Res_Conj_0001_v4_P.pdf
  - publisher: Banco Central do Brasil / CMN
  - pub_date: 2022-03-24 (redação alterada; efeitos 2022-05-02)
  - accessed: 2026-08-19
  - confidence: alta
  - class: regulatory

- **No compartilhamento do serviço de iniciação de pagamento, o art. 6º, II, da Res. Conj. nº 1/2020 define como participantes obrigatórios apenas (a) as instituições detentoras de conta e (b) as instituições iniciadoras de transação de pagamento — o papel de ITP é ocupado por instituição participante, isto é, do rol do art. 1º (autorizadas a funcionar pelo BCB).**
  - source: https://normativos.bcb.gov.br/Lists/Normativos/Attachments/51028/Res_Conj_0001_v4_P.pdf
  - publisher: Banco Central do Brasil / CMN
  - pub_date: 2020-05-04
  - accessed: 2026-08-19
  - confidence: alta (quanto ao texto); média (quanto à inferência de que isso, por si só, exige autorização específica na modalidade ITP — a exigência de autorização e o capital mínimo estão na Res. BCB nº 80/2021, não recuperada neste run)
  - class: regulatory

- **O compartilhamento de DADOS (art. 5º, I) é obrigatório apenas para instituições dos Segmentos S1 e S2 da Resolução nº 4.553/2017 (art. 6º, I, "a") e VOLUNTÁRIO para as demais instituições do art. 1º (art. 6º, I, "b"), sendo que a adesão voluntária pressupõe disponibilizar interface dedicada como instituição transmissora (art. 6º, §3º) — regime de reciprocidade.**
  - source: https://normativos.bcb.gov.br/Lists/Normativos/Attachments/51028/Res_Conj_0001_v4_P.pdf
  - publisher: Banco Central do Brasil / CMN
  - pub_date: 2020-05-04
  - accessed: 2026-08-19
  - confidence: alta
  - class: regulatory

- **Toda instituição participante deve registrar sua participação no repositório de participantes mantido por sistema eletrônico (art. 7º c/c art. 44, VI) — há barreira operacional de registro além da autorização.**
  - source: https://normativos.bcb.gov.br/Lists/Normativos/Attachments/51028/Res_Conj_0001_v4_P.pdf
  - publisher: Banco Central do Brasil / CMN
  - pub_date: 2020-05-04
  - accessed: 2026-08-19
  - confidence: alta
  - class: regulatory

- **A "agregação de dados" é expressamente definida no art. 2º, XII, como "consolidação de dados compartilhados de acordo com o disposto nesta Resolução Conjunta com a finalidade de prestar serviços aos seus clientes" — logo, agregar dados de Open Finance é atividade prevista na norma e exercida por instituição participante (receptora de dados), não atividade livre por fora do arranjo.**
  - source: https://normativos.bcb.gov.br/Lists/Normativos/Attachments/51028/Res_Conj_0001_v4_P.pdf
  - publisher: Banco Central do Brasil / CMN
  - pub_date: 2020-05-04
  - accessed: 2026-08-19
  - confidence: alta
  - class: regulatory

- **A instituição receptora de dados ou iniciadora deve identificar o cliente e obter consentimento prévio (art. 10), com finalidades determinadas e prazo de validade limitado a doze meses (art. 10, §1º, III), discriminando instituição e dados/serviços objeto do compartilhamento.**
  - source: https://normativos.bcb.gov.br/Lists/Normativos/Attachments/51028/Res_Conj_0001_v4_P.pdf
  - publisher: Banco Central do Brasil / CMN
  - pub_date: 2020-05-04
  - accessed: 2026-08-19
  - confidence: alta
  - class: regulatory

- **O escopo obrigatório do Open Finance abrange, quanto a SERVIÇOS, apenas dois: (a) iniciação de transação de pagamento e (b) encaminhamento de proposta de operação de crédito (art. 5º, II) — conciliação, contas a pagar/receber, ERP e relatórios não integram o escopo de serviços do Open Finance.**
  - source: https://normativos.bcb.gov.br/Lists/Normativos/Attachments/51028/Res_Conj_0001_v4_P.pdf
  - publisher: Banco Central do Brasil / CMN
  - pub_date: 2020-05-04
  - accessed: 2026-08-19
  - confidence: alta
  - class: regulatory

- **O compartilhamento de dados cadastrais exclui expressamente dados pessoais sensíveis, notas/pontuações de crédito e credenciais de autenticação (art. 5º, §4º, I, "a" a "c") — restrição relevante para produtos de score/credit-scoring construídos sobre Open Finance.**
  - source: https://normativos.bcb.gov.br/Lists/Normativos/Attachments/51028/Res_Conj_0001_v4_P.pdf
  - publisher: Banco Central do Brasil / CMN
  - pub_date: 2020-05-04
  - accessed: 2026-08-19
  - confidence: alta
  - class: regulatory

- **O histórico mínimo de transações compartilhado é de doze meses (art. 5º, §5º, II) — teto informacional para produtos de gestão financeira/PFM/BFM baseados em Open Finance.**
  - source: https://normativos.bcb.gov.br/Lists/Normativos/Attachments/51028/Res_Conj_0001_v4_P.pdf
  - publisher: Banco Central do Brasil / CMN
  - pub_date: 2020-05-04
  - accessed: 2026-08-19
  - confidence: alta
  - class: regulatory

## Mapa da linha regulatória

Legenda de base: **[E]** = coluna sustentada por texto normativo lido neste run; **[I]** = inferência a partir do texto lido, ainda não confirmada no dispositivo específico; **[NV]** = não verificado neste run (crença não verificada — tratar como hipótese a checar).

| Atividade | Precisa de autorização do BCB? | Norma que manda | Como um software fica do lado de fora |
|---|---|---|---|
| Conciliação financeira (bater extrato/adquirência contra ERP) | Não **[I]** — não há custódia, não há conta de pagamento, não há iniciação; fora do escopo de serviços do Open Finance (art. 5º, II) **[E]** | Lei 12.865/2013 delimita instituição de pagamento **[NV: texto não recuperado]**; Res. Conj. 1/2020 art. 5º, II **[E]** | Ler dados que o cliente já possui (arquivos, OFX/CNAB, API do PSP do próprio cliente) e apenas comparar/relatar; nunca receber ou movimentar recursos |
| Contas a pagar / contas a receber (agenda, aprovação, relatório) | Não **[I]** | idem | Manter o produto como camada de decisão e registro; o pagamento é executado pelo banco/PSP do cliente, com o dinheiro sempre em conta do cliente |
| Emissão de cobrança/boleto/PIX via PSP licenciado de terceiro | Não, para o software **[I]** — a licença é do PSP; o software é integrador | Res. Conj. 1/2020 confirma que o rol de participantes/autorizados é fechado às instituições do art. 1º **[E]**; requisitos de autorização em Res. BCB 80/2021 **[NV]** | Liquidação sempre na conta do PSP em nome do cliente final (split/subconta do PSP), nunca em conta do software; o software não pode ter posse nem poder de disposição sobre o recurso de terceiro |
| Custódia de recursos de terceiros / conta de pagamento pré-paga própria | Sim **[I], gatilho clássico** — a definição de ITP exige "sem deter em momento algum os fundos transferidos" (art. 2º, VI), o que confirma que deter fundos empurra para outra modalidade **[E]** | Res. BCB 80/2021 (requisitos e procedimentos de autorização) **[NV]**; Lei 12.865/2013 **[NV]** | Não fazer. Se precisar de saldo/escrow, usar BaaS/PSP licenciado como titular do arranjo e da conta |
| Liquidação em nome próprio / receber em conta da empresa e repassar ao cliente | Sim **[I]** | idem acima **[NV]** | Não fazer, nem "temporariamente". Este é o erro mais caro e mais comum |
| Iniciação de pagamento (ITP) construída pela própria startup | Sim **[I], alta plausibilidade]** — ITP é "instituição participante" e participantes são instituições autorizadas a funcionar pelo BCB (art. 1º c/c art. 2º, VI, art. 6º, II) **[E]**; capital mínimo e rito na Res. BCB 80/2021 **[NV]** | Res. Conj. 1/2020, arts. 1º, 2º VI, 6º II, 7º **[E]** | Consumir ITP de terceiro já autorizado (o software vira canal/parceiro tecnológico do ITP), em vez de pedir autorização própria |
| Agregação de dados bancários via Open Finance (AISP/receptora) | Sim para ser a instituição receptora **[I]** — receptora é "instituição participante" (art. 2º, IV) e deve registrar-se no repositório (art. 7º) **[E]** | Res. Conj. 1/2020, arts. 1º, 2º IV/XII, 6º, 7º, 10 **[E]** | Contratar agregador já autorizado/participante (ex.: Pluggy, Belvo, Klavi — **[NV]**, status de autorização de cada um não verificado neste run) e consumir a API dele; o consentimento do art. 10 é obtido no fluxo do participante |
| Gestão financeira para PME / ERP financeiro / relatórios / automação | Não **[I]** | fora do escopo de serviços do art. 5º, II **[E]** | SaaS puro sobre dados do próprio cliente; sem conta, sem saldo, sem movimentação |
| Score de crédito próprio a partir de dados de Open Finance | Não é atividade autorizada em si **[I]**, mas o insumo é restrito: score e dado sensível estão excluídos do compartilhamento (art. 5º, §4º, I) **[E]** | Res. Conj. 1/2020, art. 5º, §4º **[E]** | Derivar sinais dos dados transacionais compartilhados (12 meses, art. 5º, §5º, II), não importar score de terceiros pelo canal do Open Finance |
| Concessão de crédito com capital próprio (BNPL, antecipação) | Sim / rota alternativa **[NV]** — atividade privativa de instituição financeira; existe rota via SCD/SEP e via FIDC, não verificada neste run | **[NV]** | Fora do escopo desta rodada — precisa de rodada dedicada antes de qualquer decisão |

## Pistas

- **Entidade nova (alta prioridade):** Resolução Conjunta nº 4, de 24/3/2022 — rebatiza Open Banking para Open Finance e altera a definição do serviço de iniciação (art. 2º, VII), com efeitos desde 2/5/2022. Qualquer material anterior a maio/2022 usa vocabulário desatualizado.
- **Entidade nova:** Resolução Conjunta nº 3, de 24/6/2021 (alterou art. 6º, III, e §1º).
- **Entidade nova:** Resolução BCB nº 81, de 25/3/2021 — apareceu em resultado de busca como norma que disciplina processos de autorização de instituições de pagamento, ao lado da Res. BCB nº 80/2021. Status e conteúdo **não verificados**; provável par normativo (80 = requisitos/condições, 81 = procedimentos). Verificar na próxima rodada.
- **Entidade:** Circular BCB nº 3.885, de 26/3/2018 — norma ANTERIOR de autorização de instituições de pagamento (PDF disponível em normativos.bcb.gov.br, versão v7). Sucedida pela Res. BCB nº 80/2021. **Não usar**: serve apenas como pista histórica dos limiares antigos.
- **Entidade:** Resolução nº 4.282, de 4/11/2013 (CMN) — diretrizes de regulação, supervisão e vigilância de arranjos e instituições de pagamento; candidata a fonte primária sobre a fronteira "arranjo de pagamento" vs. "prestador de serviço de tecnologia".
- **Entidade:** Resolução nº 4.553/2017 — define os Segmentos S1/S2 que determinam quem é participante obrigatório de dados no Open Finance.
- **Contradição/ambiguidade a resolver:** o art. 6º, §4º (incluído pela Res. Conj. 4/2022) permite ao BCB DISPENSAR instituições da participação obrigatória com base em quantidade/natureza de clientes e canais — ou seja, "ser instituição autorizada" e "ser participante obrigatório" são conjuntos distintos. Isso importa para desenhar a rota de menor atrito.
- **Pergunta aberta operacional:** o custo real de entrada no Open Finance não é só autorização — art. 7º (registro no repositório de participantes), art. 8º (interface dedicada, jornada de consentimento/autenticação/confirmação por canais eletrônicos, ininterrupta) e art. 44 (convenção/estrutura de governança) implicam conformidade técnica certificada. Para um time de 2 devs com 3 meses, isso reforça a rota "consumir agregador/ITP de terceiro".
- **Sinal para a decisão de negócio:** a única alavanca de Open Finance com escopo obrigatório e sem custódia é a iniciação de pagamento — e ela é justamente a que exige participante autorizado. Produtos de conciliação/AP-AR/relatório vivem inteiramente fora do perímetro regulado, o que os torna os candidatos de menor atrito regulatório entre as 8 áreas.

## Lacunas

Procurado e NÃO encontrado neste run (todas são lacunas materiais para a decisão):

1. **Texto da Resolução BCB nº 80, de 25/3/2021** — tentado via `bcb.gov.br/estabilidadefinanceira/exibenormativo` (retornou SPA vazia) e via busca em `normativos.bcb.gov.br` (só retornou a Resolução nº 80/1967, homônima). Portanto NÃO foram verificados: (a) capital social integralizado e patrimônio líquido mínimos por modalidade; (b) os limiares de volume que obrigam a pedir autorização; (c) as hipóteses de dispensa; (d) se e por qual norma foi alterada, e a data da última alteração. **Crença não verificada, a tratar como hipótese:** valores da ordem de R$1 milhão para ITP e R$2 milhões para emissor de moeda eletrônica, e limiares de volume anual de transações / recursos mantidos em conta de pagamento acima dos quais a autorização é obrigatória. Não usar nenhum desses números em decisão antes de ler o texto oficial.
2. **Lei nº 12.865/2013 (planalto.gov.br)** — três tentativas, todas com ECONNRESET. Não verificados: definição legal de instituição de pagamento e de arranjo de pagamento, a vedação de atividades privativas de instituição financeira, a segregação patrimonial dos recursos em conta de pagamento, e — o mais importante para a pergunta 1 — a exclusão expressa de prestadores de serviço de tecnologia/rede do conceito de instituição de pagamento.
3. **Gatilho preciso da autorização** (custódia? liquidação em nome próprio? volume?) — só foi possível confirmar, por via indireta e forte, que a não-custódia é elemento definidor do ITP (art. 2º, VI). A regra positiva de quando a autorização é exigida está na Res. BCB 80/2021, não lida.
4. **LGPD (Lei nº 13.709/2018), papel de operador vs. controlador** — nenhuma fonte primária consultada (planalto inacessível). Nada afirmado; **crença não verificada:** SaaS que trata dado financeiro por conta e ordem do cliente tende a atuar como operador, e como controlador quando define finalidades próprias (ex.: modelagem/score). Requer rodada dedicada com o art. 5º, VI e VII, e art. 39 da LGPD.
5. **Obrigações fiscais/contábeis de produto que emita documento fiscal** (NF-e/NFS-e, convênios ICMS/ambiente municipal, certificado digital) — não pesquisado por esgotamento de orçamento. Zero evidência.
6. **Status regulatório de agregadores citados no brief (Pluggy, Belvo, Klavi)** — não verificado se são instituições autorizadas/participantes do Open Finance, ou se operam como prestadores de tecnologia sobre participantes de terceiros. Essa distinção muda a análise de risco de quem os contrata.
7. **Confirmação de que não existe Resolução Conjunta posterior à nº 4/2022** alterando a Res. Conj. 1/2020 — o PDF consolidado lido é a versão "v4" e não registra alteração posterior a 24/3/2022, mas não cruzei com a busca de normativos do BCB.

Notas de método: 11 chamadas de ferramenta (1 acima do orçamento de 10, gasta em extração local de texto do PDF já baixado, sem nova requisição de rede); 1 fonte primária efetivamente lida em profundidade (Res. Conj. 1/2020, texto consolidado, páginas 1-7 de 29); 2 buscas com retorno pobre; 3 fetches falhados por erro de rede/SPA.
