# D3 — Tamanho alcançável e segmentos

> Nota de execução: orçamento de 10 chamadas / 5 fontes lidas esgotado. Duas leituras falharam por razões técnicas (PDF primário do MDIC não parseou; TI Inside retornou HTTP 403), o que rebaixa a confiança de dois blocos de claims abaixo. Isso está declarado claim a claim.

## Claims

- **O Brasil tinha 24.213.445 empresas ativas (matrizes + filiais + MEI) ao fim do 2º quadrimestre de 2025, das quais 12.660.170 eram Microempreendedores Individuais e 3.252.308 Empresários Individuais.**
  - source: https://www.gov.br/empresas-e-negocios/pt-br/mapa-de-empresas/boletins/mapa-de-empresas-boletim-2o-quadrimestre-2025.pdf
  - publisher: MDIC — Mapa de Empresas (Governo Federal)
  - pub_date: 2025-09 (boletim do 2º quadrimestre de 2025)
  - accessed: 2026-08-19
  - confidence: média
  - class: size
  - segunda_fonte: https://fenacon.org.br/noticias/abertura-de-empresas-cresce-141-no-2o-quadrimestre-de-2025/ (FENACON, eco do mesmo boletim — confirma o agregado de 24,2 mi, NÃO é independente da fonte upstream)
  - ressalva: o PDF primário foi baixado mas não pôde ser convertido em texto nesta run; os números vêm do resumo do motor de busca sobre esse PDF, corroborados por dois ecos de entidades contábeis (FENACON, CRCSP). Tratar como "primário não verificado linha a linha" — reler o PDF antes de usar em decisão de investimento.

- **93,8% das empresas ativas no Brasil no 2º quadrimestre de 2025 são micro e pequenas empresas.**
  - source: https://www.gov.br/empresas-e-negocios/pt-br/mapa-de-empresas/boletins/mapa-de-empresas-boletim-2o-quadrimestre-2025.pdf
  - publisher: MDIC — Mapa de Empresas
  - pub_date: 2025-09
  - accessed: 2026-08-19
  - confidence: baixa
  - class: size
  - segunda_fonte: FONTE ÚNICA (percentual apareceu só no resumo do boletim; não localizei corte independente por porte fiscal ME/EPP com números absolutos)

- **O Brasil tinha aproximadamente 24 milhões de CNPJs ativos de pequenos negócios no último trimestre de 2025 — recorde histórico —, sendo que 97% das micro e pequenas empresas e 90% dos MEIs estavam efetivamente em operação.**
  - source: https://agenciasebrae.com.br/dados/brasil-tem-recorde-de-cnpj-ativos-de-pequenos-negocios/
  - publisher: Agência Sebrae de Notícias (Panorama Econômico dos Pequenos Negócios / Sebrae, com base na Receita Federal)
  - pub_date: 2026-03-18
  - accessed: 2026-08-19
  - confidence: alta (fonte lida integralmente; publisher é o produtor do dado; data-base 4T2025 = dentro da barra de frescor)
  - class: size
  - segunda_fonte: https://www.gov.br/empresas-e-negocios/pt-br/mapa-de-empresas/boletins/mapa-de-empresas-boletim-2o-quadrimestre-2025.pdf (MDIC, 24,2 mi de empresas ativas totais — ordem de grandeza compatível, mas ver contradição em Pistas)
  - implicação para D3: a taxa de operação real é o filtro que importa. ~10% dos MEIs registrados não operam; o denominador alcançável é o CNPJ que fatura, não o CNPJ que existe.

- **Havia 13,1 milhões de MEIs ativos no Brasil, concentrados em serviços (7,6 mi), comércio (3,1 mi) e indústria (1,3 mi); por região, Sudeste 6,8 mi, Sul 2,5 mi, Nordeste 2,1 mi; por UF, SP 3,7 mi, MG 1,5 mi, RJ 1,3 mi.**
  - source: https://agenciasebrae.com.br/dados/brasil-tem-recorde-de-cnpj-ativos-de-pequenos-negocios/
  - publisher: Agência Sebrae de Notícias / Panorama Econômico dos Pequenos Negócios (Sebrae, base Receita Federal)
  - pub_date: 2026-03-18
  - accessed: 2026-08-19
  - confidence: média
  - class: size
  - segunda_fonte: FONTE ÚNICA para o corte setorial e regional. O agregado de 13,1 mi conflita com os 12,66 mi de MEI do MDIC (2º quad/2025) — ver Pistas. A página lida confirmou os ~24 mi e a fonte, mas não devolveu os cortes setoriais numericamente; esses vieram do resumo de busca sobre a mesma página.

