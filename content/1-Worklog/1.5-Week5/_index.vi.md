---
title: "Worklog Tuần 5"
date: "2026-05-15"
weight: 5
chapter: false
pre: " <b> 1.5. </b> "
---

### Mục tiêu tuần 5:
* Tìm hiểu và cấu hình các lớp bảo mật mạng: Security Group và Network ACL.
* Tìm hiểu cơ chế hoạt động và triển khai NAT Gateway cho Private Subnet.
* Đánh giá bảo mật và thiết kế kiến trúc VPC tổng hợp.

### Các công việc cần triển khai trong tuần này:
| Thứ | Công việc | Ngày bắt đầu | Ngày hoàn thành | Nguồn tài liệu |
| --- | --- | --- | --- | --- |
| 6 | - **Security Group** <br> - Tìm hiểu Security Group <br> - Phân biệt inbound rule và outbound rule <br> - Ghi chú cách mở port HTTP, HTTPS, SSH <br> - Tìm hiểu stateful firewall | 15/05/2026 | 15/05/2026 | <https://cloudjourney.awsstudygroup.com/> |
| 2 | - **Network ACL** <br> - Tìm hiểu Network ACL <br> - Phân biệt Network ACL và Security Group <br> - Ghi chú inbound/outbound rule ở cấp subnet <br> - Tìm hiểu stateless firewall | 18/05/2026 | 18/05/2026 | <https://cloudjourney.awsstudygroup.com/> |
| 3 | - **NAT Gateway** <br> - Tìm hiểu NAT Gateway <br> - Ghi chú cách private subnet truy cập Internet <br> - Phân biệt NAT Gateway và Internet Gateway <br> - Cập nhật sơ đồ private subnet | 19/05/2026 | 19/05/2026 | <https://cloudjourney.awsstudygroup.com/> |
| 4 | - **VPC Security Review** <br> - Tổng hợp VPC, Subnet, Route Table, Internet Gateway, NAT Gateway <br> - Tổng hợp Security Group và Network ACL <br> - So sánh public/private architecture <br> - Chuẩn bị phần minh chứng networking cho báo cáo | 20/05/2026 | 20/05/2026 | <https://cloudjourney.awsstudygroup.com/> |

### Kết quả đạt được tuần 5:
* Phân biệt rõ sự khác nhau giữa Security Group (tác động ở cấp EC2 instance, stateful) và Network ACL (tác động ở cấp subnet, stateless).
* Cấu hình inbound/outbound rule để chặn/cho phép lưu lượng (ví dụ mở SSH port 22, HTTP port 80).
* Triển khai thành công NAT Gateway giúp máy chủ trong Private Subnet tải cập nhật phần mềm an toàn từ Internet.
* Hoàn thiện tài liệu kiến trúc mạng bảo mật VPC cho báo cáo thực tập.