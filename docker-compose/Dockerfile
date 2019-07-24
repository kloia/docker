FROM docker:18.09
ARG COMPOSE_VERSION
ARG IMAGE_TYPE="fat"
RUN apk add --no-cache \
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
  && \
  if [[ "${IMAGE_TYPE}" == "fat" ]]; then \
    apk add --no-cache \
    bash \
    ca-certificates \
    git \
    perl \
    openssh-client \
    curl \
    gnupg \
    openjdk8 \
    openssl \
  ; fi \
  && \
  pip install "docker-compose${COMPOSE_VERSION:+==}${COMPOSE_VERSION}" \
  && \
  if [[ "${IMAGE_TYPE}" == "fat" ]]; then \
    pip install awscli awsebcli direnv pipenv \
  ; fi && \
  apk del .build-deps

