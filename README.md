# Análise Comparativa de Gerenciadores de Estado em Flutter com Foco na Incidência de Antipattern

## 1. Identificação Básica

### 1.1 Título do Experimento

**Análise Comparativa de Gerenciadores de Estado em Flutter com Foco na Incidência de Antipattern**

### 1.2 ID / Código

**EXP-FLT-ANTIPATTERNS-001**

### 1.3 Versão do Documento e Histórico de Revisão

* **v1.0** — Documento inicial criado + GQM.

### 1.4 Datas

* **Criação:** 21/11/2025
* **Última atualização:** 21/11/2025

### 1.5 Autores

* **Nome:** *Juliana Parreiras Guimarães da Cunha*
* **Área:** Engenharia de Software / Flutter
* **Contato:** *julicunha04@gmail.com - (31) 9 7171-2627*

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

O estudo será realizado no contexto de aplicações Flutter, utilizando projetos open-source e análises automatizadas de código. O foco está em boas práticas de arquitetura, qualidade de código, métricas estáticas e análise de antipadrões.

### **2.3 Trabalhos e Evidências Prévias**

* *"State management patterns and their potential drawbacks"*, Manuel Plavsic (2023).
* *"The Power of Structural Design Patterns in Flutter: Your Ultimate Guide to Building Efficient Apps"*, Mosab Youssef (2024)

---

### **2.4 Referencial Teórico e Empírico Essencial**

* Estudos de antipadrões, incluindo exemplos relevantes ao desenvolvimento mobile, como *prop drilling*, uso inadequado de Providers, global state excessivo e estruturas difíceis de manter.
* Princípios de gerenciamento de estado em Flutter, considerando desde abordagens simples com `setState` até ferramentas mais estruturadas, como Provider, Riverpod, Bloc, Cubit e MobX.
* Modelos de qualidade de software, com foco em manutenibilidade, modularidade e complexidade, e como essas dimensões são afetadas pelas escolhas de gerenciamento de estado.

---

## 3. Objetivos e Questões de Pesquisa (GQM)

### 3.1 Objetivo Geral

Avaliar como diferentes gerenciadores de estado em Flutter influenciam a ocorrência de antipadrões em projetos reais, com foco na comparação entre Bloc e MobX.

### 3.2 Objetivos Específicos

1. Identificar os antipadrões mais comuns relacionados ao gerenciamento de estado em aplicações Flutter.
2. Mapear como os gerenciadores Bloc e MobX estruturam o fluxo de estado e a atualização da interface.
3. Analisar a presença de antipadrões em projetos reais que utilizam Bloc e MobX.
4. Comparar os dois gerenciadores quanto à frequência, tipo e impacto dos antipadrões encontrados.
5. Avaliar como as escolhas de arquitetura e modularização influenciam o surgimento desses antipadrões em cada tipo.
6. Propor boas práticas para reduzir o surgimento de antipadrões em projetos Flutter que utilizam Bloc ou MobX.

### 3.3 Questões de Pesquisa

1. Quais são os antipadrões mais recorrentes em projetos Flutter relacionados ao gerenciamento de estado?
2. Como os gerenciadores Bloc e MobX estruturam o fluxo de estado e quais diferenças essa estrutura gera na manutenção do código?
3. Em que situações os antipadrões surgem com mais frequência ao utilizar Bloc?
4. Em que situações os antipadrões surgem com mais frequência ao utilizar MobX?
5. Como Bloc e MobX se comparam quanto à quantidade, tipo e impacto dos antipadrões identificados em projetos reais?
6. Quais práticas podem reduzir o surgimento de antipadrões ao utilizar Bloc ou MobX em aplicações Flutter?

### 3.4 Métricas Associadas (GQM)

| RQ   | Questão de Pesquisa                                                                                                                                  | Métricas Associadas                                                                            |
| ---- | ---------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------- |
| RQ1  | Quais são os antipadrões mais recorrentes em projetos Flutter relacionados ao gerenciamento de estado?                                               | • Frequência de ocorrência de cada antipadrão por projeto                                      |
| RQ2  | Como os gerenciadores Bloc e MobX estruturam o fluxo de estado e quais diferenças essa estrutura gera na manutenção do código?                       | • Nº de camadas/arquivos no fluxo de estado • Grau de acoplamento (CBO / dependências diretas) |
| RQ3  | Em que situações os antipadrões surgem com mais frequência ao utilizar Bloc?                                                                         | • Nº de antipadrões detectados por módulo com Bloc                                             |
| RQ4  | Em que situações os antipadrões surgem com mais frequência ao utilizar MobX?                                                                         | • Nº de antipadrões detectados por módulo com MobX                                             |
| RQ5  | Como Bloc e MobX se comparam quanto à quantidade, tipo e impacto dos antipadrões identificados em projetos reais?                                    | • Comparativo percentual Bloc vs. MobX • Classificação de severidade                           |
| RQ6  | Quais práticas podem reduzir o surgimento de antipadrões ao utilizar Bloc ou MobX em aplicações Flutter?                                             | • Redução percentual de antipadrões após adoção de boas práticas                               |
| RQ7  | Como as decisões de modularização influenciam o surgimento de antipadrões em aplicações Flutter que utilizam Bloc ou MobX?                           | • Nº de antipadrões por módulo • Relação entre tamanho do módulo e incidência                  |
| RQ8  | Quais diferenças aparecem no tempo de compreensão e navegação do código entre projetos que usam Bloc e MobX, considerando a presença de antipadrões? | • Nº de passos para localizar estados/ações • Tempo médio de navegação entre arquivos          |
| RQ9  | Como o nível de experiência dos desenvolvedores impacta a probabilidade de introduzir antipadrões ao usar Bloc ou MobX?                              | • Taxa de antipadrões por desenvolvedor/comit • Comparação entre níveis de experiência         |
| RQ10 | Quais antipadrões estão associados a problemas de performance em aplicações Flutter utilizando Bloc ou MobX?                                         | • Quantidade de rebuilds desnecessários • Tempo de renderização e frame drops                  |
| RQ11 | Quais características arquiteturais dos projetos estão mais correlacionadas com a formação de antipadrões nesses dois gerenciadores?                 | • Nº de dependências entre camadas • Complexidade ciclomática por módulo                       |
| RQ12 | De que forma ferramentas automatizadas de análise estática diferem na detecção de antipadrões entre projetos com Bloc e MobX?                        | • Cobertura de regras detectadas por ferramenta • Diferença de falsos positivos/negativos      |

