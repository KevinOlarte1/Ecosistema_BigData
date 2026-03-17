# 🚀 Ecosistema Big Data - HDFS Cluster

## 📌 Descripción

Este proyecto implementa un **clúster Hadoop HDFS** utilizando Docker, como base para un ecosistema Big Data orientado a la **migración de datos desde MySQL hacia HDFS y Hive mediante Sqoop**.

Actualmente, el proyecto incluye un clúster funcional con:

* 1 NameNode
* 2 DataNodes
* Replicación de datos configurada

---

## 🏗️ Arquitectura

El clúster está compuesto por los siguientes servicios:

* **NameNode**: nodo principal que gestiona el sistema de archivos
* **DataNode 1 y 2**: nodos encargados de almacenar los bloques de datos
* **Red Docker interna** para comunicación entre nodos

---

## ⚙️ Tecnologías utilizadas

* Apache Hadoop (HDFS)
* Docker & Docker Compose
* Linux

---

## 📂 Estructura del proyecto

```
Ecosistema_BigData/
│
├── containers/
│   ├── namenode/
│   └── datanode/
│
├── config/
│   └── hadoop/
│       └── hdfs-site.xml
│
├── docker-compose.yml
├── hadoop.env
└── README.md
```

---

## ▶️ Cómo ejecutar el proyecto

### 1. Clonar el repositorio

```bash
git clone https://github.com/KevinOlarte1/Ecosistema_BigData.git
cd Ecosistema_BigData
```

### 2. Levantar el clúster

```bash
docker compose down -v
docker compose up --build -d
```

### 3. Ver logs (opcional)

```bash
docker compose logs -f
```

---

## 🌐 Interfaz web

Puedes acceder al NameNode desde:

```
http://localhost:9870
```

Ahí podrás ver:

* DataNodes activos
* Uso de almacenamiento
* Estado del clúster

---

## ✅ Validación del clúster

### 1. Acceder al NameNode

```bash
docker exec -it namenode bash
```

### 2. Ver estado del clúster

```bash
hdfs dfsadmin -report
```

Deberías ver:

```
Live datanodes (2)
```

---

### 3. Prueba de escritura en HDFS

```bash
echo "hola hdfs" > prueba.txt

hdfs dfs -mkdir -p /test
hdfs dfs -put -f prueba.txt /test/

hdfs dfs -ls /test
hdfs dfs -cat /test/prueba.txt
```

---

### 4. Verificación de replicación

```bash
hdfs fsck /test/prueba.txt -files -blocks -locations
```

Resultado esperado:

* Factor de replicación: **2**
* Bloques distribuidos en los DataNodes

---

## 🎯 Objetivo del proyecto

Este clúster es la base para un pipeline completo de Big Data:

1. MySQL (fuente de datos)
2. Sqoop (ingestión de datos)
3. HDFS (almacenamiento distribuido)
4. Hive (consulta y análisis)

---

## 🚧 Próximos pasos

* [ ] Integrar contenedor MySQL
* [ ] Migrar datos con Sqoop
* [ ] Integrar Hive
* [ ] Crear consultas analíticas

---

## 👨‍💻 Autor

Kevin Olarte
Proyecto personal / académico de Big Data

---
