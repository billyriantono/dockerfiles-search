#
# (captain obvious) build me on the target ARCH
#
FROM arm32v7/debian:stretch-slim

ARG HELM_TILLER_VERSION=2.12.3
ARG HEML_TILLER_ARCH=arm

# comment next line when building manually
# (this line is used by dockerhub to build ARM image ; see hooks/)
COPY qemu-arm-static /usr/bin

RUN apt-get update \
    && apt-get install -y --no-install-recommends \
      ca-certificates \
      wget \
    && apt-get clean \
    && rm -rf /var/lib/apt/lists/*

RUN addgroup helm \
    && useradd -g helm -m -s /bin/bash helm

USER helm
WORKDIR /home/helm

# visit https://github.com/helm/helm/releases for download links:
RUN wget -q https://storage.googleapis.com/kubernetes-helm/helm-v${HELM_TILLER_VERSION}-linux-${HEML_TILLER_ARCH}.tar.gz -O /tmp/helm_bin.tar.gz \
    && tar zxvf /tmp/helm_bin.tar.gz \
    && rm -rf /tmp/helm_bin.tar.gz

EXPOSE 44134

CMD ["/home/helm/linux-arm/tiller"]

