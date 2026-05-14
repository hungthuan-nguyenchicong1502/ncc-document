# cap quang
RUN printf "https://mirror.leaseweb.com/alpine/latest-stable/main\\nhttps://mirror.leaseweb.com/alpine/latest-stable/community\\n" \\
	> /etc/apk/repositories


RUN sed -i 's/dl-cdn.alpinelinux.org/mirror.leaseweb.com/g' /etc/apk/repositories

