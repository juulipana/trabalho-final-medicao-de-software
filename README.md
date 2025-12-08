# Análise Comparativa de Gerenciadores de Estado em Flutter com Foco na Incidência de Antipattern

## 1. Identificação Básica

### 1.1 Título do Experimento

**Análise Comparativa de Gerenciadores de Estado em Flutter com Foco na Incidência de Antipattern**

### 1.2 ID / Código

**EXP-FLT-ANTIPATTERNS-001**

### 1.3 Versão do Documento e Histórico de Revisão

* **v1.1** — Documento inicial criado + GQM.
* **v1.2** — Escopo, Objetivo, Stakeholders/Impacto, Riscos de alto nível, premissas e critérios de sucesso.
* **v1.3** — Modelo conceitual e hipóteses; Variáveis, fatores, tratamentos e objetos de estudo; Desenho experimental.
* **v1.4** — Ajustes metodológicos para garantir que todas as métricas quantitativas sejam obtidas via script automatizado.

### 1.4 Datas

* **Criação:** 21/11/2025
* **Última atualização:** 08/12/2025

### 1.5 Autores

* **Nome:** *Juliana Parreiras Guimarães da Cunha*
* **Área:** Engenharia de Software / Flutter
* **Contato:** *[julicunha04@gmail.com](mailto:julicunha04@gmail.com) - (31) 9 7171-2627*

### 1.6 Responsável Principal (PI)

* **Nome:** *Juliana Parreiras Guimarães da Cunha*
* **Papel:** Condutora do estudo

### 1.7 Projeto / Produto Relacionado

Esta pesquisa faz parte do estudo de conclusão de curso de Engenharia de Software voltado à avaliação da qualidade de código em projetos Flutter.

---

## 2. Contexto e Problema

### 2.1 Descrição do Problema / Oportunidade

Um antipadrão é uma solução comumente adotada que acaba gerando mais problemas do que benefícios. Enquanto os padrões de projeto ajudam a organizar o código de forma eficiente, os antipadrões acontecem quando adotamos soluções rápidas ou convenientes demais, que deixam o sistema confuso, frágil ou difícil de manter a longo prazo.

No Flutter, o gerenciamento de estado é responsável por controlar mudanças nos dados e atualizar a interface gráfica. Como o estado varia ao longo do tempo, o gerenciador precisa indicar quais partes da interface devem ser reconstruídas, evitando processamento desnecessário. Isso pode ser feito com `setState` ou com ferramentas mais completas, como Provider, MobX, Bloc e Cubit.

No artigo *"State management patterns and their potential drawbacks"*, Manuel Plavsic destaca vários antipadrões comuns em gerenciamento de estado de aplicações mobile, como *prop drilling*, uso inadequado de `InheritedWidget` e Provider, e problemas com *fallback providers* e *fallback values*, entre outros.

Esses problemas mostram que a forma como o estado é estruturado afeta diretamente a qualidade e a manutenção do código. Cada gerenciador de estado organiza a aplicação de maneira diferente e pode, dependendo do uso, facilitar ou evitar antipadrões. Porém, ainda não há consenso sobre qual abordagem gera mais antipadrões a longo prazo, pois isso depende do contexto e de como cada ferramenta é aplicada no projeto.

Com isso, concluímos que o **problema** está na falta de clareza sobre como diferentes gerenciadores de estado em Flutter influenciam o surgimento de antipadrões em projetos reais, o que abre uma **oportunidade de estudo em analisar, comparar e compreender como abordagens como Bloc e MobX podem reduzir, intensificar ou transformar esses antipadrões ao longo do desenvolvimento.**

### 2.2 Contexto Organizacional e Técnico

A análise técnica utilizará um script de análise estática, responsável por extrair automaticamente todas as métricas quantitativas (acoplamento, complexidade, LOC, dependências, número de rebuilds detectáveis, entre outras). A análise manual será restrita apenas à validação de antipadrões que não puderem ser classificados pelo script.

### 2.3 Trabalhos e Evidências Prévias

* *"State management patterns and their potential drawbacks"*, Manuel Plavsic (2023).
* *"The Power of Structural Design Patterns in Flutter: Your Ultimate Guide to Building Efficient Apps"*, Mosab Youssef (2024)

### 2.4 Referencial Teórico e Empírico Essencial

