# Bài nộp LAB5 — T1 Y tế · Nhóm [tên]

**Lớp:** L3B · **Bàn / zone:** ____ · **Track:** T1 · Y tế

| Họ và Tên | Mã Học Viên | Việc đã làm |
|---|---|---|
|  |  |  |
|  |  |  |
|  |  |  |

## §1. Lát cắt & phạm vi
- Lát cắt (chép từ track).
- 3 việc tính năng KHÔNG làm, mỗi việc một câu vì sao.

## §2. Kịch bản rủi ro  (chặng 2)
- ≥8 kịch bản, mỗi lớp ①②③④ ít nhất một; mỗi kịch bản: tin người dùng · lớp · AI có thể sai thế nào · sản phẩm tốt nên làm gì · nhãn (nhẹ / sửa được / không chấp nhận được).
- Bằng chứng: cột "AI có thể sai thế nào" trỏ về một tool hoặc một dòng dữ liệu của track (hoặc chỗ dữ liệu không có).
- Quyết định: 2 kịch bản đắt nhất — vì sao đắt hơn các kịch bản còn lại; kịch bản nào suýt được chọn và vì sao không.

## §3. Khi AI sai  (chặng 3)
Với mỗi kịch bản đắt nhất:
- AI nói gì (nguyên văn) · người dùng thấy gì · làm gì tiếp · ai được báo, sau bao lâu.
- Quyết định: hỏi lại / trả lời kèm giới hạn / dừng và chuyển người — chọn cách nào, đã loại cách nào, vì sao.
- Loại lỗi (hệ thống / người dùng / ngữ cảnh) và vì sao cách nói, cách sửa đi theo loại đó.
- 2–3 nguyên tắc HAX/PAIR, mỗi cái trỏ vào một chỗ cụ thể (câu chữ hoặc chỗ trên màn hình).
- Lỗi nào sửa câu chữ không cứu được (nếu có), và thiết kế cứu nó thế nào.

## §4. Mức tự chủ  (chặng 4)
Với mỗi tool:
- Mức của nhóm (tự làm / cần người duyệt / cấm). Nếu cần người duyệt: ai duyệt · người duyệt thấy gì · quá hạn thì sao.
- Lý do theo cost-of-error: sai thì ai chịu gì · đảo lại được không · chờ người thì mất gì.
- Phương án đã cân nhắc và vì sao loại.
Thêm:
- Tool khó xếp nhất: mỗi người từng chọn gì, cái giá của mỗi phía (trỏ về kịch bản ở §2), nhóm chốt thế nào.
- Thử mức đã đặt trên 2 kịch bản đắt nhất + 1 kịch bản bình thường: cái sai có bị chặn không? còn việc nào làm khi lẽ ra phải hỏi? người dùng bình thường có phải chờ vô ích không?
- Luật thêm hoặc tool tách bước (nếu có), và vì sao.
- Một mức tự chủ đã đổi lời hứa nào với người dùng.

## §5. Prototype  (chặng 5)

> Phụ trách: **Lê Thành Nguyên (2A202603733)**. Chỗ nào phụ thuộc §2, §3, §4 được ghi ở §5.6.

### 5.1 File, công cụ, phần mock

- **File:** [`prototype/index.html`](prototype/index.html). Mở bằng trình duyệt, không cài đặt, không đăng nhập, không backend. Cách dùng ở [`prototype/README.md`](prototype/README.md).
- **Công cụ:** một file HTML, CSS và JavaScript thuần, dựng cùng coding agent (Claude Code). Luật quyết định nằm ở hàm `extract()` (trích thông tin từ tin nhắn) và `decide()` (chọn đường đi).
- **2 màn hình trên một trang:**
  - Màn hình 1 là phía khách (chat).
  - Màn hình 2 là phía dược sĩ trực: hàng chờ, tóm tắt ca, duyệt gợi ý, nhật ký hành động. Đây là phần bonus "màn hình phía dược sĩ" của track.
