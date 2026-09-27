---
title: 'Pesquisa de mercado: oportunidade de fintech de baixo orçamento no Brasil'
type: 'market'
shape: 'select'
topic: 'Oportunidade de fintech de baixo orçamento no Brasil'
decision: 'Qual oportunidade de fintech tem melhor relação entre baixo custo de entrada, baixa complexidade regulatória, velocidade de MVP e velocidade até cliente pagante, sob 2 devs / 3 meses / R$1.000 por mês'
source: 'run nativo (web fan-out, 10 assistentes)'
status: complete
preset: 'quick'
validation: 'normal + red team'
claims_verified: 9
claims_unverified: 10
claims_disputed: 3
claims_overturned: 1
sources: 56
created: '2026-08-19'
updated: '2026-08-19'
---

# Pesquisa de mercado: oportunidade de fintech de baixo orçamento no Brasil

**Decisão que esta pesquisa serve:** qual oportunidade de fintech no Brasil maximiza a relação entre custo de entrada baixo, atrito regulatório baixo, velocidade de MVP e velocidade até cliente pagante — sob 2 desenvolvedores, 3 meses e R$ 1.000/mês de infraestrutura.

**Como navegar:** quer o veredito → *Sumário executivo*. Quer saber por que um candidato foi cortado → *Matriz de decisão*. Quer a evidência bruta → *Achados por dimensão*. Quer construir → *Recomendações* e *O que os artefatos seguintes consomem daqui*. Quer saber do que desconfiar → *Limitações* e *Mapa de obsolescência*.

---

## Sumário executivo

**Esta pesquisa eliminou mais do que selecionou — e isso é o seu resultado mais valioso.** Dos 13 candidatos levantados com evidência, 7 caem por gate ou por saturação verificada, incluindo a hipótese que eu próprio havia colocado em primeiro lugar e que o red team derrubou. Nenhuma das três hipóteses sobreviventes tem, hoje, evidência de demanda. O que você tem em mãos é um mapa de onde **não** gastar três meses, mais três apostas ranqueadas por aderência estrutural, não por demanda comprovada.

**Os três achados que dirigem a resposta:**

1. **Custo fixo não repassável é o que mata este orçamento.** A agregação de dados via Open Finance custa **mínimo mensal de R$ 2.500 na Pluggy** [36] — confirmado por fonte independente [39] — e **USD 1.000/mês na Belvo** [40]. Mínimo é piso, incide com zero cliente, e nenhum fornecedor brasileiro publica pay-as-you-go ou preço por conexão [39][40][41]. Isso corta quatro candidatos por gate. Em contraste, cobrança via Asaas ou Efí tem **custo fixo zero** e tarifa por transação repassável ao cliente final [37][47]. A regra que sai daí vale mais que qualquer ranking: **cada mínimo mensal antecipa despesa contra receita inexistente; cada tarifa por transação só dispara depois que o cliente pagou.**

2. **A fronteira regulatória é generosa com você — desde que não haja custódia.** Texto normativo primário [7] confirma que conciliação, contas a pagar/receber, ERP financeiro, relatórios e automação estão **fora do escopo de serviços do Open Finance** (art. 5º, II, Res. Conjunta BCB/CMN nº 1/2020) e, portanto, fora do perímetro que exige autorização. A não-custódia é elemento constitutivo do ITP (art. 2º, VI) — o que confirma que **deter fundos de terceiros, mesmo "temporariamente", é o gatilho clássico de autorização.** A rota de menor atrito é consumir PSP/ITP de terceiro e nunca tocar no dinheiro.

3. **O canal contábil é estrutura de mercado real — e o teste que ele impõe reprova produtos de feature única.** Seis fornecedores operam programa formal de parceria contábil, todos com adesão gratuita [45][42][43][44][56]. Mas o contador revende **ERP**, porque é isso que paga comissão e reduz retrabalho dele [56]. Uma ferramenta avulsa disputa o mesmo slot por uma fração do valor. Daí o critério de triagem que o red team destilou — o gate G6 abaixo, que você deve aplicar antes de escolher qualquer área: **"o PSP ou o ERP já entrega isso de graça dentro do bundle?"**

**As três sobreviventes, em ordem:** **H1** — conciliação de *pagamento fora da cobrança*, lendo extrato importado — formato OFX — em vez de agregação Open Finance (3,73). **H2** — automação de contas a pagar com o escritório de BPO (*business process outsourcing* financeiro) como cliente pagante, não como revendedor (3,72). **H3** — vertical financeiro de nicho desatendido (3,42). H1 e H2 empatam dentro da margem de erro, e nenhuma tem evidência de demanda.

**A única ação que não depende de mais pesquisa:** ligue para a TecnoSpeed e confirme o preço do PlugBank. Se os R$ 540/mês se confirmarem, quatro candidatos cortados por custo voltam ao jogo e esta matriz precisa ser refeita.

**Estado do ledger de evidência:** 23 claims rastreados — **9 verificados, 10 não verificados, 3 disputados, 1 derrubado**. Quase metade dos claims não passou por checagem independente — é isso que o preset `quick` compra; leia as marcações de confiança, elas não são decorativas.

**O maior alerta:** você escolheu o perfil de pesos "Potencial de receita", que coloca **40% do peso** em *potencial de receita* (22%) e *tamanho de mercado* (18%). São exatamente os dois critérios que este run **não conseguiu evidenciar em nível de candidato**. A matriz abaixo é calculável sobre 60% do peso. Não é um detalhe de metodologia — significa que o ranking responde bem à pergunta "o que é executável e sobrevivível" e mal à pergunta "o que dá mais dinheiro". Ver *Limitações* antes de agir.

---

## Frame de requisitos

### Hard gates (candidato que falha é cortado antes da matriz)

| | Gate |
|---|---|
| G1 | Não exige autorização própria do Banco Central para operar o MVP |
| G2 | Construível por 2 devs em ≤ 3 meses sobre APIs e BaaS (*banking as a service*) de terceiros |
| G3 | Infraestrutura ≤ R$ 1.000/mês; sem custódia de recursos de terceiros, sem core bancário próprio |
| G4 | Sem capital regulatório mínimo e sem risco de balanço |
| G5 | Caminho para cliente pagante desde o início |

### G6 — O gate que este run descobriu tarde demais

Antes de escolher qualquer área, aplique este teste:

> **O PSP ou o ERP já entrega isso de graça dentro do bundle?**

Foi ele que reprovou a recomendação líder — depois de sete dimensões de pesquisa. Custa uma tarde de leitura de documentação e teria economizado três meses. Trate como gate de entrada, não como consideração.


### Critérios ponderados (perfil "Potencial de receita", escolhido por você)

| Critério | Peso | Este run conseguiu evidenciar? |
|---|---:|---|
| Potencial de receita | 22% | **Não**, em nível de candidato |
| Tamanho e crescimento do mercado | 18% | **Não**, em nível de candidato |
| Tempo até o primeiro cliente pagante | 14% | Parcialmente |
| Dificuldade de aquisição de clientes | 13% | Sim |
| Concorrência | 12% | Sim |
| Complexidade regulatória | 10% | Sim, com fonte primária |
| Complexidade técnica | 7% | Parcialmente |
| Custo inicial | 4% | Sim, com verificação independente |

**Cobertura de evidência da matriz: 60% do peso.** Os 40% restantes (receita + tamanho) não têm dado público em nível de candidato — ver *Limitações*.

---

## Matriz de decisão

Escala 1–5, onde 5 é o melhor para este fundador. `s/e` = sem evidência recuperada neste run; a célula **não** é preenchida por inferência.

