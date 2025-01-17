# TRABALHO DE PI:  Estórias sem H
Trabalho desenvolvido durante a disciplina de Banco de Dados do Integrado

# Sumário

### 1. COMPONENTES<br>
Integrantes do grupo<br>
Lélio Marcos Rangel Cunha leliomrcunha@gmail.com<br>
Carlos Eungênio Venturin Goldner carloseugventurin@gmail.com<br>
Rodolfo Müller do Amaral  email_terceiro_componente@dominio.com<br>

### 2.MINIMUNDO<br>
> O sistema proposto conterá as informações aqui detalhadas. Das Histórias serão armazenados o número, nome, sinopse, nota e corpo. Da capa é armazenada a identificação e o link para acesso. Cada história só pode pertencer a uma capa. Dos Usuários serão armazenados o número, nome, email, senha, "bio" e link da foto. Cada Usuario pode ter várias histórias mas uma história pode ser escrita por apenas um usuário. Vale ressaltar que os usuários não são obrigados a escrever histórias. Dos Comentários são armazenados número e corpo do comentário. Um usuário pode fazer vários comentários mas cada comentário pertence somente a um usuário. Não é obrigatório que o comentário seja uma resposta e os usuários podem não comentar. Responde possui apenas a identificação de resposta. Um comentário pode ter várias respostas. Gêneros possuem número e nome. GeneroHist tem identificação relacionando gênero e história. Cada Gênero pode possuir várias histórias e cada história pode ter vários gêneros. Os gêneros não precisam ter histórias.
 

### 3.RASCUNHOS BÁSICOS DA INTERFACE (MOCKUPS)<br>
![Arquivo PDF do Protótipo Balsamiq](arquivos/Prototipo_Navegacao.pdf?raw=true)


#### 3.1 QUAIS PERGUNTAS PODEM SER RESPONDIDAS COM O SISTEMA PROPOSTO?
> Relatórios gerados:
* Relatório que informe quais são as histórias criadas por cada usuário, incluindo: número da história, nome da história, número do usuário e nome do usuário.
* Relatório que informe quais são os comentários feitos por cada usuário, incluindo: número do comentário, corpo do comentário, número da história, número do usuário e nome do usuário.
* Relatório que informe quais são os gêneros de cada história, incluindo: número da história, nome da história, número do gênero e nome do gênero.
* Relatório que informe a quantidade de histórias por gênero, incluindo: número do gênero, nome do gênero e quantidade de histórias.
* Relatório que informe a quantidade de histórias escritas por cada usuário, incluindo: número do usuário, nome do usuário e quantidade de histórias.
 

### 4 TABELA DE DADOS DO SISTEMA:
![Tabela de Dados](arquivos/Tabela_BD.xlsx?raw=true)

 ### 5.PMC<br>
 ![PMC](arquivos/PMC.png "PMC")<br>
 
 
 ### 6.MODELO CONCEITUAL<br>       
![Alt text](arquivos/modConc.png "Modelo Conceitual")
    
#### 6.1 Descrição dos dados 
    Historia: Tabela que armazena as informações relativas à história
    idHist: Campo que armazena o número identificador de cada história.
    nomHist: Campo que armazena o nome de cada história.
    dscSinopseHist: Campo que armazena a sinopse de cada história.
    linkCapaHist: Campo que armazena um link para a capa de cada história.
    notaHist: Campo que armazena o número da nota para cada história.
    dscCorpoHist: Campo que armazena o conteúdo de cada história.
    Usuario: Tabela que armazena as informações relativas ao usuário
    idUsuario: Campo que armazena o número identificador de cada usuário.
    nomUsuario: Campo que armazena o nome de cada usuário.
    dscEmailUsuario: Campo que armazena o endereço de email pertencente ao usuário.
    senhaUsuario: Campo que armazena a senha pertencente ao usuário correspondente.
    dscBioUsuario: Campo que armazena as informações da "bio" do usuário.
    linkFotoUsuario: Campo que armazena um link para a foto de cada usuário.
    Comentario: Tabela que armazena as informações relativas ao comentario feito pelo usuario em alguma história.
    idComent: Campo que armazena o número identificador de cada comentário.
    idUsuarioComent: Campo que armazena o número identificador do usuário que fez cada comentário.
    idHistoriaComent: Campo que armazena o número identificador da história que foi comentada.
    dscCorpoComent: Campo que armazena o conteúdo de cada comentário.
    idRespComent: Campo que armazena o identificador do comentário que está sendo respondido.
    Genero: Tabela que armazena as informações relativas ao gênero da história.
    idGenero: Campo que armazena o número identificador de cada gênero.
    dscGenero: Campo que armazena a denominação de cada gênero.


