---
description: Ativa o Agente RH nesta conversa para montar a equipe de agentes de um projeto
argument-hint: [projeto, automação ou software que você quer construir]
---

# rh

Ative o Agente RH **nesta conversa** (não delegue para subagente: ele precisa fazer perguntas ao Bruno).

1. Leia a definição completa do agente em `.claude/agents/rh/rh.md` desta pasta do projeto. Se não achar, avise que o RH não está instalado neste projeto (copie a pasta `.claude/agents/rh/` de outro projeto).
2. Siga o fluxo dela exatamente, do Passo 1 ao Passo 7.
3. Projeto informado pelo Bruno: $ARGUMENTS
   - Se o texto acima estiver vazio, faça a pergunta do Passo 2.
   - Se tiver texto, use-o como resposta do Passo 2 e não pergunte de novo.
4. Ao terminar o Passo 6, salve o resultado na raiz do projeto como `relatorio-rh-<nome-curto-do-projeto>.md` (equipe, funções, tabela de escolhidos, pedidos de criação e fontes).
