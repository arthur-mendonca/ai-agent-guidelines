Save as PDF

Conversation with Gemini
Criei este repo para guardar diretrizes e melhores práticas de uso de agentes de IA principalmente porque essa porra fica mais cara a cada dia e ficou muito fácil esgotar os "créditos de IA" em apenas um dia e se ver obrigado ou a esperar bastante tempo para continuar o projeto ou a comprar créditos (que é o objetivo verdadeiro das empresas de IA). Tendo isso em vista, quero que você me ajude a melhorar este documento .md presente no repo. Atualmente ele trata de métodos para economizar token, por ex. usando modelos mais caros para planejamento geral e modelos mais baratos para execução com limites bem claros e fornece uma política geral de uso de agentes de IA com foco em economia de tokens.



Preciso que você analise criticamente estas diretrizes de uso de agentes de IA. As regras são boas? Precisam de reparos? Adições, correções? Há pontos importantes não explorados?

Coding partner
Olá! Como seu parceiro de codificação, meu propósito é ajudar você a planejar, escrever, revisar e otimizar seus projetos de software. Posso te guiar em boas práticas, sugerir melhorias em arquitetura e, claro, colocar a mão na massa no código com você!

Fiz uma análise detalhada do seu guia e, em resumo: o documento está excelente, incrivelmente pragmático e muito alinhado com a realidade atual do desenvolvimento com IA. A regra central de que "IA cara pensa" e "IA barata executa" é uma das estratégias mais eficientes para economizar recursos. Além disso, a sua "Estratégia de camadas" para separar planejamento, execução e revisão é perfeita para manter a qualidade do código.

Ainda assim, como nosso objetivo é criar o guia definitivo para economia de tokens e controle técnico, trago algumas adições, refinamentos e pontos não explorados que você pode incluir no seu .md para torná-lo ainda mais poderoso.

1. Pontos Fortes (O que manter e valorizar)
Controle de Contexto: A recomendação de evitar que o agente explore o repositório inteiro e a instrução de fornecer os arquivos exatos são a melhor forma de poupar tokens de entrada (input tokens).

Uso do arquivo AI_WORKFLOW.md: Criar um arquivo com o contexto fixo do projeto evita repetições desnecessárias a cada nova sessão.

Renovação de Sessões: Fechar sessões longas e abrir novas enviando um resumo do contexto atual é uma técnica vital que previne a "alucinação" da IA e reduz o custo exponencial das conversas longas.

2. Adições e Correções Sugeridas
Aqui estão algumas sugestões de seções e regras adicionais voltadas diretamente para código e economia:

A. Adicionar o conceito de "Ignore Files" (Ex: .cursorignore / .copilotignore)
Agentes de IA costumam indexar o repositório para buscas ("embeddings"). Se o agente ler pastas compiladas ou dependências, seus tokens vão desaparecer em segundos.

O que adicionar: Recomende a criação de arquivos como .cursorignore (ou equivalente da IDE) para bloquear o agente de ler pastas como node_modules, dist, build, coverage ou arquivos .env. Isso garante que as buscas amplas, quando acidentais ou necessárias, consumam uma fração mínima de tokens.

B. Checkpoints no Controle de Versão (Git)
No "Fluxo recomendado para tarefa profissional", falta um passo de segurança essencial entre o Plano e a Execução.

O que adicionar: Antes de deixar a IA mais barata executar o código na Etapa 3, o desenvolvedor deve fazer um commit (ex: git commit -am "chore: wip antes da IA"). Isso permite que, se a IA gerar um diff caótico ou mexer em arquivos errados, o desenvolvedor possa usar um simples git reset --hard para abortar, em vez de gastar tempo desfazendo alterações arquivo por arquivo.

C. Few-Shot Prompting (Dar um exemplo economiza explicações)
No seu tópico sobre AI_WORKFLOW.md, você lista regras e padrões.

O que adicionar: Recomende colocar no AI_WORKFLOW.md um trecho de código de exemplo (Few-Shot Prompting). É muito mais "barato" em tokens mostrar um componente padrão ou a assinatura de um método do que tentar explicar por texto como a arquitetura funciona.

Exemplo para adicionar no guia: "Forneça 1 exemplo de código bem escrito no seu arquivo de contexto. A IA gasta menos tokens imitando um padrão existente do que lendo longas regras em texto."

D. Otimização de Tokens de Saída (Output Tokens)
Os tokens de saída (a resposta gerada pela IA) geralmente custam de 2x a 3x mais do que os tokens de entrada.

