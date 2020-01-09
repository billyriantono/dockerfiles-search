FROM busybox

HEALTHCHECK --interval=2s --timeout=10s --start-period=5s --retries=3 CMD stat /healthcheck.txt || exit 1
