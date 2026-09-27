# RT — Red team da recomendação de conciliação de recebimentos

## Veredito

**NÃO SOBREVIVE na forma proposta** — o caso-bandeira ("cobrança sai por boleto e o cliente paga por PIX") já é resolvido nativamente, de graça e via `txid` dentro do próprio PSP (Asaas, Iugu, Cora), e o resíduo de dor que sobra é exatamente o que a arquitetura escolhida ("só API do PSP, sem Open Finance") não consegue enxergar.

## Evidência desconfirmadora encontrada

**1. O PSP já concilia o caso-bandeira, automaticamente e sem taxa extra.**
- Afirmação: no boleto com QR Code Pix do Asaas, "o sistema relaciona a transação à cobrança original por meio de identificadores exclusivos, como o txid"; webhooks confirmam Pix e boleto separadamente "mas vincule ambos à mesma obrigação financeira". Não há cobrança separada pela conciliação — o preço citado é apenas por transação recebida (R$ 0,99 nos 3 primeiros meses, depois R$ 1,99).
- source: https://blog.asaas.com/boleto-com-qr-code/
- publisher: Asaas (PSP — conteúdo do próprio fornecedor)
- pub_date: 2026-07-23 · accessed: 2026-08-19 · confidence: **alta**
- Ataca: o núcleo da proposta de valor ("casar cobrança emitida com liquidação recebida, incluindo boleto pago por PIX"). Se o PSP em que você pretende construir já entrega isso embutido, o produto vira um wrapper de um webhook.

**2. O mecanismo do próprio arranjo PIX foi desenhado para conciliar — não é lacuna de mercado, é campo de payload.**
- Afirmação: o `txid` (mín. 26 / máx. 35 caracteres no QR dinâmico; até 25 no estático) é referenciado na pacs.008 como `TransactionIdentification <TxId>` / `idConciliacaoRecebedor`, e "o objetivo desse campo é ser um elemento que possibilite ao Banco apresentar ao usuário recebedor a funcionalidade de conciliação de pagamentos (possibilitando associar a transação Pix à cobrança correlata)". Além disso, cada transação tem `EndToEndId` único, presente tanto no extrato quanto no sistema do PSP.
- source: resultados convergentes de https://blog.tecnospeed.com.br/cobranca-pix-pago/ , https://www.bradata.com.br/blog/pix-integrado-erp-cobranca-conciliacao e https://github.com/bacen/pix-api/issues/77 (repositório oficial do BCB)
- publisher: Tecnospeed / Bradata / BACEN (pix-api)
- pub_date: n/d · accessed: 2026-08-19 · confidence: **média-alta** (ver ressalva de verificação abaixo)
- Ataca: a premissa de que o casamento é um problema de mercado. O identificador de conciliação é obrigação de desenho do arranjo, entregue ao banco recebedor. A dor residual é de *implementação do integrador*, não de ausência de infraestrutura — e dor de má implementação alheia é péssima base para um SaaS, porque some quando o integrador arruma.

**3. O caso que sobra é justamente o que a API do PSP não vê.**
- Afirmação: o Conta Azul instrui o usuário a **cancelar o boleto e importar o extrato em OFX** para casar manualmente o Pix recebido com a venda, e declara explicitamente: *"A Conta Azul não concilia automaticamente pagamentos realizados fora da plataforma."*
- source: https://ajuda.contaazul.com/hc/pt-br/articles/43775485946253-Conciliação-como-automatizar-conciliação-de-pagamentos-Pix-de-faturas-geradas-como-boleto
- publisher: Conta Azul (documentação oficial de suporte)
- pub_date/atualização: 2026-04-14 · accessed: 2026-08-19 · confidence: **alta**
- Ataca: a **arquitetura**, que é a parte mais frágil da conclusão. O único pedaço da dor que continua aberto é o pagamento feito *fora* da cobrança (PIX direto na chave, valor parcial, valor divergente). Esse evento, por definição, não tem `txid` da cobrança e frequentemente nem passa pelo PSP emissor — ele aparece no **extrato bancário**. Ou seja: os casos que a API do PSP resolve não precisam do seu produto, e os casos que precisam do seu produto exigem dado de extrato (OFX/Open Finance) — exatamente o que a conclusão excluiu por custo. A tese se autocontradiz.

