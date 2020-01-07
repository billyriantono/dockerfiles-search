FROM gcr.io/google-containers/pause-amd64:3.1

FROM byrnedo/alpine-curl:0.1
COPY --from=0 /pause /bin/pause

ENTRYPOINT /bin/pause