* Estudos de antipadrões, incluindo exemplos relevantes ao desenvolvimento mobile, como *prop drilling*, uso inadequado de Providers, global state excessivo e estruturas difíceis de manter.
* Princípios de gerenciamento de estado em Flutter, considerando desde abordagens simples com `setState` até ferramentas mais estruturadas, como Provider, Riverpod, Bloc, Cubit e MobX.
* Modelos de qualidade de software, com foco em manutenibilidade, modularidade e complexidade, e como essas dimensões são afetadas pelas escolhas de gerenciamento de estado.

---

## 3. Objetivos e Questões de Pesquisa (GQM)

### 3.1 Objetivo Geral

Avaliar como diferentes gerenciadores de estado em Flutter influenciam a ocorrência de antipadrões em projetos reais, com foco na comparação entre Bloc e MobX.

### 3.2 Objetivos Específicos

1. Identificar e catalogar os antipadrões relacionados ao gerenciamento de estado presentes em projetos Flutter que utilizam Bloc e MobX.
2. Comparar Bloc e MobX quanto à incidência, diversidade e severidade dos antipadrões identificados.
3. Avaliar como acoplamento, complexidade, modularização e tamanho dos módulos se relacionam com os antipadrões encontrados em cada gerenciador.
4. Examinar a relação entre antipadrões e comportamentos de performance.
5. Propor recomendações práticas para mitigação de antipadrões, baseadas nas evidências observadas nos projetos Bloc e MobX analisados.

### 3.3 Questões de Pesquisa

1. Quais são os antipadrões mais recorrentes em projetos Flutter relacionados ao gerenciamento de estado?
2. Como os gerenciadores Bloc e MobX estruturam o fluxo de estado e quais diferenças essa estrutura gera na manutenção do código?
3. Em que situações os antipadrões surgem com mais frequência ao utilizar Bloc?
4. Em que situações os antipadrões surgem com mais frequência ao utilizar MobX?
5. Como Bloc e MobX se comparam quanto à quantidade, tipo e impacto dos antipadrões identificados em projetos reais?
6. Quais práticas podem reduzir o surgimento de antipadrões ao utilizar Bloc ou MobX em aplicações Flutter?

### 3.4 Métricas (GQM)

| RQ       | Questão de Pesquisa                                                                                                    | Métricas (todas obtidas por análise estática)                                                                                                                          |
| -------- | ---------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **RQ1**  | Quais são os antipadrões mais recorrentes em projetos Flutter relacionados ao gerenciamento de estado?                 | • Frequência de cada antipadrão por projeto • Nº total de antipadrões por grupo                                                                                        |
| **RQ2**  | Como Bloc e MobX estruturam o fluxo de estado e que diferenças essa estrutura gera no código?                          | • Nº de arquivos por fluxo de estado • Profundidade de diretórios • Grau de acoplamento (imports diretos) • Complexidade média dos módulos                             |
| **RQ3**  | Em que situações os antipadrões surgem com mais frequência ao utilizar Bloc?                                           | • Nº de antipadrões por módulo Bloc • Ocorrências por tipo de arquivo (event/state/bloc/widget)                                                                        |
| **RQ4**  | Em que situações os antipadrões surgem com mais frequência ao utilizar MobX?                                           | • Nº de antipadrões por módulo MobX • Ocorrências por tipo de arquivo (store/actions/reactions/widget)                                                                 |
| **RQ5**  | Como Bloc e MobX se comparam quanto à quantidade, tipo e impacto dos antipadrões identificados?                        | • Distribuição percentual por tipo • Severidade estática (baixa/média/alta)                                                                                            |
| **RQ6**  | Quais práticas podem reduzir o surgimento de antipadrões ao utilizar Bloc ou MobX?                                     | • Relação entre presença de boas práticas (extração de widgets, uso de select(), modularização) e redução de antipadrões                                               |
| **RQ7**  | Como decisões de modularização influenciam o surgimento de antipadrões?                                                | • Nº de módulos/pacotes • Tamanho médio dos módulos (LOC) • Antipadrões por módulo                                                                                     |
| **RQ8**  | Quais diferenças aparecem na navegação e compreensão do código entre projetos Bloc e MobX?                             | • Nº de passos entre arquivos (grafo de imports) • Nº de arquivos necessários para localizar estados/ações                                                             |
| **RQ10** | Quais antipadrões estão associados a problemas potenciais de performance?                                              | • Tamanho de widgets dentro de `BlocBuilder`/`Observer` • Falta de `const` • Nº de reações (MobX) • Tamanho de árvores reativas — *proxies de rebuilds desnecessários* |
| **RQ11** | Quais características arquiteturais estão mais correlacionadas com antipadrões?                                        | • Nº de dependências cruzadas • Complexidade ciclomática • Profundidade de camadas • Imports circulares                                                                |
| **RQ12** | Como diferentes ferramentas de análise estática diferem na detecção de antipadrões entre Bloc e MobX?                  | • Nº de regras aplicadas por ferramenta • Diferença entre antipadrões detectados • Nº de falsos positivos/negativos estimáveis por padrões contraditórios              |

