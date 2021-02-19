# RGBank: análise de riscos com Data Science
---
Este projeto foi proposto por nosso diretor de Estatística da ICMC Júnior, **Renan Barreto**, com o intuito de trabalhar em equipe para resolver problemas de Negócio relacionados a transações bancárias.

Por mais que seja uma situação fictícia, estava valendo a efetivação do meu parceiro de equipe, **Luís Miguel**, o qual ainda era Trainee.

# Contexto
---
A história, basicamente, era a de que um cliente nos procurava para criar uma *fintech* chamada **RGBank**, e seu objetivo principal era introduzir o serviço de **análise de riscos** para verificar a veracidade das informações, ou seja, se a transação foi fraudulenta ou legítima.

O ganho da nova empresa estaria relacionado com a assertividade de nosso modelo preditivo, com as seguintes regras de negócio:

1. **A empresa vai receber 25% do valor de cada transação detectada verdadeiramente como fraude.**
2. **A empresa vai receber 5% do valor de cada transação detectada como fraude, porém a transação é verdadeiramente legítima.**
3. **A empresa vai devolver 100% do valor para o cliente, a cada transação detectada como legítima, porém a transação é verdadeiramente uma fraude.**

No final, as seguintes perguntas relacionadas aos modelos de Machine Learning e aos valores monetários deveriam ser respondidas:
- **Qual a Precisão e Acurácia dos modelos utilizados?**
- **Qual dos modelos é o melhor e porquê?**
- **Qual o Faturamento Esperado pela Empresa, se classificarmos 100% das transações, com o melhor modelo?**
- **Qual o Prejuízo Esperado pela Empresa, se classificarmos 100% das transações, em caso de falha do melhor modelo?**
- **Qual o Lucro Esperado pela empresa, se classificarmos 100% das transações, ao utilizar o melhor modelo?**

O cliente também queria uma **Análise Descritiva** dos dados.

# Divisão de tarefas:
- Eu: Pré-processamento dos Dados e Machine Learning;
- Luis: Análise Exploratória dos Dados.

# Ferramentas utilizadas
---
- Linguagem de programação Python;
- Pacotes: pandas, numpy, datetime, matplotlib, seaborn, sklearn;
- Notebook: Google Colaboratory.

# Descrição breve das etapas
---
## 1. Pré-processamento
- Criação da variável `isMerchantDest` e troca dos valores (`oldbalanceDest` e `newbalanceDest`) dos comerciantes pela mediana dos não comerciantes;
- Destrinchamento da variável `step` em `hour` e `day`.

## 2. Análise Exploratória dos Dados
Algumas visualizações que obtivemos estão abaixo:
![](https://github.com/Emersonmiady/rg-bank/blob/main/img/montant.png?raw=true)
![](https://github.com/Emersonmiady/rg-bank/blob/main/img/fraud_hour.png?raw=true)
![](https://github.com/Emersonmiady/rg-bank/blob/main/img/fraud_day.png?raw=true)



## 3. Preparando para o ML
Transformei as variáveis categóricas relevantes em *dummies*, depois dividi em 0.2 de teste e apliquei o `StandardScaler()` para a padronização dos dados, já que ultilizaríamos um modelo de Regressão Logística para a comparação de modelos.

## 4. Machine Learning: modelos testados
Foram testados:
- Naive-Bayes;
- Regressão Logística;
- Árvore de Decisão;
- Random Forest.

## 4. Resultados das métricas

![](https://github.com/Emersonmiady/rg-bank/blob/main/img/models_description.png)

O melhor modelo foi o que teve melhor Recall, pelo menos quando utilizamos as regras de negócio. Ou seja, foi a Árvore de Decisão!

## 5. Resultados de Negócio
1. "O faturamento esperado pela empresa é igual a: 3.004.400.679,40, se considerarmos 1/4 das transações em 1 mês. Entretanto, se fossemos deduzir o quanto se aumenta, para 100% das transações mensais, temos a possibilidade de encontrar 3.76x esse valor!"

2. "O prejuízo esperado pela empresa é igual a: 45.659.154,44, se considerarmos 1/4 das transações em 1 mês. Entretanto, se fossemos deduzir o quanto se aumenta, para 100% das transações mensais, temos a possibilidade de encontrar 21.19x esse valor!"

3. "O lucro esperado pela empresa é igual a: 2.958.741.524,96, se considerarmos 1/4 das transações em 1 mês. Entretanto, se fossemos deduzir o quanto se aumenta, para 100% das transações mensais, temos a possibilidade de encontrar 3.5x esse valor!"

**Observação:** não sabímos a unidade monetária!
