## Thông tin sinh viên

* **Họ tên:** Nguyễn Trịnh Tiến Đạt
* **Mã sinh viên:** 23810310148
* **Lớp:** D18CNPM2


## 1. Cách cài đặt dự án

### Bước 1: Clone source code

```bash
git clone https://github.com/NTTDat7525/Oauth_NguyenTrinhTienDat_23810310148 [tên project]
cd [tên project]
```

### Bước 2: Cài đặt thư viện

```bash
composer install
```

### Bước 3: Tạo file môi trường

```bash
cp .env.example .env
```

### Bước 4: Tạo khóa ứng dụng

```bash
php artisan key:generate
```

### Bước 5: Cấu hình database trong file `.env`

```env
tạo database tên oauth trong mysql và cấu hình env

DB_CONNECTION=mysql
DB_HOST=127.0.0.1
DB_PORT=3306
DB_DATABASE=oauth
DB_USERNAME=root
DB_PASSWORD=
```

### Bước 6: Chạy migration

```bash
php artisan migrate
```

### Bước 7: Chạy ứng dụng

```bash
php artisan serve
```

Truy cập:

```bash
http://127.0.0.1:8000
```

---

## 2. Cách cấu hình Google OAuth

### Bước 1:

Truy cập Google Cloud Console:

```bash
https://console.cloud.google.com/
```

### Bước 2:

Tạo Project mới.

### Bước 3:

Vào:

```bash
APIs & Services -> Credentials
```

### Bước 4:

Chọn:

```bash
Create Credentials -> OAuth Client ID
```

### Bước 5:

Chọn loại ứng dụng:

```bash
Web application
```

### Bước 6:

Thêm Redirect URI:

```bash
http://127.0.0.1:8000/auth/google/callback
```

### Bước 7:

Nhận được:

* `GOOGLE_CLIENT_ID`
* `GOOGLE_CLIENT_SECRET`

### Bước 8:

Thêm vào file `.env`

```env
GOOGLE_CLIENT_ID=your_google_client_id
GOOGLE_CLIENT_SECRET=your_google_client_secret
GOOGLE_REDIRECT_URI=http://127.0.0.1:8000/auth/google/callback
```

---

# Chưa nhận được mã của meta (sử dụng tài khoản của Bùi Minh Đức để test)
## 3. Cách cấu hình Facebook OAuth 

### Bước 1:

Truy cập:

```bash
https://developers.facebook.com/
```

### Bước 2:

Tạo ứng dụng mới với use case:

```bash
Authenticate and request data from users with Facebook Login
```

### Bước 3:

Thêm sản phẩm:

```bash
Facebook Login
```

### Bước 4:

Vào:

```bash
Settings -> Basic
```

Lấy:

* `App ID`
* `App Secret`

### Bước 5:

Thêm vào file `.env`

```env
FACEBOOK_CLIENT_ID=your_facebook_app_id
FACEBOOK_CLIENT_SECRET=your_facebook_app_secret
FACEBOOK_REDIRECT_URI=http://localhost:8000/auth/facebook/callback
```

### Bước 6:

Trong Facebook Login settings, cấu hình callback:

```bash
http://localhost:8000/auth/facebook/callback
```

---

## 4. Cấu hình services.php

Trong file:

```bash
config/services.php
```

thêm:

```php
'google' => [
    'client_id' => env('GOOGLE_CLIENT_ID'),
    'client_secret' => env('GOOGLE_CLIENT_SECRET'),
    'redirect' => env('GOOGLE_REDIRECT_URI'),
],

'facebook' => [
    'client_id' => env('FACEBOOK_CLIENT_ID'),
    'client_secret' => env('FACEBOOK_CLIENT_SECRET'),
    'redirect' => env('FACEBOOK_REDIRECT_URI'),
],
```
