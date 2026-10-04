# Bài 5: Thiết lập thư mục Web an toàn tại phân vùng hệ thống (/opt/)

## Các bước thực hiện

### 1. Tạo cấu trúc thư mục mới
Tạo thư mục chứa mã nguồn và lưu log trong `/opt/`:
```bash
sudo mkdir -p /opt/my-app/html
sudo mkdir -p /opt/my-app/logs
```

### 2. Phân quyền sở hữu đệ quy
Đổi chủ sở hữu thành user `devops` và nhóm thành `www-data` (để Nginx có thể truy cập):
```bash
sudo chown -R devops:www-data /opt/my-app/
```

### 3. Cấu hình phân quyền truy cập
```bash
# Đặt quyền cho các thư mục (devops toàn quyền đọc/ghi/thực thi, www-data đọc/thực thi)
sudo find /opt/my-app/ -type d -exec chmod 750 {} \;

# Đặt quyền cho các file mã nguồn (devops đọc/ghi, www-data chỉ đọc)
sudo find /opt/my-app/html/ -type f -exec chmod 640 {} \;

# Cấp quyền đặc biệt cho group www-data trên thư mục logs để Nginx có thể ghi file log
sudo chmod 770 /opt/my-app/logs/
```

## Kiểm tra kết quả

### Kiểm tra phân quyền:
```bash
ls -la /opt/my-app/
```
**Kết quả đầu ra của lệnh `ls -la /opt/my-app/`:**
```text
[Học viên chèn kết quả đầu ra tại đây]
```

### Ghi thử file bằng user devops:
```bash
echo "Update Test" >> /opt/my-app/html/index.html
```
**Log quá trình ghi thành công (không có sudo):**
```text
[Học viên chèn log terminal không lỗi permission denied tại đây]
```

### Kiểm tra nội dung log truy cập của Nginx:
```bash
tail -f /opt/my-app/logs/access.log
```
**Nội dung log:**
```text
[Học viên chèn một số dòng log Nginx trả về sau khi request thử trên trình duyệt tại đây]
```