O que adicionar nas Boas Práticas (Seção 4): Instrua os usuários a sempre limitarem a verbosidade. Você já diz para desativar explicações longas, mas pode adicionar instruções de formato aos prompts, como:

"Responda apenas com o código modificado."

"Use formato de checklist (markdown) sem parágrafos introdutórios."

E. A Regra do "Código Modular" para melhoria do RAG
Modelos de IA têm dificuldade em modificar arquivos gigantescos (mais de 1000 linhas) e gastam muitos créditos para reescrevê-los.

O que adicionar: Uma boa prática para trabalhar com agentes é manter arquivos pequenos e funções bem delimitadas. Quanto menor o arquivo, menos contexto precisa ser enviado no prompt, reduzindo o custo por interação.

3. Pequenos Reparos nos Prompts do Documento
Nos seus "Prompts reutilizáveis", recomendo adicionar uma instrução explícita sobre a formatação.

Por exemplo, no 8.1. Planejamento, você pode complementar o texto para:

Plaintext
Analise somente os arquivos selecionados.
Não implemente nada.
Crie um plano curto com:
- objetivo;
- arquivos a alterar;
- ordem das alterações;
- riscos;
- testes mínimos.
Formate a resposta estritamente em Markdown. Se faltar contexto, peça apenas o arquivo específico necessário e não gere suposições.
Resumo
Seu guia já resolve 90% do problema de desperdício de tokens. Se você adicionar as ideias de arquivos de ignore (.cursorignore), checkpoints de git antes de acionar a IA, e limitação focada em tokens de saída (output tokens), ele ficará perfeito.

Gostaria de ajuda para reescrever alguma dessas seções e gerar o código Markdown com essas atualizações para o seu repositório? Estou pronto para começar!

Você consegue gerar o arquivo .md com as correções e adições sugeridas?

Coding partner
Prefira:

Plaintext
A funcionalidade X envolve apenas estes arquivos:
- user.service.ts
- user.controller.ts
- user.dto.ts

Analise somente esses arquivos. Se precisar de outro arquivo, diga exatamente qual e por quê antes de continuar.
3. Estratégia de camadas
O uso mais eficiente de agentes de IA envolve separar planejamento, execução e revisão.

3.1. Camada 1: modelo forte como arquiteto
Use o modelo mais forte para:

entender o problema;

desenhar o plano;

identificar riscos;

apontar arquivos relevantes;

sugerir ordem de implementação;

prever testes necessários.

Exemplo de prompt:

Plaintext
Analise somente os arquivos indicados.
Não implemente nada ainda.
Quero um plano curto contendo:
- arquivos a alterar;
- ordem de alteração;
- riscos técnicos;
- testes mínimos necessários.
Não explique conceitos básicos. Formate em tópicos simples.
3.2. Camada 2: modelo barato ou agente gratuito como executor
Depois que o plano estiver claro, use uma ferramenta mais barata para executar o trabalho mecânico.

Use para:

criar arquivos;

escrever boilerplate;

gerar testes simples;

aplicar padrões já definidos;

replicar estruturas existentes;

transformar plano em código.

Exemplo de prompt:

Plaintext
Siga exatamente este plano.
Faça uma alteração por vez.
Não invente arquitetura nova.
Não altere arquivos fora do escopo.
Ao final, mostre apenas o resumo do diff e forneça o código final.
3.3. Camada 3: modelo forte como reviewer
Após a implementação, use o modelo forte para revisar o diff, não o projeto inteiro.

Exemplo:

Plaintext
Revise este diff como code reviewer.
Aponte apenas problemas que possam causar:
- bug;
- quebra de build;
- falha de segurança;
- regressão;
- inconsistência de contrato.

Ignore estilo, preferências pessoais e melhorias opcionais.
4. Boas práticas para economizar tokens
4.1. Trabalhe com diffs pequenos
Quanto menor o diff, menor o custo de revisão e menor o risco de erro.

Evite pedir grandes pacotes de alteração. Prefira dividir:

ajustar model/schema;

ajustar service;

ajustar controller;

ajustar validações;

adicionar testes;

revisar diff final.

4.2. Evite sessões longas demais
Threads longas acumulam contexto antigo, decisões superadas e ruído. Isso aumenta custo (tokens de entrada acumulativos) e piora a qualidade das respostas (alucinações).

Quando a conversa ficar longa, abra uma nova sessão com um resumo curto:

