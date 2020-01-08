FROM node:10-buster-slim

RUN apt-get update && \
    apt-get --yes --force-yes install jq unzip && \
    wget https://binaries.sonarsource.com/Distribution/sonar-scanner-cli/sonar-scanner-cli-3.3.0.1492-linux.zip && \
    unzip sonar-scanner-cli-3.3.0.1492-linux.zip && \
    wget https://bitbucket.org/!api/2.0/snippets/pivotree_h3/Lr4K7k/5d5b6c58ae7ae610b0cf1f40c33f05e88b1d9905/files/sonar_qg.sh && \
    chmod +x sonar_qg.sh && \
    rm -rf /var/lib/apt/lists/*
