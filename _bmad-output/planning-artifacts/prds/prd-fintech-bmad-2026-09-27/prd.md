---
title: Fintech MVP — Plataforma de Conciliação Automática para PMEs
status: draft
created: 2026-09-27
updated: 2026-09-27
audience: |
  Equipe de desenvolvimento, arquiteto, stakeholders técnicos internos (educacional)
---

# Fintech MVP — Plataforma de Conciliação Automática para PMEs

## Visão

**Problema:** Empresas de pequeno e médio porte (PMEs) no Brasil perdem horas reconciliando manualmente pagamentos recebidos (boleto, PIX, cartão) com contas a receber — especialmente quando há descasamento entre o meio de cobrança (ex: boleto emitido) e o meio de liquidação (ex: PIX recebido). Plataformas existentes (Conta Azul, Omie, Asaas) terceirizam a conectividade mas falham na lógica de matching, deixando ERPs e PSPs vulneráveis.

**Solução:** Uma plataforma leve que:
1. **Conecta** automaticamente ao banco do usuário via Open Finance (Pluggy) — sem quebra de senha
2. **Captura** eventos de pagamento (PIX, TED, cartão, boleto) via webhooks
3. **Reconcilia** automaticamente contra notas fiscais e documentos a receber
4. **Expõe** interface simples (web + API REST) para visualizar conflitos e resolver manually quando necessário

**Escopo MVP:** Educacional e viável em 8-12 semanas. Foco: conciliação de **PIX + boleto** com suporte a **1 banco + 1 PSP**. Sem multi-tenant, sem mobile, sem relatórios complexos. Prototipo pra validar valor e integrações.

---

## Usuários e Jornada

### Persona: Marco (Gestor Financeiro de PME)

Marco administra fluxo de caixa em uma consultoria (50 funcionários). Recebe pagamentos por **boleto (emitido no ERP), PIX (transferência direta)** e cartão (máquina). Hoje gasta **2-3h/dia** olhando extratos bancários no app do banco, cruzando com notas fiscais em planilha do Excel, anotando qual pagamento bate com qual cobrança.

**Jornada atual:**
1. Acordar; abrir app do banco
2. Conferir "extrato do dia" (PIX, TED, boleto liquidado)
3. Voltar pro ERP; encontrar NF correspondente
4. Anotar em planilha (ou deixar pra depois)
5. Gerar relatório manual de reconciliação (erro-prone, atrasado)

**Jornada desejada:**
1. Acordar; abrir dashboard da plataforma
2. Ver "R$ 25k reconciliados automaticamente hoje"
3. Ver 3 transações com conflito (ex: valor diferente, NF não encontrada)
4. Clicar em uma → ver opções ("vincular a outra NF", "marcar como adiantamento", "ignorar")
5. Pronto; dados prontos pro contador/ERP

---

## Features Essenciais (MVP)

### F1: Onboarding Simplificado
- Usuário faz signup com email
- **FR1a:** Sistema guia login via Pluggy → escolhe banco + autoriza Open Finance (read-only, sem movimentação de fundos)
- **FR1b:** Configura tipo(s) de documento a receber (NF-e pelo e-mail, upload manual via CSV, API)
- **FR1c:** Escolhe 1 PSP para receber webhooks de pagamento (MVP: Asaas ou Cielo)
- **Critério:** Onboarding completo em < 5 cliques; usuário conectado em < 3 minutos

### F2: Ingestão de Eventos de Pagamento
- **FR2a:** Webhook receiver escuta eventos de PSP (Asaas: `payment.received`, `payment.refunded`)
- **FR2b:** Normaliza pra formato interno: `{ amount, date, type, reference_id, payer_name }`
- **FR2c:** Armazena em fila/banco de dados; valida assinatura do webhook
- **Critério:** 0 pagamentos perdidos; < 30s latência de recebimento a armazenamento

### F3: Sincronização de Extrato Bancário (Open Finance)
- **FR3a:** Daemon executa a cada 6h (ou on-demand) → chama Pluggy API → puxa transações dos últimos 7 dias
- **FR3b:** Normaliza transações: `{ amount, date, description, bank_code, reference }`
- **FR3c:** Detecta duplicatas (mesmo hash com window de ±1h)
- **Critério:** Extrato sincronizado em < 60s; 99%+ de precisão contra app do banco

### F4: Matching Automático (Reconciliação)
- **FR4a:** Algoritmo: dado um pagamento recebido, busca NF com:
  - Valor = pagamento (exato ou 99-101% pra tolerância de taxa)
  - Cliente = payer_name (fuzzy match)
  - Data emissão ≤ data pagamento
  - Status = aberta/pendente (não quitada)
- **FR4b:** Se achado: marca como "reconciliado" no banco de dados
- **FR4c:** Se não achado: coloca em queue de "conflitos" pro usuário
- **FR4d:** Suporta múltiplos pagamentos → 1 NF (adiantamentos), 1 pagamento → múltiplas NFs (split)
- **Critério:** 85%+ taxa de matching automático em testes de aceitação