**4. O canal contábil existe, mas o slot já está ocupado por ERP integrado.**
- Afirmação: programas de parceria para contadores são estruturados em torno de **revenda de ERP** ("aumente sua renda com comissões sobre a venda de soluções empresariais, como um sistema ERP"), e a conciliação bancária automática aparece como *módulo dentro* desse ERP, não como produto avulso. O Conta Azul é posicionado como plataforma para micro e pequenas empresas com "conciliação bancária automática... e integração fácil com o contador".
- source: https://parceiro.gestaoclick.com.br/programa-parceria-contadores/ e https://parceiro.gestaoclick.com.br/contadores-adotam-softwares-gestao-clientes/
- publisher: GestãoClick (página oficial de programa de parceiros)
- pub_date: n/d · accessed: 2026-08-19 · confidence: **média**
- Ataca: a estratégia de distribuição. O contador monetiza revendendo *um* sistema que resolve NF, financeiro e conciliação. Uma ferramenta que faz só conciliação disputa o mesmo slot de atenção e comissão com uma fração do valor por cliente — e, se não for o ERP, vira mais um login e mais uma exportação no fluxo dele.

**5. O espaço não está vazio nem barato — está em consolidação com capital.**
- Afirmação: a Kamino levantou R$ 54 milhões (co-liderado por Flourish Ventures e Quona Capital), **adquiriu a Nimbly**, e integra software de gestão, conta própria, cartão corporativo, conexões com bancos e **conciliação automática de extratos**. Equals ("conciliação de vendas automática"), FinBits, Barte e Kobana ocupam faixas adjacentes.
- source: https://startups.com.br/negocios/fintech/como-a-kamino-quer-se-destacar-em-gestao-financeira-para-pmes/ e https://finsidersbrasil.com.br/negocios-em-fintechs/fintechs-de-gestao-financeira-para-pmes-recebem-novos-investimentos/
- publisher: Startups.com.br / Finsiders Brasil
- pub_date: n/d · accessed: 2026-08-19 · confidence: **média**
- Ataca: a premissa implícita de janela aberta. Aquisição (Nimbly) e rodada indicam consolidação, não descoberta — e concorrentes capitalizados podem oferecer conciliação como isca gratuita dentro de um bundle, a pior configuração competitiva possível para um produto de feature única com 2 devs.

**6. Iugu e Cora já empacotam o híbrido boleto+Pix como produto.**
- Afirmação: a Iugu oferece "boleto, Pix, cartão e **Bolix**" com gestão automatizada de recebíveis e "toda a conciliação financeira da empresa através de relatórios e extratos completos". A Cora anuncia **"Boleto com QR Code Pix gratuito"** e "Gestão de Cobranças Completa, Gratuita e Descomplicada", com acompanhamento de recebimentos em tempo real.
- source: https://www.iugu.com/iugu-cobranca e https://www.cora.com.br/conta-pj/gestao-de-cobrancas/
- publisher: Iugu / Cora (páginas oficiais de produto)
- pub_date: n/d (Cora: nota comparativa atualizada 2025-04-07) · accessed: 2026-08-19 · confidence: **média-alta**
- Ataca: a diferenciação. O instrumento "boleto que aceita Pix" (Bolix / boleto com QR Code) é commodity gratuita entre PSPs — quando a cobrança e o pagamento nascem no mesmo instrumento, não existe divergência para conciliar.
- Ressalva de honestidade: a página da Cora **não afirma explicitamente** baixa automática; ela promete acompanhamento em tempo real. Esse ponto é mais fraco do que o do Asaas.

## O argumento mais forte de que a conclusão está errada

A conclusão confunde **um bug de implementação com um mercado**.

O arranjo PIX foi projetado com um campo cuja finalidade declarada é permitir ao recebedor associar a transação à cobrança correlata (`txid` / `idConciliacaoRecebedor`), mais um identificador único fim-a-fim (`EndToEndId`) presente simultaneamente no extrato e no sistema do PSP. Sobre esse trilho, os PSPs brasileiros construíram e **deram de graça** o produto que a conclusão propõe vender: o Asaas casa boleto pago por Pix via `txid` e dispara webhook, a Iugu empacota o híbrido como "Bolix", a Cora oferece boleto com QR Code Pix sem custo. Não sobra wedge — sobra um webhook.

E aí vem a contradição fatal. O único bolsão de dor genuinamente aberto que esta pesquisa encontrou é o **pagamento feito fora da cobrança emitida** — o cliente que ignora o boleto e manda Pix na chave, com valor parcial ou divergente. É por isso que o Conta Azul, incumbente de ERP com base instalada, documenta esse fluxo como "cancele o boleto, importe o OFX, case na mão" e afirma que não concilia pagamentos feitos fora da plataforma. Mas esse evento não tem `txid` da cobrança e pode nem tocar o PSP emissor: ele só existe no **extrato bancário**. Logo, a única versão do produto que teria razão de existir é precisamente aquela que exige agregação de extrato (OFX ou Open Finance) — o item que a conclusão eliminou como "caro demais". A arquitetura escolhida ("só a API do PSP que o cliente já usa") garante cegueira exatamente nos casos que justificariam o produto, e visão perfeita exatamente nos casos que o PSP já resolveu sozinho.

