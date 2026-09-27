# D1 — Screening do campo

Rodada 1.1. Orçamento consumido: 10 chamadas de ferramenta, 3 páginas efetivamente lidas (asaas.com/plugins, f360.com.br/blog, pluggy.ai) + 3 varreduras de busca. Cobertura parcial e declarada como tal nas Lacunas.

## Claims

- **A Pluggy opera como camada de infraestrutura de Open Finance com +130 instituições financeiras conectadas por uma única API e declara 400+ empresas usando a plataforma.**
  - source: https://pluggy.ai/
  - publisher: Pluggy (fornecedor, auto-reportado)
  - pub_date: desconhecida (homepage sem data)
  - accessed: 2026-08-19
  - confidence: média (número auto-reportado por fornecedor, não auditado; página sem data logo frescor não confirmável)
  - class: tech

- **A Pluggy é autorizada pelo Banco Central do Brasil como Iniciadora de Transação de Pagamento (ITP), o que permitiria a um terceiro construir iniciação de pagamento PIX sem obter licença própria.**
  - source: https://pluggy.ai/
  - publisher: Pluggy
  - pub_date: desconhecida
  - accessed: 2026-08-19
  - confidence: média (auto-declaração; não verificada contra a lista oficial de autorizadas do BCB nesta rodada)
  - class: regulatory

- **Conta Azul, Nibo, MarketUP, TOTVS e Kamino aparecem nomeados como clientes da Pluggy, indicando que a conexão bancária/Open Finance já está terceirizada pelos principais ERPs e plataformas financeiras de PME no Brasil.**
  - source: https://pluggy.ai/
  - publisher: Pluggy
  - pub_date: desconhecida
  - accessed: 2026-08-19
  - confidence: média
  - class: competitor

- **A MarketUP dá depoimento na página da Pluggy destacando "conciliação bancária integrada" como o valor entregue — ou seja, conciliação bancária básica já é feature comoditizada dentro de ERPs, não produto isolado.**
  - source: https://pluggy.ai/
  - publisher: Pluggy (depoimento de cliente, registro de marketing)
  - pub_date: desconhecida
  - accessed: 2026-08-19
  - confidence: baixa (registro de marketing, voz de fornecedor)
  - class: competitor

- **A Pluggy vende, além de conectores de dados, produtos de Pagamentos via PIX com liquidação D+0 e recorrência, Enriquecimento de Dados e Cash Management — cada um desses é um bloco pronto sobre o qual um time pequeno construiria aplicação.**
  - source: https://pluggy.ai/
  - publisher: Pluggy
  - pub_date: desconhecida
  - accessed: 2026-08-19
  - confidence: média
  - class: tech

- **O diretório de plugins e parceiros do Asaas lista ERPs/financeiros de PME já integrados: Bling, Conta Azul, Omie ERP, Tiny ERP, Nibo, Granatum Financeiro e bkper.**
  - source: https://www.asaas.com/plugins
  - publisher: Asaas (fornecedor)
  - pub_date: desconhecida (página de produto sem data)
  - accessed: 2026-08-19
  - confidence: alta (página oficial do próprio fornecedor listando seu ecossistema)
  - class: competitor

- **A maioria das integrações listadas pelo Asaas é intermediada por Pluga e Make (iPaaS), não por conectores nativos — sinal de que o ecossistema de integração ao redor do PSP é raso e construído por terceiros com no-code.**
  - source: https://www.asaas.com/plugins
  - publisher: Asaas
  - pub_date: desconhecida
  - accessed: 2026-08-19
  - confidence: alta
  - class: gtm

- **O diretório do Asaas NÃO lista nenhum plugin segmentado por vertical de saúde/clínicas, escolas, academias, condomínios, advogados, oficinas ou salões — o único vertical presente é EAD/educação (Twygo, Hotmart) e e-commerce (WooCommerce, Nuvemshop, Magento).**
  - source: https://www.asaas.com/plugins
  - publisher: Asaas
  - pub_date: desconhecida
  - accessed: 2026-08-19
  - confidence: média (ausência em UM diretório não prova ausência no mercado; ver Lacunas)
  - class: competitor

