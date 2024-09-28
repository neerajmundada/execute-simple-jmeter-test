# JMeter Load Testing with Docker and GitHub Actions

This repository demonstrates how to perform load testing using JMeter in a Docker container, integrated with GitHub Actions for continuous integration and deployment (CI/CD) workflows.

## Table of Contents

- [Features](#features)
- [Project Structure](#project-structure)
- [Setup Instructions](#setup-instructions)
- [Running the Tests](#running-the-tests)
- [Viewing Results](#viewing-results)
- [Customization](#customization)
- [Prerequisites](#prerequisites)
- [License](#license)

## Features

- Run load tests using JMeter.
- Utilize Docker to containerize the JMeter environment.
- Trigger tests automatically using GitHub Actions.
- Specify custom parameters for the number of users, iterations, and timing directly from the GitHub Actions interface.
- Generate detailed test reports.

## Project Structure

```
/my-jmeter-load-testing-project
│
├── google_search.jmx                # JMeter test plan
├── docker-compose.yml               # Docker Compose configuration for JMeter
├── .github
│   └── workflows
│       └── jmeter-workflow.yml      # GitHub Actions workflow for executing the test
└── README.md                        # Project documentation
```

## Setup Instructions

1. **Clone the Repository**
   ```bash
   git clone <repository-url>
   cd <repository-directory>
   ```

2. **Modify JMeter Test Plan (Optional)**
   - Open `google_search.jmx` in JMeter to customize the test parameters or add additional requests.

3. **Docker Configuration**
   - The `docker-compose.yml` file is used to set up the JMeter environment. No external services are required.

## Running the Tests

### Manual Trigger via GitHub Actions

1. Navigate to the **Actions** tab in your GitHub repository.
2. Select the **Execute JMeter Test** workflow.
3. Click on **Run workflow**.
4. Provide the following inputs:
   - **users**: Number of virtual users for the test (default: 1).
   - **iterations**: Number of iterations each user will perform (default: 5).
   - **constant_time**: Constant wait time between iterations in milliseconds (default: 1000).
   - **random_time**: Random wait time between transactions in milliseconds (default: 10000).
   - **random_time_variance**: Variance for random wait time in milliseconds (default: 3000).
   - **wait_time**: Time to wait before shutting down the test (default: 2 minutes).

### Running Locally with Docker Compose

1. Ensure Docker and Docker Compose are installed on your machine.
2. Build and run the JMeter Docker container:
   ```bash
   docker-compose up
   ```

3. The JMeter test will execute based on the configuration specified in `google_search.jmx`.

## Viewing Results

- Test results will be saved in the `results` directory, which will include:
  - `results.jtl`: Raw test results in JMeter's format.
  - `html_report`: An HTML report generated from the test execution.

To view the generated HTML report, open the `index.html` file located in the `results/html_report` directory in a web browser.

## Customization

You can customize the following parameters in the GitHub Actions workflow:

- **`users`**: Number of virtual users to simulate during the test.
- **`iterations`**: Number of iterations for each user.
- **`constant_time`**: Fixed wait time between requests (in milliseconds).
- **`random_time`**: Random wait time for transactions (in milliseconds).
- **`random_time_variance`**: Variance for the random time (in milliseconds).
- **`wait_time`**: Duration in minutes before stopping the test execution.

### Modifying JMeter Test Plan

To change the parameters directly in the JMeter test plan (`google_search.jmx`):

1. Open the file in JMeter.
2. Update the values under **User Defined Variables** as needed.
3. Save the file.

## Prerequisites

- **Docker**: Ensure Docker is installed and running on your machine.
- **Docker Compose**: Required for managing multi-container Docker applications.
- **GitHub Account**: To utilize GitHub Actions for CI/CD.

## License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.
