# Bài nộp LAB5 — T1 · Y tế (Pharmacity) · Nhóm NguyenDucHai

## Thành viên nhóm

| Họ và Tên | Mã Học Viên | Việc đã làm |
|---|---|---|
| [Họ tên Người A] | [Mã HV] | Người A: Dựng prototype (§5), tiêu chí nghiệm thu (§6) |
| [Họ tên Người B] | [Mã HV] | Người B: Lát cắt & phạm vi (§1), UX khi AI sai (§3) |
| [Họ tên Người C] | [Mã HV] | Người C: Kịch bản rủi ro (§2), Mức tự chủ (§4), Demo (§7) |

---

## §1. Lát cắt & phạm vi
*(Người B phụ trách)*
- Lát cắt (chép từ track).
- 3 việc tính năng KHÔNG làm, mỗi việc một câu vì sao.

---

## §2. Kịch bản rủi ro  (chặng 2)
| Tin người dùng nhắn | Lớp | AI có thể sai thế nào | Một sản phẩm tốt nên làm gì | Nhãn |
| :--- | :---: | :--- | :--- | :---: |
| K1: Con mình sốt cao 39.5 độ từ chiều, có thuốc hạ sốt nào uống đỡ liền không shop? | ② Mơ hồ | Tin nhắn không nói tuổi và cân nặng của bé. AI tự tiện gọi tool goi_y_san_pham đưa Paracetamol 500mg dạng viên nén của người lớn kèm nút đặt mua ngay. | Nhận diện đối tượng là trẻ nhỏ, không tự ý gợi ý thuốc, hỏi nhanh tuổi và cân nặng, nếu sốt cao co giật chuyển khẩn cấp chuyen_duoc_si. | Không chấp nhận được |
| K2: Ba mình 65 tuổi, đang đau tức ngực trái lan lên cằm, vã mồ hôi, khó thở, có thuốc ngậm nào đỡ đau không? | ④ Domain | AI coi đây là cơn đau ngực thông thường, gọi tool goi_y_san_pham kẹo ngậm giảm đau hoặc gọi tool chuyen_duoc_si xếp vào hàng chờ chat thông thường phải đợi 5-10 phút. | Nhận diện dấu hiệu nhồi máu cơ tim, kích hoạt ngay tool khuyen_di_kham dạng banner đỏ hướng dẫn gọi cấp cứu 115 ngay, không bán thuốc và không bắt xếp hàng chờ. | Không chấp nhận được |
| K3: Pharmacity gần mình còn nước muối sinh lý Physiodose không, tối nay mình qua lấy. | ① Sự thật | Tồn kho chi nhánh chưa cập nhật thời gian thực. AI tự bịa còn rất nhiều hàng tại chi nhánh gần bạn khiến khách đến nơi lúc đêm muộn thì hết hàng. | Tra cứu tồn kho có mốc thời gian cụ thể, nếu dữ liệu cũ hơn 1 tiếng thì trả lời kèm giới hạn khuyên khách gọi hotline nhà thuốc trước khi qua. | Sửa được |
| K4: Mình đang bầu 3 tháng, bị cảm sổ mũi 2 hôm, có thuốc nào uống an toàn không ảnh hưởng em bé không ạ? | ② Mơ hồ | Khách mang thai 3 tháng đầu. AI gọi tool goi_y_san_pham các thuốc cảm OTC chứa tá dược co mạch chống chỉ định thai kỳ. | Nhận diện phụ nữ có thai, cấm tự ý gợi ý thuốc, kích hoạt tool chuyen_duoc_si kèm tóm tắt khách mang thai 3 tháng bị cảm sổ mũi 2 ngày. | Không chấp nhận được |
| K5: Bán cho tôi 2 vỉ Augmentin 1g với 1 vỉ Panadol Extra giao gấp về Cầu Giấy | ③ Thẩm quyền | Augmentin là kháng sinh kê đơn bắt buộc có đơn bác sĩ. AI gọi tool ban_thuoc_ke_don hoặc goi_y_san_pham tạo đơn giao hàng tự động. | Nhận diện thuốc kê đơn, từ chối bán qua chat tự động theo Luật Dược, yêu cầu khách tải ảnh chụp đơn thuốc có chữ ký bác sĩ để dược sĩ duyệt. | Không chấp nhận được |
| K6: Tôi bị ho rát họng 3 tuần nay uống đủ thứ siro không đỡ, có loại kháng sinh nào mạnh hơn không? | ④ Domain | Triệu chứng ho kéo dài trên 3 tuần cảnh báo bệnh lý hô hấp nặng. AI cố làm hài lòng khách bằng cách gợi ý đổi sang siro ho khác hoặc hứa hẹn thuốc mạnh hơn. | Phát hiện triệu chứng kéo dài bất thường, từ chối gợi ý thuốc tự điều trị, kích hoạt tool khuyen_di_kham chuyên khoa hô hấp và chuyển dược sĩ. | Sửa được |
| K7: Lưu lại tiền sử dị ứng Penicillin và bệnh tim của tôi vào tài khoản để lần sau tự trừ thuốc dị ứng nhé | ③ Thẩm quyền | AI tự động gọi tool luu_ghi_chu_suc_khoe vào hồ sơ khách hàng mà không có bước xác thực danh tính hay xin chấp thuận quyền riêng tư dữ liệu y tế. | Hiển thị thông báo chính sách quyền riêng tư dữ liệu sức khỏe, yêu cầu khách bấm xác nhận đồng ý trước khi lưu. | Nhẹ |
| K8: Gợi ý cho tôi thuốc trị đau dạ dày dạng gói chữ P uống trước ăn hay sau ăn | ① Sự thật | AI nhầm lẫn cơ chế tác dụng của thuốc Phosphalugel lại hướng dẫn uống trước ăn lúc đói làm giảm hiệu quả trung hòa acid. | Trích xuất chính xác hướng dẫn từ Dược thư hoặc tờ hướng dẫn sử dụng chính thức của nhà sản xuất, khuyên đọc kỹ HDSD và hỏi dược sĩ. | Sửa được |

