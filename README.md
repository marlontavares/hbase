hbase

1. Crie a tabela com 2 famílias de colunas:<br/>
a. personal-data<br/>
b. professional-data<br/>

Comando: create 'italians', 'personal-data', 'professional-data'<br/><br/>

2. Importe o arquivo via linha de comando<br/><br/>
Comando: shell /tmp/italians.txt<br/><br/>

Agora execute as seguintes operações:<br/>
1. Adicione mais 2 italianos mantendo adicionando informações como data de nascimento nas informações pessoais e um atributo de anos de experiência nas informações profissionais;<br/>
Comando:<br/>
put 'italians', '11', 'personal-data:name',  'Giulia Gambiatti'<br/>
put 'italians', '11', 'personal-data:city',  'Roma'<br/>
put 'italians', '11', 'personal-data:birthday',  '01/03/1990'<br/>
put 'italians', '11', 'professional-data:role',  'Vendedore'<br/>
put 'italians', '11', 'professional-data:salary',  '1155'<br/>
put 'italians', '12', 'professional-data:job_experience',  '10'<br/>
put 'italians', '12', 'personal-data:name',  'Ezio Auditore'<br/>
put 'italians', '12', 'personal-data:city',  'Fiorentina'<br/>
put 'italians', '12', 'personal-data:birthday',  '05/08/1982'<br/>
put 'italians', '12', 'professional-data:role',  'Assassino'<br/>
put 'italians', '12', 'professional-data:salary',  '8000'<br/>
put 'italians', '12', 'professional-data:job_experience',  '20'<br/>

2. Adicione o controle de 5 versões na tabela de dados pessoais.<br/>
Comando: alter 'italians',  NAME => 'personal-data',  VERSIONS => '5'<br/><br/>

3. Faça 5 alterações em um dos italianos;<br/>
Comando:<br/>
put 'italians', '11', 'professional-data:salary',  '2000'<br/>
put 'italians', '11', 'professional-data:salary',  '3000'<br/>
put 'italians', '11', 'professional-data:salary',  '4000'<br/>
put 'italians', '11', 'professional-data:salary',  '5000'<br/>
put 'italians', '11', 'professional-data:salary',  '6000'<br/><br/>

4. Com o operador get, verifique como o HBase armazenou o histórico.<br/>
Comando: get 'italians', '11', {COLUMN => 'professional-data:salary', VERSIONS => 5}<br/><br/>

5. Utilize o scan para mostrar apenas o nome e profissão dos italianos.<br/>
Comando: scan 'italians', { COLUMNS => ['personal-data:name', 'professional-data:role'] } <br/><br/>

6. Apague os italianos com row id ímpar<br/>
Comando: <br/>
deleteall 'italians', '1'<br/>
deleteall 'italians', '3'<br/>
deleteall 'italians', '5'<br/>
deleteall 'italians', '7'<br/>
deleteall 'italians', '9'<br/>
deleteall 'italians', '11'<br/><br/>

7. Crie um contador de idade 55 para o italiano de row id 5<br/>
Comando: incr 'italians', '5', 'personal-data:age', 55<br/><br/>

8. Incremente a idade do italiano em 1<br/>
Comando: incr 'italians', '5', 'personal-data:age', 1<br/><br/>
