# Prompt: mapeamento de processos (modelo Cortex)

Copie tudo o que está entre as linhas `=====` e cole numa sessão nova do Claude Code, aberta na pasta do seu projeto. Antes de enviar, troque o texto entre colchetes no fim pelo processo que você quer mapear.

=====

Você vai conduzir comigo o mapeamento de um processo da EMR, no modelo Cortex. Responda sempre em português do Brasil.

## Objetivo e entregável

Mapear o processo **como funciona hoje** (as-is), etapa por etapa, e classificar cada etapa em **Automatizável**, **IA** ou **Humano**. O resultado final é um `mapeamento.md` enxuto e o PDF dele, com 2 a 3 páginas, contendo só três partes:

1. **Cabeçalho:** setor, nome do processo, impacto estimado em horas por semana (hoje e potencial), documentado por (agente), assinatura humana e data, versão e confidencialidade.
2. **O processo etapa por etapa:** uma tabela.
3. **Classificação das etapas:** uma tabela.

O PDF não tem capa, sumário nem diagramas. Dores, riscos, pendências, oportunidades, solução e to-do **não entram** no documento final. O desenho da solução é uma fase seguinte, fora deste trabalho.

## Regras

- **Uma pergunta por vez**, ou um bloco curto de perguntas relacionadas. Espere minha resposta antes de seguir. Prefira perguntas abertas; use múltipla escolha só para decisões de fato fechadas.
- **Nada inventado.** Todo dado vem de mim ou de uma fonte que eu indicar. Se faltar algo, pergunte ou registre em "A confirmar".
- **Fontes em modo somente leitura.** Se eu der acesso a uma ferramenta (Azure DevOps, Notion, Jira, planilhas, banco etc.), use só leitura e só para levantar fatos do processo: volumes, tempos, histórico, regras.
- **LGPD e credenciais.** Nenhum nome de aluno ou cliente, e-mail, CPF, telefone, senha, token ou ID interno vai para os arquivos. Pessoas da equipe aparecem pelo papel (CX, TL, analista), exceto quem eu nomear como dono do processo. Ao copiar trechos de uma fonte, guarde só o que foi usado e varra por credenciais antes de salvar.
- **Gates.** Não avance sem meu "de acordo" nos pontos marcados como **GATE** abaixo.
- **Agentes do meu projeto.** Antes da etapa 1, liste os agentes em `.claude/agents/` (e subpastas) e me diga quais vai usar. Para cada etapa, se existir um agente que a cubra, como analista de processos, revisor de QA ou gerador de PDF, delegue a ele e mantenha a condução e as perguntas aqui na conversa. Se não existir, faça você mesmo. Não deixe de cumprir nenhuma etapa por falta de agente.

## Pasta e arquivos

Crie `mapeamentos/<aaaa-mm-dd>-<slug-do-processo>/` e mantenha nela:

- `status.md`: etapas do trabalho com situação (pendente, em andamento, concluída), mais as seções "A confirmar" (tabela `Pendência | Dono | Prazo`) e "Dores e riscos".
- **Arquivos de trabalho**, que servem para conduzir e validar comigo e não entram no PDF:
  - `roteiro-entrevista.md`
  - `entrevista.md`, com respostas, dores, riscos e limites
  - `registro-de-coleta.md`
  - `pdd.md`
  - `mapa-mental.mmd` e `fluxograma.mmd` em Mermaid
  - `classificacao.md`
  - `fonte-<origem>.md`, quando houver
- **Entregáveis:** `mapeamento.md`, `mapeamento.html` e `mapeamento.pdf`.

## Workflow (9 etapas)

### 1. Abertura
Confirme comigo setor, nome do processo, dono do processo (quem valida e assina), onde começa e onde termina, e o objetivo de quem pediu o mapeamento. Crie a pasta e o `status.md`.

### 2. Preparação
Pergunte quais fontes e acessos existem (ferramentas, documentos, guias, histórico), restrições de uso de dados (LGPD, política da empresa) e riscos já conhecidos. Se eu liberar uma fonte, levante nela, em modo leitura:
- volume por semana ou mês;
- tempos típicos de cada fase;
- exemplos de casos, só o padrão, sem dados pessoais;
- regras escritas.

Registre o que encontrou e de onde veio.

### 3. Entrevista
Monte o `roteiro-entrevista.md` com perguntas abertas, escritas para este processo, em blocos:
1. A história de um caso real e recente, do começo ao fim.
2. Passos, pessoas, sistemas, decisões com seus critérios, e passagens de bastão entre pessoas.
3. Exceções e caminhos alternativos. Este bloco é obrigatório.
4. Números: mínimo, típico e máximo; tempo de trabalho contra tempo de espera; de onde vem cada número.
5. Dores, como se mede o sucesso, e o que **não** deveria ser automatizado.
6. Dados e regras: LGPD, prazos, aprovações, compliance.
7. Fechamento: "o que não perguntei?", "quem mais confirma?".

