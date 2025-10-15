SET UP GitHub ACTIONS IN CI/CD PIPELINE (LINT + TEST)

Purpose: CI/CD Pipeline with github Actions for a forex landing page.HTML.
This project demonstrates a basic DevSecOps CI/CD pipeline using GitHub Actions. The pipeline is configured to automatically lint and test a HMTL application upon every push and pull request to the main branch. This ensures code quality and health before merging.

List of key learning goals.
Example:
•	Learn how to automate security testing in CI/CD.
•	Understand basic container security using Trivy.
•	Practice identifying and remediating SQL Injection (SQLi) and XSS vulnerabilities.

Tools & Environment Setup
Describe the tools you used and how you set up your lab.
Example:
Tool	Purpose
GitHub Actions	CI/CD automation
Docker	Containerization
Trivy	Image vulnerability scanner
OWASP Juice Shop	Vulnerable web app for testing
DVWA	Practice app for SQLi/XSS
VS Code	Code editing

2. How It Works: The Pipeline Breakdown
This is the core of my  documentation .I explained what the pipeline does step-by-step. And even include a simplified version of the YAML workflow file to illustrate the process.
How It Works
The entire CI/CD process is defined in the .github/workflows/superlinter.yml
Trigger: The workflow runs automatically on two events:
•	A push to the main branch.
•	A pull_request targeting the main branch.
Pipeline Steps: The workflow consists of a single job called build-and-test that performs the following steps:
1.	Checkout Code: It first checks out the repository's code.
2.	Lint Code: It executes the linting command (e.g., npm run lint) to check for code style and formatting errors. This is our first "Sec" step (Static Analysis).
3.	Run Tests: If linting passes, it executes the unit tests (e.g., npm run test) to ensure all functionality works as expected.
Here is a simplified look at the workflow file:
YAML
# ./GitHubworkflows/ci.yml
name: CI Pipeline

on:
  push:
    branches: [ main ]
  pull_request:
    branches: [ main ]

jobs:
  build-and-test:
    runs-on: ubuntu-latest
    steps:
    - name: Checkout Code
      uses: actions/checkout@v3

    - name: Setup Node.js
      uses: actions/setup-node@v3
      with:
        node-version: '18'

    - name: Install Dependencies
      run: npm install

    - name: Run Linter (ESLint)
      run: npm run lint

    - name: Run Unit Tests (Jest)
      run: npm run test



Setup and Configuration
Provide clear, numbered steps on how someone can set up this project in their own repository.
Example:
Setup and Configuration
To use this CI/CD pipeline in your own project, follow these steps:
1.	Create Workflow Directory: In your project's root, create a directory structure: .GitHub/workflows/.
2.	Add Workflow File: Copy the contents of the superlinter.yml from this repository into a new file named superlinter.yml inside the .github/workflows/ directory.
3.	Configure main.html: Ensure your package.json file has the necessary lint and test scripts. For example:
4.	Add Linter and Test Configurations: Make sure you have the necessary configuration files for your linter and test runner.

 How to Use
Once the setup is complete, the pipeline will work automatically.
1.	Make a change to your code.
2.	Commit and push the change to your repository or open a pull request.
3.	Go to the "Actions" tab in your GitHub repository to see the workflow run in real-time.
4.	You will see a green checkmark if all steps (linting and testing) pass, or a red X if any step fails.



