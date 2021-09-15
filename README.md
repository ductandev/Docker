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

# kiểm tra phiên bản
docker --version

# liệt kê các image
docker images -a

# xóa một image (phải không container nào đang dùng)
docker images rm imageid

# tải về một image (imagename) từ hub.docker.com
docker pull imagename

# liệt kê các container
docker container ls -a

# xóa container
docker container rm containerid

# tạo mới một container
docker run -it imageid 

# thoát termial vẫn giữ container đang chạy
CTRL +P, CTRL + Q

# Vào termial container đang chạy
docker container attach containerid

# Chạy container đang dừng
docker container start -i containerid

# Chạy một lệnh trên container đang chạy
docker exec -it containerid command