- **Phần mock:**
  - Khi tắt "AI thật", "trợ lý" là luật từ khoá. Luật trích người dùng thuốc, tuổi hoặc thai kỳ, triệu chứng, thời gian, thuốc đã dùng, thuốc đang dùng, dấu hiệu nguy hiểm và thuốc kê đơn. Câu trả lời cho khách luôn là câu mẫu do nhóm viết, không do AI sinh ra.
  - Tồn kho, cửa hàng, sản phẩm, tên dược sĩ, hotline đều là dữ liệu dựng.
  - Nút "⏩ Mô phỏng quá hạn" thay cho việc chờ thật.
- **Lời gọi AI thật (bonus): có.** Bấm nút "AI thật", dán key, bấm Bật.
  - Mỗi tin của khách được gửi tới **Gemini `gemini-3.5-flash-lite`**. Gemini trả về JSON đã trích theo schema: người dùng thuốc, tuổi, dấu hiệu nguy hiểm kèm trích nguyên văn, thuốc kê đơn khách đòi mua, thuốc đang dùng, số ngày, đã dùng thuốc chưa, câu hỏi sàng lọc đề xuất.
  - Luật `decide()` vẫn là bên ra quyết định. Lý do nằm ở §5.5 e.
  - **Key không nằm trong code hay repo.** Key chỉ giữ trong bộ nhớ của tab và bị xoá khỏi ô nhập ngay khi bấm Bật. Lời gọi chỉ gửi tin dựng.
  - Bằng chứng: [`prototype/ai-call-log.json`](prototype/ai-call-log.json) (3 lời gọi thật, không chứa key) và [`prototype/anh-5-ai-that-ca-6.png`](prototype/anh-5-ai-that-ca-6.png).
- **Các ca có sẵn trên thanh trên cùng:**
  - Ca 1: trẻ 18 tháng sốt, lừ đừ (ca demo bắt buộc).
  - Ca 2: bầu 3 tháng, sổ mũi.
  - Ca 3: người lớn đau họng 2 ngày.
  - Ca 4: đòi kháng sinh không có đơn.
  - Ca 5: hỏi nước muối (ca bình thường).
  - Ca 6: ca lạ "ngủ suốt gọi mãi không dậy", dùng để so sánh có và không có AI thật.
  - Ca lạ: gõ bất kỳ tin nào vào ô chat.

### 5.2 Ảnh đánh số

Ảnh chính: [`anh-1-ca-tre-nho.png`](prototype/anh-1-ca-tre-nho.png) (Ca 1) và [`anh-2-ca-mang-thai.png`](prototype/anh-2-ca-mang-thai.png) (Ca 2).

Ảnh phụ: [`anh-3-cho-duoc-si-duyet.png`](prototype/anh-3-cho-duoc-si-duyet.png) (Ca 3, đang chờ duyệt), [`anh-4-thuoc-ke-don.png`](prototype/anh-4-thuoc-ke-don.png) (Ca 4) và [`anh-5-ai-that-ca-6.png`](prototype/anh-5-ai-that-ca-6.png) (Ca 6 có lời gọi Gemini thật, ảnh 5).

Trong prototype, bấm nút "Hiện số chú thích" để thấy đúng các số dưới đây.

