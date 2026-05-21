# ES_2026-2_DeepResearch

Auditoria de maturidade de processo em ecossistemas LLM — **Atividade Avaliativa 1 (A1)**  
**Disciplina:** Engenharia de Software (COMPO503) — UFS  
**Projeto analisado:** [Alibaba-NLP/DeepResearch](https://github.com/Alibaba-NLP/DeepResearch) (Tongyi DeepResearch)

---

## Vídeo da auditoria técnica

**Link da gravação (YouTube):**

[Vídeo — A1 DeepResearch](https://youtu.be/BGsKtEVcFoI?si=xXmPQ_fwITh0l_YY)

> O mesmo link deve constar no PDF entregue no Google Classroom, conforme normas da disciplina.

---

## Objetivo deste repositório

Consolidar **artefatos da auditoria** (não é um fork de trabalho do código do DeepResearch): documentação por eixo CMMI/MPS.BR, rastreabilidade, diagrama UML, plano de melhoria e instruções de replicação.

---

## Metodologia

1. **Inspeção do clone local** do repositório `DeepResearch` (estrutura, `inference/`, `evaluation/`, `WebAgent/`, configurações).
2. **Cruzamento** com o **GitHub remoto** (issues, pull requests, Actions, Releases) para itens não armazenados no clone.
3. **Mapeamento** dos cinco eixos: GPR, GRE, PJR, V&V, GQA.
4. **Síntese** em dois níveis: evidência objetiva vs. inferência; limitações explícitas.

### Uso de IA na metodologia

Esta auditoria foi conduzida com apoio do **Cursor IDE** em modo agente, usando um assistente baseado em **Claude (família Opus)**, para acelerar leitura de código, redação inicial dos documentos, geração de tabelas e o diagrama Mermaid. **Toda evidência objetiva** (commits, PRs, issues, Releases, Actions, capturas de tela) foi **verificada manualmente** pela Equipe 1, que assina e responde pelo conteúdo final. Descrição detalhada: [docs/uso-de-ia.md](docs/uso-de-ia.md).

---

## Análise por eixo

| Eixo | Documento |
|------|-----------|
| **GPR** — Ciclo de vida e metodologias ágeis | [docs/gestao-projeto-gpr.md](docs/gestao-projeto-gpr.md) |
| **GRE** — Engenharia de requisitos e rastreabilidade | [docs/requisitos-rastreabilidade-gre.md](docs/requisitos-rastreabilidade-gre.md) |
| **PJR** — Arquitetura e modelagem | [docs/arquitetura-pjr.md](docs/arquitetura-pjr.md) |
| **V&V** — Verificação e validação | [docs/verificacao-validacao.md](docs/verificacao-validacao.md) |
| **GQA** — Qualidade de software | [docs/qualidade-gqa.md](docs/qualidade-gqa.md) |

**Índice rápido:** [docs/evidencias.md](docs/evidencias.md) · **Uso de IA:** [docs/uso-de-ia.md](docs/uso-de-ia.md)

### Padrões em OSS (aula 20–21/05/2026)

Atividades 1 a 4 sobre **Template Method**, **Mediator** e **Strategy** no DeepResearch — documento único:

**[atividade-21-05-2026/atividade-padroes-oss.md](atividade-21-05-2026/atividade-padroes-oss.md)**

---

## Achados principais (síntese)

- **Arquitetura:** agente ReAct (`MultiTurnReactAgent`) com ferramentas plugáveis (`BaseTool`), chamada ao modelo via API **OpenAI-compatible** (vLLM local) — ver [docs/arquitetura-pjr.md](docs/arquitetura-pjr.md).
- **V&V:** validação de resultados principalmente por **benchmarks e juiz LLM** (`evaluation/`); **sem** suíte `pytest` evidente na raiz; **sem** workflows de CI de testes no repositório — GitHub Actions mostra apenas *pages build*.
- **GQA:** documentação de uso forte; **ausência** de `CONTRIBUTING.md`; análise estática automatizada não evidenciada.
- **GPR:** evolução contínua por commits/merges; **sem** releases formais na página de Releases (consulta em 2026); roadmap comunicado via README.
- **GRE:** rastreabilidade exemplificada com issues **#233**, **#14**, **#181** — ver tabelas em [docs/requisitos-rastreabilidade-gre.md](docs/requisitos-rastreabilidade-gre.md).

---

## Plano de melhoria (2 ações)

Detalhamento completo: [docs/plano-melhoria.md](docs/plano-melhoria.md)

1. **Formalizar contribuição** — `CONTRIBUTING.md` + templates de issue/PR.  
2. **CI mínimo** — workflow com instalação, lint opcional e testes de fumaça nos módulos centrais.

---

## Diagrama UML

- **Descrição e Mermaid:** [docs/arquitetura-pjr.md](docs/arquitetura-pjr.md)  
- **Ponte para exportação:** [docs/uml.md](docs/uml.md)

---

## Replicação

[docs/replicacao.md](docs/replicacao.md)

---

## Estrutura deste repositório

```
ES_2026-2_DeepResearch/
├── README.md                 # este arquivo
├── LICENSE
├── atividade-21-05-2026/
│   └── atividade-padroes-oss.md   # Padrões em OSS (atividades 1–4)
└── docs/
    ├── evidencias.md
    ├── gestao-projeto-gpr.md
    ├── requisitos-rastreabilidade-gre.md
    ├── arquitetura-pjr.md
    ├── verificacao-validacao.md
    ├── qualidade-gqa.md
    ├── plano-melhoria.md
    ├── uml.md
    ├── relatorio-base.md
    ├── replicacao.md
    └── uso-de-ia.md
```

---

## Equipe — Equipe 1

| # | Nome | Matrícula |
|---|------|-----------|
| 01 | Alícia Vitória Sousa Santos | 202300027015 |
| 02 | Alisson Francisco dos Santos | 202300083248 |
| 03 | Brenno Phelipe Silva dos Santos | 202400050750 |
| 04 | Breno Copeland Pitanga | 202100011225 |
| 05 | Davi Emanuel de Menezes Costa | 202300027178 |
| 06 | Guilherme Rosário Alves | 202100022784 |
| 07 | Uilson Alves dos Santos Neto | 201900115954 |

### Contribuições na auditoria (A1)

Distribuição acordada pela **Equipe 1** *(detalhamento completo na primeira página de* [`docs/relatorio-base.md`](docs/relatorio-base.md)*)*:

| Integrante | Foco principal |
|------------|----------------|
| Alícia Vitória Sousa Santos | GPR — ciclo de vida, roadmap, GitHub/Releases, riscos de API |
| Alisson Francisco dos Santos | GRE — requisitos inferidos, rastreabilidade #233 / #14 / #181 |
| Brenno Phelipe Silva dos Santos | PJR — arquitetura ReAct, camadas, diagrama UML |
| Breno Copeland Pitanga | Introdução, contexto, referências, replicação e anexos/figuras |
| Davi Emanuel de Menezes Costa | V&V — CI, benchmarks, juiz LLM, peer review |
| Guilherme Rosário Alves | Coordenação, `relatorio-base.md`, integração dos `docs/`, figuras GitHub |
| Uilson Alves dos Santos Neto | GQA + plano de melhoria + conclusão |

*Revisão conjunta do relatório e do repositório antes da entrega no Classroom.*

---

## Licença

O conteúdo de documentação produzido pela equipe pode ser licenciado conforme [LICENSE](LICENSE) deste repositório. O código do projeto **DeepResearch** permanece sob a licença do repositório original.
