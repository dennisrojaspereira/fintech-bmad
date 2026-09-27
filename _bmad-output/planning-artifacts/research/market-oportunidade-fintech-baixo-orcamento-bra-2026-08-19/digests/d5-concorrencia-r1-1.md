# D5 — Concorrência e substitutos

> Nota de execução: orçamento de 10 chamadas de ferramenta esgotado. Páginas de preço lidas com sucesso: Conta Azul, Bling, Cora. Asaas bloqueou o acesso (302 para tela de login), Nibo retornou 404 nas duas URLs tentadas. Tudo abaixo é evidência recuperada neste run; nada é conclusão de memória de treinamento.

## Claims

- **Conta Azul cobra R$ 159,90/mês (anual) a R$ 239,90/mês (trimestral) no plano de entrada "Essencial", posicionado para MEI com faturamento até R$ 81 mil/ano e 1 usuário.**
  - source: https://contaazul.com/planos/
  - publisher: Conta Azul
  - pub_date: desconhecida (página não data)
  - accessed: 2026-08-19
  - confidence: alta
  - class: pricing

- **A escada de preços da Conta Azul sobe rápido com o porte: Controle R$ 309,90–449,90/mês (2 usuários, empresas de R$ 81 mil–R$ 360 mil/ano), Avançado R$ 399,90–519,90/mês (5 usuários, R$ 360 mil–R$ 1,5 mi/ano) e Performance R$ 719,90–839,90/mês (15 usuários, acima de R$ 1,5 mi/ano).**
  - source: https://contaazul.com/planos/
  - publisher: Conta Azul
  - pub_date: desconhecida
  - accessed: 2026-08-19
  - confidence: alta
  - class: pricing

- **A página de planos da Conta Azul não discrimina quais funcionalidades financeiras (contas a pagar/receber, conciliação bancária, emissão de NF, cobrança) pertencem a qual plano — lista tudo como recurso genérico da plataforma.**
  - source: https://contaazul.com/planos/
  - publisher: Conta Azul
  - pub_date: desconhecida
  - accessed: 2026-08-19
  - confidence: alta
  - class: competitor

- **O Bling entra em R$ 60/mês (plano Cobalto, R$ 720/ano), com notas fiscais ilimitadas (NF-e, NFC-e, NFS-e), contas a pagar/receber básicas e até 5 usuários — ou seja, o piso do ERP brasileiro para PME está em ~R$ 60/mês, quase 3x abaixo do piso da Conta Azul.**
  - source: https://www.bling.com.br/planos
  - publisher: Bling (Grupo Locaweb)
  - pub_date: desconhecida
  - accessed: 2026-08-19
  - confidence: alta
  - class: pricing

- **No Bling, "gestão financeira completa" com conciliação bancária e emissão de boletos só aparece a partir do plano Titânio, R$ 120/mês (R$ 1.440/ano, até 5.000 pedidos, até 50 usuários) — conciliação é upsell, não recurso de entrada.**
  - source: https://www.bling.com.br/planos
  - publisher: Bling
  - pub_date: desconhecida
  - accessed: 2026-08-19
  - confidence: alta
  - class: pricing

- **Bling Diamante custa R$ 650/mês (R$ 7.800/ano, até 10.000 pedidos, 100 usuários) e o Elite é sob consulta com "capacidade de API flexível (até 8x maior)" — sinal de que o topo da linha já é vendido como plataforma/integração, não como software de fluxo de caixa.**
  - source: https://www.bling.com.br/planos
  - publisher: Bling
  - pub_date: desconhecida
  - accessed: 2026-08-19
  - confidence: média
  - class: pricing

- **A Cora oferece conta PJ com mensalidade zero, boleto grátis, PIX ilimitado e gratuito, TED gratuita e cartão sem anuidade — e empacota junto gestão de fluxo de caixa, gestão de cobranças, nota fiscal integrada e link de pagamento.**
  - source: https://www.cora.com.br/
  - publisher: Cora
  - pub_date: desconhecida
  - accessed: 2026-08-19
  - confidence: alta
  - class: pricing

