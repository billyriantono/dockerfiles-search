FROM gcr.io/kaniko-project/executor:debug-v0.10.0 as kaniko

FROM jenkins/jnlp-slave:3.29-1

COPY --from=kaniko /kaniko/executor /usr/local/bin/kaniko
