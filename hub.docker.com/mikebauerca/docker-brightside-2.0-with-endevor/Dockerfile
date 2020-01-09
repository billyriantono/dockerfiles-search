# This Dockerfile is used to build an image capable of running Brightside 2.0 commands and Brightside Endevor commands
FROM mikebauerca/docker-brightside-2.0

# Installs Brightside Endevor Plug-in
USER jenkins
RUN bright plugins install @brightside/endevor@1.1.0-next.201811281633

USER root
