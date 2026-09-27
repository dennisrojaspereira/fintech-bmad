# D7 — Custo real do stack e lock-in

> Nota de execução: orçamento de 10 chamadas de ferramenta esgotado. Fontes efetivamente lidas: 3 (Pluggy, Efí, Pagar.me). Quatro tentativas de fetch retornaram 404 ou redirect para login (Belvo em 3 URLs, Asaas em 2 URLs) — registradas em Lacunas. A REGRA DE DUAS FONTES **não** foi satisfeita para nenhuma figura: cada preço abaixo tem UMA fonte oficial. Tratar como direcional, não como decidido.

## Claims

- **Pluggy cobra pelo produto "Dados" (agregação Open Finance / bancária) a partir de R$ 2.500/mês, como MÍNIMO MENSAL — 2,5x o teto de infraestrutura inteiro do fundador.**
  - source: https://pluggy.ai/precos
  - publisher: Pluggy
  - pub_date: desconhecida (página não data)
  - accessed: 2026-08-19
  - confidence: média (fonte oficial, mas sem segunda confirmação; "a partir de" sugere que o valor real negociado pode ser maior)
  - class: pricing

- **Pluggy cobra o produto "Pagamentos" (iniciação de pagamento / Pix via Open Finance) a partir de R$ 500/mês, mínimo mensal SEPARADO do produto Dados.**
  - source: https://pluggy.ai/precos
  - publisher: Pluggy
  - pub_date: desconhecida
  - accessed: 2026-08-19
  - confidence: média
  - class: pricing

- **Na Pluggy, Dados e Pagamentos são produtos separados, "cada um com seu mínimo mensal" — quem quiser agregação + iniciação paga os dois mínimos somados (a partir de R$ 3.000/mês).**
  - source: https://pluggy.ai/precos
  - publisher: Pluggy
  - pub_date: desconhecida
  - accessed: 2026-08-19
  - confidence: média
  - class: pricing

- **O modelo de cobrança da Pluggy é mínimo mensal com volume incluído + excedente cobrado POR REQUISIÇÃO DE API; a tabela de preço por requisição não é publicada, exigindo "fale com a gente".**
  - source: https://pluggy.ai/precos
  - publisher: Pluggy
  - pub_date: desconhecida
  - accessed: 2026-08-19
  - confidence: média
  - class: pricing

- **Pluggy oferece 14 dias de teste grátis em ambiente de PRODUÇÃO sem cartão de crédito; ao fim do teste as conexões PAUSAM até um plano ser ativado.**
  - source: https://pluggy.ai/precos
  - publisher: Pluggy
  - pub_date: desconhecida
  - accessed: 2026-08-19
  - confidence: média
  - class: tech

- **A Efí (ex-Gerencianet) cobra Pix via API (QR Code dinâmico) e Pix Cobrança a 1,19% por transação, sem mensalidade e sem taxa de abertura de conta.**
  - source: https://sejaefi.com.br/tarifas
  - publisher: Efí Bank
  - pub_date: desconhecida (a página avisa "as tarifas podem variar de acordo com a data de contratação")
  - accessed: 2026-08-19
  - confidence: média
  - class: pricing

- **A Efí cobra R$ 3,45 por boleto PAGO; emissão, cancelamento e boletos não pagos são gratuitos — ou seja, custo zero em boleto não convertido.**
  - source: https://sejaefi.com.br/tarifas
  - publisher: Efí Bank
  - pub_date: desconhecida
  - accessed: 2026-08-19
  - confidence: média
  - class: pricing

- **A Efí cobra Pix Automático a R$ 3,50 por transação (valor fixo, não percentual) — modelo caro para recorrência de ticket baixo.**
  - source: https://sejaefi.com.br/tarifas
  - publisher: Efí Bank
  - pub_date: desconhecida
  - accessed: 2026-08-19
  - confidence: média
  - class: pricing

- **Cartão de crédito online na Efí: 3,49% à vista, 3,99% em 2x–6x, 4,39% em 7x–12x; antecipação de recebíveis a 4% por evento, teto R$ 30,00 por borderô.**
  - source: https://sejaefi.com.br/tarifas
  - publisher: Efí Bank
  - pub_date: desconhecida
  - accessed: 2026-08-19
  - confidence: média
  - class: pricing

- **A página de tarifas da Efí não menciona mínimo mensal, pacote mínimo nem taxa de setup — manutenção mensal declarada como GRÁTIS.**
  - source: https://sejaefi.com.br/tarifas
  - publisher: Efí Bank
  - pub_date: desconhecida
  - accessed: 2026-08-19
  - confidence: média
  - class: pricing

- **Pagar.me (grupo Stone) NÃO publica tabela de preços: a página comercial fala em "as melhores taxas" e encaminha para o funil de vendas / telefone 4004-1330 — preço é negociado.**
  - source: https://pagar.me/precos
  - publisher: Pagar.me / Stone
  - pub_date: desconhecida
  - accessed: 2026-08-19
  - confidence: alta (ausência verificada diretamente na página oficial)
  - class: pricing

