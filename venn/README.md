✸ Todo mundo acha que domina JOIN até que precisa fazer uma JOIN cabeluda.

Essa semana revisei um conteúdo essencial em dados, sobretudo em SQL: o diagrama de Venn, crucial para um alicerce sólido para Análise de Dados e Business Intelligence!

Às vezes é confuso transformar uma demanda numa JOIN que funcione de primeira — mas torná-la visual pode aumentar seu desempenho na hora de estruturar queries pra dashboards e relatórios de BI.

Vamos revisar?

Temos duas tabelas: alunos do curso de Python (A) e alunos do curso de SQL (B).

Quem faz os dois cursos? É A ∩ B (intercseção) — o conectivo "E" (Python E SQL). Em SQL, isso é uma 𝗜𝗡𝗡𝗘𝗥 𝗝𝗢𝗜𝗡.

Quem faz só 𝗣𝘆𝘁𝗵𝗼𝗻? É a diferença A - B. Em SQL, uma 𝗟𝗘𝗙𝗧 𝗝𝗢𝗜𝗡.

E quem faz só 𝗦𝗤𝗟? É B - A. Em SQL, seria uma 𝗥𝗜𝗚𝗛𝗧 𝗝𝗢𝗜𝗡:


𝗦𝗘𝗟𝗘𝗖𝗧
	cs.id_aluno,
	cs.nome 𝗔𝗦 "alunos_sql"
𝗙𝗥𝗢𝗠 Curso_Python cp
𝗥𝗜𝗚𝗛𝗧 𝗝𝗢𝗜𝗡 Curso_SQL cs 
	𝗢𝗡 cs.id_aluno = cp.id_aluno
𝗪𝗛𝗘𝗥𝗘 cp.id_aluno 𝗜𝗦 𝗡𝗨𝗟𝗟;

Mas a RIGHT JOIN não é tão utilizada no dia a dia do analista pois, sintaticamente, faz mais sentido inverter a posição de B e transformá-la numa LEFT JOIN:

𝗦𝗘𝗟𝗘𝗖𝗧
	cs.id_aluno,
	cs.nome 𝗔𝗦 "alunos_sql"
𝗙𝗥𝗢𝗠 𝘊𝘶𝘳𝘴𝘰_𝘚𝘘𝘓 𝘤𝘴 
𝗟𝗘𝗙𝗧 𝗝𝗢𝗜𝗡 𝘊𝘶𝘳𝘴𝘰_𝘗𝘺𝘵𝘩𝘰𝘯 𝘤𝘱
	𝗢𝗡 cs.id_aluno = cp.id_aluno
𝗪𝗛𝗘𝗥𝗘 cp.id_aluno 𝗜𝗦 𝗡𝗨𝗟𝗟;

Isso continua sendo B - A, mas é uma forma mais legível de query, obedecendo o fluxo de leitura ocidental (esquerda → direita)

Por fim, quando eu quero  ver tudo ao mesmo tempo, (alunos que cursam Python ou alunos que cursam SQL), nós usamos uma FULL OUTER JOIN. Ele é o conjunto união, representado por A∪B.

E você com certeza já sacou que o conjunto união é identificado pelo conectivo "OU" (alunos que cursam Python OU SQL).

Minha construção dessa vez vai ser um pouco diferente, utilizando a cláusula COALESCE para retornar o primeiro valor não-nulo requisitado. (Você pode ver o que acontece sem ela na imagem 9)

𝗦𝗘𝗟𝗘𝗖𝗧 𝗖𝗢𝗔𝗟𝗘𝗦𝗖𝗘 (cp.id_aluno, cp.nome) as id_aluno,
	cp.nome as "alunos_python",
	cs.nome as "alunos_SQL"
𝗙𝗥𝗢𝗠 Curso_Python cp 
𝗙𝗨𝗟𝗟 𝗢𝗨𝗧𝗘𝗥 𝗝𝗢𝗜𝗡 Curso_SQL cs
	𝗢𝗡 cp.id_aluno = cs.id_aluno;

Um erro comum de iniciante (inclusive meu, no início): achar que JOIN se refere a tabelas e colunas. Na verdade, ele se refere sempre a registros — as tabelas são agrupadas, e você escolhe as colunas na query, que depois viram a base de qualquer dashboard ou insight de negócio confiável.

Essas três variações são as que você precisa dominar antes de entender lógicas mais complexas, como as multi JOINS, essenciais pra quem quer atuar como Analista de Dados ou de BI e trabalhar com visualização de dados.