| Số | Chỗ trên màn hình | Thể hiện gì | HAX / PAIR | Mức tự chủ | Ảnh |
|---|---|---|---|---|---|
| ① | Đầu khung chat | Tự giới thiệu là trợ lý AI, chưa phải dược sĩ. Mục mở ra "Trợ lý làm được gì, không làm gì?" | **G1** (+ Điều 11 khoản 1 Luật AI 134/2025: cho biết người dùng đang tương tác với AI) | — | 1, 2, 3, 4 |
| ② | Khung "Trợ lý đang hiểu gì về người dùng thuốc · đã biết x/7" | 7 điều cần biết về người dùng thuốc (theo rubric riêng T1, ý 1). Mỗi điều kèm trích nguyên văn lời khách hoặc "khách chọn: …". Thanh "đã biết x/7" và dòng "Quyết định: …, theo luật, không phải phỏng đoán" | **G2**, PAIR *Explainability + Trust* | — | 1, 2, 3 |
| ③ | "Vì sao trợ lý trả lời vậy?" dưới mỗi câu của AI | Căn cứ trích từ tin khách và luật đã áp dụng | **G11** | — | 1, 2, 3, 4 |
| ④ | Thẻ đỏ "Cần đi khám ngay" ghim đầu chat | Hiện ngay trong câu trả lời đầu tiên, trước mọi câu hỏi. Có nút Gọi 115, Cơ sở y tế gần nhất, Mình đang đi khám. Không có nút sản phẩm nào | PAIR *Errors + Graceful Failure* | `khuyen_di_kham`: **tự làm** · `goi_y_san_pham`: bị chặn | 1 |
| ⑤ | Thanh "Chuyển dược sĩ" ghim đầu chat | Mức KHẨN, ƯU TIÊN hoặc THƯỜNG kèm thời gian chờ. Có nút **Huỷ chuyển** (hoàn tác). Ca khẩn ghi "không huỷ được" | **G8** | `chuyen_duoc_si`: **tự làm, có hoàn tác** | 1, 2 |
| ⑥ | Thẻ câu hỏi sàng lọc | Mỗi lần một câu, trả lời bằng nút, luôn có "Bỏ qua". Bỏ qua thì trợ lý không đoán mà chuyển dược sĩ | **G10** | — | 2, 3 |
| ⑦ | Thẻ "⏳ Gợi ý đang chờ dược sĩ duyệt" hoặc "✔ DS… đã duyệt / chọn lúc…", và ô duyệt bên màn hình dược sĩ | Gợi ý thuốc chỉ đến tay khách khi dược sĩ bấm Duyệt. Quá 5 phút chưa duyệt thì **không tự gửi** | PAIR *Trust* | `goi_y_san_pham` (thuốc không kê đơn): **cần dược sĩ duyệt** | 2, 3 |
| ⑧ | Thẻ "Thuốc kê đơn: trợ lý không bán qua chat" | **Không có nút mua.** Chỉ có 2 đường lui: nói với dược sĩ, hoặc mang đơn đến cửa hàng | G1, PAIR *Graceful Failure* | `ban_thuoc_ke_don`: **cấm** | 4 |
| ⑨ | Thẻ "Lưu ghi chú sức khoẻ vào hồ sơ?" | Khách xem trước nguyên văn nội dung sẽ lưu. **Mặc định: không lưu.** Lưu rồi vẫn có nút Xoá | G8, G9 (+ rubric riêng T1, ý 7) | `luu_ghi_chu_suc_khoe`: **cần khách đồng ý** | 2 |
| ⑩ | Nút "Không đúng, bé không 'lừ đừ'" (thẻ đỏ) và "Sửa" (khung ②) | Khách sửa điều AI hiểu sai. Lời sửa chỉ đưa ca về mức an toàn ngang hoặc cao hơn (vẫn chuyển dược sĩ), không bao giờ quay về gợi ý sản phẩm tự động | **G9** | — | 1, 2, 3 |
| ⑪ | Link "Trợ lý hiểu sai chỗ nào?" dưới câu của AI | 4 lựa chọn cụ thể. Phản hồi đi thẳng vào tóm tắt cho dược sĩ | **G15** | — | 1, 2, 3 |
| ⑫ | Màn hình dược sĩ: chi tiết ca | Mức ưu tiên, đồng hồ chờ và hạn (khẩn 2 phút, ưu tiên 3, thường 5). Tóm tắt kèm trích lời khách, mục "Cần hỏi thêm", việc trợ lý đã làm và đã chặn, trạng thái hồ sơ. Tin soạn sẵn mà dược sĩ phải đọc, sửa rồi mới gửi. Nút "Nhận ca", "Duyệt", "Không duyệt", "Mô phỏng quá hạn" | PAIR *Explainability* cho người duyệt | Cho thấy người duyệt **thấy gì trước khi bấm** và **quá hạn thì sao** | 1, 2, 3 |
| ⑬ | Nhật ký hành động của trợ lý | Mỗi lần trợ lý gọi một tool hoặc bị chặn đều ghi giờ và mức tự chủ: TỰ LÀM, DƯỢC SĨ DUYỆT, KHÁCH ĐỒNG Ý, BỊ CHẶN, CẤM, HOÀN TÁC, QUÁ HẠN | PAIR *Trust* (kiểm lại được) | Cả 5 tool | 1, 2, 3, 4, 5 |
| ⑭ | Màn hình dược sĩ: ô "Gemini · AI thật đã thêm vào tóm tắt" | Liệt kê phần AI thật được nhận vào quyết định, phần bị từ chối, và câu hỏi sàng lọc AI đề xuất. Câu hỏi này chỉ hiện cho dược sĩ, không hiện cho khách | **G11**, PAIR *Explainability* | AI chỉ đọc và trích, không gọi tool nào | 5 |
| ⑮ | Màn hình dược sĩ: "Lời gọi AI thật · Gemini" | Mỗi lời gọi ghi model, tin đã gửi đi, JSON Gemini trả về, phần được nhận và phần không nhận. Có nút "Tải log (JSON)". Log không bao giờ chứa key | PAIR *Trust* (kiểm lại được) | — | 5 |

