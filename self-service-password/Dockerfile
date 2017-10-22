FROM jgoerzen/debian-base-apache:jessie
MAINTAINER Jens Dürr <dev-dockerhub@jensomato.de>

RUN DEBIAN_FRONTEND=noninteractive apt-get update && apt-get install -y \
  apt-transport-https \
  apt-utils \
  wget

RUN echo "deb [arch=amd64] https://ltb-project.org/debian/jessie jessie main" > /etc/apt/sources.list.d/ltb-project.list
RUN wget -O - https://ltb-project.org/wiki/lib/RPM-GPG-KEY-LTB-project | apt-key add -

RUN DEBIAN_FRONTEND=noninteractive apt-get update && apt-get install -y \
  self-service-password && apt-get clean && rm -rf /var/lib/apt/lists/*

RUN a2ensite self-service-password && a2dissite 000-default

# expose only apache HTTP port
EXPOSE 80
