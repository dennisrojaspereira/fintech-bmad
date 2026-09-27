# Checagem semântica de citações

Escopo: grupos de prioridade 1 a 4 completos, grupo 5 parcial. 9 URLs abertas com WebFetch em 2026-08-19. A checagem mecânica (resolução `[n]` ↔ apêndice) não foi repetida.

## Resultados

| ref | afirmação no relatório (resumida) | veredito | observação |
|---|---|---|---|
| [36] | Pluggy: mínimo mensal R$ 2.500 (Dados) e R$ 500 (Pagamentos); excedente por request; trial de 14 dias ao fim do qual as conexões pausam | **confere** | Literal na página: "A partir de R$ 2.500/mês", "A partir de R$ 500/mês", "Acima disso, o excedente é cobrado por requisição", "As conexões com contas reais de clientes pausam até você ativar um plano". A página vai além do relatório: diz explicitamente "Dados e Pagamentos são produtos separados, cada um com seu mínimo mensal (R$ 2.500 e R$ 500)" — ver Divergências. |
| [39] | Confirmação independente: Pluggy ~R$ 2.500/mês, Belvo ~R$ 6.000/mês, TecnoSpeed R$ 1.500 de adesão + R$ 540/mês | **confere** | Literal: "Pluggy: ~R$ 2.500/mês", "Belvo: ~R$ 6.000/mês", "Tecnospeed: R$ 1.500 de adesão + R$ 540/mês (o menor que encontrei até agora)". São cotações de pesquisa própria do autor, como o apêndice já rotula. Data exibida como "3 meses atrás", compatível com o carimbo ~2026-05. É relato de um desenvolvedor individual, não auditoria — a confiança "média-alta" do apêndice está calibrada. |
| [40] | Belvo plano Launch a USD 1.000/mês; sandbox grátis só para teste, não produção | **confere** | Literal: "1,000 USD/month" para o plano Launch; "Sandbox access is free and intended for testing and evaluation purposes only. Production access to serve real customers requires a paid plan." Três planos: Sandbox, Launch, Growth (custom). |
| [7] | Escopo de serviços do art. 5º, II; definição de ITP com "sem deter em momento algum os fundos transferidos" (art. 2º, VI); histórico de 12 meses (art. 5º, §5º, II) | **inacessível** | O PDF em `normativos.bcb.gov.br/.../Res_Conj_0001_v4_P.pdf` baixou (328,8 KB) mas o conteúdo não foi extraível — texto comprimido/não parseável. Nenhum dos três dispositivos pôde ser lido. Não é falha do relatório; é falha de acesso desta rodada. Nada foi verificado nem refutado. |
| [48] | "O Asaas já casa boleto pago por PIX via `txid` e dispara webhook, **sem taxa extra**" / "sem cobrança separada pela conciliação" | **impreciso** | As duas primeiras partes conferem literalmente: "o sistema relaciona a transação à cobrança original por meio de identificadores exclusivos, como o txid" e "Configure webhooks para receber a confirmação do Pix e relacioná-la automaticamente à cobrança original". A terceira **não consta**: a página não afirma ausência de cobrança pela conciliação, nem diferencia custo entre conciliação manual e automática. Publicação 2026-07-23, confirmada. |
| [49] | Conta Azul declara oficialmente que não concilia pagamentos feitos fora da plataforma; instrui cancelar boleto e importar OFX para casar na mão | **confere** | Literal: "A Conta Azul não concilia automaticamente pagamentos realizados fora da plataforma com cobranças geradas internamente." O procedimento tem três passos — cancelar a cobrança (Ações > Cancelar cobrança), importar extrato OFX (Financeiro > Conciliação > Importar extrato) e conciliar manualmente em "Conciliações pendentes". Atualização 2026-04-14, confirmada. É o achado mais bem sustentado do relatório. |
| [45] | Conta Azul publica desconto de 20% a 40%, não 85%; 6 níveis; licença R$ 199,90 a R$ 99,90; adesão gratuita | **confere** | Faixa de desconto por recomendação de 20% (Bronze) a 40% (Diamante). Seis níveis: Aspirante, Bronze, Prata, Ouro, Platina, Diamante. Licença de R$ 199,90 (Aspirante/Bronze) a R$ 99,90 (Diamante). "O Programa de Parceria Conta Azul é totalmente gratuito." Nenhuma menção a 85% — a derrubada feita pelo relatório está correta. |
| [42] | Nibo: 5 níveis, desconto 30–50%, comissão quadrimestral, adesão gratuita | **confere** | Cinco níveis por pontuação: Bronze 30%, Prata 40%, Ouro 50%, Platina 50%, Diamante 50%. "O pagamento das comissões será realizado a cada quatro meses, a pedido do parceiro." Adesão gratuita confirmada. Duas qualificações que o relatório não carrega: o teto de 50% já é atingido no terceiro nível (Ouro), e a comissão é paga "a pedido do parceiro", não automaticamente. Nenhuma das duas altera conclusão. |
| [47] | Asaas: sem mensalidade; PIX/boleto R$ 0,99 nos 3 primeiros meses e R$ 1,99 em regime; NF-e R$ 0,49 | **confere** | Literal: "No Asaas, não há mensalidade ou taxa de adesão"; "R$ 1,99 R$ 0,99 por transação recebida (Válido por 3 meses)"; "R$ 0,49 por nota emitida". A página ressalva que "As taxas apresentadas são padrão" e podem variar por contrato — o relatório não carrega essa ressalva no Asaas, embora a carregue na Efí [37]. |

