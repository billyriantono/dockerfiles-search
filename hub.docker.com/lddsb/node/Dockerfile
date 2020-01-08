FROM node:lts

COPY china-mirrors.sh .
RUN bash china-mirrors.sh

COPY scripts/* /bin/
RUN chmod -R +x /bin/

CMD ['node']