- **A Cora ataca explicitamente o preço do boleto e do PIX dos bancos tradicionais, citando concorrentes que cobram "até R$ 9,00" por boleto e "até R$ 10,00" por PIX — o preço de referência de cobrança para PME está indo a zero.**
  - source: https://www.cora.com.br/
  - publisher: Cora
  - pub_date: desconhecida
  - accessed: 2026-08-19
  - confidence: média
  - class: competitor

- **A Cora anuncia um produto pago "Cora Pro" na home, mas não publica preço nem escopo — indício de que a monetização migrou do transacional para assinatura de software financeiro, mas sem número verificável.**
  - source: https://www.cora.com.br/
  - publisher: Cora
  - pub_date: desconhecida
  - accessed: 2026-08-19
  - confidence: baixa
  - class: competitor

- **Asaas captou R$ 35 milhões do Vivo Ventures e Kamino captou R$ 54 milhões em rodada co-liderada por Flourish Ventures e Quona Capital, ambas classificadas como fintechs de gestão financeira para PMEs.**
  - source: https://finsidersbrasil.com.br/negocios-em-fintechs/fintechs-de-gestao-financeira-para-pmes-recebem-novos-investimentos/
  - publisher: Finsiders Brasil (via resultado de busca; artigo não aberto diretamente)
  - pub_date: desconhecida
  - accessed: 2026-08-19
  - confidence: baixa
  - class: competitor
  - nota: fonte única, não lida na íntegra; valores de rodada não confirmados em segunda fonte independente

- **Metas auto-reportadas: Asaas projeta chegar a R$ 1 bilhão em 2026 e R$ 2 bilhões dois anos depois; Kamino espera superar R$ 54 milhões de receita recorrente anual em 2026.**
  - source: https://finsidersbrasil.com.br/negocios-em-fintechs/fintechs-de-gestao-financeira-para-pmes-recebem-novos-investimentos/
  - publisher: Finsiders Brasil (via snippet de busca)
  - pub_date: desconhecida
  - accessed: 2026-08-19
  - confidence: baixa
  - class: competitor
  - nota: auto-reportado, fonte única; a unidade de "R$ 1 bilhão" da Asaas não está desambiguada (TPV vs. receita) na evidência recuperada

- **O mercado brasileiro de fintech em 2025 registrou o menor número de rodadas dos últimos cinco anos — 106 operações movimentando US$ 2,77 bilhões, contra 244 rodadas em 2021 — ou seja, menos cheques e cheques maiores.**
  - source: https://startups.com.br/negocios/fintech/fintechs-brasileiras-entram-em-nova-fase-com-menos-rodadas-e-mais-fidcs/
  - publisher: Startups.com.br (via snippet de busca)
  - pub_date: desconhecida
  - accessed: 2026-08-19
  - confidence: baixa
  - class: competitor

- **No 2º trimestre de 2026 o ecossistema latino-americano movimentou US$ 3,03 bilhões em 129 rodadas, com o Brasil recebendo 57% do total — capital disponível para incumbentes se expandirem sobre nichos adjacentes.**
  - source: https://startups.com.br/negocios/fintech/fintechs-brasileiras-entram-em-nova-fase-com-menos-rodadas-e-mais-fidcs/
  - publisher: Startups.com.br (via snippet de busca)
  - pub_date: desconhecida
  - accessed: 2026-08-19
  - confidence: baixa
  - class: competitor

## Tabela de preços praticados

