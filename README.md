# fintech-bmad

Projeto fintech greenfield conduzido pelo **BMAD Method v6.11.0** (Breakthrough Method of
AI-driven Development), instalado para uso com Claude Code.

O stack ainda não foi definido de propósito: a decisão de produto e de arquitetura é feita
pelos próprios agentes do BMAD, no fluxo `analyst → PM → architect → SM → dev`.

## Como começar

Abra este diretório no Claude Code. Os 49 agentes e workflows do BMAD estão expostos como
skills (`/bmad-*`). Se estiver em dúvida por onde começar:

```bash
claude
```

e invoque `/bmad-help` — ele lê o estado do projeto e recomenda o próximo passo.

### Fluxo típico de greenfield

| Etapa | Skill | Entrega |
|---|---|---|
| 1. Descoberta | `/bmad-brainstorming`, `/bmad-market-research` | exploração do domínio |
| 2. Brief | `/bmad-product-brief` | brief do produto |
| 3. Produto | `/bmad-create-prd` → `/bmad-validate-prd` | PRD |
| 4. UX | `/bmad-ux` | fluxos e telas |
| 5. Arquitetura | `/bmad-create-architecture` | documento de arquitetura |
| 6. Backlog | `/bmad-create-epics-and-stories` | épicos e histórias |
| 7. Sprint | `/bmad-sprint-planning`, `/bmad-sprint-status` | planejamento e acompanhamento |
| 8. Implementação | `/bmad-dev-story`, `/bmad-quick-dev` | código + testes |
| 9. Revisão | `/bmad-code-review`, `/bmad-retrospective` | qualidade e aprendizado |

Personas em modo conversa: `/bmad-agent-analyst`, `/bmad-agent-pm`, `/bmad-agent-architect`,
`/bmad-agent-ux-designer`, `/bmad-agent-dev`.

## Estrutura

```
_bmad/                            # framework instalado (core + módulo bmm, config.toml)
.claude/skills/                   # 49 skills BMAD expostas ao Claude Code
_bmad-output/
  planning-artifacts/             # brief, PRD, UX, arquitetura, épicos
  implementation-artifacts/       # sprint status, histórias, reviews, retrospectivas
docs/                             # conhecimento de longo prazo do projeto
```

## Configuração

Definida em `_bmad/config.toml` e `_bmad/config.user.toml`:

- idioma de conversa e de documentos: **Português (Brasil)**
- pasta de saída: `_bmad-output`

## Manutenção

```bash
npx bmad-method status
```

```bash
npx bmad-method install --action update
```

> `uv` não está instalado nesta máquina. Só as skills `bmad-build` e `bmad-build-auto`
> dependem dele (https://docs.astral.sh/uv/); o restante do fluxo funciona sem.
