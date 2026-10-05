# lam-slide

[English](README.md) | **Tiếng Việt**

Skill cho Claude giúp slide thuyết trình giữ đủ nội dung quan trọng so với tài liệu gốc. Skill chỉ lo phần nội dung, không có chức năng dựng file slide. Việc dựng file slide giao cho skill tạo slide mà bạn đang dùng.

## Skill làm gì

Khi chuyển một tài liệu thành slide, AI dễ vừa tóm tắt vừa quyết định cái gì lên slide trong cùng một lượt, và phần bị bỏ thì không hiện ra để người dùng thấy. Skill tách việc này thành 5 bước, có hai điểm dừng để người dùng duyệt:

1. **Outline đầy đủ** từ tài liệu gốc (không tóm tắt). Dừng để người dùng đối chiếu và đánh dấu ý bắt buộc giữ (must-keep).
2. **Khung slide có map**: mỗi slide lấy ý nào từ outline, ý nào chưa xếp được. Dừng để người dùng duyệt và quyết định giữ hay bỏ.
3. **Giao khung đã duyệt cho skill tạo slide** theo một hợp đồng giao nhận: số slide cố định, mức bám nguồn, danh sách must-keep; nhận lại slide kèm nội dung chữ từng slide.
4. **Đối chiếu outline với outline**: so nội dung slide đã dựng với outline gốc, báo ý khớp, ý bị rơi, ý bỏ có chủ đích.
5. **Người dùng chỉnh sửa thủ công.**

## Ranh giới

- Skill **không** tự dựng file .pptx hay slide và không thay thế skill tạo slide.
- Skill chọn skill tạo slide theo thứ tự: skill người dùng chỉ định → skill được nền tảng chọn mặc định trong số skill người dùng đã cài → skill tạo slide có sẵn mặc định trên nền tảng (nếu có) → hỏi người dùng. Nếu không có skill nào, skill giao khung slide dạng văn bản để người dùng tự dựng.
- Skill không dùng cho slide sáng tạo tự do không có tài liệu gốc.

## Cấu trúc thư mục

```
lam-slide/
  SKILL.md
README.md
README.vi.md
LICENSE.md
```

## Cài đặt

### Ứng dụng Claude (claude.ai, Claude desktop)

1. Tải repo về, nén riêng thư mục `lam-slide` thành `lam-slide.zip` (file zip phải chứa thư mục `lam-slide` ở cấp ngoài cùng).
2. Mở Claude, vào **Customize → Skills**, bấm **+** → **Create skill** → **Upload a skill** và chọn `lam-slide.zip`. Tên và vị trí menu có thể khác tùy phiên bản ứng dụng. Skill cần bật tính năng chạy mã (code execution).
3. Kiểm tra skill `lam-slide` đã hiện trong danh sách và đang bật.

### Claude Code

Chép thư mục `lam-slide` vào `~/.claude/skills/` (dùng cho mọi dự án) hoặc `.claude/skills/` của một dự án, rồi khởi động lại Claude Code.

Bạn cần có sẵn một skill tạo slide (hoặc dùng skill có sẵn của nền tảng) để chạy Bước 3.

## Cách dùng

Skill kích hoạt khi bạn đưa tài liệu gốc và yêu cầu làm slide, hoặc gọi trực tiếp bằng `/lam-slide`. Nên gọi trực tiếp khi bạn cài nhiều skill liên quan đến slide và muốn chắc chắn quy trình này chạy. Ví dụ:

- "Chuyển báo cáo này thành 12 slide cho buổi họp: …"
- "/lam-slide Làm slide từ hai tài liệu đính kèm, giữ nguyên văn các con số."

## Giới hạn

- Quy trình chưa được kiểm chứng thực nghiệm. Các lý do thiết kế trong SKILL.md là giả thuyết.
- Bước 4 cần nội dung chữ của từng slide. Nếu skill tạo slide không trả lại được và môi trường không đọc được file, bạn sẽ được nhờ cung cấp nội dung này.
- Bước 4 tìm ý bị rơi so với outline gốc; nó không được thiết kế để phát hiện nội dung bị thêm vào.

## Góp ý

Mọi góp ý xin gửi qua mục **Issues** của repo. Để dễ xử lý, nên ghi:

- yêu cầu bạn đưa ra và loại tài liệu gốc (đã bỏ thông tin cá nhân hoặc thông tin mật);
- skill tạo slide bạn dùng ở Bước 3;
- kết quả bạn mong đợi và kết quả thực tế.

Đặc biệt mong góp ý về: skill kích hoạt nhầm hoặc không kích hoạt, chỗ bàn giao ở Bước 3 bị lệch, Bước 4 bỏ lọt ý bị rơi, và chỗ hướng dẫn khó hiểu.

## Giấy phép

Skill phát hành theo giấy phép **CC BY-NC 4.0**: dùng miễn phí cho mục đích phi thương mại, cần ghi nguồn. Muốn dùng thương mại, vui lòng liên hệ tác giả qua mục **Issues**. Xem [LICENSE.md](LICENSE.md).