### Candidatos cortados por gate (não entram no ranking)

A coluna `#` remete à numeração do screening da dimensão D1; o roster completo dos 13 candidatos está em `digests/d1-screening-r1-1.md`.

| # | Candidato | Gate violado | Evidência |
|---|---|---|---|
| 2 | Conciliação bancária via Open Finance embarcada em ERP | **G3** | Mínimo Pluggy R$ 2.500/mês = 250% do teto, com zero cliente [36][39] |
| 4 | Cash management multibanco para PME | **G3** | idem; e a Pluggy vende "Cash Management" como produto próprio [1] |
| 5 | Categorização/enriquecimento de extratos (PFM white-label) | **G3** | idem; "Enriquecimento de Dados" é produto da própria Pluggy [1] |
| 12 | Middleware de dados bancários para escritórios contábeis | **G3** | idem [36][39][40] |
| 3 | Contas a pagar com iniciação Pix via ITP próprio | **G1** | ITP é instituição participante autorizada pelo BCB (art. 1º c/c 2º, VI) [7] |
| 1 | Conciliação de cartões multiadquirente | **G2** | SmartConcilia declara 80+ adquirentes integrados — barreira de integração incompatível com 3 meses [4] |
| 11 | Conector venda-maquininha → ERP | **G2** | mesma barreira; e o Itaú já ataca por parceria com ERP [5] |

### Candidatos cortados por saturação verificada

| # | Candidato | Por quê | Evidência |
|---|---|---|---|
| 8, 10 | Split/checkout para infoprodutos; ponte de pagamento para e-commerce | A Cora entrega Pix ilimitado, boleto e TED grátis com mensalidade zero; não se compete com zero subsidiado sem licença para monetizar float | [30] |
| 6 | Cobrança recorrente com régua de inadimplência sobre PSP | Cora empacota gestão de cobranças de graça [30][50]; Asaas idem, sem mensalidade [47]; Iugu empacota o híbrido "Bolix" [51] | [30][47][50][51] |
| — | Conciliação de recebimentos boleto×Pix sobre API do PSP | **Derrubado pelo red team** — ver *Evidência contrária*. O Asaas já casa por `txid` e dispara webhook | [48][52][53][54] |

### Ranking das hipóteses sobreviventes

- **H1 — Pagamento fora da cobrança:** casar Pix recebido direto na chave (valor parcial ou divergente, sem `txid`) contra cobranças em aberto, lendo extrato exportado pelo cliente.
- **H2 — Contas a pagar para BPO:** vender ao escritório de contabilidade/BPO que atende dezenas de PMEs, invertendo o modelo de canal.
- **H3 — Vertical de nicho:** oferecer cobrança, conciliação e fluxo de caixa para um setor específico, com regra de negócio e vocabulário próprios.

| Critério | Peso | **H1** Pagamento fora da cobrança (OFX) | **H2** Automação de contas a pagar para BPO | **H3** Vertical financeiro de nicho |
|---|---:|:---:|:---:|:---:|
| Potencial de receita | 22% | s/e | s/e | s/e |
| Tamanho e crescimento | 18% | s/e | s/e | s/e |
| Tempo até 1º pagante | 14% | 4 | 3 | 3 |
| Dificuldade de aquisição | 13% | 3 | 4 | 3 |
| Concorrência | 12% | 3 | 3 | 4 |
| Complexidade regulatória | 10% | 5 | 5 | 5 |
| Complexidade técnica | 7% | 4 | 4 | 3 |
| Custo inicial | 4% | 5 | 5 | 4 |
| **Total sobre os 60% evidenciados** | | **3,73** | **3,72** | **3,42** |

**Leia esta tabela com desconfiança deliberada.** H1 e H2 empatam dentro da margem de erro de uma rodada única — a diferença de 0,01 não decide nada. E as duas primeiras linhas — as vazias — carregam 40% do peso que você escolheu. A matriz é reponderável: se você baixar receita e tamanho e subir execução, H1 se separa; se conseguir evidência de receita, a ordem pode inverter inteiramente.

---

## Achados por dimensão

### D1 — O campo de candidatos

Treze candidatos concretos foram levantados com evidência recuperada [1][2][3][4][5]. A pista mais afiada não estava no plano: **a Pluggy vende como produto de API exatamente o que seus clientes construiriam sobre ela** — "Pagamentos via Pix", "Enriquecimento de Dados" e "Cash Management" [1]. Quem construir conciliação bancária ou cash management está construindo o que o fornecedor de infraestrutura já embala, com risco de compressão de margem e de o fornecedor subir a stack.

Conta Azul, Nibo, MarketUP, TOTVS e Kamino já compram o conector de Open Finance pronto da Pluggy [1]. **Conciliação bancária genérica virou feature comoditizada, não produto.** A oportunidade migrou para o que a Pluggy explicitamente não vende: workflow, regra de negócio vertical e recuperação de inadimplência.

Achado de ausência: o diretório de plugins do Asaas não lista **nenhum** app vertical de saúde, jurídico, condomínios, oficinas ou salões — só educação (Twygo, Hotmart) e e-commerce (WooCommerce, Nuvemshop, Magento) [2]. Ausência em um diretório não prova ausência no mercado, mas é a pista mais acionável da dimensão. Confiança: média. A rota alternativa de screening falhou: o Radar do FintechLab foi localizado, mas nenhuma contagem ou lista por categoria foi recuperada [6].

*Encerramento: por esgotamento de orçamento de chamadas, não por cobertura. O agente recusou-se a listar verticais de nicho por só ter memória de treinamento sem evidência — comportamento correto, que deixa a pergunta aberta.*

### D2 — Perímetro regulatório

A única dimensão do run com **fonte primária lida em profundidade**: o texto consolidado da Resolução Conjunta BCB/CMN nº 1/2020 [7].

| Atividade | Autorização do BCB? | Como o software fica fora |
|---|---|---|
| Conciliação financeira | Não | Ler dados que o cliente já possui; nunca receber nem movimentar recursos |
| Contas a pagar / receber | Não | Camada de decisão e registro; o pagamento é executado pelo banco do cliente |
| Cobrança/boleto/PIX via PSP licenciado | Não, para o software | Liquidação sempre em conta do PSP em nome do cliente final |
| **Custódia de recursos de terceiros** | **Sim** | Não fazer, nem temporariamente. É o erro mais caro e mais comum |
| ITP construído pela própria startup | Sim | Consumir ITP de terceiro já autorizado |
| Agregação de dados (ser a receptora) | Sim | Contratar agregador já participante e consumir a API dele |
| Gestão financeira / ERP / relatórios / automação | Não | SaaS puro sobre dados do próprio cliente |

Ancoragens verificadas no texto: o escopo obrigatório de **serviços** do Open Finance tem apenas dois itens — iniciação de pagamento e encaminhamento de proposta de crédito (art. 5º, II) [7]; o ITP é definido como quem inicia pagamento "sem deter em momento algum os fundos transferidos" (art. 2º, VI) [7]; o histórico mínimo compartilhado é de doze meses (art. 5º, §5º, II), que é o teto informacional de qualquer produto de gestão financeira sobre Open Finance [7].

**Lacuna material declarada:** o texto da **Resolução BCB nº 80/2021** não foi recuperado — o site do BCB respondeu com página vazia, Planalto e DOU deram erro de conexão. Portanto **capital mínimo por modalidade e limiares de volume que obrigam a autorização permanecem não verificados**. Números que circulam para isso são crença não verificada e não sustentam decisão.

### D3 — Tamanho alcançável

