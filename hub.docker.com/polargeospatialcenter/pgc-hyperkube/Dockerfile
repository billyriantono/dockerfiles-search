FROM k8s.gcr.io/hyperkube:v1.14.1

RUN apt-get update && \
 apt-get install -y ceph-fs-common && \
 rm -rf /var/lib/apt/lists/*
