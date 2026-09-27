# Hợp đồng sáu nút

Không thêm nút. Không đảo mũi tên. Nút sau chỉ được đọc sản phẩm của nút trước.

## 1. Danh sách chương

Vào: văn người dùng đã chốt, hoặc file nguồn người dùng chỉ. Không phải trí nhớ của lượt trước nếu chưa được nhắc lại.

Ra: danh sách đã kiểm. Mỗi mục:

| Trường | Luật |
|---|---|
| `n` | số nguyên 1..N, không lỗ, không trùng |
| `title` | một dòng, không `<` `>` |
| `summary` | một câu, hiện trên thẻ trang chủ |
| `body` | HTML: `h2` `p` `ul` `ol` `table` `code` `strong` `em`. Cấm `script` `iframe` `object` `link` `img` ngoài thư mục |

Trang không đếm là chương, vẫn là file: `index.html`, `tong-quan.html`, và `kien-truc.html` / `moc-thoi-gian.html` chỉ khi nguồn có sơ đồ hoặc mốc.

Cấm: bịa chương, bịa số, đổi thứ tự người dùng đã khóa, gom hai chương vào một file.

## 2. Sinh HTML

Vào: danh sách đã kiểm + tên sách + `lang`.

Ra: một tập byte trong bộ nhớ, chưa ghi đĩa: mọi HTML, `style.css`, `app.js`, `search-index.json`, `README-HOST.txt`.

Một hàm trang. Chrome giống nhau. Khác nhau chỉ có tiêu đề cửa sổ, `class="on"`, và thân.

Cấm: sinh hai chrome, để JS dựng mục lục, để trang `fetch` chỉ mục.

## 3. Thư mục gốc

Vào: tập byte.

Ra: ghi đè cây phẳng tại đường người dùng chỉ. `index.html` nằm ở gốc đường đó.

Cấm: lồng `book-site/` bắt buộc. Cấm để bản HTML cũ của lần sinh trước nằm cạnh nếu tên không còn trong danh sách — xóa file `chuong-*.html` thừa trước khi ghi.

## 4. Mở index.html

Vào: thư mục gốc trên đĩa.

Ra: người đọc bấm đúp `index.html`. Không máy chủ. Mục lục, một chương, ô tìm đều chạy.

Cấm: bảo người đọc phải `npm install`. Cấm đường dẫn chỉ chạy trên máy sinh.

## 5. Bản xem trước

Chỉ khi người dùng cần khung xem trong app builder.

Vào: cùng tập byte của nút 2. Không sinh lần hai từ nguồn khác.

Ra: ghi đè `public/sach/` bằng đúng các file đó.

Cấm: bản xem trước là React dựng lại sách. Cấm sửa CSS một phía.

## 6. Khung xem

Vào: file tĩnh đã nằm ở `public/sach/index.html`.

Ra: route `/` của ứng dụng `beforeLoad` ném redirect `href: "/sach/index.html"`. Giữ cầu xem trước và auth provider của khung. Không thêm đăng nhập vì sách.

`startup.sh` vẫn khởi động lệnh dev đã có. Không đổi cổng.

Cấm: iframe một bản khác chữ. Cấm hash-router trong JSX song song với file chương.
