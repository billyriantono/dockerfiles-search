FROM fedora

LABEL maitainer="Luiz Fernando Pereira <luizfernandopereira@outlook.com.br>" \
      company="Alternativa Informática"

RUN dnf install https://download.gocd.org/binaries/19.10.0-10357/rpm/go-agent-19.10.0-10357.noarch.rpm -y \
    && dnf install https://download.docker.com/linux/fedora/31/x86_64/stable/Packages/docker-ce-cli-19.03.4-3.fc31.x86_64.rpm -y \
    && dnf install git jq -y \
    && dnf clean all

COPY entrypoint.sh /opt/entrypoint.sh
RUN chmod +x /opt/entrypoint.sh

ENTRYPOINT [ "/opt/entrypoint.sh" ]