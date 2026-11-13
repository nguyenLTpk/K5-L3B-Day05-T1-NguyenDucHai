# Prototype: Trợ lý AI trả lời đầu tiên ở kênh "Hỏi dược sĩ" (T1)

## Mở prototype

Mở file [`index.html`](index.html) bằng trình duyệt (Chrome, Edge, Firefox). Không cần cài đặt, không đăng nhập, không có backend.

Trang có 2 màn hình:

- **Màn hình 1, khách:** khung chat với trợ lý AI.
- **Màn hình 2, dược sĩ trực:** hàng chờ, tóm tắt ca, nút duyệt gợi ý và nhật ký hành động của trợ lý.

Nút **"Hiện số chú thích"** bật các số ① đến ⑬. Các số này khớp với bảng trong `spec.md` §5.

## Các ca có sẵn

| Ca | Tin khách nhắn | Đường đi |
|---|---|---|
| **Ca 1** (ca demo bắt buộc) | "con mình 18 tháng sốt 39 độ…, uống hạ sốt rồi mà không hạ, giờ bé cứ lừ đừ, có thuốc gì mạnh hơn không" | Thẻ đỏ "Cần đi khám ngay" + chuyển dược sĩ KHẨN. Trợ lý không gợi ý sản phẩm |
| Ca 2 | "Mình đang bầu 3 tháng, bị cảm sổ mũi 2 hôm…" | Chuyển dược sĩ ƯU TIÊN, hỏi tối đa 2 câu trong lúc chờ. Dược sĩ tự chọn sản phẩm |
| Ca 3 | "Họng mình đau rát 2 ngày nay, có thuốc gì không?" | Hỏi lần lượt 3 câu, trợ lý soạn gợi ý, **dược sĩ duyệt** rồi mới gửi |
| Ca 4 | "bán mình 1 vỉ amoxicillin… khỏi cần đơn nha" | Thuốc kê đơn bị **cấm**: không có nút mua, chỉ có đường lui |
| Ca 5 (ca bình thường) | "…còn nước muối sinh lý không, tối nay mình qua lấy." | Trợ lý tự trả lời tồn kho, nút giữ hàng có hoàn tác |
| Ca 6 (ca lạ) | "thằng cu nhà em 3 tuổi sốt…, giờ cứ ngủ suốt gọi mãi không dậy…" | Chỉ có luật từ khoá: chuyển dược sĩ ƯU TIÊN, **bỏ sót** dấu hiệu nguy hiểm. Bật AI thật: Gemini bắt được dấu hiệu, ca nâng lên khám ngay + KHẨN |
| **Ca lạ** | Gõ bất kỳ tin nào vào ô chat | Đi theo luật ở `spec.md` §5.4 |

Các nút nên bấm thử khi demo:

- Ca 1: bấm **"Không đúng, bé không 'lừ đừ'"** để xem cách sửa chỉ đi về phía an toàn.
- Màn hình dược sĩ: bấm **"⏩ Mô phỏng: quá hạn"** để xem chuyện gì xảy ra khi không ai nhận ca hoặc không ai duyệt kịp.

## Ảnh đánh số

| Ảnh | Ca |
|---|---|
| [`anh-1-ca-tre-nho.png`](anh-1-ca-tre-nho.png) | Ca 1, trẻ nhỏ có dấu hiệu nguy hiểm *(ảnh chính 1)* |
| [`anh-2-ca-mang-thai.png`](anh-2-ca-mang-thai.png) | Ca 2, người mang thai *(ảnh chính 2)* |
| [`anh-3-cho-duoc-si-duyet.png`](anh-3-cho-duoc-si-duyet.png) | Ca 3, gợi ý đang chờ dược sĩ duyệt *(ảnh phụ)* |
| [`anh-4-thuoc-ke-don.png`](anh-4-thuoc-ke-don.png) | Ca 4, việc bị cấm *(ảnh phụ)* |
| [`anh-5-ai-that-ca-6.png`](anh-5-ai-that-ca-6.png) | Ca 6 có lời gọi Gemini thật *(bằng chứng bonus)* |

Để chụp lại đúng trạng thái trong ảnh, mở `index.html#case=1&play=1&annot=1&shot=1`. Thay `case=` bằng `2`, `3a` (chờ duyệt), `3` (đã duyệt), `4` hoặc `5`. Có thể thêm `say=` kèm một tin nhắn để chạy thử một ca lạ.

## Lời gọi AI thật (bonus)

Cách bật:

1. Bấm nút **"AI thật"** trên thanh trên cùng.
2. Dán Gemini API key vào ô nhập.
3. Bấm **Bật AI thật**, rồi gửi tin như bình thường.

Cách hoạt động:

- **Key không nằm trong code hay trong repo.** Key chỉ giữ trong bộ nhớ của tab, và bị xoá khỏi ô nhập ngay sau khi bấm Bật. Tải lại trang là mất key.
- **Gemini (`gemini-3.5-flash-lite`) chỉ đọc tin của khách và trả về JSON đã trích.** Quyết định vẫn do luật trong `decide()`.
- **AI chỉ được nâng mức an toàn**, ví dụ thêm một dấu hiệu nguy hiểm hoặc nhận ra người dùng thuốc là trẻ nhỏ. AI không bao giờ được hạ mức. Ví dụ: AI đoán "người lớn" thì trợ lý không nhận, vẫn hỏi lại.
- **Câu hỏi sàng lọc AI đề xuất chỉ hiện cho dược sĩ.** Nếu câu đó có liều thì bị bỏ.
- **Lỗi, quá tải (thử lại 1 lần) hoặc chậm quá 12 giây** thì trợ lý dùng luật từ khoá dự phòng.

Bằng chứng:

- [`ai-call-log.json`](ai-call-log.json): 3 lời gọi thật cho Ca 6, 3 và 4, không chứa key.
- [`anh-5-ai-that-ca-6.png`](anh-5-ai-that-ca-6.png): ảnh chụp, xem số ⑭ và ⑮.

Để chụp lại tự động, có thể truyền key qua `#key=…`. Trang sẽ xoá phần này khỏi thanh địa chỉ ngay khi đọc xong. Khi demo thì nên dùng ô nhập.

## Phần nào là mô phỏng

- **Mặc định không gọi AI.** Quyết định của "trợ lý" là **luật từ khoá** viết bằng JavaScript trong file, xem hàm `extract()` và `decide()`. Luật mô phỏng các quyết định ở `spec.md` §3 và §4. Chỉ khi bật "AI thật" thì Gemini mới tham gia vào bước đọc tin.
- Mọi cửa hàng, tồn kho, sản phẩm, tên dược sĩ, hotline và bệnh viện đều là **dữ liệu dựng**.
- Khi tắt AI thật, prototype không gửi dữ liệu đi đâu. Khi bật, prototype chỉ gửi tin nhắn dựng tới Gemini. Không dùng dữ liệu sức khoẻ thật.
- Prototype dùng để học, không liên kết với doanh nghiệp nào.