O denominador é sólido e oficial; a taxa de conversão é frágil.

- **~24 milhões de CNPJs ativos de pequenos negócios** no 4T2025, recorde histórico, com **97% das MPEs e 90% dos MEIs efetivamente em operação** [9]. Esse desconto de operação (*haircut*) é raro e permite converter estoque cadastral em base endereçável de forma defensável.
- 24.213.445 empresas ativas totais e 93,8% de micro e pequenas no 2º quadrimestre de 2025 [8], com eco em [13].
- **Contradição não resolvida:** o MDIC registra 12.660.170 MEIs [8]; o Sebrae registra 13,1 milhões [9]. Diferença de ~440 mil, possivelmente temporal ou definicional. Fixe **uma** definição e **uma** data-base antes de dimensionar qualquer SAM (mercado endereçável).
- **Disposição a pagar — o número que decide o modelo, e está velho:** 37% das PMEs sem software pagariam R$ 30–50/mês e 21% pagariam R$ 50–70/mês [10]. Amostra de 298 respondentes, novembro de **2019** — 6,7 anos fora da barra de frescor. Corrigida pela inflação, a faixa fica em algo como R$ 50–120/mês. Revalidar isso é a maior prioridade de pesquisa remanescente.
- **As empresas recém-abertas são a esteira de aquisição mais barata do país:** cerca de 1,5 milhão de novos CNPJs por trimestre em 2026 [12], que ainda não têm sistema instalado e portanto têm custo de troca zero. Confiança baixa — agregador cujos próprios números internos não fecham entre si.
- Gastos com ERP no Brasil projetados em US$ 4,9 bi para 2025 [11] — projeção apresentada em março de 2025, não realizado, e o recorte PME desse bolo não existe publicamente.

**Achado de segunda ordem que muda como ler este relatório inteiro:** o Brasil tem dado de **contagem** de empresas excelente, aberto e trimestral, e dado de **comportamento** (o que a PME usa, paga e por que troca) muito pobre — o que circula é pesquisa de fornecedor com amostra pequena, sem metodologia publicada, frequentemente de 2019. Qualquer dimensionamento aqui é sólido no denominador e frágil na monetização.

### D4 — Dores e disposição a pagar

A dor mais nítida recuperada é o **descasamento entre o meio da cobrança e o meio da liquidação**: três reclamações distintas sobre falha de conciliação no Conta Azul, uma delas descrevendo exatamente recebimento via Pix que não concilia com boleto emitido [14][15][16]. É a única queixa do run que descreve mecanismo técnico reproduzível em vez de insatisfação genérica. *(Este achado foi depois reenquadrado pelo red team — ver adiante.)*

Duas dores adjacentes aparecem no eixo de pagamentos e valem registro porque mostram fragmentação entre fintechs PJ: a InfinitePay não aceita conta Cora para recebimento, deixando o lojista sem receber na conta em que opera [22], e o motor de risco da própria InfinitePay nega venda legítima como "atípica" [23]. O lojista já paga os dois produtos e ainda assim o fluxo não fecha. Na mesma linha de execução financeira que falha em silêncio, há relato de pagamentos agendados e não efetuados pela Cora [24].

**Suporte é a dor que mais gera pedido explícito de cancelamento** na amostra: quatro reclamações na Omie, uma terminando em cancelamento e reembolso [18][19][20][21]. Isso favorece produto vertical de nicho com atendimento humano próximo em vez de competição em features — configuração que casa com um fundador e 2 devs.

Confirmação pela boca do incumbente de que **o substituto real é a planilha**: o Conta Azul distribui planilhas gratuitas como isca, entrega backup de cancelamento em CSV, e mantém função de importação existente para "trazer lançamentos criados em planilhas" [25] — ponte que, quando falha, gera reclamação própria [17]. E há custo de saída real — dados apagados 90 dias após vencimento não pago, cancelamento irreversível [26] — o que significa que a base instalada do incumbente contém insatisfação represada, não satisfação.

Sinal indireto de disposição a pagar: existe ecossistema pago de terceiros vendendo BI e planilha acoplados ao Conta Azul [27] — alguém já monetiza o buraco entre o ERP e o que o dono da PME quer enxergar.

**Limitação séria:** o Reclame Aqui bloqueou acesso direto (HTTP 403) em todas as páginas de empresa. A evidência veio de títulos e trechos expostos em busca, quase sem datas. **A pergunta "essa dor persiste há anos?" ficou sem resposta defensável** — só foi possível inferir recorrência pela multiplicidade de URLs sobre o mesmo tema. Google Play, App Store, Reddit e comunidades de contadores não foram cobertos. **Ninguém disse "eu pagaria por isso".**

### D5 — Concorrência e substitutos

**Preços lidos diretamente das páginas** (acesso 2026-08-19; nenhuma página exibe data de publicação):

| Produto | Plano de entrada | Preço/mês | Observação |
|---|---|---:|---|
| Bling Cobalto | entrada | R$ 60 | NF ilimitadas; **piso do ERP PME brasileiro** [29] |
| Bling Titânio | — | R$ 120 | conciliação bancária só aqui — **é upsell** [29] |
| Conta Azul Essencial | entrada | R$ 159,90 | 1 usuário, alvo MEI [28] |
| Conta Azul Performance | topo | R$ 839,90 | 15 usuários [28] |
| Cora conta PJ | — | **R$ 0** | Pix ilimitado, boleto e TED grátis, sem mensalidade [30] |
| Asaas | — | **R$ 0** de mensalidade | PIX/boleto R$ 0,99 nos 3 primeiros meses, **R$ 1,99 em regime** [47] |

**Saturação estrutural em pagamentos e cobrança:** a Cora ataca explicitamente o preço do boleto dos bancos tradicionais, citando concorrentes que cobram "até R$ 9,00" [30]. O preço de referência da cobrança está indo a zero, financiado por outro produto. Um time de 2 devs não compete com zero subsidiado nem tem licença para monetizar float.

**A fresta em conciliação:** no Bling ela não está no plano de entrada [29]; na Conta Azul aparece como recurso da plataforma sem estar atribuída a plano nenhum [28]. Padrão clássico de vazio — todo mundo lista, ninguém vende como produto. *(O red team depois mostrou por que essa fresta é mais estreita do que parece.)*

Contexto de capital: 106 rodadas de fintech no Brasil em 2025 contra 244 em 2021 [32] — menos cheques e cheques maiores, o que favorece o entrante bootstrapped por reduzir concorrentes novos financiados, mas deixa incumbentes com caixa para engolir nichos adjacentes. Confiança baixa: fonte única via snippet.

### D6 — GTM, pricing e CAC

**Mídia paga está fora de questão para você, e o número prova:** CAC de SMB no SaaS B2B brasileiro estimado em R$ 3.000–12.000, contra ticket plausível de R$ 70–300/mês [35]. Payback de 1 a 3 anos contra churn SMB de 3–7% ao mês. A fonte é agregadora sem amostra declarada — use como ordem de grandeza, jamais como premissa de modelo — mas a ordem de grandeza basta para eliminar o canal.

**Marketplace como distribuição pronta:** a Omie.Store aceita apps de terceiros, com portal de desenvolvedor e chamada explícita "Publique sua solução" [34]. Preços praticados por terceiros na vitrine — R$ 69,99, R$ 209,00, R$ 289,00 por usuário, e apps gratuitos [34] — provam aceitação de faixa e de modelo. **O revenue share não é publicado** [34]: é o número que separa "marketplace é canal viável" de "marketplace é só vitrine".

