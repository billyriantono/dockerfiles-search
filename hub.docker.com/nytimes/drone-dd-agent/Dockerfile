FROM tonglil/auth-gke:alpine

COPY dd-agent.sh /bin/dd-agent
COPY manifests /manifests

ENTRYPOINT ["/bin/dd-agent"]
