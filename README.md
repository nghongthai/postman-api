# Báo cáo tìm hiểu và thực hành kiểm thử API bằng Postman

## Mục Lục

1. [API là gì? Tại sao cần test?](#1-api-là-gì-tại-sao-cần-test)
2. [Postman là gì?](#2-postman-là-gì)
3. [Giao diện Postman](#3-giao-diện-postman)
4. [HTTP Methods](#4-http-methods)
5. [Gửi request đầu tiên với GET](#5-gửi-request-đầu-tiên-với-get)
6. [Cấu trúc một API URL](#6-cấu-trúc-một-api-url)
7. [Headers và Authorization](#7-headers-và-authorization)
8. [Gửi dữ liệu với POST Request](#8-gửi-dữ-liệu-với-post-request)
9. [Upload file với form-data](#9-upload-file-với-form-data)
10. [Collections](#10-collections)
11. [Environments và Variables](#11-environments-và-variables)
12. [Viết Test Script tự động](#12-viết-test-script-tự-động)
13. [Chạy Collection Runner](#13-chạy-collection-runner)
14. [Newman](#14-newman)
15. [Đọc và phân tích Response](#15-đọc-và-phân-tích-response)
16. [Ứng dụng Postman trong thực tế](#16-ứng-dụng-postman-trong-thực-tế)
17. [Best Practices và Checklist](#17-best-practices-và-checklist)
18. [Roadmap học Postman](#18-roadmap-học-postman)
19. [Kết luận](#19-kết-luận)
20. [Tài liệu tham khảo](#20-tài-liệu-tham-khảo)
21. [Phụ lục hình ảnh](#phụ-lục-danh-sách-hình-ảnh-cần-chụp)

---

## 1. API là gì? Tại sao cần test?

### 1.1. Khái niệm API

API là viết tắt của **Application Programming Interface**, nghĩa là giao diện lập trình ứng dụng. API cho phép các phần mềm hoặc hệ thống khác nhau giao tiếp và trao đổi dữ liệu với nhau.

Trong hệ thống web hoặc ứng dụng di động, API thường đóng vai trò trung gian giữa giao diện người dùng và máy chủ. Ví dụ, khi người dùng đăng nhập vào một ứng dụng, giao diện sẽ gửi tên đăng nhập và mật khẩu đến API. API tiếp nhận dữ liệu, kiểm tra thông tin trong cơ sở dữ liệu và trả về kết quả đăng nhập.

Quy trình giao tiếp cơ bản:

```text
Người dùng
    ↓
Giao diện ứng dụng
    ↓
API
    ↓
Máy chủ và cơ sở dữ liệu
    ↓
Kết quả trả về cho người dùng
```

API thường được sử dụng trong các chức năng như:

- Đăng ký tài khoản.
- Đăng nhập.
- Lấy thông tin người dùng.
- Thêm, sửa và xóa dữ liệu.
- Thanh toán trực tuyến.
- Gửi thông báo.
- Tải lên hoặc tải xuống tập tin.
- Kết nối với hệ thống bên thứ ba.

### 1.2. REST API

REST API là loại API phổ biến trong phát triển ứng dụng web hiện nay. REST API sử dụng giao thức HTTP và các phương thức như `GET`, `POST`, `PUT`, `PATCH`, `DELETE` để thao tác với dữ liệu.

Dữ liệu trao đổi giữa client và server thường có định dạng JSON.

```json
{
  "id": 1,
  "name": "Nguyen Van A",
  "email": "nguyenvana@example.com"
}
```

### 1.3. Tại sao cần kiểm thử API?

Kiểm thử API giúp xác định API có hoạt động đúng với yêu cầu hay không. Việc giao diện hoạt động bình thường không có nghĩa API không có lỗi.

Các lỗi API thường gặp:

- Trả về sai dữ liệu.
- Trả về sai mã trạng thái HTTP.
- Không kiểm tra dữ liệu đầu vào.
- Cho phép truy cập khi chưa đăng nhập.
- Làm lộ thông tin nhạy cảm.
- Không xử lý đúng dữ liệu rỗng.
- Không kiểm tra dữ liệu trùng lặp.
- Phản hồi quá chậm.
- Xảy ra lỗi khi có nhiều request.
- Không xử lý đúng ký tự đặc biệt.

Lợi ích của kiểm thử API:

- Phát hiện lỗi sớm trước khi xây dựng hoàn chỉnh giao diện.
- Kiểm tra trực tiếp logic xử lý phía máy chủ.
- Thực hiện nhanh hơn kiểm thử giao diện.
- Dễ tự động hóa.
- Có thể kiểm tra nhiều trường hợp dữ liệu.
- Hỗ trợ đánh giá tính bảo mật của hệ thống.
- Giảm chi phí sửa lỗi trong giai đoạn sau.

---

## 2. Postman là gì?

Postman là một công cụ hỗ trợ phát triển, kiểm thử và quản lý API. Postman cho phép người dùng gửi request đến máy chủ và xem response mà không cần xây dựng giao diện ứng dụng.

Postman hỗ trợ các phương thức HTTP phổ biến:

- `GET`
- `POST`
- `PUT`
- `PATCH`
- `DELETE`
- `HEAD`
- `OPTIONS`

Một số chức năng chính của Postman:

- Gửi HTTP Request.
- Kiểm tra nội dung Response.
- Thêm Header và tham số.
- Gửi dữ liệu JSON.
- Gửi dữ liệu form-data.
- Tải tập tin lên máy chủ.
- Sử dụng Authorization.
- Tổ chức request bằng Collection.
- Quản lý biến môi trường.
- Viết test script tự động.
- Chạy nhiều request bằng Collection Runner.
- Xuất và nhập Collection.
- Tạo tài liệu API.
- Chạy kiểm thử bằng Newman.

### 2.1. Ưu điểm của Postman

- Giao diện trực quan và dễ sử dụng.
- Phù hợp với người mới học kiểm thử API.
- Hỗ trợ nhiều phương thức HTTP.
- Có thể lưu và tái sử dụng request.
- Hỗ trợ JavaScript để viết test.
- Hỗ trợ làm việc nhóm.
- Có khả năng quản lý nhiều môi trường.
- Dễ dàng tích hợp vào CI/CD thông qua Newman.
- Có phiên bản sử dụng trên máy tính và trình duyệt.

### 2.2. Hạn chế của Postman

- Phiên bản miễn phí có một số giới hạn.
- Collection lớn có thể trở nên khó quản lý.
- Không phải là công cụ chuyên dụng để kiểm thử tải lớn.
- Người dùng cần biết JavaScript khi viết các test phức tạp.
- Việc đồng bộ dữ liệu cần tài khoản Postman.

![Trang chủ Postman](images/01-trang-chu-postman.png)

---

## 3. Giao diện Postman

Giao diện Postman gồm nhiều khu vực phục vụ quá trình tạo, quản lý và thực hiện kiểm thử API.

### 3.1. Workspace

Workspace là không gian làm việc chứa Collection, Environment, API và lịch sử request. Người dùng có thể tạo:

- Personal Workspace.
- Team Workspace.
- Public Workspace.

### 3.2. Collections

Collections là nơi nhóm các request có liên quan với nhau.

```text
Postman API Testing
├── Authentication
│   ├── Register
│   └── Login
├── Users
│   ├── Get All Users
│   ├── Get User By ID
│   ├── Create User
│   ├── Update User
│   └── Delete User
```

### 3.3. Request Builder

Request Builder là khu vực dùng để nhập:

- Phương thức HTTP.
- URL.
- Params.
- Authorization.
- Headers.
- Body.
- Scripts.
- Settings.

### 3.4. Response Viewer

Response Viewer hiển thị kết quả máy chủ trả về:

- Response Body.
- HTTP Status Code.
- Response Time.
- Response Size.
- Response Headers.
- Cookies.
- Kết quả test.

### 3.5. Environment Selector

Environment Selector cho phép lựa chọn môi trường đang sử dụng như:

- Development.
- Testing.
- Staging.
- Production.

### 3.6. History

History lưu lại các request đã gửi trước đó. Người dùng có thể mở lại request từ lịch sử nếu chưa lưu vào Collection.

![Tổng quan giao diện Postman](images/02-giao-dien-postman.png)

---

## 4. HTTP Methods

HTTP Method thể hiện hành động mà client muốn thực hiện đối với tài nguyên trên server.

| Phương thức | Chức năng | Ví dụ |
| --- | --- | --- |
| `GET` | Lấy dữ liệu | Lấy danh sách người dùng |
| `POST` | Tạo dữ liệu mới | Tạo tài khoản |
| `PUT` | Cập nhật toàn bộ dữ liệu | Thay đổi toàn bộ hồ sơ |
| `PATCH` | Cập nhật một phần dữ liệu | Thay đổi tên |
| `DELETE` | Xóa dữ liệu | Xóa người dùng |

### 4.1. GET

`GET` được sử dụng để lấy dữ liệu từ server.

```http
GET https://jsonplaceholder.typicode.com/posts
```

### 4.2. POST

`POST` được sử dụng để tạo dữ liệu mới.

```http
POST https://jsonplaceholder.typicode.com/posts
```

```json
{
  "title": "Bài viết mới",
  "body": "Nội dung bài viết",
  "userId": 1
}
```

### 4.3. PUT

`PUT` được sử dụng để cập nhật toàn bộ thông tin của một tài nguyên.

```http
PUT https://jsonplaceholder.typicode.com/posts/1
```

```json
{
  "id": 1,
  "title": "Tiêu đề mới",
  "body": "Nội dung mới",
  "userId": 1
}
```

### 4.4. PATCH

`PATCH` được sử dụng để cập nhật một phần thông tin của tài nguyên.

```http
PATCH https://jsonplaceholder.typicode.com/posts/1
```

```json
{
  "title": "Tiêu đề đã cập nhật"
}
```

### 4.5. DELETE

`DELETE` được sử dụng để xóa một tài nguyên.

```http
DELETE https://jsonplaceholder.typicode.com/posts/1
```

---

## 5. Gửi request đầu tiên với GET

Trong phần này, API mẫu JSONPlaceholder được sử dụng để thực hành.

URL lấy danh sách bài viết:

```text
https://jsonplaceholder.typicode.com/posts
```

### 5.1. Các bước thực hiện

1. Mở Postman.
2. Chọn tạo một HTTP Request mới.
3. Chọn phương thức `GET`.
4. Nhập URL `https://jsonplaceholder.typicode.com/posts`.
5. Nhấn `Send`.
6. Quan sát kết quả trong khu vực Response.

Kết quả trả về là danh sách các bài viết dưới dạng JSON.

```json
[
  {
    "userId": 1,
    "id": 1,
    "title": "sunt aut facere repellat provident occaecati",
    "body": "quia et suscipit..."
  }
]
```

Mã trạng thái nhận được:

```http
200 OK
```

![Gửi GET Request](images/03-get-request.png)

### 5.2. Lấy một phần tử theo ID

```text
https://jsonplaceholder.typicode.com/posts/1
```

Kết quả:

```json
{
  "userId": 1,
  "id": 1,
  "title": "sunt aut facere repellat provident occaecati",
  "body": "quia et suscipit..."
}
```

![GET bài viết theo ID](images/04-get-post-by-id.png)

---

## 6. Cấu trúc một API URL

Một API URL có thể gồm các thành phần sau:

```text
https://api.example.com:443/v1/users/10?status=active
```

| Thành phần | Giá trị | Ý nghĩa |
| --- | --- | --- |
| Protocol | `https` | Giao thức giao tiếp |
| Host | `api.example.com` | Địa chỉ máy chủ |
| Port | `443` | Cổng kết nối |
| Base Path | `/v1` | Phiên bản API |
| Resource | `/users` | Tài nguyên |
| Path Parameter | `/10` | ID của tài nguyên |
| Query Parameter | `status=active` | Điều kiện lọc |

### 6.1. Path Parameter

Path Parameter là một phần trực tiếp của URL, thường dùng để xác định một tài nguyên cụ thể.

```text
https://jsonplaceholder.typicode.com/posts/1
```

Trong đó `1` là ID của bài viết.

### 6.2. Query Parameter

Query Parameter được đặt sau dấu `?`.

```text
https://jsonplaceholder.typicode.com/posts?userId=1
```

Khi có nhiều Query Parameter, các tham số được phân tách bằng dấu `&`.

```text
https://api.example.com/users?page=1&limit=10
```

Trong Postman, Query Parameter có thể được nhập tại tab `Params`.

---

## 7. Headers và Authorization

### 7.1. Headers

Header chứa thông tin bổ sung của request hoặc response.

| Header | Chức năng |
| --- | --- |
| `Content-Type` | Cho biết định dạng dữ liệu gửi lên |
| `Accept` | Cho biết định dạng response mong muốn |
| `Authorization` | Chứa thông tin xác thực |
| `User-Agent` | Thông tin ứng dụng gửi request |
| `Cache-Control` | Điều khiển bộ nhớ đệm |

Khi gửi dữ liệu JSON, Header thường được sử dụng:

```http
Content-Type: application/json
```

Ví dụ:

| Key | Value |
| --- | --- |
| `Content-Type` | `application/json` |
| `Accept` | `application/json` |

![Cấu hình Headers](images/06-request-headers.png)

### 7.2. Authorization

Authorization được sử dụng để xác định người dùng có quyền truy cập API hay không.

Postman hỗ trợ nhiều phương thức xác thực:

- No Auth.
- API Key.
- Bearer Token.
- Basic Auth.
- Digest Auth.
- OAuth 1.0.
- OAuth 2.0.
- JWT Bearer.

#### Bearer Token

Bearer Token là phương thức phổ biến đối với REST API.

```http
Authorization: Bearer <access_token>
```

Trong Postman:

1. Chọn tab `Authorization`.
2. Chọn loại `Bearer Token`.
3. Nhập Access Token.
4. Gửi request.

Có thể sử dụng biến:

```text
{{access_token}}
```

![Sử dụng Bearer Token](images/07-bearer-token.png)

#### Basic Auth

Basic Auth sử dụng tên đăng nhập và mật khẩu. Không nên sử dụng Basic Auth trên kết nối HTTP không được mã hóa vì thông tin có thể bị đánh cắp.

---

## 8. Gửi dữ liệu với POST Request

`POST` Request thường được sử dụng để thêm dữ liệu mới vào hệ thống.

URL thực hành:

```text
https://jsonplaceholder.typicode.com/posts
```

### 8.1. Các bước thực hiện

1. Tạo request mới.
2. Chọn phương thức `POST`.
3. Nhập URL.
4. Chọn tab `Body`.
5. Chọn `raw`.
6. Chọn định dạng `JSON`.
7. Nhập dữ liệu.
8. Nhấn `Send`.

Dữ liệu gửi lên:

```json
{
  "title": "Học kiểm thử API với Postman",
  "body": "Đây là dữ liệu được gửi bằng POST Request",
  "userId": 1
}
```

Kết quả trả về:

```json
{
  "title": "Học kiểm thử API với Postman",
  "body": "Đây là dữ liệu được gửi bằng POST Request",
  "userId": 1,
  "id": 101
}
```

Mã trạng thái:

```http
201 Created
```

### 8.2. Kiểm tra dữ liệu không hợp lệ

Khi kiểm thử API, không chỉ kiểm tra trường hợp hợp lệ mà còn cần kiểm tra các trường hợp không hợp lệ:

- Thiếu trường bắt buộc.
- Truyền dữ liệu rỗng.
- Sai kiểu dữ liệu.
- Chuỗi quá dài.
- Giá trị âm.
- Email sai định dạng.
- Truyền ký tự đặc biệt.
- Truyền dữ liệu trùng lặp.

Ví dụ:

```json
{
  "title": "",
  "body": "",
  "userId": "abc"
}
```

Với API thực tế, server cần trả về mã lỗi phù hợp như:

```http
400 Bad Request
422 Unprocessable Entity
```

---

## 9. Upload file với form-data

Postman hỗ trợ tải tập tin lên server bằng định dạng `multipart/form-data`.

Khi chọn `form-data`, Postman tự động tạo Header `Content-Type` với boundary tương ứng. Vì vậy, người dùng thường không cần tự nhập thủ công Header này.

Các trường hợp cần kiểm thử:

- Upload tập tin hợp lệ.
- Upload tập tin không đúng định dạng.
- Upload tập tin vượt quá dung lượng cho phép.
- Không chọn tập tin.
- Upload nhiều tập tin cùng lúc.
- Tên tập tin có ký tự đặc biệt.
- Tập tin có nội dung nguy hiểm.
- Người dùng không có quyền upload.

---

## 10. Collections

Collection là tập hợp các request có liên quan đến một API hoặc một dự án. Thay vì để các request riêng lẻ, người dùng nên lưu chúng vào Collection để dễ quản lý, chia sẻ và chạy tự động.

### 10.1. Tạo Collection

Các bước thực hiện:

1. Chọn `New`.
2. Chọn `Collection`.
3. Nhập tên Collection.
4. Thêm mô tả.
5. Lưu Collection.

Tên Collection sử dụng trong bài:

```text
Postman API Testing
```

### 10.2. Tổ chức Collection bằng Folder

```text
Postman API Testing
├── Posts
│   ├── Get All Posts
│   ├── Get Post By ID
│   ├── Create Post
│   ├── Update Post
│   └── Delete Post
├── Users
│   ├── Get All Users
│   └── Get User By ID
└── Comments
    ├── Get All Comments
    └── Get Comments By Post
```

### 10.3. Lợi ích của Collection

- Quản lý request tập trung.
- Chia request theo chức năng.
- Dùng chung cấu hình Authorization.
- Dùng chung script.
- Dùng chung biến.
- Xuất Collection thành tập tin JSON.
- Chia sẻ Collection cho thành viên khác.
- Chạy toàn bộ request bằng Collection Runner.
- Chạy tự động bằng Newman.

---

## 11. Environments và Variables

Biến giúp tránh việc nhập lặp lại các giá trị như URL, token, ID hoặc thông tin đăng nhập.

### 11.1. Các loại biến trong Postman

- Global Variables.
- Collection Variables.
- Environment Variables.
- Local Variables.
- Data Variables.

### 11.2. Tạo Environment

Ví dụ Environment tên `Testing Environment`:

| Variable | Initial Value | Current Value |
| --- | --- | --- |
| `base_url` | `https://jsonplaceholder.typicode.com` | `https://jsonplaceholder.typicode.com` |
| `post_id` | `1` | `1` |
| `access_token` | `token_value` | `token_value` |

Sau khi tạo biến, URL có thể được viết:

```text
{{base_url}}/posts
{{base_url}}/posts/{{post_id}}
```

### 11.3. Lợi ích của Environment

Khi chuyển từ môi trường phát triển sang môi trường kiểm thử, chỉ cần thay đổi Environment thay vì sửa từng request.

| Môi trường | Base URL |
| --- | --- |
| Development | `http://localhost:5000/api` |
| Testing | `https://test-api.example.com/api` |
| Production | `https://api.example.com/api` |

Request vẫn được viết:

```text
{{base_url}}/users
```

### 11.4. Tạo biến bằng script

```javascript
const response = pm.response.json();

pm.environment.set("post_id", response.id);
```

Lấy giá trị biến:

```javascript
const postId = pm.environment.get("post_id");
console.log(postId);
```

Xóa biến:

```javascript
pm.environment.unset("post_id");
```

---

## 12. Viết Test Script tự động

Postman hỗ trợ viết test bằng JavaScript. Các đoạn test được viết trong phần Post-response hoặc Tests, tùy phiên bản giao diện.

### 12.1. Kiểm tra mã trạng thái

```javascript
pm.test("Status code là 200", function () {
    pm.response.to.have.status(200);
});
```

### 12.2. Kiểm tra thời gian phản hồi

```javascript
pm.test("Thời gian phản hồi dưới 1000 ms", function () {
    pm.expect(pm.response.responseTime).to.be.below(1000);
});
```

### 12.3. Kiểm tra Content-Type

```javascript
pm.test("Response trả về JSON", function () {
    pm.expect(pm.response.headers.get("Content-Type"))
        .to.include("application/json");
});
```

### 12.4. Kiểm tra dữ liệu response

```javascript
pm.test("Response có thuộc tính id", function () {
    const jsonData = pm.response.json();
    pm.expect(jsonData).to.have.property("id");
});
```

### 12.5. Kiểm tra giá trị cụ thể

```javascript
pm.test("ID bài viết bằng 1", function () {
    const jsonData = pm.response.json();
    pm.expect(jsonData.id).to.eql(1);
});
```

### 12.6. Kiểm tra kiểu dữ liệu

```javascript
pm.test("Title là chuỗi", function () {
    const jsonData = pm.response.json();
    pm.expect(jsonData.title).to.be.a("string");
});
```

### 12.7. Kiểm tra danh sách không rỗng

```javascript
pm.test("Danh sách bài viết không rỗng", function () {
    const jsonData = pm.response.json();

    pm.expect(jsonData).to.be.an("array");
    pm.expect(jsonData.length).to.be.above(0);
});
```

### 12.8. Kiểm tra nhiều điều kiện

```javascript
pm.test("Response bài viết hợp lệ", function () {
    const jsonData = pm.response.json();

    pm.expect(jsonData).to.have.property("id");
    pm.expect(jsonData).to.have.property("userId");
    pm.expect(jsonData).to.have.property("title");
    pm.expect(jsonData).to.have.property("body");

    pm.expect(jsonData.id).to.be.a("number");
    pm.expect(jsonData.title).to.be.a("string");
});
```

### 12.9. Lưu dữ liệu từ response

```javascript
pm.test("Lưu ID bài viết", function () {
    const jsonData = pm.response.json();

    pm.expect(jsonData).to.have.property("id");
    pm.environment.set("post_id", jsonData.id);
});
```

---

## 13. Chạy Collection Runner

Collection Runner cho phép chạy nhiều request liên tiếp theo thứ tự đã được cấu hình trong Collection.

### 13.1. Mục đích

- Chạy toàn bộ test case.
- Chạy lặp nhiều lần.
- Chọn Environment.
- Truyền dữ liệu từ CSV hoặc JSON.
- Kiểm tra số lượng test thành công và thất bại.
- Thực hiện regression testing.

### 13.2. Các bước thực hiện

1. Mở Collection.
2. Chọn chức năng `Run collection`.
3. Chọn các request cần chạy.
4. Chọn Environment.
5. Thiết lập số lần lặp.
6. Thiết lập khoảng thời gian giữa các request nếu cần.
7. Nhấn `Run`.
8. Quan sát kết quả.

Ví dụ cấu hình:

| Thiết lập | Giá trị |
| --- | --- |
| Iterations | `3` |
| Delay | `500 ms` |
| Environment | `Testing Environment` |

### 13.3. Kết quả Collection Runner

Kết quả hiển thị:

- Tổng số request.
- Tổng số test.
- Số test passed.
- Số test failed.
- Thời gian thực thi.
- Nội dung lỗi nếu có.

### 13.4. Data-Driven Testing

Collection Runner hỗ trợ đọc dữ liệu từ tập tin CSV hoặc JSON.

Ví dụ tập tin `data.csv`:

```csv
post_id,expected_status
1,200
2,200
999999,404
```

Sử dụng trong URL:

```text
{{base_url}}/posts/{{post_id}}
```

Kiểm tra mã trạng thái:

```javascript
pm.test("Kiểm tra status code theo dữ liệu", function () {
    const expectedStatus = Number(pm.iterationData.get("expected_status"));
    pm.response.to.have.status(expectedStatus);
});
```

Data-Driven Testing giúp chạy cùng một request với nhiều bộ dữ liệu khác nhau.

---

## 14. Newman

Newman là công cụ dòng lệnh dùng để chạy Postman Collection mà không cần mở giao diện Postman.

Newman phù hợp với:

- Chạy test tự động.
- Tích hợp CI/CD.
- Chạy test trên máy chủ.
- Xuất báo cáo kiểm thử.
- Chạy test sau mỗi lần cập nhật mã nguồn.

### 14.1. Cài đặt Node.js

```powershell
node --version
npm --version
```

### 14.2. Cài đặt Newman

```powershell
npm install -g newman
newman --version
```

### 14.3. Export Collection

Trong Postman:

1. Mở Collection.
2. Chọn biểu tượng ba chấm.
3. Chọn `Export`.
4. Chọn định dạng Collection.
5. Lưu tập tin JSON.

Ví dụ:

```text
Postman-API-Testing.postman_collection.json
Testing.postman_environment.json
```

### 14.4. Chạy bằng Newman

```powershell
newman run Postman-API-Testing.postman_collection.json
```

Chạy kèm Environment:

```powershell
newman run Postman-API-Testing.postman_collection.json -e Testing.postman_environment.json
```

### 14.5. Chạy nhiều vòng lặp

```powershell
newman run Postman-API-Testing.postman_collection.json -n 5
```

### 14.6. Chạy với tập tin dữ liệu

```powershell
newman run Postman-API-Testing.postman_collection.json -d data.csv
```

### 14.7. Xuất báo cáo

Xuất báo cáo JSON:

```powershell
newman run Postman-API-Testing.postman_collection.json -r cli,json
```

Cài reporter HTML:

```powershell
npm install -g newman-reporter-htmlextra
```

Chạy và xuất báo cáo HTML:

```powershell
newman run Postman-API-Testing.postman_collection.json -e Testing.postman_environment.json -r cli,htmlextra
```

### 14.8. Tích hợp CI/CD

Newman có thể tích hợp với:

- GitHub Actions.
- GitLab CI.
- Jenkins.
- Azure DevOps.
- CircleCI.

Ví dụ quy trình GitHub Actions:

```yaml
name: Postman API Tests

on:
  push:
    branches:
      - main
  pull_request:

jobs:
  api-test:
    runs-on: ubuntu-latest

    steps:
      - name: Checkout source code
        uses: actions/checkout@v4

      - name: Install Node.js
        uses: actions/setup-node@v4
        with:
          node-version: "20"

      - name: Install Newman
        run: npm install -g newman

      - name: Run Postman Collection
        run: |
          newman run postman/Postman-API-Testing.postman_collection.json \
          -e postman/Testing.postman_environment.json
```

Quy trình này sẽ tự động chạy API test khi có mã nguồn mới được đẩy lên GitHub.

---

## 15. Đọc và phân tích Response

Khi gửi request, người kiểm thử không chỉ xem nội dung dữ liệu mà cần phân tích toàn bộ response.

### 15.1. Status Code

| Mã | Tên | Ý nghĩa |
| --- | --- | --- |
| `200` | OK | Request thành công |
| `201` | Created | Tạo dữ liệu thành công |
| `204` | No Content | Thành công nhưng không có nội dung |
| `400` | Bad Request | Dữ liệu gửi lên không hợp lệ |
| `401` | Unauthorized | Chưa xác thực |
| `403` | Forbidden | Không có quyền truy cập |
| `404` | Not Found | Không tìm thấy tài nguyên |
| `409` | Conflict | Dữ liệu bị xung đột hoặc trùng lặp |
| `422` | Unprocessable Entity | Dữ liệu không vượt qua validation |
| `429` | Too Many Requests | Gửi quá nhiều request |
| `500` | Internal Server Error | Lỗi xử lý phía server |
| `502` | Bad Gateway | Gateway nhận phản hồi không hợp lệ |
| `503` | Service Unavailable | Dịch vụ tạm thời không khả dụng |

### 15.2. Response Body

Người kiểm thử cần kiểm tra:

- Response có đúng định dạng hay không.
- Có đầy đủ các trường bắt buộc hay không.
- Giá trị có đúng hay không.
- Kiểu dữ liệu có chính xác hay không.
- Có trả về dữ liệu nhạy cảm hay không.
- Thông báo lỗi có rõ ràng hay không.
- Dữ liệu có đúng với điều kiện tìm kiếm hay không.

### 15.3. Response Headers

Các Response Header cần chú ý:

- `Content-Type`
- `Content-Length`
- `Cache-Control`
- `Set-Cookie`
- `Access-Control-Allow-Origin`
- `Server`
- Security headers

Ví dụ:

```http
Content-Type: application/json; charset=utf-8
```

### 15.4. Response Time

Response Time thể hiện thời gian server xử lý request.

```text
Response Time: 250 ms
```

Một API có response đúng nhưng thời gian xử lý quá lâu vẫn có thể không đáp ứng yêu cầu chất lượng.

### 15.5. Response Size

Response Size cho biết dung lượng dữ liệu trả về. Response quá lớn có thể ảnh hưởng đến tốc độ mạng và trải nghiệm người dùng.

### 15.6. Cookies

Cookies thường được sử dụng để lưu:

- Session ID.
- Token xác thực.
- Trạng thái đăng nhập.
- Thông tin tùy chỉnh.

Người kiểm thử cần kiểm tra các thuộc tính bảo mật:

- `HttpOnly`
- `Secure`
- `SameSite`
- Thời gian hết hạn

---

## 16. Ứng dụng Postman trong thực tế

### 16.1. Kiểm thử chức năng đăng nhập

Kịch bản:

- Gửi email và mật khẩu hợp lệ.
- Kiểm tra mã trạng thái.
- Kiểm tra Access Token.
- Lưu token vào Environment.
- Sử dụng token cho các request tiếp theo.

Ví dụ script:

```javascript
pm.test("Đăng nhập thành công", function () {
    pm.response.to.have.status(200);

    const response = pm.response.json();

    pm.expect(response).to.have.property("accessToken");
    pm.environment.set("access_token", response.accessToken);
});
```

### 16.2. Kiểm thử phân quyền

Các trường hợp:

- Không có token.
- Token không hợp lệ.
- Token hết hạn.
- Người dùng thông thường truy cập API quản trị.
- Quản trị viên truy cập API quản trị.

Kết quả mong đợi:

```http
401 Unauthorized
403 Forbidden
```

### 16.3. Kiểm thử CRUD

CRUD gồm:

- Create: Tạo dữ liệu.
- Read: Đọc dữ liệu.
- Update: Cập nhật dữ liệu.
- Delete: Xóa dữ liệu.

Quy trình kiểm thử:

1. Tạo đối tượng mới.
2. Lưu ID.
3. Lấy đối tượng theo ID.
4. Cập nhật đối tượng.
5. Kiểm tra dữ liệu sau cập nhật.
6. Xóa đối tượng.
7. Kiểm tra đối tượng không còn tồn tại.

### 16.4. Kiểm thử Validation

Một số dữ liệu cần kiểm tra:

- Email không đúng định dạng.
- Mật khẩu quá ngắn.
- Thiếu trường bắt buộc.
- Số điện thoại chứa chữ.
- Ngày tháng không hợp lệ.
- Giá trị vượt quá giới hạn.
- Chuỗi chứa khoảng trắng.
- Trùng email hoặc tên người dùng.

### 16.5. Kiểm thử bảo mật cơ bản

Có thể dùng Postman để kiểm tra:

- API có yêu cầu đăng nhập hay không.
- Token hết hạn có bị từ chối hay không.
- Người dùng có truy cập dữ liệu của người khác hay không.
- Có thể thay đổi ID để lấy dữ liệu trái phép hay không.
- Server có làm lộ mật khẩu hay thông tin nhạy cảm không.
- API có giới hạn số lượng request không.
- Dữ liệu đầu vào có được kiểm tra không.

### 16.6. Kiểm thử luồng nghiệp vụ

Ví dụ luồng đặt hàng:

```text
Đăng nhập
→ Lấy danh sách sản phẩm
→ Thêm sản phẩm vào giỏ hàng
→ Tạo đơn hàng
→ Thanh toán
→ Kiểm tra trạng thái đơn hàng
```

Các request được liên kết bằng biến Environment và test script.

### 16.7. Tạo Mock Server

Postman hỗ trợ Mock Server để mô phỏng API khi backend chưa hoàn thành. Mock Server giúp frontend tiếp tục phát triển dựa trên response mẫu.

### 16.8. Tạo tài liệu API

Postman có thể tạo tài liệu từ Collection, bao gồm:

- URL.
- Method.
- Params.
- Headers.
- Request Body.
- Response mẫu.
- Mô tả request.

---

## 17. Best Practices và Checklist

### 17.1. Đặt tên request rõ ràng

Không nên viết:

```text
Request 1
Request 2
Test API
```

Nên viết:

```text
Get All Users
Get User By ID
Create New User
Update User Profile
Delete User
```

### 17.2. Tổ chức Collection theo chức năng

Nên chia request vào các folder:

- Authentication.
- Users.
- Products.
- Orders.
- Payments.
- Admin.

### 17.3. Sử dụng biến

Không nên ghi trực tiếp:

```text
https://api.example.com/api/users/15
```

Nên sử dụng:

```text
{{base_url}}/users/{{user_id}}
```

### 17.4. Không lưu thông tin bí mật trong Collection

Không nên đẩy các thông tin sau lên GitHub:

- Mật khẩu thật.
- Access Token thật.
- API Key.
- Secret Key.
- Thông tin tài khoản.
- Cookie đăng nhập.
- Chuỗi kết nối cơ sở dữ liệu.

Nên sử dụng biến môi trường và thay giá trị thật bằng dữ liệu mẫu trước khi export.

### 17.5. Mỗi request cần có test

Một request cơ bản nên kiểm tra:

- Status Code.
- Response Time.
- Content-Type.
- Cấu trúc Response.
- Dữ liệu bắt buộc.
- Kiểu dữ liệu.
- Giá trị nghiệp vụ.

### 17.6. Kiểm tra cả trường hợp thành công và thất bại

Cần kiểm tra:

- Thiếu dữ liệu.
- Sai dữ liệu.
- Không đăng nhập.
- Không có quyền.
- Tài nguyên không tồn tại.
- Dữ liệu trùng.
- Token hết hạn.
- Server xảy ra lỗi.

### 17.7. Viết mô tả cho Collection và Request

Mỗi request nên có mô tả gồm:

- Mục đích.
- Dữ liệu đầu vào.
- Điều kiện trước.
- Kết quả mong đợi.
- Các quyền cần thiết.

### 17.8. Sử dụng script ở đúng phạm vi

Script dùng chung nên đặt tại Collection hoặc Folder. Script riêng biệt nên đặt tại Request. Điều này giúp tránh lặp mã và dễ bảo trì.

### 17.9. Checklist kiểm thử API

#### Request

- [ ] Method chính xác.
- [ ] URL chính xác.
- [ ] Path Parameter chính xác.
- [ ] Query Parameter chính xác.
- [ ] Header đầy đủ.
- [ ] Authorization hợp lệ.
- [ ] Request Body đúng định dạng.
- [ ] Content-Type chính xác.

#### Response

- [ ] Status Code đúng.
- [ ] Response Body đúng.
- [ ] Kiểu dữ liệu đúng.
- [ ] Các trường bắt buộc tồn tại.
- [ ] Không có dữ liệu nhạy cảm.
- [ ] Response Time phù hợp.
- [ ] Thông báo lỗi rõ ràng.
- [ ] Response Header chính xác.

#### Security

- [ ] Không có token thì bị từ chối.
- [ ] Token sai thì bị từ chối.
- [ ] Token hết hạn thì bị từ chối.
- [ ] Người dùng không truy cập được dữ liệu trái phép.
- [ ] Không làm lộ mật khẩu.
- [ ] Có giới hạn số request.
- [ ] Dữ liệu đầu vào được kiểm tra.

#### Automation

- [ ] Request được lưu trong Collection.
- [ ] URL sử dụng biến.
- [ ] Test script được viết đầy đủ.
- [ ] Collection Runner chạy thành công.
- [ ] Newman chạy thành công.
- [ ] Không có thông tin bí mật trong file export.

---

## 18. Roadmap học Postman

### Giai đoạn 1: Kiến thức HTTP cơ bản

Tìm hiểu:

- Client và Server.
- Request và Response.
- URL.
- HTTP Methods.
- Status Code.
- Headers.
- Body.
- JSON.

### Giai đoạn 2: Thao tác Postman cơ bản

Thực hành:

- Gửi GET Request.
- Gửi POST Request.
- Gửi PUT và PATCH Request.
- Gửi DELETE Request.
- Sử dụng Params.
- Sử dụng Headers.
- Gửi dữ liệu JSON.
- Gửi form-data.

### Giai đoạn 3: Authentication

Tìm hiểu:

- API Key.
- Basic Auth.
- Bearer Token.
- JWT.
- OAuth 2.0.
- Cookie và Session.

### Giai đoạn 4: Quản lý Collection

Thực hành:

- Tạo Collection.
- Tạo Folder.
- Tạo Environment.
- Sử dụng Variables.
- Import và Export Collection.
- Chia sẻ Collection.

### Giai đoạn 5: Automation Testing

Học JavaScript cơ bản và Postman API:

- `pm.test()`
- `pm.expect()`
- `pm.response`
- `pm.environment`
- `pm.collectionVariables`
- Pre-request Script.
- Post-response Script.
- Data-Driven Testing.

### Giai đoạn 6: Collection Runner và Newman

Thực hành:

- Chạy Collection.
- Chạy nhiều vòng lặp.
- Đọc dữ liệu từ CSV.
- Đọc dữ liệu từ JSON.
- Chạy bằng Newman.
- Xuất báo cáo HTML.

### Giai đoạn 7: CI/CD

Tích hợp API test với:

- GitHub Actions.
- Jenkins.
- GitLab CI.
- Azure DevOps.

### Giai đoạn 8: Kiểm thử nâng cao

Tìm hiểu:

- Contract Testing.
- Schema Validation.
- Mock Server.
- API Documentation.
- Security Testing.
- Performance Testing cơ bản.
- Quản lý dữ liệu kiểm thử.

---

## 19. Kết luận

Qua quá trình tìm hiểu và thực hành, Postman là một công cụ hữu ích trong phát triển và kiểm thử API. Công cụ cho phép gửi request, quan sát response, kiểm tra status code, quản lý header, authorization và dữ liệu đầu vào một cách trực quan.

Bài thực hành đã thực hiện được các nội dung chính:

- Tìm hiểu khái niệm API và kiểm thử API.
- Làm quen với giao diện Postman.
- Gửi request bằng các phương thức HTTP.
- Sử dụng Query Parameter và Path Parameter.
- Cấu hình Header và Authorization.
- Gửi dữ liệu JSON bằng POST Request.
- Upload tập tin bằng form-data.
- Tổ chức request bằng Collection.
- Quản lý URL và dữ liệu bằng Environment Variables.
- Viết test script bằng JavaScript.
- Chạy nhiều request bằng Collection Runner.
- Chạy Collection trên dòng lệnh bằng Newman.
- Tìm hiểu khả năng tích hợp kiểm thử API vào CI/CD.

Postman giúp rút ngắn thời gian kiểm thử, phát hiện lỗi sớm và hỗ trợ các thành viên trong nhóm trao đổi thông tin API dễ dàng hơn. Khi kết hợp Postman Collection, test script, Environment và Newman, quy trình kiểm thử API có thể được tự động hóa và áp dụng trong các dự án phần mềm thực tế.

Bên cạnh việc sử dụng công cụ, người kiểm thử cần hiểu rõ HTTP, REST API, JSON, xác thực, phân quyền và các yêu cầu nghiệp vụ. Công cụ chỉ hỗ trợ thực hiện kiểm thử; chất lượng của quá trình kiểm thử phụ thuộc vào việc xây dựng các trường hợp kiểm thử đầy đủ và đánh giá chính xác kết quả trả về.

---

## 20. Tài liệu tham khảo

- Tài liệu chính thức của Postman.
- Tài liệu HTTP của MDN Web Docs.
- Tài liệu JSONPlaceholder.
- Video hướng dẫn Postman do giảng viên cung cấp.
- Các tài liệu về REST API và kiểm thử phần mềm.
- Tài liệu Newman Command Line Collection Runner.

---

## Phụ lục: Danh sách hình ảnh cần chụp

| STT | Nội dung hình ảnh | Tên file đề xuất |
| --- | --- | --- |
| 1 | Trang chủ Postman | `01-trang-chu-postman.png` |
| 2 | Giao diện chính Postman | `02-giao-dien-postman.png` |
| 3 | GET danh sách bài viết | `03-get-request.png` |
| 4 | GET bài viết theo ID | `04-get-post-by-id.png` |
| 5 | Query Parameters | `05-query-parameters.png` |
| 6 | Request Headers | `06-request-headers.png` |
| 7 | Bearer Token | `07-bearer-token.png` |
| 8 | POST Request | `08-post-request.png` |
| 9 | Upload file bằng form-data | `09-upload-file.png` |
| 10 | Postman Collection | `10-postman-collection.png` |
| 11 | Environment Variables | `11-environment-variables.png` |
| 12 | Test Script | `12-test-script.png` |
| 13 | Kết quả Test Script | `13-test-results.png` |
| 14 | Collection Runner | `14-collection-runner.png` |
| 15 | Kết quả Collection Runner | `15-runner-results.png` |
| 16 | Chạy Newman trên Terminal | `16-newman-cli.png` |
| 17 | Báo cáo Newman | `17-newman-report.png` |
| 18 | Phân tích Response | `18-response-analysis.png` |
