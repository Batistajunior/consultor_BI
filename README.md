# consultor_BI

primeiramente utilizei o pentaho para fazer o ETL os dados em excel cada tabela foi extraido pelo step microsoft excel input depois de feito utilizei o step multiway merge join, depois o select values 1, 2, 3, 4 e 5 em alternancia com o calculator 1,2,3 e 4 feito isso utilizei o step microsoft excel writer para a saída dos dados tratados e por fim o table output para fazer a ingestão dos dados tratados para o postgres. 
No postgres fiz a união das colunas datedat e data para fazer a analise codigo utilizado:  
-- Adicionei a coluna NewData à tabela bi_consultor



ALTER TABLE bi_consultor
ADD COLUMN NewData DATE;

-- Atualizei a coluna NewData com a combinação das datas de DateDat e Data



UPDATE bi_consultor
SET NewData = DateDat;

-- Inserir os valores da coluna Data na coluna NewData para as próximas linhas



INSERT INTO bi_consultor (NewData)
SELECT Data FROM bi_consultor;

-- Exibir a tabela bi_consultor com a nova coluna NewData




SELECT * FROM bi_consultor;



COPY bi_consultor TO '/Users/batistajunior/Downloads/tabela_bi_consultor.csv' DELIMITER ',' CSV HEADER;

na parte do consumo do postgres para o power bi, houve um erro de configuração, mas foi em virtude da minha máquina ser um sistema macos ao qual mesmo utilizando o virtual parallels o firewall não permitiu o consumo, todavia não impossibilitou a análise de dados no power bi. Pois fiz a ingestão manual dos dados.

link do power bi online: https://app.powerbi.com/groups/me/reports/e545ca38-1169-4857-af43-8089aa64d737/ReportSection?clientSideAuth=0&experience=power-bi
 