- **Emissão fiscal acoplada a recebimento já tem dois fornecedores de API nomeados no ecossistema Asaas: eNotas e NFE.io.**
  - source: https://www.asaas.com/plugins
  - publisher: Asaas
  - pub_date: desconhecida
  - accessed: 2026-08-19
  - confidence: alta
  - class: competitor

- **A Digital Manager Guru é parceira do Asaas para checkout e split de pagamento no nicho de infoprodutos, integrável sem desenvolvedor.**
  - source: https://blog.asaas.com/plugins-e-parceiros-do-asaas/
  - publisher: Asaas (blog do fornecedor)
  - pub_date: desconhecida
  - accessed: 2026-08-19
  - confidence: baixa (obtido via resumo de busca, página não lida na íntegra)
  - class: competitor

- **O volume de compras com cartão no Brasil foi de R$ 4 trilhões em 2024, segundo a Abecs, citado pela F360 — dimensiona o pool sobre o qual a conciliação de cartões opera.**
  - source: https://f360.com.br/blog/financas/software-de-conciliacao-de-cartoes/
  - publisher: F360 (ecoando a Abecs como fonte upstream)
  - pub_date: 2025-10-03
  - accessed: 2026-08-19
  - confidence: média (número é da Abecs; a F360 é ecoador. Dado de 2024 está fora da barra de 18 meses — tratar como histórico)
  - class: size/growth

- **Conciliação de cartões no Brasil tem fornecedores estabelecidos e nomeados: F360 Finanças, Conciliadora, SmartConcilia e Carat (Fiserv).**
  - source: https://f360.com.br/blog/financas/software-de-conciliacao-de-cartoes/ ; https://conciliadora.com.br/maquininha-de-cartao-que-permite-a-conciliacao-automatica ; https://sebrae.com.br/sites/PortalSebrae/ufs/sp/programas/sebrae-conecta-smartconcilia,14d39e39b1d2f710VgnVCM100000d701210aRCRD ; https://www.softwareexpress.com.br/pt/blog/conciliacao-automatica-do-carat-traz-agilidade-para-a-gestao-fin/
  - publisher: F360 / Conciliadora / Sebrae / Software Express
  - pub_date: F360 2025-10-03; demais desconhecidas
  - accessed: 2026-08-19
  - confidence: média (apenas a página da F360 foi lida na íntegra; as demais vêm de títulos e snippets de busca)
  - class: competitor

- **A SmartConcilia declara conciliar mais de 80 adquirentes no Brasil — número que quantifica a barreira de integração para quem quiser entrar em conciliação de cartões do zero.**
  - source: https://sebrae.com.br/sites/PortalSebrae/ufs/sp/programas/sebrae-conecta-smartconcilia,14d39e39b1d2f710VgnVCM100000d701210aRCRD
  - publisher: Sebrae (reproduzindo declaração do fornecedor)
  - pub_date: desconhecida
  - accessed: 2026-08-19
  - confidence: baixa (não lida na íntegra; número auto-reportado)
  - class: competitor

- **O Itaú firmou parceria com o ERP Soften para levar a venda da maquininha direto ao sistema de gestão, eliminando digitação e planilha na conciliação de PMEs — incumbente bancário atacando a mesma dor por integração vertical.**
  - source: https://www.letsmoney.com.br/noticias/itau-soften-maquininha-erp-pmes/
  - publisher: Let's Money (imprensa secundária)
  - pub_date: desconhecida
  - accessed: 2026-08-19
  - confidence: baixa (não lida na íntegra; publisher secundário)
  - class: competitor

- **O FintechLab mantém o Radar como mapeamento periódico do ecossistema, com publicações na categoria Radar em 2025-08 — mas nenhuma contagem ou lista de fintechs por categoria foi recuperada nesta rodada.**
  - source: https://fintechlab.com.br/index.php/category/radar/
  - publisher: FintechLab
  - pub_date: 2025-08 (item mais recente observado na listagem)
  - accessed: 2026-08-19
  - confidence: baixa (apenas metadado de listagem; conteúdo não lido)
  - class: size/growth

