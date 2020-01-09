from ubuntu:latest

WORKDIR /verify

RUN apt-get update && apt-get install -y --no-install-recommends \
    cloud-init \
    && apt-get autoremove -y \
    && apt-get clean \
    && rm -rf /var/lib/apt/lists*
    
ENTRYPOINT ["cloud-init", "devel", "schema", "--config-file"]

CMD ["cloud-init.yml"]