- **No 1º trimestre de 2026 foram abertas cerca de 1,54–1,64 milhão de novas empresas no Brasil (515.165 em janeiro, 481.171 em fevereiro, 543.202 em março), com São Paulo concentrando 8,75 milhões de empresas ativas, MG 2,98 mi e RJ 2,39 mi.**
  - source: https://www.empresaqui.com.br/blog/noticias/empresas-abertas-brasil-1-trimestre-2026/
  - publisher: EmpresAqui (agregador comercial, releitura do painel do Mapa de Empresas)
  - pub_date: 2026 (mês não datado na captura)
  - accessed: 2026-08-19
  - confidence: baixa
  - class: growth
  - segunda_fonte: FONTE ÚNICA — agregador. Os dois números de abertura no mesmo texto (1.638.996 e 1.539.538) não fecham entre si, o que é sinal de recorte metodológico frouxo. Substituir pelo painel oficial https://www.gov.br/empresas-e-negocios/pt-br/mapa-de-empresas/painel-mapa-de-empresas antes de usar.
  - implicação para D3: mesmo no piso, ~1,5 mi de CNPJs novos por trimestre é a esteira de aquisição mais barata que existe no Brasil — empresa recém-aberta ainda não tem sistema instalado, logo custo de troca zero.

- **[HISTÓRICO — 2019, fora da barra de frescor] 61% das PMEs brasileiras usavam Excel ou Google Planilhas para a contabilidade, 25% usavam software específico e 15% ainda usavam papel e caneta.**
  - source: https://www.capterra.com.br/blog/1108/contabilidade-online
  - publisher: Capterra Brasil (Gartner)
  - pub_date: 2019-11-27
  - accessed: 2026-08-19
  - confidence: baixa (idade: ~6,7 anos; a barra exige ≥2025-02)
  - class: size
  - segunda_fonte: alegação convergente de que "76% das PMEs não possuem nenhum sistema de gestão" circula em https://www.contabeis.com.br/noticias/65816/pmes-76-nao-possuem-nenhum-sistema-para-a-gestao-dos-negocios/ — NÃO LIDA nesta run, origem upstream não rastreada
  - metodologia (declarada): 298 profissionais, campo de 29/out a 13/nov, 83% comércio e serviços (1–99 funcionários), 17% indústria (1–499 funcionários). Amostra pequena e autosseleção de painel online.
  - uso permitido: como ordem de grandeza direcional de que a maioria da base opera em planilha. NÃO usar como número de 2026.

- **[HISTÓRICO — 2019] Disposição a pagar declarada por PMEs sem software contábil: 37% pagariam entre R$ 30 e R$ 50/mês e 21% entre R$ 50 e R$ 70/mês; 45% pretendiam investir em até 6 meses e 40% em até 12 meses.**
  - source: https://www.capterra.com.br/blog/1108/contabilidade-online
  - publisher: Capterra Brasil (Gartner)
  - pub_date: 2019-11-27
  - accessed: 2026-08-19
  - confidence: baixa
  - class: size
  - segunda_fonte: FONTE ÚNICA
  - implicação para D3 (a mais importante do digest): o ticket declarado da cauda longa de PME brasileira em 2019 estava na faixa de R$ 30–70/mês. Mesmo corrigindo por inflação acumulada, isso posiciona a faixa em algo como R$ 50–120/mês. Um micro-SaaS com R$ 1.000/mês de infra precisa de dezenas — não milhares — de assinantes para cobrir infra, mas de centenas a milhares para pagar dois desenvolvedores. Este é o número que decide o modelo de negócio e ele está desatualizado: revalidar é a maior prioridade de pesquisa remanescente.

