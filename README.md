CREATE DATABASE IF NOT EXISTS SistemaFacturacion;

USE SistemaFacturacion;

CREATE TABLE Cliente (
    id INT AUTO_INCREMENT PRIMARY KEY,
    nombre VARCHAR(100) NOT NULL,
    tipo_cliente ENUM('Bajo Consumidor', 'Medio Consumidor', 'Alto Consumidor') NOT NULL
);

CREATE TABLE Medidor (
    id INT AUTO_INCREMENT PRIMARY KEY,
    cliente_id INT,
    numero_medidor VARCHAR(20) NOT NULL,
    ubicacion VARCHAR(100),
    FOREIGN KEY (cliente_id) REFERENCES Cliente(id)
);


CREATE TABLE Tarifa (
    id INT AUTO_INCREMENT PRIMARY KEY,
    tipo_cliente ENUM('Bajo Consumidor', 'Medio Consumidor', 'Alto Consumidor') NOT NULL,
    precio FLOAT NOT NULL
);

CREATE TABLE Consumo (
    id INT AUTO_INCREMENT PRIMARY KEY,
    medidor_id INT,
    lectura_id INT,
    tarifa_id INT,
    consumo FLOAT NOT NULL,
    FOREIGN KEY (medidor_id) REFERENCES Medidor(id),
    FOREIGN KEY (lectura_id) REFERENCES Lectura(id),
    FOREIGN KEY (tarifa_id) REFERENCES Tarifa(id)
);

CREATE TABLE Cargo (
    id INT AUTO_INCREMENT PRIMARY KEY,
    descripcion VARCHAR(100) NOT NULL,
    monto FLOAT NOT NULL
);

CREATE TABLE Factura (
    id INT AUTO_INCREMENT PRIMARY KEY,
    cliente_id INT,
    total_factura FLOAT NOT NULL,
    fecha_emision DATE NOT NULL,
    fecha_vencimiento DATE NOT NULL,
    FOREIGN KEY (cliente_id) REFERENCES Cliente(id)
);

-- Insertar cliente
INSERT INTO Cliente (nombre, tipo_cliente) VALUES ('Cliente A', 'Bajo Consumidor');
-- Insertar medidor asociado al cliente
INSERT INTO Medidor (cliente_id, numero_medidor, ubicacion) VALUES (1, 'M001', 'Ubicación 1');
-- Insertar tarifa para cliente bajo consumidor
INSERT INTO Tarifa (tipo_cliente, precio) VALUES ('Bajo Consumidor', 0.15);
-- Insertar consumo asociado a un medidor y una lectura específica
INSERT INTO Consumo (medidor_id, lectura_id, tarifa_id, consumo) VALUES (1, 1, 1, 50.5);





