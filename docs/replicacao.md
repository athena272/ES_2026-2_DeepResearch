# Como replicar esta auditoria

Este repositório documenta a análise do projeto **DeepResearch**. Para reproduzir os passos:

## 1. Clonar o projeto analisado

```bash
git clone https://github.com/Alibaba-NLP/DeepResearch.git
cd DeepResearch
```

Use o mesmo commit da auditoria se quiser resultados idênticos:

```bash
git rev-parse HEAD
# Ex.: f72f75d (ajustar conforme o momento da auditoria)
```

## 2. Mapeamento de arquivos

- Listar raiz: `ls` / explorador — pastas `inference`, `evaluation`, `WebAgent`.
- Ler: `README.md`, `.env.example`, `inference/react_agent.py`, `inference/prompt.py`, `evaluation/evaluate_deepsearch_official.py`.

## 3. Evidências Git (local)

```bash
git log --oneline -40
git tag -l
git show <commit> --stat
```

## 4. GitHub (remoto)

- **Issues / PRs:** `https://github.com/Alibaba-NLP/DeepResearch/issues` e `/pulls`
- **Actions:** `https://github.com/Alibaba-NLP/DeepResearch/actions`
- **Releases:** `https://github.com/Alibaba-NLP/DeepResearch/releases`

## 5. Ferramentas opcionais

- Contagem de TODOs: `rg "TODO|FIXME" --glob "*.py"`
- Busca por testes: `glob` ou `rg "pytest"` em `requirements.txt` e arquivos `test_*.py`

## 6. Entregáveis da equipe

- PDF no Classroom (normas da disciplina).
- Vídeo: link público em [`README.md`](../README.md) (YouTube).

## 7. Reuso de IA na replicação (opcional)

Se quiser reproduzir o **mesmo tipo de apoio** que a Equipe 1 utilizou na redação da auditoria:

1. Instale o **Cursor IDE** e abra o clone do `DeepResearch` (e, se aplicável, o repositório `ES_2026-2_DeepResearch`).
2. Use o assistente configurado (neste trabalho: família **Claude** / **Opus** no Cursor) com prompts explícitos — por exemplo: explicar `MultiTurnReactAgent._run`, resumir `evaluation/evaluate_deepsearch_official.py`, ou estruturar uma tabela de eixos CMMI/MPS.BR.
3. **Sempre valide** a saída contra o **código-fonte** e o **GitHub** (issues, PRs, Actions, Releases). O modelo pode variar entre execuções; a auditoria válida é a que permanece ancorada em evidências objetivas.

Detalhamento do método, fronteira humano/IA e declaração de responsabilidade: [`uso-de-ia.md`](./uso-de-ia.md).
