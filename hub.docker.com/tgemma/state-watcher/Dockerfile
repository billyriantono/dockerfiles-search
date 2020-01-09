FROM python:3

COPY src ./

RUN pip install requests
RUN pip install PyMySQL
RUN pip install pony

ENV TZ=Europe/Zurich

CMD [ "python", "./state_watcher.py" ]