## Divergências que exigem ação

**1. [48] — "sem taxa extra" / "sem cobrança separada pela conciliação" não está na fonte.**
Onde aparece: Golpe 1 do red team ("sem cobrança separada pela conciliação"), linha do apêndice ("sem taxa extra"), e por herança a linha de corte do candidato de conciliação boleto×PIX.
A fonte sustenta o mecanismo (`txid` + webhook), mas é silente sobre custo da conciliação. Correção mínima: remover a cláusula de custo, deixando "o Asaas já casa boleto pago por PIX via `txid` e dispara webhook [48]". Se a ausência de taxa for material para o argumento, ela precisa de outra fonte — a página de tarifas [47] lista tarifa por transação recebida e não menciona cobrança de conciliação, o que é evidência de ausência, não afirmação de gratuidade.
Impacto na conclusão: baixo. O Golpe 1 continua de pé pelo mecanismo, que é o que importa — o produto vira wrapper de webhook independentemente de haver taxa.

**2. [36] — a tabela D7 subestima a própria fonte.**
A linha "Pluggy Pagamentos | a partir de R$ 500/mês | Sim, não confirmado" está desatualizada em relação ao que a página diz. A fonte é explícita: "Dados e Pagamentos são produtos separados, cada um com seu mínimo mensal (R$ 2.500 e R$ 500)". O mínimo de Pagamentos está confirmado pela fonte primária do fornecedor, não pendente. Correção: trocar "Sim, não confirmado" por "Sim".
Impacto: nenhum sobre os cortes por G3 (que dependem do mínimo de Dados), mas fecha uma ressalva desnecessária.

**3. [47] — falta a ressalva de variação por contrato.**
O relatório carrega, corretamente, a ressalva "a própria página ressalva variação por negociação" na linha da Efí [37], mas não na do Asaas, cuja página traz ressalva equivalente ("As taxas apresentadas são padrão. Para conferir as condições aplicadas ao seu contrato, consulte-as diretamente na sua conta Asaas"). Correção: espelhar a ressalva na linha do Asaas em D7 e/ou na coluna de observação do apêndice.
Impacto: cosmético, mas é assimetria de tratamento entre dois fornecedores comparados lado a lado.

**4. [42] — duas qualificações perdidas, ambas menores.**
O texto "Nibo publica 30% a 50%" está correto como faixa, mas omite que 50% é atingido já no terceiro dos cinco níveis (Ouro) e se repete em Platina e Diamante — o que enfraquece o argumento de "distribuição de cauda longa rasa" derivado da estrutura de níveis no bloco D6-V. E a comissão quadrimestral é paga "a pedido do parceiro", não automaticamente. Nenhuma correção é obrigatória; registre se o argumento de estrutura de níveis for reaproveitado.

## Não checados

| ref | por quê |
|---|---|
| [7] | Tentado e **inacessível** — PDF do BCB baixado mas não extraível. As três âncoras normativas (art. 5º II, art. 2º VI, art. 5º §5º II) permanecem sem verificação semântica independente. Isto se soma ao alerta que o próprio relatório já faz no Mapa de obsolescência (claim regulatório vencido, versão v4 não cruzada com o normativo vigente). Recomendação de checagem: abrir a versão HTML no site do BCB, não o PDF. |
| [46] | Orçamento de chamadas esgotado. O claim disputado dos "mais de 10 mil parceiros ativos" da Conta Azul segue sem confirmação semântica. |
| [37] | Orçamento esgotado. Tarifas da Efí (QR dinâmico 1,19%; boleto R$ 3,45 no recebimento; emissão e não pagos grátis; sem mensalidade) não verificadas. Note que a conta de "R$ 84.033 de volume" e "289 boletos" em D7 depende inteiramente destes números não checados. |
| [43], [44], [56] | Fora da lista de prioridades desta rodada (programas Omie, Asaas e GestãoClick). |
| [52], [53], [54] | Fora da lista de prioridades. O próprio relatório já rebaixa a confiança desse conjunto para média-alta por falta de extração do PDF oficial. |
| demais 40 refs | Fora do escopo priorizado. |