### 7	MODELO LÓGICO<br>
![Alt text](arquivos/modLog.png "Modelo Lógico")

### 8	MODELO FÍSICO<br>
```sql
CREATE TABLE hsemh.classificacao (
	idclassificacao int4 NOT NULL DEFAULT nextval('hsemh.table_name_id_seq'::regclass),
	dscclassificacao varchar NULL,
	CONSTRAINT classificacao_pkey PRIMARY KEY (idclassificacao)
);

CREATE TABLE hsemh.comentario (
	idcoment int4 NOT NULL DEFAULT nextval('hsemh.tablename1_columnname_seq'::regclass),
	dsccorpocoment varchar NULL,
	idusuario int4 NULL,
	idhist int4 NULL,
	CONSTRAINT comentario_pkey PRIMARY KEY (idcoment)
);

CREATE TABLE hsemh.genero (
	idgenero int4 NOT NULL DEFAULT nextval('hsemh.tablename_columnname_seq'::regclass),
	dscgenero varchar NULL,
	CONSTRAINT genero_pkey PRIMARY KEY (idgenero)
);

CREATE TABLE hsemh.generohist (
	fk_genero_idgenero int4 NULL,
	fk_historia_idhist int4 NULL,
	idgenerohist int4 NOT NULL DEFAULT nextval('hsemh.tablename34_columnname_seq'::regclass),
	CONSTRAINT generohist_pkey PRIMARY KEY (idgenerohist)
);

CREATE TABLE hsemh.historia (
	idhist int4 NOT NULL DEFAULT nextval('hsemh.tablename233_columnname_seq'::regclass),
	nomhist varchar NULL,
	dscsinopsehist varchar NULL,
	notahist numeric(10, 2) NULL,
	dsccorpohist varchar NULL,
	idusuario int4 NULL,
	idcapa int4 NULL,
	idclassificacao int4 NULL,
	CONSTRAINT historia_pkey PRIMARY KEY (idhist)
);

CREATE TABLE hsemh.usuario (
	idusuario int4 NOT NULL DEFAULT nextval('hsemh.usu'::regclass),
	nomusuario varchar NULL,
	dscemailusuario varchar NULL,
	senhausuario varchar NULL,
	dscbiousuario varchar NULL,
	linkfotousuario text NULL,
	CONSTRAINT usuario_dscemailusuario_key UNIQUE (dscemailusuario),
	CONSTRAINT usuario_pkey PRIMARY KEY (idusuario)
);

CREATE TABLE hsemh.capa (
	idcapa int4 NOT NULL DEFAULT nextval('hsemh.tablename4_columnname_seq'::regclass),
	linkcapa varchar NULL,
	CONSTRAINT capa_pkey PRIMARY KEY (idcapa)
);

ALTER TABLE hsemh.comentario ADD CONSTRAINT fk_comentario_2 FOREIGN KEY (idusuario) REFERENCES hsemh.usuario(idusuario) ON DELETE CASCADE;
ALTER TABLE hsemh.comentario ADD CONSTRAINT fk_comentario_3 FOREIGN KEY (idhist) REFERENCES hsemh.historia(idhist) ON DELETE CASCADE;
ALTER TABLE hsemh.generohist ADD CONSTRAINT fk_generohist_2 FOREIGN KEY (fk_genero_idgenero) REFERENCES hsemh.genero(idgenero) ON DELETE CASCADE;
ALTER TABLE hsemh.generohist ADD CONSTRAINT fk_generohist_3 FOREIGN KEY (fk_historia_idhist) REFERENCES hsemh.historia(idhist) ON DELETE CASCADE;
ALTER TABLE hsemh.historia ADD CONSTRAINT fk_historia_2 FOREIGN KEY (idusuario) REFERENCES hsemh.usuario(idusuario) ON DELETE CASCADE;
ALTER TABLE hsemh.historia ADD CONSTRAINT fk_historia_3 FOREIGN KEY (idcapa) REFERENCES hsemh.capa(idcapa) ON DELETE SET NULL;
ALTER TABLE hsemh.historia ADD CONSTRAINT fk_historia_4 FOREIGN KEY (idclassificacao) REFERENCES hsemh.classificacao(idclassificacao) ON DELETE CASCADE;
```
        
       
### 9	INSERT APLICADO NAS TABELAS DO BANCO DE DADOS<br>
```sql
insert into capa 
values (1, 'https://bit.ly/3hXmtgn'),
(2, 'https://bit.ly/3hXmtgn'),
(3, null);


INSERT INTO usuario 
VALUES ('José de Alencar','josedealencar@hotmail.com', 'c7cc12f6deb215d2381bb9ac2c9c6c70', 'José Martiniano de Alencar foi um escritor e político brasileiro. É notável como escritor por ter sido o fundador do romance de temática nacional, e por ser o patrono da cadeira fundada por Machado de Assis na Academia Brasileira de Letras.','data:image/jpeg;base64,/9j/4AAQSkZJRgABAQAAAQABAAD/2wBDAAMCAgMCAgMDAwMEAwMEBQgFBQQEBQoHBwYIDAoMDAsKCwsNDhIQDQ4RDgsLEBYQERMUFRUVDA8XGBYUGBIUFRT/2wBDAQMEBAUEBQkFBQkUDQsNFBQUFBQUFBQUFBQUFBQUFBQUFBQUFBQUFBQUFBQUFBQUFBQUFBQUFBQUFBQUFBQUFBT/wAARCAH5AZADASIAAhEB'),
('Machado de Assis', 'machadodeassis@yahoo.com', '96be35715459112775cdd0f17f03d9aa', 'Joaquim Maria Machado de Assis foi um escritor brasileiro, considerado por muitos críticos, estudiosos, escritores e leitores um dos maiores senão o maior nome da literatura do Brasil.', 'data:image/jpeg;base64,/9j/4AAQSkZJRgABAQAAAQABAAD/2wBDAAMCAgMCAgMDAwMEAwMEBQgFBQQEBQoHBwYIDAoMDAsKCwsNDhIQDQ4RDgsLEBYQERMUFRUVDA8XGBYUGBIUFRT/2wBDAQMEBAUEBQkFBQkUDQsNFBQUFBQUFBQUFBQUFBQUFBQUFBQUFBQUFBQUFBQUFBQUFBQUFBQUFBQUFBQUFBQUFBT/wAARCAH5AZADASIAAhEB'),
('Dante Alighieri', 'dante0080@gmail.com', '956d62eb88f1fadf63d3e9613df08e69', 'Dante Alighieri foi um escritor, poeta e político florentino, nascido na atual Itália.', 'data:image/jpeg;base64,/9j/4AAQSkZJRgABAQAAAQABAAD/2wBDAAMCAgMCAgMDAwMEAwMEBQgFBQQEBQoHBwYIDAoMDAsKCwsNDhIQDQ4RDgsLEBYQERMUFRUVDA8XGBYUGBIUFRT/2wBDAQMEBAUEBQkFBQkUDQsNFBQUFBQUFBQUFBQUFBQUFBQUFBQUFBQUFBQUFBQUFBQUFBQUFBQUFBQUFBQUFBQUFBT/wAARCAH5AZADASIAAhEB'),
('Aluísio Azevedo', 'aluisioaze@gmail.com', '4e234d26e1c27a3396fcab6f0c94ae44', 'Aluísio Tancredo Gonçalves de Azevedo foi um romancista, contista, cronista, diplomata, caricaturista e jornalista brasileiro; além de desenhista e pintor.', 'data:image/jpeg;base64,/9j/4AAQSkZJRgABAQAAAQABAAD/2wBDAAMCAgMCAgMDAwMEAwMEBQgFBQQEBQoHBwYIDAoMDAsKCwsNDhIQDQ4RDgsLEBYQERMUFRUVDA8XGBYUGBIUFRT/2wBDAQMEBAUEBQkFBQkUDQsNFBQUFBQUFBQUFBQUFBQUFBQUFBQUFBQUFBQUFBQUFBQUFBQUFBQUFBQUFBQUFBQUFBT/wAARCAH5AZADASIAAhEB');


INSERT INTO historia
VALUES ('Cinco Minutos','Cinco Minutos é romance de José de Alencar. Cinco Minutos, assim como “A Viuvinha“, foram escritos no início da carreira do autor. Assim como os outros romances caracterizados pelo romantismo ingênuo de Alencar, esses dois não fogem à regra, são feitos aos moldes de folhetim, curtos, quase infantis.', 8, 'É uma história curiosa a que lhe vou contar, minha prima. Mas é uma história e não um romance. Há mais de dois anos, seriam seis horas da tarde, dirigi- -me ao Rocio para tomar o ônibus de Andaraí. Sabe que sou o homem menos pontual que há neste mundo; entre os meus imensos defeitos e as minhas poucas qualidades, não conto a pontualidade, essa virtude dos reis e esse mau costume dos ingleses. Entusiasta da liberdade, não posso admitir de modo algum que um homem se escravize ao seu relógio e regule as suas ações pelo movimento de uma pequena agulha de aço ou pelas oscilações de uma pêndula.', 1, 1),
('Memórias Póstumas de Brás Cubas', 'Memórias Póstumas de Brás Cubas retrata a escravidão, as classes sociais, o cientificismo e o positivismo da época, chegando a criar, inclusive, uma nova filosofia', 4, 'Algum tempo hesitei se devia abrir estas memórias pelo princípio ou  pelo fim, isto é, se poria em primeiro lugar o meu nascimento ou a  minha morte. Suposto o uso vulgar seja começar pelo nascimento,  duas considerações me levaram a adotar diferente método: a  primeira é que eu não sou propriamente um autor defunto, mas um  defunto autor, para quem a campa foi outro berço; a segunda é que  o escrito ficaria assim mais galante e mais novo. Moisés, que também  contou a sua morte, não a pôs no intróito, mas no cabo: diferença  radical entre este livro e o Pentateuco.', 2, 1),
('Dom Casmurro', '"Dom Casmurro" conta a história de Bento Santiago (Bentinho), apelidado de Dom Casmurro por ser calado e introvertido.', 7, 'Uma noite destas, vindo da cidade para o Engenho Novo, encontrei num trem da Central um rapaz aqui do bairro, que eu conheço de vista e de chapéu. Cumprimentou-me, sentou-se ao pé de mim, falou da lua e dos ministros, e acabou recitando-me versos. A viagem era curta, e os versos pode ser que não fossem inteiramente maus. Sucedeu, porém, que, como eu estava cansado, fechei os olhos três ou quatro vezes; tanto bastou para que ele interrompesse a leitura e metesse os versos no bolso.', 2, 2),
('A Divina Comédia', 'A Divina Comédia é basicamente a história da conversão de um pecador ao caminho de Deus.', 2, 'Dante, perdido numa selva escura, erra nela toda a noite. Saindo ao amanhecer, começa a subir por uma colina, quando lhe atravessam a passagem uma pantera, um leão e uma loba, que o repelem para a selva. Aparece-lhe então a imagem de Virgílio, que o reanima e se oferece a tirá-lo de lá, fazendo-o passar pelo Inferno e pelo Purgatório. Beatriz, depois, o guiará ao Paraíso. Dante o segue.', 3, 3),
('O Cortiço', 'O Cortiço denuncia a exploração e as péssimas condições de vida dos moradores das estalagens ou dos cortiços cariocas do final do século XIX.', 6, 'João Romão foi, dos treze aos vinte e cinco anos, empregado de um vendeiro que enriqueceu entre as quatro paredes de uma suja e obscura taverna nos refolhos do bairro do Botafogo; e tanto economizou do pouco que ganhara nessa dúzia de anos, que, ao retirar-se o patrão para a terra, lhe deixou, em pagamento de ordenados vencidos, nem só a venda com o que estava dentro, como ainda um conto e quinhentos em dinheiro.', 4, 3),
('O Alienista', 'Após conquistar respeito em sua carreira de médico na Europa e no Brasil, o Dr. Simão Bacamarte retorna à sua terra-natal, Itaguaí, para se dedicar ainda mais a sua profissão.', 6, 'As crônicas da vila de Itaguaí dizem que em tempos remotos vivera ali um certo médico, o Dr. Simão Bacamarte, filho da nobreza da terra e o maior dos médicos do Brasil, de Portugal e das Espanhas.', 2, 2),
('Missa do Galo', '“Missa do Galo” é narrado em primeira pessoa, por Nogueira, que relembra quando era um jovem de 17 anos que tinha ido ao Rio de Janeiro para estudar e que foi hospedado na casa do escrivão Meneses (viúvo de sua prima).', 7, 'NUNCA PUDE entender a conversação que tive com uma senhora, há muitos anos, contava eu dezessete, ela trinta. Era noite de Natal. Havendo ajustado com um vizinho irmos à missa do galo, preferi não dormir; combinei que eu iria acordá-lo à meia-noite.', 2, 1);

INSERT INTO comentario
VALUES ('Bom!',2,2),
('Muito Bom!',2,3),
('Não gostei!',1,1),
('Discordo...',4,1);

INSERT INTO genero
VALUES ('Ficção'),
('Não ficção'),
('Ficção científica'),
('Ficção fantástica'),
('Romance'),
('Conto'),
('Biografia');

INSERT INTO GeneroHist
VALUES (1, 1),
(2, 2),
(3, 3),
(4, 4),
(5, 5),
(6, 6);

INSERT INTO classificacao
VALUES
('Livre para todos os públicos'),
('Recomendado para maiores de 12 anos')
('Recomendado para maiores de 14 anos')
('Recomendado para maiores de 16 anos')
('Recomendado para maiores de 18 anos')
('Recomendado para maiores de 10 anos');
```
### 10	TABELAS E PRINCIPAIS CONSULTAS<br>
#### 10.1	CONSULTAS DAS TABELAS COM TODOS OS DADOS INSERIDOS (Todas) <br>
```sql
SELECT * FROM comentario;
```
![Alt text](arquivos/tabelas/comentario.png "Tabela de Comentários")
```sql
SELECT * FROM genero;
```
![Alt text](arquivos/tabelas/genero.png "Tabela de Gêneros")
```sql
SELECT * FROM historia;
```
![Alt text](arquivos/tabelas/historia.png "Tabela de Histórias")
```sql
SELECT * FROM GeneroHist;
```
![Alt text](arquivos/tabelas/possui.png "Tabela GeneroHist")
```sql
SELECT * FROM usuario;
```
![Alt text](arquivos/tabelas/usuario.png "Tabela de Usuários")