Conduza a entrevista comigo, bloco a bloco, e registre tudo no `entrevista.md`. Quando eu disser "levante no [fonte]", busque lá em vez de me perguntar.

Ao final, liste o que ficou "A confirmar", com dono. Nenhum risco bloqueante pode ficar sem dono.

### 4. Modelagem
A partir da entrevista, monte:
- `registro-de-coleta.md`: tabela com uma linha por etapa, com tarefa, ator, entrada, saída, duração, sistema, frequência e volume;
- `pdd.md`: objetivo, passos, regras de negócio e exceções, só do as-is;
- `mapa-mental.mmd`: processo no centro, com ramos de sistemas, atores, etapas, decisões e exceções, e dados;
- `fluxograma.mmd`: o fluxo com decisões. Use Mermaid válido, sem parênteses ou aspas soltas nos rótulos. Se a mermaid-cli estiver disponível, renderize os `.svg`.

### 5. Validação do processo (GATE)
Apresente o processo como lista numerada de etapas, cada uma com **nome, descrição de 1 a 2 frases completas** (o que a pessoa faz, com quais informações e o que entrega), responsável e sistema, mais as exceções (E1, E2...). Peça meu "de acordo". Corrija até eu aprovar e registre a data no `status.md`. As descrições que eu aprovar aqui são as que vão para o documento.

### 6. Classificação (GATE)
Proponha, em `classificacao.md`, uma tabela `# | Etapa | Classificação | Justificativa` com **todas** as etapas validadas, com a mesma numeração e os mesmos nomes. Critérios:
- **Automatizável:** regra determinística, dado estruturado, sem julgamento.
- **IA:** interpretação de texto ou imagem, classificação, investigação ou redação com julgamento. Onde o erro custa caro, diga na justificativa onde entra a revisão humana.
- **Humano:** só decisão de negócio ou responsabilidade, aprovação, ou ato que exige uma pessoa.

**Classifique pelo potencial**, ou seja, pela natureza da tarefa, e não pelo escopo da primeira automação. Limites que eu der, como "a automação não escreve no sistema X" ou "não responde ao cliente", não rebaixam a etapa para Humano: registre-os no `entrevista.md` como insumo da fase de automação.

Se uma etapa mistura uma parte automatizável ou de IA com uma aprovação humana, divida-a em subetapas (ex.: 7.1 "IA propõe a causa provável" e 7.2 "analista confirma"). Justificativa em 1 ou 2 frases, baseada no que foi dito.

Mostre também um resumo com a contagem por classe. Peça meu "de acordo".

### 7. mapeamento.md e PDF
Escreva o `mapeamento.md` exatamente neste formato:

```markdown
---
setor: <setor>
processo: <nome do processo>
impacto_hoje: ~<N> h/semana (estimativa: <como foi calculado>, fonte <entrevista/ferramenta>)
impacto_potencial: ~<N> h/semana (estimativa: <como foi calculado>, fonte <...>)
documentado_por: Agente Claude (modelo Cortex de mapeamento)
assinatura:
data_assinatura:
versao: 1.0
confidencialidade: Uso interno
---

# O processo etapa por etapa

<Um parágrafo curto, de 2 a 3 frases: onde o processo começa, onde termina, quem o executa e o volume típico.>

| # | Etapa | Responsável | Sistema |
|---|---|---|---|
| 1 | **<nome curto: verbo + objeto>**<br><1 a 2 frases completas: o que a pessoa faz, com quais informações e o que entrega. Se houver regra ou critério de decisão, cite-o.> | <papel> | <sistema> |

## Exceções

| # | Etapa | Responsável | Sistema |
|---|---|---|---|
| E1 | **<nome curto da exceção>**<br><1 a 2 frases completas: quando acontece, o que a pessoa faz e para qual etapa o processo volta.> | <papel> | <sistema> |

# Classificação das etapas

| # | Etapa | Classificação | Justificativa |
|---|---|---|---|
| 1 | **<mesmo nome curto da tabela acima, sem a descrição>** | Automatizável / IA / Humano | <1 a 2 frases completas: por que esta classe e, se for IA, onde entra a revisão humana> |
```

Regras do documento:
- **Impacto.** `impacto_hoje` é a soma, por etapa, da duração típica vezes o volume semanal, ou o número que eu informar. `impacto_potencial` é a parte desse tempo que a automação pode liberar: quase todo o tempo das etapas Automatizável, e o das etapas IA descontada a revisão humana; etapas Humano não entram. Sempre rotule como estimativa e cite a fonte. Sem base para calcular, pergunte; nunca invente.
- **Assinatura.** `assinatura` e `data_assinatura` ficam em branco até o dono validar.
- **Tabelas.** As duas tabelas têm as mesmas etapas, com a mesma numeração e os mesmos nomes curtos. Exceções e subetapas (7.1, 7.2) também entram nas duas. A descrição da etapa aparece só na primeira tabela.
- **Clareza.** Quem não conhece o setor tem que entender o que cada etapa significa só lendo o PDF. Escreva frases completas e concretas (quem faz, o quê, com o quê e o que sai), nunca só um verbo com um objeto. Explique toda sigla ou termo interno na primeira vez em que aparecer (por exemplo, "CPL, o custo por lead"). Use as palavras que eu usei na entrevista.
- **Fora do documento:** diagramas, PDD, dores, riscos, "A confirmar", oportunidades, solução e anexos.

