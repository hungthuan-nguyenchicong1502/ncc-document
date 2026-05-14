# cap quang
RUN sed -i 's/dl-cdn.alpinelinux.org/mirror.leaseweb.com/g' /etc/apk/repositories

CMD ["sh", "-c", "tail -f >/dev/nul"]
