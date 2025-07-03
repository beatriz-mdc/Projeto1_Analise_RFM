# Etapas do projeto

***1. Processamento e preparação da base de dados***

O projeto tem como objetivo realizar a segmentação de clientes através de uma análise RFM a fim de fornecer conclusões que permitam a empresa tomar decisões mais embasadas e assertivas. O projeto foi desenvolvido individualmente.

As seguintes ferramentas foram utilizadas: 
- Google planilhas;
- Google slides.

Os dados foram compartilhados online através de 3 planilhas google disponibilizadas pela empresa, nomeadas “clientes”, “resumo compra” e “transações”, onde continham informações diversas da base de clientes como número de identificação, registro de compras, data de cadastro, entre outros. Os arquivos originais foram disponibilizados apenas para visualização, não sendo editável. Dessa forma, foi necessário criar cópias para que a edição pudesse ser realizada. Para gerar essas cópias, os arquivos foram salvos no drive pessoal e unificados em 1 único arquivo, dividido em 3 abas, através da função IMPORTRANGE.

Após uma breve avaliação inicial, foi decidido realizar algumas verificações sobre as bases a fim de localizar dados fora do padrão que pudessem impactar no processo de análise. Primeiro, foram procurados dados duplicados. Para localizar e excluir esses valores, foi utilizada a opção de “remover cópias” direto da aba “dados” dentro do google planilhas. Após selecionar os dados de cada uma das 3 abas e realizar o processo de “aba dados > limpeza de dados > remover cópias”, os dados duplicados passíveis de exclusão foram retirados. 

Em seguida, foram procurados dados nulos que pudessem constar em alguma das bases. Essa pesquisa foi realizada através de filtro inserido nas colunas de cada informação da planilha. Foram localizados dados nulos nas abas “clientes” e “transações”. Os valores nulos encontrados na aba “clientes” eram relacionados à informação de salário anual. Para esse caso, o tratamento dado foi substituir a célula vazia pelo número 0, uma vez que se entende que não é necessário ter renda própria para realizar uma compra. Também foram encontrados valores nulos na aba “transações” sendo referentes a identificação do cliente. Essas células foram excluídas, visto que se não existe rastreamento do cliente através de seu ID, mesmo que haja registro de compra, não seria possível relacionar suas informações com os demais dados da planilha.

Para a identificação de possíveis outliers também foi utilizado filtro. Na coluna “ano nascimento”, os dados foram ordenados de forma decrescente a fim de localizar alguma data que fugisse do padrão. Dessa forma, foram encontradas datas de nascimento que pertenciam a clientes > 100 anos, se destacando em relação aos demais, onde o limite chegava a casa dos 80 anos. Com isso, foi decidido excluir esses IDs da análise para evitar que sua idade desviasse demais a média final da base de clientes.
Ao analisar as informações das 3 abas, é possível notar que o ID cliente é o dado em comum entre elas. Dessa forma, para fazer qualquer relação, ela será a chave primária a ser utilizada. Após essa verificação, foi decidido que a aba “clientes” seria a base principal para unir as informações das demais abas, já que fornece dados mais completos em comparação às outras bases. Com a finalização dessa primeira etapa de tratamento, começaram a ser criadas novas variáveis, como: idade, ano de cadastro, mês de cadastro e total de filhos. Essas variáveis foram calculadas sobre os dados que constavam na própria aba base “clientes”. Todos os cálculos utilizados estão registrados na planilha.

Para unir os dados em uma única aba foi utilizada a chave primária ID cliente como principal referência. A partir dessa chave foi possível buscar novas variáveis como: última compra, ano da última compra, mês da última compra, quantidade de transações, quantidade de compras na loja, quantidade de compras online, total de compras por tipo de produto e total de compras geral. Na aba “transações” há vários registros de compras por cliente com suas respectivas datas. Dessa forma, para verificar qual a compra mais recente realizada pelo cliente, foi decidido utilizar a data de última compra encontrada. Para chegar a essa informação foi utilizado filtro ordenando as informações de data de forma decrescente. Assim, ao utilizar a função PROCV, ela puxaria a primeira data dentro da ordenação mais recente. Após localizar a data de “última compra” de cada cliente, foi verificado que alguns não possuem data informada, nem quantidade de transação, porém, possuíam registro de compra. Para esses casos foi realizado o seguinte ajuste: a data de cadastro foi considerada como a data de última compra e para o número de transações foi adicionado pelo menos 1 compra para esses clientes. 
Todos os cálculos utilizados estão registrados na planilha.

***2. Análise Exploratória***

Com a fase de exploração de dados organizada e as planilhas unificadas em uma única aba, seguimos para a análise em tabelas. Foram utilizadas tabelas dinâmicas a fim de realizar o cruzamento de dados e explorar novas variáveis. Com essa nova visão, é possível gerar insights iniciais e relacionar informações que enriquecem a análise. A partir das tabelas dinâmicas também foram criados gráficos que ajudam na melhor visualização das informações.
Todas as tabelas e gráficos criados nessa etapa estão registrados na planilha.

