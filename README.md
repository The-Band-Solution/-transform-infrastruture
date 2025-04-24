# 🧩 Immigrant Transform & Load Infrastructure

This project defines a **Docker Compose setup** for deploying two ETL transformation services: **SRO** and **CIRO**, each targeting different environments (*DevOps* and *GitLab*, respectively). These services handle **Kafka-based** event consumption, **data transformation**, and **loading into relational and MongoDB databases**.

---

## 🚀 Goal

To automate the transformation and loading of data from Kafka topics into appropriate databases using containerized ETL services for:

- **SRO** (DevOps Environment)
- **CIRO** (GitLab Environment)

---

## 📁 Project Structure

This Compose file provisions two services:

| Service | Description |
|---------|-------------|
| **SRO** | Transform and load component for the DevOps environment |
| **CIRO** | Transform and load component for the GitLab environment |

Each service is configured using environment-specific variables loaded from a `.env` file.

---

## ⚙️ Requirements

- Docker
- Docker Compose
- A pre-defined external Docker network called `base-infrastrutrure`

You can create the network (if not already created) with:

```bash
docker network create base-infrastrutrure
```

---

## 🧾 Environment Variables

Before starting the services, create a `.env` file in the project root and define the following variables:

```env
# DevOps Configuration
KAFKA_SERVER_DEVOPS=your.kafka.devops.server
KAFKA_PORT_DEVOPS=9092
DB_URL_DEVOPS=your-postgres-devops-url
DB_PORT_DEVOPS=5432
DB_NAME_DEVOPS=devops_db
DB_USERNAME_DEVOPS=user
DB_PASSWORD_DEVOPS=pass
SERVER_ETL_PORT_DEVOPS=8080
MONGO_HOST_DEVOPS=your.mongo.devops.host
MONGO_PORT_DEVOPS=27017
MONGO_DB_DEVOPS=devops_mongo_db

# GitLab Configuration
KAFKA_SERVER_GITLAB=your.kafka.gitlab.server
KAFKA_PORT_GITLAB=9092
DB_URL_GITLAB=your-postgres-gitlab-url
DB_PORT_GITLAB=5432
DB_NAME_GITLAB=gitlab_db
DB_USERNAME_GITLAB=user
DB_PASSWORD_GITLAB=pass
SERVER_ETL_PORT_GITLAB=8081
MONGO_HOST_GITLAB=your.mongo.gitlab.host
MONGO_PORT_GITLAB=27017
MONGO_DB_GITLAB=gitlab_mongo_db
```

---

## 🔧 Usage

To build and run the services:

```bash
docker compose up -d
```

Both services will run in detached mode and connect to the shared external network `base-infrastrutrure`.

---

## 🌐 Network Configuration

This stack connects to an **external Docker network**:

```yaml
networks:
  default:
    name: base-infrastrutrure
    external: true
```

Ensure the network exists beforehand, or modify the network section if you prefer internal Docker Compose networking.

---

## 📦 Images

Both services are pulled from the **GitLab Container Registry**:

- `registry.gitlab.com/immigrant-data-driven-development/etl/transform-and-load/sro`
- `registry.gitlab.com/immigrant-data-driven-development/etl/transform-and-load/ciro`

---

## ✉️ Maintainer

**Paulo Sérgio dos Santos Júnior**  
📧 [paulossjunior@gmail.com](mailto:paulossjunior@gmail.com)
