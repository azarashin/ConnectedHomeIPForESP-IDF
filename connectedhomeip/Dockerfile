FROM espressif/idf:release-v5.2

WORKDIR /home/work

RUN apt update
RUN apt upgrade -y
RUN apt install -y git gcc g++ pkg-config libssl-dev libdbus-1-dev \
    libglib2.0-dev libavahi-client-dev ninja-build python3-venv python3-dev \
    python3-pip unzip libgirepository1.0-dev libcairo2-dev libreadline-dev

RUN mkdir ~/.ssh
RUN echo -e "Host github.com\n\tStrictHostKeyChecking no\n" >> ~/.ssh/config
RUN git clone --recurse-submodules https://github.com/project-chip/connectedhomeip.git

RUN cd /home/work/connectedhomeip && \
	git pull &&\
	git submodule update --init

# . -> bash (activate.sh and bootstrap.sh are not dash scripts but bash scripts. )
RUN cd /home/work/connectedhomeip && \
	bash ./scripts/activate.sh &&\
	bash ./scripts/bootstrap.sh

RUN pip install coloredlogs

RUN echo 'cd /home/work/connectedhomeip && source scripts/activate.sh' > ~/.bashrc
