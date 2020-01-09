FROM busybox
HEALTHCHECK --interval=5s --timeout=3s --retries=4 \
  CMD stat /health_check_file || exit 1
