FROM ubuntu:latest
RUN \ 
	apt-get update && \
	apt-get -y upgrade && \
	apt-get install -y git
	
RUN apt install -y curl
RUN curl --silent --location https://deb.nodesource.com/setup_12.x | bash -
RUN apt-get install -y \
  nodejs
RUN npm install
RUN git clone https://github.com/chvin/react-tetris.git
WORKDIR ./../react-tetris
RUN npm install
RUN npm run build