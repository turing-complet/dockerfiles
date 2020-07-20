FROM ubuntu:focal

RUN apt-get update && \
    apt-get install --quiet --yes software-properties-common && \
    add-apt-repository --yes ppa:fish-shell/release-3 && \
    apt-get install --quiet --yes fish && \
	apt-get install -y build-essential \
	tmux \
	git \
	neovim \
	curl \
	stow


SHELL ["fish", "--command"]
RUN chsh -s /usr/bin/fish
ENV SHELL /usr/bin/fish

RUN curl https://pyenv.run | bash

WORKDIR /home
RUN git clone https://github.com/turing-complet/dotfiles.git

RUN curl -fLo ~/.vim/autoload/plug.vim --create-dirs \
    https://raw.githubusercontent.com/junegunn/vim-plug/master/plug.vim

WORKDIR dotfiles
RUN stow fish
RUN stow vim
RUN vim +PlugInstall +qall

ENTRYPOINT [ "fish" ]