- Kịch bản đắt nhất 1: K2 (đau tức ngực, khó thở ở người già) đắt nhất vì đây là ca cấp cứu đe dọa tính mạng tính bằng phút, nếu AI chậm trễ hoặc gợi ý sai sẽ lỡ thời gian vàng dẫn tới tử vong không thể đảo ngược.
- Kịch bản đắt nhất 2: K1 (trẻ nhỏ sốt cao) đắt thứ hai vì dùng sai liều paracetamol ở trẻ nhỏ gây suy gan cấp tính, thuốc đã uống vào dạ dày thì không thể thu hồi.
- Kịch bản suýt được chọn: K5 (đòi mua kháng sinh Augmentin không đơn) suýt được chọn nhưng loại vì cổng thanh toán và phần mềm kho vận đã có tầng chặn cứng bắt buộc tải đơn thuốc mới tạo được đơn giao hàng.

---

## §3. Khi AI sai  (chặng 3)
*(Người B phụ trách)*
Với mỗi kịch bản đắt nhất:
- AI nói gì (nguyên văn) · người dùng thấy gì · làm gì tiếp · ai được báo, sau bao lâu.
- Quyết định: hỏi lại / trả lời kèm giới hạn / dừng và chuyển người — chọn cách nào, đã loại cách nào, vì sao.
- Loại lỗi (hệ thống / người dùng / ngữ cảnh) và vì sao cách nói, cách sửa đi theo loại đó.
- 2–3 nguyên tắc HAX/PAIR, mỗi cái trỏ vào một chỗ cụ thể (câu chữ hoặc chỗ trên màn hình).
- Lỗi nào sửa câu chữ không cứu được (nếu có), và thiết kế cứu nó thế nào.

---

## §4. Mức tự chủ  (chặng 4)
Với mỗi tool:

- khuyen_di_kham:
  + Mức: tự làm.
  + Lý do theo cost-of-error: Báo nhầm chỉ làm khách tốn công tắt thông báo (đảo được ngay), nhưng chờ người duyệt thì khách lỡ thời gian vàng cấp cứu dẫn đến tử vong (không đảo được).
  + Phương án đã cân nhắc: Cần dược sĩ duyệt; loại vì đêm muộn không ai duyệt kịp khiến khách chết trong hàng chờ.

- chuyen_duoc_si:
  + Mức: tự làm.
  + Lý do theo cost-of-error: Chuyển nhầm ca nhẹ thì dược sĩ chỉ mất 1 phút đọc lướt (rất rẻ), nhưng không chuyển ca khó như trẻ em hoặc bà bầu thì khách dùng sai thuốc nguy hiểm tính mạng (rất đắt).
  + Phương án đã cân nhắc: Cần khách bấm duyệt; loại vì khách đang đau đớn hoảng loạn có thể bỏ qua nút bấm khiến ca khó bị kẹt lại với AI.

- luu_ghi_chu_suc_khoe:
  + Mức: cần người duyệt. Khách hàng duyệt; khách thấy tóm tắt thông tin sức khỏe sẽ lưu kèm ô xác nhận đồng ý; nếu quá hạn hoặc khách không bấm thì hủy bỏ, không lưu.
  + Lý do theo cost-of-error: Dữ liệu y tế lộ lọt là vi phạm pháp luật và không rút lại được; bắt khách xác nhận chỉ mất vài giây và không ảnh hưởng tính mạng.
  + Phương án đã cân nhắc: Tự làm; loại vì vi phạm luật bảo vệ dữ liệu cá nhân.

- ban_thuoc_ke_don:
  + Mức: cấm.
  + Lý do theo cost-of-error: Bán thuốc kê đơn không đơn là vi phạm pháp luật hình sự, gây ngộ độc và biến chứng nguy hiểm không thể thu hồi.
  + Phương án đã cân nhắc: Cần dược sĩ duyệt trên chat; loại vì quy trình bán thuốc kê đơn bắt buộc thẩm định qua cổng chuyên dụng, chatbot không có thẩm quyền xử lý.

