FROM node:13-alpine
ADD . /src
WORKDIR /src
RUN npm install --silent
RUN npm run build

FROM rainbean/fastapi:latest
ADD . /src
WORKDIR /src
RUN python setup.py build_ext --inplace
RUN find tostador \( -name certficate.py -or -name certficate.c \) -delete

FROM rainbean/fastapi:latest
LABEL maintainer "Jimmy Lee"
# specify module
ENV MODULE_NAME tostador.main
# serve react app by nginx
COPY --from=0 /src/build/ /app/www/
COPY --from=1 /src/tostador/ /app/tostador/
