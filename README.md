# Docker-Nginx-Passenger-Rails

## Dockerfile

```
FROM phusion/passenger-ruby24:0.9.26
```
``FROM`` khai báo base image là passenger-ruby24 của phusion với tag name 0.9.26
```
RUN /etc/my_init.d/00_regen_ssh_host_keys.sh
```
Do baseimage-docker mặc định disables SSH server, đoạn code trên có tác dụng enable chúng.
```
CMD ["/sbin/my_init"]
```
Thực thi init process trong `/sbin/my_init` <br>
CMD tương tự như RUN nó sẽ thực thi một câu lệnh, nhưng điểm khác biệt là các lệnh trong CMD sẽ mặc định được thực thi khi chạy docker run còn các lệnh trong RUN sẽ được thực khi khi chạy docker build
```
WORKDIR /tmp
```
Chỉ định nơi các lệnh như `RUN, ADD, COPPY,..` theo sau nó được thực thi.

```
ADD Gemfile /tmp/
```
Nó copy những tập tin từ nguồn trên máy chủ hoặc remote file URL vào đích trên filesystem của image

```
RUN bundle install
```
`RUN` thực thi một lệnh trong quá trình build image.

## Clone source

* Clone with SSH: <br>
```
git clone git@github.com:saiury92/docker-passenger-rails.git
```
* Clone with HTTPS: <br>
```
git clone https://github.com/saiury92/docker-passenger-rails.git
```

## Build image

```
docker build -t saiury92/passenger-ruby /path/to/docker-passenger-rails
```
## Run conatainer

```
docker run -it -p 8080:80 saiury92/passenger-ruby
```

## Run rails app

```
http://0.0.0.0:8080/
```
