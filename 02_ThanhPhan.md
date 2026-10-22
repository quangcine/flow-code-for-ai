# 02 · Mười hai mảnh ghép

Mỗi mảnh đủ bốn mục: **Vấn đề** · **Cơ chế** · **Bản tối thiểu** · **Khi nào chưa cần**.
Các mảnh độc lập tương đối; ⛔ không cần dựng đủ 12. Thứ tự dựng gợi ý ở [03_ApDung.md](03_ApDung.md).
"Bản mẫu" ở cuối mỗi mảnh là tệp trong repo `quangcine/roleflow`, đọc để tham khảo cách viết, ⛔ không chép nguyên.

## ① Hai vai và lệnh vào, rời vai

#### Vấn đề
Nhiều phiên cùng mở trên một dự án mà ⛔ không phiên nào biết mình được làm gì: phiên nào cũng code, cũng commit, sửa đè nhau.
#### Cơ chế
- Hai vai: Leader (một) giao việc, commit, đóng việc; Planner (nhiều) khảo sát, viết kế hoạch.
- Ba lệnh: vào vai (chưa có Leader thì thành Leader, có rồi thì thành Planner), rời vai, tạm dừng kèm ghi việc dở.
- Vào vai thì xưng một dòng "Tôi là vai, mã, giờ vào"; đọc việc dở của vai mình trước, rồi mới đọc mục lục.
#### Bản tối thiểu
Một đoạn trong `CLAUDE.md` mô tả hai vai và quyền của từng vai, cộng một skill vào vai hỏi người dùng muốn nhận vai nào.
#### Khi nào chưa cần
Người dùng chỉ chạy một phiên mỗi lúc. Lúc ấy phiên duy nhất làm cả hai việc, chỉ cần giữ thói quen "viết kế hoạch trước, code sau".
Bản mẫu: `rulebook/Roles.md` (mục ①), `skills/start/SKILL.md`, `skills/done/SKILL.md`.

## ② Sổ vai có khoá

#### Vấn đề
Phiên tự xưng danh trong tin nhắn thì chỉ người nhận biết. Tên phiên có thể tự đổi; phiên đã xong việc vẫn hiện như đang chạy.
Hai phiên sửa tay cùng một tệp sổ thì một bên mất dòng.
#### Cơ chế
- Một tệp sổ ở gốc dự án, chỉ giữ phiên **đang sống** (vai, mã, giờ vào, đang làm gì); ⛔ không giữ lịch sử.
- Mọi thao tác ghi sổ đi qua một script có khoá tệp; ⛔ không sửa tay. Hai phiên gõ cùng lúc vẫn nhận hai mã khác nhau.
- Đối chiếu bằng giờ vào trong sổ, ⛔ không tin tên phiên.
#### Bản tối thiểu
Một script nhỏ với ba lệnh: ghi dòng, xoá dòng, in sổ. Khoá bằng `flock` hoặc cơ chế khoá tệp của ngôn ngữ người dùng quen.
#### Khi nào chưa cần
Chưa có hai vai (mảnh ①) thì chưa cần sổ. Chỉ một người, một phiên thì sổ là thủ tục thừa.
Bản mẫu: `scripts/activerole.py`, `skills/role-show/SKILL.md`.

## ③ Idea, Plan, mục lục trạng thái

#### Vấn đề
Ý tưởng bàn xong trôi mất; kế hoạch nằm rải trong tin nhắn; ⛔ không ai biết việc nào đã duyệt, việc nào đang làm, việc nào bỏ.
#### Cơ chế
- Hai loại tệp: **Idea** (vì sao, chọn hướng nào, người dùng đã chốt gì) và **Plan** (bước thi công, tiêu chí xong, đường lùi, tệp nào được chạm).
- Tên tệp mang mốc giờ tạo để ⛔ không trùng và sắp theo thời gian.
- Tệp đứng yên trong một thư mục; trạng thái là dòng trong các tệp mục lục (nháp, đã qua rà, xong, huỷ, hoãn), có cột "đang cầm".
- Plan có dòng nhật ký: ai bắt đầu thi công, lúc nào dừng.
#### Bản tối thiểu
Một thư mục kế hoạch, một khuôn Plan (mục tiêu, bước có ô đánh dấu, tiêu chí xong) và hai tệp mục lục: đang làm, đã xong.
#### Khi nào chưa cần
Việc làm xong trong một phiên, ⛔ không cần ai rà. Tách Idea khỏi Plan chỉ đáng khi một ý tưởng sinh nhiều Plan hoặc cần bàn nhiều vòng.
Bản mẫu: `rulebook/Roles.md` (mục sổ vai và mục lục), `skills/PlanModule/SKILL.md`.

