<img width="1314" height="186" alt="image" src="https://github.com/user-attachments/assets/03c812a3-579f-49a5-9823-2efaec055ad2" />



RahasyaScan is an all-in-one DevSecOps security scanning toolkit designed to automatically detect hardcoded secrets, exposed credentials, and vulnerable dependencies across source code repositories.

Built for local use, Docker, and CI/CD pipelines, RahasyaScan unifies multiple industry-trusted security tools into a single, automated, developer-friendly scanner.

“If it’s exposed — it’s already compromised.”

**_🔍 What RahasyaScan Solves_**

Modern codebases often suffer from:

 - Hardcoded API keys & secrets

 - Leaked credentials in Git history

 - Vulnerable open-source dependencies

 - Missing security visibility in CI/CD

RahasyaScan addresses this by combining Secrets Detection + Software Composition Analysis (SCA) into a single execution flow.

**⚙️ Requirements**
Local System

 - Docker ≥ 20.x

 - Git

 - Internet access (for tool updates & Snyk)

Supported Platforms

 - Linux

 - macOS

 - Windows (via Docker Desktop)

❗ No language runtime needed on host — everything runs inside Docker.

**_🚀 Features (In-Depth)_**
🔐 Secrets Detection

RahasyaScan integrates multiple scanners to minimize false negatives:

Tool	Purpose
Gitleaks	Detects secrets in Git history and working tree
GittyLeaks	Pattern-based secret discovery
TruffleHog	Entropy-based secret scanning
Detect-Secrets	Yelp’s high-confidence secret scanner
GitGuardian (ggshield)	Enterprise-grade secret detection
Talisman	Git hook-style deep secret scanning with HTML report
📦 Dependency Vulnerability Scanning (SCA)

Snyk scans:

 - All supported package managers

 - Multiple languages in monorepos

 - Known CVEs with severity filtering

 - Token is securely requested at runtime

 - No credentials are stored permanently
 

**_📊 Unified Results Output_**

 - All scan outputs are saved to: /repo/Secret_Detection_Reports/




_Easy integration with:_

 - CI artifacts

 - SIEM tools

 - Security dashboards
 

🧠 DevSecOps-Ready Design

 - Containerized

 - Non-intrusive

 - CI/CD friendly

 - Shift-Left security aligned


**_📥 Installation_**

 
1️⃣ Installation 🐳 (Docker-Based — No Local Setup Pain)
https://docs.docker.com/get-docker/

2️⃣ Pull RahasyaScan from Docker Hub
docker pull aniket2003/rahasyascan:v1.0.0

▶️ Running RahasyaScan (Local Scan)

Navigate to your project repository and run:

docker run -it \
  -v "$(pwd)":/repo \
  aniket2003/rahasyascan:v1.0.0


📌 This mounts your repository inside the container securely.

🧩 Available Scan Options

Once the tool starts, you’ll be prompted to choose scans.

  🔹 Run all secret-scanning tools
     -scan

  🔹 Run specific tools
    -scan gitleaks trufflehog ggshield

  🔹 Run dependency scanning (Snyk)
    -scan snyk


🔐 You’ll be securely prompted to enter your Snyk API token at runtime.

🔹 Include Talisman (pre-commit & repo scan)
-include_talisman

🧷 Available Tools
 Flag	Tool
 - gitleaks	Git history secret scanning
 - gittyleaks	Pattern-based detection
 - trufflehog	Entropy detection
 - detect-secrets	Yelp secrets detection
 - ggshield	GitGuardian scanning
 - talisman	Pre-commit style scanning
 - snyk	Dependency vulnerability scanning

🔑 Snyk Authentication Flow

  🔹Tokens are never hardcoded

  🔹Requested securely during runtime:

  🔹Enter your Snyk API Token:


Token is:

  🔹Used temporarily

  🔹Logged out after scan

  🔹Unset from environment

🎨 Customization
  🔹Add/Remove Tools

  🔹Edit /app/entrypoint.sh:

  🔹Add new scanners

  🔹Disable unused ones

  🔹Ignore Paths (TruffleHog)

  🔹Edit:/trufflehog_exclude.txt

  

**_CI/CD Integration_**

RahasyaScan is designed for:

  🔹GitHub Actions

  🔹GitLab CI

  🔹Jenkins

  🔹Azure DevOps

Example (GitHub Actions):

- name: Run RahasyaScan
  run: |
    docker run -v ${{ github.workspace }}:/repo aniketkasturi/rahasyascan

📦 What This Pipeline Does
On every push / PR

🔍 Secrets Scanning

Gitleaks,GittyLeaks,TruffleHog,Detect-Secrets


🧩 Dependency Scanning

Snyk (multi-language, all manifests)


📁 Artifacts

Unified reports uploaded for Security Team


🧠 Shift-Left Security - Vulnerabilities caught before merge


**_🛡 Security Philosophy_**

  🔹No secrets stored

  🔹No background services

  🔹No outbound telemetry

  🔹Fully transparent execution

**👤 Author**

Aniket Kasturi
Penetration Testing | Cloud Security | Offensive Security | DevSecOps