---

## 4. Escopo e contexto do experimento

### 4.1 Escopo funcional / de processo

O experimento abrange a análise automatizada de repositórios Flutter que utilizam Bloc ou MobX. Um script executará toda a mineração, classificação e extração de métricas (acoplamento, complexidade, tamanho, estrutura e antipadrões identificáveis via análise estática). A validação manual será aplicada apenas quando a detecção automática não for conclusiva. Não fazem parte do escopo análises manuais extensas ou avaliações subjetivas de arquitetura ou lógica de negócio.

### 4.2 Contexto do estudo (tipo de organização, projeto, experiência)
O estudo é conduzido em um contexto acadêmico, no âmbito de um projeto de pesquisa em Engenharia de Software, sem vínculo com organizações comerciais. Os repositórios avaliados são projetos públicos do GitHub, desenvolvidos por programadores de diferentes níveis de experiência e sem padronização prévia. O objetivo é observar práticas reais de desenvolvimento Flutter com Bloc e MobX, utilizando análise automatizada para garantir consistência e independência da experiência individual dos autores dos projetos.

### 4.3 Premissas
* Presume-se que os repositórios possuam estrutura de pastas compatível com análise automatizada.
* Assume-se que o script conseguirá extrair todas as métricas necessárias conforme planejado.

### 4.4 Restrições

* Tempo limitado para coleta e análise dos projetos.
* Dependência de ferramentas de análise estática disponíveis publicamente.
* Acesso restrito apenas a repositórios open-source.
* Ausência de orçamento para aquisição de ferramentas pagas.

### 4.5 Limitações previstas

* A análise manual será mínima e limitada à validação de antipadrões cuja classificação automática não for conclusiva.
* Diferenças de contexto entre os repositórios podem influenciar os resultados.
* Resultados podem não se aplicar a outros contextos, arquiteturas ou ferramentas.

## 5. Stakeholders e impacto esperado

### 5.1 Stakeholders principais
* Desenvolvedores mobile que utilizam Flutter e precisam escolher ou manter um gerenciador de estado.
* Startups e pequenas empresas que precisam tomar decisões rápidas e embasadas sobre arquitetura, evitando riscos e retrabalho.
* Engenheiros de software e arquitetos interessados em padrões, antipadrões e boas práticas de estruturação de estado.
* Pesquisadores e estudantes que estudam qualidade de código, manutenibilidade e práticas de desenvolvimento em Flutter.
* Comunidade open-source Flutter, que pode se beneficiar de evidências sobre uso e impactos dos principais gerenciadores de estado.

### 5.2 Interesses e expectativas dos stakeholders
* **Desenvolvedores mobile:**
  * Entender qual gerenciador de estado tende a gerar menos antipadrões.
  * Obter dicas para melhorar qualidade e manutenção do código.

* **Startups e pequenas empresas:**
  * Diminuir riscos técnicos ao escolher um gerenciador de estado.
  * Ajudar em decisões arquiteturais com base em evidências.

* **Engenheiros de software e arquitetos:**
  * Identificar impactos dos gerenciadores Bloc e MobX na arquitetura geral.
  * Validar boas práticas e evidenciar problemas recorrentes de projeto.

* **Pesquisadores e estudantes:**
  * Obter dados para estudos sobre qualidade de software e engenharia Flutter.
  * Aprofundar o entendimento sobre antipadrões em projetos reais.

* **Líderes técnicos e gestores:**
  * Tomar decisões de padrão arquitetural com evidências reais.
  * Reduzir retrabalho e garantir qualidade de entrega das equipes.

* **Comunidade open-source Flutter:**
  * Análises que ajudem a evoluir práticas coletivas.
  * Identificar pontos fracos comuns em projetos públicos.

