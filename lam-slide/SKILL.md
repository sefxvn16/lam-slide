---
name: lam-slide
description: "Quy trình 5 bước giúp slide thuyết trình giữ đầy đủ nội dung từ tài liệu gốc: lập outline, dựng khung slide và map từng ý, chuyển khung đã duyệt cho skill tạo slide, sau đó đối chiếu outline để kiểm tra các ý bị thiếu. Skill chỉ đảm bảo tính đầy đủ của nội dung, không trực tiếp tạo file slide. Dùng khi người dùng cung cấp tài liệu gốc cụ thể (báo cáo, đề xuất, hồ sơ, biên bản họp...) và muốn chuyển thành slide hoặc bài thuyết trình, đặc biệt với tài liệu dài, nhiều nguồn hoặc dùng cho các buổi trình bày quan trọng; hoặc khi người dùng gõ /lam-slide hay yêu cầu làm slide theo đúng quy trình này. Không dùng cho slide sáng tạo tự do không có tài liệu gốc để bám sát, hoặc khi chỉ cần chỉnh thiết kế, định dạng một file slide có sẵn."
---

# Quy trình làm slide không mất nội dung quan trọng

## Phạm vi

Skill này chỉ đảm bảo nội dung slide đầy đủ và đúng với tài liệu gốc ở Bước 1, 2 và 4. Skill không trực tiếp dựng file slide và không thay thế skill tạo slide; phần dựng file ở Bước 3 được thực hiện bởi skill tạo slide dựa trên kết quả bàn giao tại bước này.

## Lý do thiết kế

Quy trình dựa trên một giả định: khi AI vừa hiểu nội dung vừa quyết định nội dung nào được đưa lên slide trong cùng một lượt xử lý (ví dụ yêu cầu “tóm tắt” rồi “dựng slide” ngay), AI sẽ tự đánh giá mức độ quan trọng mà không có bước đối chiếu, khiến người dùng khó nhận ra nội dung nào đã bị bỏ sót. Vì vậy, quy trình tách hai việc này thành các bước riêng và bổ sung một bước đối chiếu rõ ràng ở giữa.

## Áp dụng quy trình 5 bước sau, tuần tự, không gộp bước

### Bước 1 - Outline đầy đủ (KHÔNG phải tóm tắt)

Liệt kê đầy đủ các ý, số liệu và luận điểm trong tài liệu gốc dưới dạng outline chi tiết:

- Không rút gọn và không giới hạn độ dài
- Không tự đánh giá cái gì quan trọng/không quan trọng - liệt kê đầy đủ
- Nếu tài liệu dài hoặc có nhiều nguồn, chia theo từng phần và lập outline cho từng phần trước khi gộp lại, tránh bỏ sót nội dung ở các phần sau

Sau khi hoàn thành outline, dừng lại để người dùng kiểm tra và đối chiếu với tài liệu gốc, đồng thời đánh dấu các ý **bắt buộc giữ** (must-keep). Chỉ chuyển sang Bước 2 sau khi người dùng xác nhận outline đã đầy đủ.

### Bước 2 - Dựng khung slide có map tường minh

Từ outline đã được duyệt, nhóm các nội dung thành khung slide với số lượng slide theo yêu cầu của người dùng, hoặc tự đề xuất nếu người dùng không chỉ định.

Bắt buộc thể hiện rõ:

- Mỗi slide gồm những ý nào từ outline Bước 1, có map cụ thể và không ẩn
- Liệt kê riêng những ý **chưa xếp được vào slide nào** để người dùng chủ động quyết định giữ hay bỏ

Sau đó dừng lại, chờ người dùng duyệt bảng map và xác nhận việc giữ/bỏ các ý chưa được xếp vào slide. Chỉ chuyển sang Bước 3 sau khi đã có xác nhận.

### Bước 3 - Giao khung slide đã duyệt cho skill tạo slide

Skill này không tự dựng slide. Ở Bước 3, giao khung slide đã được duyệt cho skill tạo slide theo các điều khoản dưới đây, sau đó nhận kết quả để thực hiện Bước 4.

**Chọn skill tạo slide:**

- Nếu người dùng đã chỉ định skill: sử dụng đúng skill đó.
- Nếu người dùng chưa chỉ định: sử dụng skill tạo slide được nền tảng chọn theo cơ chế mặc định, trong số các skill người dùng đã cài, và thông báo cho người dùng biết đã sử dụng skill nào.
- Nếu người dùng chưa cài skill tạo slide: sử dụng skill tạo slide mặc định có sẵn trên nền tảng (ví dụ skill do Anthropic cung cấp sẵn trên Claude), nếu có.
- Không có skill nào kể trên: hỏi người dùng muốn dùng skill nào để tạo file .pptx trước khi tiếp tục. Nếu người dùng không có skill, chỉ bàn giao khung slide đã duyệt dưới dạng văn bản để người dùng tự dựng; không tự dựng file. Bước 4 được thực hiện khi người dùng gửi lại nội dung slide đã dựng.

