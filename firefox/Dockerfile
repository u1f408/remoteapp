FROM docker.io/alpine:edge
EXPOSE 5900

RUN apk add --no-cache tini tigervnc openbox xterm firefox python3 py3-xdg shadow font-dejavu
ADD startup /usr/local/bin/startup
RUN useradd -m user && mkdir -p /home/user/.vnc /home/user/.config/openbox /home/user/.mozilla
ADD autostart /home/user/.config/openbox/autostart
RUN sh -c 'echo session=openbox > /home/user/.vnc/config' && sh -c 'echo Passw0rd | vncpasswd -f > /home/user/.vnc/passwd' && chmod 600 /home/user/.vnc/passwd && chown -R user: /home/user

USER user
ENV USER=user
ENV HOME=/home/user
ENTRYPOINT ["/sbin/tini"]
CMD ["/usr/local/bin/startup"]
