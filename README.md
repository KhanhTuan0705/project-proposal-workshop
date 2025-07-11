# **Proposal: Dự án Bảo mật Tự động với AWS GuardDuty và Lambda**

---

# **Thông Tin Sinh Viên Thực Tập**

- 👨‍🎓 **Họ và Tên**: Nguyễn Khánh Tuấn
- 👨‍🎓 **Trường Đại Học**: Đại Học Công Nghệ TP.HCM (HUTECH)
- 🆔 **MSSV**: 2180601761
- 📧 **Gmail**: nguyentuankhanh106@gmail.com
- 🐱 **Github**: [https://github.com/KhanhTuan0705](https://github.com/KhanhTuan0705)
- 🔗 **Link Project Proposal**: [KhanhTuan0705/Project-Proposal](https://khanhtuan0705.github.io/project-proposal-workshop/)

---

# 1. 📄 **Executive Summary**

### **Problem Statement**
Hiện nay, việc phát hiện và phản ứng với các mối đe dọa bảo mật trong môi trường AWS thường gặp phải nhiều vấn đề như phát hiện muộn, chi phí cao và quá trình phản ứng thủ công chậm. Điều này có thể dẫn đến thiệt hại nghiêm trọng về tài sản, dữ liệu và uy tín của doanh nghiệp.

### **Solution Overview**
Giải pháp bảo mật này sử dụng **AWS GuardDuty** để phát hiện các mối đe dọa bảo mật như quét cổng hoặc tấn công brute-force, và **Lambda** để tự động dừng các EC2 instances khi phát hiện mối đe dọa. **SNS** sẽ gửi thông báo qua email để người quản trị có thể xử lý nhanh chóng và hiệu quả. **EventBridge** sẽ giúp kết nối các sự kiện và kích hoạt các hành động tự động khi có mối đe dọa.

### **Business Benefits và ROI Summary**
- **Lợi ích cho doanh nghiệp**: Giảm thiểu chi phí bảo mật thủ công, tăng cường khả năng bảo vệ hệ thống khỏi các mối đe dọa tiềm ẩn.
- **ROI**: Dự án sử dụng các dịch vụ AWS Free Tier, giúp giảm thiểu chi phí ban đầu. Dự kiến ROI đạt 25% trong 6 tháng khi hệ thống tự động hóa được triển khai và vận hành.

### **Investment Required và Timeline**
- **Đầu tư cần thiết**: Dự án sử dụng AWS Free Tier, do đó, chi phí phát sinh sẽ tối thiểu trong giai đoạn phát triển và thử nghiệm.
- **Timeline**: Dự án dự kiến hoàn thành trong 3 tháng.

### **Success Metrics và Expected Outcomes**
- **Success Metrics**: Độ chính xác của hệ thống trong việc phát hiện và phản ứng với mối đe dọa đạt trên 95%, thời gian phản ứng tự động dưới 5 giây.
- **Expected Outcomes**: Cải thiện bảo mật hệ thống và giảm thiểu các sự cố bảo mật thông qua tự động hóa.

---

# 2. 🎯 **Problem Statement**

### **Current Situation Analysis**
Nhiều doanh nghiệp hiện nay gặp khó khăn trong việc phát hiện và xử lý các mối đe dọa bảo mật một cách kịp thời. Các giải pháp hiện tại chủ yếu dựa vào phương pháp thủ công, khiến việc xử lý mối đe dọa trở nên chậm chạp và thiếu hiệu quả.

### **Pain Points Identification**
- Thời gian phát hiện và phản ứng với các mối đe dọa bảo mật quá chậm.
- Các biện pháp thủ công không đủ nhanh để bảo vệ hệ thống khỏi các cuộc tấn công.
- Chi phí vận hành cao do phải thuê đội ngũ bảo mật và xử lý thủ công.

### **Stakeholders Affected và Their Concerns**
- **Doanh nghiệp**: Quan tâm đến chi phí và hiệu quả của hệ thống bảo mật.
- **Nhân viên IT**: Quan tâm đến việc có thể giảm tải công việc thủ công và cải thiện quy trình bảo mật.

### **Business Consequences của Inaction**
Nếu không có hệ thống tự động phát hiện và phản ứng, doanh nghiệp có thể đối mặt với các sự cố bảo mật nghiêm trọng, gây mất dữ liệu và giảm lòng tin của khách hàng.

### **Market Opportunity**
Giải pháp này sẽ giúp doanh nghiệp tiết kiệm chi phí và cải thiện khả năng bảo mật hệ thống, giúp doanh nghiệp luôn sẵn sàng đối phó với các mối đe dọa bảo mật ngày càng tinh vi.

---

# 3. 🏗️ **Solution Architecture**

### **High-level Architecture Diagram**
![Solution Architecture Diagram](/images/arc-001-light.png)

### **AWS Services Selection và Justification**
- **AWS GuardDuty**: Giúp phát hiện các mối đe dọa trong hệ thống EC2, S3, và VPC, cung cấp cảnh báo khi có hành vi đáng ngờ.
- **AWS Lambda**: Giúp tự động dừng EC2 instances khi phát hiện mối đe dọa, giảm thiểu sự can thiệp thủ công.
- **Amazon SNS**: Gửi thông báo cảnh báo đến người quản trị qua email khi có mối đe dọa.
- **Amazon EventBridge**: Kết nối các sự kiện và kích hoạt hành động tự động.
- **AWS IAM**: Quản lý quyền truy cập và bảo mật các dịch vụ AWS.

### **Component Interactions và Data Flow**
1. **GuardDuty** phát hiện mối đe dọa từ **attack-ec2**.
2. **EventBridge** nhận sự kiện từ GuardDuty và kích hoạt **Lambda**.
3. **Lambda** dừng **target-ec2** và gửi thông báo qua **SNS**.
4. **SNS** gửi thông báo cảnh báo qua email cho người quản trị.

---

# 4. 🔧 **Technical Implementation**

### **Implementation Phases và Deliverables**
1. **Phase 1**: Thiết kế hệ thống và lựa chọn dịch vụ AWS (2 tuần)
2. **Phase 2**: Phát triển và triển khai Lambda functions, cấu hình GuardDuty, SNS (4 tuần)
3. **Phase 3**: Kiểm thử và triển khai toàn bộ hệ thống (4 tuần)

### **Technical Requirements**
- **Compute**: AWS Lambda (miễn phí 1 triệu lượt gọi mỗi tháng)
- **Storage**: Amazon S3 (miễn phí 5GB bộ nhớ lưu trữ)
- **Network**: AWS API Gateway (miễn phí 1 triệu yêu cầu mỗi tháng)

### **Development Approach và Methodologies**
- **Phương pháp phát triển**: Agile Development với các giai đoạn triển khai ngắn, kiểm thử liên tục.

### **Testing Strategy**
- **Unit Testing**: Kiểm tra các hàm Lambda.
- **Integration Testing**: Kiểm tra việc tích hợp Lambda, GuardDuty, SNS và EventBridge.
- **Performance Testing**: Kiểm tra hiệu suất khi có nhiều mối đe dọa phát sinh.

### **Deployment Plan và Rollback Procedures**
- **Deployment Plan**: Triển khai qua AWS CloudFormation và API Gateway.
- **Rollback Procedures**: Quay lại phiên bản trước nếu gặp sự cố nghiêm trọng.

### **Configuration Management**
- Sử dụng Git và AWS CloudFormation để quản lý cấu hình.

---

# 5. 📅 **Timeline & Milestones**

### **Project Phases Breakdown**
1. **Giai đoạn 1: Thiết kế và lập kế hoạch** (1 tuần)
2. **Giai đoạn 2: Phát triển và triển khai** (1 tuần)
3. **Giai đoạn 3: Kiểm thử và triển khai** (1 tuần)

### **Key Milestones và Success Criteria**
- **Milestone 1**: Thiết kế hệ thống và lựa chọn các dịch vụ AWS.
- **Milestone 2**: Phát triển và kiểm thử giải pháp.
- **Milestone 3**: Triển khai vào môi trường sản xuất.

---

# 6. 💰 **Budget Estimation**

### **AWS Infrastructure Costs (Monthly/Annually)**
- **Monthly**: Chi phí chủ yếu là miễn phí trong AWS Free Tier.
- **Annually**: Chi phí phát sinh nếu vượt quá giới hạn Free Tier.

### **Development Costs (One-time)**
- **Chi phí nhân sự**: Dự án yêu cầu 480 giờ làm việc (chi phí nhân sự khoảng $2,400).

### **Operational Costs (Ongoing)**
- **Chi phí AWS**: Phát sinh khi vượt quá Free Tier.

---

# 7. ⚠️ **Risk Assessment**

### **Risk Identification**
1. **Technical Risks**: Hệ thống không hoạt động như mong đợi khi tích hợp GuardDuty với Lambda.
2. **Business Risks**: Khách hàng không chấp nhận công nghệ mới.

---

# 8. 🎯 **Expected Outcomes**

### **Success Metrics**
- **Technical**: Thời gian phản hồi dưới 5 giây, độ chính xác đạt 95%.
- **Business**: Tiết kiệm chi phí bảo mật và tăng hiệu quả công việc.

---

### **Long-term Value**
- Giải pháp có thể mở rộng và áp dụng cho nhiều hệ thống AWS trong tương lai.

---

Đây là **Proposal** chi tiết cho dự án của bạn với **AWS GuardDuty** và **Lambda**, được viết theo dạng **Markdown**.
