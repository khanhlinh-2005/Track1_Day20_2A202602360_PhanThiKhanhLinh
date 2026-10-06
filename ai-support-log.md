# AI Support Log

## Thông tin

- **Học viên:** Phan Thị Khánh Linh
- **MHV:** 2A202602360
- **Bài:** Track 1 · Day 20 · Product Metrics
- **Ngày thực hiện:** 06/10/2026
- **Công cụ AI:** OpenAI Codex trong ứng dụng Codex

## AI Support Log

**AI đã giúp tôi ở đâu?**

AI giúp tôi so sánh ba hướng đề tài gồm AI Travel Planner, AI Personal
Assistant for Students và AI Customer Support Agent. Sau đó, AI đề xuất chọn AI
Personal Assistant for Students vì đề tài này gần với bối cảnh sinh viên và có
thể thu hẹp thành một use case rõ ràng: biến một assignment thành kế hoạch khả
thi và hoàn thành từng milestone đúng hạn.

AI hỗ trợ tôi phân biệt core job, core action, core value và core value event.
Các ứng viên được xem xét gồm thêm assignment, chấp nhận kế hoạch do AI tạo,
bắt đầu task và hoàn thành milestone. AI phản biện rằng `study_plan_generated`
chỉ là output của hệ thống, còn `study_plan_accepted` mới thể hiện ý định chứ
chưa chứng minh value. Từ đó, phương án được chọn là sinh viên hoàn thành một
milestone đã lên kế hoạch và xác nhận kết quả.

AI cũng gợi ý hệ thống metric gồm activation, engagement, North Star Metric,
cohort retention và counter-metric. AI giúp chuẩn hóa tên event theo dạng
`object_action`, ví dụ `assignment_added`, `study_plan_accepted`,
`study_task_completed`, `study_task_reopened` và
`study_task_rescheduled`. Với mỗi event, AI đề xuất thời điểm ghi nhận và quy
tắc chống duplicate do reload, retry hoặc autosave.

Cuối cùng, AI rà soát chuỗi logic từ core action đến cadence, metric, product
loop và tracking để phát hiện các điểm không nhất quán trước khi hoàn thiện bài.

**AI sai, hời hợt hoặc đề xuất metric sai nature ở đâu?**

AI có xu hướng đưa ra các ngưỡng cụ thể như task từ 15 đến 120 phút, activation
trong 72 giờ và retention tại W1/W4/W8. Các con số này giúp metric có thể tính
được nhưng chưa phải benchmark đã được dữ liệu thực tế chứng minh. Nếu sử dụng
chúng như kết luận chắc chắn, team có thể tối ưu theo một ngưỡng sai với hành vi
học của sinh viên.

Yêu cầu evidence cho mỗi task hoàn thành cũng có thể tạo thêm friction hoặc
khiến sản phẩm thu thập quá nhiều dữ liệu học tập. AI ban đầu tập trung vào độ
chính xác của tracking hơn là chi phí thao tác và quyền riêng tư của người dùng.
Vì vậy, evidence phải được thiết kế ở mức tối thiểu cần thiết và cần kiểm chứng
qua prototype trước khi triển khai rộng.

Ngoài ra, số milestone hoàn thành có thể tăng giả nếu một task lớn bị chia thành
quá nhiều task nhỏ. Vì vậy, tôi không dùng số task completed thuần làm North
Star Metric mà thêm quality threshold và counter-metric để chống gaming.

**Tôi đã tự sửa hoặc quyết định lại điều gì?**

Tôi chọn tiếp tục với đề tài StudyFlow AI và chỉ phân tích một use case, thay vì
đánh giá toàn bộ trợ lý học tập. Core action cuối cùng là:

- **Actor:** Sinh viên có assignment đang hoạt động.
- **Object:** Một `study_task` thuộc assignment đã được lên kế hoạch.
- **Completion rule:** Task chuyển sang `completed` bởi sinh viên, có thời điểm
  hoàn tất và bằng chứng tối thiểu về outcome.
- **Candidate event:** `study_task_completed`.

Tôi không chọn “chấp nhận kế hoạch AI” làm core action vì hành vi này chỉ thể
hiện ý định. Completion của milestone mới chứng minh sinh viên đã tạo ra tiến
độ thật và tiến gần hơn tới việc nộp assignment đúng hạn.

Tôi tự kết luận natural cadence là theo tiến trình và deadline, đo chính theo
tuần ở cấp sinh viên. StudyFlow không cần trở thành daily habit. Notification
chỉ nhắc lại một lịch đã được sinh viên chấp nhận; lý do tự nhiên để quay lại là
assignment còn dang dở, milestone tiếp theo, feedback mới hoặc deadline thật.

North Star Metric được chốt là:

> Số milestone học tập duy nhất được sinh viên hoàn thành đúng hạn, có bằng
> chứng hợp lệ và không bị mở lại trong 24 giờ, trong mỗi tuần học.

Tôi bổ sung ba counter-metric gồm tỷ lệ task bị mở lại trong 24 giờ, tỷ lệ
micro-task và số lần reschedule trung vị trên mỗi task. Các metric này giúp phát
hiện trường hợp NSM tăng do tick hoàn tất sai, chia vụn công việc hoặc kế hoạch
AI thiếu thực tế.

Tôi tự viết metric hypothesis:

> Nếu StudyFlow tạo được task vừa sức và dùng effort thực tế để hiệu chỉnh phần
> kế hoạch còn lại, thì số milestone đúng hạn trên mỗi sinh viên đủ điều kiện và
> W4 retention sẽ tăng trong bốn đến tám tuần, vì nhiều sinh viên vượt được
> first value và tiếp tục tạo tiến độ sau một task bị miss.

Các ngưỡng 15–120 phút, 72 giờ và W1/W4/W8 được giữ dưới dạng giả thuyết vận
hành ban đầu. Chúng cần được kiểm chứng bằng phỏng vấn sinh viên, phân phối
time-to-first-value và dữ liệu cohort thực tế trước khi trở thành target chính
thức.
