FROM gcr.io/google_containers/hyperkube-amd64:v1.3.0

MAINTAINER lhcalibur <liuhan@hotmail.com>

# Manifests for the docker-multinode guide
COPY master-multi.json /etc/kubernetes/manifests-multi/
COPY addon-manager.json /etc/kubernetes/manifests-multi/

# TODO: Move out kube-proxy to a DaemonSet again
COPY kube-proxy.json /etc/kubernetes/manifests-multi/
