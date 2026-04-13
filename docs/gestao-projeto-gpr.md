# Ciclo de vida e metodologias ágeis (GPR)

## 1. Evidências no repositório local

### 1.1 Roadmap e comunicação de evolução

- **`README.md`:** seção **News** com datas (ex.: disponibilização no OpenRouter, release do modelo).
- **`WebAgent/README.md`:** linha do tempo de releases de modelos (WebWalker, WebDancer, WebSailor, etc.) e figura de roadmap (`assets/road_map_webwatcher.png`).
- **Interpretação:** planejamento **comunicado** ao público, não substitui Milestones/GitHub Projects para rastrear trabalho interno.

### 1.2 Histórico Git (clone local)

- `git log` mostra commits recentes com correções, merges de PRs e atualizações de subpastas (ex.: `Merge pull request #226`, `#208`).
- **`git tag -l`:** vazio no clone — **não há tags de versão** no histórico local analisado.

### 1.3 Gestão de riscos técnicos (APIs LLM e serviços)

- **`.env.example`:** lista dependências de múltiplos provedores (OpenAI-compatible, Serper, Jina, Dashscope, SandboxFusion).
- **`inference/react_agent.py` — `call_server`:** retentativas e backoff para falhas de rede/API.
- **README:** nota de que demos online podem falhar por latência e limites de QPS — reconhecimento de risco operacional voltado ao usuário.

## 2. Evidências apenas no GitHub remoto (verificação manual)

| Item | Onde verificar | O que registrar no relatório |
|------|----------------|------------------------------|
| Milestones | `https://github.com/Alibaba-NLP/DeepResearch/milestones` | Existência, datas, percentual concluído |
| Projects | Aba Projects do repositório | Quadros Kanban, se houver |
| Releases | `https://github.com/Alibaba-NLP/DeepResearch/releases` | Em abril/2026: **“There aren’t any releases”** — ausência de releases formais |
| Frequência de entrega | Insights → Commits / Releases | Gráfico de atividade; merges por período |
| Discussões de risco | Issues + Discussions | Bugs de API, quebras de compatibilidade |

## 3. Síntese GPR

- **Ritmo:** desenvolvimento contínuo visível por commits e merges; **sem** releases nomeadas no GitHub no momento consultado.
- **Planejamento ágil formal (Milestones/Projects):** **não inferível** pelo filesystem; exige GitHub.
- **Riscos de volatilidade de APIs:** **parcialmente mitigados** no código (retries) e **explicitados** na documentação (dependência de chaves e serviços).

## 4. Relação CMMI / MPS.BR

- **CMMI — Planejamento e monitoramento:** há monitoramento implícito via issues/PRs no GitHub, mas **sem** evidência local de plano de projeto versionado ou estimativas.
- **MPS.BR — Gerência de projetos:** o repositório se comporta como **projeto de pesquisa open source** com comunicação por README; faltam artefatos típicos de gerência (escopo baseline, cronogramo) no código.

## 5. Comandos Git úteis (replicação da auditoria)

```bash
cd /caminho/para/DeepResearch
git log --oneline --since="2025-01-01" | wc -l
git shortlog -sn --since="2025-06-01"
git log --merges --oneline -20
```

## 6. Texto sugerido para o relatório

> A gestão do ciclo de vida no DeepResearch combina divulgação de roadmap e notícias nos arquivos README com um fluxo de desenvolvimento orientado a merges de pull requests visíveis no histórico Git. Não foram encontradas tags de versão no clone local, e a página de Releases do GitHub não lista pacotes versionados, o que enfraquece a rastreabilidade entre “entrega oficial” e conjuntos de commits. Os riscos associados à volatilidade de APIs externas são parcialmente endereçados por retentativas na camada de chamada ao modelo e pela externalização de credenciais em `.env`. Para alinhamento com práticas de gerência de projetos mais formais, recomenda-se complementar esta análise com a inspeção de Milestones e Projects no GitHub, caso existam.