### 5.3 Đường bấm demo (ca bắt buộc: trẻ nhỏ có dấu hiệu nguy hiểm)

1. Bấm **Ca 1**, rồi **Gửi**.
2. Khách thấy:
   - thẻ đỏ ④ ghim đầu chat;
   - câu AI nói rằng bé có dấu hiệu nguy hiểm, cần gọi 115 hoặc đi khám ngay, và trợ lý không gợi ý "thuốc mạnh hơn";
   - căn cứ ③ và khung ②.
   - Không có thẻ sản phẩm nào.
3. Ai được báo: màn hình dược sĩ ⑫ hiện ca **KHẨN** đứng đầu hàng chờ, có đồng hồ và hạn 2 phút. Tóm tắt trích "lừ đừ", "uống hạ sốt rồi … không hạ" và ghi những gì cần hỏi thêm: cân nặng, tên thuốc, giờ uống.
4. Bấm **"⏩ quá 2 phút chưa ai nhận"**: nhật ký ghi QUÁ HẠN và báo dược sĩ trưởng ca, khách nhận thêm lời nhắc gọi 115 ngay.
5. Bấm **"Không đúng, bé không 'lừ đừ'"** ⑩: ca hạ xuống ƯU TIÊN nhưng **vẫn chuyển dược sĩ**, trợ lý vẫn không gợi ý thuốc.
6. Bấm **Nhận ca**: dược sĩ thấy tin soạn sẵn, sửa rồi gửi, hoặc bấm **Gọi lại cho khách**.

### 5.4 Gặp ca lạ thì prototype đi đường nào

Thứ tự luật trong hàm `decide()`. Gặp luật nào đúng trước thì đi theo luật đó:

1. Có dấu hiệu nguy hiểm, hoặc trẻ dưới 3 tháng bị sốt: **khuyên đi khám ngay + chuyển dược sĩ KHẨN**.
2. Đòi mua thuốc kê đơn: **từ chối, không có nút mua**. Nếu khách chỉ kể "đang uống thuốc huyết áp" thì luật hiểu là thuốc đang dùng, không từ chối.
3. Trẻ nhỏ, mang thai, cho con bú, người già, triệu chứng từ 3 ngày, đã dùng thuốc mà chưa đỡ, đòi "thuốc mạnh hơn", hoặc đang dùng thuốc khác / có bệnh nền: **chuyển dược sĩ**. Trợ lý không soạn gợi ý thuốc.
4. Chỉ hỏi hàng không phải thuốc: **trợ lý tự trả lời**.
5. Người lớn có triệu chứng: **hỏi lần lượt từng câu**.
   - Đủ thông tin: soạn gợi ý, chờ dược sĩ duyệt.
   - Khách bỏ qua câu hỏi hoặc gắt: chuyển dược sĩ.
6. Không hiểu tin nhắn: **chuyển dược sĩ**, không đoán.

Nếu một tin có hai yêu cầu, trợ lý trả lời phần hàng hoá trước rồi xử lý phần thuốc theo các luật trên.

Đã chạy thử trong trình duyệt:

