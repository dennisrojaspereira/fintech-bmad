# V1 — Verificação: custo de Open Finance e de cobrança

Run de verificação executado em 2026-08-19. Orçamento: 6 fontes lidas / 12 chamadas — consumido integralmente.
Nenhuma conclusão abaixo vem de memória de treinamento; todas apontam para material recuperado neste run.

## Afirmação A — verificada (escopo parcial: só a perna "Dados")

**Alegação:** Pluggy cobra mínimo mensal de R$ 2.500 (Dados) e R$ 500 (Pagamentos), produtos separados com mínimos independentes.

**A1 — R$ 2.500/mês mínimo para Dados: VERIFICADA por fonte independente.**

- source: https://www.tabnews.com.br/GuilhermeVieira/estou-desenvolvendo-um-app-de-financas-pessoais-e-nao-consigo-pagar-o-open-finance-pluggy-r2-5k-mes-belvo-r6k-mes-tecnospeed-r1-5k-de-entrada-r540
  - publisher: TabNews (comunidade de devs BR) — autor GuilhermeVieira, relato de cotação própria
  - pub_date: "3 meses atrás" no momento do acesso (≈ maio/2026); a plataforma não expôs data absoluta na extração
  - accessed: 2026-08-19
  - confidence: média-alta para o valor, média para a data
  - trecho: "Pluggy: ~R$ 2.500/mês" — no mesmo post, "Belvo: ~R$ 6.000/mês" e "Tecnospeed: R$ 1.500 de adesão + R$ 540/mês"
  - por que conta como independente: publisher distinto do fornecedor, com dado próprio (cotação levantada pelo autor), não republicação da página de preços

- source: https://www.pluggy.ai/precos (fonte primária do fornecedor, recuperada neste run apenas via snippet de busca)
  - publisher: Pluggy (o próprio fornecedor)
  - pub_date: ausente
  - accessed: 2026-08-19
  - confidence: alta para a estrutura, nula como confirmação independente do valor
  - conteúdo recuperado: dois produtos com mínimos distintos (Dados R$ 2.500, Pagamentos R$ 500), volume incluído dentro do mínimo, excedente cobrado por request, trial de 14 dias em produção sem cartão

**A2 — R$ 500/mês mínimo para Pagamentos e a independência entre os dois mínimos: NÃO VERIFICADA.**
Nenhuma fonte fora da Pluggy citou o número R$ 500 nem confirmou que os dois mínimos são cumulativos (isto é: se o cliente contrata os dois, paga R$ 3.000 ou apenas o maior). Isso é materialmente relevante para a decisão e permanece sinalizado.

**Tentativa de terceira fonte que falhou:** https://blog.usesecuro.com/post/pluggy-quanto-custa-usar-api-open-banking — publisher Securo, pub_date 2026-07-14, accessed 2026-08-19, confidence nula para preço. O post é promocional e **não publica nenhum número**; trecho literal: "Para saber os valores mais atuais e os detalhes por faixa de uso, sempre recomendo acessar as páginas oficiais da Pluggy." Registrado como fonte inútil para preço, exatamente o padrão de roundup previsto nas regras.

## Afirmação B — não verificada (confirmada por primária do fornecedor, sem contraparte independente)

**Alegação:** Efí cobra Pix via API a 1,19% por transação e boleto a R$ 3,45 apenas quando pago, sem mensalidade e sem taxa de abertura de conta.

- source: https://sejaefi.com.br/tarifas
  - publisher: Efí Bank (o próprio fornecedor) — tabela de tarifas oficial, Conta Empresas
  - pub_date: ausente na página; sem carimbo de atualização
  - accessed: 2026-08-19
  - confidence: alta para os valores vigentes, mas é o mesmo emissor da afirmação
  - trechos literais: "Receber por QR Code dinâmico 1,19%"; "Recebimento R$3,45"; "Emissão, baixa, cancelamento e boletos não pagos GRÁTIS"; "Abertura de conta GRÁTIS"; "Manutenção da conta GRÁTIS"
  - ressalva literal da própria página, que enfraquece o uso da tarifa como número fixo de modelagem: "As tarifas podem variar de acordo com a data de contratação e/ou negociações comerciais."

**Precisão a corrigir na afirmação:** o 1,19% está publicado especificamente para **recebimento por QR Code dinâmico** (o caminho da API), não como "1,19% por transação Pix" genérico. Emissão de boleto, baixa, cancelamento e boletos não pagos aparecem como grátis; o R$ 3,45 incide sobre **recebimento** de boleto. A redação da afirmação é compatível com a tabela, mas o escopo "QR dinâmico" precisa ser preservado.

**Por que o veredito é "não verificada" e não "verificada":** as duas evidências disponíveis (página de tarifas e as discussões em comunidade.sejaefi.com.br, estas últimas apenas em snippet de busca, não lidas) são **do mesmo publisher**. Pela definição de independência do contrato, isso é confirmação primária da estrutura de cobrança, não checagem independente do valor. Nenhum terceiro com dado próprio coube no orçamento. A afirmação permanece de pé e sinalizada.

- source secundária não lida (registrada como pista): https://comunidade.sejaefi.com.br/discussao/custos-taxas-api-pix-4 e https://comunidade.sejaefi.com.br/discussao/tarifas-api-pix-transferencia-contas-efi-13 — publisher Efí (fórum próprio, conteúdo de usuários), accessed 2026-08-19 apenas como resultado de busca, confidence baixa. Snippets convergem com 1,19% via API e "sem tarifa para criar cobrança nem para devolução".

