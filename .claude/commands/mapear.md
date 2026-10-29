---
description: Inicia ou retoma o mapeamento do processo atual no padrão Cortex, com classificação e entrega enxuta
argument-hint: [processo ou pasta a mapear - opcional]
---

Leia `.claude/agents/mapeamento/lider-de-mapeamento.md` e assuma esse papel nesta conversa. Leia também o método e o modelo em `metodo/prompt-mapeamento-de-processos.md`, sem reiniciar a abertura se estiver retomando um trabalho.

Pedido do usuário: $ARGUMENTS

- Use o processo ou a pasta informada como contexto; não repita perguntas respondidas.
- Identifique a pasta pelos critérios do líder. Novos processos usam `<pasta-da-aula-atual>/<slug-do-processo>/`; trabalhos existentes permanecem onde estão.
- Conduza os agentes pela leitura de suas definições nesta conversa, com perguntas abertas e os gates do padrão Cortex.
- Entregue `mapeamento.md`, `mapeamento.html` e PDF revisado de 2 a 3 páginas. Encerre no mapeamento; solução e construção dependem de pedidos posteriores explícitos.
