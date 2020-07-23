FROM ubuntu:focal

RUN apt-get update && \
    apt-get install --quiet --yes software-properties-common && \
    add-apt-repository --yes ppa:fish-shell/release-3 && \
    apt-get install --quiet --yes fish && \
	apt-get install -y build-essential \
	libssl-dev \
	zlib1g-dev \
	libbz2-dev \
	libreadline-dev \
	libsqlite3-dev \
	wget \
	llvm \
	libncurses5-dev \
	libncursesw5-dev \
	xz-utils \
	tk-dev \
	libffi-dev \
	liblzma-dev \
	python-openssl \
	locales \
	locales-all \
	tmux \
	git \
	neovim \
	curl \
	nodejs \
	stow


ENV LC_ALL "en_US.UTF-8"
ENV LANG "en_US.UTF-8"
ENV LANGUAGE "en_US.UTF-8"

RUN useradd --create-home \
	--shell /usr/bin/fish admin && \
	echo "admin:admin" | chpasswd && adduser admin sudo

RUN chown -R admin: /home/admin
USER admin

SHELL ["fish", "--command"]
# RUN chsh -s /usr/bin/fish
ENV SHELL /usr/bin/fish

RUN curl https://pyenv.run | bash

ENV HOME /home/admin
WORKDIR $HOME
RUN git clone https://github.com/turing-complet/dotfiles.git

RUN curl -fLo ~/.vim/autoload/plug.vim --create-dirs \
    https://raw.githubusercontent.com/junegunn/vim-plug/master/plug.vim


WORKDIR dotfiles
RUN stow fish
RUN stow vim
RUN stow nvim
RUN stow tmux

RUN source ~/.config/fish/config.fish
RUN pyenv install 3.8.3
RUN pyenv global 3.8.3
RUN pyenv virtualenv venv-tools
RUN pyenv activate venv-tools
RUN pip install black jedi pynvim

RUN vim +PlugInstall +qall

WORKDIR $HOME
ENTRYPOINT [ "fish" ]
