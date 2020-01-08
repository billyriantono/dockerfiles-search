FROM ubuntu:16.04
RUN apt-get update && apt-get install --yes curl && rm -rf /var/lib/apt/lists/*  && \
  (curl https://omnitruck.chef.io/install.sh | bash -s -- -P chefdk -c stable -v 2.5.3)
