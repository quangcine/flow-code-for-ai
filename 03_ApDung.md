# 03 · Áp dụng ở máy người dùng

Quy trình sáu bước bạn (Claude) làm khi người dùng đưa repo này. ⛔ Không nhảy bước; mỗi bước có đầu ra cụ thể.

## Bước 1 · Khảo sát

Mục tiêu: biết người dùng đang có gì, bằng số đếm, ⛔ không đoán.
- Đọc `~/.claude`: tệp `CLAUDE.md`, thư mục `skills/`, `agents/`, `commands/` nếu có, `settings.json` (hook, quyền).
- Đọc `CLAUDE.md` (hoặc `AGENTS.md`) ở gốc dự án đang mở, và mọi thư mục tài liệu, kế hoạch sẵn có.
- Đếm bằng lệnh: số skill, số agent, số dòng `CLAUDE.md`, số tệp kế hoạch. Ghi lệnh kèm kết quả.
- Hỏi người dùng thói quen thật: thường mở mấy phiên cùng lúc, việc hay dở dang ở đâu, từng mất công vì chuyện gì.

Đầu ra: một bảng ngắn "đang có" trình người dùng xem, kèm lệnh đã chạy.

## Bước 2 · Đối chiếu từng mảnh

Với mỗi mảnh ở [02_ThanhPhan.md](02_ThanhPhan.md), xếp vào một trong ba ô:
- **Có rồi**: người dùng đã có thứ làm cùng việc, có thể dưới tên khác. Giữ cái của họ, ⛔ không dựng thêm bản thứ hai.
- **Thiếu**: chưa có gì làm việc này. Xét mục "Khi nào chưa cần" trước khi xếp vào danh sách nên dựng.
- **Xung đột**: thứ họ có làm ngược nguyên lý (vd luật cho mọi phiên tự commit). Nêu rõ chỗ ngược, ⛔ không tự sửa.

Đầu ra: bảng 12 dòng, mỗi dòng một ô và một câu lý do.

## Bước 3 · Hỏi người dùng chọn mảnh đầu tiên

- Trình bảng bước 2 ở văn xuôi trước, rồi hỏi bằng `AskUserQuestion`, mỗi lượt một câu.
- Gợi ý thứ tự (người dùng có quyền đổi): Idea và Plan (③) → sổ nợ (⑥) → hai vai (① ②) → subagent thi công (⑤).
  Lý do: mảnh đầu đem lợi ngay cả khi chỉ một phiên; mảnh sau chỉ có giá trị khi đã có mảnh trước.
- Mảnh ⑦ (cửa verify) và ⑫ (quy ước hỏi) rẻ, có thể đi kèm mảnh đầu nếu người dùng đồng ý.
- Mảnh nằm ô "Xung đột" thì hỏi riêng: giữ cách của họ, hay đổi theo nguyên lý; nói được gì, mất gì.

## Bước 4 · Dựng một mảnh

- Viết theo tên thư mục, ngôn ngữ, công cụ của người dùng; ⛔ không chép câu chữ bản mẫu.
- Viết tiêu chí xong của mảnh **trước** khi dựng (bước 5 đo theo đó).
- Sửa `CLAUDE.md` của người dùng thì sao lưu trước, chỉ thêm đúng đoạn cần, trình phần thêm cho họ duyệt.
- Mảnh có script thì kèm lệnh chạy thử và kết quả mong đợi.
- Dựng xong, nhắc người dùng mở phiên mới: luật, skill, agent chỉ nạp lúc phiên khởi động.

## Bước 5 · Kiểm

- Đo theo tiêu chí đã viết ở bước 4, bằng lệnh; ghi lệnh kèm kết quả.
- Phần cần dùng thật (vd lệnh vào vai ở phiên thứ hai) thì nhờ người dùng chạy, ⛔ không tự khai là đạt.
- Để người dùng dùng thật **ít nhất một phiên** trước khi bàn mảnh tiếp.

## Bước 6 · Lặp

- Hỏi người dùng sau khi dùng: chỗ nào vướng, chỗ nào thừa. Thừa thì gỡ, ⛔ không giữ cho đủ bộ.
- Quay lại bước 3 với mảnh tiếp theo.
- Mỗi lần thêm luật, tìm luật cũ có thể mâu thuẫn (xem mảnh ⑩) và báo người dùng nếu thấy.

## ⛔ Đừng làm

- **Cài nguyên `quangcine/roleflow` rồi bảo là xong.** Bản mẫu mang giả định của dự án khác (cây thư mục, tên lệnh, quy ước);
  người dùng sẽ có hai bộ luật song song, ⛔ không biết bộ nào thắng.
- **Ghi đè `CLAUDE.md` của người dùng.** Tệp đó chứa thói quen họ đã tích luỹ; mất là mất luôn. Chỉ thêm, có sao lưu, có duyệt.
- **Dựng đủ 12 mảnh trong một phiên.** Chưa dùng thật thì ⛔ không biết mảnh nào cần; dựng hết là đẻ luật ⛔ không ai theo,
  và ngữ cảnh phiên cạn trước khi kịp kiểm.
- **Tự quyết thay người dùng** ở chỗ đổi thói quen làm việc của họ. Mọi thay đổi quy trình đều phải hỏi.
- **Báo xong khi chưa đo.** Mỗi mảnh xong phải có lệnh đo và kết quả.
