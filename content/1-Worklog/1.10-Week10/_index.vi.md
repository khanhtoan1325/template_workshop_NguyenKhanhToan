---
title: "Worklog Tuần 10"
date: "2026-06-19"
weight: 10
chapter: false
pre: " <b> 1.10. </b> "
---

### Mục tiêu tuần 10:
* Tìm hiểu dịch vụ cơ sở dữ liệu quan hệ Amazon RDS và so sánh với cơ sở dữ liệu tự quản trị.
* Thực hành tạo cơ sở dữ liệu RDS MySQL, cấu hình bảo mật Security Group và kiểm tra kết nối.
* Bắt đầu triển khai dự án nhóm.

### Các công việc cần triển khai trong tuần này:
| Thứ | Công việc | Ngày bắt đầu | Ngày hoàn thành | Nguồn tài liệu |
| --- | --- | --- | --- | --- |
| 6 | - **Amazon RDS** <br> - Tìm hiểu Relational Database Service <br> - Ghi chú lợi ích managed database <br> - Phân biệt RDS và database tự cài trên EC2 <br> - Tìm hiểu các engine: MySQL, PostgreSQL, MariaDB | 19/06/2026 | 19/06/2026 | <https://cloudjourney.awsstudygroup.com/> |
| 2 | - **RDS MySQL** <br> - Tìm hiểu endpoint, port, username, password <br> - Ghi chú cách kết nối RDS từ bên ngoài <br> - Tìm hiểu Security Group cho database <br> - Phân tích public/private access cho RDS | 22/06/2026 | 22/06/2026 | <https://cloudjourney.awsstudygroup.com/> |
| 3 | - **RDS Backup & Security** <br> - Tìm hiểu automated backup <br> - Tìm hiểu snapshot database <br> - Ghi chú Multi-AZ ở mức cơ bản <br> - Tổng hợp checklist bảo mật database | 23/06/2026 | 23/06/2026 | <https://cloudjourney.awsstudygroup.com/> |
| 4 | - **Dự Án Nhóm**<br>- Xây dựng layout Editor chính cho ứng dụng<br>- Thiết kế layout 4 vùng: MenuList (sidebar), MenuItem (panel), Scene (player), Timeline (dòng thời gian)<br>- Tích hợp react-resizable-panels cho phép kéo thay đổi kích thước<br>- Xây dựng Navbar: tên video, resize canvas (16:9 / 9:16 / 1:1), dropdown user menu, nút download<br>- Xây dựng MenuList sidebar 9 icon: Upload, Subtitle, Dubbing, Render, Audio, Logo, Settings, User<br>- Cấu hình React Router v6: route /, /auth, /auth/register | 24/06/2026 | 24/06/2026 | <https://www.remotion.dev/> <br> <https://ui.shadcn.com/> |

### Kết quả đạt được tuần 10:
* Hiểu rõ ưu thế vận hành của RDS (tự động backup, vá lỗi bảo mật) so với cài database trên EC2.
* Khởi tạo thành công database RDS MySQL, liên kết Security Group chỉ cho phép kết nối đến từ các subnet được chỉ định.
* Thiết lập cơ chế sao lưu tự động và tạo snapshots cho cơ sở dữ liệu.
* Làm việc nhóm để phân công các task đầu tiên cho dự án nhóm.