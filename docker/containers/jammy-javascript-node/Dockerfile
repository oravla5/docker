FROM buildpack-deps:jammy

ARG USERNAME=dev

RUN groupadd --gid 1000 ${USERNAME} \
  && useradd --uid 1000 --gid ${USERNAME} --shell /bin/bash --create-home ${USERNAME} 