### 5.3 Impactos potenciais no processo / produto

* Impacto positivo na qualidade futura de projetos Flutter, ao levantar antipadrões comuns.
* Insights que podem influenciar escolhas arquiteturais em novos produtos.
* Ajuda a ajustar prazos de projetos em andamento com base em dados.
* Melhora na documentação e na tomada de decisão técnica a partir dos resultados obtidos em projetos reais.

## 6. Riscos de alto nível, premissas e critérios de sucesso

### 6.1 Riscos de alto nível

**Correção em um risco:**

* Indisponibilidade dos repositórios open-source selecionados.
* Atrasos na análise devido à complexidade maior do que o previsto.
* Diferenças estruturais entre os projetos que prejudiquem comparações justas.
 
### 6.2 Critérios de sucesso globais (go / no-go)

**Go (seguir com o experimento / aplicar recomendações):**
* Métricas extraídas **formalmente pelo script** com consistência reprodutível.
* Identificação e quantificação de antipadrões suficientes para permitir comparação.
* Métricas principais (acoplamento, complexidade, modularização) calculadas de forma consistente e reproduzível.
**No-Go (parar / não prosseguir com mudanças):**
* Incapacidade de encontrar repositórios comparáveis ou remoção/indisponibilidade dos mesmos.
* Falha persistente das ferramentas de análise ou impossibilidade técnica de extrair métricas confiáveis.
* Número de ocorrências de antipadrões insuficiente para análise estatística significativa.

### 6.3 Critérios de parada antecipada (pré-execução)
* Impossibilidade do script extrair métricas fundamentais (CBO, complexidade, LOC, detecção inicial de antipadrões).

---

# 7. Modelo Conceitual e Hipóteses

## **7.1 Modelo conceitual do experimento**

O experimento parte da premissa de que o gerenciador de estado utilizado (Bloc ou MobX) influencia diretamente:

* **A incidência de antipadrões** em diferentes partes do código.
* **A modularização e o acoplamento** entre componentes.
* **A manutenibilidade percebida** (incluindo esforço para navegação e compreensão).
* **A ocorrência de problemas de performance**, como rebuilds desnecessários.
* **A previsibilidade do fluxo de estado** (impactando complexidade e clareza arquitetural).

Modelo conceitual resumido:

```
Gerenciador de Estado (Bloc vs. MobX)
            ↓ influencia
Estrutura do Fluxo de Estado e Arquitetura Interna
            ↓ influencia
Métricas de Qualidade e Ocorrência de Antipadrões
            ↓ influencia
Manutenibilidade e Complexidade do Código
            ↓ influencia
Desempenho percebido e problemas correlatos
```

* **Bloc**, por ser mais prescritivo e baseado em eventos/estados explícitos, tende a **reduzir antipadrões relacionados à imprevisibilidade**, mas pode **aumentar complexidade estrutural e boilerplate**, gerando antipadrões como *inflated states* ou *eventos excessivos*.

* **MobX**, por adotar reatividade implícita, tende a permitir **maior agilidade e concisão**, mas pode **aumentar acoplamento e dependências invisíveis**, gerando antipadrões como *reactions ocultas*, *rebuilds inesperados* e *global stores centrais*.

---

## **7.2 Hipóteses formais (H0 e H1)**

As hipóteses abaixo foram formuladas para as **questões principais**, isto é, aquelas diretamente relacionadas à comparação Bloc vs. MobX.

### **H1 – Ocorrência geral de antipadrões**

* **H0₁:** Não há diferença significativa na quantidade de antipadrões entre projetos que utilizam Bloc e MobX.
* **H1₁:** Projetos que utilizam MobX apresentam maior quantidade de antipadrões que projetos que utilizam Bloc.

### **H2 – Acoplamento e modularização**

* **H0₂:** Não há diferença significativa no acoplamento entre módulos em projetos com Bloc e MobX.
* **H1₂:** Projetos com MobX apresentam maior acoplamento entre módulos do que projetos com Bloc.

### **H3 – Complexidade do fluxo de estado**

* **H0₃:** Bloc e MobX apresentam complexidade média de fluxo de estado equivalente.
* **H1₃:** O Bloc apresenta maior complexidade estrutural (mais arquivos, mais camadas) do que o MobX.

### **H4 – Rebuilds desnecessários**

