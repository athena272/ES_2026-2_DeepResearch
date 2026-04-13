# Engenharia de requisitos (GRE) — rastreabilidade

## 1. Processo RFC / propostas formais

- **Clone local:** não há pasta `rfcs/`, `docs/rfc/` nem menções a “RFC” nos `.md` pesquisados na raiz.
- **Conclusão:** mudanças parecem seguir o fluxo **Issues + Pull Requests** do GitHub, não um processo RFC nomeado no repositório.

## 2. Três requisitos inferidos (da documentação e do código)

| ID | Requisito inferido | Evidência documental | Evidência no código |
|----|-------------------|----------------------|---------------------|
| **R1** | O sistema deve aceitar datasets de avaliação em **JSON** ou **JSONL** com campos `question` e `answer`. | `README.md` (seção “Prepare Evaluation Data”) | `run_multi_react.py` — leitura de `.json` / `.jsonl` e validação básica |
| **R2** | O agente deve permitir **chamadas a ferramentas** (busca, visita, scholar, Python, parse de arquivos) durante o raciocínio ReAct. | `README.md`, `prompt.py` (assinaturas em `<tools>`) | `react_agent.py` — `TOOL_CLASS`, `custom_call_tool` |
| **R3** | A inferência deve obter respostas do modelo via **API compatível com OpenAI** (servidor local vLLM ou, opcionalmente, OpenRouter). | `README.md` (Quick Start, seção OpenRouter), comentários em `react_agent.py` | `call_server` usando `OpenAI` SDK e `http://127.0.0.1:{port}/v1` |

## 3. Trilhas de rastreabilidade (Issue → PR → código)

### Trilha A — completa (exemplo real verificado no GitHub)

| Etapa | Artefato | Detalhe |
|-------|----------|---------|
| **Problema / requisito corretivo** | [Issue #233](https://github.com/Alibaba-NLP/DeepResearch/issues/233) | Ajuste de lógica (`parse_retry_times`) e importação tipada (`Any`). |
| **Mudança integrada** | [PR #233](https://github.com/Alibaba-NLP/DeepResearch/pull/233) | Revisão aprovada; merge em 2026-01-08. |
| **Código final** | Commits `c05398f`, `f4b6a05` | `inference/tool_visit.py`, `inference/tool_python.py` |

### Trilha B — issue de defeito → correção em arquivo

| Etapa | Artefato | Detalhe |
|-------|----------|---------|
| **Issue** | [Issue #14](https://github.com/Alibaba-NLP/DeepResearch/issues/14) | WebWalker executava sempre no site de exemplo; URL incorreta / configuração. |
| **Integração** | Commit `569126e` (mensagem: `fix WebWalker env variable and root url bug (#14)`) | Ligação explícita ao número da issue. |
| **Código** | `WebAgent/WebWalker/src/app.py` | Alteração pontual (1 arquivo no commit citado). |

*Nota:* a timeline da issue #14 referencia também o commit `72fa820`; em auditorias diferentes pode haver múltiplos commits para o mesmo relato — vale cruzar `git log` com os comentários da issue.

### Trilha C — melhoria de benchmark / dados

| Etapa | Artefato | Detalhe |
|-------|----------|---------|
| **Rastreabilidade** | Commit `eb0c36d` — `update BrowseComp-vl benchmark of WebWatcher (#181)` | Referência à issue **#181**. |
| **Código / dados** | `WebAgent/WebWatcher/benchmark/bc_vl_level1.jsonl`, `bc_vl_level2.jsonl` | Atualização massiva de entradas de benchmark. |

## 4. O que ainda pode ser preenchido manualmente

Para cada linha da tabela abaixo, abrir o PR no GitHub e copiar hash de merge e lista de arquivos (já parcialmente feito acima).

| Issue | PR (número) | Commit principal | Arquivos |
|-------|-------------|-------------------|----------|
| #233 | #233 | `f4b6a05` | `inference/tool_python.py`, `inference/tool_visit.py` |
| #14 | *(verificar PR vinculado na UI, se houver)* | `569126e` | `WebAgent/WebWalker/src/app.py` |
| #181 | *(verificar PR na UI)* | `eb0c36d` | `WebAgent/WebWatcher/benchmark/*.jsonl` |

## 5. Relação CMMI / MPS.BR

- **REQM / Gerência de requisitos:** as trilhas mostram **ligação** entre relatos públicos (issues) e alterações no código; a profundidade depende do uso consistente de “Closes #n” e de templates de issue — a ser confirmado amostralmente no GitHub.

## 6. Texto sugerido para o relatório

> A engenharia de requisitos no DeepResearch manifesta-se de forma predominante **informal**, centrada em issues e pull requests, sem processo RFC dedicado nos arquivos versionados. Foram construídas três trilhas de rastreabilidade: (i) a correção vinculada à issue #233, integrada pelo pull request homônimo e materializada em alterações nos arquivos `inference/tool_visit.py` e `inference/tool_python.py`; (ii) o defeito descrito na issue #14, com commit explícito na linha do histórico apontando para `WebAgent/WebWalker/src/app.py`; (iii) a atualização de benchmarks BrowseComp-vl referenciada à issue #181. Requisitos funcionais de alto nível — formato de entrada de dados, uso de ferramentas pelo agente e consumo de API OpenAI-compatible — foram inferidos a partir do README e corroborados pelo código do agente ReAct.
