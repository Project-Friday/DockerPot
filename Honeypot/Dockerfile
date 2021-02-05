FROM ubuntu:latest

# Install Dependencies
ARG DEBIAN_FRONTEND=noninteractive

RUN apt-get update; \
	apt-get upgrade -y; \
	apt-get install -y \
		apt-utils \
		openssh-server \
		sudo \
		man \
		perl \
		wget \
		tar \
		adduser \
		netstat-nat \
		net-tools \
		curl \
		iputils-ping \
		nano

# Create a user
RUN groupadd -g 123 test_system; \
	useradd -rm -d /home/test -s /bin/bash test; \
	echo 'test:test' | chpasswd

# Install forced proxy
COPY proxy_config.sh /tmp/
RUN cat /tmp/proxy_config.sh >> /home/test/.bashrc; \
	chown root:root /home/test/.bashrc; \
	rm /tmp/proxy_config.sh

# Expand image to normal size
RUN yes | /usr/local/sbin/unminimize

# Run the services
RUN service ssh start

# Docker configuration
EXPOSE 22/tcp
CMD ["/usr/sbin/sshd","-D"]