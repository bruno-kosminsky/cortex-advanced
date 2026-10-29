# Córtex ADVANCED

Equipes de agentes de IA, para o [Claude Code](https://claude.com/claude-code), que **mapeiam um processo de trabalho** e **transformam o mapa em um POP** (Procedimento Operacional Padrão).

Este repositório guarda só os agentes e os processos que eles seguem. Os resultados de cada trabalho (mapas, POPs, relatórios) ficam fora, porque podem conter informação interna.

## Como funciona

Um processo passa por três fases. Cada fase termina em um ponto em que uma pessoa decide.

| Fase | Comando | O que sai | Quem decide |
|---|---|---|---|
| 1. Mapear | `/mapear` | `mapeamento.md`, `mapeamento.html` e PDF de 2 a 3 páginas, com cada etapa classificada em **Automatizável**, **IA** ou **Humano** | O dono do processo valida o processo, a classificação e assina |
| 2. Escrever o POP | `/escrever-pop` | `pop.md`: quem faz, o que faz, com o quê, como confere e o que fazer nas exceções | Quem executa o processo valida; o dono aprova |
| 3. Automatizar | pedido explícito | Desenho do processo futuro e, se aceito, a construção | O dono aprova o plano e cada construção |

A fase 3 só começa quando a pessoa pede. O `/mapear` termina na entrega do mapa revisado.

## Equipes e agentes

Cada equipe é uma pasta em `.claude/agents/`.

**`mapeamento/`**: mapeia o processo atual.

| Agente | O que faz |
|---|---|
| `lider-de-mapeamento` | Conduz as 9 etapas, registra as aprovações e coordena as correções |
| `analista-de-processos` | Entrevista com perguntas abertas, coleta fontes em leitura, modela e classifica o processo |
| `redator-de-mapa` | Escreve o mapa e gera HTML e PDF |
| `revisor-de-mapa` | Só lê. Confere fidelidade, classes, estimativas, privacidade e PDF |

**`pop/`**: transforma o mapa assinado em POP.

| Agente | O que faz |
|---|---|
| `redator-de-pop` | Escreve o POP sem inventar regra e avalia se o processo deve virar um POP ou vários |
| `revisor-de-pop` | Só lê. Compara o POP com o mapa e confere se dá para executar e controlar |

**`automacao/`**: só sob pedido explícito.

| Agente | O que faz |
|---|---|
| `arquiteto-de-automacao` | Desenha o processo futuro e propõe ferramentas |
| `engenheiro-de-automacao` | Constrói uma tarefa por vez, com dado de teste |

**`rh/`**: monta e contrata equipes.

| Agente | O que faz |
|---|---|
| `rh` | Mapeia a equipe existente e escreve o pedido de vaga de quem falta. Não cria agentes |
| `construtor-de-agentes` | Cria o agente pedido, depois da aprovação, dentro da pasta da equipe |

## Comandos

| Comando | Para que serve |
|---|---|
| `/mapear <processo ou pasta>` | Inicia ou retoma o mapeamento de um processo |
| `/escrever-pop` | Escreve o POP a partir de um mapa assinado |
| `/revisar-pop` | Revisa o POP escrito |
| `/rh <projeto>` | Monta a equipe de agentes de um projeto |
| `/contratar` | Cria o agente aprovado, na equipe escolhida |

## Estrutura do repositório

```
.claude/
  agents/{mapeamento, pop, automacao, rh}/   um arquivo .md por agente
  commands/                                  um arquivo .md por comando
metodo/prompt-mapeamento-de-processos.md     o método das 9 etapas e o modelo do mapa
CLAUDE.md                                    regras e fluxo do projeto
```

## Regras que os agentes seguem

- **Nada inventado.** Todo dado vem da pessoa ou de uma fonte indicada. O que falta vira pendência com dono.
- **Pessoas decidem nos gates.** Validação do processo, classificação, assinatura, validação de quem executa e aprovação do POP são humanas. Nome e data de assinatura vêm da própria pessoa.
- **Fontes em leitura.** Sistemas consultados no levantamento são só lidos.
- **Privacidade.** Nenhum dado pessoal, e-mail, telefone, CPF ou credencial vai para os arquivos.
- **Revisão separada.** Quem revisa lê os arquivos salvos, não confia no que foi escrito.
- **Onde gravar.** Cada processo novo fica em `<pasta-da-aula>/<slug-do-processo>/`, com o mapa, o POP e os materiais juntos.
- **Nesta conversa.** Os agentes rodam lendo a definição na própria conversa, para poder perguntar à pessoa. Não são delegados a subagentes.

## Como usar em outro projeto

1. Copie para o seu projeto as pastas `.claude/agents/` (ou só as equipes que quiser), `.claude/commands/` e `metodo/`.
2. Copie o `CLAUDE.md` e **adapte** o que for específico de quem o escreveu: nomes, caminhos e regras locais.
3. Abra o Claude Code na pasta do projeto e rode `/mapear <processo>`.

Para levar uma equipe isolada, copie a pasta dela em `.claude/agents/`.

## Limites

- Os agentes são instruções para o Claude Code, não um programa. O resultado depende da conversa e da revisão das pessoas.
- Estimativas de impacto (horas por semana) são estimativas com fonte e premissas, não medições.
- Este repositório não define licença de uso.
