FROM ubuntu:18.04
LABEL org.label-schema.schema-version="1.0.0-rc.1"
ARG BUILD_DATE
ARG VCS_REF
LABEL org.label-schema.build_date=$BUILD_DATE
LABEL org.label-schema.name="jlosito/dana"
LABEL org.label-schema.maintainer="lositojohnj@gmail.com"
LABEL org.label-schema.description="Test/benchmark regression and comparison system with dashboard"
LABEL org.label-schema.url="https://github.com/google/dana"
LABEL org.label-schema.vcs-url="https://gitlab.com/jlosito/dana-dockerfile"
LABEL org.label-schema.vcs-ref=$VCS_REF
RUN apt-get update && apt-get install -y \
	nodejs \
	npm \
	git
RUN git clone https://github.com/google/dana.git
WORKDIR /dana
RUN npm install
RUN cp -r demo/configs configs
RUN cp -r demo/projects www/views/projects
EXPOSE 7000
ENTRYPOINT ["npm", "start"]