Some a isso o canal: o contador revende **ERP**, porque é isso que paga comissão e reduz retrabalho dele; uma ferramenta de conciliação avulsa é mais um login para o escritório e comissão menor, disputando o mesmo slot que GestãoClick e Conta Azul já ocupam. E some o campo competitivo: Kamino com R$ 54 milhões, aquisição da Nimbly e conciliação automática de extratos embutida, mais Equals, FinBits, Barte e Kobana — todos com incentivo para oferecer conciliação como isca gratuita de um bundle maior.

O resultado é o pior formato possível para 2 devs, 3 meses e R$ 1.000/mês: uma feature gratuita de terceiros, vendida por um canal que prefere o concorrente empacotado, num mercado onde a versão que funciona custa o dado que você decidiu não comprar.

## O que procurei e NÃO encontrei

- **Não encontrei** nenhuma startup brasileira de conciliação para PME documentada como morta, encerrada ou pivotada por falta de mercado. Busquei explicitamente por encerramento/pivot/aquisição nesse espaço e o retorno foi o oposto: financiamento (Kamino, R$ 54M) e consolidação por aquisição (Nimbly). **Ausência de evidência de fracasso é um achado real** — mas leia com cuidado: o padrão observado não é "ninguém sobrevive", é "conciliação vira módulo de plataforma maior", forma diferente e igualmente ruim de derrubar a tese de produto autônomo.
- **Não consegui verificar o texto do Manual de Padrões para Iniciação do Pix (BCB) na fonte primária.** O PDF oficial (`II_ManualdePadroesparaIniciacaodoPix.pdf`, ~3MB) foi baixado, mas o conteúdo não é extraível como texto pelo meu leitor. A afirmação sobre a finalidade conciliatória do `txid` fica apoiada em fontes secundárias convergentes (Tecnospeed, Bradata, issue do repositório oficial bacen/pix-api) — confidence média-alta, não alta. **Ação antes de decidir: abrir o manual manualmente e localizar `txid` / `idConciliacaoRecebedor`.**
- **Não encontrei** documentação de Efí, Pagar.me, InfinitePay ou Stone sobre baixa automática de cobrança; a busca por Efí especificamente não retornou material sobre conciliação de contas a receber. A generalização "todo PSP já concilia" está comprovada para Asaas (forte), Iugu e Cora (média-alta) e **não verificada** para os demais.
- **Não encontrei** nenhum escritório contábil ou BPO financeiro brasileiro que revenda ferramenta de conciliação **de terceiro, avulsa**. Todos os programas de parceria localizados são de revenda de ERP. Isso não prova que o canal rejeitaria — prova que não há precedente localizável do modelo proposto.
- **Não encontrei** dados de disposição a pagar, ticket médio ou tamanho de mercado para conciliação de recebimentos PME no Brasil. A conclusão não tem, nesta rodada, nenhuma sustentação quantitativa de demanda.

## Se não é essa, qual área seria

**Não há base, nesta pesquisa, para eleger com confiança outra das oito áreas.** Não busquei evidência primária sobre contas a pagar, automação financeira, verticais de nicho ou Open Finance, e apontar uma delas agora seria memória de treinamento disfarçada de achado — exatamente o que as regras proíbem.

O que a evidência **sim** sustenta é uma redireção dentro do próprio problema, e ela é desconfortável para o orçamento:

1. **O alvo real é "pagamento fora da cobrança", não "conciliação de cobrança".** É o único bolsão que um incumbente de ERP documenta como manual e declara não resolver (Conta Azul, 2026-04-14). Mas resolvê-lo exige dado de extrato — OFX importado ou Open Finance. **Isso inverte a premissa arquitetural da conclusão**; o caminho barato de validar é OFX/extrato automático (a Cora, por exemplo, entrega extrato automático agendado em CSV/PDF/OFX de graça) antes de pagar por agregação.
2. **Qualquer que seja a área, o teste de sobrevivência agora é: "o PSP ou o ERP entrega isso de graça no bundle?"** Foi esse teste que a recomendação de conciliação reprovou. Aplique-o *antes* de escolher a próxima área, não depois.
3. **Próximas verificações, em ordem de valor:** (a) abrir o Manual de Padrões do Pix e confirmar o texto do `txid`; (b) ler a documentação de API de Efí, Pagar.me e InfinitePay procurando baixa automática e webhook de liquidação; (c) entrevistar 5 escritórios de BPO financeiro sobre o fluxo "cliente pagou Pix na chave em vez do boleto" — quanto tempo custa hoje e quem paga por isso.
