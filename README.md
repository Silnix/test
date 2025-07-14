# Hệ Thống Quản Lý Thư Viện

## Cấu trúc dự án
- `frontend/` - Ứng dụng Vue.js
- `backend/` - API server Node.js/Express
- `GD/` - Thư mục chứa thiết kế giao diện

## Cài đặt và chạy

### 1. Cài đặt dependencies

#### Backend
```bash
cd backend
npm install
```

#### Frontend
```bash
cd frontend
npm install
```

### 2. Khởi động MongoDB
Đảm bảo MongoDB đang chạy trên localhost:27017

### 3. Chạy Backend
```bash
cd backend
npm start
```
Backend sẽ chạy trên http://localhost:5000

### 4. Chạy Frontend
```bash
cd frontend
npm run dev
```
Frontend sẽ chạy trên http://localhost:5173

## API Endpoints

### Đăng ký
- **POST** `/api/auth/register`
- Body: `{ username, password, ho_ten, email, dia_chi }`

### Đăng nhập
- **POST** `/api/login`
- Body: `{ username, password }`

### Kiểm tra danh sách users (debug)
- **GET** `/api/users`
- Trả về danh sách tất cả users (không bao gồm password)

### Lấy danh sách độc giả (users loại 2)
- **GET** `/api/users/readers`
- Trả về danh sách chỉ users loại 2 (độc giả)

### Cập nhật thông tin user
- **PUT** `/api/users/:id`
- Body: `{ ho_ten, dia_chi, email }`
- Cập nhật thông tin người dùng theo ID

### Xóa user
- **DELETE** `/api/users/:id`
- Xóa người dùng theo ID

### Thống kê tổng quan
- **GET** `/api/stats/overview`
- Trả về số liệu tổng quan: users, books, borrows, categories

### Thống kê đăng ký theo tháng
- **GET** `/api/stats/registrations`
- Trả về số lượng đăng ký theo từng tháng trong năm

### Thống kê mượn sách theo tháng
- **GET** `/api/stats/borrows`
- Trả về số lượng mượn sách theo từng tháng trong năm

### Thống kê sách theo danh mục
- **GET** `/api/stats/books-by-category`
- Trả về phân bố sách theo danh mục

### Tìm kiếm sách
- **GET** `/api/books/search?q=keyword`

## Tính năng đã hoàn thành

### Frontend
- ✅ Form đăng ký với đầy đủ thông tin
- ✅ Validation form
- ✅ Kết nối API đăng ký
- ✅ Chuyển hướng sau đăng ký thành công

### Backend
- ✅ API đăng ký với validation
- ✅ Model User với đầy đủ trường
- ✅ Tự động sinh ID người dùng
- ✅ Kiểm tra trùng lặp username/email
- ✅ CORS configuration

## Cơ sở dữ liệu
- Database: `QLTV`
- Collection: `NGUOIDUNG`
- Schema User: `ID`, `username`, `password`, `ho_ten`, `dia_chi`, `email`, `loai`

### Loại người dùng (trường `loai`)
- `1` = Admin/Quản trị viên
- `2` = Người dùng thường (mặc định khi đăng ký)

## Test hệ thống

### Chạy test tự động
```bash
node test-register.js
```

### Kiểm tra thủ công
1. Truy cập `http://localhost:5000/api/users` để xem danh sách users
2. Đăng ký qua frontend tại `http://localhost:5173/register`
3. Kiểm tra lại danh sách users để xác nhận user mới đã được thêm 