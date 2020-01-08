FROM jupyterhub/k8s-hub:0.8.2

LABEL maintainer="Luigi Di Fraia"

USER root

COPY sac-logo.png /usr/local/share/jupyterhub/static/images/sac-logo.png

# Switch back to jovyan to avoid the container from running as root
USER $NB_UID