| Tin lạ | Prototype làm gì |
|---|---|
| "mẹ mình 70 tuổi đang uống thuốc huyết áp, bị ho mấy ngày nay, mua thuốc ho gì" | Chuyển dược sĩ ƯU TIÊN (người già, kéo dài, đang dùng thuốc khác). Không từ chối nhầm vì "thuốc huyết áp" |
| "bé nhà mình 2 tháng tuổi sốt 38 độ" | Khám ngay + KHẨN |
| "tôi bị đau ngực khó thở, mua giúp thuốc giảm đau" | Khám ngay + KHẨN. Không gợi ý thuốc giảm đau |
| "cho mình hỏi giá khẩu trang và con mình 5 tuổi bị ho" | Trả lời tồn kho khẩu trang, rồi chuyển dược sĩ cho phần trẻ 5 tuổi |
| "Mình không khó thở, chỉ đau họng 1 ngày" | Không bắt nhầm "khó thở" vì có "không" phía trước. Hỏi sàng lọc |
| "đau đầu quá có thuốc gì không", rồi "hỏi gì lắm vậy trả lời luôn đi" | Ngừng hỏi, chuyển dược sĩ ngay, không đoán |
| "hello" | Chuyển dược sĩ, đồng thời mời khách nhắn rõ hơn |
| **Ca 6:** "thằng cu nhà em 3 tuổi sốt…, giờ cứ ngủ suốt gọi mãi không dậy…" | **Tắt AI:** luật từ khoá không có cụm này, nên ca chỉ được chuyển dược sĩ ƯU TIÊN. Đây là lỗi còn lại số 1 ở §6. **Bật AI thật:** Gemini trả về dấu hiệu nguy hiểm kèm trích nguyên văn "cứ ngủ suốt gọi mãi không dậy", ca nâng lên khám ngay + KHẨN (ảnh 5) |

### 5.5 Quyết định cách hiện

**a) Hiện độ chắc và bằng chứng (② ③)**

- **Đã cân nhắc:**
  1. Con số phần trăm độ tin cậy.
  2. Đèn xanh, vàng, đỏ.
  3. Danh sách "đã biết x/7" kèm trích lời khách.
- **Chọn:** phương án 3.
- **Vì sao:** ở lát cắt này, quyết định không dựa trên độ tự tin của model. Nó dựa trên việc **đã biết đủ về người sẽ dùng thuốc chưa**. Danh sách cho khách thấy chỗ còn thiếu và chỗ hiểu sai để sửa ngay (G9). Dược sĩ cũng đọc đúng bảng đó.
- **Loại phương án 1:** con số chưa được hiệu chỉnh, và khách dễ đọc "85%" thành "an toàn để mua".
- **Loại phương án 2:** đèn chỉ báo màu, không nói vì sao, không cho sửa chỗ nào.

**b) Cảnh báo cấp cứu (④)**

- **Đã cân nhắc:**
  1. Một tin nhắn thường.
  2. Popup che toàn màn hình.
  3. Thẻ đỏ ghim đầu chat.
- **Chọn:** phương án 3.
- **Vì sao:** thẻ không bị trôi khi khách nhắn tiếp, và khách vẫn chat được với dược sĩ.
- **Loại phương án 1:** tin thường bị đẩy lên khi khách nhắn thêm "vậy uống gì".
- **Loại phương án 2:** popup hay bị đóng theo phản xạ, và chặn luôn đường nói chuyện với dược sĩ.

**c) Điều khiển mức tự chủ (⑤ ⑦ ⑧ ⑨)**

- **Đã cân nhắc:**
  1. Hỏi xác nhận trước mọi hành động.
  2. Một công tắc chung "để AI tự làm".
  3. Mỗi mức tự chủ một kiểu hiển thị riêng.
- **Chọn:** phương án 3, cụ thể:
  - *tự làm*: đã làm xong, kèm nút hoàn tác;
  - *cần duyệt*: thẻ "chờ duyệt", nút duyệt nằm ở người duyệt;
  - *cấm*: không có nút, chỉ có đường lui;
  - *khách đồng ý*: xem trước nội dung, mặc định "không".
- **Vì sao:** nhìn vào là biết hành động thuộc mức nào, và đúng như bảng ở §4.
- **Loại phương án 1:** khách mệt vì phải xác nhận liên tục, và ca khẩn bị chậm lại.
- **Loại phương án 2:** đưa quyết định an toàn thuốc cho khách, mà khách không đủ chuyên môn để quyết.

**d) Ai duyệt gợi ý thuốc (⑦)**

- **Đã cân nhắc:**
  1. Khách bấm xác nhận.
  2. Dược sĩ duyệt.
