![image](https://user-images.githubusercontent.com/42485856/133894956-b66c5f2f-68f9-446b-933e-23d72359c98a.png)

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
Sau khi cài đặt, bạn có thể cho user hiện tại thuộc group docker, để khi gõ lệnh không cần xin quyền "**sudo**"
```
sudo usermod -aG docker $USER
```
Logout sau đó login lại để có hiệu lực.

============================================================================
```
$ docker                      Liệt kê tất cả các lệnh con trong docker
$ docker image --help         Đưa ra các hướng dẫn trợ giúp về các lệnh con có trong image, và tương tự với các lệnh khác
```
![image](https://user-images.githubusercontent.com/42485856/133465267-0c271afe-182d-40d1-808d-d40d3f1572f8.png)

[Image]() trong docker là những phần mềm được đóng gói và quản lý bởi docker. VD như image đóng gói phần mềm php, image đóng gói hệ điều hành ubuntu...vv. Trong docker các [image]() "**chỉ có thể đọc không thể sửa đổi**". Khi [image]() được docker khởi chạy thì phiên bản thực thi của image được gọi là các [container](). Các [container]() thì "**có thể ghi được các dữ liệu vào trong đó**'. Như vậy là để có [container]() để chạy các ứng dụng thì chúng ta phải có [image]() trước

[image]() là một gói phần mềm trong đó chứa những thứ cần như thư viện, các file cấu hình, biến môi trường để chạy mội ứng dụng nào đó. Nó giống như cái USB chứa bộ cài đặt hệ điều hành Windows!

Khi một phiên bản của [image]() chạy, phiên bản chạy đó gọi là [container]() - (vậy muốn có container phải có image). Bất ký lúc nào bạn cũng có thể kiểm tra xem có bao nhiêu [container]() đang chạy và nó sinh ra từ [image]() nào.

Bước đầu, để có [image]() nào đó bạn tải về từ https://hub.docker.com/search?q=&type=image, tại đó có đủ các loại phù hợp với công việc của bạn!

![image](https://user-images.githubusercontent.com/42485856/133891060-72aa2669-a4db-40de-8c9d-46cb9b099085.png)


- **REPOSITORY** : là tên của image
- **TAG** : là phiên bản của image, với giá trị latest có nghĩa là bản cuối. Muốn tải về bản khác latest vào mục TAGS trên https://hub.docker.com/search?q=&type=image tìm bản phù hợp.
- **IMAGE ID** : là một chuỗi định danh duy nhất của image trên hệ thống của bạn.
```
$ docker search ubuntu                                                      Tìm kiếm các phiên bản trực tiếp bằng lệnh docker
```

## 1. Kiểm tra phiên bản docker
`$ docker --version`
Hoặc thông tin chi tiết hơn:
`$ docker info`

## 2. Liệt kê tất cả các image
```
docker images
docker images -a
```

## 3. Tải về một image (imagename) từ hub.docker.com
```
docker pull repository:tag                                                  VD: docker pull ubuntu:20.04
```
Hoặc tải về bản mới nhất
```
docker pull repository                                                      (Mặc định sẽ tải phiên bản mới nhất )
```

## 4. Liệt kê tất cả các container
```
docker container ls -a
docker container ls --all
```
![image](https://user-images.githubusercontent.com/42485856/133483878-2abf20bf-aa8d-4d7d-b581-d768da346cc1.png)

- **CONTAINER ID** : một con số (mã hash) gán cho container, bạn dùng mã này để quản lý container này, như xóa bỏ, khởi động, dừng lại ...
- **IMAGE** : cho biết container sinh ra từ image nào.
- **COMMAND** : cho biết lệnh, ứng dụng chạy khi container chạy (/bin/bash là terminate)
- **STATUS** : cho biết trạng thái, (exit - đang dừng)

## 5. Xóa một image (phải không có container nào đang chạy)
```
docker image rm imageid                                                     Chỉ cần ghi ký tự đầu của IMAGE ID docker vẫn hiểu và tự xóa
docker image rm repository:tag                                              Thêm -f là bắt buộc xóa
```

## 6. Xóa container
```
docker container rm containerid
```

## 7. Xóa container đang chạy
```
docker rm -f NAME
docker rm -f ID
```

## 8. Tạo mới và Chạy một container
```
docker run -it repository:tag
docker run -it imageid                                                    
```
- -i  có nghĩa duy trì mở stdin để nhập lệnh.
- -t  nó có nghĩa là console, cho phép kết nối với terminal để tương tác

Kiểm tra thông tin phiên bản của image ubuntu:
```
cat /etc/*release
```

## 9. Đặt tên cho container, đặt hostname cho container 
Cấu trúc: `docker run -it --name "CONTAINER NAME" -h HOSTNAME image`
```
docker run -it --name "ABC" -h ubuntu1 repository:tag
```
![image](https://user-images.githubusercontent.com/42485856/133892005-84f0cc2f-4acc-4b9e-b142-15d05b9433d1.png)


### 10. Kiểm tra có các container nào đang chạy
```
docker ps
```
Nếu muốn liệt kê tất cả các container kể cả những container không chạy gõ lệnh
```
docker ps -a
```

## 11. Vào termial container đang chạy
```
docker attach containerid
docker container attach containerid
```

## 12. Chạy container đang dừng
```
docker start containerid
docker container start -i containerid
```

## 13. Chạy một lệnh trên container đang chạy
```
docker exec -it containerid command
```

## 14. Thoát termial vẫn giữ container đang chạy
```
CTRL + P, CTRL + Q
CRT + P rồi Q
```

## 15. Đang đứng ở host ép container bắt buộc dừng lại
```
docker stop containerid
docker stop name
```

## 16. Dừng và thoát hẳn container trong terminal
```
exit
```

## 17. Đang đứng bên ngoài container nhưng muốn thi hành lệnh trong container đang chạy
```
docker exec CONTAINER lệnh                    VD: $ docker exec U1 ls 
```

```
docker exec -it CONTAINER lệnh
```
- (tham số -it: nhận input và kết nối terminal + Tên container + lệnh thực thi ) ~ Lệnh này tương tự như lệnh attch \
VD : docker exec -it U1 bash ---> (lệnh bash kết nối luôn với terminal)


## 18. Lưu container thành Images
Muốn commit **CONTAINER** nào trở thành **IMAGE** thì **CONTAINER** đó phải ở trạng thái "**dừng**"
```
docker commit CONTAINER IMAGE:TAG              VD: $ docker commit U1 ubuntu-nano:version1
```
![image](https://user-images.githubusercontent.com/42485856/133897653-01f094dc-3316-476c-a730-398b4569e326.png)

## 19. Lưu Image ra thành file (Đóng gói )
```
docker save --output name.tar IMAGE_ID
```

## Một vài tham số khác:

Tạo và chạy container, container tự xóa khi kết thúc thì thêm vào tham số --rm
```
docker run -it --rm ubuntu
```
Tạo và chạy container - khi container chạy thi hành ngay một lệnh nào đó, ví dụ ls -la
```
docker run -it --rm debian ls -la
```
Tạo và chạy container - ánh xạ một thự mục máy host vào một thư mục container, chia sẻ dữ liệu
```
docker run -it --rm -v path-in-host:path-in-container debian
```
Vào container đang đang chạy

Kiểm tra xem bằng lệnh docker ps, nếu có một container với ID là containerid đang chạy, để quay quay trở lại terminal của nó dùng lệnh:
```
docker container attach containerid
```
Chạy một container đang dừng
```
docker container start -i containerid
```
Nếu cần xóa bỏ hẳn một container thì dùng lệnh
```
docker container rm containerid
```
![image](https://user-images.githubusercontent.com/42485856/133487593-b81f3306-9f5e-412c-a50d-9a49713c0e13.png)

