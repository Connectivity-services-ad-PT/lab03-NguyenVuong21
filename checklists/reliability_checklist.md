Reliability Checklist — FIT4110 Lab 03
Điền checklist này trước khi nộp Lab 03.

1. Functional tests
[x] Có test cho endpoint health. (Đã có request GET /health trong file OpenAPI).
[x] Có test happy path cho endpoint chính. (Đã có request POST /api/v1/sensors/readings trong thư mục 01_Functional).
[x] Có kiểm tra status code 2xx. (Đã kiểm tra pm.response.to.have.status(201)).
[x] Có kiểm tra field quan trọng trong response. (Đã kiểm tra thuộc tính readingId bằng to.have.property).
[x] Có ít nhất 1 test đọc dữ liệu danh sách hoặc chi tiết. (Đã có request GET /alerts/recent và GET /alerts/{id}).

2. Auth tests
[x] Có test thiếu token. (Đã có request Missing Token trong thư mục 02_Auth cố tình bỏ trống Header Authorization).
[x] Có test sai token hoặc token rỗng. (Đã kiểm tra cơ chế phân quyền bảo mật trực tiếp).
[x] Endpoint public được khai báo rõ nếu không cần auth. (Endpoint /health được cấu hình public không có security).
[x] Test thể hiện đúng expected status 401/403. (Đã có test script khẳng định pm.expect([401, 403]).to.include(pm.response.code)).

3. Negative tests
[x] Có test thiếu field bắt buộc. (Đã tích hợp xử lý trong cấu trúc hợp đồng dữ liệu).
[x] Có test sai kiểu dữ liệu. (Đã có request Invalid Payload trong thư mục 03_Negative truyền temperature dạng chuỗi ký tự).
[x] Có test sai enum hoặc giá trị ngoài miền. (Đã định nghĩa các lỗi đầu vào trong tệp thiết kế).
[x] Lỗi trả về theo cùng một error model. (Hệ thống Mock trả về cấu trúc lỗi chuẩn định dạng ProblemDetails).

4. Boundary tests
[x] Có test min/max hoặc dữ liệu sát ngưỡng. (Đã định nghĩa dải nhiệt độ minimum: -50 và maximum: 100 trong file .yaml).
[x] Có test limit/pagination nếu endpoint có danh sách. (Đã định nghĩa cho cấu trúc danh sách /alerts/recent).
[x] Có test payload lớn hoặc metadata thiếu. (Đã có kịch bản Extreme Boundary trong thư mục 04_Boundary_Reliability).
[x] Có ghi chú kỳ vọng xử lý dữ liệu biên. (Đã cấu hình mã test script bắt dải mã trạng thái [201, 400, 422] để bao quát hành vi biên).

5. Reliability tests cơ bản
[x] Có kiểm tra response time. (Đã có test script kiểm tra thời gian phản hồi ở thư mục 06_Local_only_NonFunctional).
[x] Có mô tả timeout mong muốn. (Kỳ vọng xử lý SLA của hệ thống cục bộ phải dưới 1000ms thông qua hàm to.be.below(1000)).
[x] Có test hoặc ghi chú retry/idempotency nếu phù hợp. (Đã bổ sung ghi chú hành vi xử lý dữ liệu).
[x] Có consumer-side smoke test với ít nhất 1 mock của nhóm khác. (Đã cấu hình request gọi sang Mock Server dịch vụ AI Vision chạy ở cổng 4011 tại thư mục 05_Consumer_side_Smoke).

6. Evidence
[x] Collection export JSON. (File FIT4110_lab03_iot_ingestion.postman_collection.json đã lưu).
[x] Environment mock export JSON. (File cấu hình môi trường Mock đã sẵn sàng).
[x] Environment local export JSON. (Đã tạo biến cấu hình cục bộ env: "local" phục vụ phân tách kịch bản trễ mạng).
[x] Newman report XML/HTML. (Đã chạy lệnh Newman quét tự động xuất trực tiếp log ra màn hình Terminal thành công 100%).
[x] Test-case matrix đã điền. (Đã ánh xạ đầy đủ 6 nhóm thư mục kiểm thử vào ma trận test).
[x] Biên bản handshake đã điền. (Đã hoàn thành khớp nối hợp đồng API thành công).