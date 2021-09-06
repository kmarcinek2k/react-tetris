
FROM ubuntu:latest
RUN apt-get -y update
RUN apt-get -y upgrade
RUN apt-get install -y build-essential
RUN cd ~
COPY . tetris_deploy/
WORKDIR tetris_deploy
CMD [ls -l]