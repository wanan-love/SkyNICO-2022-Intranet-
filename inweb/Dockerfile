FROM nginx
LABEL author="wanan"
COPY inweb/inrun.sh /tmp/inrun.sh
COPY inweb/PaintedEggshell /root/PaintedEggshell
RUN sed -i 's/deb.debian.org/mirrors.aliyun.com/' /etc/apt/sources.list  \
    && sed -i 's/security.debian.org/mirrors.aliyun.com/' /etc/apt/sources.list \
    && apt -y update  \
    && apt -y upgrade  \
    && apt install -y net-tools openssh-server vim inetutils-ping \
    && sed -i 's/#Port 22/Port 443/' /etc/ssh/sshd_config \
    && useradd testuser -m \
    && chown root /home/testuser \
    && chmod +x /tmp/inrun.sh

RUN ["/bin/bash", "-c", "passwd root <<-EOF\nroot\nroot\nEOF"]
RUN ["/bin/bash", "-c", "passwd testuser <<-EOF\n!QAZ2wsx\n!QAZ2wsx\nEOF"]
COPY inweb/flag /home/testuser/flag
ENTRYPOINT /tmp/inrun.sh && tail -f /dev/null
