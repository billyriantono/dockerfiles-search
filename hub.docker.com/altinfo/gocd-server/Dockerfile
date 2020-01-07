FROM fedora

LABEL maitainer="Luiz Fernando Pereira <luizfernandopereira@outlook.com.br>" \
      company="Alternativa Informática"

RUN dnf install httpd-tools git -y \
    && dnf install https://download.gocd.org/binaries/19.10.0-10357/rpm/go-server-19.10.0-10357.noarch.rpm -y \
    && dnf clean all

COPY entrypoint.sh /opt/entrypoint.sh
COPY plugins/google-oauth-authorization-plugin-3.0.1-28.jar /opt/google-oauth-authorization-plugin-3.0.1-28.jar
RUN chmod +x /opt/entrypoint.sh

EXPOSE 8153 8154

ENTRYPOINT [ "/opt/entrypoint.sh" ]