# CLAUDE.md — Córtex ADVANCED

Projeto: **mapeamento de processos com IA, no padrão Cortex**. A ferramenta entrevista o Bruno sobre o processo atual, valida e classifica as etapas em Automatizável, IA ou Humano. Entrega `mapeamento.md`, `mapeamento.html` e PDF de 2 a 3 páginas. O desenho da solução é uma fase posterior, iniciada somente quando o Bruno pedir.

Idioma: PT-BR. Linguagem simples.

## Equipes

Cada equipe (squad) é uma pasta em `.claude/agents/<equipe>/`. Para levar uma equipe para outro projeto, copie a pasta dela para `.claude/agents/` do outro projeto.

### `rh/` — monta e contrata equipes

| Agente | O que faz | O que entrega |
|---|---|---|
| `rh` | Mapeia as equipes do projeto e escreve o pedido de vaga de quem falta, dizendo a equipe. Não cria agentes | `relatorio-rh-<projeto>.md` |
| `construtor-de-agentes` | Cria (contrata) os agentes pedidos pelo RH, depois do "sim" do Bruno, sempre dentro da pasta da equipe | `.claude/agents/<equipe>/<nome>.md` |

### `mapeamento-processos/` — mapeia processos; solução e construção em fase posterior

| Agente | O que faz | O que entrega |
|---|---|---|
| `lider-de-mapeamento` | Conduz as 9 etapas, confere entregas, registra aprovações e coordena correções | `<pasta-do-processo>/status.md` e resumo final |
| `analista-de-processos` | Faz perguntas abertas, coleta fontes em leitura, modela e classifica o processo atual, com impacto estimado e validação humana | Entrevista, coleta, PDD, diagramas de trabalho e `classificacao.md` |
| `designer-de-documentos` | Produz documento enxuto e PDF, com etapas descritivas e classificação | `mapeamento.md`, `mapeamento.html` e PDF de validação ou final |
| `revisor-qa` | Confere fidelidade, classes, estimativas, privacidade e PDF. Só lê e aponta; também revisa construções quando solicitadas | Veredito Aprovado/Devolver, com arquivo e linha |
| `arquiteto-de-automacao` | Só após pedido explícito de solução: desenha o processo futuro e propõe ferramentas; tarefas somente se aceitas | `tobe.md` e, se aceita, `todo.md`, na pasta selecionada |
| `engenheiro-de-automacao` | Só após aprovação do plano e da construção: executa uma tarefa por vez, com dado de teste | `automacao/<nome>/` com o fluxo/script e `LEIAME.md` |

### `pop/` — transforma o mapa validado em POP

| Agente | O que faz | O que entrega |
|---|---|---|
| `redator-de-pop` | Parte de um mapeamento assinado e escreve o POP: responsável, entrada, ação, decisão, saída, controle e exceções por etapa. Não inventa regra nem marca o POP como validado ou aprovado | `<pasta-da-aula>/<slug-do-processo>/pop.md` (ex.: `Aula-02/organizacao-semana-dias-gestor/pop.md`) |
| `revisor-de-pop` | Só lê. Compara o POP com o mapa e confere se dá para executar e controlar, termos, pendências, versão e privacidade | Veredito Aprovado/Devolver, com arquivo e linha |

Ordem: `redator-de-pop` → `revisor-de-pop` → validação de quem executa → aprovação do dono do processo (pessoas, não agentes). Lacuna de fato do processo atual volta ao `analista-de-processos`. Rode os dois nesta conversa.

## Como rodar um mapeamento

**Comece pelo líder:** `/mapear <processo ou pasta>`. Ele identifica a pasta certa e retoma pelo status e pelas evidências dela.

Fluxo padrão: abertura → preparação → entrevista → modelagem → validação do processo (GATE) → classificação (GATE) → documento e PDF (GATE de nome e data) → QA → entrega.

O líder conduz `analista-de-processos` → `designer-de-documentos` → `revisor-qa`. O método e o modelo de saída estão em `Mapeamentos/prompt-mapeamento-de-processos.md`; leia o trecho entre os delimitadores como referência, sem reiniciar a abertura ao retomar. Para seleção de pasta e condução dos agentes, siga o líder.

- Rode cada agente **nesta conversa**, lendo sua definição. O líder mantém as perguntas e os gates; o revisor faz uma passagem separada de leitura dos arquivos salvos. Não delegue entrevistas para subagentes.
- Prefira uma pergunta aberta por vez ou um bloco curto relacionado. Pare nos gates; não repita perguntas nem aprovações já registradas para o mesmo conteúdo. Antes de alterar recursos, explique o escopo e obtenha aprovação, conforme a regra global.
- Novos trabalhos ficam em `Mapeamentos/<aaaa-mm-dd>-<slug-do-processo>/`, preservando a capitalização existente. Não mova, converta, sobrescreva nem consolide mapeamentos anteriores sem aprovação específica. Automações construídas ficam em `automacao/`.
- O `/mapear` termina na entrega revisada. Só depois de um pedido explícito de solução entra o `arquiteto-de-automacao`; construção tem aprovação própria e revisão do `revisor-qa` por tarefa.

## Como montar ou mudar a equipe

1. `/rh <projeto>` — mapeia a equipe e escreve as vagas.
2. Bruno aprova as vagas.
3. `/contratar` — pergunta para qual equipe e qual funcionário; o `construtor-de-agentes` cria na pasta da equipe e atualiza a seção dela acima.

## Princípios universais de execução

Este bloco é universal: todo `CLAUDE.md`/`AGENTS.md`/`GEMINI.md` de projeto, vault ou subdir (existente ou criado depois) precisa replicar este bloco textualmente. Ele orienta comportamento; não concede permissão. Permissões formais continuam em `.agents/agents.yaml`, e regras locais mais restritivas continuam válidas.

1. **Pensar antes de agir.** Antes de implementar, editar, mover, resumir ou responder, identifique objetivo, contexto disponível, restrições e ambiguidade relevante. Se a ambiguidade muda a ação e não pode ser resolvida por ferramenta/contexto, faça uma pergunta curta; se o padrão é óbvio, aja.
2. **Simplicidade primeiro.** Entregue a menor solução correta, verificável e reversível. Evite arquitetura, abstração, automação ou texto que não seja necessário para resolver o problema atual.
3. **Contexto antes de invenção.** Consulte as fontes canônicas disponíveis (vault, arquivos locais, logs, web/ferramentas quando cabível). Se a informação relevante estiver ausente ou contraditória, declare o gap; não preencha com suposição silenciosa.
4. **Discordância útil.** Se o pedido, premissa ou plano parecer errado, perigoso, caro demais ou desalinhado com os objetivos do Bruno, diga isso com fundamento e proponha alternativa melhor.
5. **Ação verificável.** Quando usar ferramentas ou alterar algo, verifique o resultado antes de declarar concluído. Diferencie fato observado, hipótese e recomendação.
6. **Escopo cirúrgico.** Toque só o que a tarefa pede. Não melhore código, texto ou estrutura adjacentes. Não refatore o que não está quebrado. Problema lateral que você viu: mencione em uma linha, não resolva por conta. Efeito colateral que SUAS mudanças criaram: limpe. Bagunça pré-existente: deixe.
7. **Toda resposta termina com próximo passo.** Nenhum agente ou LLM fecha resposta sem propor um próximo passo coerente e objetivo para avançar. Foco em destravar a próxima frente, não em refinar microdetalhes do que acabou de entregar. Se não há próximo passo óbvio, pergunte qual é a próxima frente — silêncio passivo é falha.
