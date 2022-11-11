FROM projectmonai/monai:1.0.1


### Set environment variables
# Change default Shell to bash
SHELL ["/bin/bash", "-c"]
# Set Timezone
ARG DEBIAN_FRONTEND=noninteractive
ENV TZ=Asia/Seoul
# Set python encoding type
ENV PYTHONIOENCODING=UTF-8
# Set Beep theme
ENV BEEP_MARIO='-f 130 -l 100 -n -f 262 -l 100 -n -f 330 -l 100 -n -f 392 -l 100 -n -f 523 -l 100 -n -f 660 -l 100 -n -f 784 -l 300 -n -f 660 -l 300 -n -f 146 -l 100 -n -f 262 -l 100 -n -f 311 -l 100 -n -f 415 -l 100 -n -f 523 -l 100 -n -f 622 -l 100 -n -f 831 -l 300 -n -f 622 -l 300 -n -f 155 -l 100 -n -f 294 -l 100 -n -f 349 -l 100 -n -f 466 -l 100 -n -f 588 -l 100 -n -f 699 -l 100 -n -f 933 -l 300 -n -f 933 -l 100 -n -f 933 -l 100 -n -f 933 -l 100 -n -f 1047 -l 400'


### Change settings
# Change Timezone
# RUN ln -snf /usr/share/zoneinfo/$TZ /etc/localtime && echo $TZ > /etc/timezone
# Change bash shell prompt color of root account
# RUN sed -i 's/    xterm-color) color_prompt=yes;;/    #xterm-color) color_prompt=yes;;\n    xterm-color|*-256color) color_prompt=yes;;/' /root/.bashrc
RUN sed -i 's/#force_color_prompt=yes/force_color_prompt=yes/' /root/.bashrc
# Change original green color of bash shell prompt to red color
RUN sed -i 's/    PS1=\x27${debian_chroot:+(\$debian_chroot)}\\\[\\033\[01;32m\\\]\\u@\\h\\\[\\033\[00m\\\]:\\\[\\033\[01;34m\\\]\\w\\\[\\033\[00m\\\]\\\$ \x27/    PS1=\x27\${debian_chroot:+(\$debian_chroot)}\\\[\\033\[01;31m\\\]\\u@\\h\\\[\\033\[00m\\\]:\\\[\\033\[01;34m\\\]\\w\\\[\\033\[00m\\\]\\\$ \x27/' /root/.bashrc
# Update PubKey
RUN apt-key adv --keyserver keyserver.ubuntu.com --recv-keys A4B469963BF863CC

# Install essential packages
RUN apt update \
    && apt install -y \
        tzdata \
        beep \
        wget \
        git \
        ca-certificates \
        apt-transport-https
# Change Ubuntu repository address to Kakao server in Republic of Korea
RUN sed -i 's/^deb http:\/\/archive.ubuntu.com/deb http:\/\/mirror.kakao.com/g' /etc/apt/sources.list
RUN sed -i 's/^deb http:\/\/security.ubuntu.com/deb http:\/\/mirror.kakao.com/g' /etc/apt/sources.list


### Setup requirements
# Install pytorch requirements
RUN apt update \
    && apt install -y \
        libglu1-mesa-dev \
        libglib2.0-0 \
        libsm6 \
        libxext6 \
        libxrender-dev

# Configure default Pypi repository
RUN mkdir -p ~/.config/pip \
    && echo -e \
"[global]\n"\
"index-url=https://mirror.kakao.com/pypi/simple/\n"\
"trusted-host=mirror.kakao.com\n"\
        > ~/.config/pip/pip.conf \
    && pip install -U pip

### Postprocessing & Cleaning
# Add Bash alias
RUN echo 'alias l="ls -alh --full-time"' >> ~/.bashrc
RUN echo 'alias cls="clear"' >> ~/.bashrc

# Welcome message
RUN echo "echo -e '\x1b[1;32m      ___           ___           ___           ___                 \n     /__/\\         /  /\\         /__/\\         /  /\\        ___     \x1b[0;36mMedical Open Network for Artificial Intelligence\x1b[1;32m\n    |  |::\\       /  /::\\        \\  \\:\\       /  /::\\      /  /\\    \x1b[1;32mAI Toolkit for Healthcare Imaging\n    |  |:|:\\     /  /:/\\:\\        \\  \\:\\     /  /:/\\:\\    /  /:/    \n  __|__|:|\\:\\   /  /:/  \\:\\   _____\\__\\:\\   /  /:/~/::\\  /__/::\\    \n /__/::::| \\:\\ /__/:/ \\__\\:\\ /__/::::::::\\ /__/:/ /:/\\:\\ \\__\\/\\:\\__ \n \\  \\:\\~~\\__\\/ \\  \\:\\ /  /:/ \\  \\:\\~~\\~~\\/ \\  \\:\\/:/__\\/    \\  \\:\\/\\n  \\  \\:\\        \\  \\:\\  /:/   \\  \\:\\  ~~~   \\  \\::/          \\__\\::/\n   \\  \\:\\        \\  \\:\\/:/     \\  \\:\\        \\  \\:\\          /__/:/ \n    \\  \\:\\        \\  \\::/       \\  \\:\\        \\  \\:\\         \\__\\/  \n     \\__\\/         \\__\\/         \\__\\/         \\__\\/                \n\x1b[0m'" >> ~/.bashrc
RUN echo "echo -e '\x1b[0;33mUbuntu\t'\$(sed -n '/VERSION=/p' /etc/os-release | cut -d '\"' -f 2)" >> ~/.bashrc
RUN echo "echo -e 'Python \t'\$(python -V | cut -d ' ' -f 2)" >> ~/.bashrc
RUN echo "echo -e 'PIP \t'\$(pip -V | cut -d '(' -f 1 | cut -d ' ' -f 2-)" >> ~/.bashrc
RUN echo "echo -e '\t'\$(sed -n '/index-url/p' ~/.config/pip/pip.conf)" >> ~/.bashrc
RUN echo "echo -e -n 'PyTorch' && echo \$(pip freeze | grep ^torch) | sed 's/torch//' | sed 's/ /\n\t/g' | sed 's/==/ /g'" >> ~/.bashrc
RUN echo "echo -n -e '\x1b[0m'" >> ~/.bashrc

RUN echo "if command -v nvidia-smi &> /dev/null" >> ~/.bashrc
RUN echo "then" >> ~/.bashrc
RUN echo "    echo -e -n '\x1b[0;33mCUDA\t' && echo -e \$(nvcc -V) | grep 'Cuda compilation tools' | cut -d ',' -f 3 | sed 's/ V//g' | cut -d ' ' -f 1" >> ~/.bashrc
RUN echo "    echo -e '\tcuDNN '\$(grep '^#define CUDNN_' /usr/include/cudnn_version.h | cut -d ' ' -f 3 | sed -z 's/\n//' | sed -z 's/\n/./g') | sed 's/.(CUDNN_MAJOR.//'" >> ~/.bashrc
RUN echo "    echo -e '\x1b[0;32m' && nvidia-smi -L && echo -e '\x1b[0m'" >> ~/.bashrc
RUN echo "else" >> ~/.bashrc
RUN echo "echo -e -n '\n'" >> ~/.bashrc
RUN echo "fi" >> ~/.bashrc

# Clean the cache
RUN apt clean \
    && rm -rf /var/lib/apt/lists/*
# Set workspace
WORKDIR /workspace