FROM ubuntu:bionic

RUN apt-get update && apt-get install -y \
	build-essential \
	ca-certificates \
	git \
	qml-module-qtgraphicaleffects \
	qml-module-qt-labs-folderlistmodel \
	qml-module-qt-labs-settings \
	qml-module-qtquick-controls \
	qml-module-qtquick-dialogs \
	qmlscene qt5-default \
	qt5-qmake \
	qtdeclarative5-dev \
	qtdeclarative5-localstorage-plugin \
	qtdeclarative5-qtquick2-plugin \
	qtdeclarative5-window-plugin \
	--no-install-recommends \
	&& rm -rf /var/lib/apt/lists/*

RUN git clone --depth 1 --recursive https://github.com/Swordfish90/cool-retro-term.git /src
WORKDIR /src
RUN qmake \
	&& make

ENTRYPOINT [ "/src/cool-retro-term" ]
