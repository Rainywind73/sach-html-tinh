# Mẫu trang

Mọi HTML cùng khung này. Thay `LANG`, `TITLE`, `NAV`, `MAIN`.

```html
<!doctype html>
<html lang="LANG">
<head>
<meta charset="utf-8">
<meta name="viewport" content="width=device-width, initial-scale=1">
<title>TITLE</title>
<link rel="stylesheet" href="style.css">
<script>try{if(localStorage.theme==='dark')document.documentElement.classList.add('dark')}catch(e){}</script>
</head>
<body>
<header class="top">
  <button class="menu" id="menu" type="button">Mục lục</button>
  <span class="brand">TÊN NGẮN</span>
  <input id="q" type="search" placeholder="Tìm trong sách" autocomplete="off">
  <button id="theme" type="button">Nền</button>
</header>
<div id="hits"></div>
<div class="layout">
<nav class="toc">NAV</nav>
<main>
MAIN
<footer>CHÂN — sách mở trực tiếp, không cần máy chủ.</footer>
</main>
</div>
<script>window.SEARCH_INDEX=INDEX_JSON;</script>
<script src="app.js" defer></script>
</body>
</html>
```

Script trong `head` chạy trước khi vẽ, để nền tối không nháy. Không đặt nó cuối trang.

## Mục lục

`NAV` là HTML tĩnh, sinh lúc ghi file:

- Dòng nhỏ «MỤC LỤC».
- Liên kết tương đối tới trang chủ, tổng quan, sơ đồ, mốc nếu các file đó tồn tại.
- Mỗi chương: `<a href="chuong-03.html">03. Tiêu đề đã escape</a>`.
- Đúng một `a` có `class="on"`: trang đang mở. Trang chủ không có `on` trên chương.

Không dựng danh sách này bằng `app.js`.

## Thân

Trang chủ: dòng dấu, `h1`, câu dẫn, lưới thẻ. Mỗi thẻ là `<a>` tới chương và câu tóm.

Chương: `h1` là «Chương NN. tiêu đề», đoạn `lead` là câu tóm, rồi `body` nguyên văn.

Tổng quan: một bảng số, tên, một câu.

## CSS — token, không hex rải

`:root` đủ sáu biến: nền, mực, nhấn, thẻ, kẻ, mực phụ, cộng nền mục lục và chữ mục lục. `html.dark` đổi cùng tên biến, không đổi selector của trang.

- Thân: serif hệ thống (`Palatino`, `Times New Roman`). Chrome: sans hệ thống. Không `@import` phông.
- `html { font-size: 18px }`, dòng 1.4–1.6.
- Lưới: `280px 1fr` từ 900px trở lên. Dưới 900px một cột; `nav.toc` thành lớp phủ khi `body.nav-open`.
- Nút mục lục `display` chỉ trên màn hẹp. Ô chạm tối thiểu 44px.
- `@media print`: giấu `.top`, `nav.toc`, `#hits`. `main` hết cỡ trang.
- Không ảnh nền, không bóng lớn, không gradient trang trí.

## Vì sao không một file

Một file thì in một chương kéo cả sách, và một chương hỏng cú pháp làm sập mục lục. Nhiều file thì mỗi chương là một tài liệu, liên kết là `href` trình duyệt hiểu khi mở `file://`.
