FROM nvcr.io/nvidia/pytorch:22.04-py3
RUN apt update -y && apt install -y zip htop screen libgl1-mesa-glx sudo git black

# Install requirements.txt
COPY requirements.txt .
RUN pip install -r requirements.txt

# Create user & add to sudoers
ARG USERNAME=user
ARG USER_UID=1000
ARG USER_GID=$USER_UID
ARG USER_SH=/bin/bash
RUN groupadd -g $USER_GID $USERNAME \
  && useradd -u $USER_UID -g $USER_GID -s $USER_SH -m $USERNAME \
  && echo $USERNAME ALL=\(root\) NOPASSWD:ALL > /etc/sudoers.d/$USERNAME \
  && chmod 0440 /etc/sudoers.d/$USERNAME

USER $USERNAME