## Tabela de custo

| fornecedor | categoria | modelo de cobrança | preço | mínimo mensal? | sandbox grátis? | URL | data de acesso |
|---|---|---|---|---|---|---|---|
| Pluggy — produto "Dados" | Open Finance / agregação | mínimo mensal + excedente por requisição de API | a partir de R$ 2.500/mês; preço por requisição não publicado | SIM — R$ 2.500/mês | Trial de 14 dias em produção, sem cartão; conexões pausam depois | https://pluggy.ai/precos | 2026-08-19 |
| Pluggy — produto "Pagamentos" | Iniciação de pagamento / Pix Open Finance | mínimo mensal + excedente por requisição | a partir de R$ 500/mês | SIM — R$ 500/mês (separado de Dados) | mesmo trial de 14 dias | https://pluggy.ai/precos | 2026-08-19 |
| Efí (ex-Gerencianet) | Cobrança / Pix / boleto | 100% variável por transação | Pix API 1,19%; boleto pago R$ 3,45; Pix Automático R$ 3,50; cartão 3,49%–4,39% | NÃO mencionado; mensalidade GRÁTIS | não declarado na página de tarifas (lacuna) | https://sejaefi.com.br/tarifas | 2026-08-19 |
| Pagar.me / Stone | Cobrança / adquirência | não publicado | "fale com vendas" | desconhecido | desconhecido | https://pagar.me/precos | 2026-08-19 |
| Belvo | Open Finance / agregação | NÃO RECUPERADO | — | — | — | 404 em /pt-br/precos/, /pricing/, /pt-br/pricing/ | 2026-08-19 |
| Asaas | Cobrança / Pix / boleto | NÃO RECUPERADO | — | — | — | /precos e /tarifas redirecionam para /login/auth | 2026-08-19 |

## Cabe em R$ 1.000/mês?

**Open Finance / agregação de dados — NÃO.**
Cálculo explícito: mínimo mensal da Pluggy para o produto Dados = R$ 2.500/mês, cobrado no mês 1, com zero cliente pagante. Teto de infraestrutura = R$ 1.000/mês. Déficit = **R$ 1.500/mês (250% do teto) antes de qualquer hospedagem, banco de dados ou domínio**. Um produto cuja proposta de valor central é agregação/conciliação via Open Finance está fora do orçamento na configuração declarada, independentemente do número de clientes — o mínimo é piso, não função do volume. O trial de 14 dias cobre validação técnica, não os 3 meses até MVP nem o período até o primeiro cliente pagante; ao fim dele "as conexões pausam", o que significa produto morto em ~2 semanas se não houver contrato assinado.

Consequência de modelagem: no modelo de mínimo mensal, o custo por cliente é **fixo e regressivo** — R$ 2.500 ÷ 1 cliente = R$ 2.500/cliente; ÷ 20 clientes = R$ 125/cliente/mês. Para o custo de agregação cair abaixo de ~R$ 50/cliente/mês seriam necessários ~50 clientes. Ou seja: a economia unitária só fecha depois de uma escala que o cenário de 3 meses não produz. **O mínimo mensal é exatamente o mecanismo que mata este orçamento**, como o brief antecipou.

**Iniciação de pagamento via Open Finance (Pluggy Pagamentos) — DEPENDE, e é apertado.**
Cálculo: R$ 500/mês de mínimo consome 50% do teto, sobrando R$ 500/mês para hospedagem + banco + observabilidade + qualquer outra API. Viável no papel para um MVP enxuto, mas não deixa margem para adicionar o produto Dados (que somaria R$ 2.500) nem folga para o excedente por requisição, cujo preço unitário não é publicado — risco de conta variável não estimável antes de falar com vendas.

**Cobrança / Pix / boleto — SIM, com custo fixo ZERO.**
Cálculo com Efí: mensalidade R$ 0 + setup R$ 0 + abertura de conta R$ 0 = **R$ 0/mês de custo fixo**. Todo o custo é variável e proporcional a transação processada:
- Pix a 1,19%: consumir R$ 1.000 de tarifa exige R$ 84.033 de volume transacionado no mês (1.000 ÷ 0,0119).
- Boleto a R$ 3,45 por boleto **pago**: R$ 1.000 equivale a 289 boletos pagos/mês; boletos emitidos e não pagos custam R$ 0, o que elimina o risco de queimar orçamento com cobrança que não converte.
- Pix Automático a R$ 3,50 fixo: 20 clientes com 1 cobrança recorrente mensal cada = R$ 70/mês. Mas se o produto for recorrência de ticket baixo com muitas cobranças, o valor fixo domina: 300 cobranças/mês = R$ 1.050 e estoura o teto sozinho.

