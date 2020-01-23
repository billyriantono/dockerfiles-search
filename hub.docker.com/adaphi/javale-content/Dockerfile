# Docker support, thanks to xinyifly

FROM azul/zulu-openjdk:8

ENV TINI_VERSION v0.18.0
ADD https://github.com/krallin/tini/releases/download/${TINI_VERSION}/tini /tini
RUN chmod +x /tini

WORKDIR /app
COPY ./ ./
RUN bash ./posix-compile.sh

EXPOSE 8484 7575 7576 7577

ENTRYPOINT ["/tini", "--"]
CMD ["bash", "./posix-launch.sh"]
