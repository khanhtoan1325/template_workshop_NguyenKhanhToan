---
title: "Event 2"
date: 2026-06-27
weight: 2
chapter: false
pre: " <b> 4.1. </b> "
---

# Bài thu hoạch: “Cloud, AI Agent và Amazon Q trên AWS”

### Mục Đích Của Sự Kiện

- Chia sẻ kiến thức thực tế về Cloud Computing, AI Agent, DevOps AI và bảo mật hệ thống trên AWS.
- Giới thiệu các hướng ứng dụng Generative AI trong doanh nghiệp như trợ lý giọng nói, tự động hóa DevOps và quản trị nhân sự.
- Trình bày cách các dịch vụ AWS như Amazon Bedrock, Amazon Q, Amazon ECS, VPC, Interface Endpoint, Route 53 Resolver và Application Load Balancer hỗ trợ xây dựng hệ thống AI hiện đại.
- Giúp người tham dự hiểu rõ hơn về xu hướng kết hợp giữa Cloud, AI và Automation trong quá trình phát triển, vận hành và bảo mật hệ thống.
- Định hướng cho sinh viên và developer cách phát triển kỹ năng phù hợp với thị trường IT/Cloud trong thời đại AI.

### Danh Sách Diễn Giả

- **Steve Trần** – Founder của Cloud Thinker  
  Chủ đề: *Con đường sự nghiệp với Cloud và giới thiệu Cloud Thinker*

- **Hiếu Nghị** – Renova Cloud  
  Chủ đề: *Xây dựng trợ lý giọng nói bằng AI*

- **Kiệt** – AWS Study Group  
  Chủ đề: *Voice Agent và ứng dụng AI trên AWS*

- **Trung Nguyễn** – Founder & CEO của R AI  
  Chủ đề: *Triển khai Voice AI cho tiếng Việt*

- **Bảo** – Cloud Kinetic  
  Chủ đề: *Tìm hiểu về AWS DevOps AI Agent*

- **Nguyên Nguyễn** – Cloud Engineer, Cloud Kinetic  
  Chủ đề: *DevOps AI Agent và xử lý incident trên AWS*

- **Trường** – Solution Architect, Noventic  
  Chủ đề: *Ứng dụng Amazon Q trong quản trị nhân sự*

- **Minh Anh** – Solution Architect, Noventic  
  Chủ đề: *Amazon Q và tự động hóa quy trình HR*

- **Toàn Nguyễn** – AWS Security Builder  
  Chủ đề: *Thiết lập bảo mật cho Amazon Q với Private Connection*

### Nội Dung Nổi Bật

#### Con Đường Sự Nghiệp Với Cloud Và Giới Thiệu Cloud Thinker

Session đầu tiên do anh Steve Trần trình bày, tập trung vào hành trình phát triển sự nghiệp trong lĩnh vực Cloud. Anh chia sẻ quá trình bắt đầu học Cloud, từng thi trượt chứng chỉ Azure, sau đó chuyển hướng sang AWS, trở thành Solution Architect tại AWS Việt Nam và thành lập startup Cloud Thinker.

Các ý chính bao gồm:

- Việc học Cloud là một hành trình dài, cần sự kiên trì và khả năng học hỏi liên tục.
- Thất bại khi học hoặc thi chứng chỉ không phải là điểm kết thúc, mà là kinh nghiệm để tiếp tục phát triển.
- AI đang thay đổi cách lập trình viên viết code, vận hành hệ thống và xử lý công việc hằng ngày.
- AI có thể hỗ trợ tăng tốc độ coding nhưng chưa thể thay thế hoàn toàn con người trong các hệ thống critical.
- Doanh nghiệp vẫn cần những kỹ sư có nền tảng kỹ thuật vững và biết cách ứng dụng AI hiệu quả.

Ngoài ra, diễn giả cũng giới thiệu nền tảng **Agentic Platform** của Cloud Thinker. Nền tảng này hướng đến việc sử dụng AI Agent để hỗ trợ các bài toán như xử lý sự cố hệ thống, review code trước khi đưa lên production, tối ưu chi phí Cloud theo hướng FinOps và kiểm thử bảo mật.

Một nội dung đáng chú ý khác là sự khác nhau giữa kiến trúc **Single Agent** và **Multi-Agent**. Single Agent phù hợp với các tác vụ đơn giản, trong khi Multi-Agent giúp chia nhỏ nhiệm vụ, quản lý context tốt hơn và tối ưu chi phí vận hành mô hình AI.