#### 10.2 PRINCIPAIS CONSULTAS DO SISTEMA 
```sql
SELECT h.idhist, h.nomhist, h.idusuario, u.nomusuario FROM historia h JOIN usuario u ON (h.idusuario = u.idusuario);
```
![Alt text](arquivos/relatorios/primeira.png "Primeira Consulta")
```sql
SELECT c.idcoment, c.dsccorpocoment, c.idhist, u.idusuario, u.nomusuario FROM comentario c JOIN usuario u ON (c.idusuario = u.idusuario);
```
![Alt text](arquivos/relatorios/segunda.png "Segunda Consulta")
```sql
SELECT h.idhist, h.nomhist, g.idgenero, g.dscgenero FROM historia h JOIN generohist p ON (h.idhist = p.fk_historia_idhist) JOIN genero g ON (p.fk_genero_idgenero = g.idgenero);
```
![Alt text](arquivos/relatorios/terceira.png "Terceira Consulta")
```sql
SELECT g.*, COUNT(*) AS "Histórias" FROM genero g JOIN generohist p ON (g.idgenero = p.fk_genero_idgenero) JOIN historia h ON (p.fk_historia_idhist = h.idhist) GROUP BY g.idgenero ORDER BY g.idgenero;
```
![Alt text](arquivos/relatorios/quarta.png "Quarta Consulta")
```sql
SELECT u.idusuario, u.nomusuario, COUNT(*) FROM usuario u JOIN historia h ON (u.idusuario = h.idusuario) GROUP BY u.idusuario ORDER BY u.idusuario;
```
![Alt text](arquivos/relatorios/quinta.png "Quinta Consulta")
 <br>
 <br>
 
 ### 11 Gráficos, relatórios, integração com Linguagem de programação e outras solicitações.<br>
     
 #### 11.1	Integração com Linguagem de programação; <br>
 ![Alt text](arquivos/relatorios/item11/integ.png "Integração")
 #### 11.2	Desenvolvimento de gráficos/relatórios pertinentes, juntamente com demais <br>
 #### solicitações feitas pelo professor. <br>
