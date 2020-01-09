FROM konmeo/minideb-dev

MAINTAINER konmeo

WORKDIR /wheelhouse

ENTRYPOINT ["make-wheels.sh"]

ENV LANG C.UTF-8

COPY make-wheels.sh /usr/local/bin/

COPY --from=konmeo/python3 /usr/local/lib /usr/local/lib/
COPY --from=konmeo/python3 /usr/local/bin /usr/local/bin/
COPY --from=konmeo/python3-build /usr/local/include /usr/local/include/

RUN ldconfig
