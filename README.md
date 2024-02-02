# Estudo de caso

### BikeShop

Visão Geral:

A BikeShop é uma empresa especializada na venda de bicicletas e acessórios relacionados. 
Localizada em uma área urbana movimentada de Uberlândia, Minas Gerais, a empresa tem 
como objetivo oferecer uma variedade de bicicletas de alta qualidade para ciclistas de todos os 
níveis, desde iniciantes até ciclistas experientes e entusiastas.

Desafio:

A BikeShop está crescendo rapidamente e enfrenta desafios no gerenciamento eficiente de seu 
inventário, clientes e vendas. Atualmente, eles estão registrando essas informações 
manualmente ou usando planilhas eletrônicas, o que se tornou ineficiente e propenso a erros. 
Eles reconhecem a necessidade de um sistema de banco de dados centralizado que possa 
armazenar e gerenciar essas informações de forma mais eficaz.

Objetivos do Sistema de Banco de Dados:

Gerenciar o inventário de bicicletas e acessórios, incluindo detalhes como modelo, marca, 
quantidade em estoque, preço de venda e fornecedor.
Manter um registro centralizado de clientes, incluindo informações como nome, endereço, 
número de telefone, endereço de e-mail e histórico de compras.
Registrar e acompanhar as vendas de bicicletas e acessórios, incluindo detalhes como data da 
venda, produtos vendidos, preço de venda, método de pagamento e vendedor responsável.

Requisitos Funcionais do Sistema de Banco de Dados:

Capacidade de adicionar, atualizar e excluir itens do inventário, bem como verificar a 
disponibilidade de produtos em tempo real.
Capacidade de adicionar novos clientes, atualizar informações existentes e manter um histórico 
de suas compras anteriores.
Funcionalidade para registrar novas vendas, incluindo a associação dos produtos vendidos aos 
clientes correspondentes e a geração de recibos.
Recursos de segurança para proteger os dados do cliente e do inventário contra acesso não 
autorizado.
Capacidade de gerar relatórios de vendas, análises de estoque e dados do cliente para ajudar 
na tomada de decisões comerciais.

Abordagem Proposta:

A BikeShop planeja desenvolver um sistema de banco de dados personalizado usando 
tecnologias modernas de banco de dados, como MySQL ou PostgreSQL. Eles planejam 
colaborar com desenvolvedores de software especializados para projetar e implementar o 
sistema de acordo com seus requisitos específicos. O sistema será acessado por funcionários 
autorizados por meio de uma interface de usuário intuitiva, onde poderão realizar todas as 
operações necessárias de forma eficiente.

Benefícios Esperados:

Melhoria na eficiência operacional, permitindo que a BikeShop gerencie seu inventário, clientes 
e vendas de forma mais rápida e precisa.
Maior satisfação do cliente, oferecendo um serviço mais personalizado e mantendo um 
histórico detalhado das interações anteriores.
Melhoria na tomada de decisões comerciais com base em relatórios e análises de dados 
precisos e atualizados.
Com um sistema de banco de dados eficiente e bem projetado, a BikeShop está confiante de 
que poderá atender às demandas de seus clientes de maneira mais eficaz e continuar 
prosperando no mercado de bicicletas.

Modelo lógico para o estudo de caso

Tabelas: 

Inventário
* ID_Inventario (Chave Primária)
* Modelo
* Marca
* Quantidade
* Preço
* ID_Fornecedor (Chave Estrangeira referenciando a tabela de Fornecedores)

Clientes

* ID_Cliente (Chave Primária)
* Nome
* Endereço
* Número_de_Telefone
* Email

Vendas

* ID_Venda (Chave Primária)
* Data
* ID_Cliente (Chave Estrangeira referenciando a tabela de Clientes)
* ID_Inventario (Chave Estrangeira referenciando a tabela de Inventário)
* Quantidade_Vendida
* Preço_Total
* Método_de_Pagamento
* ID_Vendedor (Chave Estrangeira referenciando a tabela de Vendedores)

Fornecedores

* ID_Fornecedor (Chave Primária)
* Nome_do_Fornecedor
* Endereço_do_Fornecedor
* Número_de_Telefone_do_Fornecedor
* Email_do_Fornecedor

Vendedores

* ID_Vendedor (Chave Primária)
* Nome_do_Vendedor
* ID_Funcionario (Chave Estrangeira referenciando a tabela de Funcionários)

Funcionários

* ID_Funcionario (Chave Primária)
* Nome_do_Funcionario
* Cargo
* Salário
* Data_de_Admissão

Relacionamentos:

Um fornecedor pode fornecer múltiplos itens de inventário, mas cada item de inventário é 
fornecido por apenas um fornecedor. (Relacionamento um para muitos entre Fornecedores e 
Inventário)

Um cliente pode fazer várias compras, mas cada compra é feita por apenas um cliente. 
(Relacionamento um para muitos entre Clientes e Vendas)

