FROM ubuntu:16.04

MAINTAINER Oleksandr Kravchuk <dev@sashko.rv.ua>

# First things first
RUN apt-get update
RUN apt-get install -q -y apt-utils
RUN apt-get -y upgrade

# Switch frontend to noninteractive
ENV DEBIAN_FRONTEND=noninteractive

RUN apt-get clean

# Install Yocto/Poky dependencies
RUN apt-get install -q -y gawk wget git-core diffstat unzip texinfo \
                          gcc-multilib build-essential chrpath socat \
                          cpio python python3 python3-pip python3-pexpect \
                          xz-utils debianutils iputils-ping libsdl1.2-dev xterm

# Install other useful packages
RUN apt-get install -q -y vim tig openssh-server screen tmux

# Create 'developer' user
RUN useradd --create-home --shell /bin/bash developer
RUN echo 'developer:developer'
RUN echo "developer ALL=(ALL) NOPASSWD: ALL" | tee -a /etc/sudoers

# Fix locale
RUN apt-get install -q -y locales

RUN locale-gen en_US.UTF-8
ENV LANG en_US.UTF-8
ENV LANGUAGE en_US:en
ENV LC_ALL en_US.UTF-8

RUN dpkg-reconfigure --frontend=noninteractive locales

# Switch frontend back
ENV DEBIAN_FRONTEND=teletype

# Expose SSH port
EXPOSE 22

# Switch user and work directory
USER developer
WORKDIR /home/developer/

# Run BASH
CMD ["bash"]
