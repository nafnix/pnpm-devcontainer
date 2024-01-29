# syntax=docker/dockerfile:1
FROM mcr.microsoft.com/devcontainers/base:bookworm

ARG DEBIAN_FRONTEND=noninteractive

# RUN ln -sf /usr/share/zoneinfo/Asia/Shanghai /etc/localtime

ARG USER=vscode
USER ${USER}
ARG HOME=/home/${USER}
WORKDIR ${HOME}

ARG PNPM_HOME=${HOME}/.local/share/pnpm
ENV PATH="${PNPM_HOME}:$PATH"
RUN <<EOT
    wget -qO- https://get.pnpm.io/install.sh | ENV="${HOME}/.zshrc" SHELL=/bin/zsh sh -
    pnpm env use -g lts
EOT

# ARG OHMYZSH_HOME=${HOME}/.oh-my-zsh
# ARG OHMYZSH_THEME=${OHMYZSH_HOME}/custom/themes
# RUN <<EOT
#     git clone --depth=1 https://github.com/romkatv/powerlevel10k.git ${OHMYZSH_THEME}/powerlevel10k
#     sed -i 's|ZSH_THEME="devcontainers"|ZSH_THEME="powerlevel10k/powerlevel10k"|g' .zshrc
#     echo 'POWERLEVEL9K_DISABLE_CONFIGURATION_WIZARD=true' >> .zshrc
# EOT

RUN echo 'alias pn=pnpm' >> .zshrc