## Candidatos levantados

| # | Candidato | Área | Cliente pagante | Quem já faz (nomes) | Fonte |
|---|---|---|---|---|---|
| 1 | Conciliação de recebíveis de maquininha multi-adquirente para varejo multi-loja | conciliação financeira | Redes de varejo, franquias, food service com múltiplas lojas | F360 Finanças, Conciliadora, SmartConcilia (80+ adquirentes), Carat/Fiserv | f360.com.br/blog ; sebrae.com.br SmartConcilia ; conciliadora.com.br |
| 2 | Conciliação bancária automática via Open Finance embarcada em ERP de PME | conciliação financeira | ERPs e plataformas de gestão (B2B2B), não a PME direto | Pluggy como infraestrutura; Conta Azul, Nibo, MarketUP, TOTVS, Kamino já consumindo | pluggy.ai |
| 3 | Contas a pagar automatizadas com iniciação de pagamento PIX via ITP de terceiro | contas a pagar e receber | PMEs de médio porte, escritórios contábeis, BPO financeiro | Kamino (cliente Pluggy); Pluggy fornece o trilho ITP | pluggy.ai |
| 4 | Cash management / tesouraria multi-banco para PME com várias contas | gestão financeira PME | PME com 3+ bancos, grupos empresariais | Pluggy vende "Cash Management" como produto de API — concorrência na camada de aplicação NÃO mapeada nesta rodada | pluggy.ai |
| 5 | Categorização e enriquecimento de extratos (PFM/BFM white-label) | automação financeira | Fintechs, ERPs, bancos digitais | Pluggy ("Enriquecimento de Dados") | pluggy.ai |
| 6 | Cobrança recorrente com régua de inadimplência sobre PSP existente | cobrança PME | Prestadores de serviço com mensalidade | Asaas nativamente; réguas de terceiros montadas via Pluga/Make | asaas.com/plugins |
| 7 | Emissão fiscal automática disparada pelo recebimento (NF-e/NFS-e) | automação financeira | PMEs de serviço, e-commerce | eNotas, NFE.io | asaas.com/plugins |
| 8 | Split de pagamento e checkout para infoprodutos/marketplaces | pagamentos e PIX | Produtores digitais, marketplaces | Digital Manager Guru (parceira Asaas), Hotmart | blog.asaas.com/plugins-e-parceiros-do-asaas |
| 9 | Cobrança e conciliação para plataformas de EAD | vertical de nicho (educação) | Escolas/EAD, criadores de curso | Twygo e Hotmart já integrados ao Asaas | asaas.com/plugins |
| 10 | Ponte de pagamentos para e-commerce em plataformas de loja | pagamentos e PIX | Lojistas online | WooCommerce, Nuvemshop, Magento — plugins Asaas já existentes | asaas.com/plugins |
| 11 | Conector venda-maquininha para ERP em tempo real | conciliação financeira | PMEs varejistas | Itaú + Soften (parceria bancária) | letsmoney.com.br |
| 12 | Middleware de dados bancários para escritórios de contabilidade | Open Finance | Escritórios contábeis / BPO financeiro | Nibo e Conta Azul (clientes Pluggy) — nenhum player dedicado ao contador identificado nesta rodada | pluggy.ai |
| 13 | Camada de automação no-code ligando PSP a CRM/ERP | automação financeira | PMEs sem time de TI | Pluga e Make dominam essa ponte hoje no ecossistema Asaas | asaas.com/plugins |

Candidatos 14–15 (verticais aparentemente não-atendidos: saúde/clínicas, jurídico, construção, agro, salões, oficinas, condomínios) NÃO foram levantados com evidência nesta rodada — ver Lacunas. Não os registro como candidatos porque seria conclusão a partir de memória de treinamento.

## Pistas