| produto | plano de entrada | preço/mês | o que inclui | URL | data de acesso |
|---|---|---|---|---|---|
| Conta Azul | Essencial | R$ 159,90 (anual) / R$ 239,90 (trimestral) | 1 usuário; alvo MEI até R$ 81 mil/ano; features financeiras não discriminadas por plano | https://contaazul.com/planos/ | 2026-08-19 |
| Conta Azul | Controle | R$ 309,90 / R$ 449,90 | 2 usuários; ME de R$ 81 mil a R$ 360 mil/ano | https://contaazul.com/planos/ | 2026-08-19 |
| Conta Azul | Avançado | R$ 399,90 / R$ 519,90 | 5 usuários; R$ 360 mil a R$ 1,5 mi/ano | https://contaazul.com/planos/ | 2026-08-19 |
| Conta Azul | Performance | R$ 719,90 / R$ 839,90 | 15 usuários; acima de R$ 1,5 mi/ano | https://contaazul.com/planos/ | 2026-08-19 |
| Bling | Cobalto | R$ 60 (R$ 720/ano) | NF ilimitadas, contas a pagar/receber básicas, até 200 pedidos, 5 usuários | https://www.bling.com.br/planos | 2026-08-19 |
| Bling | Titânio | R$ 120 (R$ 1.440/ano) | + conciliação bancária, emissão de boletos, dashboards, até 5.000 pedidos, 50 usuários | https://www.bling.com.br/planos | 2026-08-19 |
| Bling | Diamante | R$ 650 (R$ 7.800/ano) | + suporte premium, gerente dedicado, até 10.000 pedidos, 100 usuários | https://www.bling.com.br/planos | 2026-08-19 |
| Bling | Elite | sob consulta | + API até 8x maior, usuários ilimitados | https://www.bling.com.br/planos | 2026-08-19 |
| Cora (conta PJ) | Conta PJ | R$ 0 (sem mensalidade/manutenção) | boleto grátis, PIX e TED gratuitos, cartão sem anuidade, fluxo de caixa, cobranças, NF integrada, link de pagamento | https://www.cora.com.br/ | 2026-08-19 |
| Cora Pro | Cora Pro | não publicado | escopo não divulgado na home | https://www.cora.com.br/ | 2026-08-19 |
| Asaas | — | NÃO OBTIDO | página /precos redireciona para login (302) | https://www.asaas.com/precos | 2026-08-19 |
| Nibo | — | NÃO OBTIDO | /precos e /planos-e-precos retornam 404 | https://www.nibo.com.br/precos | 2026-08-19 |
| Omie, Tiny, Granatum | — | NÃO OBTIDO | fora do orçamento de chamadas | — | — |

Barra de frescor: nenhuma das três páginas lidas exibe data de publicação ou de atualização. Registro a data de acesso (2026-08-19) e declaro a data de publicação desconhecida — o requisito de "≤3 meses" não é verificável nessas fontes, apenas presumível por serem páginas comerciais vivas.

## Vazios e saturações

**Pagamentos e PIX — SATURADO.** Evidência direta: a Cora entrega PIX ilimitado gratuito, boleto grátis e TED grátis com mensalidade zero, financiado por outro produto. Um time de 2 devs não tem como competir em preço contra zero subsidiado, nem tem a licença para monetizar float. Área a evitar como produto principal.

**Cobrança para pequenas empresas — SATURADO/DISPUTADO.** Cora empacota "gestão de cobranças" e link de pagamento de graça na conta PJ; a Asaas, o player dedicado, acabou de receber cheque estratégico de corporate VC (Vivo Ventures, R$ 35 mi — confidence baixa, fonte única). O preço de referência do boleto está sendo empurrado a zero pela própria Cora, que publica comparativo contra "até R$ 9,00". Margem estruturalmente comprimida.

**Gestão financeira para PMEs (ERP leve) — SATURADO por baixo.** O Bling ancora o piso em R$ 60/mês com NF ilimitada. Qualquer produto novo de gestão financeira genérica precisa cobrar menos que R$ 60 ou provar valor acima de R$ 160 (Conta Azul Essencial) — e ambos os extremos são ruins para um MVP de 3 meses.

**Conciliação financeira — DISPUTADO, mas com fresta.** Evidência: no Bling a conciliação bancária não está no plano de entrada, só a partir de R$ 120/mês (Titânio). Na Conta Azul, a conciliação é citada como recurso da plataforma sem estar atribuída a nenhum plano específico — tratada como feature secundária, não como produto. Isso é o padrão clássico de vazio: todo mundo lista, ninguém vende como produto principal. Fresta plausível, não comprovada nesta rodada.

**Contas a pagar e receber — DISPUTADO.** Presente no plano mais barato do Bling (R$ 60) como "básico", presente na Conta Azul sem discriminação de plano. Commoditizado como checkbox; a diferenciação teria de vir de automação (captura de nota, agendamento, aprovação), não do cadastro em si.

