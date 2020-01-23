FROM gradle:jre9
USER root
RUN apt-get update && apt-get install -y --no-install-recommends vim \
    && rm -rf /var/lib/apt/lists/*; 
CMD ["/bin/bash"]