* **H0₄:** A frequência de rebuilds desnecessários é igual entre Bloc e MobX.
* **H1₄:** O MobX apresenta maior quantidade de rebuilds desnecessários.

### **H5 – Esforço cognitivo para navegação**

* **H0₅:** A facilidade de navegação e compreensão do código é igual em ambos os gerenciadores.
* **H1₅:** Projetos com MobX exigem maior esforço de navegação devido ao acoplamento implícito.

### **H6 – Severidade dos antipadrões**

* **H0₆:** A severidade dos antipadrões é equivalente entre Bloc e MobX.
* **H1₆:** Antipadrões encontrados em projetos MobX têm maior severidade e impacto arquitetural.

---

## **7.3 Nível de significância e considerações de poder**

* **Nível de significância adotado: α = 0,05.**
* Considerações:

  * A amostra é **muito pequena** (apenas dois grandes repositórios).
  * O poder estatístico formal (>= 80%) **não poderá ser garantido** devido ao N reduzido.
  * A análise será predominantemente **descritiva e exploratória**, com suporte de testes estatísticos apenas onde fizer sentido.
  * A confiabilidade será reforçada por:

    * triangulação de métricas diferentes,
    * rastreabilidade clara dos antipadrões,
    * análise manual complementar,
    * replicabilidade dos cálculos.
---

# 8. Variáveis, fatores, tratamentos e objetos de estudo

## 8.1 Objetos de estudo
Os objetos de estudo desta pesquisa são (1) o gerenciador de estado adotado pelos repositórios analisados e (2) os artefatos produzidos durante esse processo, ou seja, o código-fonte.

## 8.2 Sujeitos / participantes

Esta pesquisa não envolve participantes humanos. Os “sujeitos” analisados são exclusivamente repositórios públicos de código-fonte Flutter que utilizam os gerenciadores de estado MobX ou Bloc. Todas as análises serão feitas apenas sobre esses repositórios, sem interação com desenvolvedores ou coleta de dados pessoais.

## 8.3 Variáveis independentes
| Fator                     | Descrição                    | Níveis                            |
| ------------------------- | ---------------------------- | --------------------------------- |
| **Gerenciador de estado** | Tecnologia analisada         | *Bloc*, *MobX*                    |
| **Módulo analisado**      | Parte do sistema             | múltiplos módulos por repositório |
| **Tipo de antipadrão**    | Categoria segundo literatura | ~10 categorias predefinidas       |

Variável primária: **Gerenciador de estado**
Variáveis secundárias: **módulo**, **tipo de antipadrão**.

---

## **8.4 Tratamentos (condições experimentais)**

O experimento terá **duas condições principais**:

### **T1 – Projeto com Bloc**

* Código estruturado com eventos, estados e blocos.
* Fluxo de estado explicitamente definido.

### **T2 – Projeto com MobX**

* Código estruturado com observables, actions e reações.
* Fluxo de estado mais implícito e reativo.

Não haverá grupo controle, pois é um projeto experimental comparativo.

---
## 8.5 Variáveis dependentes
* **Número total de antipadrões por módulo**
* **Classificação de severidade dos antipadrões**
* **CBO (acoplamento entre objetos)**
* **Complexidade ciclomática média por módulo**
* **Número de rebuilds desnecessários detectados**
* **Tamanho dos módulos (LOC, nº de arquivos)**
* **Número de passos de navegação entre arquivos**


## **8.6 Variáveis de controle / bloqueio**
* **Tamanho do projeto** (LOC e número de arquivos)
* **Tipo de aplicação** (evitar comparar apps totalmente diferentes em propósito)
* **Versão mínima do Flutter analisada**
* **Ferramentas de análise estática usadas**
* **Tipo de arquitetura base** (ex.: evitar comparar projetos com Clean Architecture complexa vs. projetos simples)
* **Ambiente de execução** (mesma versão do SDK)

## 8.7 Variáveis de confusão

* Diferença na experiência dos contribuidores originais dos repositórios.
* Diferenças arquiteturais não relacionadas ao gerenciador de estado.
* O projeto MobX ou Bloc pode ter mais funcionalidades, aumentando LOC.
* O script ajuda a evitar erros na coleta e classificação dos dados, mas ainda podem existir diferenças entre os projetos que fogem do nosso controle e podem influenciar os resultados.

---

# 9. Desenho Experimental