#### Xây Dựng Trợ Lý Giọng Nói Bằng AI

Session này giới thiệu cách xây dựng một hệ thống **Voice Agent** sử dụng AI. Kiến trúc Voice AI thông thường gồm ba thành phần chính: **Speech-to-Text**, **LLM** và **Text-to-Speech**.

Quy trình hoạt động cơ bản như sau:

- Người dùng nói vào hệ thống.
- Speech-to-Text chuyển giọng nói thành văn bản.
- LLM xử lý nội dung và tạo câu trả lời.
- Text-to-Speech chuyển câu trả lời thành giọng nói để phản hồi lại người dùng.

Trong phần demo, hệ thống Voice Agent được dùng để trả lời thông tin về sản phẩm Apple, cụ thể là MacBook Pro. Demo được triển khai trên hạ tầng AWS Bedrock, giúp người tham dự hình dung rõ hơn cách AI có thể được ứng dụng trong chăm sóc khách hàng, tư vấn sản phẩm và tự động hóa giao tiếp bằng giọng nói.

Các thách thức nổi bật khi triển khai Voice AI cho tiếng Việt bao gồm:

- Tiếng Việt là ngôn ngữ ít tài nguyên hơn so với tiếng Anh.
- Cần xử lý độ trễ thấp bằng cơ chế streaming dữ liệu thời gian thực.
- Hệ thống cần nhận diện giới tính để xưng hô phù hợp như anh, chị.
- AI cần hiểu khi nào nên ngắt lời, khi nào nên giữ im lặng để cuộc hội thoại tự nhiên hơn.
- Cần xử lý tốt sự khác biệt về giọng nói theo vùng miền.
- Cần có cơ chế chuyển tiếp sang nhân viên thật khi AI không xử lý được yêu cầu.

Điểm quan trọng của session này là mô hình **Human-in-the-loop**. Khi AI bị quá tải, trả lời chưa tốt hoặc khách hàng không hài lòng, hệ thống có thể chuyển cuộc gọi sang nhân viên hỗ trợ một cách mượt mà. Điều này cho thấy AI nên được thiết kế để phối hợp với con người, thay vì hoạt động hoàn toàn độc lập.

#### Tìm Hiểu Về AWS DevOps AI Agent

Session này tập trung vào bài toán vận hành hệ thống và xử lý sự cố trong môi trường Cloud. Trước đây, khi hệ thống gặp lỗi, kỹ sư DevOps phải tự kiểm tra nhiều nguồn dữ liệu như log, metric, dashboard và cảnh báo. Quá trình tìm nguyên nhân gốc rễ thường tốn nhiều thời gian, nhất là với các hệ thống lớn và phân tán.

Giải pháp **DevOps AI Agent** được giới thiệu nhằm tự động hóa quá trình điều tra incident. Công cụ này giúp kỹ sư nhanh chóng phân tích tình trạng hệ thống, xác định nguyên nhân có thể xảy ra và đề xuất hướng khắc phục.

Các trụ cột chính của DevOps AI Agent bao gồm:

- **Context Learning**: học và hiểu ngữ cảnh của hệ thống.
- **Control**: đảm bảo con người vẫn có quyền kiểm soát quyết định cuối cùng.
- **Integration**: tích hợp với các công cụ thông qua MCP tool.
- **Collaboration**: hỗ trợ cộng tác qua Slack, ServiceNow và các nền tảng vận hành.
- **Convenient**: giúp kỹ sư thao tác thuận tiện hơn trong quá trình xử lý sự cố.
- **Cost-effective**: tối ưu chi phí bằng cách tính theo thời gian chạy thực tế.

Trong phần live demo, diễn giả giả lập một cuộc tấn công từ chối dịch vụ vào ứng dụng thương mại điện tử chạy trên AWS ECS. Khi ứng dụng bị chậm nghiêm trọng, DevOps AI Agent đã phân tích dữ liệu, tìm ra nguyên nhân và đưa ra kế hoạch khắc phục trong vài phút.

Bài học quan trọng từ session này là AI Agent chỉ hoạt động hiệu quả khi hệ thống có **Good Observability**, tức là phải có đầy đủ log, metric và thông tin giám sát. AI không thay thế kỹ sư DevOps mà đóng vai trò hỗ trợ, giúp tăng tốc quá trình điều tra và xử lý sự cố.

