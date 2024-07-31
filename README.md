# 📊 Previsão de Estoque Inteligente na AWS com [SageMaker Canvas](https://aws.amazon.com/pt/sagemaker/canvas/)

### Criaçao do modelo:

- Primeiro passo foi criar minha conta dentro da AWS e entender mais a fundo como essa site funciona, explorando suas centenas de possibilidades.
- Dentro do SageMaker Canvas eu criei o meu modelo de projeto, importando uma dataset de quantidade de estoque.
- Fiz a limpesa desses dados, substituindo os falores em falta por zero e definindo que a coluna alvo da analise seria a de quantidade de estoque. Levando em consideraçao tambem os feriados do Brasil e como isso afetava.
- Treinei meu modelo com uma contruçao longa que levou cerca de 2 horas

![image](https://github.com/user-attachments/assets/0bc3c5cc-71a7-458c-819f-03d40b0927ca)

### Analise de resultados:

- 1. Avg. wQL (Weighted Quantile Loss):
   É a metrica que mede o erro entre os valores previstos pelo modelo e os valores reais, onde o objetivo é prever nao apenas um valor central, mas tambem um intervalo de confiança.
   Meu resultado obtido foi 1.006 que sugere que o modelo está fazendo previsões com qualidade muito próxima ao valor ideal.

- 2.  MAPE (Mean Absolute Percentage Error):
   Mede o erro percentual médio absoluto entre os valores previstos e os valores reais.
   Meu resultado obteve um MAPE de 0.002 que significa, em média, as previsões estão erradas em 0.2%

- 3. WAPE (Weighted Absolute Percentage Error):
   Similar ao MAPE, mas ponderado. Ele é útil quando há uma variação significativa nas magnitudes dos valores reais.
   Meu resultado obteve um WAPE de 1.004 sugere que há algum peso considerado nas previsões, mas o valor é relativamente baixo, indicando bom desempenho.

- 4. RMSE (Root Mean Square Error):
   Mede a raiz quadrada do erro médio quadrático. Ele penaliza erros maiores mais severamente do que erros menores.
   Obtive um RMSE de 3.414 significa que, em média, as previsões estão erradas em aproximadamente 3 unidades. Sugere que há algum erro médio quadrático nas previsões, mas se os valores reais e previstos estiverem próximos, isso pode indicar um bom ajuste geral.

- 5. MASE (Mean Absolute Scaled Error):
   Compara a precisão do modelo com a de um modelo ingênuo, como a média dos valores passados.
   Obtive um MASE de 0.000 que indica que o modelo está fazendo previsões com uma precisão muito alta em relação ao modelo de referência. No entanto, um valor tão baixo pode também sugerir um possível erro de cálculo ou configuração.

- 6. Os feriados nao impactaram no resutlado.
     
  7. ![image](https://github.com/user-attachments/assets/918794c6-0ac6-4e98-8207-855d519878b4)

  
### Previsão:

- 1. Muitos produtos acabaram com uma historical demand zerada, oq leva-nos a concluir que ou foi descontinuado ou precisamos reaver o controle de estoque pois ele esta acabando e nao esta sendo reposto
- 2. Os valores previstos em seu modo geral tendem a uma queda nas previsoes, o que pode ocorrer por algumas razoes, sendo elas:
     
     1. Tendência Natural de Dados:
      Se os dados históricos mostram uma tendência natural de queda nas vendas ou no estoque de produtos, o modelo pode estar capturando essa tendência e projetando-a para o futuro. Isso pode ocorrer se houver uma diminuição na demanda ou um ciclo sazonal que resulta em vendas mais baixas ao longo do tempo.

     2. Mudanças no Comportamento do Consumidor:
     Alterações no Mercado: Mudanças no comportamento do consumidor ou no mercado, como uma diminuição no interesse por certos produtos ou a introdução de novos concorrentes, podem causar uma previsão de queda nas vendas.
    
     3.  Sazonalidade e Efeitos Temporais:
Fatores Sazonais: Se o seu modelo não estiver ajustado para capturar efeitos sazonais ou outros fatores temporais, pode haver uma previsão de queda baseada em padrões sazonais ou cíclicos que não foram considerados.

P10 LINHA ROSA (Reflete um cenário pessimista)

P50 LINHA VERDE(Reflete um cenário neutro)

P90 LINHA AMARELO(Reflete um cenário otimista)

![Captura de tela 2024-07-31 174754](https://github.com/user-attachments/assets/bd3ffa89-126b-415a-a2a4-223ba51edb98)

![image](https://github.com/user-attachments/assets/ff52f96c-8353-44d4-810a-187a0477d6c1)