- goi_y_san_pham:
  + Mức: cần người duyệt. Dược sĩ trực online duyệt; dược sĩ thấy tin nhắn của khách, tóm tắt triệu chứng, thẻ sản phẩm AI đề xuất kèm liều lượng và cảnh báo; nếu quá hạn sau 3 phút thì chuyển hẳn cuộc chat sang dược sĩ gọi lại, không tự tiện hiện nút đặt hàng cho khách.
  + Lý do theo cost-of-error: Khách không có chuyên môn y tế, nếu để AI tự gợi ý lung tung thì khách tin tưởng bấm mua ngay trong đêm, uống vào người là không đảo lại được; bắt dược sĩ duyệt chỉ tốn 1-2 phút nhưng chặn đứng nguy cơ mua nhầm và ngộ độc thuốc.
  + Phương án đã cân nhắc:
    * Tự làm: Loại vì AI gợi ý lung tung khách tự bấm mua đêm uống vào nguy hiểm tính mạng (như ca K1 trẻ nhỏ, K4 bà bầu).
    * Khách hàng tự duyệt: Loại vì khách không có kiến thức y khoa, không thể tự thẩm định đơn thuốc.

Thêm:

- Tool khó xếp nhất: goi_y_san_pham.
  + Ý kiến muốn tự làm: Để khách mua hàng nhanh lúc đêm muộn, không bắt khách chờ. Cái giá: AI gợi ý lung tung, khách bấm mua uống phải thuốc chống chỉ định (như ca K1 trẻ nhỏ uống paracetamol người lớn gây suy gan) là không thu hồi được.
  + Ý kiến muốn cấm: Cấm AI gợi ý mọi sản phẩm để an toàn tuyệt đối. Cái giá: Chatbot thành vô dụng, khách cần mua đồ cơ bản như nước muối sinh lý (ca K3) hay bông băng cũng bị chặn khiến khách bỏ đi.
  + Nhóm chốt: Đặt mức cần người duyệt (dược sĩ duyệt thẻ gợi ý trước khi hiển thị nút đặt hàng cho khách); riêng vật tư y tế không phải thuốc thì cho phép hiển thị kèm khuyến cáo.
- Thử mức đã đặt trên 2 kịch bản đắt nhất + 1 kịch bản bình thường:
  + K2 (đau ngực cấp cứu): Cái sai bị chặn hoàn toàn vì khuyen_di_kham tự làm hiện banner 115 ngay; AI không làm việc lẽ ra phải hỏi; khách không phải chờ đợi.
  + K1 (trẻ nhỏ sốt cao): Cái sai bị chặn vì goi_y_san_pham bắt buộc dược sĩ duyệt và chuyen_duoc_si tự kích hoạt chuyển dược sĩ ngay, không để khách mua lung tung; AI chỉ hỏi nhanh tuổi và cân nặng; khách phải chờ dược sĩ nhưng thời gian này là cần thiết cho an toàn.
  + K3 (nước muối sinh lý): Cái sai bị chặn nhờ timestamp tồn kho; đây là vật tư y tế thông thường nên được duyệt hiển thị nhanh; người bình thường không phải chờ vô ích.
- Luật thêm hoặc tool tách bước: Thêm luật bắt buộc dược sĩ duyệt thẻ gợi ý thuốc trước khi hiện nút đặt mua; cấm hiển thị nút đặt mua thuốc với trẻ dưới 6 tuổi và phụ nữ có thai.
- Một mức tự chủ đã đổi lời hứa nào với người dùng: Đổi lời hứa từ "AI tự chẩn đoán và bán thuốc tức thì" thành "AI tiếp đón, sàng lọc sơ bộ và có dược sĩ kiểm soát an toàn trước khi đưa thuốc cho bạn".

---

## §5. Prototype  (chặng 5)
*(Người A phụ trách)*
- Link hoặc file · công cụ · phần nào mock · có lời gọi AI thật không.
- 1–2 ảnh có đánh số; mỗi số: thể hiện gì · nguyên tắc HAX/PAIR nào · mức tự chủ nào.
- Quyết định: cách hiện độ chắc/bằng chứng và điều khiển mức tự chủ — đã nghĩ tới cách nào khác, vì sao chọn cách này.

---

## §6. Tốt là gì  (chặng 6 — nhẹ, bỏ được nếu thiếu giờ)
*(Người A phụ trách)*
- 3 tiêu chí Pass/Fail chấm được; thiết kế của nhóm đạt tiêu chí nào trên 2 kịch bản đắt nhất; lỗi còn lại.

---

## §7. Demo
*(Người C phụ trách phân chia lượt & tổng hợp)*
- Ca lạ nhận được ở demo: prototype đã làm gì, và nhóm có đổi ý gì sau ca đó không.

