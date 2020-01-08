ARG freetds_version=1.00.110
ARG ruby_version=2.5.3

FROM veracross/freetds:${freetds_version} as freetds
FROM circleci/ruby:${ruby_version}-node-browsers

COPY --from=freetds /usr/local /usr/local
