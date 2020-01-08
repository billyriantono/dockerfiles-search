FROM salivaoverflow/droidkernel:base
ENV PROJECT=/project/ranchu ARCH=x86_64 \
	CROSS_COMPILE=/root/x86_64-linux-android-4.9/bin/x86_64-linux-android-
COPY ["./.ycm_extra_conf.py", "/root/.ycm_extra_conf.py"]
COPY ["./entrypoint.sh", "/root/entrypoint.sh"]
RUN chmod a+x /root/entrypoint.sh && \
	cd /root && \
	git clone https://android.googlesource.com/platform/prebuilts/gcc/linux-x86/x86/x86_64-linux-android-4.9 && \
	apt-get install -y bc
ENTRYPOINT ["/root/entrypoint.sh"]