## **9.1 Tipo de desenho**

Este estudo adota um desenho observacional e comparativo, baseado em análises automatizadas de código-fonte. Não há intervenções nos repositórios, o objetivo é observar e comparar como projetos Flutter que utilizam MobX ou Bloc apresentam diferenças estruturais e ocorrência de antipadrões. Trata-se, portanto, de um desenho não experimental, onde os grupos (MobX e Bloc) são analisados tal como se encontram.

## **9.2 Randomização e alocação**

Neste estudo não há randomização, pois não existem sujeitos nem tarefas a serem sorteados. A alocação dos repositórios é feita automaticamente pelo script, que identifica o gerenciador de estado usado (MobX ou Bloc) e classifica cada projeto no grupo correspondente.

## 9.3 Balanceamento

O balanceamento é garantido selecionando repositórios com características mínimas semelhantes, evitando grupos muito diferentes entre si.

## 9.4 Número de grupos e sessões

Serão dois grupos: repositórios que usam MobX e repositórios que usam Bloc. Cada repositório passa por uma única rodada de análise, executada automaticamente pelo script. Isso é suficiente porque o estudo é observacional: o código não muda entre rodadas, então repetir a análise não traria novos dados.

# **10. População, sujeitos e amostragem**

## **10.1 População-alvo**

A população-alvo inclui:

1. **Projetos Flutter open-source** que utilizam predominantemente:

   * Bloc
   * MobX

2. **Módulos internos desses repositórios**, como:

   * stores, blocs, estados, eventos,
   * widgets consumidores de estado,
   * camadas de aplicação (domain, presentation, data),
   * componentes altamente afetados por fluxos de estado.

---

## **10.2 Critérios de inclusão de sujeitos (projetos / participantes)**

Repositórios Flutter open-source disponíveis no GitHub ou plataformas similares, que utilizem predominantemente Bloc ou MobX, possuam alto número de estrelas e não misturem de forma significativa múltiplos gerenciadores de estado.

---

## **10.3 Critérios de exclusão**

Projetos que misturam diversos gerenciadores de estado simultaneamente, repositórios muito pequenos (com menos de cinco módulos ou menos de 3.000 linhas de código) e repositórios com poucas estrelas.

---

## **10.4 Tamanho da amostra planejado**

O estudo pretende analisar aproximadamente 20 a 30 repositórios em cada grupo (MobX e Bloc), totalizando de 40 a 60 projetos. Esse tamanho é suficiente para garantir variabilidade estrutural, detectar padrões recorrentes e manter o processamento viável dentro dos recursos disponíveis. Além disso, o volume proposto oferece poder analítico adequado para comparar a presença de antipadrões entre os dois grupos.

---

## **10.5 Método de seleção / recrutamento**

**Projetos:**
Seleção sistemática através de busca no GitHub utilizando filtros como:

* linguagem: Dart,
* framework: Flutter,
* tecnologias: Bloc / MobX,
* ordenação por número de estrelas.
---

## **10.6 Treinamento e preparação dos sujeitos**

Como se tratam de projetos, não será feito nenhum de treinamento ou preparação dos sujeitos. Os pré-requisitos serão satisfeitos através de uma análise mais específica dos códigos dos repositórios analisados, que determinará o escopo do projeto.

---

# **11. Instrumentação e protocolo operacional**

## **11.1 Instrumentos de coleta**

Serão utilizadas ferramentas de análise estática, incluindo dart_code_metrics para métricas como complexidade ciclomática, acoplamento e detecção de antipadrões, SonarQube (Community Edition) quando aplicável para identificação de code smells, e scripts personalizados em Python ou Dart para extrair métricas específicas, como número de rebuilds, módulos e dependências.-Também será usado o GitHub API para coleta de informações do repositório.

---

## **11.2 Materiais de suporte**

Serão utilizados um documento padronizado de checklist de antipadrões baseado na literatura, planilhas para coleta de métricas como CBO, complexidade, LOC e estrutura de módulos, um roteiro curto para desenvolvedores no estudo cognitivo, scripts automatizados de coleta de dados e uma lista de commits e releases dos projetos para contextualização.

---

## **11.3 Procedimento experimental**

<img width="1024" height="768" alt="Process of Creative Thinking Flowchart Graph" src="https://github.com/user-attachments/assets/817ba352-3f25-4010-a499-eceac5366b9d" />

