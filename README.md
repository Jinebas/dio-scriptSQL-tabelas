# Banco de Dados Gerenciador de Espaçonaves :space_invader::airplane::small_airplane:



## Script de criação de tabelas

   <br/>

***CREATE DATABASE*** EstrelaDaMorte

***USE*** EstrelaDaMorte

  <br/>  <br/>

**>>>Criação de Tabela PLANETAS**

***CREATE TABLE*** Planetas(  <br/>
	IdPlaneta int NOT NULL,  <br/>
	Nome varchar(50) NOT NULL,  <br/>
	Rotacao float NOT NULL,  <br/>
	Orbita float NOT NULL,  <br/>
	Diametro float NOT NULL,  <br/>
	Clima varchar(50) NOT NULL,  <br/>
	Populacao int NOT NULL,  <br/>
)  <br/>
GO

***ALTER TABLE*** Planetas ***ADD CONSTRAINT*** PK_Planetas ***PRIMARY KEY*** (IdPlaneta);  <br/>
GO

  <br/>  <br/>

**>>>Criação de Tabela NAVES**

***CREATE TABLE*** Naves(  <br/>
	IdNave int NOT NULL,  <br/>
	Nome varchar(100) NOT NULL,  <br/>
	Modelo varchar(150) NOT NULL,  <br/>
	Passageiros int NOT NULL,  <br/>
	Carga float NOT NULL,  <br/>
	Classe varchar(100) NOT NULL,  <br/>
)  <br/>
GO

***ALTER TABLE*** Naves ***ADD CONSTRAINT*** PK_Naves ***PRIMARY KEY*** (IdNave);  <br/>
GO

  <br/>  <br/>

**>>>Criação de Tabela PILOTOS** 

***CREATE TABLE*** Pilotos(  <br/>
	IdPiloto int NOT NULL,  <br/>
	Nome varchar(200) NOT NULL,  <br/>
	AnoNascimento varchar(10) NOT NULL,  <br/>
	IdPlaneta int NOT NULL,  <br/>
)  <br/>
GO

***ALTER TABLE*** Pilotos ***ADD CONSTRAINT*** PK_Pilotos ***PRIMARY KEY*** (IdPiloto);  <br/>
GO

***ALTER TABLE*** Pilotos  ***ADD  CONSTRAINT*** FK_Pilotos_Planetas ***FOREIGN KEY***(IdPlaneta)
***REFERENCES*** Planetas (IdPlaneta)  <br/>
GO

***ALTER TABLE*** Pilotos ***CHECK CONSTRAINT*** FK_Pilotos_Planetas  <br/>
GO

  <br/>  <br/>

**>>>Criação de Tabela PILOTOS NAVES**

***CREATE TABLE*** PilotosNaves(  <br/>
	IdPiloto int NOT NULL,  <br/>
	IdNave int NOT NULL,  <br/>
	FlagAutorizado bit NOT NULL,  <br/>
)  <br/>
GO

***ALTER TABLE*** PilotosNaves ***ADD CONSTRAINT*** PK_PilotosNaves ***PRIMARY KEY*** (IdPiloto, IdNave);  <br/>
GO

***ALTER TABLE*** PilotosNaves  ***ADD CONSTRAINT*** FK_PilotosNaves_Pilotos ***FOREIGN KEY***(IdPiloto)
***REFERENCES*** Pilotos (IdPiloto)  <br/>
GO

***ALTER TABLE*** PilotosNaves  ***ADD CONSTRAINT*** FK_PilotosNaves_Naves ***FOREIGN KEY***(IdNave)
***REFERENCES*** Naves (IdNave)  <br/>
GO

***ALTER TABLE*** PilotosNaves  ***ADD CONSTRAINT*** DF_PilotosNaves_FlagAutorizado  ***DEFAULT (1) FOR*** FlagAutorizado  <br/>
GO

  <br/>  <br/>

**>>>Criação de Tabela HISTÓRICO DE VIAGENS**

***CREATE TABLE*** HistoricoViagens(  <br/>
	IdNave int NOT NULL,  <br/>
	IdPiloto int NOT NULL,  <br/>
	DtSaida datetime NOT NULL,  <br/>
	DtChegada datetime NULL  <br/>
)  <br/>
GO

***ALTER TABLE*** HistoricoViagens  ***ADD  CONSTRAINT*** FK_HistoricoViagens_PilotosNaves ***FOREIGN KEY***(IdPiloto, IdNave) ***REFERENCES*** PilotosNaves (IdPiloto, IdNave)  <br/>
GO

***ALTER TABLE*** HistoricoViagens ***CHECK CONSTRAINT*** FK_HistoricoViagens_PilotosNaves  <br/>
GO
