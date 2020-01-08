FROM sergey11166/android-sdk-docker

RUN apt-get -q --yes update && apt-get -q --yes install lib32stdc++6 lib32z1

RUN echo y | sdkmanager --update && \
	echo y | sdkmanager "system-images;android-28;google_apis;x86_64"

# Clean up
RUN rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/* && \
	apt-get autoremove -y && \
	apt-get clean