Plaintext
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
4.3. Não deixe o agente explorar o repositório inteiro sem necessidade
Exploração ampla consome muito contexto. Restrinja explicitamente:

Plaintext
Não faça busca ampla no repositório.
Analise apenas os arquivos selecionados.
Se precisar de outro arquivo, diga qual arquivo e por que ele é necessário.
4.4. Não rode dois agentes caros em paralelo
Usar o mesmo modelo avançado em dois editores ou projetos ao mesmo tempo pode consumir a cota muito rapidamente.

Recomendação:

projeto profissional: modelo forte apenas para tarefas críticas;

projeto pessoal: agente gratuito, modelo menor ou autocomplete;

revisão final: modelo forte, preferencialmente analisando apenas o diff.

4.5. Desative explicações longas quando não forem necessárias
Explicações extensas também consomem tokens. Para tarefas práticas, seja explícito:

Plaintext
Não explique conceitos básicos.
Não escreva resposta longa.
Mostre apenas:
1. arquivos alterados;
2. resumo do que mudou;
3. riscos;
4. testes sugeridos.
4.6. Use arquivos de "Ignore" (.cursorignore / .copilotignore)
Agentes de IA costumam indexar o repositório para buscas semânticas (embeddings). Se o agente ler pastas irrelevantes, seus limites de tokens desaparecerão.
Sempre crie um arquivo equivalente ao .gitignore para a IA (ex: .cursorignore) e adicione:

node_modules/

dist/, build/, out/

.env, arquivos de chaves e secrets

coverage/

Arquivos estáticos pesados (imagens, vídeos).

4.7. Otimize os Tokens de Saída (Output Tokens)
Tokens gerados pela IA custam de 2 a 3 vezes mais que tokens enviados. Obrigue a IA a ser concisa na resposta adicionando restrições de formato no prompt:

"Responda apenas com o código modificado."

"Use formato de checklist sem parágrafos introdutórios."

"Não explique o código gerado."

4.8. Mantenha o código modular (Melhora o RAG e reduz custo)
Modelos de IA têm dificuldade em ler e modificar arquivos gigantescos (ex: mais de 1000 linhas) e gastam muitos tokens para reescrevê-los.
Divida responsabilidades em arquivos menores e funções delimitadas. Quanto menor o arquivo, menos contexto precisa ser enviado, reduzindo drasticamente o custo por interação.

5. Quando usar cada tipo de ferramenta
5.1. Modelo avançado / modo de alta inteligência
Use quando o problema envolver:

múltiplos arquivos com dependências entre si;

bugs difíceis de reproduzir;

arquitetura;

segurança;

performance;

integrações externas;

refatoração arriscada;

revisão de código importante;

análise de trade-offs.

Não use esse modo como autocomplete.

5.2. Modelo intermediário ou mini
Use para:

implementar tarefas bem especificadas;

revisar arquivos pequenos;

gerar testes simples;

criar funções utilitárias;

transformar requisitos em checklist;

analisar mensagens de erro;

escrever scripts;

criar documentação técnica curta.

5.3. Autocomplete de IA
Use para:

completar linhas;

sugerir nomes;

escrever funções pequenas;

gerar blocos repetitivos;

completar imports;

acelerar código que você já sabe escrever.

O autocomplete não deve decidir arquitetura.

5.4. Agente gratuito ou secundário
Use para:

projeto pessoal;

protótipos;

boilerplate;

tarefas de baixo risco;

execução de plano feito por modelo melhor;

componentes simples;

pequenas correções.

Sempre revise o resultado antes de aceitar.

6. Fluxo recomendado para tarefa profissional
Etapa 1: Entender manualmente a demanda
Antes de chamar o agente, identifique:

objetivo da tarefa;

arquivos prováveis;

regras de negócio;

risco de regressão;

testes necessários.

Etapa 2: Pedir plano ao modelo forte
Prompt sugerido:

Plaintext
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
Etapa 3: Criar um Checkpoint de Segurança (Git)
Antes de deixar a IA editar arquivos (especialmente de forma autônoma), faça um commit temporário:

Bash
git commit -am "chore: wip antes da IA"
Se o agente mais barato produzir um código caótico ou modificar arquivos errados na próxima etapa, basta um git reset --hard para abortar, poupando tempo de reversão manual.

Etapa 4: Executar com modelo barato ou manualmente
Prompt sugerido:

