# Guia de Boas Práticas para Uso de Agentes de IA no Desenvolvimento de Software

## TL;DR

Use agentes de IA como ferramentas especializadas, não como substitutos permanentes de julgamento técnico. Modelos caros e modos de raciocínio avançado devem ser reservados para problemas difíceis, arquitetura, debugging complexo e revisão crítica. Tarefas mecânicas devem ser delegadas a modelos mais baratos, autocompletes ou agentes gratuitos.

A regra central é simples:

> **IA cara pensa. IA barata executa. O desenvolvedor recorta o problema e valida o resultado.**

---

## 1. Objetivo do guia

Este guia define boas práticas para usar agentes de IA em projetos pessoais e profissionais, especialmente em ambientes com limitação de tokens, créditos ou tempo de uso.

O foco é aumentar produtividade sem desperdiçar cota, sem perder controle técnico do código e sem transformar o agente em uma fonte constante de débito técnico.

---

## 2. Princípios gerais

### 2.1. Não use o modelo mais forte para qualquer tarefa

Modelos de alta inteligência devem ser usados quando há necessidade real de raciocínio complexo.

Use modelos fortes para:

- decisões arquiteturais;
- debugging difícil;
- análise de fluxos entre vários arquivos;
- revisão crítica de código;
- segurança;
- concorrência;
- autenticação/autorização;
- transações;
- integração entre sistemas;
- refactors grandes;
- investigação de regressões.

Não use modelos fortes para:

- renomear variáveis;
- criar DTOs simples;
- gerar boilerplate;
- ajustar CSS;
- criar componentes triviais;
- escrever comentários;
- gerar testes óbvios;
- corrigir erro de sintaxe simples;
- fazer alterações repetitivas.

---

### 2.2. Trate o agente como um colaborador caro

Um agente avançado deve ser tratado como um consultor técnico de alto custo. Ele não deve ser usado para tudo. Antes de acioná-lo, pergunte:

- Eu já sei exatamente qual é o problema?
- Eu posso resolver isso com autocomplete?
- Eu posso usar um modelo menor?
- Eu preciso mesmo que o agente leia vários arquivos?
- A tarefa exige raciocínio ou apenas digitação?

Se a tarefa for apenas mecânica, use uma ferramenta mais barata.

---

### 2.3. O desenvolvedor deve recortar o problema

Agentes gastam muitos tokens quando precisam descobrir sozinhos onde mexer. Sempre que possível, entregue o contexto mínimo necessário.

Em vez de pedir:

```txt
Analise o projeto inteiro e implemente a funcionalidade X.
```

Prefira:

```txt
A funcionalidade X envolve apenas estes arquivos:
- user.service.ts
- user.controller.ts
- user.dto.ts

Analise somente esses arquivos. Se precisar de outro arquivo, diga exatamente qual e por quê antes de continuar.
```

---

## 3. Estratégia de camadas

O uso mais eficiente de agentes de IA envolve separar planejamento, execução e revisão.

### 3.1. Camada 1: modelo forte como arquiteto

Use o modelo mais forte para:

- entender o problema;
- desenhar o plano;
- identificar riscos;
- apontar arquivos relevantes;
- sugerir ordem de implementação;
- prever testes necessários.

Exemplo de prompt:

```txt
Analise somente os arquivos indicados.
Não implemente nada ainda.
Quero um plano curto contendo:
- arquivos a alterar;
- ordem de alteração;
- riscos técnicos;
- testes mínimos necessários.
Não explique conceitos básicos. Formate em tópicos simples.
```

---

### 3.2. Camada 2: modelo barato ou agente gratuito como executor

Depois que o plano estiver claro, use uma ferramenta mais barata para executar o trabalho mecânico.

Use para:

- criar arquivos;
- escrever boilerplate;
- gerar testes simples;
- aplicar padrões já definidos;
- replicar estruturas existentes;
- transformar plano em código.

Exemplo de prompt:

```txt
Siga exatamente este plano.
Faça uma alteração por vez.
Não invente arquitetura nova.
Não altere arquivos fora do escopo.
Ao final, mostre apenas o resumo do diff e forneça o código final.
```

---

### 3.3. Camada 3: modelo forte como reviewer

Após a implementação, use o modelo forte para revisar o diff, não o projeto inteiro.

Exemplo:

```txt
Revise este diff como code reviewer.
Aponte apenas problemas que possam causar:
- bug;
- quebra de build;
- falha de segurança;
- regressão;
- inconsistência de contrato.

Ignore estilo, preferências pessoais e melhorias opcionais.
```

- Parar criar um arquivo .txt com o diff: 

```
git diff > diff.txt
```

---

## 4. Boas práticas para economizar tokens

### 4.1. Trabalhe com diffs pequenos

Quanto menor o diff, menor o custo de revisão e menor o risco de erro.

