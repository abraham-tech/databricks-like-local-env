FROM openjdk:11-jre-slim

ENV POLYNOTE_VERSION=0.5.0

WORKDIR /polynote

RUN apt-get update && \
    apt-get install -y wget unzip && \
    wget https://github.com/polynote/polynote/releases/download/v${POLYNOTE_VERSION}/polynote-dist.tar.gz && \
    tar -xzf polynote-dist.tar.gz --strip-components=1 && \
    rm polynote-dist.tar.gz && \
    apt-get remove -y wget unzip && \
    apt-get autoremove -y && \
    apt-get clean

COPY config /polynote/config
COPY notebooks /polynote/notebooks

EXPOSE 8192

CMD ["/polynote/polynote.py"]
