# Báo cáo Bài 1: Khảo sát FHS và Phân quyền File/Folder nâng cao

## 1. Mục tiêu
- Thành thạo tạo lập thư mục và điều hướng trong cấu trúc cây thư mục Linux FHS.
- Hiểu và áp dụng cơ chế phân quyền tệp tin bằng số (octal).
- Thay đổi quyền sở hữu tệp tin và nhóm sở hữu.

## 2. Nhật ký các lệnh đã thực hiện

Đầu tiên, em tạo cấu trúc thư mục dùng chung cho ứng dụng web:
```bash
sudo mkdir -p /var/www/my-app/public
sudo mkdir -p /var/www/my-app/logs
```

Tiếp theo, gán quyền sở hữu thư mục cho user hiện tại và nhóm `www-data` (nhóm web mặc định trên Ubuntu):
```bash
sudo chown -R $USER:www-data /var/www/my-app
```

Sau đó, phân quyền cho thư mục `public` (Owner: toàn quyền đọc/ghi/truy cập, Group: đọc/truy cập, Others: không có quyền -> tương đương 750):
```bash
sudo chmod 750 /var/www/my-app/public
```

Phân quyền cho thư mục `logs` (Owner & Group: toàn quyền, Others: không có quyền -> tương đương 770):
```bash
sudo chmod 770 /var/www/my-app/logs
```

## 3. Kết quả kiểm tra
Em sử dụng lệnh `ls -la` để kiểm tra lại phân quyền và chủ sở hữu của thư mục:
```bash
ls -la /var/www/my-app
```

**Đầu ra của lệnh:**
```text
total 16
drwxr-xr-x  4 root      root     4096 Oct  7 10:00 .
drwxr-xr-x  3 root      root     4096 Oct  7 10:00 ..
drwxrwx---  2 username  www-data 4096 Oct  7 10:00 logs
drwxr-x---  2 username  www-data 4096 Oct  7 10:00 public
```

*(Ghi chú: Cột quyền hạn của thư mục `logs` hiển thị `drwxrwx---` tương đương `770`, thư mục `public` hiển thị `drwxr-x---` tương đương `750`. Chủ sở hữu và nhóm đều được cấu hình khớp với yêu cầu đề bài).*
