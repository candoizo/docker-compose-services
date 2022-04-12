# Development environment setup
# RUN git clone $GITHUB_BASE_GIT --single-branch --depth 1 --branch $GITHUB_BASE_BRANCH $BUGZILLA_WWW \
#     && ln -sf $BUGZILLA_LIB $BUGZILLA_WWW/local
# COPY conf/checksetup_answers.txt $BUGZILLA_WWW/checksetup_answers.txt
# RUN bugzilla_config.sh
# RUN su - $BUGZILLA_USER -c dev_config.sh
#
# RUN chown -R $BUGZILLA_USER.$BUGZILLA_USER $BUGZILLA_WWW /home/$BUGZILLA_USER

RUN pacman -Sy openvpn transmission-cli --noconfirm --noprogress


RUN openvpn --daemon vpnd --config /torrent/vpn.ovpn


RUN ip rule add from $(ip route get 1 | grep -Po '(?<=src )(\S+)') table 128

RUN ip route add table 128 to $(ip route get 1 | grep -Po '(?<=src )(\S+)')/32 dev $(ip -4 route ls | grep default | grep -Po '(?<=dev )(\S+)')

RUN ip route add table 128 default via $(ip -4 route ls | grep default | grep -Po '(?<=via )(\S+)')


RUN curl ifconfig.io

RUN transmission-remote 172.17.0.2:9091 -o -pt

CMD ["/usr/bin/supervisord", "-c", "/etc/supervisord.conf"]
