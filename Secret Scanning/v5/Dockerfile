# Use Python base image for tool compatibility
FROM python:3.12-slim-bullseye

# Set environment variables for version numbers
ENV GO_VERSION=1.22.0
ENV GITLEAKS_VERSION=8.18.2
ENV TRUFFLEHOG_VERSION=3.68.3
ENV TALISMAN_VERSION=1.32.0
ENV TALISMAN_HTML_REPORT_VERSION=1.3

# Install Ruby, system deps, security tools
RUN apt-get update && \
    apt-get install -y git wget make curl unzip procps ruby bash ca-certificates && \
    gem install lolcat && \
    wget https://go.dev/dl/go${GO_VERSION}.linux-amd64.tar.gz -O go.tar.gz && \
    tar -xvf go.tar.gz && \
    mv go /usr/local && \
    rm go.tar.gz && \
    apt-get clean && \
    rm -rf /var/lib/apt/lists/* && \
    pip install gittyleaks detect-secrets ggshield && \
    wget https://github.com/gitleaks/gitleaks/releases/download/v${GITLEAKS_VERSION}/gitleaks_${GITLEAKS_VERSION}_linux_x64.tar.gz -O gitleaks.tar.gz && \
    tar -xzf gitleaks.tar.gz -C /usr/local/bin/ && \
    rm gitleaks.tar.gz && \
    wget https://github.com/trufflesecurity/trufflehog/releases/download/v${TRUFFLEHOG_VERSION}/trufflehog_${TRUFFLEHOG_VERSION}_linux_amd64.tar.gz -O trufflehog.tar.gz && \
    tar -xzvf trufflehog.tar.gz -C /usr/local/bin/ && \
    rm trufflehog.tar.gz && \
    wget https://github.com/thoughtworks/talisman/releases/download/v${TALISMAN_VERSION}/talisman_linux_amd64 -O /usr/local/bin/talisman && \
    chmod +x /usr/local/bin/talisman

# -------------------- SNYK INSTALL --------------------
RUN curl -sSL https://static.snyk.io/cli/latest/snyk-linux -o /usr/local/bin/snyk && \
    chmod +x /usr/local/bin/snyk

RUN mkdir -p /root/.talisman && \
    curl https://github.com/jaydeepc/talisman-html-report/archive/v${TALISMAN_HTML_REPORT_VERSION}.zip -o /root/.talisman/talisman_html_report.zip -J -L && \
    cd /root/.talisman && \
    unzip talisman_html_report.zip -d . && \
    mv talisman-html-report-1.3 talisman_html_report && \
    rm talisman_html_report.zip

ENV PATH="$PATH:/usr/local/go/bin" \
    GIT_DISCOVERY_ACROSS_FILESYSTEM=true

ENV GGSHIELD_TOKEN=abcd
RUN echo "$GGSHIELD_TOKEN" | ggshield auth login --method token 2>&1 || true

WORKDIR /app

# Banner
# Create RahasyaScan Blood-Red Banner
RUN echo '\033[1;31m\n\
██████╗  █████╗ ██╗  ██╗ █████╗ ███████╗██╗   ██╗ █████╗ ███████╗ ██████╗ █████╗ ███╗   ██╗\n\
██╔══██╗██╔══██╗██║  ██║██╔══██╗██╔════╝╚██╗ ██╔╝██╔══██╗██╔════╝██╔════╝██╔══██╗████╗  ██║\n\
██████╔╝███████║███████║███████║███████╗ ╚████╔╝ ███████║███████╗██║     ███████║██╔██╗ ██║\n\
██╔══██╗██╔══██║██╔══██║██╔══██║╚════██║  ╚██╔╝  ██╔══██║╚════██║██║     ██╔══██║██║╚██╗██║\n\
██║  ██║██║  ██║██║  ██║██║  ██║███████║   ██║   ██║  ██║███████║╚██████╗██║  ██║██║ ╚████║\n\
╚═╝  ╚═╝╚═╝  ╚═╝╚═╝  ╚═╝╚═╝  ╚═╝╚══════╝   ╚═╝   ╚═╝  ╚═╝╚══════╝ ╚═════╝╚═╝  ╚═╝╚═╝  ╚═══╝\n\
\n\
                    ☠  R A H A S Y A S C A N  ☠\n\
            Vulnerable Dependencies | Secrets Detection\n\
\n\
  \"The quieter you become, the more you are able to hear.\"\n\
\n\
                    Author : Aniket Kasturi\n\
              If it'\''s exposed — it'\''s already compromised.\n\
\033[0m' > /app/banner.txt


RUN echo -e "Secret_Detection_Reports/\ntalisman_html_report/" > /trufflehog_exclude.txt

# -------------------- ENTRYPOINT --------------------
RUN { \
echo '#!/bin/bash'; \
echo 'cat /app/banner.txt | lolcat -t'; \
echo 'printf "\n\033[1mFeatures Available:\033[0m\n"'; \
echo 'printf "%s\n" "- gitleaks"'; \
echo 'printf "%s\n" "- gittyleaks"'; \
echo 'printf "%s\n" "- trufflehog"'; \
echo 'printf "%s\n" "- detect-secrets"'; \
echo 'printf "%s\n" "- ggshield"'; \
echo 'printf "%s\n" "- talisman"'; \
echo 'printf "%s\n" "- snyk (Dependency Scanning)"'; \
echo ''; \
echo 'read -p "Enter flags (example: -scan snyk gitleaks): " cmd'; \
echo 'TOOLS=()'; \
echo 'if echo "$cmd" | grep -q "^-scan "; then'; \
echo '  cmd=${cmd#-scan }'; \
echo '  IFS=" " read -r -a TOOLS <<< "$cmd"'; \
echo 'else'; \
echo '  echo "Invalid input"; exit 1;'; \
echo 'fi'; \
echo 'cd /repo || exit 1'; \
echo 'mkdir -p /repo/Secret_Detection_Reports'; \
echo 'for tool in "${TOOLS[@]}"; do'; \
echo 'case "$tool" in'; \

echo 'snyk)'; \
echo '  printf "\n\033[0;36mStarting Snyk Dependency Scan...\033[0m\n"'; \
echo '  read -s -p "Enter your Snyk API Token: " SNYK_TOKEN'; \
echo '  echo ""'; \
echo '  export SNYK_TOKEN'; \
echo '  snyk auth "$SNYK_TOKEN"'; \
echo '  snyk test --all-projects --severity-threshold=low | tee /repo/Secret_Detection_Reports/snyk_report.txt'; \
echo '  snyk logout'; \
echo '  unset SNYK_TOKEN'; \
echo '  printf "\033[0;32mSnyk scan complete.\033[0m\n"'; \
echo '  ;;'; \

echo 'gitleaks) gitleaks detect --source=. --report-path=/repo/Secret_Detection_Reports/gitleaks.json ;;'; \
echo 'gittyleaks) gittyleaks --find-anything > /repo/Secret_Detection_Reports/gittyleaks.txt ;;'; \
echo 'trufflehog) trufflehog git file:///repo --exclude-paths=/trufflehog_exclude.txt > /repo/Secret_Detection_Reports/trufflehog.txt ;;'; \
echo 'detect-secrets) detect-secrets scan --all-files > /repo/Secret_Detection_Reports/detect_secrets.txt ;;'; \
echo 'ggshield) ggshield secret scan repo . > /repo/Secret_Detection_Reports/ggshield.txt ;;'; \
echo 'talisman) talisman --scanWithHtml --reportDirectory=/repo/Secret_Detection_Reports ;;'; \
echo '*) echo "Unknown tool: $tool";;'; \
echo 'esac'; \
echo 'done'; \
} > /app/entrypoint.sh && chmod +x /app/entrypoint.sh

ENTRYPOINT ["/app/entrypoint.sh"]
