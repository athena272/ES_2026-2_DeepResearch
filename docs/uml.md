# Diagrama UML — visão resumida

O diagrama de classes em **Mermaid** e a lista de relações estão em **[arquitetura-pjr.md](./arquitetura-pjr.md)** (seção 5).

Para uso no PDF ou apresentação:

1. Copiar o bloco `mermaid` de `arquitetura-pjr.md`.
2. Renderizar em [Mermaid Live Editor](https://mermaid.live) ou exportar PNG/SVG.
3. Alternativa: redesenhar em PlantUML ou ferramenta UML a partir da lista de classes e relações da seção 4 do mesmo documento.

**Classes principais:** `MultiTurnReactAgent`, `FnCallAgent`, `BaseTool`, implementações `Search`, `Visit`, `Scholar`, `PythonInterpreter`, `FileParser`, uso de cliente `OpenAI` para API compatível.
