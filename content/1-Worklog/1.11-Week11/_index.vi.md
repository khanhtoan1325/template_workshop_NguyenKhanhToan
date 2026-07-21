---
title: "Worklog Tuần 11"
date: "2026-06-26"
weight: 11
chapter: false
pre: " <b> 1.11. </b> "
---

### Mục tiêu tuần 11:
* Tìm hiểu giải pháp giám sát Amazon CloudWatch (Metrics, Logs, Alarms).
* Tìm hiểu công cụ quản lý hạ tầng bằng mã (Infrastructure as Code) AWS CloudFormation.
* Tiếp tục phối hợp và triển khai các hạng mục của dự án nhóm.

### Các công việc cần triển khai trong tuần này:
| Thứ | Công việc | Ngày bắt đầu | Ngày hoàn thành | Nguồn tài liệu |
| --- | --- | --- | --- | --- |
| 6 | - **Amazon CloudWatch** <br> - Tìm hiểu CloudWatch Metrics <br> - Tìm hiểu CloudWatch Logs <br> - Tìm hiểu CloudWatch Alarm <br> - Ghi chú vai trò monitoring hệ thống | 26/06/2026 | 26/06/2026 | <https://cloudjourney.awsstudygroup.com/> |
| 2 | - **Dự Án Nhóm**<br>- Tích hợp Remotion Player vào giao diện xem trước video (cấu hình canvas 1080x1920 (9:16), 30fps)<br>- Kết nối playerRef vào Zustand store để các component khác có thể gọi play/pause/seekTo<br>- Tích hợp @designcombo/timeline: drag-drop track, zoom, scroll timeline<br>- Xử lý sự kiện timeline qua @designcombo/events (RxJS-like): PLAYER_PLAY, PLAYER_PAUSE, PLAYER_SEEK, TIMELINE_SEEK<br>- Thêm phím tắt: L (lock timeline), P (lock player), F (fullscreen)<br>- Tích hợp getVideoMetadata() tính duration video tự động | 29/06/2026 | 29/06/2026 | <https://www.remotion.dev/>|
| 3 | - **AWS CloudFormation** <br> - Tìm hiểu Infrastructure as Code <br> - Tìm hiểu CloudFormation Template <br> - Ghi chú các thành phần Resources, Parameters, Outputs <br> - Mô tả lợi ích tự động hóa hạ tầng | 30/06/2026 | 30/06/2026 | <https://cloudjourney.awsstudygroup.com/> |
| 4 | - **Dự Án Nhóm**<br>- Amazon RDS MySQL – Cơ sở dữ liệu cho hệ thống<br>- Tạo RDS instance MySQL tại region ap-southeast-2<br>- Cấu hình Security Group cho phép EC2 kết nối qua port 3306<br>- Tạo database db_sub_video, tạo user và phân quyền đầy đủ<br>- Kết nối Backend (SQLAlchemy) với endpoint RDS<br>- Cấu hình connection pool: pool_recycle=3600, pool_pre_ping=True<br>- Kiểm tra public/private access, tắt public access để đảm bảo bảo mật | 01/07/2026 | 01/07/2026 |<https://cloudjourney.awsstudygroup.com/> |

### Kết quả đạt được tuần 11:
* Hiểu cơ chế giám sát tài nguyên thông qua CloudWatch Metrics, Alarms gửi thông báo và thu thập Log từ EC2.
* Tìm hiểu cấu trúc Template YAML/JSON của AWS CloudFormation để tự động khởi tạo hạ tầng.
* Triển khai các tính năng then chốt của dự án nhóm đúng theo kế hoạch đã phân chia.