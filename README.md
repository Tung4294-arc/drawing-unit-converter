# Drawing Unit Converter

Công cụ web một trang (single-page) dành cho kiến trúc sư: chuyển đổi đơn vị
feet/inch sang mét hoặc milimét trên ảnh bản vẽ tay, đồng thời làm thẳng các
nét vẽ nguệch ngoạc.

Toàn bộ xử lý chạy trên **trình duyệt** — không cần backend, không cần cài đặt.

## Tính năng

- **Tải ảnh** bản vẽ định dạng PNG hoặc JPG và xem ảnh gốc.
- **Chuyển đổi đơn vị** tự động qua OCR (Tesseract.js):
  - Nhận dạng các dạng: `5'6"`, `5'-6"`, `10ft`, `24in`, `12"`.
  - Xuất ra **mét (m)** hoặc **milimét (mm)** — chọn bằng radio.
  - Vẽ text mới đè lên text cũ, kèm nền trắng để che chữ gốc.
- **Làm thẳng nét vẽ** bằng OpenCV.js (Hough Line Transform):
  - Tự phát hiện các đường gần thẳng và vẽ lại với độ dày đồng nhất.
  - Tự động căn thẳng ngang / dọc cho những đường lệch nhẹ.
- **Tải ảnh kết quả** dưới dạng PNG, giữ nguyên độ phân giải ảnh gốc.

## Cách dùng

1. Mở file `index.html` trực tiếp trong trình duyệt (Chrome / Edge / Firefox).
   - Hoặc phục vụ qua một web server tĩnh đơn giản (ví dụ:
     `python3 -m http.server`) rồi truy cập `http://localhost:8000`.
2. Bấm **Tải ảnh lên** và chọn ảnh bản vẽ PNG/JPG.
3. Chọn đơn vị xuất (**Mét** hoặc **Milimét**) và các bước xử lý mong muốn:
   - `Chuyển đổi đơn vị` — bật OCR và thay số trên ảnh.
   - `Làm thẳng nét vẽ` — bật phát hiện và vẽ lại đường thẳng.
4. Bấm **Xử lý**. Lần đầu chạy sẽ tải Tesseract.js và OpenCV.js từ CDN,
   vui lòng đợi vài giây.
5. Khi xong, bấm **Tải kết quả** để lưu ảnh PNG đầu ra.

## Thư viện sử dụng (qua CDN)

- [Tesseract.js 5](https://github.com/naptha/tesseract.js) — OCR trong trình duyệt.
- [OpenCV.js 4.9](https://docs.opencv.org/4.9.0/opencv.js) — xử lý ảnh + Hough Lines.

## Ghi chú

- Kết quả OCR phụ thuộc vào độ rõ của chữ viết tay; ảnh càng nét thì tỉ lệ
  nhận dạng đúng càng cao.
- Việc "làm thẳng nét vẽ" chỉ áp dụng cho các đường gần thẳng. Đường cong,
  nét chữ và ký hiệu sẽ được giữ nguyên.
- File `index.html` là self-contained — có thể copy đi nơi khác và mở trực tiếp.