#### Ứng Dụng Amazon Q Trong Quản Trị Nhân Sự

Session này trình bày cách ứng dụng **Amazon Q** vào lĩnh vực quản trị nhân sự. Bộ phận HR thường gặp nhiều khó khăn như lọc CV thủ công, viết mô tả công việc mất thời gian, đánh giá ứng viên dựa trên cảm tính và lo ngại rủi ro bảo mật khi đưa dữ liệu nội bộ lên các công cụ AI công cộng.

Amazon Q được giới thiệu như một trợ lý AI dành cho doanh nghiệp, có khả năng kết nối với nhiều nguồn dữ liệu khác nhau như SharePoint, OneDrive, Google Drive, GitHub, Jira và Amazon S3. Nhờ các Action Connectors và MCP, Amazon Q có thể hỗ trợ truy xuất, phân tích và tự động hóa quy trình làm việc dựa trên dữ liệu nội bộ.

Trong phần demo, Amazon Q được sử dụng để:

- Tự động soạn thảo bản mô tả công việc cho vị trí Junior Cloud Engineer.
- Kích hoạt kỹ năng **HR Talent Review Assistant** để quét thư mục chứa CV ứng viên.
- Phân tích CV dựa trên các tiêu chí như technical skill và communication.
- Chấm điểm và phân loại ứng viên theo kết quả Pass hoặc Reject.
- Xuất báo cáo trực quan dưới dạng file HTML.
- Đồng bộ quy trình tuyển dụng lên một ứng dụng pipeline tracking được xây dựng bằng No-code/Low-code.

Session này cho thấy AI có thể hỗ trợ HR giảm bớt công việc lặp lại, tăng tốc quá trình tuyển dụng và giúp việc đánh giá ứng viên trở nên có hệ thống hơn. Tuy nhiên, dữ liệu nhân sự là dữ liệu nhạy cảm nên yếu tố bảo mật cần được đặt lên hàng đầu khi triển khai.

#### Thiết Lập Bảo Mật Cho Amazon Q Với Private Connection

Session cuối tập trung vào vấn đề bảo mật khi kết nối Amazon Q với các MCP Server hoặc hệ thống bên thứ ba. Nếu dữ liệu đi qua Internet công cộng, doanh nghiệp có thể đối mặt với nhiều rủi ro như tấn công Man-in-the-middle, DDoS hoặc rò rỉ thông tin nội bộ.

Giải pháp được đề xuất là đưa luồng kết nối vào trong mạng riêng VPC thông qua kiến trúc **Private Connection**. Kiến trúc này sử dụng nhiều thành phần AWS để cô lập luồng dữ liệu khỏi Internet công cộng.

Các thành phần chính bao gồm:

- **VPC Connection** để kết nối hệ thống trong môi trường mạng riêng.
- **Interface Endpoint** để truy cập dịch vụ một cách private.
- **Route 53 Resolver** để xử lý phân giải DNS trong môi trường nội bộ.
- **Application Load Balancer** để điều phối request.
- **TLS** để mã hóa dữ liệu trong quá trình truyền tải.

Trong phần demo, diễn giả thực hiện truy vấn bảo mật và kiểm tra độ trễ của hệ thống khi hoạt động qua môi trường private. Nội dung này giúp người tham dự hiểu rằng khi triển khai AI trong doanh nghiệp, bảo mật không chỉ nằm ở tầng ứng dụng mà còn phải được thiết kế ở tầng mạng, kết nối và luồng dữ liệu.

Một điểm cần cân nhắc là chi phí vận hành. Kiến trúc bảo mật nâng cao có thể làm tăng chi phí do sử dụng endpoint, hạ tầng mạng và data transfer. Tuy nhiên, đối với các hệ thống xử lý dữ liệu nội bộ hoặc dữ liệu khách hàng, khoản chi phí này là hợp lý để đảm bảo an toàn thông tin.

### Những Gì Học Được

#### Kiến Thức Chuyên Môn

