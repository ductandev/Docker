# Docker
```
echo "# Docker" >> README.md
git init
git add README.md
git commit -m "first commit"
git branch -M main
git remote add origin https://github.com/ductandev/Docker.git
git push -u origin main
```

## Cài Docker trên Ubuntu

Chạy các lệnh để cài đặt:
```
$ sudo apt update
$ sudo apt install apt-transport-https ca-certificates curl software-properties-common
$ curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo apt-key add -
$ sudo add-apt-repository "deb [arch=amd64] https://download.docker.com/linux/ubuntu bionic stable"
$ sudo apt update
$ apt-cache policy docker-ce
$ sudo apt install docker-ce
$ sudo systemctl status docker
```
Sau khi cài đặt, bạn có thể cho user hiện tại thuộc group docker, để khi gõ lệnh không cần xin quyền **sudo**
```
sudo usermod -aG docker $USER
```
Logout sau đó login lại để có hiệu lực.


## 1. Kiểm tra phiên bản docker
`$ docker --version`
Hoặc thông tin chi tiết hơn:
`$ docker info`

## 2. Liệt kê các image
docker images -a

## 3. Xóa một image (phải không container nào đang dùng)
docker images rm imageid

## 4. Tải về một image (imagename) từ hub.docker.com
docker pull imagename

## 5. Liệt kê các container
docker container ls -a

## 6. Xóa container
docker container rm containerid

## 7. Tạo mới và Chạy một container
docker run -it imageid `

## 8. Thoát termial vẫn giữ container đang chạy
CTRL +P, CTRL + Q

## 9. Vào termial container đang chạy
docker container attach containerid

## 10. Chạy container đang dừng
docker container start -i containerid

## 11. Chạy một lệnh trên container đang chạy
docker exec -it containerid command
