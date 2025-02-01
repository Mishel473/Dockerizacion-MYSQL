Ejercicio 1: Crear un contenedor con Docker-MySQL y persistir la información

PASOS PARA CREAR UN CONTENEDOR EN DOCKER

//docker run --name mysql-container -e MYSQL_ROOT_PASSWORD=tu_contraseña -e MYSQL_DATABASE=mi_base_datos -v mysql-data:/var/lib/mysql -d mysql:latest

//docker ps

//docker exec -it mysql-container mysql -uroot -p

Ejercicio 2: Dockerizando el servicio de MySQL Paso 1: Crear un archivo docker-compose.yml

///////////////////////////////////////////// version: '3.8' services: mysql: image: mysql:latest container_name: mysql-container environment: MYSQL_ROOT_PASSWORD: tu_contraseña MYSQL_DATABASE: mi_base_datos volumes: - mysql-data:/var/lib/mysql ports: - "3306:3306" volumes: mysql-data: ///////////////////////////////////////////////

//docker-compose up -d

//docker-compose ps

//docker-compose down

//docker-compose up -d

Ejercicio 3: Usar MySQL con Docker y Docker Compose

Creación de una Aplicación Node.js Paso 1: Crear el proyecto Node.js Inicia un proyecto Node.js:

/////////////////////// mkdir docker-mysql-node cd docker-mysql-node npm init -y ///////////////////

///npm install mysql2 express

///////////////////////////////////////

const express = require('express'); const mysql = require('mysql2');

const app = express(); const port = 3000;

// Conexión a la base de datos const db = mysql.createConnection({ host: 'localhost', // Cambiar si estás usando un contenedor separado user: 'root', password: 'tu_contraseña', database: 'mi_base_datos', });

db.connect((err) => { if (err) { console.error('Error conectando a la base de datos:', err); } else { console.log('Conectado a MySQL'); } });

app.get('/', (req, res) => { db.query('SELECT NOW() AS fecha', (err, results) => { if (err) { res.status(500).send('Error ejecutando la consulta'); } else { res.json(results); } }); });

app.listen(port, () => { console.log(Servidor escuchando en http://localhost:${port}); });

///////////////////////////////////////

//docker-compose up -d

//node index.js

//http://localhost:3000
