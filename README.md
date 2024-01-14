- 👋 Hi, I’m @wilbastos01
- 👀 I’m interested in tecnologia e trabalhar remotamente para poder conhecer lugares com diversas culturas e culinarias
- 🌱 I’m currently learning data analist
- 💞️ I’m looking to collaborate on um projeto no qual me traga mais conhecimento
- 📫 How to reach me instagram wilbastos01 ou linkenid:www.linkedin.com/in/willian-bastos-8a8b20266
- 😄 Pronouns: wil
- ⚡ Fun fact: amo futebol e tocedor do são paulo fc

<!---
wilbastos01/wilbastos01 is a ✨ special ✨ repository because its `README.md` (this file) appears on your GitHub profile.
You can click the Preview link to take a look at your changes.
--->
# criação da database
create database biblioteca;

# criação da tabela

create table cad_livros(
id_livro int not null auto_increment,
nome_livro varchar(50) not null,
autor varchar (100) not null,
qt_copias int,
primary key(id_livro)
);

## criação da tabela de alunos 
create table cad_alunos(
id_cad int not null auto_increment,
nome_aluno varchar(100),
sobrenome varchar(100),
serie varchar(10),
rg varchar(10),
primary key(id_cad)
);

alter table cad_alunos add column rg varchar(50);

## criação da tabela emprestimo
create table emprestimo(
id_emprestimo int not null auto_increment,
qt_emprestimo int not null,
id_cad int not null,
id_livro int not null,
data_emprestimo date not null,
status_emprestimo varchar(50),
primary key (id_emprestimo)
);

## criar as relações ou constraints foreing keys

alter table emprestimo add constraint fk_emprestimo_cad_alunos
foreign key(id_cad) references cad_alunos(id_cad);

alter table emprestimo add constraint fk_emprestimo_cad_livros
foreign key(id_livro) references cad_livros(id_livros);

#### vamos fazer os inserts nas tabelas alunos livros e emprestimo #####

## insert de alunos ##

insert into cad_alunos(nome_aluno,sobrenome,serie,rg) values
("willian","bastos","1","5567");
insert into cad_alunos(nome_aluno,sobrenome,serie,rg) values
("maria","silva","2","5567");
insert into cad_alunos(nome_aluno,sobrenome,serie,rg) values
("jorge","soares","3","5567");
insert into cad_alunos(nome_aluno,sobrenome,serie,rg) values
("nicole","pereira","4","5567");
insert into cad_alunos(nome_aluno,sobrenome,serie,rg) values
("antonio","bastos","5","5567");


## insert dos livros ##

insert into cad_livros(nome_livro,autor,qt_copias) values 
("pai rico pai pobre","rebert klyosaki","1");
insert into cad_livros(nome_livro,autor,qt_copias) values 
("ponto de inflexição","flavio augusto","2");
insert into cad_livros(nome_livro,autor,qt_copias) values 
("do mil ao milhão","thiago nigro","3");
insert into cad_livros(nome_livro,autor,qt_copias) values 
("codigo dos milhões","pablo marçal","4");
insert into cad_livros(nome_livro,autor,qt_copias) values 
("os segredos da mente milionaria","harv eker","5");

## insert dos emprestimos ( ação de emprestimo)

insert into emprestimo (qt_emprestimo,id_cad,id_livro,data_emprestimo,status_emprestimo)
values (4,3,5,'2023-09-12','emprestou');
insert into emprestimo (qt_emprestimo,id_cad,id_livro,data_emprestimo,status_emprestimo)
values (3,4,2,'2023-09-20','devolveu');
insert into emprestimo (qt_emprestimo,id_cad,id_livro,data_emprestimo,status_emprestimo)
values (2,5,3,'2023-10-07','emprestou');

## trazer os livros com informações consolidadas dos alunos,livros e emprestimo ##

select nome_aluno,nome_livro,qt_emprestimo,data_emprestimo,status_emprestimo
from emprestimo
join cad_alunos on cad_alunos.id_cad = emprestimo.id_cad
join cad_livros on cad_livros.id_livro = emprestimo.id_livro
order by qt_emprestimo;
