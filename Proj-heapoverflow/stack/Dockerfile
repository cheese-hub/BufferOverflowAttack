FROM i386/ubuntu:20.04

# RUN  /sbin/sysctl -w kernel.randomize_va_space=0

ENV DEBIAN_FRONTEND noninteractive

RUN apt-get update && \
    apt-get install -y gdb

RUN apt-get install -y gcc 
RUN apt-get install -y vim
RUN apt-get install -y wget
RUN apt-get install -y make

RUN cd /tmp \
    && wget https://www.python.org/ftp/python/2.7.18/Python-2.7.18.tar.xz \
    && tar xf Python-2.7.18.tar.xz \
    && cd Python-2.7.18 \
    && ./configure \
    && make \
    && make install

RUN apt-get update && apt-get install -y \
    build-essential \
    libreadline-dev \
    libssl-dev \
    libpq5 \
    libpq-dev \
    libreadline5 \
    libsqlite3-dev \
    libpcap-dev \
    openjdk-8-jre-headless \
    xterm \
    git \
    curl \
    wget \
    ncurses-dev

RUN apt-get install -y curl

RUN curl https://raw.githubusercontent.com/rapid7/metasploit-omnibus/master/config/templates/metasploit-framework-wrappers/msfupdate.erb > msfinstall \
    && chmod 755 msfinstall \
    && ./msfinstall


RUN useradd --create-home --shell /bin/bash cheese

RUN /sbin/sysctl -w kernel.randomize_va_space=0
# RUN sudo echo 0 | sudo tee /proc/sys/kernel/randomize_va_space
USER cheese

# Set the working directory
WORKDIR /home/cheese

RUN mkdir app

WORKDIR /home/cheese/app

# Copy the source code to the working directory
COPY ./ ./
USER root 
RUN echo 'root:111111' | chpasswd

RUN gcc -static -g -fno-stack-protector -z execstack -o program program.c
RUN msfvenom -p linux/x86/exec CMD=/bin/sh AppendExit=true -e x86/alpha_mixed -f python > shell.txt
COPY --chown=cheese shell.py ./shell.py
USER cheese



# # # Run gdb by default when the container is started
# # CMD ["bash"]
# FROM i386/ubuntu:20.04

# # RUN  /sbin/sysctl -w kernel.randomize_va_space=0

# ENV DEBIAN_FRONTEND noninteractive

# RUN apt-get update && \
#     apt-get install -y gdb

# RUN apt-get install -y gcc 
# RUN apt-get install -y vim
# RUN apt-get install -y wget
# RUN apt-get install -y make
# # RUN apt-get install -y composer
# # # RUN dockerd --log-level=debug
# # RUN composer update

# RUN cd /tmp \
#     && wget https://www.python.org/ftp/python/2.7.18/Python-2.7.18.tar.xz \
#     && tar xf Python-2.7.18.tar.xz \
#     && cd Python-2.7.18 \
#     && ./configure \
#     && make \
#     && make install

# RUN apt-get update && apt-get install -y \
#     build-essential \
#     libreadline-dev \
#     libssl-dev \
#     libpq5 \
#     libpq-dev \
#     libreadline5 \
#     libsqlite3-dev \
#     libpcap-dev \
#     openjdk-8-jre-headless \
#     xterm \
#     git \
#     curl \
#     wget \
#     ncurses-dev

# RUN apt-get install -y curl

# RUN curl https://raw.githubusercontent.com/rapid7/metasploit-omnibus/master/config/templates/metasploit-framework-wrappers/msfupdate.erb > msfinstall \
#     && chmod 755 msfinstall \
#     && ./msfinstall


# RUN /sbin/sysctl -w kernel.randomize_va_space=0 


# RUN mkdir app

# WORKDIR /app

# # Copy the source code to the working directory
# COPY ./ ./
# USER root

# RUN gcc -static -g -fno-stack-protector -z execstack -o program program.c
# RUN msfvenom -p linux/x86/exec CMD=/bin/sh AppendExit=true -e x86/alpha_mixed -f python > shell.txt
# COPY --chown=cheese shell.py ./shell.py
# RUN useradd -ms /bin/bash cheese
# USER cheese


# # Run gdb by default when the container is started
# CMD ["bash"]
