# Garantia da qualidade de software (GQA)

## 1. CONTRIBUTING e governança de contribuição

- **Evidência local:** não existe arquivo `CONTRIBUTING.md` na raiz do clone analisado.
- **Impacto (PPQA / GQA):** contribuidores não têm um guia único versionado para fluxo de PR, padrões de commit ou checklist de qualidade — aumenta variabilidade e dificulta auditoria objetiva de aderência.

## 2. Ferramentas de análise estática

- **CodeQL / SonarQube:** não foram encontrados arquivos de configuração típicos (`.github/codeql`, `sonar-project.properties`) no clone local; a aba Actions remota não indica análise CodeQL nas execuções visíveis.
- **Lint / format / type-check:** não há na raiz `ruff.toml`, `.flake8`, `mypy.ini`, `pyproject.toml` com hooks — o projeto parece depender de convenções implícitas e de dependências em `requirements.txt` sem pipeline obrigatório.

## 3. Pontos fortes observáveis

- **`.env.example`:** documenta variáveis para APIs e caminhos; reduz erro de configuração.
- **`.gitignore`:** exclui `.env`, caches e artefatos de cobertura — boa higiene.
- **Documentação:** `README.md` detalhado, `FAQ.md`, `Tech_Report.pdf`, instruções de formato JSON/JSONL para datasets.
- **Tratamento de erros em pontos críticos:** retries na chamada LLM (`call_server`); loops de retry em busca (`tool_search.py` usa tentativas em laço HTTP).

## 4. Fragilidades e sinais de dívida técnica

- **TODOs dispersos:** comentários `TODO` em subprojetos `WebAgent/` (ex.: multimodalidade, ajustes de modelo) — indicam trabalho incompleto ou dependente de evolução externa.
- **Blocos `except` genéricos:** em `react_agent.py`, vários `except:` sem tipo capturam falhas de ferramenta de forma opaca (mensagens genéricas), dificultando diagnóstico e testabilidade.
- **Acoplamento a serviços externos:** Serper, Jina, Dashscope, sandbox — falhas ou mudanças de API afetam diretamente as tools (risco operacional, não apenas de código).
- **Duplicação / escopo:** o monorepo inclui vários agentes em `WebAgent/` com cópias de utilitários semelhantes — possível duplicação e custo de manutenção.

## 5. Avaliação de aderência (visão local)

| Prática | Aderência observada |
|---------|---------------------|
| Guia de contribuição explícito | Baixa (arquivo ausente) |
| CI para qualidade de código | Não evidenciada |
| Análise estática automatizada | Não evidenciada |
| Documentação de uso | Alta |
| Gestão de segredos (.env) | Adequada no modelo |

## 6. Relação CMMI / MPS.BR

- **PPQA (CMMI):** processo de avaliação objetiva da qualidade dos artefatos fica **fraco** sem contribuição formal e sem gates automatizados visíveis.
- **GQA (MPS.BR):** práticas de garantia da qualidade existem de forma **informal** (documentação, revisões pontuais em PRs no GitHub), não como processo institucionalizado no repositório.

## 7. Texto sugerido para o relatório

> Do ponto de vista de garantia da qualidade, o repositório apresenta documentação de uso robusta e isolamento de credenciais via `.env`, porém carece de um `CONTRIBUTING.md` e de integração contínua que execute testes ou análise estática. A dívida técnica manifesta-se em comentários TODO em submódulos extensos e em tratamento genérico de exceções em trechos do agente. Para uma organização que buscasse maturidade inicial formal (ex.: MPS.BR nível G), seriam necessários artefatos mínimos de processo (guia de contribuição, critérios de aceite) e evidências objetivas de verificação (build/test) nos fluxos de mudança.