---

## 4. Escopo e contexto do experimento

### 4.1 Escopo funcional / de processo (incluído e excluído)
Este projeto abrange a análise comparativa de dois aplicativos Flutter com tamanho de código equivalente, sendo um baseado em Bloc e outro em MobX. Serão selecionados repositórios open-source amplamente reconhecidos (medidos pelo número de estrelas no GitHub) que utilizem esses gerenciadores de estado de forma predominante.

O estudo não incluirá repositórios que utilizem outros gerenciadores de estado ou qualquer framework que não seja Flutter. Além disso, o contexto funcional das aplicações não será considerado: o foco está exclusivamente sobre características internas do código e seu tamanho, visando permitir uma comparação entre os projetos analisados.

### 4.2 Contexto do estudo (tipo de organização, projeto, experiência)
O estudo será realizado usando de grandes projetos open-source desenvolvidos em Flutter, escolhidos por sua relevância e número de estrelas. A análise focará em dois repositórios comparáveis em tamanho de código, sendo um baseado em Bloc e outro em MobX.

Não há organização ou equipe específica envolvida; os projetos analisados refletem contribuições de desenvolvedores da comunidade, com níveis variados de experiência. A criticidade do domínio das aplicações não será considerada, já que o foco está na estrutura interna do código e nas práticas de gerenciamento de estado.

### 4.3 Premissas
O estudo assume que os repositórios open-source selecionados permanecerão disponíveis durante a análise e que possuem tamanhos e complexidade comparáveis. Também se presume que as ferramentas de análise funcionarão de forma consistente ao longo de toda a pesquisa.

### 4.4 Restrições

* Tempo limitado para coleta e análise dos projetos.
* Dependência de ferramentas de análise estática disponíveis publicamente.
* Acesso restrito apenas a repositórios open-source.
* Ausência de orçamento para aquisição de ferramentas pagas.

### 4.5 Limitações previstas

* Amostra pequena (apenas dois projetos).
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

### 6.1 Riscos de alto nível (negócio, técnicos, etc.)

* Indisponibilidade dos repositórios open-source selecionados.
* Atrasos na análise devido à complexidade maior do que o previsto.
* Diferenças estruturais entre os projetos que prejudiquem comparações justas.
* Risco de resultados pouco generalizáveis por conta da amostra reduzida.
  
### 6.2 Critérios de sucesso globais (go / no-go)

**Go (seguir com o experimento / aplicar recomendações):**
* Seleção de pelo menos um repositório representativo para cada gerenciador (Bloc e MobX) com tamanho e complexidade comparáveis.
* Identificação e quantificação de antipadrões suficientes para permitir comparação (ocorrências relevantes em ambos os projetos).
* Métricas principais (acoplamento, complexidade, modularização) calculadas de forma consistente e reproduzível.
* Relatório com evidências claras que suportem recomendações práticas e mudanças arquiteturais.

**No-Go (parar / não prosseguir com mudanças):**
* Incapacidade de encontrar repositórios comparáveis ou remoção/indisponibilidade dos mesmos.
* Falha persistente das ferramentas de análise ou impossibilidade técnica de extrair métricas confiáveis.
* Número de ocorrências de antipadrões insuficiente para análise estatística significativa.

### 6.3 Critérios de parada antecipada (pré-execução)
* Impossibilidade de encontrar dois projetos open-source comparáveis em tamanho e complexidade.
* Mudanças significativas nos repositórios.

---

## Referências
* PLAVSIC, Manuel. State management patterns and their potential drawbacks. 2023. 
* YOUSSEF, Mosab. The Power of Structural Design Patterns in Flutter: Your Ultimate Guide to Building Efficient Apps. 2024. 

*O desenvolvimento desta pesquisa ainda está em andamento.*
