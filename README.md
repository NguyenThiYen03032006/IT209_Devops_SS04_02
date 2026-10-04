# Báo cáo Bài tập 2: Quản lý nhánh và Giải quyết xung đột (Merge Conflict)


## 2. Các bước thực hiện bài tập

### Bước 1: Khởi tạo kho lưu trữ và tạo nhánh chính (main)
1. Tạo thư mục bài tập và khởi tạo Git:
   ```bash
   mkdir -p homework/session_04/ex2
   cd homework/session_04/ex2
   git init
   ```
2. Tạo tệp `README.md` ban đầu trên nhánh `main`:
   ```bash
   echo "# Dự án Quản lý phiên bản" > README.md
   git add README.md
   git commit -m "Initial commit on main"
   ```

### Bước 2: Tạo và phát triển trên nhánh phụ (feature-update)
1. Tạo và chuyển sang nhánh mới `feature-update`:
   ```bash
   git checkout -b feature-update
   ```
2. Thêm nội dung mới vào `README.md` trên nhánh phụ:
   ```bash
   echo "Tính năng mới đang phát triển trên nhánh feature-update" >> README.md
   git add README.md
   git commit -m "Update README on feature-update branch"
   ```

### Bước 3: Quay lại nhánh `main` và tạo xung đột
1. Chuyển trở lại nhánh `main`:
   ```bash
   git checkout main
   ```
2. Chỉnh sửa cùng dòng/đoạn trong `README.md` trên nhánh `main`:
   ```bash
   echo "Cập nhật quan trọng trên nhánh main" >> README.md
   git add README.md
   git commit -m "Update README on main branch"
   ```

### Bước 4: Gộp nhánh và xử lý Merge Conflict thủ công
1. Tiến hành gộp nhánh `feature-update` vào `main`:
   ```bash
   git merge feature-update
   ```
   *(Git thông báo xung đột tại file `README.md`)*

2. Mở file `README.md` để kiểm tra các ký hiệu đánh dấu xung đột:
   ```text
   <<<<<<< HEAD
   Cập nhật quan trọng trên nhánh main
   =======
   Tính năng mới đang phát triển trên nhánh feature-update
   >>>>>>> feature-update
   ```

3. **Xử lý thủ công:** Xóa các ký hiệu `<<<<<<<`, `=======`, `>>>>>>>` và chỉnh sửa lại nội dung hoàn chỉnh mong muốn:
   ```text
   Cập nhật quan trọng trên nhánh main và tích hợp tính năng từ nhánh feature-update.
   ```

4. Lưu file và hoàn tất gộp nhánh:
   ```bash
   git add README.md
   git commit -m "Resolve merge conflict between main and feature-update"
   ```

---

## 3. Kiểm tra lịch sử Commit (Đồ thị nhánh)

Sử dụng lệnh kiểm tra lịch sử dạng đồ thị:
```bash
git log --graph --oneline
```

**Kết quả hiển thị mong đợi:**
```text
*   <commit-hash> (HEAD -> main) Resolve merge conflict between main and feature-update
|\  
| * <commit-hash> (feature-update) Update README on feature-update branch
* | <commit-hash> Update README on main branch
|/  
* <commit-hash> Initial commit on main
```