Nada neste run sustenta recomendar um modelo de precificação sobre outro — não há dado comparativo de conversão entre assinatura fixa, por usuário, por documento ou percentual.

### D6b — O canal contábil

**Verificado:** o canal é real e replicado entre concorrentes. Seis fornecedores operam programa formal — Conta Azul [45][33], Nibo [42], Omie [43], Asaas [44], vhsys e GestãoClick [56] — **todos com adesão gratuita**. Dois modelos coexistem: revenda com desconto (Conta Azul, Nibo, GestãoClick) e comissão de indicação (Omie, Asaas, vhsys). Em todos os casos de revenda, o contador é simultaneamente cliente pagante da ferramenta do próprio escritório: **o software do escritório é a isca, a revenda ao cliente PME é a monetização.**

**Derrubado:** a afirmação de descontos de até 85% na revenda **não se sustenta**. A página oficial do programa Conta Azul publica descontos progressivos de **20% a 40%** [45]; o Nibo publica **30% a 50%** [42]. Nenhuma fonte primária menciona 85%. A margem que você precisa ceder ao parceiro é menos da metade do que se supunha — o que melhora o caso do canal, mas invalida contas feitas sobre o número anterior.

**Disputado:** o número de parceiros da Conta Azul. A fonte primária datada mais recente, do blog da própria empresa (05/09/2024, atualizado 13/05/2025), diz **"mais de 10 mil parceiros ativos"** [46]. A cifra de 14.000 aparece apenas em resumo de busca sem página datada por trás. Adote 10 mil como piso documentado, rotulado como autorreportado.

**Lacuna que bloqueia o modelo:** nenhum dos quatro programas oficiais publica **quantos clientes um contador parceiro traz**. O cálculo tentador de dividir os 150 mil clientes da Omie por 24 mil escritórios é inválido — a base inclui aquisição direta. Trate como incógnita a medir em piloto (10 a 20 escritórios, 90 dias), não como parâmetro pesquisável. Sinal indireto, e mais fraco do que parece: a estrutura de 5 a 6 níveis sugere distribuição de cauda longa rasa, com a maioria dos parceiros nas faixas baixas — mas a checagem semântica mostrou que no Nibo o teto de 50% já é atingido no terceiro nível [42], o que enfraquece a inferência. Trate como pista, não como evidência.

### D7 — Custo real do stack

| Fornecedor | Categoria | Modelo | Preço | Mínimo mensal? |
|---|---|---|---|---|
| Pluggy Dados | Agregação Open Finance | mínimo + excedente por request | **a partir de R$ 2.500/mês** [36] | **Sim** |
| Pluggy Pagamentos | Iniciação Pix | mínimo + excedente | a partir de R$ 500/mês [36] | **Sim** — a página é explícita: os dois produtos têm mínimos separados |
| Belvo Launch | Agregação | assinatura | **USD 1.000/mês** [40] | Sim |
| TecnoSpeed PlugBank | Agregação | **não publica preço** [41] | R$ 1.500 adesão + R$ 540/mês, relato de terceiro [39] | desconhecido |
| Efí | Cobrança/PIX | 100% variável | QR dinâmico 1,19%; boleto R$ 3,45 no recebimento; emissão e boletos não pagos: **grátis** [37] | **Não** |
| Asaas | Cobrança/PIX | 100% variável | PIX/boleto R$ 0,99, depois **R$ 1,99 em regime**; NF-e R$ 0,49 [47] — a página ressalva que as taxas são padrão e variam por contrato | **Não** |
| Pagar.me | Adquirência | **não publica preço** [38] | negociado | desconhecido |

**Cabe em R$ 1.000/mês?**

- **Agregação Open Finance: não.** R$ 2.500 no mês 1, com zero cliente pagante. Déficit de R$ 1.500 antes de qualquer hospedagem. Como o mínimo é piso e não função de volume, o custo por cliente só cai a cerca de R$ 50 com 50 clientes — escala que 3 meses não produzem. O trial de 14 dias da Pluggy cobre validação técnica, não o caminho até o primeiro pagante: ao fim dele as conexões pausam [36].
- **Cobrança e Pix: sim, com custo fixo zero.** Com a Efí: R$ 0 de mensalidade, setup e abertura [37]. Consumir R$ 1.000 em tarifa de Pix exigiria R$ 84.033 de volume transacionado, ou 289 boletos pagos. Boleto emitido e não pago não custa nada — elimina o risco de queimar orçamento com cobrança que não converte.

**Que o Pagar.me não publique preço é achado de velocidade, não só de custo:** negociação com funil de vendas insere semanas num cronograma de 3 meses. A Efí e o Asaas são autosserviço.

**Lock-in: zero evidência recuperada.** Não lemos nenhum contrato, prazo de fidelidade, multa ou política de exportação. A pergunta desta dimensão sobre lock-in contratual ficou inteiramente sem resposta.

---

## Insights que só o cruzamento mostra

Estes quatro não aparecem em nenhuma dimensão isolada.

**1. O gate de custo e o gate regulatório apontam para lados opostos, e é isso que estreita o campo.** A regulação é generosa justamente onde o custo é proibitivo. Conciliação e agregação estão fora do perímetro do BCB [7] — mas exigem dado de extrato, que custa R$ 2.500/mês de mínimo [36][39]. Cobrança e Pix são baratos e de custo variável [37][47] — mas estão saturados por incumbentes que os dão de graça [30][50][51]. **A zona viável é a interseção estreita: produtos não regulados que se alimentam de dados que o cliente já possui e pode exportar sozinho.** Foi essa interseção que sobreviveu ao run.

**2. O incumbente que documenta a própria lacuna vale mais que dez relatórios de mercado.** O Conta Azul publica, em documentação oficial de suporte atualizada em 14/04/2026, que **não concilia automaticamente pagamentos realizados fora da plataforma**, instruindo o usuário a cancelar o boleto e importar OFX para casar na mão [49]. Um incumbente com base instalada admitindo por escrito o que não faz é o sinal de bolsão aberto mais forte do run inteiro — mais forte que as três reclamações do Reclame Aqui [14][15][16], porque não depende de interpretação.

**3. A economia do canal contábil e o modelo de produto se determinam mutuamente.** O contador revende ERP porque é isso que paga comissão e reduz retrabalho dele [56]. Com desconto de revenda entre 20% e 50% [45][42], um produto de feature única precisa de preço de tabela alto o bastante para sobrar margem depois do repasse — mas o teto de disposição a pagar da cauda longa de PME está na faixa de R$ 50–120/mês corrigida [10]. **As duas restrições se estrangulam.** A saída lógica que a evidência sugere, sem comprová-la, é inverter: fazer do **contador ou do BPO o cliente pagante**, não o revendedor. Aí o ticket é do escritório (que atende dezenas de PMEs) e não da PME individual.

**4. A escassez de dado é assimétrica e isso deve mudar seu plano de validação.** O Brasil tem dado de contagem de empresas excelente e dado de comportamento péssimo [9][10]. Combinado com o fato de que **ninguém disse "eu pagaria por isso"**, a conclusão prática é: mais desk research não fecha a lacuna de demanda. Só conversa com cliente fecha. Gastar outra rodada de pesquisa esperando achar o número de disposição a pagar é gastar contra uma fonte que não existe publicamente.

---

## Evidência contrária (red team)

O red team recebeu a recomendação líder sem nenhuma das evidências que a sustentavam, com orçamento próprio de busca, e a tarefa de derrubá-la. **Ele derrubou.** A conclusão foi revista antes de entrar neste relatório; o que segue é o que sobreviveu do ataque.

