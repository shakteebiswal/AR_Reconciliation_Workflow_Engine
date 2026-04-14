# AR_Reconciliation_Workflow_Engine
High-performance AR Reconciliation Engine using FastAPI &amp; SQLAlchemy. An event-driven, micro-batch processing engine which features a multi-threaded Saga-pattern orchestrator for resilient, stateful financial auditing ensuring state persistence, idempotency, and parallel execution.

# Key Features
## Parallel Processing:
Uses a ThreadPoolExecutor with 20 workers for high-throughput I/O.

## State Persistence:
Atomic commits to PostgreSQL after every stage (Matching, Validation, Routing).

## Fault Tolerance:
Ability to resume halted workflows from the exact last successful stage.

## Observability:
REST endpoints to monitor real-time batch progress.

# Setup & Security (Required)
To run this project in Google Colab and access the FastAPI dashboard via a public URL, you must configure a private ngrok tunnel.

## 1. Generate an ngrok Token
Go to ngrok.com and create a free account.

Navigate to your Dashboard and select Your Authtoken.

Copy the alphanumeric token provided.

## 2. Configure Colab Secrets (🔑)
To keep your token secure and private, this notebook uses Google Colab's Secrets feature. Do not paste your token directly into the code.

Open the notebook in Google Colab.

Click the Key icon (Secrets) in the left-hand sidebar.

Click + Add new secret.

Set the Name to: NGROK_TOKEN

Set the Value to: (Paste your authtoken here).

Important: Toggle the Notebook access switch to ON.

## Architecture
<img width="1408" height="768" alt="ai_backend_engineer_assignment_dataset architecture" src="https://github.com/user-attachments/assets/d86d2e52-b6fa-4c85-8429-10d51c9a0f69" />

#### Ingestion:
API receives a batch of records.

#### Dispatch:
Records are queued into the Thread Pool.

#### Orchestration:
Each thread manages a unique state machine for a record.

#### Persistence:
Progress is saved to PostgreSQL at every step to prevent data loss.

## API Endpoints
Once the ngrok tunnel is live, you can interact with the engine using:

#### POST /trigger-batch:
Starts the reconciliation process for the loaded dataset.

#### GET /summary:
Returns a live count of records in each processing stage (Ingested, Matched, Validated, Completed).

## Tech Stack
#### Framework:
FastAPI

#### Database:
PostgreSQL & SQLAlchemy

#### Concurrency:
Python ThreadPoolExecutor

#### Tunneling:
Pyngrok

## Data Handling: Pandas



