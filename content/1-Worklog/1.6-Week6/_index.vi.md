---
title: "Worklog Tuần 6"
date: "2026-05-22"
weight: 6
chapter: false
pre: " <b> 1.6. </b> "
---

### Mục tiêu tuần 6:
* Tìm hiểu cơ chế hoạt động của VPC Endpoint để kết nối riêng tư với dịch vụ AWS.
* Thiết lập Gateway Endpoint để kết nối Private Subnet với Amazon S3.
* Tìm hiểu Interface Endpoint (AWS PrivateLink) và thiết kế sơ đồ mạng VPC nâng cao.

### Các công việc cần triển khai trong tuần này:
| Thứ | Công việc | Ngày bắt đầu | Ngày hoàn thành | Nguồn tài liệu |
| --- | --- | --- | --- | --- |
| 6 | - **VPC Endpoint** <br> - Tìm hiểu VPC Endpoint <br> - Ghi chú lợi ích khi truy cập AWS service qua mạng private <br> - Phân biệt Gateway Endpoint và Interface Endpoint <br> - Liên hệ với service Amazon S3 | 22/05/2026 | 22/05/2026 | <https://cloudjourney.awsstudygroup.com/> |
| 2 | - **Gateway Endpoint for S3** <br> - Tìm hiểu Gateway Endpoint <br> - Ghi chú cách truy cập S3 từ private subnet <br> - Tìm hiểu endpoint policy <br> - Mô tả luồng truy cập S3 không qua Internet | 25/05/2026 | 25/05/2026 | <https://cloudjourney.awsstudygroup.com/> |
| 3 | - **Interface Endpoint / AWS PrivateLink** <br> - Tìm hiểu Interface Endpoint <br> - Tìm hiểu AWS PrivateLink <br> - Ghi chú sự khác nhau với Gateway Endpoint <br> - Mô tả trường hợp dùng trong hybrid access | 26/05/2026 | 26/05/2026 | <https://cloudjourney.awsstudygroup.com/> |
| 4 | - **VPC Diagram & Documentation** <br> - Vẽ sơ đồ tổng hợp VPC Endpoint <br> - Ghi chú luồng truy cập S3 private <br> - Tổng hợp kiến thức VPC nâng cao <br> - Chuẩn bị nội dung cho phần workshop/báo cáo | 27/05/2026 | 27/05/2026 | <https://cloudjourney.awsstudygroup.com/> |

### Kết quả đạt được tuần 6:
* Hiểu cơ chế hoạt động của VPC Endpoints trong việc định tuyến lưu lượng nội bộ mà không đi qua Internet Public.
* Cấu hình thành công Gateway Endpoint cho Amazon S3 và thiết lập Endpoint Policy để giới hạn truy cập.
* Nắm vững kiến thức về Interface Endpoint sử dụng công nghệ AWS PrivateLink và trường hợp áp dụng cho Hybrid Network (On-premise kết nối đám mây).
* Hoàn thiện sơ đồ định tuyến private kết nối S3 phục vụ minh chứng cho bài báo cáo.