## ④ Rà Plan

#### Vấn đề
Plan viết xong trông sạch, nhưng thi công thì lộ bước thiếu, con số sai, hai mục chỏi nhau. Sửa lúc thi công đắt hơn nhiều lúc còn trên giấy.
#### Cơ chế
- Rà nhiều lớp, ⛔ không lớp nào thay lớp nào: logic (mỗi khẳng định đã đo hay đang đoán), đọc trọn để bắt mâu thuẫn,
  đo lại từng con số bằng lệnh, kiểm quy ước (khuôn, link, chữ phủ định ⛔ không rơi mất).
- Mỗi vòng một agent rà mới, ⛔ không mang thiên kiến của vòng trước; lặp tới khi một vòng ra 0 lỗi, đặt trần (vd 3 vòng);
  hết trần mà chưa sạch thì dừng, hỏi người dùng đi tiếp hay xem lại cách viết Plan.
- Lỗi hình thức, số liệu thì tự sửa; đụng phạm vi, thiết kế thì hỏi người dùng.
#### Bản tối thiểu
Một skill liệt kê bốn lớp rà và một khuôn báo lỗi (loại, chỗ, vì sao sai, cách sửa). Chạy tay sau mỗi lần viết Plan.
#### Khi nào chưa cần
Plan vài dòng, sửa một chỗ, đường lùi rẻ. Lúc ấy đo lại các con số là đủ.
Bản mẫu: `skills/reviewplan/SKILL.md`, `agents/plan-reviewer.md`, `skills/checkplan/SKILL.md`.

## ⑤ Thi công bằng subagent Coder, Reviewer, Tester

#### Vấn đề
Leader tự code thì cạn ngữ cảnh; một agent vừa code vừa tự chấm thì dễ chấm dễ dãi.
#### Cơ chế
- Ba subagent nối tiếp: Coder viết, Reviewer chỉ đọc và chấm, Tester chạy cửa verify và đo hành vi thật.
- Một thư mục pipeline chung: mỗi agent ghi kết quả vào tệp, agent sau đọc tệp của agent trước. Leader chỉ đọc dòng kết luận.
- Coder soi Plan trước khi code; thấy lệch thì dừng, trả câu hỏi về Leader.
- Mắc ở đâu thì gọi một Coder **mới** cho vòng sửa, chỉ đưa tệp lỗi; ⛔ không nhắn tiếp Coder cũ.
- Tin gọi luôn dặn: mơ hồ thì dừng hỏi; ⛔ không commit, push, deploy; báo cáo liệt kê đường đầy đủ từng tệp đã chạm.
#### Bản tối thiểu
Một agent Coder và một agent Reviewer, cộng một skill mô tả thứ tự gọi và thư mục pipeline.
#### Khi nào chưa cần
Việc sửa vài dòng mà người dùng đứng xem trực tiếp. Lưu ý: subagent ⛔ không có công cụ hỏi người dùng, mọi câu hỏi phải đi qua Leader.
Bản mẫu: `skills/codeplan/SKILL.md`, `agents/executor.md`, `agents/reviewer.md`, `agents/qa-testing.md`.

## ⑥ Sổ nợ ngắn hạn và lệnh tạm dừng

