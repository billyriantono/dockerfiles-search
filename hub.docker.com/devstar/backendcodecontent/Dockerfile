# Use OpenJDK 8
FROM openjdk:8-jdk

ENV URL "https:\/\/localhost:8080\/"
ENV TAGS "@cwe-319-auth"
ENV TAGS_SKIP "~@skip"

# Set a sensible server directory.
WORKDIR /home/bdd-security

# Add the directory
ADD . .

COPY ./entrypoint.sh entrypoint.sh
COPY ./runtests.sh runtests.sh
RUN chmod +x runtests.sh
RUN chmod +x entrypoint.sh

ENTRYPOINT ["/home/bdd-security/entrypoint.sh"]