Cada venda inclui vários itens de inventário, e cada item de inventário pode estar presente em 
várias vendas. (Relacionamento muitos para muitos entre Vendas e Inventário)

Um vendedor pode fazer várias vendas, mas cada venda é realizada por apenas um vendedor. 
(Relacionamento um para muitos entre Vendedores e Vendas)

Cada vendedor é associado a apenas um funcionário. (Relacionamento um para um entre 
Funcionários e Vendedores)

Este modelo lógico de banco de dados reflete as entidades principais e seus relacionamentos 
no contexto da BikeShop, permitindo a organização eficiente dos dados e a realização de 
operações de negócios necessárias

### Modelo Conceitual

!["Modelo conceitual de banco de dados"](estcaso-conceitual.png)

### Modelo Lógico

!["Modelo lógico de banco de dados"](estcaso-logico.png)

```sql
-- MySQL Workbench Forward Engineering

SET @OLD_UNIQUE_CHECKS=@@UNIQUE_CHECKS, UNIQUE_CHECKS=0;
SET @OLD_FOREIGN_KEY_CHECKS=@@FOREIGN_KEY_CHECKS, FOREIGN_KEY_CHECKS=0;
SET @OLD_SQL_MODE=@@SQL_MODE, SQL_MODE='ONLY_FULL_GROUP_BY,STRICT_TRANS_TABLES,NO_ZERO_IN_DATE,NO_ZERO_DATE,ERROR_FOR_DIVISION_BY_ZERO,NO_ENGINE_SUBSTITUTION';

-- -----------------------------------------------------
-- Schema mydb
-- -----------------------------------------------------

-- -----------------------------------------------------
-- Schema mydb
-- -----------------------------------------------------
CREATE SCHEMA IF NOT EXISTS `mydb` DEFAULT CHARACTER SET utf8 ;
SHOW WARNINGS;
USE `mydb` ;

-- -----------------------------------------------------
-- Table `mydb`.`Fornecedores`
-- -----------------------------------------------------
CREATE TABLE IF NOT EXISTS `mydb`.`Fornecedores` (
  `idfornecedores` INT NOT NULL AUTO_INCREMENT,
  `nomedofornecedor` VARCHAR(50) NOT NULL,
  `enderecodofornecedor` VARCHAR(250) NOT NULL,
  `numerotelefonefornecedor` VARCHAR(15) NOT NULL,
  `emailfornecedor` VARCHAR(100) NOT NULL,
  PRIMARY KEY (`idfornecedores`),
  UNIQUE INDEX `emailfornecedor_UNIQUE` (`emailfornecedor` ASC) VISIBLE)
ENGINE = InnoDB;

SHOW WARNINGS;

-- -----------------------------------------------------
-- Table `mydb`.`Inventario`
-- -----------------------------------------------------
CREATE TABLE IF NOT EXISTS `mydb`.`Inventario` (
  `idinventario` INT NOT NULL AUTO_INCREMENT,
  `modelo` VARCHAR(70) NOT NULL,
  `marca` VARCHAR(50) NOT NULL,
  `quantidade` INT NOT NULL,
  `preco` DECIMAL(10,2) NOT NULL,
  `Fornecedores_idfornecedores` INT NOT NULL,
  PRIMARY KEY (`idinventario`, `Fornecedores_idfornecedores`),
  INDEX `fk_Inventario_Fornecedores_idx` (`Fornecedores_idfornecedores` ASC) VISIBLE,
  CONSTRAINT `fk_Inventario_Fornecedores`
    FOREIGN KEY (`Fornecedores_idfornecedores`)
    REFERENCES `mydb`.`Fornecedores` (`idfornecedores`)
    ON DELETE NO ACTION
    ON UPDATE NO ACTION)
ENGINE = InnoDB;

SHOW WARNINGS;

-- -----------------------------------------------------
-- Table `mydb`.`Vendas`
-- -----------------------------------------------------
CREATE TABLE IF NOT EXISTS `mydb`.`Vendas` (
  `idvendas` INT NOT NULL AUTO_INCREMENT,
  `data` DATE NOT NULL,
  `quantidadevendida` INT NOT NULL,
  `precototal` DECIMAL(10,2) NOT NULL,
  `metodopagamento` VARCHAR(30) NOT NULL,
  PRIMARY KEY (`idvendas`))
ENGINE = InnoDB;

SHOW WARNINGS;

-- -----------------------------------------------------
-- Table `mydb`.`Clientes`
-- -----------------------------------------------------
CREATE TABLE IF NOT EXISTS `mydb`.`Clientes` (
  `idcliente` INT NOT NULL AUTO_INCREMENT,
  `nome` VARCHAR(50) NOT NULL,
  `endereco` VARCHAR(250) NOT NULL,
  `numerodetelefone` VARCHAR(15) NOT NULL,
  `email` VARCHAR(100) NOT NULL,
  `Vendas_idvendas` INT NOT NULL,
  PRIMARY KEY (`idcliente`, `Vendas_idvendas`),
  UNIQUE INDEX `email_UNIQUE` (`email` ASC) VISIBLE,
  INDEX `fk_Clientes_Vendas1_idx` (`Vendas_idvendas` ASC) VISIBLE,
  CONSTRAINT `fk_Clientes_Vendas1`
    FOREIGN KEY (`Vendas_idvendas`)
    REFERENCES `mydb`.`Vendas` (`idvendas`)
    ON DELETE NO ACTION
    ON UPDATE NO ACTION)
ENGINE = InnoDB;

SHOW WARNINGS;

-- -----------------------------------------------------
-- Table `mydb`.`Vendedores`
-- -----------------------------------------------------
CREATE TABLE IF NOT EXISTS `mydb`.`Vendedores` (
  `idvendedores` INT NOT NULL AUTO_INCREMENT,
  `nomevendendor` VARCHAR(50) NOT NULL,
  `Vendas_idvendas` INT NOT NULL,
  PRIMARY KEY (`idvendedores`, `Vendas_idvendas`),
  INDEX `fk_Vendedores_Vendas1_idx` (`Vendas_idvendas` ASC) VISIBLE,
  CONSTRAINT `fk_Vendedores_Vendas1`
    FOREIGN KEY (`Vendas_idvendas`)
    REFERENCES `mydb`.`Vendas` (`idvendas`)
    ON DELETE NO ACTION
    ON UPDATE NO ACTION)
ENGINE = InnoDB;

SHOW WARNINGS;

-- -----------------------------------------------------
-- Table `mydb`.`Funcionario`
-- -----------------------------------------------------
CREATE TABLE IF NOT EXISTS `mydb`.`Funcionario` (
  `idfuncionario` INT NOT NULL AUTO_INCREMENT,
  `nomefuncionario` VARCHAR(50) NOT NULL,
  `cargo` VARCHAR(30) NOT NULL,
  `salario` DECIMAL(10,2) NOT NULL,
  `dataadmissao` DATE NOT NULL,
  `Vendedores_idvendedores` INT NOT NULL,
  `Vendedores_Vendas_idvendas` INT NOT NULL,
  PRIMARY KEY (`idfuncionario`, `Vendedores_idvendedores`, `Vendedores_Vendas_idvendas`),
  INDEX `fk_Funcionario_Vendedores1_idx` (`Vendedores_idvendedores` ASC, `Vendedores_Vendas_idvendas` ASC) VISIBLE,
  CONSTRAINT `fk_Funcionario_Vendedores1`
    FOREIGN KEY (`Vendedores_idvendedores` , `Vendedores_Vendas_idvendas`)
    REFERENCES `mydb`.`Vendedores` (`idvendedores` , `Vendas_idvendas`)
    ON DELETE NO ACTION
    ON UPDATE NO ACTION)
ENGINE = InnoDB;

SHOW WARNINGS;

-- -----------------------------------------------------
-- Table `mydb`.`Vendas_has_Inventario`
-- -----------------------------------------------------
CREATE TABLE IF NOT EXISTS `mydb`.`Vendas_has_Inventario` (
  `Vendas_idvendas` INT NOT NULL,
  `Inventario_idinventario` INT NOT NULL,
  `Inventario_Fornecedores_idfornecedores` INT NOT NULL,
  PRIMARY KEY (`Vendas_idvendas`, `Inventario_idinventario`, `Inventario_Fornecedores_idfornecedores`),
  INDEX `fk_Vendas_has_Inventario_Inventario1_idx` (`Inventario_idinventario` ASC, `Inventario_Fornecedores_idfornecedores` ASC) VISIBLE,
  INDEX `fk_Vendas_has_Inventario_Vendas1_idx` (`Vendas_idvendas` ASC) VISIBLE,
  CONSTRAINT `fk_Vendas_has_Inventario_Vendas1`
    FOREIGN KEY (`Vendas_idvendas`)
    REFERENCES `mydb`.`Vendas` (`idvendas`)
    ON DELETE NO ACTION
    ON UPDATE NO ACTION,
  CONSTRAINT `fk_Vendas_has_Inventario_Inventario1`
    FOREIGN KEY (`Inventario_idinventario` , `Inventario_Fornecedores_idfornecedores`)
    REFERENCES `mydb`.`Inventario` (`idinventario` , `Fornecedores_idfornecedores`)
    ON DELETE NO ACTION
    ON UPDATE NO ACTION)
ENGINE = InnoDB;

SHOW WARNINGS;

SET SQL_MODE=@OLD_SQL_MODE;
SET FOREIGN_KEY_CHECKS=@OLD_FOREIGN_KEY_CHECKS;
SET UNIQUE_CHECKS=@OLD_UNIQUE_CHECKS;

```