#### Vấn đề
Phiên hết ngữ cảnh hay người dùng phải đi giữa chừng; việc dở chỉ nằm trong đầu phiên đó và mất theo.
#### Cơ chế
- Lệnh tạm dừng viết một tệp nợ ngắn theo khuôn cố định: việc dở, Plan đang cầm, tệp đã chạm chưa commit, bước tiếp, câu đang chờ người dùng.
- Một tệp chỉ mục nợ; phiên mới vào vai đọc nợ của vai mình trước, nhận nợ thì đánh dấu giữ chỗ để phiên khác ⛔ không nhận trùng.
- Nợ dài hạn (hoãn có điều kiện) để riêng, chỉ đọc khi người dùng hỏi.
#### Bản tối thiểu
Một khuôn tệp nợ năm mục, giới hạn vài chục dòng, và một dòng trong luật: "vào phiên thì đọc nợ trước".
#### Khi nào chưa cần
Việc thường xong gọn trong một phiên. Có dấu hiệu cần: người dùng hay hỏi "lần trước làm tới đâu rồi".
Bản mẫu: `skills/pause/SKILL.md`, `scripts/activerole.py`.

## ⑦ Cửa verify đúng kho

#### Vấn đề
Claude báo "xong" khi chưa chạy kiểm tra nào, hoặc chạy kiểm tra của kho khác. Lỗi kiểu dữ liệu, tên sai lọt tới người dùng.
#### Cơ chế
- Mỗi kho ghi rõ lệnh verify của nó trong `CLAUDE.md` của kho (kiểm kiểu, lint, các script soát riêng).
- Định tiêu chí xong **trước** khi làm; làm tới khi cửa xanh. Phần động ⛔ không tự đo được thì báo người dùng test.
- Cửa dùng chung hỏng thì ⛔ không sửa giữa lượt; ghi nợ, sửa khi mọi vai đã dừng.
#### Bản tối thiểu
Một dòng trong `CLAUDE.md` mỗi kho: lệnh verify là gì, chạy ở thư mục nào.
#### Khi nào chưa cần
Kho chỉ có tài liệu, ⛔ không có gì để kiểm tự động. Khi ấy tiêu chí xong là danh sách đọc soát.
Bản mẫu: `rulebook/Details.md` (Nguyên tắc làm việc, mục 4), `templates/CLAUDE.md`.

## ⑧ Hạn mức ngữ cảnh

#### Vấn đề
Phiên chạy dài, ngữ cảnh phình tới lúc bị nén tự động giữa một việc dở; sau nén, phiên làm tiếp theo bản tóm tắt thiếu chi tiết.
#### Cơ chế
- Một ngưỡng cố định; chạm ngưỡng thì ⛔ không nhận việc mới, xong việc dở rồi tạm dừng hoặc rời vai.
- Đo bằng script đọc số token thật của lượt cuối trong nhật ký phiên, ⛔ không ước theo kích thước tệp nhật ký.
- Vừa bị nén thì đọc lại luật vai và mốc Plan đang cầm, ⛔ không tin bản tóm tắt.
#### Bản tối thiểu
Một dòng luật nêu ngưỡng và việc phải làm khi chạm; đo tay khi phiên đã chạy lâu.
#### Khi nào chưa cần
Phiên thường ngắn, ít khi tới ngưỡng nén.
Bản mẫu: `skills/ctx/SKILL.md`, `rulebook/Roles.md` (mục ⑥).

## ⑨ Memory: một tệp một sự thật, mục lục dẫn link

#### Vấn đề
Bài học ghi chép lại ở nhiều nơi (luật, kế hoạch, lời nhắc), lâu ngày các bản lệch nhau mà ⛔ không cửa nào bắt.
#### Cơ chế
- Mỗi sự thật một tệp memory riêng, có tên ngắn.
- Mục lục memory chỉ một dòng mỗi mục: nhãn ngắn đủ biết có cần mở hay không, cộng link. Dòng dài quá một ngưỡng là đang viết lại, ⛔ không còn là dẫn link.
- Tài liệu khác cần nhắc thì dẫn link, ⛔ không chép.
- Chỉ Leader ghi memory; vai khác ghi bài học vào báo cáo, Leader quyết.
#### Bản tối thiểu
Thư mục memory sẵn có của Claude Code, cộng luật "dẫn link, ⛔ không chép" và giới hạn độ dài mỗi dòng mục lục.
#### Khi nào chưa cần
Người dùng còn ít bài học, mục lục chưa tới vài chục dòng. Luật dẫn link vẫn nên có ngay từ đầu.
Bản mẫu: `rulebook/Details.md` (Ba luật quản lý luật).

