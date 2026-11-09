# Mini guideline — bài làm cá nhân

> Điền nội dung này trước khi bắt đầu gán nhãn. Giữ lại các quyết định sau khi self-QC.

## Định nghĩa lớp

| Lớp | Định nghĩa của bạn | Ví dụ/điểm phân biệt |
| --- | --- | --- |
| `car` | Xe chở người cỡ nhỏ, 4 bánh, khoang lái và khoang khách liền nhau, thân thấp. Gồm sedan, hatchback, SUV, taxi và xe bán tải. | Nóc thấp, thường có nắp capo và cốp nhô ra rõ. Taxi vàng vẫn là car. Bán tải có thùng hở phía sau vẫn là car, không phải truck. |
| `truck` | Xe chuyên chở hàng hóa: cabin lái tách riêng với thùng hàng hoặc rơ-moóc phía sau. Gồm xe tải thùng, xe ben, xe đầu kéo, xe chuyên dụng (cẩu, cứu hộ). | Có khe hoặc đường ranh rõ giữa cabin và thùng. Thùng hàng thường cao và vuông hơn cabin. Xe chở hàng chất cao vẫn là truck. |
| `bus` | Xe chở khách cỡ lớn, thân dài hình hộp liền khối, nhiều cửa sổ chạy dọc thân. Gồm xe buýt thành phố, xe buýt nối toa, xe 2 tầng, minibus chở khách. | Dài hơn rõ rệt so với car và van, có dãy cửa sổ đều và cửa lên xuống ở hông. Buýt nối toa vẽ một box. Thường có số tuyến hoặc màu sơn tuyến. |
| `van` | Xe thân hộp cỡ vừa, nóc cao, đầu xe ngắn hoặc gần như phẳng, một khối liền từ đầu đến đuôi. Gồm minivan và van chở hàng hoặc chở người. | Cao hơn car, nắp capo ngắn và không có cốp riêng. Ngắn hơn bus nhiều và chỉ có 1–2 hàng cửa sổ. Phân vân giữa van với car hoặc bus thì ghi tên ảnh vào bảng ca mơ hồ và hỏi giảng viên. |

## Quy tắc chung

- Box bám sát vật thể nghĩa là: Top chạm trần, bot chạm bánh xe, bao gồm cả gương và phần nhòe chuyển động, không tính bóng đổ
- Vật thể bị che khuất: vẫn gán nếu phần nhìn thấy đủ để nhận ra lớp. Box chỉ bao phần nhìn thấy, không đoán phần bị che. Mỗi xe đúng một box, kể cả khi bị xe khác chia làm hai mảnh.
- Vật thể bị cắt bởi rìa ảnh: box chạm đúng rìa ảnh, không kéo dài ra ngoài khung. Chỉ còn một mảnh hẹp ở mép ảnh, không xác định được lớp thì không gán.
- Vật thể rất nhỏ/mơ hồ: xe ở xa vẫn gán nếu còn thấy được hình xe (cạnh ngắn khoảng ≥ 8 px). Nhỏ hơn hoặc nhòe đến mức không chắc là xe hay lớp nào thì không đoán, bỏ qua.
- Xe đỗ bên đường vẫn gán như xe đang chạy (lớp mô tả loại xe, không mô tả trạng thái).
- Không gán: người đi bộ, xe đạp, xe máy, xe ba bánh, nhà chờ xe buýt, lan can, tường hay ống bên lề đường dù model gợi ý là xe.

## Ghi lại quyết định cho ít nhất ba ca mơ hồ

| Ảnh | Tình huống | Quyết định cuối | Lý do theo schema |
| --- | --- | --- | --- |
| `drive_005.jpg`, `drive_006.jpg` | Xe cứu hộ nhìn từ góc cạnh chéo, phần thùng xe không rõ ràng, giống xe Van | Đánh là truck vì mắt thường nhận ra là xe cứu hộ với các đặc điểm như: có rơ móc và đèn cứu hộ | Xe cứu hộ là xe chuyên dụng, có cabin tách khỏi phần cẩu/kéo phía sau, khớp định nghĩa `truck`. |
| `drive_005.jpg`, `drive_006.jpg`, `drive_041.jpg` | Xe thân hộp màu trắng, nóc cao, đầu ngắn; không thấy rõ khe giữa cabin và thùng nên có thể là van chở hàng hoặc xe tải nhỏ thùng kín | Gán `van` (vẫn còn phân vân, cần hỏi giảng viên) | Thân xe là một khối liền từ đầu đến đuôi, không có ranh cabin/thùng như `truck`, kích thước vừa như minivan. |
| `drive_012.jpg` | Xe minibus màu be chở khách, ngắn hơn xe buýt thành phố nhưng dài hơn van | Gán `bus` | Có dãy cửa sổ chạy dọc thân và cửa khách ở hông; định nghĩa `bus` đã gồm minibus chở khách. |
| `drive_029.jpg` | Xe buýt lớn ở góc dưới phải bị rìa ảnh cắt mất phần lớn thân | Gán `bus`, box chạm rìa phải và rìa dưới | Phần còn thấy (nóc dài có cục điều hòa, dãy cửa sổ dọc thân, cửa lên xuống ở hông) đủ nhận ra là bus; theo quy tắc cắt khung thì không đoán phần ngoài ảnh. |
| Nhiều ảnh (vd. `drive_008.jpg`, `drive_024.jpg`) | Minivan/MPV màu tối nhìn từ trên cao, dễ nhầm với SUV | Gán `van` khi nóc cao và đầu xe ngắn rõ; nếu có capo dài kiểu SUV thì gán `car` | Phân biệt theo hình dáng: van là một khối liền, đầu ngắn; car có capo nhô ra. |
