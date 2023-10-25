# Use Debian as the base image
FROM debian:bullseye-slim

# Install git and bash
RUN apt-get update \
	&& apt-get install -y \
	git \
	bash \
	cmake \
	gcc \
	g++ \
	python3 \
	python3-pip \
	python3-venv \
	sudo \
	vim \
	nano

# Create a new user and set its shell to /bin/bash
RUN useradd -ms /bin/bash math

# Set the password for the 'math' user
RUN echo "math:math" | chpasswd

# Add the new user to the sudo group
RUN usermod -aG sudo "math" && echo "Added user 'math' to the sudo users group"

# Switch to the new user
USER math

# Customize .bashrc for a colored prompt and screen clearing
RUN echo 'clear' >> /home/math/.bashrc && \
    echo "PS1='\[\033[01;32m\]\u@\h\[\033[00m\]:\[\033[01;34m\]\w\[\033[00m\]\$ '" >> /home/math/.bashrc

# Create a welcome message
RUN echo 'echo "Welcome to your Docker container!"' >> /home/math/.bashrc && \
	echo 'echo "This is an isolated environment that effectively acts as your own personal server."' >> /home/math/.bashrc && \
	echo 'echo "This container has been set up for you by Kade Angell (mathadmin@usu.edu)"' >> /home/math/.bashrc && \
	echo 'echo "The default password for this account is math."' >> /home/math/.bashrc

# Set the working directory
WORKDIR /home/math

# Set the default command to /bin/bash
CMD ["/bin/bash"]

