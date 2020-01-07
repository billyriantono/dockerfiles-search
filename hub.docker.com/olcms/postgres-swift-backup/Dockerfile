FROM postgres:9.6.3

COPY backup /backup

RUN /backup/setup-base-system.sh

CMD /backup/do_backup.py
