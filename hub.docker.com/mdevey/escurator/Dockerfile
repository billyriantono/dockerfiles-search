FROM mdevey/curator as bin
FROM python:3.6-alpine3.6
RUN apk --no-cache upgrade && apk --no-cache add ca-certificates pigz
COPY --from=bin /curator /curator
COPY requirements.txt ./
RUN pip3 install -r requirements.txt
COPY run.py /run.py
ENTRYPOINT ["/usr/local/bin/python"]
CMD ["run.py"]
