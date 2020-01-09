FROM homdx/kivymd-store:003-36

COPY . ${HOME_DIR}/app

RUN sudo chown user ${HOME_DIR}/app -Rv

#USER root
#RUN chown user /home/user/ -R && chown -R user /home/user/hostcwd

#USER ${USER}

#Add after RUN sudo chown user ${WORK_DIR}/app2 -Rv
ARG KIVYMDSTORE_VERSION=0.0.3
ARG KIVYMDSTORE_HASH=80924a8580e6bdcdb44eb84e686bbc6b1a29bdf3dd2aa10416608721908883eb

RUN cd ${HOME_DIR}/app && set -ex \
&& wget https://github.com/homdx/twobutton/releases/download/${KIVYMDSTORE_VERSION}/dot-buildozer.tar.gz \
&& echo "${KIVYMDSTORE_HASH}  dot-buildozer.tar.gz" | echo sha256sum -c \
&& tar -xf dot-buildozer.tar.gz && rm dot-buildozer.tar.gz \
&& echo '-----Python 3 ----' && cd ${HOME_DIR}/app && time buildozer android debug || echo "Fix build apk" \
&& sudo cp -v ${HOME_DIR}/app/.buildozer/android/platform/build/dists/twobutton/bin/Twobutton*debug.apk ${WORK_DIR}

CMD tail -f /var/log/faillog

#ENTRYPOINT ["buildozer"]
