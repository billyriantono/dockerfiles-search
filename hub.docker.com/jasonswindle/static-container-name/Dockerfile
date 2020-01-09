FROM busybox:latest

RUN echo 80a37072-7ca0-4b23-a6e2-71e5851af708 > /uuid-test.txt

CMD [ "tail", "-f", "/dev/null", "/uuid-test.txt" ]