“Security is not a feature — it’s a mindset.”
<img width="1314" height="186" alt="image" src="https://github.com/user-attachments/assets/03c812a3-579f-49a5-9823-2efaec055ad2" />



RahasyaScan is an all-in-one DevSecOps security scanning toolkit designed to automatically detect hardcoded secrets, exposed credentials, and vulnerable dependencies across source code repositories.

Built for local use, Docker, and CI/CD pipelines, RahasyaScan unifies multiple industry-trusted security tools into a single, automated, developer-friendly scanner.

“If it’s exposed — it’s already compromised.”

**_🔍 What RahasyaScan Solves_**

Modern codebases often suffer from:

 - Hardcoded API keys & secrets

 - Leaked credentials in Git history

 - Vulnerable open-source dependencies

 - Missing security visibility in CI/CD

RahasyaScan addresses this by combining Secrets Detection + Software Composition Analysis (SCA) into a single execution flow.

**⚙️ Requirements**
Local System

 - Docker ≥ 20.x

 - Git

 - Internet access (for tool updates & Snyk)

Supported Platforms

 - Linux

 - macOS

 - Windows (via Docker Desktop)

❗ No language runtime needed on host — everything runs inside Docker.

**_🚀 Features (In-Depth)_**
🔐 Secrets Detection

RahasyaScan integrates multiple scanners to minimize false negatives:

Tool	Purpose
Gitleaks	Detects secrets in Git history and working tree
GittyLeaks	Pattern-based secret discovery
TruffleHog	Entropy-based secret scanning
Detect-Secrets	Yelp’s high-confidence secret scanner
GitGuardian (ggshield)	Enterprise-grade secret detection
Talisman	Git hook-style deep secret scanning with HTML report
📦 Dependency Vulnerability Scanning (SCA)

Snyk scans:

 - All supported package managers

 - Multiple languages in monorepos

 - Known CVEs with severity filtering

 - Token is securely requested at runtime

 - No credentials are stored permanently
 

**_📊 Unified Results Output_**

 - All scan outputs are saved to: /repo/Secret_Detection_Reports/




_Easy integration with:_

 - CI artifacts

 - SIEM tools

 - Security dashboards
 

🧠 DevSecOps-Ready Design

 - Containerized

 - Non-intrusive

 - CI/CD friendly

 - Shift-Left security aligned


**_📥 Installation_**

 
1️⃣ Installation 🐳 (Docker-Based — No Local Setup Pain)
https://docs.docker.com/get-docker/

2️⃣ Pull RahasyaScan from Docker Hub
docker pull aniket2003/rahasyascan:latest

▶️ Running RahasyaScan (Local Scan)

Navigate to your project repository and run:

docker run --rm -it -v "$(pwd)":/repo aniket2003/rahasyascan:latest


📌 This mounts your repository inside the container securely.

🧩 Available Scan Options

Once the tool starts, you’ll be prompted to choose scans.

  🔹 Run all secret-scanning tools
     -scan

  🔹 Run specific tools
    -scan gitleaks trufflehog ggshield

  🔹 Run dependency scanning (Snyk)
    -scan snyk


🔐 You’ll be securely prompted to enter your Snyk API token at runtime.

🔹 Include Talisman (pre-commit & repo scan)
-include_talisman

🧷 Available Tools
 Flag	Tool
 - gitleaks	Git history secret scanning
 - gittyleaks	Pattern-based detection
 - trufflehog	Entropy detection
 - detect-secrets	Yelp secrets detection
 - ggshield	GitGuardian scanning
 - talisman	Pre-commit style scanning
 - snyk	Dependency vulnerability scanning

🔑 Snyk Authentication Flow

  🔹Tokens are never hardcoded

  🔹Requested securely during runtime:

  🔹Enter your Snyk API Token:


Token is:

  🔹Used temporarily

  🔹Logged out after scan

  🔹Unset from environment

🎨 Customization
  🔹Add/Remove Tools

  🔹Edit /app/entrypoint.sh:

  🔹Add new scanners

  🔹Disable unused ones

  🔹Ignore Paths (TruffleHog)

  🔹Edit:/trufflehog_exclude.txt

  

**_CI/CD Integration_**

RahasyaScan is designed for:

  🔹GitHub Actions

  🔹GitLab CI

  🔹Jenkins

  🔹Azure DevOps

Example (GitHub Actions):

- name: Run RahasyaScan
  run: |
    docker run -v ${{ github.workspace }}:/repo aniketkasturi/rahasyascan

📦 What This Pipeline Does
On every push / PR

🔍 Secrets Scanning

Gitleaks,GittyLeaks,TruffleHog,Detect-Secrets


🧩 Dependency Scanning

Snyk (multi-language, all manifests)


📁 Artifacts

Unified reports uploaded for Security Team


🧠 Shift-Left Security - Vulnerabilities caught before merge


**_🛡 Security Philosophy_**

  🔹No secrets stored

  🔹No background services

  🔹No outbound telemetry

  🔹Fully transparent execution

**👤 Author**

Aniket Kasturi
Penetration Testing | Cloud Security | Offensive Security | DevSecOps

“Security is not a feature — it’s a mindset.”
