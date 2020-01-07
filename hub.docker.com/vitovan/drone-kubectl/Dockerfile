FROM bitnami/kubectl:1.13

LABEL maintainer "Vito Van <awesomevito@live.com>"

COPY init-kubectl kubectl /opt/kubectl/bin/

USER root

ENV PATH="/opt/kubectl/bin:$PATH"

ENTRYPOINT ["kubectl"]

CMD ["--help"]
