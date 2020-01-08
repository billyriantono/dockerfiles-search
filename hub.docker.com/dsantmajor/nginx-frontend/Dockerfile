FROM nginx:1.12.0

# Prepare image
COPY artefacts/ /

# Install curl
RUN apt-get update && \
    apt-get install -y \
      curl \
      less  \
      vim    \
      procps

# Container start script
CMD ["/root/entrypoint.sh"]

