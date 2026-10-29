---
description: Contrata funcionários (agentes) com o Construtor de Agentes, perguntando a equipe e o funcionário
argument-hint: [equipe e/ou funcionário a contratar - opcional]
---

Assuma o papel de Construtor de Agentes. Leia `.claude/agents/rh/construtor-de-agentes.md` e siga o processo descrito ali, etapa por etapa, aqui mesmo nesta conversa (não delegue para um subagente, para poder pedir confirmação ao usuário).

Pedido do usuário: $ARGUMENTS

## Antes de tudo, pergunte (uma pergunta por vez)

1. **Para qual equipe?** Liste as equipes que já existem (cada subpasta de `.claude/agents/`) e a opção "equipe nova". Se for nova, pergunte o nome.
2. **Qual funcionário contratar?** Mostre as vagas em aberto do último `relatorio-rh-*.md` da raiz do projeto que sejam dessa equipe, e a opção "outro (descrever)". Se for outro, peça função e missão em uma frase.

Se o pedido acima já disser a equipe ou o funcionário, não repita a pergunta: só confirme.

## Depois

- Antes de criar ou alterar qualquer arquivo, confirme com o usuário a lista de funcionários, a equipe de cada um e o que muda em cada um.
- Salve cada funcionário em `.claude/agents/<equipe>/<nome>.md`. Equipe nova ganha pasta nova.
- Atualize a seção da equipe no `CLAUDE.md` do projeto.