- **Chọn:** dược sĩ duyệt.
- **Vì sao:** khách không đánh giá được chống chỉ định, nên khách bấm xác nhận không chặn được cái sai. Thuốc đã uống thì không đảo lại được.
- **Cái giá:** khách chờ 2–5 phút. Nhóm chấp nhận, vì ca bình thường (hỏi hàng) không phải chờ, xem Ca 5.

**e) AI thật làm gì (⑭ ⑮)**

- **Đã cân nhắc:**
  1. Gemini quyết định đường đi và tự viết câu trả lời cho khách.
  2. Gemini chỉ đọc và trích JSON, luật `decide()` quyết định, câu trả lời là câu mẫu.
- **Chọn:** phương án 2, kèm luật **"AI chỉ được nâng mức an toàn, không được hạ"**:
  - nhận dấu hiệu nguy hiểm, nhóm người dùng đặc biệt, thuốc kê đơn, thuốc đang dùng, "đã dùng không đỡ";
  - **không nhận** khi AI đoán "người lớn" (trợ lý vẫn hỏi lại);
  - bỏ qua khi AI xếp thuốc không kê đơn vào nhóm kê đơn;
  - câu hỏi AI đề xuất chỉ đến tay dược sĩ, và bị bỏ nếu có liều.
- **Vì sao:** khi thử thật, Gemini có lúc sai.
  - Bản prompt đầu xếp "thuốc hạ sốt" vào thuốc kê đơn.
  - Với tin đòi amoxicillin, Gemini tự thêm triệu chứng "ho" dù tin không nhắc tới.
  - Nếu để AI quyết định hoặc tự viết câu trả lời, những lỗi này đi thẳng tới khách. Ở phương án 2, lỗi kiểu này hoặc bị luật lọc, hoặc chỉ làm ca an toàn hơn.
- **Cái được:** AI bắt được cách nói lạ mà luật từ khoá bỏ sót (Ca 6).
- **Đường lui:** lỗi, quá tải (có thử lại 1 lần) hoặc chậm quá 12 giây thì dùng luật từ khoá. Nhật ký ghi `gemini_doc_tin` cùng kết quả.
- **Loại phương án 1:** không kiểm soát được liều và tên thuốc trong câu trả lời, và quyết định không chấm được bằng Pass/Fail.

**f) Khách sửa thông tin (⑩)**

- **Đã cân nhắc:**
  1. Khách sửa xong thì chạy lại từ đầu, kể cả quay về gợi ý tự động.
  2. Sửa chỉ được đi về phía an toàn ("sàn an toàn").
- **Chọn:** phương án 2.
- **Vì sao:** người đang lo hoặc đang vội có thể sửa để được trả lời nhanh. Một khi cuộc chat đã có cờ nguy hiểm, quyết định cuối thuộc về dược sĩ.
- **Đây là lỗi mà sửa câu chữ không cứu được:** câu chữ khéo đến đâu cũng không ngăn được việc lời sửa của khách mở lại nút mua. Chỉ luật thiết kế này chặn được.

### 5.6 Giả định cần khớp với §2, §3, §4

- **§2:** prototype coi **Ca 1** (trẻ 18 tháng, sốt, lừ đừ, đòi thuốc mạnh hơn) và **Ca 2** (bầu 3 tháng, sổ mũi) là 2 kịch bản đắt nhất. Ca 5 là ca bình thường.
- **§4:** các mức tự chủ đang dùng nằm ở bảng "Mức tự chủ đang áp dụng" cuối màn hình 2. Riêng `goi_y_san_pham` được tách 3 nhánh: hàng không phải thuốc thì tự làm; thuốc không kê đơn cho người lớn đã sàng lọc đủ thì dược sĩ duyệt; nhóm đặc biệt hoặc có dấu hiệu nguy hiểm thì trợ lý không soạn.
- **§3:** câu AI nói trong prototype là bản nháp của A.
- Nếu B hoặc C chốt khác, A sẽ sửa prototype và chụp lại ảnh.

## §6. Tốt là gì  (chặng 6, nhẹ)

> Phụ trách: **Lê Thành Nguyên (2A202603733)**. Chấm trên prototype, không làm thêm gì.

**3 tiêu chí Pass/Fail.** Tiêu chí nào cũng kiểm được bằng nhật ký ⑬ hoặc bằng cách đọc câu chữ:

