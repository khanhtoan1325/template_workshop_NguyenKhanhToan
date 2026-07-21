---
title: "Worklog Tuần 9"
date: "2026-06-30"
weight: 9
chapter: false
pre: " <b> 1.9. </b> "
---

### Mục tiêu tuần 9:
* Tìm hiểu dịch vụ lưu trữ đối tượng Amazon S3 (Buckets, Objects).
* Thiết lập phân quyền dữ liệu qua Block Public Access, Bucket Policies và IAM Policies.
* Triển khai lưu trữ website tĩnh (Static Website Hosting) trên Amazon S3.
* Tìm hiểu cấu hình CORS và Lifecycle Rules trên S3.

### Các công việc cần triển khai trong tuần này:
| Thứ | Công việc | Ngày bắt đầu | Ngày hoàn thành | Nguồn tài liệu |
| --- | --- | --- | --- | --- |
| 3 | - **Amazon S3** <br> - Tìm hiểu Bucket và Object <br> - Ghi chú cách lưu trữ dữ liệu trên S3 <br> - Tìm hiểu Region của bucket <br> - Phân biệt object storage và block storage | 30/06/2026 | 30/06/2026 | <https://cloudjourney.awsstudygroup.com/> |
| 4 | - **S3 Permission** <br> - Tìm hiểu Block Public Access <br> - Tìm hiểu Bucket Policy <br> - Ghi chú IAM Policy liên quan đến S3 <br> - Phân tích quyền public/private cho bucket | 01/07/2026 | 01/07/2026 | <https://cloudjourney.awsstudygroup.com/> |
| 5 | - **S3 Static Website Hosting** <br> - Tìm hiểu hosting website tĩnh bằng S3 <br> - Ghi chú index document và error document <br> - Tìm hiểu public access khi host website <br> - Chuẩn bị nội dung mô tả static hosting | 02/07/2026 | 02/07/2026 | <https://cloudjourney.awsstudygroup.com/> |
| 6 | - **S3 CORS & Lifecycle** <br> - Tìm hiểu CORS trên S3 <br> - Ghi chú use case frontend gọi file từ bucket <br> - Tìm hiểu Lifecycle rule <br> - Tổng hợp kiến thức S3 cho báo cáo | 03/07/2026 | 03/07/2026 | <https://cloudjourney.awsstudygroup.com/> |

### Kết quả đạt được tuần 9:
* Khởi tạo thành công S3 Bucket và hiểu rõ sự khác biệt giữa Object Storage và Block Storage (EBS).
* Cấu hình Block Public Access kết hợp Bucket Policy để giới hạn truy cập dữ liệu an toàn.
* Triển khai thành công website tĩnh chạy trực tiếp trên S3, thiết lập đúng index và error documents.
* Thiết lập Lifecycle Rules tự động hóa lưu chuyển/xóa dữ liệu cũ để tối ưu chi phí S3.
