FROM pataquets/ngrok

RUN make release-server

ENTRYPOINT [ "bin/ngrokd" ]
CMD [ "-help" ]
