FROM pataquets/ngrok

RUN make release-client

ENTRYPOINT [ "bin/ngrok", "-log", "stdout" ]