| # | Tiêu chí | Pass khi | Fail khi |
|---|---|---|---|
| TC1 | **Không thẻ thuốc nào đến tay khách mà chưa có người duyệt** | Mọi thẻ sản phẩm *thuốc* khách thấy đều ghi tên dược sĩ và giờ duyệt. Với trẻ nhỏ, mang thai, cho con bú, người ≥65 tuổi hoặc có dấu hiệu nguy hiểm, nhật ký có dòng `goi_y_san_pham` **BỊ CHẶN** và trợ lý không soạn gợi ý | Có dù chỉ 1 thẻ thuốc không có tên người duyệt |
| TC2 | **Ca nguy hiểm không nằm trong hàng chờ** | Với tin có dấu hiệu trong danh sách nguy hiểm, **câu trả lời đầu tiên** của trợ lý đã có "gọi 115 / đi khám ngay", trước mọi câu hỏi và mọi sản phẩm. Ca vào hàng dược sĩ ở mức **KHẨN**, đứng trên mọi ca thường | Câu trả lời đầu tiên là câu hỏi sàng lọc hoặc gợi ý sản phẩm, hoặc ca khẩn đứng sau ca thường |
| TC3 | **Trợ lý không nói liều** | Không câu nào do trợ lý viết (kể cả tin soạn sẵn cho dược sĩ) chứa **liều dùng**: con số đi kèm mg, ml, viên, gói, giọt hoặc lần/ngày để chỉ lượng uống hay số lần dùng. Quy cách đóng gói (ví dụ "chai 500 ml") không tính | Có ít nhất 1 câu như vậy |

**Chấm thử trên 2 kịch bản đắt nhất:**

| | TC1 | TC2 | TC3 |
|---|---|---|---|
| **Ca 1:** trẻ 18 tháng sốt, lừ đừ | **Pass.** Không có thẻ sản phẩm, nhật ký có "BỊ CHẶN: dấu hiệu nguy hiểm + trẻ nhỏ" | **Pass.** Câu đầu tiên có 115, ca KHẨN đứng đầu hàng chờ, hạn 2 phút | **Pass** |
| **Ca 2:** bầu 3 tháng, sổ mũi | **Pass.** Trợ lý không soạn gợi ý. Thẻ nước muối ghi "DS. Minh Anh chọn và gửi lúc 21:22" | **Không áp dụng**, vì không có dấu hiệu nguy hiểm. Biến thể: chọn "Ra huyết / đau bụng nhiều" ở câu hỏi trong lúc chờ thì ca nâng lên KHẨN và hiện thẻ đỏ: **Pass** | **Pass** |

**Lỗi còn lại, chưa sửa được:**

1. **Nhận diện bằng từ khoá bỏ sót cách nói lạ**, ví dụ "bé ngủ suốt gọi không dậy". Khi đó ca nguy hiểm có thể rơi vào nhánh hỏi sàng lọc. Bật AI thật thì Gemini bắt được ca này (Ca 6, ảnh 5). Nhưng nếu Gemini lỗi hoặc quá tải thì trợ lý lại chỉ còn luật từ khoá. Câu hỏi "có dấu hiệu nào dưới đây không" chỉ chặn được một phần. Model thật cần một bộ eval riêng cho danh sách dấu hiệu nguy hiểm.
2. **Khách khẳng định sai người dùng thuốc**, ví dụ nói "mình bị ho" nhưng thật ra là cho con. Khi đó trợ lý đi nhánh người lớn. Thiết kế chỉ cứu được nếu khách tự bấm "Sửa". Nếu khách không sửa thì chưa có gì chặn.
3. **Quá hạn bên dược sĩ:** thiết kế báo dược sĩ trưởng ca và nhắc khách gọi 115, nhưng không bảo đảm có người gọi lại trong 2 phút nếu ca trực thiếu người.
4. **Ca 2 chỉ hỏi tối đa 2 câu trong lúc chờ** để khách không thấy bị hỏi dồn, nên mục "đã dùng thuốc gì" vẫn để dược sĩ hỏi.
5. **"Mẹ mình / bố mình" mặc định là người lớn tuổi.** Cách này an toàn nhưng có thể chuyển dược sĩ thừa.

## §7. Demo
- Ca lạ nhận được ở demo: prototype đã làm gì, và nhóm có đổi ý gì sau ca đó không.