**Automação financeira — VAZIO PARCIAL (não verificado).** Não recuperei nesta rodada nenhum player brasileiro dedicado que venda automação financeira como produto autônomo para PME — o que vi foi automação embutida em ERP (Bling) e em conta PJ (Cora). Registro como hipótese de vazio, não como achado: ausência de evidência neste orçamento de busca não é evidência de ausência.

**Open Finance — NÃO AVALIADO.** Nenhuma evidência recuperada. Vazio ou saturação indeterminados.

**Fintechs verticais de nicho — NÃO AVALIADO diretamente.** O único sinal adjacente é o funding de Kamino e Asaas em "gestão financeira para PMEs" (fonte única, confidence baixa), o que sugere que o genérico está capitalizado e o nicho vertical é onde sobra espaço — mas isso é inferência, não evidência.

## Pistas

- **Cora Pro** é a entidade nova mais relevante: uma conta PJ de mensalidade zero lançando um tier pago sem preço público significa que o incumbente gratuito está subindo para software financeiro por assinatura. Se o Cora Pro cobrir conciliação e contas a pagar, ele mata simultaneamente o vazio de conciliação e o de contas a pagar. Prioridade máxima de investigação na próxima rodada.
- **Kamino** apareceu como player que eu não tinha na lista das 8 áreas — gestão financeira para PMEs, com ARR auto-reportado de R$ 54 mi para 2026. Merece screening dedicado.
- **Contradição de posicionamento**: Bling entra em R$ 60/mês e Conta Azul em R$ 159,90/mês para clientes nominalmente do mesmo porte (MEI/ME). Ou os produtos não são substitutos reais, ou a Conta Azul está vendendo para um segmento acima do que a página declara. Isso muda o cálculo de willingness-to-pay do fundador.
- **Pergunta aberta**: por que a página de planos da Conta Azul deixou de mapear features por plano? Pode indicar reempacotamento recente (e portanto instabilidade competitiva) ou venda assistida.
- **Sinal de mercado**: menos rodadas e cheques maiores (106 operações em 2025 vs. 244 em 2021) favorece o entrante bootstrapped — menos concorrentes novos financiados — mas também significa incumbentes com caixa para engolir nichos adjacentes.

## Lacunas

1. **Preços da Asaas — não obtidos.** `asaas.com/precos` e `www.asaas.com/precos` respondem 302 para `/login/auth`. A tabela de tarifas da Asaas é a peça mais importante que falta, porque define o teto de preço de qualquer produto de cobrança. Próxima tentativa: `asaas.com/tarifas`, `asaas.com/precos-e-taxas`, ou a central de ajuda.
2. **Preços do Nibo — não obtidos.** `/precos` e `/planos-e-precos/` retornam 404. URL correta desconhecida.
3. **Omie, Tiny e Granatum — não consultados.** Fora do orçamento de chamadas. Sem eles, o mapa de preços de gestão financeira para PME está incompleto em três players relevantes.
4. **Vagas abertas — não pesquisadas.** Nenhuma consulta a páginas de carreira de Cora, Asaas, Conta Azul, Bling ou Nibo. Este era o sinal pedido para inferir direção de expansão dos incumbentes e não foi coletado. É a lacuna metodológica mais séria desta rodada.
5. **Preço do Cora Pro — não publicado** na home; nenhuma página dedicada consultada.
6. **Substituto real (planilha, WhatsApp, contador, internet banking) — ZERO evidência recuperada.** Não fiz nenhuma busca sobre como PMEs brasileiras resolvem controle financeiro hoje sem software. A pergunta 6 da dimensão está inteiramente sem resposta e não deve ser preenchida por inferência do sintetizador.
7. **Regra de duas fontes não satisfeita** para nenhum número de tração ou captação. Todos os claims de funding e receita nesta rodada são fonte única, via snippet de busca, sem o artigo lido na íntegra.
8. **Datas de publicação ausentes** em 100% das páginas de preço lidas — a barra de frescor de ≤3 meses não pôde ser verificada.