**Đầu vào giao cho skill tạo slide:**

- Khung slide đã duyệt ở Bước 2, kèm theo map từng ý.
- Số lượng slide phải đúng như Bước 2.
- Mức độ bám nguồn: giữ sát cấu trúc và câu chữ của khung slide đã duyệt.
- Danh sách các ý must-keep đã đánh dấu ở Bước 1 và những câu người dùng yêu cầu giữ nguyên văn.
- Các yêu cầu về màu sắc, layout và phong cách do người dùng cung cấp.

Nếu skill tạo slide có bước xác nhận cấu trúc hoặc danh sách slide trước khi dựng, phải đối chiếu với map ở Bước 2 trước khi xác nhận.

**Đầu ra nhận lại:** slide hoặc file đã dựng, kèm nội dung chữ của từng slide. Yêu cầu skill tạo slide trả kèm phần nội dung này để làm đầu vào cho Bước 4. Nếu không có, đọc nội dung chữ trực tiếp từ file nếu môi trường cho phép; nếu không thể, yêu cầu người dùng cung cấp trước khi thực hiện Bước 4.

Lưu ý quan trọng: không mặc định rằng skill tạo slide đã kiểm tra tính đầy đủ của nội dung so với tài liệu gốc. Việc kiểm tra này vẫn thuộc Bước 1, 2 và 4 của skill này và phải được thực hiện độc lập với skill tạo slide được sử dụng.

Ràng buộc: Có thể rút gọn câu chữ để phù hợp với slide, nhưng không được bỏ bất kỳ ý nào trong danh sách must-keep ở Bước 1. Nếu người dùng yêu cầu “giữ nguyên văn”, phải giữ đầy đủ câu được yêu cầu, không tự ý cắt ngắn.

### Bước 4 - Đối chiếu outline với outline (không phải "kiểm tra tự do")

Liệt kê toàn bộ nội dung **hiện có trong slide đã dựng*** thành một outline mới. Sau đó đối chiếu từng dòng với outline gốc ở Bước 1 để xác định những ý bị thiếu.

Đây là phép đối chiếu trực tiếp (diff), không phải yêu cầu AI tự kiểm tra xem có bỏ sót gì không. Lý do là cùng một AI có thể lặp lại điểm mù ban đầu nếu chỉ được yêu cầu tự rà soát. Vì vậy, quy trình dùng đối chiếu từng dòng thay vì dựa vào việc tự kiểm tra.

Báo cáo rõ cho người dùng: ý nào khớp, ý nào bị thiếu, ý nào bị thiếu nhưng là do người dùng đã chủ động quyết định bỏ ở Bước 2.

Bổ sung các ý bị thiếu ngoài chủ đích vào slide, sau đó thực hiện lại một lượt đối chiếu để xác nhận..

### Bước 5 - Người dùng chỉnh sửa thủ công

Bước cuối cùng thuộc về người dùng, không phải AI.

## Phân việc với skill tạo slide

Skill này phụ trách phần nội dung khi chuyển tài liệu gốc thành slide. Skill tạo slide chỉ đảm nhiệm việc dựng file ở Bước 3, không thay thế các Bước 1, 2 và 4.

- **Chưa có nội dung gốc:** yêu cầu người dùng cung cấp tài liệu trước khi bắt đầu (ví dụ kịch bản pitch đã soạn), sau đó dùng tài liệu đó làm đầu vào cho Bước 1.
- **Slide sáng tạo tự do, không có tài liệu gốc:** không dùng skill này.

## Lưu ý khi thực hiện

- Không tự gộp Bước 1 và Bước 2, tức không vừa lập outline vừa nhóm nội dung thành slide trong cùng một lượt xử lý. Việc tách hai bước là cần thiết để giữ được điểm kiểm tra chéo của quy trình.
- Nếu người dùng chỉ yêu cầu “làm slide từ tài liệu này” mà không đề cập đến quy trình, mặc định vẫn thực hiện đầy đủ 5 bước, trừ khi người dùng yêu cầu bỏ qua bước cụ thể.
- Nếu người dùng bỏ qua Bước 2: thông báo ngắn gọn rằng sẽ không có bảng map để phân biệt nội dung bị thiếu ngoài ý muốn với nội dung người dùng chủ động bỏ. Sau đó dùng outline đã duyệt ở Bước 1 làm đầu vào cho Bước 3; Bước 4 vẫn đối chiếu với outline ở Bước 1.
- Cách chọn skill tạo slide và quy trình giao nhận thực hiện theo Bước 3.
