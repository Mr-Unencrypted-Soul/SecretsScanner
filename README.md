☠️ RahasyaScan

RahasyaScan is an all-in-one DevSecOps security scanning toolkit designed to automatically detect hardcoded secrets, exposed credentials, and vulnerable dependencies across source code repositories.

Built for local use, Docker, and CI/CD pipelines, RahasyaScan unifies multiple industry-trusted security tools into a single, automated, developer-friendly scanner.

“If it’s exposed — it’s already compromised.”

🔍 What RahasyaScan Solves

Modern codebases often suffer from:

Hardcoded API keys & secrets

Leaked credentials in Git history

Vulnerable open-source dependencies

Missing security visibility in CI/CD

RahasyaScan addresses this by combining Secrets Detection + Software Composition Analysis (SCA) into a single execution flow.

⚙️ Requirements
Local System

Docker ≥ 20.x

Git

Internet access (for tool updates & Snyk)

Supported Platforms

Linux

macOS

Windows (via Docker Desktop)

❗ No language runtime needed on host — everything runs inside Docker.

🚀 Features (In-Depth)
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

All supported package managers

Multiple languages in monorepos

Known CVEs with severity filtering

Token is securely requested at runtime

No credentials are stored permanently

📊 Unified Results Output

All scan outputs are saved to:

/repo/Secret_Detection_Reports/


Easy integration with:

CI artifacts

SIEM tools

Security dashboards

🧠 DevSecOps-Ready Design

Containerized

Non-intrusive

CI/CD friendly

Shift-Left security aligned

📥 Installation
1️⃣ Pull from Docker Hub
docker pull aniketkasturi/rahasyascan


OR build locally:

docker build -t rahasyascan .

🛠 Usage
1️⃣ Clone the target repository
git clone https://github.com/target/repo.git

2️⃣ Run RahasyaScan
docker run -it \
  -v $(pwd)/repo:/repo \
  rahasyascan


⚠️ The repository must be mounted at /repo

🏁 Flags & Commands

When prompted inside the container:

🔎 Scan Specific Tools
-scan gitleaks trufflehog snyk

🔍 Full Secrets Scan
-scan gitleaks gittyleaks trufflehog detect-secrets ggshield talisman

📦 Dependency Scan Only
-scan snyk

🧪 Mixed Scan
-scan gitleaks snyk trufflehog

🧷 Available Tools
Flag	Tool
gitleaks	Git history secret scanning
gittyleaks	Pattern-based detection
trufflehog	Entropy detection
detect-secrets	Yelp secrets detection
ggshield	GitGuardian scanning
talisman	Pre-commit style scanning
snyk	Dependency vulnerability scanning
🔑 Snyk Authentication Flow

Token is never hardcoded

Requested securely during runtime:

Enter your Snyk API Token:


Token is:

Used temporarily

Logged out after scan

Unset from environment

🎨 Customization
Add/Remove Tools

Edit /app/entrypoint.sh:

Add new scanners

Disable unused ones

Ignore Paths (TruffleHog)

Edit:

/trufflehog_exclude.txt

CI/CD Integration

RahasyaScan is designed for:

GitHub Actions

GitLab CI

Jenkins

Azure DevOps

Example (GitHub Actions):

- name: Run RahasyaScan
  run: |
    docker run -v ${{ github.workspace }}:/repo aniketkasturi/rahasyascan

🛡 Security Philosophy

No secrets stored

No background services

No outbound telemetry

Fully transparent execution

👤 Author

Aniket Kasturi
DevSecOps | Cloud Security | Offensive Security

“Security is not a feature — it’s a mindset.”