![Alt text](arquivos/relatorios/item11/rel.png "Primeiro Relatório")
![Alt text](arquivos/relatorios/item11/rel2.png "Segundo Relatório")
![Alt text](arquivos/relatorios/item11/rel3.png "Terceiro Relatório")
![Alt text](arquivos/relatorios/item11/rel4.png "Quarto Relatório")
![Alt text](arquivos/relatorios/item11/rel5.png "Quinto Relatório")
 
 ### 12 Slides e Apresentação em vídeo. <br>
    
 #### 12.1 Slides; <br>
 ![Arquivo PDF dos Slides](arquivos/slides.pdf?raw=true)
 #### 12.2 Apresentação em vídeo <br>
 [Vídeo Pecha Kucha](https://youtu.be/OwmfmOc2FDI)
 <br>
 <br>   


    
##### About Formatting
    https://help.github.com/articles/about-writing-and-formatting-on-github/
    
##### Basic Formatting in Git
    
    https://help.github.com/articles/basic-writing-and-formatting-syntax/#referencing-issues-and-pull-requests
   
    
##### Working with advanced formatting
    https://help.github.com/articles/working-with-advanced-formatting/

#### Mastering Markdown
    https://guides.github.com/features/mastering-markdown/

### OBSERVAÇÕES IMPORTANTES

#### Todos os arquivos que fazem parte do projeto (Imagens, pdfs, arquivos fonte, etc..), devem estar presentes no GIT. Os arquivos do projeto vigente não devem ser armazenados em quaisquer outras plataformas.
1. Caso existam arquivos com conteúdos sigilosos, comunicar o professor que definirá em conjunto com o grupo a melhor forma de armazenamento do arquivo.

#### Todos os grupos deverão fazer Fork deste repositório e dar permissões administrativas ao usuário deste GIT, para acompanhamento do trabalho.

#### Os usuários criados no GIT devem possuir o nome de identificação do aluno (não serão aceitos nomes como Eu123, meuprojeto, pro456, etc). Em caso de dúvida comunicar o professor.


Link para BrModelo:<br>
http://sis4.com/brModelo/brModelo/download.html
<br>


Link para curso de GIT<br>
![https://www.youtube.com/curso_git](https://www.youtube.com/playlist?list=PLo7sFyCeiGUdIyEmHdfbuD2eR4XPDqnN2?raw=true "Title")
