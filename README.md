# ES_2026-2_DeepResearch

Auditoria de maturidade de processo em ecossistemas LLM — **Atividade Avaliativa 1 (A1)**  
**Disciplina:** Engenharia de Software (COMPO503) — UFS  
**Projeto analisado:** [Alibaba-NLP/DeepResearch](https://github.com/Alibaba-NLP/DeepResearch) (Tongyi DeepResearch)

---

## Vídeo da auditoria técnica

**Substitua o link abaixo pelo URL do vídeo (YouTube, Drive ou outro) após gravação (7–15 min):**

[Vídeo — A1 DeepResearch](https://www.youtube.com/SEU_LINK_AQUI)

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

---

## Análise por eixo

| Eixo | Documento |
|------|-----------|
| **GPR** — Ciclo de vida e metodologias ágeis | [docs/gestao-projeto-gpr.md](docs/gestao-projeto-gpr.md) |
| **GRE** — Engenharia de requisitos e rastreabilidade | [docs/requisitos-rastreabilidade-gre.md](docs/requisitos-rastreabilidade-gre.md) |
| **PJR** — Arquitetura e modelagem | [docs/arquitetura-pjr.md](docs/arquitetura-pjr.md) |
| **V&V** — Verificação e validação | [docs/verificacao-validacao.md](docs/verificacao-validacao.md) |
| **GQA** — Qualidade de software | [docs/qualidade-gqa.md](docs/qualidade-gqa.md) |

**Índice rápido:** [docs/evidencias.md](docs/evidencias.md)

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
    └── replicacao.md
```

---

## Equipe — Equipe 1

| # | Nome | Matrícula |
|---|------|-----------|
| 01 | Alícia Vitória Sousa Santos | 202300027015 |
| 02 | Alisson Francisco dos Santos | 202300083248 |
| 03 | Brenno Phelipe Silva dos Santos | 202400050750 |
| 04 | Davi Emanuel de Menezes Costa | 202300027178 |
| 05 | Guilherme Rosário Alves | 202100022784 |
| 06 | Uilson Alves dos Santos Neto | 201900115954 |

*Contribuições individuais na auditoria: descrever na primeira página do PDF entregue no Google Classroom, conforme normas da disciplina.*

---

## Licença

O conteúdo de documentação produzido pela equipe pode ser licenciado conforme [LICENSE](LICENSE) deste repositório. O código do projeto **DeepResearch** permanece sob a licença do repositório original.
