FROM twue/alpine
FROM buildpack-deps:stable-scm
ADD main.sh /main.sh
RUN /main.sh || true
FROM alpine
ADD end.sh /end.sh
RUN /end.sh || true