Plaintext
Implemente apenas a etapa 1 do plano.
Faça o menor diff possível.
Responda apenas com o código modificado.
Não altere arquitetura, nomes ou estilo fora do necessário.
Não modifique arquivos não relacionados.
Etapa 5: Revisar o diff
Use:

Bash
git diff
Depois envie ao modelo forte:

Plaintext
Revise este diff.
Aponte apenas problemas reais.
Não sugira melhorias cosméticas.
Classifique cada ponto como:
- bloqueante;
- importante;
- opcional.
Etapa 6: Testar
O agente pode sugerir testes, mas a responsabilidade final é do desenvolvedor.

Checklist mínimo:

build passa;

lint passa;

testes existentes passam;

fluxo principal funciona manualmente;

erros previsíveis foram testados;

não houve alteração colateral em arquivos irrelevantes.

7. Fluxo recomendado para projeto pessoal
Projetos pessoais toleram mais experimentação, mas ainda exigem controle.

Estratégia
Use agente gratuito para implementar rápido.

Use autocomplete para acelerar trechos óbvios.

Use modelo intermediário para organizar tarefas.

Use modelo forte apenas quando houver bloqueio real.

Faça revisão final por diff antes de consolidar mudanças.

Prompt útil:

Plaintext
Estou em um projeto pessoal.
Priorize velocidade, mas não invente arquitetura complexa.
Implemente a solução mais simples que funcione.
Antes de alterar muitos arquivos, proponha um plano curto.
8. Prompts reutilizáveis
8.1. Planejamento
Plaintext
Analise somente os arquivos selecionados.
Não implemente nada.
Crie um plano curto com:
- objetivo;
- arquivos a alterar;
- ordem das alterações;
- riscos;
- testes mínimos.
Formate a resposta estritamente em tópicos usando Markdown. Se faltar contexto, peça apenas o arquivo específico necessário e não gere suposições.
8.2. Implementação restrita
Plaintext
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
8.3. Revisão de diff
Plaintext
Revise este diff como code reviewer.
Procure apenas:
- bugs;
- quebras de contrato;
- falhas de segurança;
- regressões;
- problemas de runtime;
- testes faltantes relevantes.
Ignore estilo e preferências pessoais. Formate como uma checklist objetiva.
8.4. Debugging
Plaintext
Ajude a investigar este bug.
Não proponha solução ainda.
Primeiro liste as hipóteses mais prováveis, em ordem.
Depois diga quais evidências devo coletar para confirmar ou eliminar cada hipótese.
8.5. Refactor controlado
Plaintext
Quero refatorar este trecho sem alterar comportamento.
Antes de editar, identifique:
- comportamento atual;
- riscos de regressão;
- testes que protegem a mudança;
- menor sequência segura de alteração.
Não implemente até o plano estar claro.
8.6. Testes
Plaintext
Gere testes para este código.
Cubra apenas:
- caminho feliz;
- erro mais provável;
- edge case relevante.
Não gere testes redundantes nem casos artificiais.
Responda com o código do teste diretamente.
8.7. Controle de contexto
Plaintext
Não leia o projeto inteiro.
Use apenas o contexto fornecido.
Se precisar de outro arquivo, diga exatamente qual arquivo precisa e por quê.
Não continue sem esse contexto.
9. Checklist antes de chamar um agente caro
Antes de usar modelo avançado, responda:

A tarefa exige raciocínio complexo?

Há risco real de quebrar algo importante?

Eu selecionei os arquivos relevantes?

O prompt está específico?

Eu proibi refactor oportunista?

Eu pedi plano antes de implementação?

Eu posso usar um modelo menor para executar?

A sessão atual está curta o bastante?

O agente precisa mesmo editar arquivos ou apenas orientar?

Se a maioria das respostas for “não”, provavelmente não vale usar o modelo caro.

10. Checklist depois de aceitar código gerado por IA
Depois que o agente alterar código:

leia o diff;

verifique se não houve alteração fora do escopo;

confira imports e dependências;

rode build;

rode testes;

teste manualmente o fluxo principal;

procure tratamento de erro ausente;

verifique logs sensíveis;

confira se não foram expostos secrets;

garanta que o código segue o padrão do projeto;

remova comentários inúteis gerados pela IA.

11. Sinais de mau uso de agentes
Você provavelmente está desperdiçando tokens quando:

pede para o agente “analisar tudo” sem necessidade;

deixa o agente decidir sozinho onde mexer;

usa modo avançado para tarefas triviais;

mantém duas sessões caras em paralelo;

aceita grandes diffs sem revisar;

