FROM ubuntu:focal

RUN apt-get update && \
    apt-get install --quiet --yes software-properties-common && \
    add-apt-repository --yes ppa:fish-shell/release-3 && \
    apt-get install --quiet --yes fish

SHELL ["fish", "--command"]

RUN chsh -s /usr/bin/fish

ENV SHELL /usr/bin/fish

ENTRYPOINT [ "fish" ]
