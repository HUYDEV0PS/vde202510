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

----
Giải pháp ChatGPT để không mất file README.md khi reset

# Quy Trình Backup – Reset – Restore Để Tạo Pull Request Đúng Chuẩn

Khi làm việc với Git, đặc biệt trong trường hợp cần đồng bộ lại lịch sử commit giữa **fork** và **repo gốc**, bạn sẽ phải chạy:

```
git reset --hard upstream/main
```

Lệnh này sẽ đưa repo của bạn về đúng trạng thái của repo gốc, bao gồm:

* Xóa toàn bộ file của bạn trong thư mục
* Thay thế bằng toàn bộ file từ repo gốc
* Ghi đè README.md của bạn bằng README.md gốc

Đây là hành vi **bình thường** và **bắt buộc** để tạo PR đúng chuẩn.
Tuy nhiên, bạn vẫn muốn giữ lại toàn bộ code của mình — đặc biệt là file README.md đã tự viết.
Vì vậy, bạn cần **backup trước khi reset**.

---

## 🔥 Quy Trình Đúng Chuẩn

### 1️⃣ Backup toàn bộ code trước khi reset

```bash
mkdir ~/backup_l7
cp -r /home/ubuntu/homework/l7/* ~/backup_l7/
```

Tiếp theo, bạn tiến hành reset repo:

```bash
git reset --hard upstream/main
```

Sau lệnh này:

* README.md gốc sẽ xuất hiện lại
* File của bạn biến mất (tạm thời)
* Lịch sử commit đã đồng bộ với repo gốc

---

### 2️⃣ Khôi phục code của bạn sau khi reset

Copy toàn bộ file từ bản backup vào lại thư mục dự án:

```bash
cp -r ~/backup_l7/* /home/ubuntu/homework/l7/
```

Lúc này:

* Toàn bộ code của bạn được khôi phục
* README.md của bạn cũng trở lại
* Lịch sử commit vẫn giữ nguyên theo repo gốc → sẵn sàng tạo PR

---

### 3️⃣ Commit và push code lên repo fork của bạn

```bash
git add .
git commit -m "Add WordPress & MySQL Kubernetes manifests"
git push -f origin main
```

Vì lịch sử commit đã thay đổi nên cần dùng:

```
-f  (force push)
```

---

## 🎉 Kết quả

* README.md của bạn **không bị mất**
* README.md của bạn **xuất hiện trong Pull Request**
* Repo gốc sẽ nhận được README.md **phiên bản do bạn viết**
* Bạn đã đồng bộ lịch sử commit đúng chuẩn, PR sẽ tạo được mà không lỗi

---

## 📝 Tóm tắt quy trình

| Bước                   | Mục đích                                     |
| ---------------------- | -------------------------------------------- |
| Backup code            | Giữ lại toàn bộ file của bạn trước khi reset |
| Reset về upstream/main | Đồng bộ lịch sử commit để GitHub tạo PR      |
| Restore code           | Đưa code của bạn trở lại thư mục dự án       |
| Commit & push          | Đẩy code lên repo fork để tạo PR             |
| Tạo Pull Request       | Gửi thay đổi về repo gốc                     |

---

