# DashboardFilmes
# DOCUMENTAÇÃO DO DASHBOARD USANDO IMBD DATASET  

Download da base de dados do IMDb, encontrada no Kaggle, para fins educacionais de portfólio.  

TRANSFORMAÇÃO DE DADOS EM INFORMAÇÕES PARA RESPONDER ÀS SEGUINTES PERGUNTAS:  
1. As pessoas estão assistindo menos filmes atualmente?  
2. Quais são os gêneros de filmes mais populares em termos de vendas?  
3. Como a duração dos filmes varia por gênero?  
4. Qual o top 5 filmes mais bem avaliados?  

---

## PROCESSO DE TRANSFORMAÇÃO DE DADOS em geral  
- importei os dados em formato csv.  
- colunas inúteis removidas.  
- nomes de colunas renomeadas para pt-BR.  
- ao final, modifiquei a cor de fundo, e a cor de cada grafico para ficarem harmoniosos, na mesma paleta.  

---

## 1. AS PESSOAS ESTÃO ASSISTINDO MENOS FILMES ATUALMENTE?  
- Gráfico de linhas,  
- eixo y a coluna “Ano_Lançamento” com os anos, no eixo x a coluna “Vendas” com o quantidade monetária.  
- Alterei o tipo de dado da coluna “Vendas” para valor decimal fixo, com o formato moeda, com 2 casas decimais.  
- Substituí o valor “ , ” por “ . ” como separador de milhar.  
- Removi valores em branco de todas as colunas.  

---

## 2. QUAIS SÃO OS GÊNEROS DE FILMES MAIS POPULARES EM TERMOS DE VENDAS?  
- Gráfico de pizza,  
- mostrando percentual de vendas por gênero.  
- Extrai só o primeiro valor antes da vírgula usando o delimitador por vírgula para separar os 3 valores na coluna “Gênero”, isso criou as tabelas Gênero 1, 2 e 3.  
- Excluí a 2 e a 3.  
- Renomeei a “Gênero 1” para “Gênero”.  
- Tirei o valor para não ficar poluído, e mostrar apenas a porcentagem.  
- Formatação da legenda e título.  

---

## 3. COMO A DURAÇÃO DOS FILMES VARIA POR GÊNERO?  
- Gráfico de barras clusterizado,  
- Substituí o valor da coluna “Duração”, (‘min’ por ‘’) um string vazia após o número.  
- Alterei o tipo do dado de Text para Inteiro.
- Usei DAX para criar uma nova coluna e converter os minutos em horas:  
    DuraçãoHora =  
    VAR Minutos = [Duração]  
    VAR Horas = INT(Minutos / 60)  
    VAR MinRestantes = MOD(Minutos, 60)  
    RETURN FORMAT(Horas, "0") & ":" & FORMAT(MinRestantes, "00")

- Usei no eixo Y a coluna “Gênero”.
- Usei no eixo X a MÉDIA da coluna “Duração”.
- Usei “DuraçãoHora” como valor do rótulo.

---

## 4. QUAL O TOP 5 FILMES MAIS BEM AVALIADOS?
- Tabela Ranqueada,
- Adicionei o tipo de grafico “tabela”.
- Inseri a coluna “Filme”, “Avaliação IMDB”, “Diretor” e “Gênero”.
- Filtrei em ”Top N 5”, para mostrar apenas os 5 primeiros resultados.
- Coloquei em ordem Decrescente, da maior avaliação para a menor.
- Alterei a cor de cada barra, para fazer referencia a coluna de genero usada tambem no grafico pizza.
