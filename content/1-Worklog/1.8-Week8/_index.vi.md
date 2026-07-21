---
title: "Worklog Tuần 8"
date: "2026-06-23"
weight: 8
chapter: false
pre: " <b> 1.8. </b> "
---

### Mục tiêu tuần 8:
* Tìm hiểu ổ lưu trữ khối Amazon EBS và các loại volume.
* Thực hành tạo snapshot để sao lưu và phục hồi dữ liệu EBS volume.
* Cấp phát Elastic IP phục vụ IP tĩnh cho EC2 và review toàn bộ bảo mật máy chủ.

### Các công việc cần triển khai trong tuần này:
| Thứ | Công việc | Ngày bắt đầu | Ngày hoàn thành | Nguồn tài liệu |
| --- | --- | --- | --- | --- |
| 3 | - **EBS Volume** <br> - Tìm hiểu Elastic Block Store <br> - Ghi chú vai trò ổ đĩa gắn với EC2 <br> - Phân biệt root volume và additional volume <br> - Tìm hiểu các loại EBS cơ bản | 23/06/2026 | 23/06/2026 | <https://cloudjourney.awsstudygroup.com/> |
| 4 | - **EBS Snapshot** <br> - Tìm hiểu snapshot <br> - Ghi chú cách backup dữ liệu EC2 <br> - Phân biệt volume và snapshot <br> - Tìm hiểu cách phục hồi từ snapshot | 24/06/2026 | 24/06/2026 | <https://cloudjourney.awsstudygroup.com/> |
| 5 | - **Elastic IP** <br> - Tìm hiểu Elastic IP <br> - Ghi chú khi nào cần IP tĩnh <br> - Tìm hiểu rủi ro phát sinh phí nếu không dùng <br> - Ghi chú cách release Elastic IP | 25/06/2026 | 25/06/2026 | <https://cloudjourney.awsstudygroup.com/> |
| 6 | - **EC2 Review & Backup** <br> - Tổng hợp EC2, AMI, Instance Type, Key Pair <br> - Tổng hợp EBS, Snapshot, Elastic IP <br> - Ghi chú checklist bảo mật EC2 <br> - Chuẩn bị nội dung compute cho báo cáo | 26/06/2026 | 26/06/2026 | <https://cloudjourney.awsstudygroup.com/> |

### Kết quả đạt được tuần 8:
* Nắm vững cơ chế hoạt động của EBS Root Volume và Additional EBS Volume.
* Tạo lập EBS Snapshot thành công phục vụ sao lưu định kỳ, kiểm thử khôi phục thành công dữ liệu từ Snapshot lên EC2.
* Hiểu rõ cơ chế tính phí của Elastic IP (bị tính phí khi không gắn vào EC2 chạy) và biết cách thu hồi (release) địa chỉ IP tĩnh.
* Tổng hợp hoàn thiện checklist bảo mật và sao lưu dữ liệu máy chủ EC2.
