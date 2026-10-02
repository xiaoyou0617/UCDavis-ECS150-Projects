#The image to be loaded/downloaded
FROM --platform=linux/amd64 ubuntu:22.04

#Updating package lists
RUN apt-get update -y -o Acquire::http::Pipeline-Depth=0 -o Acquire::http::No-Cache=true -o Acquire::BrokenProxy=true
RUN apt-get update --fix-missing -y -o Acquire::http::Pipeline-Depth=0 -o Acquire::http::No-Cache=true -o Acquire::BrokenProxy=true

#Installing libraries
RUN apt-get install -y gdb gdbserver vim emacs libssl-dev lynx build-essential g++ libstdc++6 cmake clang lldb git -o Acquire::http::Pipeline-Depth=0 -o Acquire::http::No-Cache=true -o Acquire::BrokenProxy=true
