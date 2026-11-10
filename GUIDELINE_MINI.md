# Mini guideline — bài làm cá nhân

## Định nghĩa lớp

| Lớp | Định nghĩa của bạn | Ví dụ/điểm phân biệt |
|---|---|---|
| car (0) | Xe con chở người cỡ nhỏ: sedan, hatchback, SUV, taxi và xe bán tải (cabin nhỏ). | Thân thấp hơn van, không có thùng hàng cao như xe tải. Xe bán tải vẫn là car. |
| truck (1) | Xe tải chở hàng và xe đầu kéo: có thùng hàng rời hoặc cabin tách biệt với thùng. | Thân cao, dài, có thùng chở hàng. Xe bán tải/cabin nhỏ không thuộc truck. |
| bus (2) | Xe buýt và minibus chở khách: thân dài, nhiều cửa sổ dọc thân. | Dài và cao hơn van, hàng cửa sổ liền dọc thân xe. |
| van (3) | Xe van và minivan chở hàng hoặc chở người: thân hộp liền khối, cỡ giữa car và bus. | Thân vuông, nóc cao, thường không có phần đầu xe nhô ra như car; nhỏ hơn bus. |

## Quy tắc chung

- Box bám sát vật thể nghĩa là: cạnh box chạm vào phần ngoài cùng nhìn thấy được của xe (nóc, đuôi, đầu, bánh), không chừa nhiều nền và không cắt mất một phần xe. Mỗi xe một box riêng.
- Vật thể bị che khuất: nếu phần nhìn thấy đủ để nhận ra loại xe thì vẽ box quanh phần nhìn thấy và gán lớp theo loại xe; nếu chỉ thấy một mảnh nhỏ không đủ nhận ra lớp thì không gán.
- Vật thể bị cắt bởi rìa ảnh: vẽ box quanh phần nhìn thấy, kéo sát tới rìa ảnh; chỉ gán khi phần còn lại đủ để nhận ra lớp.
- Vật thể rất nhỏ/mơ hồ: chỉ gán khi còn nhìn rõ loại xe; xe ở quá xa, quá nhỏ hoặc mờ đến mức không phân biệt được lớp thì bỏ, và áp dụng cùng một ngưỡng cho cả 50 ảnh.
- Trạng thái xe (đang chạy hay đỗ) không ảnh hưởng đến lớp: xe đỗ vẫn gán theo loại xe.

## Ghi lại quyết định cho ít nhất ba ca mơ hồ

| Ảnh | Tình huống | Quyết định cuối | Lý do theo schema |
|---|---|---|---|
| ⟨drive_007⟩ | Xe bán tải (cabin nhỏ, có thùng phía sau), dễ nhầm với truck | Gán car (0) | Schema ghi xe bán tải/cabin nhỏ thuộc car, truck chỉ dành cho xe tải chở hàng và xe đầu kéo |
| ⟨drive_030⟩ | Xe cỡ giữa, thân hộp, không rõ là van hay minibus | Gán van (3) nếu nhỏ, thân liền khối; gán bus (2) nếu dài, có hàng cửa sổ dọc thân | Schema: bus là xe buýt/minibus chở khách, van là xe van/minivan; xe van lớn không được gán bus |
| ⟨drive_041⟩ | Xe ở xa hoặc bị xe khác che gần hết, chỉ thấy một phần nhỏ | Bỏ không gán nếu không nhận ra được lớp; vẽ box quanh phần nhìn thấy nếu còn đủ nhận ra | Lớp mô tả loại vật thể; chỉ gán khi phần nhìn thấy đủ để xác định lớp |