## Existe fornecedor sem mínimo mensal?

| fornecedor | preço público? | modelo | mínimo mensal | URL | data de acesso |
|---|---|---|---|---|---|
| Pluggy | sim (parcial) | mínimo mensal com volume incluído + excedente por request; produtos Dados e Pagamentos separados | R$ 2.500 (Dados) / R$ 500 (Pagamentos) | https://www.pluggy.ai/precos | 2026-08-19 |
| Belvo | sim (só o plano de entrada) | assinatura por plano; "Growth" e acima são "Custom" / contact sales | USD 1.000/mês (plano Launch) | https://belvo.com/plans-and-pricing/ | 2026-08-19 |
| TecnoSpeed (PlugBank) | **não publica preço** | negociado; formulário "nossa equipe entra em contato em até 24h" | não publicado; terceiro relata R$ 1.500 de adesão + R$ 540/mês | https://tecnospeed.com.br/plugbank/api-open-finance/ | 2026-08-19 |
| Klavi | **não publica preço** | não divulgado; site institucional sem página de preços nos resultados | desconhecido | https://klavi.ai/ | 2026-08-19 |
| Iniciador | **não publica preço** (nenhuma página de preço apareceu na busca) | desconhecido | desconhecido | — sem URL de preço recuperada | 2026-08-19 |
| Quanto | **não publica preço** (nenhuma página de preço apareceu na busca) | desconhecido | desconhecido | — sem URL de preço recuperada | 2026-08-19 |
| Celcoin | **não publica preço**; citada apenas como instituição autorizada | desconhecido | desconhecido | https://www.tabnews.com.br/GuilhermeVieira/estou-desenvolvendo-um-app-de-financas-pessoais-e-nao-consigo-pagar-o-open-finance-pluggy-r2-5k-mes-belvo-r6k-mes-tecnospeed-r1-5k-de-entrada-r540 | 2026-08-19 |
| Sensedia | não investigado dentro do orçamento (é plataforma de API management, não agregador de dados) | — | — | — | — |

Notas de leitura da tabela:

- Belvo: o sandbox é grátis mas explicitamente não serve para produção — "Sandbox access is free and intended for testing and evaluation purposes only." Não há free tier de produção. A página não menciona pay-as-you-go, preço por conexão ativa nem por link. Conversão de USD 1.000 para BRL não foi recuperada neste run; em qualquer câmbio plausível o valor estoura o teto de R$ 1.000.
- Pluggy: o trial de 14 dias em produção sem cartão e o app de consumidor "Meu Pluggy" existem, mas nenhum dos dois é plano de produção contínuo — não resolvem o teto.
- TecnoSpeed é o único candidato cujo mensal relatado (R$ 540) cabe sob R$ 1.000, mas o número vem de relato de terceiro na TabNews, **não é confirmado pelo fornecedor**, e vem acompanhado de R$ 1.500 de adesão. A página oficial do produto não publica nenhum valor.

**Conclusão explícita:** não foi encontrado, neste run, nenhum fornecedor brasileiro de agregação de dados bancários / Open Finance que publique modelo pay-as-you-go, preço por conexão ativa ou plano de produção sem mínimo mensal — o padrão do mercado é mínimo mensal com volume incluído (Pluggy, Belvo) ou preço não publicado sob negociação comercial (TecnoSpeed, Klavi, Iniciador, Quanto, Celcoin), e o único mensal relatado abaixo de R$ 1.000 (TecnoSpeed, R$ 540 + R$ 1.500 de adesão) é dado de terceiro não confirmado pelo fornecedor.

## Lacunas

1. **R$ 500 do produto Pagamentos da Pluggy** — nenhuma fonte independente citou esse número. Não sei se os mínimos são cumulativos quando se contrata Dados + Pagamentos. Impacto direto no orçamento modelado.
2. **Fonte independente para as tarifas da Efí** — tudo que encontrei é do próprio emissor (site de tarifas + fórum da Efí). Não coube no orçamento buscar um comparador de gateways com dado próprio. A afirmação B fica de pé porém sinalizada.
3. **Preço da Klavi, Iniciador, Quanto e Celcoin** — nenhuma página de preços apareceu nas buscas; para Iniciador e Quanto não recuperei sequer URL de preço para citar como prova de "não publica". O achado "não publica preço" para esses dois é inferido de ausência em resultado de busca, não de página lida — evidência mais fraca que a da TecnoSpeed, onde a página foi lida e a ausência de preço confirmada.
4. **Sensedia** — não investigada; avaliada como fora da categoria (gestão/gateway de APIs, não agregador de dados de Open Finance), mas isso não foi confirmado por fonte neste run.
5. **Data de publicação** — nem a página de preços da Pluggy, nem a de tarifas da Efí, nem a de planos da Belvo carregam data ou versão. Todos os valores devem ser tratados como "vigentes em 2026-08-19, sem garantia de estabilidade", agravado pela ressalva contratual da Efí sobre variação por negociação.
6. **Câmbio USD/BRL** para converter o plano Launch da Belvo não foi recuperado; a conclusão de que estoura o teto não depende do valor exato.