Ressalva material: essas tarifas são, tipicamente, custo da transação do cliente final e repassáveis/embutíveis no take rate — diferente do mínimo de Open Finance, que é custo puro do fundador. Isso torna cobrança/Pix estruturalmente compatível com orçamento apertado: **custo variável repassável vs. custo fixo não repassável**.

**Fixo vs. variável — leitura de arquitetura de custo.**
- Custo FIXO que não escala com clientes (perigoso a zero cliente): mínimos mensais de Open Finance (Pluggy Dados R$ 2.500, Pagamentos R$ 500).
- Custo VARIÁVEL que só existe quando há receita (seguro): tarifas por transação da Efí.
- Regra derivada para a decisão do fundador: **cada mínimo mensal contratado antecipa despesa contra receita inexistente e encurta o runway; cada tarifa por transação só dispara depois que o cliente pagou.** Sob teto de R$ 1.000/mês e 3 meses até MVP, a oportunidade que depende de mínimo mensal de agregação é a mais frágil do conjunto.

**Hospedagem** — não recuperada neste run (orçamento esgotado). Não há evidência para afirmar quanto sobra depois da infra de aplicação. Lacuna declarada.

## Pistas

- Entidade/mecanismo novo: a Pluggy separa "Dados" e "Pagamentos" em produtos com mínimos independentes — armadilha de precificação para quem assume que uma conta Open Finance cobre leitura e iniciação. Vale confirmar se existe plano combinado.
- Contradição em potencial: "a partir de R$ 2.500/mês" com preço por requisição não publicado significa que o valor efetivo só aparece em proposta comercial. Toda modelagem financeira construída sobre R$ 2.500 é piso otimista.
- Pagar.me não publicar preço é achado de velocidade, não só de custo: negociação com funil de vendas de grupo Stone insere semanas de calendário num cronograma de 3 meses. A Efí, que publica tarifa e abre conta grátis, é auto-serviço — o time de 2 devs integra sem falar com ninguém.
- Asaas redirecionar /precos e /tarifas para /login/auth sugere que a tabela vive atrás de cadastro. Fricção menor que negociação, mas ainda não é preço público verificável.
- Pergunta aberta que decide a dimensão: existe fornecedor de Open Finance com preço por conexão ativa (por item/mês) SEM mínimo mensal, ou em modelo pay-as-you-go? Se existir, a categoria de conciliação/agregação volta ao jogo. Se não existir no mercado brasileiro, a conclusão "agregação está fora do teto" endurece.
- Pergunta aberta sobre lock-in não respondida por evidência: nenhuma das páginas lidas expôs prazo de contrato, multa de rescisão ou termos de exportação de dados.

## Lacunas

Procurado e NÃO encontrado neste run:

1. **Belvo — página de preços não localizada.** 404 em `https://belvo.com/pt-br/precos/`, `https://belvo.com/pricing/` e `https://belvo.com/pt-br/pricing/`. Não é possível afirmar que a Belvo não publica preço; é possível afirmar que o preço não está nas URLs canônicas testadas. Sem segundo ponto de comparação para o custo de conexão de Open Finance — a lacuna mais grave deste digest, porque a viabilidade da categoria repousa hoje sobre um único fornecedor.
2. **Asaas — preço atrás de login.** `https://www.asaas.com/precos` e `https://www.asaas.com/tarifas` redirecionam (302) para `http://www.asaas.com/login/auth`. Tabela de Pix/boleto do Asaas não verificada.
3. **Pagar.me — fornecedor NÃO publica preço.** Confirmado por leitura direta: nenhuma taxa numérica na página comercial, encaminhamento para vendas. ACHADO, não lacuna: implica negociação e prazo.
4. **Custo por CONEXÃO BANCÁRIA ATIVA por mês, por cliente** — não publicado por nenhuma fonte lida. A Pluggy expõe mínimo mensal + excedente por requisição, não preço por item/conexão. A pergunta 3 do brief permanece sem resposta com evidência.
5. **Não cobertos por esgotamento de orçamento (zero tentativas):** Iugu, Celcoin, Stark Bank, Klavi, CNPJá, Serpro, BigDataCorp, Focus NFe, NFE.io e todos os provedores de hospedagem.
6. **Sandbox da Efí** — a página de tarifas não menciona ambiente de homologação/sandbox. Não verificado.
7. **Lock-in e custo de saída (pergunta 5 do brief)** — ZERO evidência recuperada. Nenhum contrato, prazo de fidelidade, multa de rescisão ou política de exportação de dados foi lido. Qualquer afirmação sobre lock-in neste run seria memória de treinamento, portanto omitida.
8. **REGRA DE DUAS FONTES não satisfeita** para nenhum preço listado. Todos os valores têm uma única página oficial de origem. Nenhuma página trazia data de publicação, logo a BARRA DE FRESCOR (≤3 meses) não pôde ser verificada — apenas a data de acesso (2026-08-19) é conhecida, e a Efí avisa explicitamente que tarifas variam conforme a data de contratação.
