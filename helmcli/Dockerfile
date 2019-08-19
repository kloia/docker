ARG DOCKER_VERSION=latest
FROM docker:${DOCKER_VERSION}
MAINTAINER docker@kloia.com

ARG COMPOSE_VERSION


ENV KUBECTL_VERSION=v1.12.0
ENV HELM_VERSION=v2.12.3

RUN apk add --no-cache \
  curl \
  python \
  py-pip \
  libffi \
  && \
  apk add --no-cache --virtual .build-deps \
  build-base \
  libffi-dev \
  python-dev \
  openssl-dev \
  make \
  git \
  bash \
  openssh \
  gettext

RUN pip install "docker-compose${COMPOSE_VERSION:+==}${COMPOSE_VERSION}" \ 
  awscli \
  awsebcli \
  direnv \
  pipenv

RUN apk --no-cache update \
     && curl -LO https://storage.googleapis.com/kubernetes-release/release/${KUBECTL_VERSION}/bin/linux/amd64/kubectl \
     && mv kubectl /usr/local/bin/kubectl \
     && curl -LO https://storage.googleapis.com/kubernetes-helm/helm-${HELM_VERSION}-linux-amd64.tar.gz \
     && tar -zxvf helm-${HELM_VERSION}-linux-amd64.tar.gz \
     && mv linux-amd64/helm /usr/local/bin/helm \
     && chmod +x /usr/local/bin/kubectl /usr/local/bin/helm \
     && rm -rf helm-${HELM_VERSION}-linux-amd64.tar.gz
