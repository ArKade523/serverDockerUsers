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
RUN useradd -ms /bin/bash gas

# Set the password for the 'gas' user
RUN echo "gas:gas" | chpasswd

# Add the new user to the sudo group
RUN usermod -aG sudo "gas" && echo "Added user 'gas' to the sudo users group"

# Switch to the new user
USER gas

# Install F' tools
# Don't worry about being in a venv, this is a docker container anyway
RUN python3 -m venv /home/gas/fprime \
	&& . /home/gas/fprime/bin/activate \
	&& pip install --upgrade pip \
	&& pip install -U fprime-tools

# Customize .bashrc for a colored prompt and screen clearing
RUN echo 'clear' >> /home/gas/.bashrc && \
    echo "PS1='\[\033[01;32m\]\u@\h\[\033[00m\]:\[\033[01;34m\]\w\[\033[00m\]\$ '" >> /home/gas/.bashrc

# Create a welcome message
RUN echo 'echo "Welcome to your Docker container for F-Prime development."' >> /home/gas/.bashrc && \
	echo 'echo "This container has been set up for you by Kade Angell"' >> /home/gas/.bashrc && \
	echo '. /home/gas/fprime/bin/activate' >> /home/gas/.bashrc && \
	echo 'echo "If this is your first time logging in, run fprime-util new --project \nIf not, ignore this message"' >> /home/gas/.bashrc && \
	echo 'echo "The default password for this account is gas."' >> /home/gas/.bashrc

# Set the working directory
WORKDIR /home/gas

# Set the default command to /bin/bash
CMD ["/bin/bash"]

