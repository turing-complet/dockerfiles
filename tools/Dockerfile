FROM ubuntu:focal

ENV DEBIAN_FRONTEND noninteractive
ENV TZ America/Los_Angeles

RUN apt-get update -y && apt-get upgrade -y
RUN apt-get install -y software-properties-common build-essential

RUN apt-get install -y \
    python3.9 python3.9-venv python3-pip && \
	# ctags
	apt-get install -y gcc make pkg-config autoconf automake \
	python3-docutils libseccomp-dev libjansson-dev \
	libyaml-dev libxml2-dev && \
	# other packages
	apt-get install -y locales locales-all \
	zsh tmux git curl nodejs npm \
	stow jq sudo

ENV LC_ALL "en_US.UTF-8"
ENV LANG "en_US.UTF-8"
ENV LANGUAGE "en_US.UTF-8"

RUN git clone https://github.com/universal-ctags/ctags.git
WORKDIR ctags
RUN ./autogen.sh && ./configure && make && make install

RUN npm install -g tldr pyright

RUN useradd --create-home \
	--shell /usr/bin/zsh admin && \
	echo "admin:admin" | chpasswd && adduser admin sudo

RUN chown -R admin: /home/admin
USER admin
ENV HOME /home/admin
WORKDIR $HOME

RUN sh -c "$(curl -fsSL https://raw.github.com/ohmyzsh/ohmyzsh/master/tools/install.sh)"
RUN curl -LO https://github.com/neovim/neovim/releases/download/v0.6.0/nvim.appimage && \
    chmod u+x nvim.appimage && \
    ./nvim.appimage --appimage-extract

SHELL ["zsh", "-c"]
ENV SHELL /usr/bin/zsh

RUN git clone https://github.com/turing-complet/dotfiles.git
WORKDIR $HOME/dotfiles
RUN stow vim
RUN stow nvim
RUN stow tmux
RUN rm ~/.zshrc && stow zsh

WORKDIR $HOME
RUN source ~/.zshrc
RUN python3 -m pip install nox tox ipython black pynvim

RUN echo "let g:python3_host_prog = 'python3'" >> .vimrc
RUN echo "alias nvim=$HOME/squashfs-root/usr/bin/nvim" >> .zshrc
ENTRYPOINT [ "zsh" ]
