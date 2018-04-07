FROM          alpine

RUN           apk add --no-cache coreutils
CMD           ["trap : TERM INT; sleep infinity & wait"]
