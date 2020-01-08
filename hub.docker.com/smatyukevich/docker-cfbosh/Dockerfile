# Dockerfile for BOSH/CF operations
FROM ubuntu:16.04
RUN DEBIAN_FRONTEND=noninteractive apt-get update && apt-get install -y build-essential zlibc zlib1g-dev ruby ruby-dev openssl libxslt-dev libxml2-dev libssl-dev libreadline6 libreadline6-dev libyaml-dev libsqlite3-dev sqlite3 wget curl vim jq python3-yaml netcat dnsutils git gettext-base libcurl3 whois
RUN wget https://s3.amazonaws.com/bosh-cli-artifacts/bosh-cli-2.0.28-linux-amd64 && chmod +x bosh-cli* && mv bosh-cli* /usr/local/bin/bosh
RUN curl -sL "https://cli.run.pivotal.io/stable?release=linux64-binary&source=github" | tar -zx && mv cf /usr/local/bin/
RUN wget https://releases.hashicorp.com/vault/0.7.3/vault_0.7.3_linux_amd64.zip && unzip vault*zip && mv vault /usr/local/bin && rm vault*zip
RUN wget https://github.com/pivotal-cf/om/releases/download/0.25.0/om-linux && chmod +x om-linux && mv om-linux /usr/local/bin 
RUN gem install cf-uaac bundler
RUN wget https://github.com/pivotalservices/cf-mgmt/releases/download/v0.0.65/cf-mgmt-linux && chmod +x cf-mgmt-linux && mv cf-mgmt-linux /usr/local/bin/cf-mgmt
RUN wget https://github.com/s-matyukevich/yaml2json/releases/download/0.0.1/yaml2json && chmod +x yaml2json && mv yaml2json /usr/local/bin/yaml2json
RUN wget https://releases.hashicorp.com/terraform/0.11.14/terraform_0.11.14_linux_amd64.zip && unzip terraform_0.11.14_linux_amd64.zip && mv terraform /usr/local/bin/
