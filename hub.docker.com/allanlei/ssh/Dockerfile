FROM    alpine

RUN     apk --no-cache add \
            openssh-client

COPY    entrypoint.sh /
RUN     chmod +x /entrypoint.sh
VOLUME  ["/root/.ssh/"]
ENTRYPOINT ["/entrypoint.sh"]
CMD     ["ssh"]
