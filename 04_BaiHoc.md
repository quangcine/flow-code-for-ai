# 04 · Bài học đã trả giá

Mỗi bài theo khuôn: **chuyện gì xảy ra · vì sao · luật rút ra · điều kiện áp dụng**.
Ca thật được kể trung tính; con số giữ lại khi chính nó là bài học.

## 1. Chia đợt theo "script hoá được hay không", ⛔ không theo số dòng

- **Chuyện gì xảy ra.** Một việc sửa hàng loạt được chia đợt theo số dòng. Đo lại thì lối viết script tốn khoảng 2,5 token mỗi dòng,
  lối đọc rồi sửa từng tệp tốn khoảng 14: chênh khoảng 5 lần.
- **Vì sao.** Số dòng ⛔ không nói lên chi phí; chi phí nằm ở chỗ mô hình có phải đọc từng chỗ hay ⛔ không.
- **Luật rút ra.** Trước khi chia đợt, hỏi "phần nào viết được thành script"; phần đó gom một đợt.
- **Điều kiện áp dụng.** Việc lặp lại cùng một khuôn. Việc mỗi chỗ một kiểu thì vẫn phải đọc từng chỗ.

## 2. ⛔ Không ghi kết quả vào tài liệu trong cùng lệnh sinh ra kết quả

- **Chuyện gì xảy ra.** Một lệnh vừa chạy phép đo vừa ghi câu kết luận vào tài liệu; câu ấy viết trước khi biết kết quả.
- **Vì sao.** Lúc gõ lệnh chưa có số; câu ghi ra là câu đoán, dù trông như đã đo.
- **Luật rút ra.** Chạy đo, đọc kết quả, rồi mới ghi ở lệnh sau.
- **Điều kiện áp dụng.** Mọi tài liệu ghi số đo: Plan, báo cáo, tệp nợ.

## 3. Luật nào cũng ghi kèm điều kiện áp dụng

- **Chuyện gì xảy ra.** Một luật "làm tệp nặng trước" được áp cho cả lối script, nơi nó vô nghĩa.
- **Vì sao.** Luật ra đời trong một hoàn cảnh; mang sang hoàn cảnh khác mà ⛔ không ghi điều kiện thì thành luật sai.
- **Luật rút ra.** Mỗi luật kèm một câu "đúng khi nào", như chính khuôn của tệp này.
- **Điều kiện áp dụng.** Mọi luật bạn viết cho người dùng.

## 4. Cửa verify chung hỏng thì ⛔ không sửa giữa lượt

- **Chuyện gì xảy ra.** Đang thi công thì cửa kiểm dùng chung báo đỏ vì lỗi của chính cửa; ý định đầu tiên là sửa luôn.
- **Vì sao.** Sửa thước ngay lúc đang đo, sửa hụt là cửa lọt thứ khác mà ⛔ không ai biết; các phiên khác đang dựa vào cửa ấy.
- **Luật rút ra.** Ghi nợ, ⛔ không khai đạt; sửa cửa khi mọi vai đã dừng, rồi chạy lại cho mọi việc dở.
- **Điều kiện áp dụng.** Có từ hai phiên dùng chung một cửa kiểm.

## 5. Coder soi Plan trước khi code

- **Chuyện gì xảy ra.** Một mốc Plan ghi khoảng 350 dòng phải sửa; Coder đo ra khoảng 1.900, gấp hơn 5 lần, vì Plan chỉ đếm phần vỏ.
- **Vì sao.** Plan viết lúc chưa mở hết mã; số đếm sai đều ở mọi chỗ thì đọc ⛔ không thấy.
- **Luật rút ra.** Người thi công đo lại số liệu, danh sách tệp trước khi làm; lệch thì dừng, trả về người giao.
- **Điều kiện áp dụng.** Mọi lần giao Plan cho một phiên hay subagent khác người viết.

## 6. Soát báo cáo bằng cơ chế khác, soi chỗ khẳng định ⛔ không kèm đo

- **Chuyện gì xảy ra.** Báo cáo thi công ghi "hành vi giữ nguyên". Mở mã thì thấy một lớp mới dựng thẻ ảnh với địa chỉ rỗng.
- **Vì sao.** Câu khẳng định ⛔ không kèm phép đo là câu đoán; người viết báo cáo tin mã của mình.
- **Luật rút ra.** Trước khi chuyển tiếp báo cáo: kiểm lại vài số then chốt bằng cách đếm khác, mở mã ở mọi câu khẳng định trần.
- **Điều kiện áp dụng.** Mọi báo cáo từ subagent hay phiên khác, trước khi tới tay người dùng.

## 7. Chốt xong ⛔ không phải lệnh giao

- **Chuyện gì xảy ra.** Người dùng vừa chốt một thay đổi cấu trúc thì phiên điều phối giao thi công ngay;
  bước thi công chỉ nằm trong một tin nhắn dài, người dùng phải chặn lại.
- **Vì sao.** Một tin nhắn ⛔ không có tiêu chí nghiệm thu, đường lùi, và ⛔ không ai rà.
- **Luật rút ra.** Chốt → ghi vào Plan → rà tới sạch → chờ người dùng bảo giao.
- **Điều kiện áp dụng.** Mọi thay đổi chạm nhiều tệp hoặc khó lùi. Sửa một dòng người dùng đứng xem thì có thể làm ngay nếu họ nói rõ.

## 8. Rà Plan phải nhiều vòng, mỗi vòng một agent mới