## ⑩ Tách luật nạp mỗi phiên và luật chi tiết

#### Vấn đề
`CLAUDE.md` phình vì mỗi luật kéo theo lý do, ca thật; mọi lượt của mọi phiên trả giá đọc lại.
#### Cơ chế
- Tệp nạp mỗi phiên chỉ giữ bản ngắn của luật cộng bảng "làm việc gì thì đọc gì".
- Tệp chi tiết giữ lý do, ca thật, quy trình; đọc qua skill hoặc khi đúng việc. Hai nơi vênh thì bản ngắn thắng.
- Ghi luật mới thì tìm luật cũ có thể mâu thuẫn ở mọi nơi; thấy thì báo người dùng, ⛔ không tự chọn bên thắng.
- Sửa luật xong thì nhắn các phiên đang chạy: luật chỉ nạp lúc phiên khởi động.
#### Bản tối thiểu
Tách `CLAUDE.md` thành hai tệp: bản ngắn và bản chi tiết, bản ngắn có một bảng trỏ sang mục tương ứng.
#### Khi nào chưa cần
`CLAUDE.md` của người dùng còn ngắn (vài chục dòng). Tách sớm chỉ thêm một chỗ phải đồng bộ.
Bản mẫu: `templates/CLAUDE.md`, `rulebook/Details.md`, `skills/rules-details/SKILL.md`.

## ⑪ Cửa kiểm tài khoản trước mỗi lệnh đẩy

#### Vấn đề
Một máy đăng nhập nhiều tài khoản (GitHub, cơ sở dữ liệu cloud, nền tảng deploy); đẩy nhầm tài khoản là hỏng ở nơi khó gỡ.
#### Cơ chế
- Ngay trước mỗi lệnh đẩy, chạy lệnh in tài khoản đang dùng (vd `git remote -v`, lệnh `whoami` của CLI) và in ra cho người dùng.
- Căn cứ là định danh (email, mã tài khoản, mã dự án), ⛔ không phải tên tài nguyên.
- Sai thì dừng, báo người dùng; ⛔ không tự đăng xuất, đăng nhập lại hay đổi token.
- Từ khoá đẩy do người dùng gõ; Claude làm xong thì verify rồi chờ.
#### Bản tối thiểu
Một skill deploy liệt kê lệnh kiểm tài khoản của từng công cụ người dùng có, cộng một dòng luật "kiểm trước mỗi lệnh đẩy".
#### Khi nào chưa cần
Người dùng chỉ có một tài khoản cho mọi dịch vụ và chưa cho Claude tự đẩy.
Bản mẫu: `skills/git/SKILL.md`, `rulebook/Details.md` (mục Deploy).

## ⑫ Quy ước hỏi người dùng

#### Vấn đề
Claude hỏi trống kiểu "chọn A hay B?"; người dùng ⛔ không thấy cơ chế đang chạy nên trả lời theo cảm giác, quyết định sai đi thẳng vào mã.
#### Cơ chế
- Văn xuôi trước: đang có gì, chỗ hở ở đâu, một ví dụ cụ thể có số liệu, vì sao Claude ⛔ không tự quyết được.
- Rồi mới gọi `AskUserQuestion` với một câu ngắn; mỗi lựa chọn nói được gì, mất gì.
- Mỗi lượt một câu; câu thuộc Plan nào thì phiên đang cầm Plan đó hỏi, tránh hai phiên hỏi cùng một chuyện.
- Hỏi về giao diện thì mở ảnh từng lựa chọn cho người dùng xem.
#### Bản tối thiểu
Hai dòng luật trong `CLAUDE.md`: "chưa chắc thì hỏi bằng `AskUserQuestion`" và "bối cảnh viết trước, câu hỏi một dòng".
#### Khi nào chưa cần
Luôn cần. Chỉ mức chi tiết của bối cảnh co giãn theo độ lớn của quyết định.
Bản mẫu: `templates/CLAUDE.md`, `rulebook/Details.md` (mục Giao tiếp).