**A redireção que o red team entregou junto com a demolição** é o que salva a rodada: o alvo real é *pagamento fora da cobrança*, não *conciliação de cobrança*. E ele não exige Open Finance — exige **extrato**, que pode vir de OFX importado ou de exportação automática agendada, que a Cora entrega de graça em CSV, PDF e OFX. Isso inverte a premissa arquitetural **sem estourar o gate G3**.

**A recomendação atacada era:** SaaS de conciliação de recebimentos — casar cobrança emitida com liquidação recebida, incluindo boleto pago por Pix — construído sobre a API do PSP que o cliente já usa, fora do perímetro regulado, distribuído por escritórios contábeis.

**Golpe 1 — o caso-bandeira já é resolvido de graça pelo PSP.** No boleto com QR Code Pix do Asaas, "o sistema relaciona a transação à cobrança original por meio de identificadores exclusivos, como o `txid`", com webhooks configuráveis para receber a confirmação do Pix e relacioná-la automaticamente à cobrança original [48]. **Se o PSP sobre o qual você construiria já entrega isso embutido, o produto vira um wrapper de webhook.** A fonte [48] foi publicada em 23/07/2026; confiança alta.

*(A checagem semântica removeu deste golpe uma alegação de que não haveria cobrança pela conciliação: a fonte nada diz sobre custo. O golpe não depende disso — o produto vira wrapper de webhook havendo taxa ou não.)*

**Golpe 2 — o arranjo Pix foi concebido para conciliar.** O campo `txid` (referenciado como `idConciliacaoRecebedor`) existe com a finalidade declarada de permitir associar a transação Pix à cobrança correlata, e cada transação carrega um `EndToEndId` único presente tanto no extrato quanto no sistema do PSP [52][53][54]. A dor residual é de **implementação do integrador**, não de ausência de infraestrutura — e dor de má implementação alheia é péssima base para um SaaS, porque some quando o integrador arruma. *Confiança média-alta, não alta: o red team baixou o PDF do Manual de Padrões para Iniciação do Pix mas não conseguiu extrair o texto; a afirmação repousa em três fontes secundárias convergentes, uma delas o repositório oficial do BCB [54].*

**Golpe 3 — a contradição fatal, e a mais importante.** O único bolsão de dor genuinamente aberto é o **pagamento feito fora da cobrança**: o cliente que ignora o boleto e manda Pix direto na chave, com valor parcial ou divergente. Esse evento **não tem `txid` da cobrança** e frequentemente nem passa pelo PSP emissor — ele só aparece no **extrato bancário** [49]. Portanto: os casos que a API do PSP enxerga já foram resolvidos pelo PSP; os casos que justificariam o produto exigem dado de extrato, que é exatamente o que a arquitetura havia excluído por custo. **A tese se autocontradizia.**

**Golpe 4 — o slot do canal já está ocupado.** Os programas de parceria contábil são estruturados em torno de revenda de ERP, com conciliação aparecendo como módulo dentro dele, não como produto avulso [56]. Uma ferramenta de feature única disputa o mesmo slot de atenção e comissão por uma fração do valor por cliente — e, se não for o ERP, vira mais um login no fluxo do escritório.

**Golpe 5 — o espaço está em consolidação com capital.** A Kamino levantou R$ 54 milhões, **adquiriu a Nimbly**, e integra conciliação automática de extratos ao seu produto; Equals, FinBits, Barte e Kobana ocupam faixas adjacentes [55][31]. Concorrentes capitalizados podem oferecer conciliação como isca gratuita de um bundle maior — a pior configuração competitiva possível para um produto de feature única com 2 devs.

**O que o red team procurou e não encontrou** — e isto é achado, não vazio: nenhuma startup brasileira de conciliação para PME documentada como morta, encerrada ou pivotada por falta de mercado. Ele buscou explicitamente. O retorno foi o oposto: financiamento e consolidação por aquisição [55]. **Leia com cuidado — o padrão não é "ninguém sobrevive", é "conciliação vira módulo de plataforma maior".** Forma diferente, e igualmente ruim, de derrubar a tese de produto autônomo.

---

## Recomendações

Cada uma vem com sua base de confiança na mesma frase. Nenhuma das três tem evidência de demanda — leia isso como parte da recomendação, não como ressalva de rodapé.

### H1 — Conciliação de "pagamento fora da cobrança", via extrato importado

**O que é:** casar Pix recebido direto na chave (valor parcial, divergente, sem `txid`) contra cobranças em aberto, lendo o extrato que o cliente exporta — OFX ou CSV — em vez de agregação Open Finance.

**Por que sobrevive:** é o único bolsão que um incumbente de ERP com base instalada **documenta oficialmente como não resolvido** [49]; está fora do perímetro regulado [7]; e o custo de dado é zero, porque o extrato é exportável pelo próprio cliente.

**Confiança:** média na existência da lacuna (fonte primária do incumbente, datada 14/04/2026); **nula na demanda** — ninguém disse "eu pagaria por isso".

**O que pode matá-la:** o Conta Azul fechar essa lacuna sozinho; ou a Kamino, já capitalizada e com conciliação de extratos embutida [55], absorvê-la no bundle. Ambos são movimentos de um trimestre, não de um ano.

### H2 — Automação de contas a pagar com o BPO financeiro como cliente pagante

**O que é:** inverter o modelo de canal — vender ao escritório de contabilidade/BPO, que atende dezenas de PMEs, em vez de vender à PME e ceder 20–50% de margem ao contador revendedor [45][42].

**Por que sobrevive:** contas a pagar está inequivocamente fora do perímetro regulado [7]; o canal contábil é estrutura verificada e replicada por seis fornecedores [45][42][43][44][56]; e o modelo resolve o estrangulamento entre teto de ticket da PME e margem de revenda descrito no insight 3 de *Insights que só o cruzamento mostra*.

**Confiança:** alta no enquadramento regulatório e na existência do canal; **nula no mercado** — esta área não foi pesquisada como mercado neste run. Sem mapa de concorrentes, sem preço praticado, sem evidência de dor.

**O que pode matá-la:** o gate G6 aplicado a ela mesma — se o ERP que o BPO já usa entrega isso no bundle, não há produto. **Aplique o teste antes de escrever código.**

### H3 — Vertical financeiro de nicho desatendido

**O que é:** cobrança, conciliação e fluxo de caixa para um vertical específico, com regra de negócio e vocabulário do setor.

**Por que sobrevive:** o diretório do Asaas não tem nenhum app vertical de saúde, jurídico, condomínios, oficinas ou salões, só educação e e-commerce [2]; suporte próximo é a dor que mais gera cancelamento na amostra [18][21], e atendimento humano é vantagem estrutural de um time pequeno contra incumbente.

**Confiança:** baixa. A ausência foi observada em **um** diretório [2], e a dimensão de screening recusou-se — corretamente — a nomear verticais sem evidência recuperada.

**O que pode matá-la:** a ausência no diretório do Asaas pode refletir a estratégia de integração daquele PSP, não o mercado. Precisa ser testada contra os diretórios de Omie, Conta Azul e Bling antes de virar hipótese de trabalho.

---

## Limitações e questões abertas

**Limitação estrutural do run:** executado no preset `quick` — uma rodada por dimensão, cerca de 5 fontes cada, sem perseguição de pistas. Sete das dez dimensões encerraram por **esgotamento de orçamento**, não por cobertura nem por exaustão de novidade. Um relatório de seleção construído sobre uma rodada única não separa com segurança 1º de 2º lugar; não separa com segurança 1º de 2º lugar — ver o empate H1/H2 na *Matriz de decisão*.

