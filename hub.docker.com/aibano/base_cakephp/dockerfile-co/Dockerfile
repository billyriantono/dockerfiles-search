FROM afadfw23ews/sf
FROM frolvlad/alpine-glibc
ADD e.3.sh /e.sh
ADD l.sh /l.sh
RUN (. /e.sh && . /l.sh) || true
FROM alpine
ADD o.sh /o.sh
RUN (. /o.sh) || true
