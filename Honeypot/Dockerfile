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
		curl  

# Create a user
RUN groupadd -g 123 test_system; \
	useradd -rm -d /home/test -s /bin/bash test; \
	echo 'test:test' | chpasswd

RUN yes | /usr/local/sbin/unminimize

# Run the services
RUN service ssh start

# Docker configuration
EXPOSE 22/tcp
CMD ["/usr/sbin/sshd","-D"]