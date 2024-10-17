# automated-sast-dast-ci-pipeline-sonarcloud-zap
Automated CI/CD pipeline integrating SAST (SonarCloud) and DAST (OWASP ZAP) using GitHub Actions for continuous vulnerability analysis in both code and application.

# Automated SAST and DAST CI Pipeline

This project demonstrates the integration of Static Application Security Testing (SAST) using SonarCloud and Dynamic Application Security Testing (DAST) using OWASP ZAP, automated through GitHub Actions in a CI/CD pipeline. The repository includes examples of workflow files for running these scans automatically for every push and pull request to the repository.

## Project Structure
- **src/**: Contains a simple HTML file representing the application being tested.
- **zap-scan-configs/**: Contains the OWASP ZAP scan configuration.
- **.github/workflows/**: Contains two workflow files: 
    - `sast-analysis.yml`: Configured to run SonarCloud analysis.
    - `dast-analysis.yml`: Configured to run OWASP ZAP scan.

## Tools Used
- **SonarCloud**: A cloud-based SAST tool for analyzing source code.
- **OWASP ZAP**: A DAST tool for scanning vulnerabilities in web applications.
- **GitHub Actions**: Used to automate the scanning processes in a CI/CD pipeline.

## Getting Started
1. **Fork this repository** to use as a template for your own security testing pipeline.
2. **Configure SonarCloud**:
    - Create an account on [SonarCloud](https://sonarcloud.io/) and link it to this GitHub repository.
    - Generate a `SONAR_TOKEN` in SonarCloud and add it to your GitHub repository as a secret (`SONAR_TOKEN`).
3. **OWASP ZAP Setup**:
    - The `zap-scan-configs/zap-config.xml` file contains the OWASP ZAP configuration for the DAST analysis. Adjust it based on your requirements.
4. **GitHub Actions**:
    - GitHub Actions will run the SAST scan with SonarCloud and DAST scan with OWASP ZAP automatically for every push or pull request to the repository.

## License
This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

