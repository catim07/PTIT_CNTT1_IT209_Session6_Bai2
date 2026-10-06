# Bài 2: Áp dụng Kỹ thuật Stash để Quản lý Công việc Đang Dở dở (Git Stash Workflows)

## Mục tiêu
- Sử dụng `git stash` để lưu tạm các thay đổi chưa commit khi cần chuyển sang xử lý tác vụ khẩn cấp.
- Khôi phục công việc lưu tạm và quản lý danh sách stash (`stash list`, `stash pop`, `stash drop`).

---

## 1. Bối cảnh & Các bước thực hiện

### Bước 1: Phát triển dở dang trên nhánh `feature/checkout`
Giả sử đang thực hiện tính năng thanh toán nhưng có thay đổi chưa commit:
```bash
echo "const cart = [];" > checkout.js
echo "// Work in progress logic..." >> checkout.js
```

Kiểm tra trạng thái làm việc (`git status`):
```text
On branch feature/checkout
Changes not staged for commit:
  modified:   checkout.js
```

### Bước 2: Tạm cất thay đổi bằng `git stash`
Do cần chuyển gấp sang sửa lỗi Hotfix, tiến hành cất giữ trạng thái hiện tại:
```bash
git stash save "WIP: dang lam do tinh nang checkout"
```

Kiểm tra thư mục làm việc sau khi stash:
```bash
git status
# Working tree clean
```

### Bước 3: Kiểm tra danh sách Stash
```bash
git stash list
```

**Kết quả màn hình:**
```text
stash@{0}: On feature/checkout: WIP: dang lam do tinh nang checkout
```

### Bước 4: Khôi phục công việc sau khi hoàn thành tác vụ khẩn cấp
Sau khi hoàn thành tác vụ khác, quay lại nhánh `feature/checkout` và khôi phục mã nguồn:
```bash
git stash pop
```

---

## 2. Kết quả sau khi Khôi phục

```bash
git status
```

**Màn hình kết quả:**
```text
On branch feature/checkout
Changes not staged for commit:
  modified:   checkout.js
```

Nội dung mã dở dang trong file `checkout.js` đã được khôi phục đầy đủ.

---

## 3. Kết luận
- `git stash` giúp lập trình viên linh hoạt chuyển đổi giữa các nhánh và tác vụ mà không bị ràng buộc phải commit các mã nguồn chưa hoàn chỉnh hoặc rác vào lịch sử Git.
