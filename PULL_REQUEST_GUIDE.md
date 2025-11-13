Dưới đây là nội dung **định dạng Markdown (.md)** — bạn có thể copy nguyên file:

---

```md
# Hướng dẫn tạo Pull Request (PR) trên GitHub

## Bước 1: Fork repo gốc
1. Mở repo gốc:  
   https://github.com/vntechies/vde202510
2. Nhấn nút **Fork** (góc phải trên).
3. GitHub sẽ tạo một bản sao repo vào tài khoản của bạn.  
   Ví dụ:  
   https://github.com/HUYDEV0PS/vde202510

---

## Bước 2: Chuẩn bị thư mục code
Chuyển đến thư mục chứa code bạn muốn đẩy lên GitHub, ví dụ:
```

/homework/l7

````

---

## Bước 3: Khởi tạo Git repo mới
```sh
cd /homework/l7
rm -rf .git     # Xóa repo cũ nếu có
git init
````

---

## Bước 4: Kết nối repo local với repo fork

```sh
git remote add origin https://github.com/HUYDEV0PS/vde202510.git
git remote -v
```

Kết quả mong đợi:

```
origin  https://github.com/HUYDEV0PS/vde202510.git (fetch)
origin  https://github.com/HUYDEV0PS/vde202510.git (push)
```

---

## Bước 5: Thêm remote repo gốc (upstream)

```sh
git remote add upstream https://github.com/vntechies/vde202510.git
git fetch upstream
```

---

## Bước 6: Reset code để đồng bộ với repo gốc

```sh
git reset --hard upstream/main
```

> Sau bước này, thư mục sẽ rỗng hoặc chỉ còn các file của repo gốc.

---

## Bước 7: Add code, commit và push lên repo cá nhân

```sh
git add .
git commit -m "Add WordPress & MySQL Kubernetes code"
git push -f origin main   # push force vì đã thay đổi lịch sử commit
```

---

## Tiếp theo: Tạo Pull Request

1. Truy cập repo fork của bạn trên GitHub.
2. Nhấn **Compare & pull request**.
3. Kiểm tra thay đổi và nhấn **Create Pull Request**.

---

```

---

Nếu bạn muốn, tôi có thể tạo file `.md` để bạn tải về luôn.
```
