---
title: "Worklog Tuần 7"
date: "2026-05-29"
weight: 7
chapter: false
pre: " <b> 1.7. </b> "
---

### Mục tiêu tuần 7:
* Tìm hiểu dịch vụ máy chủ ảo Amazon EC2 và các thuộc tính liên quan (Instance Types, AMIs).
* Thực hành tạo và kết nối SSH bảo mật vào EC2 thông qua Key Pair.
* Tìm hiểu cấu hình Security Group bảo vệ máy chủ EC2.

### Các công việc cần triển khai trong tuần này:
| Thứ | Công việc | Ngày bắt đầu | Ngày hoàn thành | Nguồn tài liệu |
| --- | --- | --- | --- | --- |
| 6 | - **Amazon EC2** <br> - Tìm hiểu EC2 là gì <br> - Ghi chú vai trò của máy chủ ảo trên AWS <br> - Tìm hiểu Instance Type <br> - Tìm hiểu trạng thái EC2 instance | 29/05/2026 | 29/05/2026 | <https://cloudjourney.awsstudygroup.com/> |
| 2 | - **AMI & Instance Type** <br> - Tìm hiểu Amazon Machine Image <br> - Phân biệt Amazon Linux, Ubuntu, Windows Server <br> - Tìm hiểu CPU, RAM, storage của instance type <br> - Ghi chú cách chọn instance phù hợp | 01/06/2026 | 01/06/2026 | <https://cloudjourney.awsstudygroup.com/> |
| 3 | - **Key Pair & SSH** <br> - Tìm hiểu Key Pair <br> - Ghi chú public key/private key <br> - Tìm hiểu cách SSH vào EC2 <br> - Ghi chú các lỗi thường gặp khi SSH | 02/06/2026 | 02/06/2026 | <https://cloudjourney.awsstudygroup.com/> |
| 4 | - **EC2 Security Group** <br> - Cấu hình rule SSH/HTTP/HTTPS cho EC2 <br> - Ghi chú nguyên tắc không mở port bừa bãi <br> - Tìm hiểu public IP và private IP <br> - Tổng hợp quy trình tạo EC2 an toàn | 03/06/2026 | 03/06/2026 | <https://cloudjourney.awsstudygroup.com/> |

### Kết quả đạt được tuần 7:
* Khởi tạo thành công máy chủ ảo EC2 với hệ điều hành Amazon Linux / Ubuntu phù hợp.
* Nắm vững cơ chế mật mã hóa khóa công khai (Key Pair) để thiết lập kết nối SSH từ xa.
* Biết cách khắc phục các lỗi phân quyền SSH key (như lỗi chmod 400).
* Thiết lập Security Group bảo mật cho EC2 chỉ mở các port dịch vụ cần thiết (SSH port 22, HTTP port 80).