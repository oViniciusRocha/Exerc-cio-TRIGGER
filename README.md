# Exerc-cio-TRIGGER
create database pedido;
use pedido;

CREATE TABLE Pedidos(

IDPedido INT AUTO_INCREMENT PRIMARY KEY,

DataPedido DATETIME,

NomeClient VARCHAR (100)

);


INSERT INTO Pedidos (DataPedido, NomeCLiente) values

(NOW(),'CLiente 1'),

(NOW(),'CLiente 1'),

(NOW(),'CLiente 1');


DELIMITER $

CREATE TRIGGER RegistroDataCriacaoPedido

BEFORE INSERT ON Pedidos

FOR EACH ROW

BEGIN 

 SET NEW.DataPedido = NOW();
 
END;

$

DELIMITER ;v


este codigo cria uma tabela e um trigger, trigger este que estancia a data "DataPedido" a data atual da inserção.

-----------------------------------------------------------------------------------------------------------------------------------------





