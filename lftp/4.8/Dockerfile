FROM minidocks/base:3.8
LABEL maintainer="Martin Hasoň <martin.hason@gmail.com>"

RUN apk --update add lftp && clean

COPY rootfs /

CMD [ "lftp" ]
