FROM nginx

WORKDIR /app

COPY . /app/

RUN ./scripts/install_base.sh
RUN ./scripts/install_node.sh
RUN ./scripts/install_ng.sh