- Cloud Computing vẫn là nền tảng quan trọng để triển khai các hệ thống AI hiện đại.
- AI Agent có thể hỗ trợ nhiều tác vụ khác nhau như xử lý incident, review code, tối ưu chi phí và kiểm thử bảo mật.
- Voice Agent thường được xây dựng dựa trên ba thành phần chính: Speech-to-Text, LLM và Text-to-Speech.
- Khi triển khai Voice AI cho tiếng Việt, cần quan tâm đến latency, xưng hô, giọng vùng miền và trải nghiệm hội thoại tự nhiên.
- DevOps AI Agent giúp rút ngắn thời gian điều tra sự cố nhưng cần hệ thống có observability tốt.
- Amazon Q có thể hỗ trợ doanh nghiệp tự động hóa các quy trình như phân tích CV, tạo JD và quản lý tuyển dụng.
- Private Connection giúp tăng cường bảo mật khi kết nối AI với hệ thống nội bộ hoặc MCP Server bên thứ ba.
- Multi-Agent Architecture phù hợp với các bài toán phức tạp cần chia nhỏ nhiệm vụ và quản lý context tốt.

#### Tư Duy Kỹ Thuật

- AI nên được xem là công cụ hỗ trợ và khuếch đại năng lực con người, không phải công cụ thay thế hoàn toàn kỹ sư.
- Khi xây dựng hệ thống AI, cần quan tâm đồng thời đến hiệu năng, chi phí, bảo mật và trải nghiệm người dùng.
- Hệ thống production cần được thiết kế với khả năng quan sát tốt thông qua log, metric và monitoring.
- Với dữ liệu nội bộ doanh nghiệp, không nên đưa dữ liệu lên public AI nếu chưa có kiểm soát bảo mật phù hợp.
- Human-in-the-loop là một thiết kế quan trọng để đảm bảo chất lượng dịch vụ khi AI chưa đủ khả năng xử lý.
- Developer cần học cách kết hợp kiến thức backend, cloud, AI và security để thích nghi với xu hướng mới.

### Ứng Dụng Vào Công Việc Và Học Tập

Những kiến thức học được từ sự kiện có thể áp dụng vào quá trình học tập và các dự án cá nhân của em như:

- Tìm hiểu sâu hơn về AWS, đặc biệt là Amazon Bedrock, Amazon Q, ECS, VPC và các dịch vụ bảo mật mạng.
- Áp dụng tư duy AI Agent vào các dự án cá nhân như chatbot hỗ trợ học tập, trợ lý tra cứu tài liệu hoặc hệ thống tự động phân tích log.
- Cải thiện dự án backend bằng cách bổ sung logging, monitoring và error handling rõ ràng hơn.
- Khi xây dựng ứng dụng có AI, cần thiết kế quy trình có con người kiểm soát ở những bước quan trọng.
- Tìm hiểu thêm về kiến trúc Multi-Agent để phục vụ các bài toán automation phức tạp.
- Áp dụng kiến thức bảo mật như private network, TLS, endpoint và phân quyền truy cập khi triển khai ứng dụng trên Cloud.
- Rèn luyện kỹ năng sử dụng AI như một công cụ hỗ trợ học tập, viết code, kiểm tra lỗi và phân tích hệ thống.

### Trải Nghiệm Trong Event

Tham gia sự kiện này là một trải nghiệm rất hữu ích đối với em. Các nội dung được trình bày không chỉ xoay quanh lý thuyết mà còn có nhiều demo thực tế, giúp em dễ hình dung cách AI và AWS được áp dụng trong doanh nghiệp.

Em ấn tượng với các phần demo về Voice Agent, DevOps AI Agent và Amazon Q trong quy trình HR. Những ví dụ này cho thấy AI có thể được ứng dụng vào nhiều lĩnh vực khác nhau, từ chăm sóc khách hàng, vận hành hệ thống cho đến quản trị nhân sự.

Là sinh viên ngành Software Engineering và có định hướng theo Backend Development, sự kiện giúp em hiểu rằng ngoài kỹ năng lập trình, em cần học thêm về Cloud, DevOps, AI Agent, bảo mật và kiến trúc hệ thống. Đây là những kiến thức quan trọng để phát triển nghề nghiệp trong thời đại AI.

#### Một số hình ảnh khi tham gia sự kiện

*Thêm các hình ảnh của bạn tại đây.*

> Tổng thể, sự kiện đã mang lại cho em nhiều kiến thức bổ ích về Cloud, AI Agent, Amazon Q và bảo mật hệ thống trên AWS. Sự kiện cũng giúp em có thêm định hướng rõ ràng hơn trong việc học tập và phát triển kỹ năng để theo đuổi lĩnh vực Backend, Cloud và AI trong tương lai.