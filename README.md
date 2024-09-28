
# JMeter Performance Testing with Grafana Monitoring

This project demonstrates how to run a JMeter load test using GitHub Actions, while monitoring the test in real-time using Grafana and InfluxDB.

## Features
- Run a Google Search performance test using JMeter.
- Customize test parameters directly from GitHub Actions inputs:
  - Number of users
  - Number of iterations per user
  - Constant time between iterations
  - Random time and variance between transactions
- Real-time monitoring of test execution using Grafana and InfluxDB.
- Automatically stop Grafana and InfluxDB after a specified time (default: 2 minutes).

## Prerequisites
- **GitHub Actions**: No local setup required.
- **Docker**: Ensure Docker Compose is available in the environment for running Grafana and InfluxDB.

## Project Structure

```
/my-jmeter-grafana-project
│
├── google_search.jmx        # JMeter test plan
├── docker-compose.yml       # Docker Compose for InfluxDB and Grafana
├── .github
│   └── workflows
│       └── jmeter-workflow.yml  # GitHub Actions workflow for test execution
└── README.md               # Project documentation
```

## How to Run

1. **Fork the repository** or **clone it locally**.
2. **Customize the JMeter test** in `google_search.jmx`.
3. **Run the GitHub Actions workflow**:
   - Go to the "Actions" tab in your GitHub repository.
   - Select the "JMeter Test with Grafana Monitoring" workflow.
   - Enter the following inputs:
     - **users**: Number of virtual users for the test.
     - **iterations**: Number of iterations per user.
     - **constant_time**: Constant wait time between iterations (in milliseconds).
     - **random_time**: Random wait time between transactions (in milliseconds).
     - **random_time_variance**: Variance for the random time (in milliseconds).
     - **grafana_timeout**: Grafana shutdown time in minutes (default: 2 minutes).
   - Click "Run workflow".
4. **Monitor in Grafana**:
   - After starting the test, open Grafana at `http://localhost:3000` to monitor real-time results.
   - Default login for Grafana is `admin/admin`.
5. **View Test Results**:
   - Results are stored as artifacts in the GitHub workflow under the "Actions" tab.
   - Download them and view detailed reports using JMeter.

## Grafana and InfluxDB

- **InfluxDB** is used to store the JMeter test metrics.
- **Grafana** is used to visualize the metrics in real-time.
- Both services will automatically shut down after a specified time to save resources.

## Docker Compose

The `docker-compose.yml` file is placed in the root directory and is responsible for starting and stopping the Grafana and InfluxDB services.

## Customization

You can customize the following in the GitHub Actions workflow:

- **`users`**: Number of virtual users.
- **`iterations`**: Number of iterations per user.
- **`constant_time`**: Wait time after each iteration (default: 1000 ms).
- **`random_time`**: Wait time after each transaction (default: 10000 ms).
- **`random_time_variance`**: Variance for the random time (default: 3000 ms).
- **`grafana_timeout`**: Time to keep Grafana running after the test (default: 2 minutes).

## License

This project is licensed under the MIT License.
