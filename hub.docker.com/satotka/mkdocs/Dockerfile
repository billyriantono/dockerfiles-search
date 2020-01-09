FROM python:3.5

RUN pip install mkdocs

WORKDIR /workdir

COPY docs/index.md /workdir/docs/
COPY mkdocs.yml /workdir/

VOLUME /workdir
EXPOSE 8000

ENTRYPOINT ["mkdocs"]
CMD ["serve", "--dev-addr=0.0.0.0:8000"]
