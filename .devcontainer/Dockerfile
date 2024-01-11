# syntax=docker/dockerfile:1
FROM library/debian:latest

ARG USER=vscode
ARG DEBIAN_FRONTEND=noninteractive
RUN apt update \
    && apt install -y --no-install-recommends sudo zsh git curl wget apt-transport-https ca-certificates \
    && apt autoremove -y \
    && rm -rf /var/lib/apt/lists/* \
    && useradd -m -s /bin/zsh ${USER} \
    && echo "${USER} ALL=(ALL) NOPASSWD: ALL" >/etc/sudoers.d/${USER} \
    && chmod 0440 /etc/sudoers.d/${USER}


USER ${USER}
ARG HOME=/home/${USER}
WORKDIR ${HOME}

ARG PNPM_HOME=${HOME}/.local/share/pnpm
ENV PATH="${PNPM_HOME}:$PATH"
RUN <<EOT
    wget -qO- https://get.pnpm.io/install.sh | ENV="${HOME}/.zshrc" SHELL=/bin/zsh sh -
    pnpm env use -g lts
    echo 'alias pn=pnpm' >> .zshrc
EOT

ARG OHMYZSH_HOME=${HOME}/.oh-my-zsh
ARG OHMYZSH_THEME=${OHMYZSH_HOME}/custom/themes
RUN <<EOT
    sh -c "$(curl -fsSL https://install.ohmyz.sh)"
    mkdir -p ${OHMYZSH_THEME}
    git clone --depth=1 https://github.com/romkatv/powerlevel10k.git ${OHMYZSH_THEME}/powerlevel10k
    sed -i 's|ZSH_THEME="robbyrussell"|ZSH_THEME="powerlevel10k/powerlevel10k"|g' .zshrc
    echo 'POWERLEVEL9K_DISABLE_CONFIGURATION_WIZARD=true' >> .zshrc
EOT