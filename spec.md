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
*(Người C phụ trách)*
Với mỗi tool:
- Mức của nhóm (tự làm / cần người duyệt / cấm). Nếu cần người duyệt: ai duyệt · người duyệt thấy gì · quá hạn thì sao.
- Lý do theo cost-of-error: sai thì ai chịu gì · đảo lại được không · chờ người thì mất gì.
- Phương án đã cân nhắc và vì sao loại.
Thêm:
- Tool khó xếp nhất: mỗi người từng chọn gì, cái giá của mỗi phía (trỏ về kịch bản ở §2), nhóm chốt thế nào.
- Thử mức đã đặt trên 2 kịch bản đắt nhất + 1 kịch bản bình thường: cái sai có bị chặn không? còn việc nào làm khi lẽ ra phải hỏi? người dùng bình thường có phải chờ vô ích không?
- Luật thêm hoặc tool tách bước (nếu có), và vì sao.
- Một mức tự chủ đã đổi lời hứa nào với người dùng.

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