- **A adoção de software de gestão entre PMEs cresce com o porte: 42% de adoção em empresas de 50–99 funcionários (comércio/serviços) e 45% em empresas de 250–499 funcionários (indústria), contra ~25% na média geral.**
  - source: https://www.capterra.com.br/blog/1108/contabilidade-online
  - publisher: Capterra Brasil (Gartner)
  - pub_date: 2019-11-27
  - accessed: 2026-08-19
  - confidence: baixa
  - class: size
  - segunda_fonte: FONTE ÚNICA
  - implicação: a variável que separa "adota software" de "não adota" é ter empregados, não ser CNPJ. MEI sem empregado é o segmento de menor adoção e menor ticket — maior volume, pior economia unitária.

- **Os gastos com ERP no Brasil deveriam alcançar US$ 4,9 bilhões em 2025 (+11% a/a), com quase 30% do mercado já em ERP SaaS; o mercado brasileiro de software, serviços e hardware deveria crescer 9,5% em 2025.**
  - source: https://tiinside.com.br/20/03/2025/mercado-brasileiro-de-software-deve-crescer-95-em-2025-aponta-estudo/
  - publisher: TI Inside, reportando o estudo "Mercado Brasileiro de Software — Panorama e Tendências 2025" da ABES
  - pub_date: 2025-03-20
  - accessed: 2026-08-19
  - confidence: baixa
  - class: size/growth
  - segunda_fonte: FONTE ÚNICA na prática. Os ecos em 4matt.com.br, fenati.org.br e terra.com.br reproduzem o MESMO estudo ABES — isso é um publisher upstream, não quatro fontes.
  - ressalva: a URL retornou HTTP 403 nesta run; os números vêm do resumo de busca. Além disso, trata-se de uma PROJEÇÃO para 2025 apresentada em março de 2025, não de um realizado — pelo cartão de qualidade, é hipótese, não achado. O realizado de 2025 já deveria estar publicado (edição 2026 do estudo ABES) e não foi recuperado.

## Pistas

**Contradição direta no número de MEIs.** MDIC/Mapa de Empresas registra 12.660.170 MEIs no 2º quadrimestre de 2025; Sebrae/Panorama (base Receita Federal, 4T2025) fala em 13,1 milhões de MEIs ativos. A diferença de ~440 mil pode ser puramente temporal (dois quadrimestres de defasagem, num ritmo de abertura recorde), mas também pode ser definicional — "ativo" no Mapa de Empresas = situação cadastral ativa na Junta/RFB, enquanto o Sebrae aplica um filtro de operação. Não resolvido nesta run. Antes de dimensionar SAM, fixar UMA definição e UMA data-base.

**Contradição no denominador "pequenos negócios".** Sebrae diz ~24 milhões de CNPJs ativos de *pequenos negócios*; MDIC diz 24,2 milhões de empresas *totais* (incluindo 205 mil S.A. e 92 mil outros tipos societários). Os dois números quase coincidem porque micro e pequenas são 93,8% do total — mas usá-los como se fossem a mesma coisa é erro. Se o produto exclui MEI, o universo cai de ~24 mi para ~11,5 mi; se exclui também empresas sem empregados, cai muito mais (magnitude não recuperada — ver Lacunas).

**A taxa de operação é o filtro decisivo e existe dado sobre ela.** 90% dos MEIs e 97% das MPEs em operação (Sebrae, 4T2025). Isso é raro e valioso: permite converter estoque cadastral em base endereçável com um haircut defensável, em vez de chutar.

**O contador como canal está implicitamente confirmado pela distribuição das fontes.** Os ecos do boletim do Mapa de Empresas com maior profundidade editorial vieram de FENACON (federação dos serviços contábeis) e CRCSP (conselho regional de contabilidade). A infraestrutura de informação da PME brasileira passa pelo contador. Não recuperei, porém, nenhum número sobre tamanho do mercado de serviços contábeis nem sobre quantos escritórios de contabilidade existem no Brasil — pergunta 4 do brief ficou meio respondida.

**Sinal contraditório sobre adoção que precisa ser resolvido.** Circulam três números incompatíveis: 25% usam software (Capterra 2019), 27% possuem sistemas integrados (atribuído a ABDI/Sebrae, Pesquisa de Maturidade Digital 2024), e 24% possuem alguma ferramenta (complemento dos "76% sem sistema"). Eles são suspeitosamente convergentes em ~25% — o que é encorajador — mas nenhum foi verificado na origem. A Pesquisa de Maturidade Digital ABDI/Sebrae 2024 (índice médio de digitalização 35 pontos numa escala 0–80) é a fonte primária mais promissora não lida.

