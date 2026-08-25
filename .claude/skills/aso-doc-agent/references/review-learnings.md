---
source-git-commit: 2a3a02ea04fac7ce37fdc43e836a4832be224e25
workflow-type: tm+mt
source-wordcount: '248'
ht-degree: 0%

---
# Agente de documento ASO — Revisar aprendizados

Lições duráveis extraídas do feedback de revisão de RP humana sobre as PRs desse agente. Ler
este arquivo no início da Etapa 4 (Pesquisa + rascunho) em `pipeline.md`, antes da elaboração
qualquer coisa — o ponto é que uma correção que um revisor faz uma vez não deve precisar ser
feito novamente em um próximo ticket.

## O que pertence a este local

Somente feedback **generalizável** — um padrão que se repetirá em tíquetes futuros, aproximadamente
tom, estrutura, seções ausentes, posicionamento de arquivo incorreto ou precisão de conteúdo. Exemplos:

- &quot;Sempre mencione a guia Ignorado para oportunidades que suportam ignorar/ignorar.&quot;
- &quot;Não confirme a marcação no nível da Ultimate, a menos que o tíquete ou uma página irmã existente o confirme — deixe-o comentado e sinalize como um item aberto.&quot;
- &quot;As novas páginas de instruções sobre oportunidades precisam de uma entrada TOC.md e uma entrada card-grid na página de aterrissagem dos tipos de oportunidade, não apenas da página em si.&quot;

## O que NÃO pertence a este local

Feedback mecânico único que se aplicava somente a uma única PR: erros de digitação, um link quebrado, um
vírgula ausente, um caminho de arquivo incorreto nessa PR específica. Corrija-os diretamente na PR — eles
não generalize para rascunhos futuros, portanto, uma entrada durável seria apenas ruído.

## Formato de entrada

```markdown
## YYYY-MM-DD — SITES-XXXXX (PR #NN)

**Lesson:** [one or two sentences — the generalizable rule]

**Why:** [what the reviewer actually said, or the specific mistake it corrects]

**Applies to:** [which ticket types / pages this affects — "all opportunity how-to pages", "settings/setup pages", "everything", etc.]
```

Entradas mais recentes na parte superior. Se uma lição posterior substituir ou restringir uma lição anterior, edite
a entrada anterior para observar que em vez de deixar duas regras conflitantes no arquivo.

&#x200B;---

Nenhuma entrada ainda — este arquivo recebe sua primeira entrada na primeira vez que um humano solicita alterações
em uma das relações públicas desse agente.
