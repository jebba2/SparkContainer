# SparkContainer

# Spark Docker Cluster (Python 3.11)

A containerized Apache Spark cluster designed for local development. This setup provides a scalable environment with a Spark Master and multiple Spark Workers, all running on **Python 3.11** and **Debian Bookworm**.

## 🚀 Quick Start

1. **Build and start the cluster** (with 3 workers):
```bash
docker-compose up -d --scale spark-worker=3

```


2. **Access the Web UIs**:
* **Spark Master UI**: [http://localhost:8081](https://www.google.com/search?q=http://localhost:8080)


3. **Shutdown the cluster**:
```bash
docker-compose down

```

## 🛠 Project Structure

```text
.
├── docker/
│   └── Dockerfile          # Python 3.11 + Java 17 + Spark 3.5.0
├── apps/                   # Place your PySpark scripts here
├── docker-compose.yml      # Cluster orchestration & resource limits
└── README.md

```

## ⚙️ Configuration

### Resource Limits

To ensure the cluster doesn't overwhelm your host machine, the following limits are applied via `docker-compose.yml`:

| Component | CPU Limit | RAM Limit | Spark Executor Memory |
| --- | --- | --- | --- |
| **Master** | 0.5 Core | 512 MB | N/A |
| **Worker** | 1.0 Core | 1.5 GB | 1 GB |

### Environment Details

* **Python**: 3.11-slim-bookworm
* **Java**: OpenJDK 17 (Headless)
* **Spark**: 3.5.0
* **Hadoop**: 3.x

## 📝 Running Jobs

To run a Python script located in your `./apps` folder on the cluster:

```bash
docker exec -it spark-master spark-submit \
  --master spark://spark-master:7077 \
  --deploy-mode client \
  /opt/spark/apps/your_script.py

```

## 🔧 Troubleshooting

* **Java Path Issues**: The Dockerfile creates a symlink at `/usr/lib/jvm/java-17-fixed` to ensure compatibility across different CPU architectures (AMD64/ARM64).
* **Missing Dependencies**: The image includes `procps` and `curl`, which are required for Spark's internal management scripts.

---
