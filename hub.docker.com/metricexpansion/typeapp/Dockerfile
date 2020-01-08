FROM ubuntu:18.04 AS frontend
RUN apt-get update \
 && apt-get install -y npm

COPY frontend/package.json frontend/package-lock.json /frontend/

RUN cd /frontend \
 && npm install

COPY frontend /frontend-src/

RUN cp -r /frontend-src/* /frontend/ \
 && cd /frontend/ \
 && npm run build

RUN cd /frontend/build && ls

# END FRONTEND BUILD

FROM ubuntu:18.04
RUN apt-get update \
 && apt-get install -y python3 python3-pip

RUN pip3 install sanic requests numpy seaborn pandas nltk

COPY backend /app
COPY --from=frontend /frontend/build /app/frontend/build

EXPOSE 8000/tcp
CMD cd /app && python3 app.py