# Pipeline Deployment & Initial Setup

Once the CLI binary is installed, follow these steps to initialize your working directory, configure cloud authentication, and execute a test pipeline.

---

## 1. Directory Initialization

Navigate to your working project directory and initialize a new pipeline configuration.

```bash
mkdir my-data-pipeline
cd my-data-pipeline
data-cli init

```

This command creates a standard configuration workspace containing a default `pipeline.config.yaml` file.

---

## 2. Environment Configuration

To prevent exposing credentials, set your API token and environment endpoint as local environment variables rather than hardcoding them into configuration files.

Run the following commands in your shell session, or add them to your profile:

```bash
export CLOUD_DATA_API_KEY="your_api_key_here"
export CLOUD_DATA_ENV="production"

```

To verify that your environment variables are correctly assigned:

```bash
data-cli auth check

```

---

## 3. Pipeline Configuration (`pipeline.config.yaml`)

Open `pipeline.config.yaml` in your text editor and define your source and destination parameters. Below is a sample configuration for a standard streaming pipeline:

```yaml
version: "1.0"
pipeline:
  name: "daily_customer_telemetry"
  batch_size: 5000
  retry_limit: 3

source:
  type: "local_stream"
  path: "/var/log/telemetry/*.json"

destination:
  endpoint: "[https://ingest.clouddata.example.com/v1/telemetry](https://ingest.clouddata.example.com/v1/telemetry)"
  compression: "gzip"

```

---

## 4. Execution & Connectivity Test

Run a dry-run test to validate your configuration, IAM permissions, and network route without pushing production data:

```bash
data-cli pipeline test --config pipeline.config.yaml

```

If the connection is successful, execute the pipeline:

```bash
data-cli pipeline run --config pipeline.config.yaml

```

---

## Troubleshooting Execution Failures

* **`ERR_UNAUTHORIZED (401)`**: Verify that your `CLOUD_DATA_API_KEY` is active and carries the `DataIngestWriter` permission.
* **`ERR_CONNECTION_TIMEOUT`**: Ensure outbound traffic over **Port 443** is allowed by your network firewall.
