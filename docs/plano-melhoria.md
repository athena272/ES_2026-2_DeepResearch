# Plano de melhoria de processo (2 ações prioritárias)

**Cenário-alvo:** elevar práticas do projeto no sentido de uma **maturidade inicial organizada**, análoga ao que se espera ao buscar **MPS.BR nível G** (processos básicos definidos e compreendidos pela organização, com foco em **gestão de requisitos, projetos e qualidade** de forma enxuta).

As ações abaixo derivam dos **gaps** observados na auditoria: ausência de `CONTRIBUTING.md`, ausência de CI de testes/análise estática no repositório, validação principalmente por benchmarks externos, e dependência forte de APIs de terceiros.

---

## Ação 1 — Institucionalizar contribuição e critérios de aceite

| Campo | Conteúdo |
|-------|----------|
| **Problema observado** | Não há guia único `CONTRIBUTING.md`; contribuições dependem de conhecimento implícito e de discussões em issues. |
| **Risco atual** | Variabilidade nas mudanças, dificuldade de onboarding, fragilidade em auditorias de qualidade (PPQA / GQA). |
| **Ação proposta** | Adicionar `CONTRIBUTING.md` com: como abrir issues (template), formato mínimo de PR, checklist (teste manual descrito, impacto em `.env.example`, atualização de README se comportamento mudar). Opcional: issue templates em `.github/ISSUE_TEMPLATE/`. |
| **Esforço estimado** | Baixo a médio (1–3 dias de equipe, iterando com mantenedores). |
| **Impacto esperado** | Maior **previsibilidade** e **rastreabilidade** entre requisito (issue) e entrega (PR); alinha-se a **REQM** e **PPQA** (critérios objetivos de aceite). |
| **CMMI / MPS.BR** | **REQM** (explicitar como mudanças são propostas e aceitas); **PPQA** (critérios de avaliação de artefatos); **GQA** (garantir que práticas acordadas sejam seguidas). |

### Texto para o relatório

> Como primeira ação prioritária recomenda-se a formalização de um guia de contribuição (`CONTRIBUTING.md`) e, quando possível, templates de issue/pull request. Isso estabelece acordo explícito sobre como requisitos e correções entram no repositório, melhorando a rastreabilidade entre relatos de usuários e integrações de código — requisito central em gerência de requisitos e em processos de garantia da qualidade em níveis iniciais de maturidade.

---

## Ação 2 — Introduzir verificação automatizada mínima (CI + testes de fumaça)

| Campo | Conteúdo |
|-------|----------|
| **Problema observado** | Não há suíte de testes automatizada evidente no núcleo `inference/`; a aba Actions no GitHub não mostra workflows de teste ou lint — apenas *pages build*. |
| **Risco atual** | Regressões silenciosas em `react_agent.py` ou nas tools; dependência de validação apenas por execução manual ou benchmarks pesados. |
| **Ação proposta** | Criar workflow GitHub Actions que: (1) instale dependências a partir de `requirements.txt` (ou subset); (2) execute **lint** opcional (ex.: `ruff`) e **testes de fumaça** mínimos (ex.: importação dos módulos principais, teste de parsing JSONL com fixture pequena); (3) falhe o PR em caso de erro. Evoluir para testes de unidade em `tool_*` com mocks HTTP. |
| **Esforço estimado** | Médio (configuração inicial 2–5 dias; expansão contínua). |
| **Impacto esperado** | Evidência objetiva de **verificação** (CMMI **VER**) a cada mudança; redução de custo de retrabalho. |
| **CMMI / MPS.BR** | **VER** (verificação sistemática); **V&V** no sentido de detectar defeitos antes da integração; reforço de **GQA** ao padronizar checagens. |

### Texto para o relatório

> Como segunda ação prioritária recomenda-se a implementação de um pipeline de integração contínua com escopo incremental, começando por instalação de dependências, verificação de sintaxe e testes de fumaça sobre os módulos centrais do agente. Tal medida fornece evidências repetíveis de verificação — elemento frequentemente ausente em projetos de pesquisa sem amadurecimento de engenharia — e cria base para evolução em direção a cobertura de testes mais ampla.

---

## Observação sobre certificação

Nenhuma destas ações “garante” certificação MPS.BR ou CMMI; elas **endereçam lacunas observadas** que um avaliador associaria à definição e à evidência de processos básicos (requisitos, qualidade, verificação).