- **Contradição de posicionamento**: a Pluggy vende ao mesmo tempo a infraestrutura (conectores, ITP, cash management, enriquecimento) e produtos que competem com o que seus próprios clientes construiriam em cima dela. Um fundador que construir "conciliação bancária" ou "cash management" está construindo o que o fornecedor de API já embala como produto — risco de compressão de margem e de o fornecedor subir a stack. Isso reposiciona a oportunidade para camadas que a Pluggy explicitamente NÃO vende: workflow, regra de negócio vertical, cobrança e recuperação de inadimplência.
- **Conciliação bancária virou feature, não produto.** Conta Azul, Nibo, MarketUP e TOTVS já compram o conector pronto. Entrar em "conciliação bancária para PME" agora é entrar depois da comoditização. Conciliação de CARTÕES (multi-adquirente, 80+ adquirentes) é caso diferente: a barreira é integração e não commodity — mas exatamente por isso é cara demais para 2 devs em 3 meses.
- **O ecossistema de integração do Asaas é intermediado por iPaaS (Pluga, Make), não por conectores nativos.** Sinal duplo: barreira de entrada baixa para quem quiser construir integrações verticais diretas, e indício de que ninguém investiu nelas ainda.
- **Ausência notável no diretório do Asaas**: nenhum plugin de saúde/clínicas, academias, condomínios, advogados, oficinas ou salões. Educação e e-commerce estão cobertos. Essa é a pista mais acionável da rodada, mas precisa ser testada contra os diretórios de Omie, Conta Azul e Bling antes de virar conclusão.
- **Incumbente bancário se movendo**: Itaú integrando maquininha direto no ERP de PME. Se bancos estão fechando a lacuna de conciliação por parceria com ERP, a janela em conciliação para PME está estreitando.
- **Pergunta aberta e bloqueante**: qual o custo real por conexão da Pluggy (e de Belvo/Klavi)? Sem tabela de preço pública, não há como verificar se R$1.000/mês de infraestrutura suporta um produto baseado em Open Finance. Isso trava os candidatos 2, 3, 4, 5 e 12.

## Lacunas

- **Preços de Open Finance as-a-service**: a página "Planos e Preços" da Pluggy existe mas não foi lida (orçamento esgotado). Sem isso, a viabilidade de R$1.000/mês para qualquer candidato baseado em Open Finance é INDETERMINADA. Prioridade máxima da próxima rodada; repetir para Belvo e Klavi.
- **Radar FintechLab 2025/2026**: procurei e não recuperei nenhuma contagem, lista por categoria ou dimensionamento de segmento. Só confirmei que o Radar existe e teve publicação em 2025-08. Nenhum dado de tamanho/crescimento do ecossistema foi obtido nesta rodada.
- **Diretórios de app de Omie, Conta Azul, Bling e Tiny**: aplicativos.omie.com.br não resolve DNS; bling.com.br/integracoes retorna 404. As URLs corretas desses marketplaces não foram encontradas. É a maior lacuna de screening — é exatamente ali que os micro-SaaS financeiros verticais brasileiros estariam listados, e é a evidência que faltou para responder a pergunta 3 (verticais atendidos vs. desatendidos).
- **Verticais brasileiros com fintech/SaaS financeiro dedicado**: nenhuma evidência recuperada para saúde, jurídico, construção, agro, salões, oficinas ou condomínios. Tenho crenças de treinamento sobre players nesses nichos que estou deliberadamente NÃO registrando como achado, conforme a regra 1.
- **Preços dos concorrentes de conciliação** (F360, Conciliadora, SmartConcilia): nenhum preço público recuperado. O artigo da F360 é peça promocional sem tabela de preço.
- **Regulatório**: nada recuperado de texto primário do Banco Central nesta rodada. A tese de que se pode operar cobrança/PIX sobre PSP ou ITP de terceiro sem licença própria está apoiada apenas em auto-declaração de fornecedor, não em norma. Verificar contra a resolução do BCB sobre ITP e contra a lista oficial de instituições autorizadas antes de qualquer decisão.
- **Frescor**: o único dado datado desta rodada é de 2025-10 (F360) — 10 meses, fora da barra de 6 meses para screening competitivo. Todas as páginas de fornecedor lidas são sem data. O screening competitivo desta rodada NÃO satisfaz a barra de frescor e deve ser tratado como orientação, não como retrato atual do mercado.
