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
- Vídeo: substituir o placeholder de link no [`README.md`](../README.md) na raiz deste repositório.
