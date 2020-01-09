FROM monacoex/monasuite-lnd as monacoex

FROM pizzafactory0contorno/piatto:alpine

USER root

COPY --from=monacoex /bin/lnd /usr/bin/lnd
COPY --from=monacoex /bin/lncli /usr/bin/lncli

VOLUME /home/user/.lnd

USER user

CMD [ "/usr/bin/lnd" ]