**Pergunta aberta com peso de decisão:** o segmento com maior adoção declarada (50–499 funcionários) é exatamente o segmento que já tem ERP instalado, contador dedicado e ciclo de venda longo — incompatível com "3 meses até MVP e velocidade até cliente pagante". O segmento compatível com o perfil do fundador (MEI e ME sem empregados, ticket R$ 30–70) é o de pior economia unitária. D3 não resolve essa tensão sozinho; ela precisa ser cruzada com a dimensão de canal e CAC.

## Lacunas

Procurado e NÃO encontrado nesta run:

1. **Corte por porte fiscal com números absolutos (ME vs EPP vs demais).** O Mapa de Empresas publica natureza jurídica (MEI, EI, LTDA, S.A.), não porte fiscal. Só recuperei o percentual agregado 93,8% de MPE. Quantas são microempresas (até R$ 360 mil/ano) e quantas são EPP (até R$ 4,8 mi/ano) separadamente: não obtido. Fonte a atacar: Receita Federal / Portal do Simples Nacional (estatísticas de optantes por porte), que publica isso abertamente.

2. **Quantas empresas brasileiras têm empregados.** Esta é a variável de segmentação mais preditiva de adoção de software financeiro e eu não obtive o número. Fonte canônica: IBGE CEMPRE (Cadastro Central de Empresas) e RAIS/Novo CAGED. O CEMPRE tem defasagem de ~2 anos, então o dado mais recente provavelmente é de 2023–2024 — já seria "histórico" pela barra de frescor, mas é o melhor que existe.

3. **Ticket médio ATUAL (2025–2026) de software financeiro/ERP para PME brasileira.** Encontrei apenas a faixa declarada de 2019 (R$ 30–70/mês). Não recuperei tabela de preços praticada, ARPU reportado por player, nem pesquisa recente de disposição a pagar. Caminho mais barato para fechar esta lacuna: páginas públicas de preço de Conta Azul, Bling, Omie, Tiny e Contabilizei — preço de tabela é dado primário auto-reportado e gratuito, e três ou quatro deles dão uma faixa defensável em uma única rodada.

4. **Tamanho e crescimento do mercado de serviços contábeis para PME no Brasil.** Nada recuperado: nem receita agregada, nem número de escritórios, nem ticket médio de honorários. Fonte a atacar: CFC (Conselho Federal de Contabilidade) publica estatísticas de profissionais e organizações contábeis registradas; IBGE PAS (Pesquisa Anual de Serviços) tem a receita do setor por CNAE.

5. **Realizado de 2025 do mercado de software brasileiro.** Só recuperei a PROJEÇÃO feita em março de 2025. A edição 2026 do estudo ABES (que traria o realizado de 2025) não foi recuperada — e o site que a reportava bloqueou o acesso.

6. **Recorte de ERP/SaaS financeiro especificamente PME.** O número de US$ 4,9 bi é ERP Brasil inteiro, dominado por grandes contas e por Totvs/SAP/Oracle. A fatia PME desse bolo — que é o que importa para dimensionar um micro-SaaS — não foi encontrada em nenhuma fonte. Suspeito que não exista publicamente com metodologia aberta; a rota alternativa é bottom-up pelos números auto-reportados de base de clientes de Totvs, Omie, Conta Azul e Bling (relatórios de resultados da Totvs são públicos e trazem segmentação).

7. **Disposição a pagar por segmento (pergunta 5 do brief).** Só existe o corte por porte de 2019. Nenhum dado recente por setor (comércio × serviços × indústria) foi localizado. Provável que dado público fino sobre isso simplesmente não exista no Brasil — a rota realista é pesquisa primária do próprio fundador, não desk research.

**Achado de segunda ordem sobre a própria disponibilidade de dados:** o Brasil tem dado de CONTAGEM de empresas excelente, aberto, oficial e trimestral (Mapa de Empresas, Receita Federal, Sebrae). Tem dado de COMPORTAMENTO (o que a PME usa, o que paga, por que troca) muito pobre — o que circula é pesquisa de vendor com amostra pequena, sem metodologia publicada, e frequentemente de 2019. Qualquer dimensionamento aqui será sólido no denominador e frágil na taxa de conversão. Planejar a decisão sabendo que a fragilidade está do lado da monetização, não do lado do universo.