Evite pedir grandes pacotes de alteração. Prefira dividir:

1. ajustar model/schema;
2. ajustar service;
3. ajustar controller;
4. ajustar validações;
5. adicionar testes;
6. revisar diff final.

---

### 4.2. Evite sessões longas demais

Threads longas acumulam contexto antigo, decisões superadas e ruído. Isso aumenta custo (tokens de entrada acumulativos) e piora a qualidade das respostas (alucinações).

Quando a conversa ficar longa, abra uma nova sessão com um resumo curto:

```txt
Contexto:
- Projeto NestJS com PostgreSQL e Prisma.
- Estou mexendo no módulo de tickets.
- Já implementei criação e listagem.
- O problema atual é validar permissões do atendente.

Arquivos relevantes:
- ticket.service.ts
- ticket.controller.ts
- permissions.guard.ts

Tarefa:
Corrigir apenas a validação de permissão para atualização de ticket.
```

---

### 4.3. Não deixe o agente explorar o repositório inteiro sem necessidade

Exploração ampla consome muito contexto. Restrinja explicitamente:

```txt
Não faça busca ampla no repositório.
Analise apenas os arquivos selecionados.
Se precisar de outro arquivo, diga qual arquivo e por que ele é necessário.
```

---

### 4.4. Não rode dois agentes caros em paralelo

Usar o mesmo modelo avançado em dois editores ou projetos ao mesmo tempo pode consumir a cota muito rapidamente.

Recomendação:

- projeto profissional: modelo forte apenas para tarefas críticas;
- projeto pessoal: agente gratuito, modelo menor ou autocomplete;
- revisão final: modelo forte, preferencialmente analisando apenas o diff.

---

### 4.5. Desative explicações longas quando não forem necessárias

Explicações extensas também consomem tokens. Para tarefas práticas, seja explícito:

```txt
Não explique conceitos básicos.
Não escreva resposta longa.
Mostre apenas:
1. arquivos alterados;
2. resumo do que mudou;
3. riscos;
4. testes sugeridos.
```

---

### 4.6. Use arquivos de "Ignore" (.cursorignore / .copilotignore)

Agentes de IA costumam indexar o repositório para buscas semânticas (embeddings). Se o agente ler pastas irrelevantes, seus limites de tokens desaparecerão.
Sempre crie um arquivo equivalente ao `.gitignore` para a IA (ex: `.cursorignore`) e adicione:
- `node_modules/`
- `dist/`, `build/`, `out/`
- `.env`, arquivos de chaves e secrets
- `coverage/`
- Arquivos estáticos pesados (imagens, vídeos).

---

### 4.7. Otimize os Tokens de Saída (Output Tokens)

Tokens gerados pela IA custam de 2 a 3 vezes mais que tokens enviados. Obrigue a IA a ser concisa na resposta adicionando restrições de formato no prompt:
- *"Responda apenas com o código modificado."*
- *"Use formato de checklist sem parágrafos introdutórios."*
- *"Não explique o código gerado."*

---

### 4.8. Mantenha o código modular (Melhora o RAG e reduz custo)

Modelos de IA têm dificuldade em ler e modificar arquivos gigantescos (ex: mais de 1000 linhas) e gastam muitos tokens para reescrevê-los.
Divida responsabilidades em arquivos menores e funções delimitadas. Quanto menor o arquivo, menos contexto precisa ser enviado, reduzindo drasticamente o custo por interação.

---

## 5. Quando usar cada tipo de ferramenta

### 5.1. Modelo avançado / modo de alta inteligência

Use quando o problema envolver:

- múltiplos arquivos com dependências entre si;
- bugs difíceis de reproduzir;
- arquitetura;
- segurança;
- performance;
- integrações externas;
- refatoração arriscada;
- revisão de código importante;
- análise de trade-offs.

Não use esse modo como autocomplete.

---

### 5.2. Modelo intermediário ou mini

Use para:

- implementar tarefas bem especificadas;
- revisar arquivos pequenos;
- gerar testes simples;
- criar funções utilitárias;
- transformar requisitos em checklist;
- analisar mensagens de erro;
- escrever scripts;
- criar documentação técnica curta.

---

### 5.3. Autocomplete de IA

Use para:

- completar linhas;
- sugerir nomes;
- escrever funções pequenas;
- gerar blocos repetitivos;
- completar imports;
- acelerar código que você já sabe escrever.

O autocomplete não deve decidir arquitetura.

---

### 5.4. Agente gratuito ou secundário

Use para:

- projeto pessoal;
- protótipos;
- boilerplate;
- tarefas de baixo risco;
- execução de plano feito por modelo melhor;
- componentes simples;
- pequenas correções.

Sempre revise o resultado antes de aceitar.

---

## 6. Fluxo recomendado para tarefa profissional

