FROM ubuntu/apache2:edge

RUN apt-get update -y && apt install python3-pip -y
RUN apt-get install gcalcli -y
RUN apt-get install git
WORKDIR /root
RUN git clone https://github.com/veebch/hometime.git