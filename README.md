https://img.shields.io/github/last-commit/ifaakash/APM/main  
https://img.shields.io/badge/Maintained-Yes-Green

# Local Setup Guide

To set up the monitoring stack locally, follow these steps:

1. **Clone the repository** and navigate to the root directory.

2. **Start the Docker containers**:
   ```bash
   docker compose --file docker-compose.yml up --build -d
   ```

3. **Access Grafana**:
   - Open your browser and go to `http://localhost:3000`.
   - Log in with the default credentials:
     - **Username:** `admin`
     - **Password:** `admin`
   - You will be prompted to change the password on first login.

4. **Configure Loki as a data source in Grafana**:
   - Go to **Configuration** → **Data Sources** → **Add data source**.
   - Select **Loki**.
   - Set the URL to `http://loki:3100`.
   - Click **Save & Test**.

5. **Explore logs**:
   - Go to **Explore** (compass icon).
   - Select the **Loki** data source.
   - Use LogQL queries to view logs. For example:
     ```
     {container="grafana"}   # Logs from the Grafana container
     {job="docker"}          # All Docker logs
     {service="loki"}        # Logs from the Loki service
     ```

## Verification and Debugging

To ensure everything is working correctly, run the following checks:

- **Check container status**:
  ```bash
  docker-compose ps
  # Should show all containers running
  ```

- **Verify Promtail is scraping logs**:
  ```bash
  curl http://localhost:9080/metrics
  ```

- **Confirm Loki is ready**:
  ```bash
  curl http://localhost:3100/ready
  ```
