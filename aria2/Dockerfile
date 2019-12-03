FROM jgoerzen/debian-base-minimal:buster
MAINTAINER Jens Dürr <dev-dockerhub@jensomato.de>

RUN DEBIAN_FRONTEND=noninteractive apt-get update && \
	apt-get install --no-install-recommends -y ca-certificates aria2 && \
	apt-get clean && rm -rf /var/lib/apt/lists/*

COPY conf/09-aria2 /usr/local/preinit/
COPY conf/aria2.conf /etc/aria2/
COPY conf/aria2.service /etc/systemd/system/

ENV GID=1000
ENV UID=1000

VOLUME /download

EXPOSE 6800/tcp
