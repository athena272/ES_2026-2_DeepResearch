# Verificação e validação (V&V)

## Distinção conceitual

| Tipo | Significado no contexto DeepResearch | Evidências no repositório |
|------|--------------------------------------|---------------------------|
| **Verificação** | O *software* se comporta conforme especificação técnica (build, execução, formato de saída, ausência de erros óbvios). | Scripts de inferência e avaliação; retries em `call_server`; checagem de tags `<answer>` nas estatísticas. |
| **Validação** | A *resposta da IA* atende ao objetivo do usuário ou a um critério de qualidade externo (benchmark, juiz LLM). | `evaluation/evaluate_deepsearch_official.py` — juiz automático comparando predição com gabarito; métricas agregadas. |

## 1. Verificação (técnica)

### 1.1 Testes automatizados (unitários / integração)

- **Busca no clone local:** não foram encontrados arquivos `test_*.py` nem `pytest` em `requirements.txt` da raiz.
- **Interpretação:** não há suíte de testes automatizados evidente para o núcleo `inference/`; a verificação depende de execução manual ou de pipelines externos não presentes no diretório analisado.

### 1.2 Integração contínua (CI)

**Clone local:** não existe pasta `.github/` no working tree (confirmado com `git ls-tree` sem entradas `.github`).

**GitHub remoto (consulta em abril/2026):** a aba Actions lista **apenas** execuções do workflow nativo **“pages build and deployment”** (GitHub Pages), com **2 execuções** — não há evidência de workflow que rode testes, lint ou build de Python no repositório.

**Conclusão:** a **verificação automatizada contínua** (no sentido clássico de CI para qualidade de código) **não está demonstrada**; o que existe é publicação de páginas.

### 1.3 Mecanismos que reduzem falhas técnicas (não “alucinação”)

- **`inference/react_agent.py` — `call_server`:** retentativas com backoff exponencial para `APIError`, `APIConnectionError`, `APITimeoutError` e falhas genéricas; timeout de 600s.
- **Loop `_run`:** limite de chamadas LLM (`MAX_LLM_CALL_PER_RUN`), limite de tempo (~150 min), truncamento quando contagem de tokens excede limiar e mensagem forçando formato `<answer>`.
- **`sanity_check_output`:** verifica presença de tags `<redacted_thinking>` (uso específico do formato do modelo; não é validação semântica).

## 2. Validação (saída da IA)

### 2.1 Benchmarks e juiz LLM

O arquivo `evaluation/evaluate_deepsearch_official.py` implementa:

- **`call_llm_judge`:** envia pergunta, resposta correta e predição do modelo a um **modelo juiz** (via LiteLLM ou cliente OpenAI), com múltiplas tentativas e formatos estruturados (`json_schema`) para datasets específicos (ex.: BrowseComp, xbench).
- **Critério:** classificação do tipo “Correct/Incorrect” ou equivalente conforme dataset — isso é **validação por proxy**, não prova de ausência de alucinação em sentido forte; depende do juiz e do gabarito.

### 2.2 Anti-alucinação

- **Não há** um módulo dedicado a “detecção de alucinação” no núcleo `inference/`.
- A mitigação observável é **indireta:** uso de ferramentas de busca/visita para ancorar respostas em fontes externas (design do agente ReAct + prompts em `prompt.py`), e **avaliação posterior** em benchmarks.

## 3. Revisão entre pares (peer review)

- **No código:** não há política documentada no repositório local.
- **No GitHub:** exemplos de PRs com revisão (ex.: issue/PR **#233**: aprovação registrada antes do merge). A equipe pode anexar prints ou links no relatório.
- **Limitação:** regras de branch protection e revisão obrigatória **não são verificáveis** publicamente de forma completa; descrever apenas o que for visível nos PRs.

## 4. Relação CMMI / MPS.BR

- **VER (Verification):** ausência de CI de testes enfraquece evidência objetiva de verificação independente e repetível no repositório.
- **VAL (Validation):** scripts de avaliação com juiz e datasets aproximam-se de validação em relação a requisitos de desempenho em benchmarks — alinhado a “validar produto” em cenário de pesquisa.

## 5. Texto sugerido para o relatório (parágrafo)

> A verificação no sentido de testes automatizados e pipeline de CI para o código Python não se materializa de forma clara no repositório analisado: não há suíte `pytest` evidente na raiz nem workflows GitHub Actions dedicados a testes ou análise estática — apenas execuções de *pages build* para GitHub Pages. Em contrapartida, o projeto emprega retentativas na chamada ao servidor de inferência e políticas de término no loop do agente. A validação da qualidade das respostas é principalmente **extrínseca**, via scripts em `evaluation/` que submetem predições a um modelo juiz e comparam com gabaritos, o que se alinha a validação por desempenho em benchmarks, com ressalva de que isso não equivale a garantia formal contra alucinações.
