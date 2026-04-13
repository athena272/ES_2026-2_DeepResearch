# Base para o relatório PDF (A1)

Use este roteiro para gerar o **PDF** no Classroom. Ajuste formatação ABNT ou normas do professor conforme orientação local.

## Capa / primeira página

- Título: **Atividade Avaliativa 1 — Auditoria de Maturidade em Ecossistemas LLM**
- Disciplina, turma, semestre
- **Projeto analisado:** DeepResearch — `https://github.com/Alibaba-NLP/DeepResearch`
- **Equipe 1** — completar com **contribuição individual** de cada membro:

| # | Nome | Matrícula |
|---|------|-----------|
| 01 | Alícia Vitória Sousa Santos | 202300027015 |
| 02 | Alisson Francisco dos Santos | 202300083248 |
| 03 | Brenno Phelipe Silva dos Santos | 202400050750 |
| 04 | Davi Emanuel de Menezes Costa | 202300027178 |
| 05 | Guilherme Rosário Alves | 202100022784 |
| 06 | Uilson Alves dos Santos Neto | 201900115954 |

- Data

## 1. Introdução

- Objetivo da auditoria
- Escopo (cinco eixos GPR, GRE, PJR, V&V, GQA)
- Metodologia (clone local + GitHub remoto)
- Limitações (o que só o remoto comprova)

## 2. Contexto do projeto DeepResearch

- Propósito (agente de pesquisa profunda, Tongyi DeepResearch)
- Stack (Python, vLLM, qwen_agent, ferramentas externas)
- Estrutura de pastas relevante (`inference/`, `evaluation/`, `WebAgent/`)

## 3. GPR — Ciclo de vida e metodologias ágeis

- Roadmap comunicado (README, WebAgent)
- Histórico Git / ausência de tags (se aplicável)
- Releases e Milestones (dados do GitHub)
- Riscos de APIs LLM e mitigações (`.env`, retries)

*Fonte interna:* `docs/gestao-projeto-gpr.md`

## 4. GRE — Engenharia de requisitos

- Três requisitos inferidos (formato de dados, ferramentas, API OpenAI-compatible)
- Tabelas de rastreabilidade Issue → PR → código (ex.: #233, #14, #181)
- Ausência de processo RFC nomeado

*Fonte interna:* `docs/requisitos-rastreabilidade-gre.md`

## 5. PJR — Arquitetura e modelagem

- Fluxo ReAct e separação de camadas
- Padrões (Strategy, Adapter, Facade, Pipeline)
- **Figura:** diagrama de classes UML (exportar de Mermaid ou redesenhar)

*Fonte interna:* `docs/arquitetura-pjr.md`, `docs/uml.md`

## 6. V&V — Verificação e validação

- Distinção verificação vs. validação
- Testes automatizados e CI
- Benchmarks e juiz LLM
- Peer review (exemplos de PRs)

*Fonte interna:* `docs/verificacao-validacao.md`

## 7. GQA — Qualidade de software

- CONTRIBUTING, lint, análise estática
- Pontos fortes e fragilidades
- Dívida técnica (TODOs, exceções genéricas)

*Fonte interna:* `docs/qualidade-gqa.md`

## 8. Plano de melhoria de processo

- Duas ações prioritárias (MPS.BR G / maturidade inicial)
- Relação com CMMI e MR-MPS-SW

*Fonte interna:* `docs/plano-melhoria.md`

## 9. Conclusão

- Síntese dos achados
- Trabalhos futuros (aprofundar WebAgent, métricas de Issues)

## Referências

- Repositório: https://github.com/Alibaba-NLP/DeepResearch
- Documentos da equipe neste repositório
- Material de aula (CMMI-DEV v2.0, MR-MPS-SW) — conforme bibliografia do professor

## Anexos (opcional)

- Screenshots GitHub (Actions, issue #233)
- Hash do commit da auditoria: `git rev-parse HEAD` no clone do DeepResearch