### Etapa 1: Entender manualmente a demanda

Antes de chamar o agente, identifique:

- objetivo da tarefa;
- arquivos prováveis;
- regras de negócio;
- risco de regressão;
- testes necessários.

---

### Etapa 2: Pedir plano ao modelo forte

Prompt sugerido:

```txt
Você é um reviewer/arquiteto técnico.
Analise somente os arquivos abaixo.
Não implemente nada.
Produza um plano objetivo para resolver a tarefa.
Inclua:
- arquivos a alterar;
- ordem de implementação;
- riscos;
- testes necessários;
- perguntas bloqueantes, se houver.
```

---

### Etapa 3: Criar um Checkpoint de Segurança (Git)

Antes de deixar a IA editar arquivos (especialmente de forma autônoma), faça um commit temporário:
```bash
git commit -am "chore: wip antes da IA"
```
Se o agente mais barato produzir um código caótico ou modificar arquivos errados na próxima etapa, basta um `git reset --hard` para abortar, poupando tempo de reversão manual.

---

### Etapa 4: Executar com modelo barato ou manualmente

Prompt sugerido:

```txt
Implemente apenas a etapa 1 do plano.
Faça o menor diff possível.
Responda apenas com o código modificado.
Não altere arquitetura, nomes ou estilo fora do necessário.
Não modifique arquivos não relacionados.
```

---

### Etapa 5: Revisar o diff

Use:

```bash
git diff
```

Depois envie ao modelo forte:

```txt
Revise este diff.
Aponte apenas problemas reais.
Não sugira melhorias cosméticas.
Classifique cada ponto como:
- bloqueante;
- importante;
- opcional.
```

---

### Etapa 6: Testar

O agente pode sugerir testes, mas a responsabilidade final é do desenvolvedor.

Checklist mínimo:

- build passa;
- lint passa;
- testes existentes passam;
- fluxo principal funciona manualmente;
- erros previsíveis foram testados;
- não houve alteração colateral em arquivos irrelevantes.

---

## 7. Fluxo recomendado para projeto pessoal

Projetos pessoais toleram mais experimentação, mas ainda exigem controle.

### Estratégia

1. Use agente gratuito para implementar rápido.
2. Use autocomplete para acelerar trechos óbvios.
3. Use modelo intermediário para organizar tarefas.
4. Use modelo forte apenas quando houver bloqueio real.
5. Faça revisão final por diff antes de consolidar mudanças.

Prompt útil:

```txt
Estou em um projeto pessoal.
Priorize velocidade, mas não invente arquitetura complexa.
Implemente a solução mais simples que funcione.
Antes de alterar muitos arquivos, proponha um plano curto.
```

---

## 8. Prompts reutilizáveis

### 8.1. Planejamento

```txt
Analise somente os arquivos selecionados.
Não implemente nada.
Crie um plano curto com:
- objetivo;
- arquivos a alterar;
- ordem das alterações;
- riscos;
- testes mínimos.
Formate a resposta estritamente em tópicos usando Markdown. Se faltar contexto, peça apenas o arquivo específico necessário e não gere suposições.
```

---

### 8.2. Implementação restrita

```txt
Implemente apenas a tarefa descrita.
Faça o menor diff possível.
Não faça refactor oportunista.
Não altere estilo de código não relacionado.
Não modifique arquivos fora do escopo.
Ao final, mostre apenas:
- arquivos alterados;
- resumo do diff;
- testes sugeridos.
Responda fornecendo apenas os blocos de código necessários.
```

---

### 8.3. Revisão de diff

```txt
Revise este diff como code reviewer.
Procure apenas:
- bugs;
- quebras de contrato;
- falhas de segurança;
- regressões;
- problemas de runtime;
- testes faltantes relevantes.
Ignore estilo e preferências pessoais. Formate como uma checklist objetiva.
```

---

### 8.4. Debugging

```txt
Ajude a investigar este bug.
Não proponha solução ainda.
Primeiro liste as hipóteses mais prováveis, em ordem.
Depois diga quais evidências devo coletar para confirmar ou eliminar cada hipótese.
```

---

### 8.5. Refactor controlado

```txt
Quero refatorar este trecho sem alterar comportamento.
Antes de editar, identifique:
- comportamento atual;
- riscos de regressão;
- testes que protegem a mudança;
- menor sequência segura de alteração.
Não implemente até o plano estar claro.
```

---

### 8.6. Testes

```txt
Gere testes para este código.
Cubra apenas:
- caminho feliz;
- erro mais provável;
- edge case relevante.
Não gere testes redundantes nem casos artificiais.
Responda com o código do teste diretamente.
```

---

### 8.7. Controle de contexto

```txt
Não leia o projeto inteiro.
Use apenas o contexto fornecido.
Se precisar de outro arquivo, diga exatamente qual arquivo precisa e por quê.
Não continue sem esse contexto.
```

