# Stream-to-warehouse-poc
A fully containerized real-time analytics stack featuring a Python-based clickstream generator, Redpanda (Kafka-compatible) message broker, and RisingWave streaming database. This POC demonstrates sub-second SQL windowing and incremental materialized views on live IOT-style data.

# Project Architecture
This project simulates a production-grade data pipeline where user-click events are captured, buffered, and analyzed in real-time.

# ad-click-gen:
A Python producer (containerized) that generates synthetic ad-click events and pushes them to Redpanda.

# redpanda: 
A high-performance, Kafka-compatible message broker that handles the event stream.

# risingwave: 
The streaming database that consumes the stream to perform real-time SQL transformations.

# Quick Start
Spin up the stack:

Bash

docker-compose up -d
Verify the Healthcheck: The ad-click-gen service waits for Redpanda to be fully healthy before starting the Python script.

Analyze Data: Connect any Postgres-compatible tool (DBeaver/pgAdmin) to localhost:4566.

# Key Technical Implementation
Healthcheck Dependencies: Utilized Docker healthcheck and service_healthy conditions to ensure service stability and prevent producer "cold-start" failures.

# Resource Management: 
Optimized Redpanda for local development using --overprovisioned and --smp 1 flags to run efficiently on a single machine.

# Streaming Logic:

# Tumble Windows: 
For hourly non-overlapping click reports.

# Hopping Windows: 
For 1-minute moving averages updated every 30 seconds to track traffic trends.

Infrastructure as Code
The entire environment is defined in docker-compose.yml, to manage networking, volumes, and service dependencies for complex data systems.
