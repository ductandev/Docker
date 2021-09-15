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

========================================================================================
```
$ docker                      Liệt kê tất cả các lệnh con trong docker
$ docker image --help         Đưa ra các hướng dẫn trợ giúp về các lệnh con có trong image, và tương tự với các lệnh khác
```
![image](https://user-images.githubusercontent.com/42485856/133465267-0c271afe-182d-40d1-808d-d40d3f1572f8.png)

[Image]() trong docker là những phần mềm được đóng gói và quản lý bởi docker. VD như image đóng gói phần mềm php, image đóng gói hệ điều hành ubuntu...vv. Trong docker các [image]() "**chỉ có thể đọc không thể sửa đổi**". Khi [image]() được docker khởi chạy thì phiên bản thực thi của image được gọi là các [container](). Các [container]() thì "**có thể ghi được các dữ liệu vào trong đó**'. Như vậy là để có [container]() để chạy các ứng dụng thì chúng ta phải có [image]() trước

[image]() là một gói phần mềm trong đó chứa những thứ cần như thư viện, các file cấu hình, biến môi trường để chạy mội ứng dụng nào đó. Nó giống như cái USB chứa bộ cài đặt hệ điều hành Windows!

Khi một phiên bản của [image]() chạy, phiên bản chạy đó gọi là [container]() - (vậy muốn có container phải có image). Bất ký lúc nào bạn cũng có thể kiểm tra xem có bao nhiêu [container]() đang chạy và nó sinh ra từ [image]() nào.

Bước đầu, để có [image]() nào đó bạn tải về từ https://hub.docker.com/search?q=&type=image, tại đó có đủ các loại phù hợp với công việc của bạn!

- **Repository**: là tên của image
- **TAG**: là phiên bản của image, với giá trị latest có nghĩa là bản cuối. Muốn tải về bản khác latest vào mục TAGS trên https://hub.docker.com/search?q=&type=image tìm bản phù hợp.
- **IMAGE ID**: là một chuỗi định danh duy nhất của image trên hệ thống của bạn.
```
$ docker search ubuntu         Tìm kiếm các phiên bản trực tiếp bằng lệnh docker
```

## 1. Kiểm tra phiên bản docker
`$ docker --version`
Hoặc thông tin chi tiết hơn:
`$ docker info`

## 2. Liệt kê tất cả các image
```
docker images -a
```

## 3. Xóa một image (phải không container nào đang dùng)
```
docker image rm imageid                         Chỉ cần ghi ký tự đầu của IMAGE ID docker vẫn hiểu và tự xóa
docker image rm Tên_image:tag
```

## 4. Tải về một image (imagename) từ hub.docker.com
```
docker pull Tên_image:tag                                VD: docker pull ubuntu:20.04
```

## 5. Liệt kê các container
```
docker container ls -a
```

## 6. Xóa container
```
docker container rm containerid
```

## 7. Tạo mới và Chạy một container
```
docker run -it Tên_image:lastest
docker run -it imageid                      (kết nối với terminal -t)
```

## 8. Thoát termial vẫn giữ container đang chạy
CTRL +P, CTRL + Q

## 9. Vào termial container đang chạy
```
docker container attach containerid
```

## 10. Chạy container đang dừng
```
docker container start -i containerid
```

## 11. Chạy một lệnh trên container đang chạy
```
docker exec -it containerid command
```
