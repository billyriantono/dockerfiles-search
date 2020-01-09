FROM alerta/alerta-web:7.4.1

# Set maintainer field
LABEL maintainer="rosskouk - rosskouk@gmail.com"

# Switch to root for plugin installation
USER root

# Install the routing plugin
RUN /venv/bin/pip install git+https://github.com/rosskouk/alerta-plugins.git@master#subdirectory=routing

USER 1001