- **Chuyện gì xảy ra.** Một Plan đóng gói cấu hình qua năm vòng rà: 26 lỗi, rồi 10, 8, 3, cuối cùng 0.
  Ở nơi khác, vòng 3 vẫn ra 18 lỗi, vòng 6 còn bắt một con số sai gần 7 lần; một câu rơi mất chữ "không" biến cảnh báo thành lời cho phép.
- **Vì sao.** Mỗi vòng sửa lại đẻ chỗ lệch mới; người rà cũ quen mắt với câu đã đọc.
- **Luật rút ra.** Lặp tới khi một vòng ra 0 lỗi; đo lại số bằng lệnh; sau khi bác một tiền đề, tìm chính chuỗi đó trên toàn bộ tài liệu.
- **Điều kiện áp dụng.** Plan nhiều bước hoặc chạm nhiều tệp. Plan vài dòng thì một vòng là đủ.

## 9. Đổi nền dưới một Plan đã duyệt thì trả Plan về rà lại

- **Chuyện gì xảy ra.** Plan đã qua rà thì một thư mục cấu hình nó dựa vào bị đổi tên; Plan phải trả về nháp, rà lại hai vòng mới giao được.
- **Vì sao.** Plan ghi đường, số đếm theo nền cũ; thi công theo đó là sai từ bước đầu.
- **Luật rút ra.** Trước khi giao, đo lại phần "hiện trạng" của Plan; nền đổi thì trả về rà.
- **Điều kiện áp dụng.** Plan nằm chờ lâu, hoặc có việc khác chạm cùng vùng trong lúc chờ.

## 10. Tên thư mục cấu hình có thể bị nạp ngầm

- **Chuyện gì xảy ra.** Một thư mục luật chi tiết đặt tên `rules/` trong thư mục cấu hình của Claude Code; mọi tệp `.md` trong đó
  bị nạp vào mọi phiên và mọi subagent, thêm khoảng 12 nghìn token mỗi nơi.
- **Vì sao.** Claude Code có quy ước tự nạp với tên đó; tách luật ra để đọc khi cần mà vẫn bị nạp hết.
- **Luật rút ra.** Đặt tên khác cho thư mục luật đọc theo việc; đo ngữ cảnh khởi động sau mỗi lần đổi cấu trúc cấu hình.
- **Điều kiện áp dụng.** Mọi lần thêm thư mục vào cấu hình Claude Code. Kiểm tài liệu bản Claude Code người dùng đang chạy.

## 11. Dẫn link, ⛔ không chép

- **Chuyện gì xảy ra.** Một tệp lời nhắc chép tay phình tới hơn 34 nghìn ký tự, hơn 200 luật, nặng hơn cả mục lục memory,
  trong khi phần lớn đã có memory riêng.
- **Vì sao.** Chép là nuôi hai bản của một luật; tới ngày lệch nhau ⛔ không cửa nào bắt.
- **Luật rút ra.** Đã có nơi giữ thì dẫn link một dòng; chưa có thì viết nơi giữ trước rồi mới rút gọn.
- **Điều kiện áp dụng.** Mọi tài liệu; việc nhất thời (số đo tạm, ranh giới tệp một lần) thì viết thẳng.

## 12. Trùng thì giữ một, cũ có thay thế thì bỏ; nhưng đo trước

- **Chuyện gì xảy ra.** Đếm trong nhật ký phiên thì 15 lệnh tự viết có 0 lần dùng, vì skill thi công và bảng agent đã làm thay.
- **Vì sao.** Đồ thừa vẫn tốn ngữ cảnh và gây nhầm lẫn khi tên na ná nhau.
- **Luật rút ra.** Chỉ dọn khi người dùng bảo hoặc khi thêm cái thay thế; đo còn ai dùng, link nào trỏ tới, rồi trình người dùng; dời vào chỗ xoá mềm, ⛔ không xoá hẳn.
- **Điều kiện áp dụng.** Có dữ liệu dùng thật để đếm. Chưa đếm được thì để yên.

## 13. Luật mới ⛔ không tới phiên đang chạy

- **Chuyện gì xảy ra.** Phiên điều phối ghi một luật mới, nhưng chính nó đã vào phiên trước giờ ghi, nên ngữ cảnh của nó vẫn mang bản cũ.
- **Vì sao.** `CLAUDE.md`, skill, agent nạp lúc phiên khởi động.
- **Luật rút ra.** Ghi luật mới thì làm hai việc: ghi tệp cho phiên sau, nhắn tay từng phiên đang chạy.
- **Điều kiện áp dụng.** Có nhiều phiên chạy song song lúc sửa luật.

## 14. Giao subagent theo mốc, đọc theo dòng

- **Chuyện gì xảy ra.** Đo nhiều ngày: subagent thi công trung bình khoảng 240 nghìn token ngữ cảnh mỗi lượt, vì ôm trọn Plan.
  Khoảng 97% chi phí subagent là đọc lại ngữ cảnh.
- **Vì sao.** Mỗi lượt gọi công cụ đọc lại mọi thứ đã nạp.
- **Luật rút ra.** Plan nhiều mốc thì mỗi mốc một subagent; tin gọi ghi khoảng dòng cần đọc; vòng sửa gọi agent mới chỉ kèm tệp lỗi.
- **Điều kiện áp dụng.** Plan dài, nhiều mốc. Plan ngắn giao trọn vẫn rẻ.
