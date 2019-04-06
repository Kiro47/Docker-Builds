FROM ubuntu:16.04

RUN apt update
RUN apt install -y software-properties-common

RUN add-apt-repository -y ppa:openjdk-r/ppa
RUN add-apt-repository -y ppa:cwchien/gradle
RUN apt update
RUN apt install -y wget curl zip unzip gradle-5.0 openjdk-11-jre git gcc g++ bash bison flex jython 
RUN mkdir --parents ~/.gradle/init.d/
RUN mkdir --parents ~/git/ghidra.bin/
RUN cd ~/git && git clone https://github.com/NationalSecurityAgency/ghidra.git ~/git/ghidra.bin/
COPY repos.gradle /root/.gradle/init.d/repos.gradle

RUN mkdir ~/flatRepo ~/Downloads

RUN cd ~/Downloads
RUN curl -OL https://github.com/pxb1988/dex2jar/releases/download/2.0/dex-tools-2.0.zip
RUN unzip dex-tools-2.0.zip
RUN cp dex2jar-2.0/lib/dex-*.jar ~/flatRepo/

RUN cd ~/flatRepo && curl -OL https://storage.googleapis.com/google-code-archive-downloads/v2/code.google.com/android4me/AXMLPrinter2.jar

RUN cd ~/Downloads && curl -OL https://sourceforge.net/projects/catacombae/files/HFSExplorer/0.21/hfsexplorer-0_21-bin.zip
RUN mkdir ~/Downloads/hfsx 

RUN cd ~/Downloads/hfsx &&  unzip ../hfsexplorer-0_21-bin.zip && cd lib && cp csframework.jar hfsx_dmglib.jar hfsx.jar iharder-base64.jar ~/flatRepo/

RUN update-alternatives --set java /usr/lib/jvm/java-11-openjdk-amd64/bin/java

RUN cd ~/git/ghidra.bin/ && gradle prepDev -x yajswDevUnpack && gradle sleighCompile && gradle buildNatives_linux64


RUN cd ~/Downloads  && curl -OL https://sourceforge.net/projects/yajsw/files/yajsw/yajsw-stable-12.12/yajsw-stable-12.12.zip
RUN mkdir -p ~/git/ghidra.bin/Ghidra/Features/GhidraServer/ 
RUN cp ~/Downloads/yajsw-stable-12.12.zip ~/git/ghidra.bin/Ghidra/Features/GhidraServer/

RUN cd ~/git/ghidra.bin/ && gradle yajswDevUnpack && gradle buildGhidra