***3. Análise***

Após os primeiros insights observados através das tabelas dinâmicas e gráficos, iniciamos a segmentação de clientes. Para a segmentação será utilizado a análise RFM (recência, frequência e monetário) para cada cliente. Para calcular o RFM, começamos pelo cálculo do quartil dividido em 5 intervalos de 0 a 4. Para calcular a recência consideramos a data de última compra, frequência se refere ao número de transações e monetário ao valor total de compra. 
Abaixo está a tabela com os números encontrados para cada variável:

![image](https://github.com/user-attachments/assets/cef09a65-2e94-4c59-ba62-60ffbe73e6ed)

Com os valores encontrados foram criados intervalos de 1 a 5 a fim de localizar onde cada cliente se encaixava. Abaixo estão os intervalos utilizados para cada RFM:

![image](https://github.com/user-attachments/assets/69b02be4-9a19-4a20-af8b-47dc6815a8d1)

Cada cliente teve seus RFMs calculados. Com esses valores, foi feito o cálculo RFM que é a média da soma dos valores encontrados. A partir desses valores foi gerada uma tabela com 5 segmentações de clientes descritas abaixo:

**Melhores Clientes**
**Características:** Alta Recência, Alta Frequência, Alto Valor Monetário.
**Descrição:** Esses são os clientes mais valiosos para o negócio. Compraram recentemente, compram com frequência e gastam uma boa quantidade de dinheiro em cada transação.

**Clientes Leais**
**Características:** Alta Frequência, Médio/Alto Valor Monetário, Baixa Recência.
**Descrição:** Esses clientes compram frequentemente, mas já faz algum tempo que não realizam uma compra recente. Eles têm um bom histórico de compras, mas precisam de um incentivo para voltar.

**Clientes Potenciais**
**Características:** Alta Recência, Alta Frequência, Baixo Valor Monetário.
**Descrição:** Esses clientes estão comprando frequentemente e recentemente, mas ainda não gastam muito. Eles têm um bom comportamento de compra, mas há potencial para aumentar o valor das transações.

**Clientes de Risco**
**Características:** Baixa Recência, Alta Frequência, Alto Valor Monetário.
**Descrição:** Esses clientes costumavam comprar com frequência e gastaram muito, mas não compraram recentemente. Eles estão em risco de se tornarem inativos.

**Clientes Inativos**
**Características:** Baixa Recência, Baixa Frequência, Baixo Valor Monetário.
**Descrição:** Esses clientes não compram há muito tempo, não compram com frequência e gastam pouco. São clientes inativos ou até perdidos.

Com as segmentações definidas foi feita a distribuição dos clientes através do resultado do cálculo RFM. Abaixo a tabela com o resultado:

![image](https://github.com/user-attachments/assets/f5c488e2-a467-4809-bd75-6a5e63af6729)

Após os dados definidos e a segmentação realizada, foi desenvolvido um dashboard em google sheets que resume as principais informações levantadas ao longo da análise considerando a resposta a campanha de marketing, ano e a classificação de clientes como os filtros.

![image](https://github.com/user-attachments/assets/10528b11-b63c-41f2-9267-5fb4576beed0)

A análise realizada mostrou que a maioria dos clientes realiza suas compras em loja física com preferência para produtos como vinhos e carnes. Outro dado importante observado é que a maioria não respondeu a campanha de marketing realizada, porém, apesar do baixo engajamento, o valor total de compras ainda é alto. Isso mostra que o marketing teve um direcionamento errado nas decisões sobre a campanha e mostra também que mesmo com o baixo envolvimento com a marca, o cliente continua disposto a gastar no Mercado.

Dessa forma, verificamos que há um potencial a ser explorado dentro do segmento de clientes do Mercado, porém, é necessário um melhor direcionamento para cada tipo de cliente. Abaixo algumas sugestões para cada segmento encontrado:

- **Melhores Clientes > Ação recomendada:** Benefícios exclusivos, programas de fidelidade ou recompensas.
- **Clientes Leais > Ação recomendada:** Ofertas que incentivem uma nova compra a fim de aumentar o engajamento com a empresa.
- **Clientes Potenciais > Ação recomendada:** estratégias para aumentar o gasto médio (up-selling ou cross-selling) e ofertas para aumentar o valor da compra;
- **Clientes de Risco > Ação recomendada:** Campanhas de reengajamento para que voltem a comprar.

Com isso, concluímos que “O Mercado” possui clientes que consomem seus produtos, preferencialmente em loja física, mas que precisam de uma melhor campanha de marketing direcionada corretamente para que sejam fidelizados.