### F5: Dashboard de Visualização
- **FR5a:** Tela principal mostra:
  - Hoje: "R$ XX reconciliados" + "Y conflitos"
  - Lista últimas 50 transações: Status (OK, Conflito), Valor, Data, Cliente, Ação
  - Resumo por tipo (PIX, boleto, cartão)
- **FR5b:** Tela de conflitos: lista, detalhe, ações (vincular a NF diferente, ignorar, marcar adiantamento)
- **FR5c:** Sem autenticação social; usuário/senha simples (educacional)
- **Critério:** < 2s load time; usável em desktop + tablet

### F6: API REST de Leitura
- **FR6a:** `GET /v1/reconciliations` → lista reconciliações com filtros (date_from, date_to, status)
- **FR6b:** `GET /v1/conflicts` → lista conflitos
- **FR6c:** `POST /v1/conflicts/{id}/resolve` → resolve manualmente (vincular, ignorar, split)
- **FR6d:** `GET /v1/summary` → resumo do dia/mês
- **Critério:** Rate limit 1000 req/min; auth via API key simples

---

## Requisitos Não-Funcionais

### Segurança & Conformidade
- **RNF1:** Chaves de acesso ao Open Finance (Pluggy) armazenadas em env vars/secrets, nunca em logs
- **RNF2:** Senha do usuário hasheada (bcrypt), conexão HTTPS sempre
- **RNF3:** Webhooks de PSP validados via HMAC SHA256 (assinatura)
- **RNF4:** Sem armazenamento de senha bancária (sempre via Pluggy)
- **RNF5:** Conformidade mínima LGPD: direito de acesso/exclusão de dados, privacidade policy

### Performance
- **RNF6:** Dashboard carrega em < 2s (p95)
- **RNF7:** Webhook processing < 1s (p95)
- **RNF8:** Matching automático roda em < 5s por 1000 transações

### Disponibilidade
- **RNF9:** 99.5% uptime (educacional; não SLA comercial)
- **RNF10:** Retry automático em falhas transitórias (ex: timeout de Pluggy)

### Escalabilidade (futuro, fora do MVP)
- **RNF11:** Arquitetura preparada pra multi-tenant (não implementado)
- **RNF12:** Banco de dados com particionamento por período (futuro)

---

## Integrações Externas

| Sistema | Tipo | MVP | Nota |
|---------|------|-----|------|
| **Pluggy** | Data Connector | SIM | Open Finance; ~80% dos bancos BR |
| **Asaas** | PSP Webhook | SIM | PIX + boleto; webhook nativo |
| **Cielo** | PSP Webhook | NÃO | Cartão; pode vir em v1.1 |
| **Stripe** | PSP API | NÃO | Internacional; pós-MVP |
| **E-mail** | Documento | SIM | Usuario faz upload de NF-e |
| **ERP (Omie/Conta Azul)** | Sync | NÃO | Futuro; pra agora é manual |

---

## Métricas de Sucesso (MVP)

| Métrica | Baseline | Meta | Janela |
|---------|----------|------|--------|
| **Matching Rate** | 0% (manual hoje) | ≥ 85% | Testes E2E |
| **Time to Reconcile** | 120-180 min/dia (manual) | < 10 min/dia | Feedback usuario |
| **Dashboard Adoption** | N/A | 1 usuario real testando | 2 semanas |
| **API Latency (p95)** | N/A | < 500ms | Prod monitoring |
| **Webhook Delivery** | N/A | 99.9% (sem perda) | Prod logs |
| **Uptime** | N/A | ≥ 99.5% | Prod monitoring |

---

## Constraints & Riscos

### Constraints
- **C1:** MVP usa Pluggy + Asaas; se qualquer um cair, plataforma não funciona
- **C2:** Matching baseado em fuzzy string é frágil com nomes de cliente muito variáveis
- **C3:** Sem suporte a PIX automático recorrente (Pluggy não expõe chave PIX pro remetente)
- **C4:** Sem mobile neste MVP

### Riscos
- **R1 (TECH):** Pluggy pode ter downtime ou latência; mitigar: retry + fallback (marcar manual)
- **R2 (TECH):** Asaas webhook pode falhar; mitigar: polling de backup a cada 6h
- **R3 (MARKET):** PMEs podem não confiar em terceiro novo; mitigar: educação + prototipo gratuito
- **R4 (LEGAL):** Pluggy/Asaas podem mudar termos; mitigar: contrato revisor legal antes de launch

---

## Roadmap (Fora do MVP)

- **v1.1 (Q4 2026):** Suporte a cartão (Cielo); integrações com 3+ bancos
- **v2.0 (Q1 2027):** Multi-tenant; dashboard de admin; relatórios exportáveis
- **v2.5 (Q2 2027):** Sync com ERP (Omie, Conta Azul); mobile app

---

## Open Questions
- [ ] Qual é a estrutura legal? (Empresa, CNPJ, termos de serviço)
- [ ] Onde vai ficar hosted? (AWS, Heroku, on-prem educacional)
- [ ] Quanto de histórico bancário puxar na primeira sincronização? (7d vs 30d vs 90d)
- [ ] Telefone de suporte ou só chat/email?