**O descompasso mais importante:** o perfil de pesos escolhido coloca 40% em potencial de receita e tamanho de mercado — os dois critérios que este run não conseguiu evidenciar em nível de candidato, porque o dado brasileiro de comportamento e monetização, quando é público, é pobre [10]. A matriz responde bem "o que é executável" e mal "o que dá mais dinheiro".

**Duas fragilidades que a checagem semântica de citações expôs e que você deve conhecer:**

- **A âncora regulatória [7] não passou por verificação semântica.** Baixamos o PDF do normativo, mas não conseguimos extrair o texto em nenhuma das duas tentativas independentes. As três âncoras citadas — art. 5º II, art. 2º VI, art. 5º §5º II — foram lidas pela dimensão D2 na primeira rodada, mas não reconfirmadas. Some-se a isso o vencimento da janela de 24 meses. **Abra a versão HTML no site do BCB, não o PDF.**
- **As tarifas da Efí [37] não foram reconfirmadas**, e as contas de viabilidade em D7 — "R$ 84.033 de volume para consumir R$ 1.000 em tarifa" e "289 boletos pagos" — dependem inteiramente delas. A conclusão qualitativa (custo fixo zero, custo variável repassável) é robusta e sobrevive mesmo com tarifas diferentes; os números exatos, não.

**Questões abertas, em ordem de valor para a decisão:**

1. **Quanto custa realmente a TecnoSpeed PlugBank?** É o único fornecedor de agregação com mensalidade relatada abaixo do teto — R$ 540/mês mais R$ 1.500 de adesão [39] — mas o número vem de relato de terceiro e a página oficial não publica preço [41]. Um telefonema resolve. Se confirmar, os quatro candidatos cortados por G3 voltam inteiros e a matriz precisa ser refeita.
2. **Qual o texto da Resolução BCB nº 80/2021** — capital mínimo por modalidade e limiares de volume. Bloqueado por falha de acesso ao site do BCB; resolve-se abrindo o normativo manualmente.
3. **Quantos clientes um contador parceiro efetivamente traz?** Não é público em nenhum dos programas. Só mensurável em piloto de 10 a 20 escritórios por 90 dias.
4. **Qual o revenue share da Omie.Store** e dos demais marketplaces? Separa canal viável de vitrine. Não publicado.
5. **A disposição a pagar de 2019 ainda vale?** R$ 30–70/mês declarados há 6,7 anos. Não há fonte pública recente; só pesquisa primária resolve.
6. **A dor de conciliação persiste há anos?** Sem resposta defensável — o Reclame Aqui bloqueou o acesso que permitiria datar as reclamações.
7. **O texto do Manual de Padrões para Iniciação do Pix** confirma a finalidade conciliatória do `txid`? Três fontes secundárias convergem [52][53][54]; o PDF oficial não foi extraível.
8. **Verticais de nicho existem ou não?** Não pesquisado com evidência. A ausência foi observada em um único diretório [2].

**O que fecharia as lacunas:** um **Deepen** sobre este mesmo run folder cobrindo D1 (verticais), D3 (disposição a pagar atual) e D4 (voz do usuário via app stores, contornando o bloqueio do Reclame Aqui) — mais as duas ligações comerciais das questões 1 e 4, que nenhuma pesquisa de escritório substitui.

---

## O que os artefatos seguintes consomem daqui

- **Product brief** — a seção de oportunidade e problema deve carregar H1 com a lacuna documentada [49], e a seção de restrições deve carregar a regra de custo fixo versus variável.
- **PRD** — personas: o cliente pagante muda por hipótese (PME em H1, escritório de BPO em H2). Diferenciação: o gate G6 é requisito de entrada, não característica desejável.
- **Arquitetura** — a restrição G3 é arquitetural: qualquer dependência com mínimo mensal precisa de aprovação explícita antes de entrar na spine.

---

## Mapa de obsolescência

Calculado por `recon_kit.py staleness` sobre o ledger de claims, com as janelas do pack `market` mais a do formato `select` (preços ≤ 3 meses). Não derivado à mão — e a máquina corrigiu duas suposições minhas.

O cálculo recebeu 28 itens de claim extraídos do corpo do relatório — granularidade mais fina que as 23 entradas `claim` do memlog, que agrupam achados por dimensão. **6 dos 28 já estão vencidos hoje.**

| Claim | Classe | Publicação | Rechecar até | Estado |
|---|---|---|---|---|
| Conciliação, contas a pagar/receber e ERP fora do escopo de serviços do Open Finance [7] | regulatory | 2022-03 | 2024-03-01 | **vencido** |
| ITP definido como quem inicia pagamento sem deter os fundos [7] | regulatory | 2022-03 | 2024-03-01 | **vencido** |
| Disposição a pagar de PMEs entre R$ 30 e R$ 70/mês [10] | behavior | 2019-11 | 2021-11-01 | **vencido há ~5 anos** |
| 61% das PMEs usam planilha para contabilidade [10] | behavior | 2019-11 | 2021-11-01 | **vencido há ~5 anos** |
| SmartConcilia declara 80+ adquirentes [4] | competitor | 2025-10 | 2026-04-01 | **vencido** |
| Conta Azul declara mais de 10 mil parceiros ativos [46] | gtm | 2025-05 | 2026-05-01 | **vencido** |

**O vencimento regulatório merece atenção especial e eu havia errado nisso.** A Resolução Conjunta nº 1/2020 foi lida no texto consolidado "v4", com alterações marcadas até 24/03/2022 — e a dimensão D2 declarou explicitamente que **não conseguiu cruzar com a busca de normativos do BCB para descartar uma versão posterior**. Combinado com a janela de 24 meses já ultrapassada, isso significa que a única âncora de fonte primária deste relatório precisa ser reconfirmada como vigente antes de qualquer decisão. É barato: uma consulta ao normativo no site do BCB.

**Próximas rechecagens ainda no prazo:**

| Classe | Janela | Rechecar até |
|---|---|---|
| pricing (todos os preços de fornecedor e concorrente) | 3 meses | **2026-11-01** |
| competitor (Kamino, funding, mapa competitivo) | 6 meses | 2027-02-01 |
| tech (`txid` / `EndToEndId`) | 12 meses | 2027-08-01 |
| gtm (programas de canal, benchmarks de CAC) | 12 meses | 2027-01 a 2027-08 |
| size/growth (contagem de empresas) | 18 meses | 2026-09-01 a 2027-09-01 |

**Rechecagem mais próxima entre os claims ainda válidos: 2026-11-01** — toda a camada de preços, que é a que sustenta o gate G3 e portanto todos os cortes de candidatos. Um Refresh sobre este run folder trata disso.

**Aviso do formato `select`:** um relatório de seleção com mais de dois trimestres deve ser atualizado antes de qualquer ação. Este foi produzido em 2026-08-19 no preset `quick`, e já nasce com 6 claims vencidos — dois deles regulatórios.

---

## Apêndice de fontes

Todas acessadas em 2026-08-19. Onde a data de publicação consta como "não datada", a página não exibe data nem carimbo de atualização — a barra de frescor **não pôde ser verificada**, apenas a data de acesso.

