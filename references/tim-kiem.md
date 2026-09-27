# Chỉ mục và tìm trên file://

`file://` coi mỗi file là một gốc khác. `fetch("search-index.json")` bị chặn. Vì vậy chỉ mục phải là dữ liệu trong chính trang, không phải request.

## Bản ghi

```json
{"chapter": 3, "title": "03. Tên", "text": "câu tóm cộng thân đã cắt thẻ", "url": "chuong-03.html"}
```

- `chapter` 0 cho trang không phải chương (chủ, tổng quan, sơ đồ, mốc).
- `text` tối đa khoảng 1.500 ký tự sau khi cắt thẻ và gộp khoảng trắng. Đủ để tìm câu, không nhét cả sách vào mỗi trang đến mức nặng.
- `url` tương đối, cùng thư mục. Không `./` bắt buộc, không `../`, không tuyệt đối.
- Cùng mảng ghi thêm `search-index.json` cho người host bằng máy chủ. Trang không đọc file đó.

Nhúng cuối `body`, trước script:

```html
<script>window.SEARCH_INDEX=[...];</script>
<script src="app.js" defer></script>
```

JSON phải `ensure_ascii` tùy ý nhưng hợp lệ: escape `<` trong chuỗi thành `\u003c` để một chương có chữ `<` không đóng nhầm thẻ script.

## app.js

Một IIFE. Không `import`, không `type="module"` — module thường không chạy từ `file://`.

Chuẩn hóa: `toLowerCase()`, `normalize("NFD")`, bỏ dấu `\u0300-\u036f`. «Dong» khớp «Đồng».

Khi gõ:

- Chờ 80 ms. Xóa hẹn giờ cũ.
- Dưới 2 ký tự sau chuẩn hóa: giấu `#hits`.
- Điểm: +6 nếu chuỗi nằm trong tiêu đề, +1 nếu nằm trong `text`. Cộng dồn nếu cả hai.
- Sắp giảm dần. Lấy 12.
- Mỗi dòng là `<a href="URL">TIÊU ĐỀ</a>`. Tiêu đề lấy từ chỉ mục đã sinh, không lấy từ ô gõ. Ô gõ không được thành HTML.
- Không thấy: một dòng chữ «Không thấy», không phải liên kết.

Nền: bấm `#theme` thì đảo class `dark` trên `documentElement`, ghi `localStorage.theme` là `"dark"` hoặc `""`. `localStorage` có thể ném trong chế độ chặn — nuốt lỗi.

Mục lục hẹp: `#menu` đảo `nav-open` trên `body`.

Bấm ra ngoài ô tìm và `#hits` thì giấu kết quả.

## Không làm trong app.js

- Không `fetch`, `XMLHttpRequest`, `Worker`.
- Không `innerHTML` từ `input.value`.
- Không lịch sử trình duyệt giả. Chuyển chương là `href` thường, để nút Back của trình duyệt đúng.
- Không lưu chương đang đọc lên mạng.
