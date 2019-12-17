# otus-web

Простая защита от DDOS
Написать конфигурацию nginx, которая даёт доступ клиенту только с определенной cookie.
Если у клиента её нет, нужно выполнить редирект на location, в котором кука будет добавлена, после чего клиент будет обратно отправлен (редирект) на запрашиваемый ресурс.

Смысл: умные боты попадаются редко, тупые боты по редиректам с куками два раза не пойдут


# Работоспособность

Поднимаем стенд `vagrant up`

Заходим без куков
```
mario@mario:~/otus/otus-web$ curl -I 192.168.10.10
HTTP/1.1 302 Moved Temporarily
Server: nginx/1.16.1
Date: Tue, 17 Dec 2019 05:25:07 GMT
Content-Type: text/html
Content-Length: 145
Connection: keep-alive
Location: http://192.168.10.10/setc
Set-Cookie: base_uri=http://192.168.10.10/
```
Заходим с куками
```
mario@mario:~/otus/otus-web$ curl -I --cookie "secret=otus" http://192.168.10.10
HTTP/1.1 200 OK
Server: nginx/1.16.1
Date: Tue, 17 Dec 2019 05:33:10 GMT
Content-Type: text/html
Content-Length: 4833
Last-Modified: Fri, 16 May 2014 15:12:48 GMT
Connection: keep-alive
ETag: "53762af0-12e1"
Accept-Ranges: bytes
```