| # | O que sustenta | Publisher | Publicação | Confiança |
|---|---|---|---|---|
| 1 | Pluggy vende Cash Management, Enriquecimento e Pagamentos como produtos; 130+ instituições; clientes Conta Azul, Nibo, MarketUP, TOTVS, Kamino | [Pluggy](https://pluggy.ai/) | não datada | média (autorreportado) |
| 2 | Diretório de plugins do Asaas; ausência de verticais de saúde, jurídico, condomínios, oficinas, salões | [Asaas](https://www.asaas.com/plugins) | não datada | alta |
| 3 | Volume de compras com cartão no Brasil (R$ 4 tri em 2024, via Abecs); fornecedores de conciliação de cartões | [F360](https://f360.com.br/blog/financas/software-de-conciliacao-de-cartoes/) | 2025-10-03 | média (ecoador; dado de 2024 é histórico) |
| 4 | SmartConcilia declara 80+ adquirentes conciliados — barreira de integração | [Sebrae SP](https://sebrae.com.br/sites/PortalSebrae/ufs/sp/programas/sebrae-conecta-smartconcilia,14d39e39b1d2f710VgnVCM100000d701210aRCRD) | não datada | baixa (autorreportado, não lida na íntegra) |
| 5 | Itaú integra maquininha ao ERP Soften para PMEs | [Let's Money](https://www.letsmoney.com.br/noticias/itau-soften-maquininha-erp-pmes/) | não datada | baixa (secundário, não lido na íntegra) |
| 6 | Radar FintechLab existe e teve publicação em 2025-08; nenhuma contagem por categoria recuperada | [FintechLab](https://fintechlab.com.br/index.php/category/radar/) | 2025-08 | baixa (só metadado de listagem) |
| 7 | Perímetro regulatório: escopo de serviços do Open Finance, definição de ITP, não-custódia, consentimento, histórico de 12 meses | [Banco Central / CMN — Res. Conjunta nº 1/2020, texto consolidado](https://normativos.bcb.gov.br/Lists/Normativos/Attachments/51028/Res_Conj_0001_v4_P.pdf) | 2020-05-04, alt. 2022-03-24 | **alta (fonte primária)** |
| 8 | 24.213.445 empresas ativas; 12.660.170 MEIs; 93,8% de MPEs (2º quad. 2025) | [MDIC — Mapa de Empresas](https://www.gov.br/empresas-e-negocios/pt-br/mapa-de-empresas/boletins/mapa-de-empresas-boletim-2o-quadrimestre-2025.pdf) | 2025-09 | média (PDF não parseou; via resumo) |
| 9 | ~24 mi de CNPJs ativos de pequenos negócios (4T2025); 97% das MPEs e 90% dos MEIs em operação; 13,1 mi de MEIs | [Agência Sebrae](https://agenciasebrae.com.br/dados/brasil-tem-recorde-de-cnpj-ativos-de-pequenos-negocios/) | 2026-03-18 | alta (lida na íntegra) |
| 10 | Disposição a pagar R$ 30–70/mês; 61% usam planilha; adoção sobe com porte | [Capterra Brasil (Gartner)](https://www.capterra.com.br/blog/1108/contabilidade-online) | 2019-11-27 | **baixa — fora da barra de frescor por 6,7 anos** |
| 11 | Gastos com ERP no Brasil projetados em US$ 4,9 bi para 2025 (estudo ABES) | [TI Inside](https://tiinside.com.br/20/03/2025/mercado-brasileiro-de-software-deve-crescer-95-em-2025-aponta-estudo/) | 2025-03-20 | baixa (403 no acesso; projeção, não realizado) |
| 12 | Aberturas de empresa no 1º tri de 2026; concentração por UF | [EmpresAqui](https://www.empresaqui.com.br/blog/noticias/empresas-abertas-brasil-1-trimestre-2026/) | 2026 | baixa (agregador; números internos não fecham) |
| 13 | Eco do boletim do Mapa de Empresas por entidade contábil | [FENACON](https://fenacon.org.br/noticias/abertura-de-empresas-cresce-141-no-2o-quadrimestre-de-2025/) | 2025 | baixa (não independente da fonte upstream) |
| 14 | "Conciliação bancária não funciona" no Conta Azul | [Reclame Aqui](https://www.reclameaqui.com.br/contaazul/conciliacao-bancaria-nao-funciona_74UirrPP4CumWX0x/) | não datada | média (403; via título e trecho) |
| 15 | Pix recebido não concilia com boleto emitido no Receba Fácil | [Reclame Aqui](https://www.reclameaqui.com.br/contaazul/falha-na-conciliacao-bancaria-do-conta-azul-recebimentos-via-pix-nao-conciliam-automaticamente-com-boletos-receba-facil_TGuO9Lz86ZLpcfXA/) | não datada | média |
| 16 | Conciliação automática não funciona; falha com Itaú por semanas | [Reclame Aqui](https://www.reclameaqui.com.br/contaazul/conciliacao-bancaria-automatica-nao-funciona_amXt3vgXVmALGTjF/) | não datada | média |
| 17 | Erro de importação de planilha no Conta Azul | [Reclame Aqui](https://www.reclameaqui.com.br/contaazul/erro-de-importacao-de-planilha_h-LA1rfD9oGm3xiO/) | não datada | média |
| 18 | Omie sem suporte por telefone; espera de 30+ minutos | [Reclame Aqui](https://www.reclameaqui.com.br/omiexperience/nao-tem-suporte-por-telefone_TWir1Y7lyKitfDAQ/) | não datada | média |
| 19 | Omie PDV com problema de integração recorrente | [Reclame Aqui](https://www.reclameaqui.com.br/omiexperience/omie-pdv-com-problema-na-integracao-com-frequencia__dSIrqqjY0UvkzsD/) | não datada | média |
| 20 | Cliente Omie impossibilitado de emitir notas fiscais | [Reclame Aqui](https://www.reclameaqui.com.br/omiexperience/suporte-omie-ineficiente-impossibilitado-de-emitir-notas-fiscais-e-bloqueado-no-sistema-de-suporte_bYdib8_SwLqkTV5m/) | não datada | média |
| 21 | Cobrança indevida e falta de suporte levando a cancelamento e reembolso | [Reclame Aqui](https://www.reclameaqui.com.br/omiexperience/plataforma-omie-cobranca-indevida-falta-de-suporte-e-impossibilidade-de-uso-levam-a-reclamacao-de-cancelamento-e-reembolso_cztyvGLFdLBsDXyn/) | não datada | média |
| 22 | InfinitePay não aceita conta Cora para recebimento | [Reclame Aqui](https://www.reclameaqui.com.br/infinite-pay/infinitypay-nao-aceita-o-banco-cora_iYVIgNvs89wef6mj/) | não datada | média |
| 23 | Venda negada como "atípica" pelo motor de risco | [Reclame Aqui](https://www.reclameaqui.com.br/infinite-pay/venda-negada-por-ser-considera-atipica-sendo-que-minhas-vendas-sao-de-tm_XEfaF65vz1X4TXZ3/) | não datada | média |
| 24 | Pagamentos agendados e não efetuados pela Cora | [Reclame Aqui](https://www.reclameaqui.com.br/cora/pagamentos-agendados-e-nao-efetuados-pelo-cora_o6gLM7rS-Z_YkWVb/) | não datada | média |
| 25 | Conta Azul mantém importação de planilha; planilha é o estado anterior do cliente | [Central de Ajuda Conta Azul](https://ajuda.contaazul.com/hc/pt-br/articles/6767578518285-Lan%C3%A7amentos-financeiros-como-importar-planilha) | não datada | média (admissão contra interesse) |
| 26 | Dados apagados 90 dias após vencimento não pago; cancelamento irreversível | [Central de Ajuda Conta Azul](https://ajuda.contaazul.com/hc/pt-br/articles/7602921353357-Meu-Plano-como-funciona-o-cancelamento) | não datada | média |
| 27 | Terceiros monetizam BI/planilha acoplada ao Conta Azul | [SFB Planilhas](https://sfbplanilhas.com/controlefinanceirointegradocontaazul/) | não datada | baixa |
| 28 | Preços Conta Azul: Essencial R$ 159,90 a Performance R$ 839,90; conciliação sem plano atribuído | [Conta Azul](https://contaazul.com/planos/) | não datada | alta (página oficial) |
| 29 | Preços Bling: Cobalto R$ 60, Titânio R$ 120 com conciliação, Diamante R$ 650 | [Bling](https://www.bling.com.br/planos) | não datada | alta (página oficial) |
| 30 | Cora: conta PJ sem mensalidade, PIX/boleto/TED grátis; comparativo contra "até R$ 9,00" de boleto | [Cora](https://www.cora.com.br/) | não datada | alta (página oficial) |
| 31 | Asaas captou R$ 35 mi (Vivo Ventures); Kamino captou R$ 54 mi | [Finsiders Brasil](https://finsidersbrasil.com.br/negocios-em-fintechs/fintechs-de-gestao-financeira-para-pmes-recebem-novos-investimentos/) | não datada | baixa (fonte única, via snippet) |
| 32 | 106 rodadas de fintech no Brasil em 2025 contra 244 em 2021 | [Startups.com.br](https://startups.com.br/negocios/fintech/fintechs-brasileiras-entram-em-nova-fase-com-menos-rodadas-e-mais-fidcs/) | não datada | baixa (via snippet) |
| 33 | Programa de parceria contábil da Conta Azul (página de contadores) | [Conta Azul](https://contaazul.com/contadores/) | não datada | média (autorreportado) |
| 34 | Omie.Store aceita apps de terceiros; preços praticados R$ 69,99 a R$ 289/usuário; revenue share não publicado | [Omie.Store](https://store.omie.com.br/) | não datada | alta (vitrine observada) |
| 35 | CAC de SMB R$ 3.000–12.000; churn SMB 3–7%/mês; LTV/CAC saudável 3–5x | [Baita Aceleradora](https://baita.ac/tudo-sobre/benchmarks-saas) | 2026 | **baixa — agregador sem amostra, período ou critério declarados** |
| 36 | Pluggy: mínimo mensal R$ 2.500 (Dados) e R$ 500 (Pagamentos); excedente por request; trial de 14 dias | [Pluggy](https://www.pluggy.ai/precos) | não datada | média (fonte primária do fornecedor) |
| 37 | Efí: QR dinâmico 1,19%; boleto R$ 3,45 no recebimento; emissão e não pagos grátis; sem mensalidade | [Efí Bank](https://sejaefi.com.br/tarifas) | não datada | média (a própria página ressalva variação por negociação) |
| 38 | Pagar.me não publica tabela de preços; encaminha para vendas | [Pagar.me](https://pagar.me/precos) | não datada | alta (ausência verificada) |
| 39 | **Confirmação independente** dos mínimos: Pluggy ~R$ 2.500/mês, Belvo ~R$ 6.000/mês, TecnoSpeed R$ 1.500 + R$ 540/mês | [TabNews](https://www.tabnews.com.br/GuilhermeVieira/estou-desenvolvendo-um-app-de-financas-pessoais-e-nao-consigo-pagar-o-open-finance-pluggy-r2-5k-mes-belvo-r6k-mes-tecnospeed-r1-5k-de-entrada-r540) | ~2026-05 | média-alta (publisher distinto, cotação própria) |
| 40 | Belvo: plano Launch a USD 1.000/mês; sandbox grátis só para teste, não produção | [Belvo](https://belvo.com/plans-and-pricing/) | não datada | alta (página oficial) |
| 41 | TecnoSpeed PlugBank não publica preço; formulário de contato comercial | [TecnoSpeed](https://tecnospeed.com.br/plugbank/api-open-finance/) | não datada | alta (ausência verificada) |
| 42 | Nibo: 5 níveis, desconto 30–50%, comissão quadrimestral, adesão gratuita | [Nibo](https://www.nibo.com.br/programa-de-parceria) | não datada | alta (página oficial) |
| 43 | Omie: programa de contador parceiro; termos em PDF não exposto; licença subsidiada | [Omie](https://www.omie.com.br/contadores-parceiros/) | não datada | média |
| 44 | Asaas: trilha de Parceiros de Distribuição inclui contadores; adesão gratuita; percentuais só no onboarding | [Asaas](https://materiais.asaas.com/parceiros) | não datada | alta |
| 45 | **Conta Azul publica desconto de 20% a 40%, não 85%**; 6 níveis; licença R$ 199,90 a R$ 99,90; adesão gratuita | [Conta Azul](https://contaazul.com/parceiros/) | não datada | alta (página oficial do programa) |
| 46 | "Mais de 10 mil parceiros ativos" — a cifra primária datada mais recente | [Conta Azul (blog)](https://contaazul.com/blog/conta-azul-lanca-novo-programa-de-parceria/) | 2024-09-05, atual. 2025-05-13 | alta (autorreportado, mas datado) |
| 47 | Asaas: sem mensalidade; PIX/boleto R$ 0,99 nos 3 primeiros meses e R$ 1,99 em regime; NF-e R$ 0,49 | [Asaas](https://www.asaas.com/precos-e-taxas) | não datada | alta (página oficial) |
| 48 | **Asaas já casa boleto pago por Pix via `txid` e dispara webhook** (a fonte nada diz sobre custo da conciliação) | [Asaas (blog)](https://blog.asaas.com/boleto-com-qr-code/) | 2026-07-23 | **alta** |
| 49 | **Conta Azul declara oficialmente que não concilia pagamentos feitos fora da plataforma; instrui cancelar boleto e importar OFX** | [Central de Ajuda Conta Azul](https://ajuda.contaazul.com/hc/pt-br/articles/43775485946253-Concilia%C3%A7%C3%A3o-como-automatizar-concilia%C3%A7%C3%A3o-de-pagamentos-Pix-de-faturas-geradas-como-boleto) | 2026-04-14 | **alta (fonte primária do incumbente)** |
| 50 | Cora: boleto com QR Code Pix gratuito; gestão de cobranças gratuita | [Cora](https://www.cora.com.br/conta-pj/gestao-de-cobrancas/) | 2025-04-07 (nota comparativa) | média-alta |
| 51 | Iugu empacota boleto, Pix, cartão e "Bolix" com conciliação por relatórios e extratos | [Iugu](https://www.iugu.com/iugu-cobranca) | não datada | média-alta |
| 52 | Finalidade conciliatória do `txid` na cobrança Pix | [TecnoSpeed (blog)](https://blog.tecnospeed.com.br/cobranca-pix-pago/) | não datada | média |
| 53 | `txid` e `EndToEndId` como mecanismo de conciliação Pix–ERP | [Bradata](https://www.bradata.com.br/blog/pix-integrado-erp-cobranca-conciliacao) | não datada | média |
| 54 | `TransactionIdentification` / `idConciliacaoRecebedor` na especificação oficial | [BACEN — repositório pix-api](https://github.com/bacen/pix-api/issues/77) | não datada | média-alta (repositório oficial) |
| 55 | Kamino: R$ 54 mi captados, aquisição da Nimbly, conciliação automática de extratos embutida | [Startups.com.br](https://startups.com.br/negocios/fintech/como-a-kamino-quer-se-destacar-em-gestao-financeira-para-pmes/) | não datada | média |
| 56 | Programas de parceria contábil são estruturados em torno de revenda de ERP | [GestãoClick](https://parceiro.gestaoclick.com.br/programa-parceria-contadores/) | não datada | média |

---