### **Passo 1 – Seleção final dos repositórios**

* Verificar tamanho comparável (LOC, nº arquivos, nº módulos).
* Garantir dominância do gerenciador de estado (Bloc ou MobX).

### **Passo 2 – Caracterização inicial**

* Extração inicial de:

  * número de módulos,
  * número de camadas,
  * LOC total,
  * número de widgets dependentes de estado.

### **Passo 3 – Execução das métricas estáticas**

* Rodar ferramentas em todo o repositório.
* Registrar:

  * CBO,
  * complexidade por módulo,
  * LCOM (coesão),
  * dependências entre módulos,
  * tamanho das stores/blocs.

### **Passo 4 – Identificação de antipadrões**

A partir de:

1. Regras automatizadas detectadas pelas ferramentas.
2. Checklist manual baseado em literatura (prop drilling, global store excessivo, acoplamento implícito etc.).

### **Passo 5 – Classificação da severidade**

Cada ocorrência recebe:
**Baixa**, **Média**, **Alta** (conforme impacto arquitetural).

### **Passo 6 – Comparação entre Bloc e MobX**

* Comparativo módulo a módulo.
* Comparativo global (por projeto).
* Análise descritiva e visualização (percentuais, gráficos).

### **Passo 7 – Síntese dos resultados**

* Consolidação dos achados frente às hipóteses H0/H1.
* Recomendação de boas práticas.

---

## **11.4 Plano de piloto**

Antes da coleta real, o pipeline será executado em um repositório pequeno (como um exemplo em Flutter com Bloc ou MobX) pra validar a execução das ferramentas, a confiabilidade das métricas, o tempo médio do processo e a clareza do checklist de antipadrões. Com base nessa validação, scripts e planilhas serão ajustados conforme necessário. Esse piloto assegura a consistência do processo antes da análise dos repositórios principais.

---

# **12. Plano de análise de dados**

## **12.1 Estratégia geral de análise**

A análise será comparativa, descritiva e exploratória, combinando métricas quantitativas obtidas pelas ferramentas, identificação manual de antipadrões não detectados automaticamente, cruzamentos entre variáveis como acoplamento e antipadrões, além de avaliações em nível de módulo e de projeto. Como envolve apenas dois repositórios, o objetivo não é a generalização estatística, mas sim um entendimento profundo e baseado em evidências.

---

## **12.2 Métodos estatísticos planejados**

* **Estatísticas descritivas:** média, mediana, variância, histogramas.

* **Comparações pareadas Bloc vs. MobX:**

  * diferença absoluta de métricas,
  * diferença relativa (%),
  * análise qualitativa de severidade.

* **Testes estatísticos:**
  Como o N é muito pequeno, só testes exploratórios simples podem ser levados na conta:

  * Será aplicado um teste não paramétrico para comparar as distribuições entre módulos, como o Mann-Whitney, caso haja quantidade suficiente de módulos. Também será calculada a correlação de Spearman para verificar a relação entre o acoplamento e a quantidade de antipadrões.

---

## **12.3 Tratamento de dados faltantes e outliers**

Se alguma ferramenta falhar em um módulo, ele será reprocessado manualmente. Caso surjam métricas inconsistentes, como uma complexidade muito fora da curva, o outlier será investigado para verificar se representa um caso real, sendo mantido, ou um erro da ferramenta, sendo corrigido ou removido. Já em situações de dados ausentes nas tarefas cognitivas, o participante será excluído apenas da métrica afetada.

---

## **12.4 Plano de análise para dados qualitativos**

Para antipadrões identificados manualmente ou análises narrativas, primeiro será feita uma codificação inicial por tipo, como prop drilling, acoplamento implícito ou rebuilds inesperados, seguida da classificação por severidade. Em seguida, cada antipadrão será mapeado por gerenciador de estado, indicando onde ocorre com mais frequência, por que surge e qual é seu impacto no fluxo e na modularização. Depois, os achados qualitativos serão triangulados com os quantitativos, como quando um acoplamento elevado é explicado pelo uso de global stores. Por fim, será produzida uma síntese final com recomendações práticas.

---

## Referências
* PLAVSIC, Manuel. State management patterns and their potential drawbacks. 2023. 
* YOUSSEF, Mosab. The Power of Structural Design Patterns in Flutter: Your Ultimate Guide to Building Efficient Apps. 2024.