---

## 9. Checklist antes de chamar um agente caro

Antes de usar modelo avançado, responda:

- A tarefa exige raciocínio complexo?
- Há risco real de quebrar algo importante?
- Eu selecionei os arquivos relevantes?
- O prompt está específico?
- Eu proibi refactor oportunista?
- Eu pedi plano antes de implementação?
- Eu posso usar um modelo menor para executar?
- A sessão atual está curta o bastante?
- O agente precisa mesmo editar arquivos ou apenas orientar?

Se a maioria das respostas for “não”, provavelmente não vale usar o modelo caro.

---

## 10. Checklist depois de aceitar código gerado por IA

Depois que o agente alterar código:

- leia o diff;
- verifique se não houve alteração fora do escopo;
- confira imports e dependências;
- rode build;
- rode testes;
- teste manualmente o fluxo principal;
- procure tratamento de erro ausente;
- verifique logs sensíveis;
- confira se não foram expostos secrets;
- garanta que o código segue o padrão do projeto;
- remova comentários inúteis gerados pela IA.

---

## 11. Sinais de mau uso de agentes

Você provavelmente está desperdiçando tokens quando:

- pede para o agente “analisar tudo” sem necessidade;
- deixa o agente decidir sozinho onde mexer;
- usa modo avançado para tarefas triviais;
- mantém duas sessões caras em paralelo;
- aceita grandes diffs sem revisar;
- usa a mesma thread por muitas horas;
- pede explicações longas para tarefas simples;
- permite refactor oportunista;
- não separa planejamento de execução;
- usa IA para código que você nem chegou a ler.

---

## 12. Sinais de bom uso de agentes

Você está usando bem quando:

- o agente recebe contexto pequeno e relevante;
- cada tarefa gera diff pequeno;
- modelos fortes são usados para raciocínio, não digitação;
- modelos baratos executam tarefas mecânicas;
- você faz checkpoints no Git antes de execuções automatizadas;
- você revisa o diff antes de aceitar;
- cada prompt tem restrições claras e pede objetividade (poucos output tokens);
- o agente pede arquivos específicos, não o projeto inteiro;
- sessões longas são substituídas por resumos curtos;
- decisões importantes continuam sendo suas.

---

## 13. Arquivo auxiliar recomendado no projeto

Crie um arquivo `AI_WORKFLOW.md` na raiz do projeto com informações fixas para reduzir repetição de contexto.

Exemplo:

```md
# AI Workflow

## Stack

- Node.js
- TypeScript
- NestJS
- PostgreSQL
- Prisma
- Docker

## Comandos

- npm run build
- npm run test
- npm run lint
- npx prisma migrate dev

## Padrões do projeto

- Services concentram regras de negócio.
- Controllers não devem conter lógica complexa.
- DTOs validam entrada.
- Repositories/Prisma concentram acesso ao banco.

## Restrições para agentes

- Não fazer refactor oportunista.
- Não alterar arquivos fora do escopo.
- Não criar abstrações sem necessidade.
- Não modificar contratos públicos sem avisar.
- Sempre sugerir testes para mudanças de regra de negócio.

## Exemplo de Código Base (Few-Shot Prompting)

```typescript
// Exemplo de Service Padrão
@Injectable()
export class UserService {
  constructor(private readonly prisma: PrismaService) {}
  
  async findById(id: string): Promise<User | null> {
    return this.prisma.user.findUnique({ where: { id } });
  }
}
```

> **Dica:** Fornecer 1 exemplo de código bem escrito ajuda a IA a imitar o padrão. É muito mais barato em tokens a IA copiar um padrão de código existente do que tentar interpretar longas regras textuais sobre a arquitetura (Few-Shot Prompting).

Esse arquivo pode ser colado ou referenciado no início de sessões novas, evitando que o agente redescubra padrões básicos do projeto.

---
```
## 14. Política pessoal de uso recomendada

Uma política eficiente pode ser:

1. **Autocomplete sempre liberado** para trechos pequenos.
2. **Agente gratuito** para boilerplate e projeto pessoal.
3. **Modelo intermediário** para implementação bem especificada.
4. **Modelo forte** apenas para planejamento, debugging difícil e revisão final.
5. **Nunca usar dois modelos fortes em paralelo.**
6. **Nunca aceitar diff grande sem revisão.**
7. **Nunca pedir análise global quando três arquivos bastam.**
8. **Sempre dividir tarefa grande em etapas menores.**

---
```
## 15. Regra final

O melhor uso não é deixar o agente “codar tudo”. O melhor uso é manter o desenvolvedor no controle do escopo, da arquitetura, dos riscos e da validação, usando a IA para reduzir esforço operacional e ampliar capacidade de análise.

> **Controle o contexto. Controle o diff. Controle o custo.**
