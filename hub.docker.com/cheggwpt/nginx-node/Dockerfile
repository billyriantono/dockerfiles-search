FROM cheggwpt/nginx:latest

ENV yarn_version 0.19.1

RUN	apk --update --no-cache add nodejs curl gnupg git && \
	curl -o- -L \
	https://yarnpkg.com/install.sh \
	| bash -s -- --version ${yarn_version} && \
	ln -s /root/.yarn/bin/yarn /usr/local/bin/yarn && \
	[[ "${yarn_version}" = "$(yarn --version)" ]] && \
	apk del curl gnupg
