FROM cassandra:latest
RUN sed -ri 's/^(# )?('"authenticator"':).*/\2 '"PasswordAuthenticator"'/' "$CASSANDRA_CONFIG/cassandra.yaml"
EXPOSE 7000 7001 7199 9042 9160
CMD ["cassandra", "-f"]