usa a mesma thread por muitas horas;

pede explicações longas para tarefas simples;

permite refactor oportunista;

não separa planejamento de execução;

usa IA para código que você nem chegou a ler.

12. Sinais de bom uso de agentes
Você está usando bem quando:

o agente recebe contexto pequeno e relevante;

cada tarefa gera diff pequeno;

modelos fortes são usados para raciocínio, não digitação;

modelos baratos executam tarefas mecânicas;

você faz checkpoints no Git antes de execuções automatizadas;

você revisa o diff antes de aceitar;

cada prompt tem restrições claras e pede objetividade (poucos output tokens);

o agente pede arquivos específicos, não o projeto inteiro;

sessões longas são substituídas por resumos curtos;

decisões importantes continuam sendo suas.

13. Arquivo auxiliar recomendado no projeto
Crie um arquivo AI_WORKFLOW.md na raiz do projeto com informações fixas para reduzir repetição de contexto.

Exemplo:

Markdown
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
Dica: Fornecer 1 exemplo de código bem escrito ajuda a IA a imitar o padrão. É muito mais barato em tokens a IA copiar um padrão de código existente do que tentar interpretar longas regras textuais sobre a arquitetura (Few-Shot Prompting).


Esse arquivo pode ser colado ou referenciado no início de sessões novas, evitando que o agente redescubra padrões básicos do projeto.

---

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

## 15. Regra final

A IA deve acelerar o desenvolvimento, não sequestrar o processo técnico.

O melhor uso não é deixar o agente “codar tudo”. O melhor uso é manter o desenvolvedor no controle do escopo, da arquitetura, dos riscos e da validação, usando a IA para reduzir esforço operacional e ampliar capacidade de análise.

> **Controle o contexto. Controle o diff. Controle o custo.**
"""

with open("ai-agent-guidelines-v2.md", "w") as f:
    f.write(content)

print("File generated successfully.")

Seu arquivo MD (Markdown) está pronto!
MD icon
 ai-agent-g...delines-v2 
MD

O arquivo atualizado, ai-agent-guidelines-v2.md, agora inclui todas as melhorias que discutimos, totalmente integradas com o tom direto e pragmático original.

Aqui estão os principais pontos que adicionei ao documento:

Nova Seção 4.6 (Arquivos de "Ignore"): Incluí a orientação para criar um arquivo .cursorignore ou .copilotignore e bloquear de cara pastas como node_modules/, dist/ e arquivos .env, evitando o desperdício de embeddings na leitura cega pelo agente.

Nova Seção 4.7 (Otimização de Output Tokens): Adicionada a instrução de limitar a verbosidade do retorno da IA com comandos como "Não explique o código", visto que tokens de geração são sempre os mais caros.

Nova Seção 4.8 (Código Modular): Incluí a recomendação de quebrar componentes em arquivos curtos não apenas por "boas práticas de dev", mas porque arquivos pequenos reduzem o contexto na reescrita e otimizam o RAG (Recuperação Aumentada por Geração).

Atualização no Fluxo Profissional (Etapa 3): Coloquei o comando git commit -am "chore: wip antes da IA" antes da execução de um agente mais barato. Assim você garante um botão rápido de reset caso o bot alucine em arquivos não relacionados.

Atualização nos Prompts (Seção 8): Ajustei os exemplos de Planejamento e Implementação para amarrarem a formatação diretamente ao uso do Markdown sem suposições ("Formate a resposta estritamente em tópicos usando Markdown").

Atualização do AI_WORKFLOW.md (Seção 13): Adicionei o recurso prático de colocar um trecho de código padrão usando Few-Shot Prompting, explicando que a IA imita padrões estruturais lendo muito menos tokens do que interpretando parágrafos de texto explicativo.

Dê uma conferida no arquivo gerado! Se quiser, podemos fazer novos ajustes na redação ou incorporar mais algum conceito técnico que você prefira.




Gemini is AI and can make mistakes.

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
```

Esse arquivo pode ser colado ou referenciado no início de sessões novas, evitando que o agente redescubra padrões básicos do projeto.

---

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

## 15. Regra final

A IA deve acelerar o desenvolvimento, não sequestrar o processo técnico.

O melhor uso não é deixar o agente “codar tudo”. O melhor uso é manter o desenvolvedor no controle do escopo, da arquitetura, dos riscos e da validação, usando a IA para reduzir esforço operacional e ampliar capacidade de análise.

> **Controle o contexto. Controle o diff. Controle o custo.**
