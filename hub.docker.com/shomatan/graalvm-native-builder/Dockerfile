FROM oracle/graalvm-ce:19.2.1

LABEL maintainer "Shoma Nishitateno <shoma416@gmail.com>"

RUN gu install native-image

WORKDIR /work

ENTRYPOINT ["native-image"]

CMD ["--help"]
