# sources:
# https://docs.docker.com/develop/develop-images/multistage-build/
# https://nodejs.org/en/docs/guides/nodejs-docker-webapp/


FROM node:12 as react

WORKDIR /squeng/app

COPY klaant-client/package*.json ./
RUN npm install

COPY klaant-client/public ./public
COPY klaant-client/src ./src
# https://create-react-app.dev/docs/adding-custom-environment-variables#linux-macos-bash
RUN INLINE_RUNTIME_CHUNK=false npm run build


FROM hseeberger/scala-sbt:11.0.4_1.3.3_2.12.10 as play

WORKDIR /squeng/app

COPY klaant-server/app ./app
COPY klaant-server/conf ./conf
COPY klaant-server/project ./project
COPY klaant-server/public ./public
COPY klaant-server/reinraum ./reinraum
COPY klaant-server/build.sbt ./
COPY --from=react /squeng/app/build ./public/build
RUN sbt stage


FROM openjdk:11

WORKDIR /squeng/app

COPY --from=play /squeng/app/target/universal/stage ./target/universal/stage

RUN groupadd -r gruppe && useradd --no-log-init -r -g gruppe benutzer
USER benutzer

EXPOSE 8080
EXPOSE 8484
CMD ["target/universal/stage/bin/klaant", "-Dpidfile.path=play.pid", "-Dhttp.port=8080", "-Dhttps.port=8484"]
