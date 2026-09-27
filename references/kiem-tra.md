# Cửa kiểm

Chưa qua cửa thì chưa báo xong. Làm trên đúng cây vừa ghi.

## Cây

- `index.html` ở gốc, không chỉ ở thư mục con.
- Số file `chuong-NN.html` bằng N. Không thừa `chuong-25.html` nếu danh sách dừng ở 24.
- `style.css`, `app.js`, `search-index.json`, `README-HOST.txt` có mặt.
- Không file nào chứa `http://` hoặc `https://` trong `href`/`src` (chân trang và chữ trong thân được phép nhắc một tên miền nếu nguồn đã viết; liên kết thì không).

## Mở bằng file

Mở `index.html` bằng giao thức file, không qua máy chủ:

- Thấy tiêu đề sách và ít nhất một thẻ chương.
- Bấm một chương: mục lục đánh dấu đúng chương, thân không rỗng.
- Gõ hai chữ có trong một tiêu đề: ra đúng chương. Gõ một chữ: không hiện kết quả.
- Bấm «Nền»: nền đổi, tải lại vẫn giữ.
- Thu hẹp ~390 px: không thanh cuộn ngang; nút «Mục lục» mở được lớp phủ.
- Bảng mạng của trang: không request ra ngoài.

Nếu chỉ kiểm qua máy chủ tĩnh, ghi rõ chưa chứng minh `file://`. Hai chế độ không thay nhau: máy chủ không bắt lỗi `fetch` vì `fetch` cùng gốc sẽ thành công và giấu lỗi.

## Hai cây

Khi có `public/sach/`:

- Cùng tập tên file.
- Hash `index.html`, `chuong-01.html`, `style.css`, `app.js` hai phía khớp.
- Ứng dụng `/` trả chuyển hướng tới `/sach/index.html`, không phải một trang React có cùng chữ.

## Chữ

- Không số nào không có trong nguồn. Ô trống của nguồn vẫn là «chưa có», không thành 0.
- Không chương nào có `<script` trong thân.
- Tiêu đề trong mục lục khớp `h1`.

Hỏng một mục: sửa nguồn, sinh lại cả cây, kiểm lại. Không vá tay một HTML rồi bỏ qua hash.
