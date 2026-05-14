# cap quang

printf "https://mirror.leaseweb.com/alpine/latest-stable/main\\nhttps://mirror.leaseweb.com/alpine/latest-stable/community\\n" > /etc/apk/repositories

RUN printf "https://mirror.leaseweb.com/alpine/latest-stable/main\\nhttps://mirror.leaseweb.com/alpine/latest-stable/community\\n" > /etc/apk/repositories

apk update && apk upgrade

RUN printf "https://mirror.leaseweb.com/alpine/latest-stable/main\\nhttps://mirror.leaseweb.com/alpine/latest-stable/community\\n" \\
	> /etc/apk/repositories

apk update && apk upgrade

RUN sed -i 's/dl-cdn.alpinelinux.org/mirror.leaseweb.com/g' /etc/apk/repositories

sed -i 's/dl-cdn.alpinelinux.org/mirror.leaseweb.com/g' /etc/apk/repositories

vi /etc/apk/repositories

https://dl-cdn.alpinelinux.org/alpine/v3.19/main
https://dl-cdn.alpinelinux.org/alpine/v3.19/community

https://mirror.leaseweb.com/alpine/latest-stable/main
https://mirror.leaseweb.com/alpine/latest-stable/community

apk update && apk upgrade