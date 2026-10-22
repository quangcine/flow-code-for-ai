# 01 · Tư duy nền

Tệp này nêu các nguyên lý mà mọi mảnh ở [02_ThanhPhan.md](02_ThanhPhan.md) dựa vào.
Mỗi nguyên lý một khối: **vấn đề** (chuyện xảy ra khi thiếu nó) → **nguyên lý** → **vì sao**.
Hiểu nguyên lý thì bạn tự dựng được mảnh phù hợp với người dùng, kể cả khi mảnh đó trông khác hẳn bản mẫu.

## 1. Tách người nghĩ và người giao việc

**Vấn đề.** Một phiên vừa khảo sát, vừa thiết kế, vừa code, vừa soát kết quả thì ngữ cảnh đầy rất nhanh.
Tới lúc cần soát kết quả hay trả lời một câu hỏi chặn đường, phiên ấy đã quá tải hoặc vừa bị nén ngữ cảnh, mất bức tranh chung.

**Nguyên lý.** Chia hai vai.
- **Planner** (có thể nhiều phiên): khảo sát, hỏi người dùng, viết ý tưởng và kế hoạch. ⛔ Không code, ⛔ không giao việc.
- **Leader** (đúng một phiên): cầm kế hoạch đã chắc, giao cho subagent thi công, soát kết quả, đóng việc.
  Leader tự code chỉ khi người dùng nói rõ.

**Vì sao.** Leader giữ bản đồ của cả nhóm; giữ tay Leader rảnh thì lúc cần soát, chặn hai người sửa cùng tệp, Leader vẫn còn sức.
Nhiều Planner chạy song song vì việc nghĩ ⛔ không đụng tệp code của nhau.

## 2. Chốt ⛔ không phải là lệnh giao

**Vấn đề.** Người dùng vừa đồng ý một hướng, phiên Claude hăng hái đi làm ngay.
Bước thi công chỉ nằm trong một tin nhắn dài, ⛔ không ai rà, ⛔ không có tiêu chí nghiệm thu; người dùng phải chặn lại giữa chừng.

**Nguyên lý.** Chốt xong thì đi đủ ba bước: ghi chốt vào kế hoạch thành bước cụ thể (thứ tự, tiêu chí xong, đường lùi, danh sách tệp)
→ rà kế hoạch tới khi sạch → chờ người dùng bảo giao.

**Vì sao.** Một quyết định đúng vẫn có thể thi công sai. Kế hoạch viết ra rồi rà mới bắt được bước thiếu, con số sai, hai mục chỏi nhau.

## 3. Tài liệu là bộ nhớ chung giữa các phiên

**Vấn đề.** Mỗi phiên Claude bắt đầu trắng. Điều đã bàn ở phiên trước, lý do chọn hướng này, việc làm dở: mất hết khi phiên đóng hay nén ngữ cảnh.

**Nguyên lý.** Mọi thứ cần sống qua phiên đều ghi ra tệp: ý tưởng, kế hoạch, nhật ký thi công, tệp nợ việc dở.
Phiên mới đọc tệp, ⛔ không dựa vào trí nhớ hay bản tóm tắt.

**Vì sao.** Phiên quên, tệp ⛔ không quên. Bản tóm tắt sau nén ngữ cảnh là bản rút gọn của chính mô hình, dễ rơi chi tiết then chốt.

## 4. Trạng thái nằm ở dòng mục lục, tệp đứng yên

**Vấn đề.** Dời tệp kế hoạch qua lại giữa các thư mục "nháp", "đã duyệt", "xong" làm gãy mọi link trỏ tới nó,
và hai phiên dời cùng lúc thì lạc tệp.

**Nguyên lý.** Tệp nằm yên một chỗ. Trạng thái là **dòng** trong vài tệp mục lục (nháp, đã qua rà, xong, huỷ, hoãn).
Đổi trạng thái là chuyển dòng, kèm một cột cho biết ai đang cầm việc đó.

**Vì sao.** Link ⛔ không gãy, và chỉ cần đọc một tệp mục lục là biết việc nào đang có người nhận, tránh hai phiên làm trùng.

