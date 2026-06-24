# CI/CD Event Log Generation

Standalone synthetic CI/CD event log generator extracted from the observability platform.

## What Is Included

- `kafka/event_generator/generator.py` generates realistic CI/CD pipeline events.
- `kafka/producer/producer.py` publishes generated events to Kafka.
- `services/event_schema.py` validates and normalizes event payloads.
- `docker-compose.yml` starts local Kafka, Zookeeper, and Kafka UI for testing.

## Setup

```bash
python -m venv .venv
source .venv/bin/activate
pip install -r requirements.txt
```

## Generate JSONL Events

```bash
python kafka/event_generator/generator.py --count 100000 --output database/sample_cicd_events.jsonl
```

## Publish Events To Kafka

Start Kafka:

```bash
docker-compose up -d
```

Create or verify the topic:

```bash
docker-compose exec kafka kafka-topics --bootstrap-server kafka:29092 --create --if-not-exists --topic cicd-events --partitions 6 --replication-factor 1
```

Publish events:

```bash
python kafka/event_generator/generator.py --count 100000 --to-kafka --rate 1000
```

Kafka UI is available at http://localhost:8080.