Gere o `mapeamento.html` a partir do `.md`, com o CSS abaixo:
- o cabeçalho vira um bloco de dados no topo;
- as classificações viram selos.

O título do HTML é o nome do processo.

```css
@page { size: A4; margin: 14mm 12mm; }
body { font-family: -apple-system, "Segoe UI", Arial, sans-serif; font-size: 10.5px; color: #1d1d1f; }
h1 { font-size: 15px; margin: 14px 0 6px; border-bottom: 2px solid #1d1d1f; padding-bottom: 3px; }
h2 { font-size: 12px; margin: 10px 0 4px; }
.cabecalho { display: grid; grid-template-columns: 150px 1fr; gap: 3px 10px; border: 1px solid #d2d2d7; border-radius: 6px; padding: 8px 10px; }
.cabecalho dt { font-weight: 600; color: #555; }
table { width: 100%; border-collapse: collapse; margin: 4px 0 8px; }
th, td { border: 1px solid #d2d2d7; padding: 3px 5px; text-align: left; vertical-align: top; }
th { background: #f2f2f5; }
tr { break-inside: avoid; }
td:first-child { width: 28px; text-align: center; }
.selo { display: inline-block; padding: 1px 6px; border-radius: 9px; font-weight: 600; font-size: 9.5px; white-space: nowrap; }
.selo.auto { background: #dff3e4; color: #1b6b34; }
.selo.ia { background: #e3ecfb; color: #1f4ea3; }
.selo.humano { background: #fbe9dc; color: #9a4a12; }
```

Fluxo do PDF:
- **Antes da assinatura:** gere só o HTML e um PDF de validação, `mapeamento-para-validacao.pdf`. No lugar da assinatura, ele tem a linha "Validado por: ____ Data: __/__/____".
- **Depois que eu informar o nome e a data da assinatura (GATE):** preencha `assinatura` e `data_assinatura`, gere o `mapeamento.pdf` final e apague o PDF de validação.
- **Como imprimir:** use o Chrome ou Chromium em modo headless, com `--headless --no-pdf-header-footer --print-to-pdf=<arquivo> <html>`, ou o Playwright se estiver instalado. Se nenhum dos dois estiver disponível, me diga para abrir o HTML no navegador e imprimir em PDF, no formato A4 e sem cabeçalho nem rodapé.
- **Tamanho:** o PDF deve ter 2 ou 3 páginas. Se passar disso, encurte primeiro as justificativas e depois as descrições, mas mantenha em cada etapa pelo menos uma frase completa que explique a tarefa. Não reduza a fonte nem corte etapas.

### 8. QA
A revisão deve ser feita por quem não escreveu o documento:
- **Se houver agente de QA** ou revisor no meu projeto, use-o.
- **Se não houver,** acione um subagente `general-purpose`, que vem com o Claude Code, para revisar a pasta com contexto limpo. Ele só lê e reporta; não altera arquivos.
- **Se não for possível usar subagente,** faça você mesmo, relendo os arquivos do disco.

Você corrige o que for apontado e me reporta. O revisor confere:
- **Cabeçalho:** completo, com impacto rotulado como estimativa e com fonte.
- **Estrutura:** só as duas seções; sem diagramas, dores, riscos ou solução no documento.
- **Etapas:** todas as validadas estão presentes, iguais nas duas tabelas, e cada uma tem classificação e justificativa.
- **Clareza:** cada etapa tem descrição em frases completas que uma pessoa de fora do setor entende (o que faz, com quê e o que entrega); nenhuma sigla ou termo interno sem explicação.
- **Origem dos dados:** nada inventado; cada número tem fonte.
- **Privacidade:** nenhum dado pessoal ou credencial em **nenhum** arquivo da pasta. Faça uma busca por e-mails, CPFs, telefones, "senha", "token" e "login".
- **PDF:** 2 a 3 páginas.

### 9. Entrega
Mostre:
- os caminhos do `mapeamento.md` e do PDF;
- a contagem por classe;
- o impacto de hoje e o potencial;
- as pendências de "A confirmar", com dono.

Atualize o `status.md`. Pare aqui: o desenho da solução é a fase seguinte, e só começa quando eu pedir.

## Comece agora

Comece pela etapa 1 com o processo abaixo. Faça a primeira pergunta.

**Processo a mapear:** [DESCREVA AQUI: setor, o que é o processo, quem participa, por onde chega o trabalho, para onde vai e por que você quer mapear e automatizar]

=====
