# Creación de tablas en Aurora serverless

Para la creación de las tablas en auroraserverless se establece con los siguientes DDL's

```sql

drop table DBName.Users;
CREATE TABLE IF NOT EXISTS DBName.Users (
    id INT AUTO_INCREMENT PRIMARY KEY,
    email VARCHAR(255) NOT NULL,
    name VARCHAR(255) NOT NULL,
    lastName VARCHAR(255) NOT NULL,
    phone VARCHAR(30) NOT NULL,
    password VARCHAR(255) NOT NULL,
    rol VARCHAR(10) NULL,
    lastState VARCHAR(255) NULL,
    position VARCHAR(255) NULL,
  	updated TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
    created TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
    Dashboard boolean NULL,
    Chat boolean NULL,
    Reportes boolean NULL,
    Respuestas boolean NULL,
    MiCuenta boolean NULL,
    RecuperarPsswrd boolean NULL,
    Consultar boolean NULL,
    Nuevo boolean NULL,
    sessionId VARCHAR(255) NULL
);

drop table DBName.Conversations;
CREATE TABLE IF NOT EXISTS DBName.Conversations (
    id INT AUTO_INCREMENT PRIMARY KEY,
    sessionId VARCHAR(255) NULL,
    lastState VARCHAR(255) NULL,
    intent VARCHAR(255) NULL,
    lastQuestion int(11) NULL,
    startConversation TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
    endConversation TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
    updated TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
    created TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
    agent VARCHAR(255) NULL
);

drop table DBName.Reports;
CREATE TABLE IF NOT EXISTS DBName.Reports (
    id INT AUTO_INCREMENT PRIMARY KEY,
    reportId VARCHAR(255) NOT NULL,
    agent VARCHAR(255) NOT NULL,
    comment text NOT NULL,
    priorityAttention boolean NULL,
    processStatus VARCHAR(255) NOT NULL,
    updated TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
    created TIMESTAMP DEFAULT CURRENT_TIMESTAMP
);
drop table DBName.Historic;
CREATE TABLE IF NOT EXISTS DBName.Historic (
    id INT AUTO_INCREMENT PRIMARY KEY,
    sessionId VARCHAR(255) NOT NULL,
    mensaje text NULL,
    tipo VARCHAR(255) NOT NULL,
    registro TIMESTAMP DEFAULT CURRENT_TIMESTAMP
);

```  

Diagrama Entidad-Relacion  
 
