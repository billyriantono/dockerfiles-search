FROM ruby
RUN apt-get -y update \
	&& apt-get -y install \
 		cmake \
		libicu-dev
RUN gem install gollum
RUN gem install redcarpet org-ruby github-linguist github-markdown gollum-rugged_adapter

COPY ./README.md /README.md


# Docker labels
ARG BUILD_DATE
ARG VCS_REF

LABEL org.label-schema.name="Gollum wiki" \
	org.label-schema.description="A simple, Git-powered wiki with a sweet API and local frontend" \
	org.label-schema.usage="/README.md" \
	org.label-schema.url="https://github.com/thomasleveil/docker-gollum" \
	org.label-schema.vcs-url="https://github.com/thomasleveil/docker-gollum.git" \
	org.label-schema.build-date=$BUILD_DATE \
	org.label-schema.vcs-ref=$VCS_REF \
	org.label-schema.schema-version="1.0.0-rc1"


VOLUME /wiki
WORKDIR /wiki

ENTRYPOINT ["gollum", "--port", "8080", "--adapter=rugged"]
CMD ["--emoji", "--live-preview", "--h1-title", "--allow-uploads", "--user-icons=gravatar"]
EXPOSE 8080