## 5. Ngữ cảnh là tài nguyên có hạn

**Vấn đề.** Mỗi lượt gọi công cụ, mô hình đọc lại toàn bộ ngữ cảnh. Ngữ cảnh phình thì mỗi lượt đắt hơn, chậm hơn,
và tới ngưỡng thì bị nén, mất chi tiết.

**Nguyên lý.**
- Đặt một ngưỡng (vd vài trăm nghìn token); chạm ngưỡng thì ⛔ không nhận việc mới, xong việc dở rồi bàn giao.
- Đọc theo khoảng dòng, ⛔ không đọc trọn tệp lớn; lệnh in dài thì lọc.
- Giao subagent đúng phần nó cần đọc, ⛔ không giao đọc trọn kế hoạch.
- Luật nạp mỗi phiên giữ ngắn; lý do và ca thật để tệp riêng, đọc khi cần.

**Vì sao.** Phần lớn chi phí của subagent là đọc lại ngữ cảnh chứ ⛔ không phải viết ra; cắt phần đọc thừa là cắt thẳng vào chi phí.

## 6. Đo trước khi kết luận

**Vấn đề.** Báo cáo ghi "đã xong", "hành vi giữ nguyên", "cửa kiểm xanh". Người nhận chuyển tiếp nguyên văn cho người dùng,
rồi lỗi lộ ra ở dùng thật.

**Nguyên lý.**
- Mỗi con số trong kế hoạch, báo cáo đều phải đo được bằng lệnh; ghi lệnh kèm kết quả.
- Người nhận báo cáo kiểm lại vài số then chốt bằng **cơ chế khác** (họ đếm bằng log thì mình đếm bằng tệp).
- Chỗ nào báo cáo khẳng định mà ⛔ không kèm phép đo thì mở mã ra xem.

**Vì sao.** Một con số sai đều ở mọi chỗ thì ⛔ không mâu thuẫn với gì cả; đọc bao lần cũng ⛔ không thấy, chỉ lộ khi đo.

## 7. Ranh giới tự quyết và phải hỏi

**Vấn đề.** Claude tự quyết hộ người dùng những chuyện họ chưa từng đồng ý; hoặc ngược lại, hỏi mọi thứ vụn vặt làm người dùng mệt.

**Nguyên lý.** Vẽ ranh giới rõ, ghi vào luật.
- Tự quyết: thứ tự làm, chia đợt, cách đo, câu chữ, nhắc luật.
- Phải hỏi: đổi thiết kế đã chốt, nới hay cắt phạm vi, đụng hạ tầng cloud, mọi thứ chạm tới người dùng thật hay dữ liệu thật.
- Mơ hồ, có hai cách hiểu thì hỏi.

**Vì sao.** Mọi quyết định bám kế hoạch đã duyệt; ngoài kế hoạch là vùng của người dùng.

## 8. Luật nạp theo việc

**Vấn đề.** Gom mọi luật vào một tệp nạp mỗi phiên thì tệp phình, mỗi lượt trả giá đọc lại, và luật quan trọng chìm giữa luật vụn.

**Nguyên lý.** Tách hai tầng.
- Tầng nạp mỗi phiên: vài chục dòng luật luôn đúng, cộng một bảng **"làm việc gì thì đọc gì"**.
- Tầng chi tiết: lý do, ca thật, quy trình dài; chỉ đọc khi đúng việc.

**Vì sao.** Chi phí nạp lặp lại ở mọi lượt của mọi phiên; một dòng thừa ở tầng nạp đắt hơn nhiều so với một dòng ở tầng chi tiết.

## Khi nào chưa cần cả bộ

Người dùng chỉ chạy một phiên mỗi lúc, việc nhỏ, ít khi dở dang thì chưa cần hai vai hay sổ vai.
Nguyên lý 3, 5, 6 thì đáng dùng ở mọi quy mô. Chọn mảnh theo đau thật của người dùng, xem [03_ApDung.md](03_ApDung.md).
