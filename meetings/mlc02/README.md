# Métricas para avaliar Modelos de Classificação
### Ana Chaves e Olavo Morais
### [Slides](slides.pdf)


# Matriz de Confusão, Métricas de Avaliação, Curva ROC e AUC

## Acurácia

A acurácia é a métrica mais simples para avaliar classificadores: corresponde a % de acertos que o modelo teve ao se considerar todas as previsões que ele fez

![formula_acuracia](https://external-content.duckduckgo.com/iu/?u=https%3A%2F%2Fbioinfo.com.br%2Fwp-content%2Fuploads%2F2021%2F07%2Fimage.png&f=1&nofb=1&ipt=503047bd6297f782d2c503f95fa720ca296c3f047f8946da0c920d3232102de5&ipo=images)

De forma análoga, é possível calcular o erro dividindo o total de classificações erradas pelo total de itens.

### Problemas com a acurárcia
#### Pode ser enganosa em casos de desbalanceamentos 
Supondo um conjunto de dados com 1000 amostras, das quais 950 a resposta é SIM e 50 a resposta é NÃO, um modelo que sempre responde SIM sem fazer nenhum tipo de processamento terá 95% de acurácia. Na prática você tem um modelo inútil mas que tem uma acurácia alta


#### Não transmite o tipo de erros e acertos que o modelo comete
Muitas vezes, alguns tipos de erros são mais "custosos" que outros. Por exemplo, em caso de um classificador que diz se uma pessoa tem uma determinada doença ou não, é preferível que o classificador "erra para mais" ao dizer que uma pessoa saudável está doente (muito provavelmente essa pessoa irá fazer testes complementares que vão revelar que na verdade ela está saudável) do que mandar uma pessoa doente para casa ao dizer que ela está saudável. Asssim, é necessário alguma forma de avaliar quais tipos de erro o modelo está confundindo, quais classes ele está confundindo com quais, quais classes ele está com mais precisão, etc.

## Matriz de Confusão

- Forma visual de representar os tipos de classificações que o modelo está produzindo
- Linhas representam as classes reais e colunas representam as classes classificadas pelo modelo (não é uma verdade absoluta, várias referências invertem as linhas com as colunas, sempre bom indicar para evitar erros na interpretação)
- Pode ser generalizada para classificadores com mais de 2 classes

Exemplo de matrizes de confusão: 

![Matriz de confusão](https://external-content.duckduckgo.com/iu/?u=https%3A%2F%2Ftse2.mm.bing.net%2Fth%3Fid%3DOIP.0GdIstULaMtd4oRSDDyWrAHaDu%26pid%3DApi&f=1&ipt=9524f6b20f500d9f2407813b403f8750856598d577e6dc1d452ce3ceda9c7dbd&ipo=images)


![matriz_exemplo](https://media.licdn.com/dms/image/C4E12AQEr83oq0FX3gA/article-inline_image-shrink_400_744/0/1545440533552?e=1713398400&v=beta&t=Z8S7EihCaP3KqoJxTYL51NHyR3xGOgjcFLSa1h6ZjL4)

Cada uma das 4 posições da matriz de confusão tem um nome, sendo eles:
- Verdadeiro Positivo(VP) ou True Positive(TP): caso em que o modelo respondeu SIM e a resposta esperada era SIM
- Verdadeiro Negativo(VN) ou True Negative(TN): caso em que o modelo respondeu NÃO e a resposta esperada era NÃO
- Falso Positivo(FP) ou False Positive(FP): caso em que o modelo respondeu SIM e a resposta esperada era NÃO
- Falso Negativo(FN) ou False Negative(FN): caso em que o modelo respondeu NÃO e a resposta esperada era SIM


Perceba que os elementos da diagonal principal são considerados acertos, enquanto os que estão fora dela são considerados erros.

## Métricas para avaliar o modelo

### Sensibilidade

- Avalia a capacidade do modelo de detectar corretamente os resultados positivos que são verdadeiramente positivos

![formula_recall](data:image/png;base64,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)

- De maneira mais informal: “De todos que a resposta é ‘SIM’, quantos o modelo detectou”

- Uma sensibilidade alta indica que o modelo aprendeu a detectar a classe positiva

### Especificidade

- Avalia a capacidade do modelo de detectar corretamente os resultados negativos que são verdadeiramente negativos

![formula especificidade](data:image/jpeg;base64,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wmEVkrdbI/aGbtsTfUDpGzHdT4Lp5mz7iGG5Wp6jFqCNlVNUGLlc0OAboLmuu29ybWsgspFE8n5zZiWUn1sTAyWISiWIm+iRrb2v1sRY/n6L24d5mfiuWY6ueNsbnPkbpaSR3XWvugkyLzmlayFz5TZrAST5AC5K1cGxeCtw5lRhUgkhk1aXAOF7O0nZwBG4Pgg3kWjjdcabBqmoY0OMEUsgaTYEtYXAX8OirbAs/wCO1+GtqMHweGSFxcA72mNu4Njs5wP+Cci10Ve52z1WUWY6Khwijjnmqow4B0unvXILQTt+6dyV85e4iTuzUzDM10Jo6mVt4i2QPY7YkDbbfS6xBIuLbILEREQEREBERAREQEREBERAREQEREBERAREQEREBERAREQEREBERAREQEREBERAREQEREBERBUOOf7xOGfhnfwZlu8d/wDZ+E/jov8A1KlFZkuOXPlPizpXiSCMsEYDdJGh7bk9f6w/ovXOuUo8VgpmVEr4/Z5mzAsDTcgEaTf70yFVvjoOX8/VJ93DsZimv/wxzaT/AJOd+kvopRwF/o6g/wC7UfxFJM65UgxfBTTYgXN7zXsey2pjh4i/mCQfQr7yXllmFYAykpXukaxz3angAkudfoEhXFz/AFGNNEjcuQ0T6QwP5jpy8SA2dr02eB7trbHe6ifBqpxkYFQMp4aM4Zrlu8l/P08x2s+/brf93oreqYGyU72S+69rmu8NiLH/ADWjl7A4MPwmOlwwObDHq0hzi47uLjufUlCvHOP80cR/DVP8IqpOFcGYHZPiOWpcPbS65dIqBLzL6+9fSwjr6q6cWoRU4XUU7yWieOSMkWuA5paSP1XMyVllmFYAykppHSNY6R2p4APedfwUnYrTim+pbxWwY4K2N9UIv2bZb6C7U73rEG3XxXawHJeJVWd4sWzq6na+nYGxRU+ojbVa972AL3HqSSfCyk+MZNjqs30WJSSva+jFmsAbpduTueo97/BShIUREVBERAREQEREBERAREQEREBERAREQEREBERAREQEREBERAREQEREBERAREQEREBERAREQEREBERAREQEREBERAREQEREBERAREQEREBERAREQEREBERAREQEREBERAREQEREBERAREQEREBERAREQEREBERAREQEREBERAREQEREBERAREQEREBERAREQEREBERAREQEREBERAREQEREBERAREQEREBERAREQEREBERAREQEREBERAREQEREBERAREQEREBERAREQEREH//Z)

- De maneira mais informal: “De todos que a resposta é ‘NÃO’, quantos o modelo detectou”

- Uma especificidade alta indica que o modelo aprendeu a detectar a classe negativa

### Precisão

- Avalia o número de vezes que o modelo acertou em relação ao total de vezes que o modelo previu uma classe

![formula precisao](https://miro.medium.com/max/700/1*pDx6oWDXDGBkjnkRoJS6JA.png)

- De maneira mais informal: “De todos que o modelo respondeu ‘SIM”, quantos o modelo acertou”

- Uma precisão alta indica que o modelo está confiante em prever esta classe

### F1 Score
- Junta a precisão e a sensibilidade para uma classe em uma única métrica

- É uma média harmônica entre precisão e sensibilidade(garante que a métrica será baixa se uma das duas métricas for muito baixa mesmo que a outra seja bem alta)

![f1score_formula](https://inside-machinelearning.com/wp-content/uploads/2021/09/F1-Score.png)

- Exite uma versão mais "genérica" da f1-score que utiliza pesos, mas quase sempre a f1-score acaba sendo usada

![f-beta-formula](data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAAfgAAABkCAMAAABdJdLBAAAAilBMVEX///8AAAD+/v6oqKhxcXH7+/v4+Pju7u729vbz8/Pl5eVZWVnm5ubt7e3Jycna2trT09OEhISPj4/Ly8uxsbHBwcEtLS0SEhK4uLijo6Pe3t48PDwZGRmVlZV8fHxdXV1KSko1NTVra2smJiZERESdnZ0nJycXFxdmZmZaWloLCwt4eHgwMDBCQkKWhq1nAAAbbklEQVR4nO1dCZeiPLMmQfZFVtkVdxvb///3blUFENR2ev9m7stzzkwDQhJSqTVJIUkTJkyYMGHChAkTJkyYMGHChAkTJkyYMGHChAkTJkyYMGHChAkA/vBwwn8AqmN6bu5MZP+PIQ8KBljHE+X/XnwXbfjgz5KxUyq/sqMncf6Ndfz/wf+8R7ABivI95UhKR2SfzTRJyhIWwYn64bKGvfLNPfTNw/xLRXClY5bvoMAHK5ckPa9StT2WDPVzbwRPaV60jzxQ63Ccxw5cjBcsgz/7yP5ooVwVULp2fbAtn/zxQ+ia+MkSnTSS9zF2vBvJWWZ8W7veBWi0eQax7IhT3T1FH+bPtpzQQq3OLq7U9+6+YTGIgR17le2PdbnnV1UA2Edz4+PEUkLXe/SM4br5B4t6G04QUBMrObT5J8ZTuoXeOmnUP4Dva9h7AM2NX1mzyelQyUE1+/rjO9VnogDpXrDXKpol7DKnXgBxbe/YCQgueSvGivmH6BexHrOPd4nH2PYRB2WMrT5c2FuYb/smrqPPcL0GBN+jSFMDKML+toa9D96aFS4nojhZCS/hP+Z4LaieEsC7sCKEsbNhoNY50d04sbUgN48PrH7wOH/jBA5Txko/jvyD4IoPQYGOXD14DefEWPCBcv5gleYJY5s4zV4YS9IPNpEAItKlA7lhs18V9VwyL6wM6fWMeMcaIHzwmPDARPKTcgwiuIRWHal1vDRjr56gO9CxZKubMe2Yg241xsOCSzFjO7hBirfPKn4MdXlYyA+sJXO13bnvLwZeIVc6Q5ODPFTGv9pHdgRNJukgJ+tPsLxesJKkI4cCsl+27mbUrdhqYLFVtHtC+ORZ/6cJW2lYzgYLRJWnLtkixJ9ElwATVsqQf+xT4bU/Qg/72xuKRCSVxYgK2ud4TwTpjhVHp6ph3PSjeFLVDD66e+Bq8vEvCN0/pH1tXE5uBlMOCoWEUQiS2hg3g49Pb4UHVeZumUXMoNSMedIvgkvzNdtookXmCt7r/FnCE6NDOV7Bkpj4w2cHoHtr83K0YBbm4AEF9G2nCIDuQOYR6VBaL8nlgKHpYwkO2Z/csW1sIPWcYdstKfBUcWwH6c0NTdP0rptVzbYdnVoAlzW1JwE8rPF2MOk2XTfssSHpliTDqYmKzNhiLLOAVXZUv8vYq2idJApWr5TGVunKtYnwm2qLLgbTVxhUxoKVpvSr8FsB3baaf5bwucVekWUNKAC0FUc7iuR81juKUNVIEWpXi0+D33bzUYHmiiUZ6SJQhBVUkK1OMUjX7FSvPGFBeNG5tvZzRRRvu/tTffIzXcqXs81JFpdVtzrt6pWfOhJ3Z7PTzG1bY0ezup7JRC7d9a3AhnuX1tJVB5TnvtDeUBuHcbodhyF1+PWMsk3Zgy/T/mSEULAV5F01cbWqN35qYBmqV612VhDuLcHem65HYIBZH7VjvgajZltv+KafIzxHFX4yJBU9w5pidd4r8z033FMcRxQAb+cM+Qkpv8YuILrn4wK9BVuH5HRsWRlJ7gWsj8Kbk+OTdoNluwBWEw7JHMbHK5wyUwrx3oBYEc3lcn2E872kRGAtJJEkXBAQrq9gyq6A0VDcoB4KyECPh62QWsoTv5exNIJWs4a6xIa6Z+J+Gx5YQD2101ezhmrAsIWRWjUsWW9FJchlvYCHH97o9Z8C0GvmDM4/zfEZKuLQX7MFeIZcqHqB3jtUgB4DrkbJeiLKa8s7fpfQtrPwSbAQ2UqHYXSuWbncsdUC6A8P5yvWBBoMXME07itbp9xesBrGmXHorGWQwdacuy+sdOkVyGkCJo3X7DVS5yfSIgGrN1u2WbKLfxlb/ZxME6A88nvZqfsO5pGVOFwNuOd13g2/slLzmh3JzkkX7BJL7oIt4TcVxoQVSiYOOaJ3/soKIRlOo/H2GwAtUw0NlnvC96+aC24ZX+yBKsMs4JViocz0c1ETiqgrH18vHJZM/h74kvDsxbstNEMmUrX5knrctfZSxRJsQrZdwlBVV8J5mAlVBRQvoQjlRK3XtiwRMtwngwMoXqDtBTZYTYWDONni9ThhtSkFVp6Db9MA90OtmxEjtJR/RHcKFphmHiKTy3SzXRN36GdSU1JIgxTHbibeyDJFV1FwQ4rKVhwqxW+Hb7ARIzZ+wPGqSwhl1vh0FIf36sh+YQvX2FtNs6R3euSfY9nRzXVDCIbLnUmrAUUt2T+BYHwl6cxx2gcbq5tIwywhx9fYicGEpiUKzzDLke8atiMjGwZWg32uR1QxOApnYvgKDUeJYg9rF8vGIBoMAUk+Mv+27UGCTbynO2p2Vu/W0MJTG6yUhcj3QJ5gSKM1eLmbAVmB02EQQl3o3nDp2mjgqS0r7G8MJf8RHBlmZHA9ILzJbnEXrOBS+EqjGY2h5ePAH/woHLoxdOB5tr0P6gllzsrC8tsfUZGeO1sdRPzRA/MOmosOUQ4cbPYzOxz6f0kvgbRJ5G6cgi4X9iK4MmCJChdkQTI2Iw1ORMlu300KhF1x20QctItiwa6ScF6g7DY86NWZStYJNI63Xs2+s3r7Pn/pFFKU/HL4RpJOrZ3R4QHh7S3hADxRHuiwuNVHvOcloM6tCXQF6JXl+P046fcuzDO87jbsNYsiTxenEmnxbd9W4Mxivz+D1WahjETXz+jccUlF+S9OQPZCf3viOvDcgg5FiACDRGUrbHDA4hOb1nIcNkUB6cKa6K6JziuwMM9ngsvbci9RNWtAlretuhoMvI1voEko7GljGL55FG76Saz+THg1JrgZa5auOLwfnRW6XFjO7EmYbX8Tl8QgMdS3ELb9mJ+iPqjekRPYeKN1l8gOZ816VdElGL/y9Xno0aZzp3KUKMTV4CiABsB3M5Y4TLkYrytsEfoXGGcGq6wYax3hq20bQflRG9vwTZ4g/ainRKuS9SnD0Ahqq6x/LRBhTYolyIlQ9VJ8+F+Fb6BRmz+K+v5d50+MOzBfkqiz098kfNCM5wGgb9D7c2f3lO/DN1f46JJ1gHbP5ChtyavsRmajnbCF1lFJrWBgHehGcBRO9PuKIgOAfcutIPJ3yIWg6jcjA6ale1o19zyP4Rt4HcdijSjNObHjLIviXPTQvGaHq/SLO/d00/Uw+nAk0DShqN7qth/B8tbe+pw75+1ogobjuH5T1N8GpDnxez0nj+2G8m34ZgC0065S2BpQmkv6Gh3FTpkSgfVrcaAjyGJTqlb0Al+XREWbXAN4LgJZpAsVj4Or52xBdwzbVnfSHvn7DK+jw0MnYaPt2Dq/tgps+l1nvHA04cmZhwHQdnnPdDEFOH4XwZCNsIGzTxAeOOWIIpOTh1LfeuT9bZsbb9WZMTFlh2bSehBHAql8EIHAQfWXoRTu7CIlioBDBeEBZqwLi67iHHh+vqeraGtzchTANFcNJPyBFBzwrOjxbkiQ3XWN9nIaLML8q4QRd6U8hW/wFEq50HhGwlOF4ERAH4LBe6HTeahLLeGF0RFLDvxOAt5RRORW5dqvsjzYLX6ndqli6NHZ40Uvzzg+a0UmWt5vzOoOA1UC5kyYZq1XVwxYGJm21oYRRbR8B7Oz8OgefjUD0q98RwpGCS2UAwpIllStZoa6FK3KhGQ3LbaY28sAw8pl1LaW7C11Jg6MF7C7tNm+90uM6hqZQH8+GggsUCiJoCtDaw0V14YdsVW5zwqHBAtKLTXe4VxVTKED7dQk7DC3N5migm1n2idZlci2229+dT7ee8VYadvBztyTwXY/yN78wfB7Qnj04taRaYYnIuUbQxeDLIMfedQGNMjU3XTykoB20W7cEZWYqhGP4vz1dikHYCDTiiUMoQSyvyVxo6LttoS+13bQ17aZFmyLcgWM+tJfIfNjzaHpQZ2+0WpjMdHwwo5wx7kfYN6RfuCdV7e+SmTyFEm9mZcu6gOi5eDLwYUtUBSgG19U8rJkq7lgdStbsQD8HvjnG+qFJZWF3gjcN/PZ4ndDOKuB+A2KUjjq5Tq7Z9snhM8tnMivUYqt8hvbtwOXsma8uGduvbQT8hy5pbhamTaFdVbDMB+u77iayJ0BzepYRMhfhD09E+YyHltzyQEN0FjQqgWpM7XC62cgkYM+ZL1lh0rMyMBAqGmYkce+vIoabbZzey0tBa/7vltUunWHXiM6CeyEjpnTxqktl97Ja2MRS7MN7mDhStXWgROh4sDFuYT6zrF5L/joz3ufkUuczhAPZZvNjLDZRPdu5ZsLMcDpPrC6mlm1tansN+gu0Rjzhk9JjjM4MQa/5aIZQ4PAyE6+N3jYyDbWyc/Mlh1zf2Vt/LbVamWdKgzrRsHGquuTL0aHZC6tGUhWLp6uN0FH1PB8ktti4A7jGgmSjOtiOjgIr+sJDB/7aiPChXhIo1SrTtAqmWJJGB/CVgWxQlO/qgwnUD3WEeGAm7fNAeFhnQLzz6R7g6EAOs47f4z0hghq3D9zd8Xxq8dmG4lOEMOKhlL3TbqHW5x6HKrtt2rj91f5g3OD99ew+8V8uJDK17CP4mjtdd5db6fy1eHTUifPlbtqHrRmhMHdfav6YhVtWIwh/orlBMMDfVzQWzBs8wq7q0SJg9lqFrgfXO8J2hKNpj+Otmc3VL1v8NZtNH/RfOcM1IBkt/US9fn1Kh88wge3Px7tXzGub4odnXYtGg0Mfv3lHaXLlvVi0dSXZVmnls3UIGHbAgzM7I8FjFtaCUP8KWWfAyyzw1OacjG7ule+1Kv/efAYraii3tUXMKlKYYKizbAM8/1xvL7pz4WR8Tlzv0ITcLEfraAd1hFvaHhNdP8a0oQ1oQNyHuW0WE6WiQkh4/R8Zdw9cGEIeJTZW3Nq7wCo+M3zOnClQqV/RapMQAC9C2J0YysW5EtmyQ44owsOcLJ//vAt0I+tCv8LS75iq5afMjN/ufjhl7TJBATGS8Q0l36iNWvE8Esyoda0YuBjxcG/ufkFouimrT8jPHi07bzFhC9BsbpZSD4PFQoW1iyhERCPokvvxRs27rc9PbCwJ3wB+kKEQky3c9tz0KF4HBbjSZe3Xf4J/yC8kpU2uP8vvQGfgnmlSHkGdK9GtrMm+7cIH5Y54e8H3zfMMnBdedPOY+DKftk475Jylo7jN/PibsVc9T9p9ISvQ5kxdlidQNHXhgg0oorPcVHkOryR5E5g3eJq+00y/6/DU5LgxoQF7tbop75xrZGuxtWWWd74WUUzbzFY9Za1kzIT/hI896ltoHnqeemxn1ANGbPQnZfbv88H0PVifacHJvxP8XxKPk0ofKMeWWvbYbjWV1ovfrRc8w+EdzN5wt+Ep+HTLnyjRHIr6cU6RKnfwTOAlp2XI5zP16Vsk47/6/A0/mmNFpEDnAO5d1wyF7drXPPdnTiZrPp/FPqrCN9caZ+DOa+3B4uxfeAE9dtW/ZfxtYjfhI/BK1kyWn6PqxY3qOJR19djOijOM6v+KxD1qIY0kf43wGlBYDHKL4Cpd2iFqiu2e4xvf1jGt0BLz3VRWIEzUX6A63IfPr7wVXhrsYz7CsyWlizjdPnabbv9IdAiMtNrJ/KMoGHrpdjC+oECvlj/m6sDv+vFvz6ZpJu5h0kZJdXO5953bX+eY7YP1gwD7jYwulgXvch+cnETx0Qfu0W5rvc4H6CdmGWqzlmkGHgf7FDstc+fLst8s37ljRyLb13/HOaxaKTnSJ8ZT/Zsu17gsm8pOq7X5XfZ0hrtV02HU68uYysv3Qf7dP7DdMcsHqvZVmxtUOMABU8kUg+8r4hquz0cjsnxUFif2RccrItHpql+Kp4u/XqjMf1/N9dnzeGwhUZui1X6iQ5VvXYroGQH5bc5Ufz+SBH73/insv1+CLbFtqljxFu2wIXWCoURZLEd6X3AjKls488Kxo53ORL+CBx3j+pyj2KrzIfAJSf2HikpnkM1pWjkbWK7d5WLiyJeaA4FswWkP0YT44U1Xl/pD8LYiCRPuEVM7io0LZwp7DFko0eiPE3YMVc1E/cffZhWaXO7e10g+ETSUwllVf2gNC5S7WMj/YZydXyiYMwSgQuPLvdJnb4PzvZxvt5vB6YOosDwS8fkHLcyvY4n+KvgmppCyvyxbcOzhtJSSca6T1rxfjhx5D3akZmnaf4JxZGxxeP0pptWQOu7TyWjgj5p9mTVw0g9/VymiznQ4zdypBlL0uZcmpeUslISkYObpEAZ5TdrdwjI5XUvLoEv259Va7Ad+4mVxx8eDBTe4+vDKMfdlQ4yJj56AFzZJkwJ637XGL8/5TfnuCtXjJdssNHz24HrLP2fT6ACQv3ADmhTYpjIEi/M93fJoHDfP5FW0H2cb4OSftAVoxAJu400wDGkp0GA12lfkbf3I6OtVOJOWlVRqEnck+V95IgFCNxMK7+SMamlGsP1WBfXJcUFIzdWxJaVfJ/hHqH5fv9Qq7xFeHCYS8pd4RQtx2PZelgFbRolPDXTYB95hmiyHQVB5BiZSJ7obSm9Ie3Xbp4vP/4KuBdU89+IoIQiLIgD7RC2lL037HhLeYno3kTjBUHaop16dErq07hoMN+Eu0solS12NkYjWLJLRQ2ehesOymSPO1GPQiljxqQDeq/JdmbjGqOkz00X15iarKSESMasxFlqfQnNWDzKVf4W4eWy3R+Slv02T2eDbnSzbjV2WKP/fDyQtjJ8crHXRZtRKW0zruAm4sc1fA+ef0Dg24D7wX3g0DaFAVaZEt1Vb8BPnL57QJTH3PfyjWyMS5GPH3dYgPiIElbgN4tK3GVNWadyVAHhsk1cLaULto5w130mKTamuBQEPmOa+Mii72qoeSG0Btwebdlajk+0NMl5YduSle6JlZhd6YEyfEx4SqxEI1fDJBFim6e3A7XtriiXG6a13bJL6tYiHQvmwLdiF5MsnamEfZfsCpNT/3aKk++HBj3omocGulZkBZXmr+BGqkpa3iQBjde4NkhO7umO9J7hzh+gOMs4+CPxvGGL4zZ0haM2x7QRihQmrMauT0XKjIgdkEJdvhJMVYQpaO2LWFFsdSYYDDU0ooWEDsEyX7KkZmfbO4iMpjeQaaXaPU6UAYs7QGeRHQ3HMtqBmAcTPyQCFirWn7HSEJsCMZMCCETh6zgzIQdpE/HyK13+NwBseXh5I0fmaXeb4wrP7Xrxehx/84FTtqGm3tLk8dhuU6Avg7krnxKRly73JBtFcygpKeaywdTXaE+jIywJKwkJNp8FyDjLztSKSpG/UKYk0MqldWfRU8DbMRVKpeihpmDqgRkwfz1an9J+5ogIz9sPHg2aiakrTpW/gle1xAbyzjLZi/C0cxBhg/kJEyXj9xRQ9UPXLERmlIJycksiQ/+/P48xx9zsiuMWbCEMNu/weIafi+X95PPf2OvqunukiFqnD7NXyO1jnRlhi9zCuJKMsiYqho7af9WmLEIDssH0WaqGRi1IiZpmK4ERaeswRrTOODC0muazJHMNY/baCvewRhRb1hwKPMC8y1fEi7aNlttuHwfhhTmxMFVvKooPaNpC0ynZWUKCDZPokYHpilFLOmD7c+GbX0MkUkdRWiKRETyfC+Q32So55aTBD5Hc+ml5yZLNbLZ38y7RBKY0qbv9V7jxr9LCYCECMrklOq4NCoVrkcUSHkJ9Ouv2FABZKF9m7zGoXSY5O6GVSWLMXluR3q1NKYa5NvaksjdddhRRcOyE+HGcs0Fxk+SavmLebmXBftl0HdWGb4qfDN/8FnovHmwp8uLfGslIbPqmUZtYaAgZk0Wrw4+G9CnfEahI8KM47BCgTeWWgyT2lNly2T5pgspgr62n2KVG9srWY8C4S9QKEFqgEtH3BHrkYmNJ9cLKTUCH8tAEE+pGt/rwcA4UpzzG632bArvohzr6OBaOzX63qk7hm866/+f5vdOTQPjL822ZQuYe/d095TF74k0yNPvItn2ve2AfWadzFTpq23GrwRjpU/JxTEOG6WWFSdflOgSDcUFxQmMrst61a1DRckiGXmen4zOw6vndFwPVluJB/y0+cDq22CwPc9IRqU/XfGjn9iMVIOnJAu0Nkx8O3/wacrC+iRxe0tm6DyHo3kQomW8p3wvjK7xh2BGnGQ1D75LTZJ1/RAABTlmzRYEKfoUCTWtcWSwShVVN+3kPtxGDyVgJSQ93HB4lixha9ddmgoAmFyDdskP/+Qjf0fV2Ekw9D3Nwa6uWv/HjJDQcQPDUJBDU5UdTFfyVcLsl+3Cwexpi3TeCwdw7ymP4Zqz0MDiw7Hsx7dSkbmIfUuCAUgPh9L/ILwynik2fJgfXgQZgfEDvnhOLnrE6TIxGn7sCZVziAMhJxd9PsD724+VSmBJoylFqc0qiKwySXBUWhFjriirLadc1hyWFHpQuYS7vwzf/uLBXu/yCGK7YPLsza7rUn+6CDUL1nMI3i/GkDS4Mv87VhG0sWPPJQ5TbCFho4Rnado4RzYElRRrUWnhN+GkBJQdnEEQ9rQUCkbQlswzsrgKlR4xpN837zH0PCC/sUpFbvQ/UZ631qG1YKjLHoM/A3YtMq1GwrTl+BWcpzcHXIOfdi1RscG0bqfdvkx7zeq8MRdEq1nmpj9F9w4O3Mbyqn4khs6keR7KcBTvm/Q052MuVaUetNR9jJicnr7aU5AVE78qbgd0l4weqFQU4k8iBKbG9CzAnPL3IFcXcUapk8bmwDUbt0R8B5/puJv8hx+svZNuJyVmReNMDybG3zagQmUtTzGbtzAOSVeiVFJ5XJ+iBegswO1Cze6+gldwDs7zlv67mTQyZ11VQdB/SeQtRP23DSQxfFwEq0RGzwY4YD9eDXxdDoN3Emga7sjWUhZVPn0ua036vk4kifevvN8fWuEvJg8C5YKDBYemDjy+TWNc3rYj2yGW7T838iPD0QaoaZ3lQgrANzYJ07agp8a6B3I1WPo07rw1liL9gS8aiNk7R52cZXv8NYKJe6vnk9Dz1Jk9d6ZpGLk2vPj4wTpI0bNjXPGbNaUAQfQ9UTC5dlkfMcsxKK1I726EEN09KaYKEJW1YDXXugoaTWuHo3L54wvXXungd5sldy/c6PrtNkC2hXdEkiVg4ZV6AvJTW1vChxrLG8CEn5Q2jYLuKKUemAqoGv5qDlRRyG32iAxRNpe/821oev/Li63YYe87zqX/eTo/2p1comqNpmjOaQVbwi5Cj83noXP181Q49TW8LUfI5ReoUXcvDeO50GelVL8dskkgEbe7mfYH4vUnxqJ7PjQe9nx5Xd0pLpTZSPZLhaA6VDAV7nvhapCjPdudar8Icj0oXleDBnA5w7thzfn6+/GeBrvA37sB5J36UVUQk+MtV3BXwL/P3PZxLaylP+G/BBL31r0utCZ9ALDyjCf8xqHtW/ujmrAl/J7iZxr/7lesJfw8mjp8wYcKECRMmTJgwYcKECRPegf8Dzwe6JpTaDs4AAAAASUVORK5CYII=)

## Espaço ROC
- Receiver operating characteristic(ROC) space ou espaço da característica de operação do receptor

- Espaço em que o eixo Y representa a taxa de verdadeiros positivos (sensibilidade) e o Eixo X representa a taxa de falsos positivos (1 - especificidade)

- De forma mais informal: "O eixo Y representa a razão entre o número de vezes que o modelo respondeu SIM e a resposta era SIM, enquanto o eixo X representa a razão entre o número de vezes que o modelo respondeu SIM e a respota era NÃO"

- Perceba que ambos os eixos podem ser interpretados como uma porcentagem, e elas não são complementares, isso é, sua soma não deve obrigatóriamente dar 100% pois são porcentagens calculadas em cima de coisas diferentes

- Uma vez que temos um modelo e suas métricas, podemos marcar um ponto no Espaço ROC referente a esse modelo

A figura abaixo possui 3 modelos A,B e C e seus respectivos pontos no Espaço ROC

![espaço_roc](https://www.researchgate.net/publication/278962753/figure/fig3/AS:669094160388116@1536535887764/Figura-31-Exemplo-de-espaco-ROC.png)

Dentre os pontos do Espaço ROC, destaco os seguintes: 

- Ponto Ótimo (0,1): modelo perfeito, 0% de taxa de falsos positivos (ou seja, de todas as vezes que a resposta era NÃO, 0% ele respondeu SIM) e 100% de taxa de verdadeiros positivos (de todas as vezes que a resposta era SIM, 100% ele respondeu SIM); O ideal é que o seu modelo esteja próximo a essa região

- Inferno ROC (1,0): pior modelo possível, 100% de taxa de falsos positivos (ou seja, de todas as vezes que a resposta era NÃO, 100% ele respondeu SIM) e 0% de taxa de verdadeiros positivos (ou seja, de todas as vezes que a resposta era SIM, 0% ele respondeu SIM); O ideal é que o seu modelo esteja longe dessa região

- Origem (0,0): nessa região, estão localizados os modelos que sempre respondem NÃO. Imagine que seu modelo não faça nenhum tipo de processamento e sempre responda que NÃO. Seu modelo vai ter 0% de taxa de verdadeiro positivo(de todos os casos que a resposta é SIM, 0% delas seu modelo respondeu SIM) e 0% de taxa de falsos positivos (de todos as vezes que a resposta era NÃO, 0% delas o seu modelo respondeu SIM).

- Canto Superior Esquerdo (1,1): nessa região, estão localizados os modelos que sempre respondem SIM. Imagine que seu modelo não faça nenhum tipo de processamento e sempre responda que SIM. Seu modelo vai ter 100% de taxa de verdadeiro positivo(de todos os casos que a resposta é SIM, 100% delas seu modelo respondeu SIM) e 100% de taxa de falsos positivos (de todos as vezes que a resposta era NÃO, 100% delas o seu modelo respondeu SIM).

- Linha de Referência: corresponde a linha da função identidade. Modelos que caem próximo a essa linha se comportam de forma aleatória, isso é, acertam tanto quanto se eles tivessem chutado

## Curva ROC

Alguns modelos operam com um tipo de limiar para realizar suas classificações. Um exemplo é a regressão logística, que é um classificador binário (ou seja, classifica apenas em duas classes). No entanto, em vez de determinar se um exemplo é positivo ou negativo, a regressão logística fornece uma probabilidade de o exemplo ser positivo (e, consequentemente, uma probabilidade de ser negativo).

Dessa forma, é necessário estabelecer um limite/limiar. Por exemplo, um limiar de 50% implica que se a probabilidade de ser positivo for superior a 50%, então o modelo responde 'SIM', caso contrário, 'NÃO'. Esse limite poderia ser ajustado para 60% ou 40%. É necessário testar diferentes valores de limites e comparar como o desempenho do modelo é afetado por essas variações.

A curva ROC é a curva formado por diversos pontos, onde cada ponto representa um modelo treinado com um limiar diferente. Essa curva pode ser empregada na seleção do melhor limiar, isto é, o limite que faz o modelo se aproximar mais do ponto ideal (0,1).

![curva_roc](https://external-content.duckduckgo.com/iu/?u=https%3A%2F%2Fmachinelearningmastery.com%2Fwp-content%2Fuploads%2F2019%2F10%2FROC-Curve-of-a-Logistic-Regression-Model-and-a-No-Skill-Classifier.png&f=1&nofb=1&ipt=e2870d58de98b02fde010606df80347f4c78a9136e04d152adf046c055a469a6&ipo=images)

Na imagem acima, cada ponto representa um modelo de regressão logística treinado com um limiar diferente. Os limites que produziram pontos mais próximos ao ponto (0,1) são recomendados.

A curva ROC também pode ser usada para comparar 2 ou mais modelos diferentes
![curva_roc_2_modelos](https://i.stack.imgur.com/fn2QC.png)

### Area Under Curve (AUC)

Uma métrica muito usada para comparar duas curvas ROC é calcular a área de cada curva. Essa métrica varia de 0 a 1, e pode nos ajudar a escolher um modelo que esteja tenha a curva mais próxima do ponto ideal

![auc_2_curvas](https://external-content.duckduckgo.com/iu/?u=https%3A%2F%2Ftse2.mm.bing.net%2Fth%3Fid%3DOIP.2uveIfqT8_xEeICL66dV0gHaFh%26pid%3DApi&f=1&ipt=acf4d403073beea027935b964c376b5d99d128726330c21d32c46ca0a196fad2&ipo=images)

No exemplo acima, o modelo que produziu a curva ROC 1 está mais próximo do ideal e possui uma área maior, enquanto o modelo que produziu a curva ROC 2 está mais próximo de um modelo aleatório.

## E para Generalizar?

Até então, tanto a matriz de confusão, as métricas apresentadas e a curva ROC estavam se referindo a classificadores binários, mas todos os elemtnos citados podem ser adaptados para classificadores que fazem previsões para mais de 2 classes.

### Matriz de Confusão para N Classes
Consiste em uma matriz N x N, onde o elemento da linha i e coluna j representa o número de vezes que o modelo previu i e a resposta correta era j
![matriz_3_classes](https://external-content.duckduckgo.com/iu/?u=https%3A%2F%2Fmiro.medium.com%2Fmax%2F1400%2F1*yH2SM0DIUQlEiveK42NnBg.png&f=1&nofb=1&ipt=958c07167fe5eae4065eabd598606f87b576bfcbaa177675f6954925e6e5b7ff&ipo=images)

Perceba que as previsões da diagonal principal são consideras acertos, enquanto as que estão fora são consideradas erros

### Precisão, Sensibilidade e F1 para N Classes
As métricas também podem ser adaptadas para cada classe
![precision_recall_multiclasses](https://external-content.duckduckgo.com/iu/?u=https%3A%2F%2Fmiro.medium.com%2Fmax%2F1216%2F1*eS4zV29dd9vFo0KQSk8s7w.png&f=1&nofb=1&ipt=b431bf00cd15202126a1363ba558dcf49dc2144aeeb61ad9dc97b4a1ebdbbd4a&ipo=images)

Como é possível perceber pela imagem, precisão reflete a "confiança" do modelo ao responder uma classe, isso é, de todas as vezes que ele respondeu uma determinada classe, quantas ele acertou. A sensibilidade/recall reflete o quão bem o modelo aprendeu a detectar uma classe, isso é, de todas as vezes que a resposta esperada era de uma classe, quantas o modelo acertou

Para calcular a F1 de cada classe, basta fazer a média harmônica entre a precisão e o recall da respectiva classe

### Curva ROC e AUC
A curva ROC também pode ser generalizada para modelos de classificação multiclasse. Em vez de ter apenas uma curva (como em um modelo binário), você pode criar curvas individuais para cada classe. Para fazer isso, precisamos calcular a sensibilidade (ou recall) para cada classe. 

A sensibilidade/recall de uma classe é determinada pelo número de vezes que o modelo corretamente previu essa classe, dividido pelo número total de exemplos que pertencem a essa classe. Já no eixo X, para cada classe é calculado como 1 menos a especificidade, issso é, o número de vezes que o modelo previu essa determinada classe quando na verdade a resposta real era outra classe.

![multiclasse_roc](https://i.stack.imgur.com/7O1Ar.png)


####  Um comentário sobre micro average e macro average
Perceba na imagem acima que também é possível calcular 2 curvas médias, sendo uma a média macro e a outra a média micro. A média macro de uma métrica corresponde a média simples dessa métrica calculada para cada classe. Então em um classficador com 4 classes, por exemplo, para calcular a precisão média macro, basta calcular a precisão de cada classe, somar essas 4 precisões e dividir por 4. Já para calcular a precisão média micro, você calcula usando o "Verdadeiros Positivos" gerais, isso é, a soma dos verdadeiros positivos de cada classe e também o mesmo com o verdadeiros negativos. 

![media_macro](https://miro.medium.com/v2/resize:fit:1400/1*A8-O-bAXAAXPJCri66aMCg.png)

![media_micro](https://miro.medium.com/v2/resize:fit:1200/1*DdVtgn3uHgBp3a9qjU9hqg.png)

## Referências
- ROC and AUC, Clearly Explained! - StatQuest (https://www.youtube.com/watch?v=4jRBRDbJemM)

- Machine Learning Fundamentals: The Confusion Matrix - StatQuest (https://www.youtube.com/watch?v=vP06aMoz4v8)

- Machine Learning Fundamentals: Sensitivity and Specificity - StatQuest (https://www.youtube.com/watch?v=vP06aMoz4v8)

- Inteligência Artificial - Uma Abordagem de Aprendizado de Máquina - André Carlos Ponce de Leon Ferreira Et Al. Carvalho

- Micro-average, Macro-average, Weighting: Precision, Recall, F1-Score (https://vitalflux.com/micro-average-macro-average-scoring-metrics-multi-class-classification-python/#When_to_use_Micro-averaging_Macro-averaging_Weighting_scores)
