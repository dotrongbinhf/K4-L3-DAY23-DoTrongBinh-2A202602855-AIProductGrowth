# Worksheet — AI trực inbox ngoài giờ cho shop thời trang

Họ tên: Đỗ Trọng Bình · MSSV: 2A202602855 · Ngày làm: 09/10/2026

## Chuẩn bị — số liệu đầu vào

**Trạng thái:** Đã đọc HANDBOOK §2 và đối chiếu one-pager với workbook Day 22 ngày 09/10/2026. Dự án ở giai đoạn ý tưởng, chưa có MVP, khách hàng, Eval hoặc pilot được xác nhận. Các số dưới đây là giả định/dự toán từ bài trước, không phải số vận hành thực đo. Runway chưa có trong hai tài liệu.

**Nguồn:** [Mô hình Day 22](../Track1_Day22_2A202602855_DoTrongBinh/DoTrongBinh_Day22_model.xlsx) và [One-pager Day 22](../Track1_Day22_2A202602855_DoTrongBinh/DoTrongBinh_Day22_onepager.pdf), lập ngày 08/10/2026. Tham chiếu sheet/ô bên dưới thuộc workbook này. Link tương đối dùng để tra cứu trên máy; khi nộp repo độc lập cần cung cấp bản nguồn được phép chia sẻ hoặc phụ lục số liệu trong repo.

| Đầu vào | Giá trị | Đơn vị / kỳ / phạm vi cần xác nhận | Nguồn và ngày số liệu |
|---|---|---|---|
| Tên và mô tả sản phẩm AI | AI trực inbox ngoài giờ cho shop thời trang | Xử lý hỏi size, giá, tồn kho và hỗ trợ tạo đơn trên Messenger, ca 19:00–24:00 | 0_README!B29:B31; 5_90Day_Plan!B5:B8 |
| Người trả tiền | Chủ shop thời trang — khách hàng mục tiêu, chưa có người trả phí | Ngân sách nhân sự trực inbox/vận hành dự kiến; cần phỏng vấn xác nhận | 0_README!B28:B30 |
| Người sử dụng | Dự kiến: chủ shop/nhân viên vận hành; người mua tương tác với AI qua Fanpage shop | Chưa có người dùng thật được xác nhận; shop tự xử lý ca chuyển người (HITL A) | 0_README!B28:B33; 1_Cost_Job!B6; 5_90Day_Plan!B8 |
| Điểm chạm người dùng cuối | Dự kiến Messenger webhook + Send API, inbox hiện có của shop | Chưa triển khai; quyền Page/API là điều kiện pilot; chưa có bằng chứng thương hiệu riêng trước người mua | 5_90Day_Plan!B8; B41 |
| ARPU dự kiến | $120/shop/tháng | Recurring: $30 phí nền + $90 gói 1.000 phiên; không cộng setup $20 một lần | 4_Channel_Fit!B5; 2_Pricing!B57:B66; B101 |
| Gross margin (GM) | Dự toán 68,7329%; mục tiêu 60% | COGS $37,520533/shop/tháng gồm API, retry, infra, QA; loại overhead | 2_Pricing!B32; B66:B68 |
| CAC dự toán | $120/shop trả phí mới | Cohort $600 / 5 khách dự kiến; 20 cơ hội × win rate 25%; chưa đo | 4_Channel_Fit!B21; B45:B48 |
| CAC payback mục tiêu | Trần nội bộ 6 tháng; template SMB 12 tháng | Dự toán payback tại baseline ≈1,4549 tháng; dùng 6 tháng làm giới hạn nội bộ đã chọn | 4_Channel_Fit!B8; B49:B50 |
| Runway | Chưa có trong tài liệu Day 22 | Cần tiền mặt khả dụng và net burn/tháng, cùng ngày chốt; kế hoạch 90 ngày không phải runway | Chưa có nguồn |
| Value Metric / cách thu phí đã chọn | Hybrid: phí nền + số hội thoại có phản hồi nghiệp vụ AI | Gói $120/tháng; vượt gói $0,09/phiên khi được phép; ca chuyển người vẫn dùng quota; không thu theo đơn hàng | 3_Value_Metric!B30:B34; B40:B42 |
| Đơn vị giá trị / Job hoàn thành | Yêu cầu mua hàng xử lý đúng, đủ, khách xác nhận, không cần người | Nếu mua: đơn hợp lệ và khách xác nhận; bỏ ngang không tính; mở lại cùng vấn đề trong 24h hủy hoàn thành | 0_README!B32:B33 |
| Cost/Job (COGS) | $0,05002738/completed Job, khoảng 1.309,22 VND | Bao gồm API, retry, infra và QA cho toàn bộ phiên thử, chia cho số Job hoàn thành; chưa overhead | 1_Cost_Job!B62:B69 |
| Cost/Job có overhead | $0,07669404/completed Job | Overhead thêm $20/shop/tháng; tách khỏi COGS dùng tính GM | 1_Cost_Job!B59; B65:B67 |
| Job / shop / tháng | 1.000 phiên thử; 750 Job hoàn thành | Containment giả định 75%; chưa có Eval; không đồng nhất completed với billable conversations | 1_Cost_Job!B9:B11; 0_README!B35 |
| Chi phí LLM + retry / shop / tháng | $18,1872 | $16,84 LLM + $1,3472 retry; mức retry 8% là giả định | 1_Cost_Job!B46; B72; B75 |
| COGS ngoài LLM + retry / shop / tháng | $19,333333 | Infra $6 + QA $13,333333; speech/telephony = 0 do text-only; escalation do shop chịu | 1_Cost_Job!B74; B76; B90:B95 |

**Bối cảnh dự án:** Founder trực tiếp bán và triển khai (Sales-Led); pain moment giả định lúc 22:30. Phạm vi chỉ Messenger text với catalog/bảng size/giá/tồn kho/chính sách shop duyệt. Không tự giảm giá, bảo đảm size vừa hoặc hứa giao hàng khi thiếu dữ liệu. Mục tiêu 90 ngày 09/10/2026–06/01/2027: 10 phỏng vấn, 20 cơ hội demo, 2 shop pilot và 5 shop trả phí cộng dồn; đây đều là kế hoạch, chưa đạt. Nguồn: 0_README!B31; B39:B40; 5_90Day_Plan!B5:D18.

**Phân loại ở Trạm 1:** Chọn B2B theo hiện trạng sản phẩm ở giai đoạn ý tưởng: bán công cụ vận hành cho shop; chưa có bằng chứng về quyền tiếp cận độc lập người mua cuối hoặc thương hiệu riêng trước họ. AI trả lời khách của shop và tích hợp Meta chưa đủ chứng minh B2B2C; Meta không phải partner phân phối.

**Quy ước:** Giữ cùng đồng tiền và cùng phạm vi khách trong phép tính. Không thay dữ liệu thiếu bằng 0; không tô đèn xanh khi chưa có số. Nếu cần bảo mật, nhân mọi số tiền với cùng một hệ số và ghi “số đã được scale” trong README.md.

**Hai hướng tính [MH] để điền ở Trạm 3 (chưa phải ngưỡng đã chốt):**

- Lãi gộp / khách / tháng = ARPU × GM; CAC tối đa = ARPU × GM × số tháng payback mục tiêu. Cần thêm lý do chọn ranh giới xanh/vàng; công thức này mới cho trần CAC.
- Trần chi phí LLM + retry / completed Job = [ARPU × (1 − GM mục tiêu) − COGS ngoài LLM + retry / shop / tháng] ÷ số completed Job / shop / tháng. Chỉ so với LLM + retry/completed Job, không so với Cost/Job tổng COGS.

**Đối chiếu từ đầu vào Day 22 (chưa chốt ba màu):**

- Lãi gộp tháng = $120 − $37,520533 = $82,479467/shop; CAC tối đa nội bộ = $82,479467 × 6 = **$494,8768**. Mức $989,7536 trong template ứng với 12 tháng, không phải trần nội bộ.
- Ngân sách COGS để GM ≥60% = $120 × 40% = **$48/shop/tháng**. Sau infra + QA: ngân sách LLM + retry = $48 − $19,333333 = **$28,666667/shop/tháng**, tương đương **1,5762×** baseline $18,1872 (khớp 2_Pricing!B79). Nếu volume/QA/infra thay đổi phải tính lại.
- Ngưỡng containment **72%** trong 2_Pricing!B75 là ngưỡng giữ giá gói ≤25% giá trị thời gian tránh được: $120 ÷ (1.000 × 10/60 × $4 × 25%) = 72%. Không dùng ngưỡng Outcome 58,63% ở B33 cho Hybrid. Khi volume và chi phí cố định, containment thấp làm giảm giá trị khách nhận được dù GM hóa đơn có thể vẫn giữ nguyên.

**Các khoản chưa có:** Runway, dữ liệu retention/churn, thời gian tới giá trị đầu tiên, kết quả Eval/pilot, willingness to pay và thời gian lao động tiết kiệm thực tế. Giá API/tỷ giá ghi trong nguồn đã kiểm tra 08/10/2026 theo tác giả; lần đọc này không xác minh lại các trang giá, không nhận là benchmark mới.

**Tự kiểm tra trước Trạm 1:**

- [x] Có worksheet.md và dashboard.md ở thư mục gốc.
- [ ] Có đủ ARPU, GM, CAC, payback, runway và Cost/Job từ bài của tôi — đã có dự toán của 5 mục; còn thiếu runway.
- [x] Đã đọc HANDBOOK §2 về ba tầng, thẻ đèn, nguồn ngưỡng và luật.

## Trạm 1 — Loại mô hình

### Ba câu hỏi theo thực tế ngày 09/10/2026

1. **Ai trả tiền?** Chưa có khách trả tiền được xác nhận. Người mua mục tiêu trong mô hình đã chọn là chủ shop thời trang, chi từ ngân sách nhân sự trực inbox/vận hành của shop; không bán thuê bao cho người mua quần áo.
2. **Ai dùng?** Chưa có MVP hoặc người dùng thật được xác nhận. Sản phẩm được thiết kế để chủ shop/nhân viên quản lý catalog, chính sách và nhận ca chuyển người; người mua quần áo tương tác với AI trong Messenger của Fanpage shop.
3. **Có chạm end-user không?** Điểm chạm dự kiến là Messenger webhook + Send API của shop, chưa được triển khai/cấp quyền pilot được xác nhận. Chưa có dữ liệu end-user thực tế, quyền tiếp cận độc lập hay thương hiệu của sản phẩm trước người mua được chứng minh. Shop là khách mua công cụ vận hành, không phải partner phân phối đã ký; Meta là bề mặt tích hợp.

**Câu chốt loại:** Chúng tôi chọn mô hình **B2B** ở giai đoạn ý tưởng vì người mua mục tiêu là chủ shop thời trang, người vận hành là chủ shop/nhân viên, còn tương tác với người mua cuối dự kiến nằm trong Messenger của shop và chưa có quyền tiếp cận độc lập hoặc thương hiệu riêng được chứng minh.

**Bảng sử dụng:** HANDBOOK **§3.2 — B2B**, không trộn bảng B2C/B2B2C. **Đèn bật trước: Time-to-first-value (TTFV)** — thời gian từ ký thỏa thuận đến lần đầu shop xác nhận giá trị đo được, không phải ngày cài xong chatbot. Việc trả lời khách trong một Fanpage không tự biến shop thành partner B2B2C.

### Khả năng đo toàn bộ bảng đèn B2B

Ngày kiểm kê: **09/10/2026**. Hạn hai tuần: **23/10/2026**. Người chuẩn bị phép đo: **Đỗ Trọng Bình**.

- ✅ chỉ dùng khi có số thực và nguồn kiểm tra được. Bài Day 22 có dự toán, chưa đủ để đánh dấu ✅ cho đèn vận hành.
- 🔧 là có thể thiết lập và lấy quan sát ban đầu trước 23/10, nếu diễn ra demo/khảo sát như kế hoạch; không có quan sát thì giữ “chưa có số”, không thay bằng 0.
- ❌ là chưa có số và chưa có điều kiện bảo đảm lấy số trong hai tuần. Với các đèn này, phương pháp có thể đã biết nhưng khách/cohort/log chưa tồn tại; ghi cụ thể bên dưới thay vì nói chưa biết cách đo khi đã biết. Pilot Day 22 dự kiến bắt đầu 26/10, sau hạn hai tuần.

| # | Tầng | Đèn trong HANDBOOK §3.2 | ✅ / 🔧 / ❌ | Số nằm ở đâu / cần gì để đo | Mốc và giới hạn |
|---|---|---|---|---|---|
| 1 | L | **Time-to-first-value (TTFV)** ⭐ | ❌ | Chưa có thỏa thuận/pilot và dấu mốc shop xác nhận giá trị. Cần `agreement_signed_at`, `first_verified_value_at`, log Job và time study được shop xác nhận; không lấy thời gian cài đặt làm giá trị. | Thiết kế log trước 23/10; chỉ có thể lấy số sau khi shop ký và nhận giá trị trong pilot từ 26/10. Dự kiến rà soát trong báo cáo 09/11, chưa bảo đảm có giá trị đạt. |
| 2 | L | **Pipeline coverage** | 🔧 | Lập CRM cơ hội: shop, người quyết định, nhu cầu ngoài giờ, trạng thái demo, giá trị recurring theo cùng kỳ và ngày đóng dự kiến. Coverage = giá trị cơ hội đủ điều kiện / target recurring cùng kỳ; 20 cơ hội ở Day 22 chỉ là mục tiêu. | Đến 23/10 thu danh sách demo ban đầu và chốt target cùng kỳ; mục tiêu 5 shop cộng dồn không tự là target doanh thu quý. Chưa có cơ hội/target thì chỉ số chưa xác định. |
| 3 | L | **% deal chết ở khâu security/procurement** | 🔧 | CRM phải ghi mọi deal đã đóng thắng/thua và lý do mất: quyền Page, dữ liệu, an toàn, duyệt ngân sách. Tử số là deal bị chặn ở duyệt an toàn/mua hàng, mẫu số là tổng deal đóng trong kỳ; không tính deal còn mở là thất bại. | Thiết lập trước 23/10 và ghi các quyết định phát sinh qua demo; không có deal đóng thì N/A, không ghi 0%. Chưa có evidence pack hoàn thành. |
| 4 | O | **POC → paid** | ❌ | Chưa có POC hoàn thành hoặc hợp đồng trả tiền. Cần danh sách cohort pilot, ngày bắt đầu/kết thúc, thời hạn chuyển đổi và hóa đơn/thanh toán xác nhận; tách pilot đang chạy. | Pilot dự kiến 26/10–08/11; bắt đầu kiểm kê từ 09/11, tỷ lệ chỉ có khi cohort đủ thời hạn chuyển đổi. Win rate mục tiêu 25% không phải POC → paid. |
| 5 | O | **Sales cycle (tuần)** | 🔧 | CRM ghi `qualified_at`, `signed_at` và thỏa thuận ký. Tính tuần từ cơ hội đủ điều kiện đến chữ ký; không tính từ lead thô hoặc dùng số 19 tuần trong handbook làm số của dự án. | Thiết lập và lấy ngày vào pipeline trước 23/10; nếu chưa có chữ ký, chỉ báo tuổi deal đang mở, chưa có sales cycle hoàn tất. |
| 6 | O | **Usage depth trong tài khoản** | ❌ | Chưa có tài khoản hoạt động. Vì bán Hybrid chứ không bán seat, cần thống nhất workflow đã mua với shop và log workflow được dùng thật hằng tuần; loại test nội bộ, spam và lỗi kỹ thuật. | Chốt danh mục workflow trước 23/10; lấy tuần sử dụng thật sau go-live từ 26/10 nếu pilot được cấp quyền. Quota tiêu thụ không tự đồng nghĩa usage depth. |
| 7 | O | **Chi phí triển khai ÷ ACV** | 🔧 | Day 22 dự toán onboarding 2h × $4 = $8 và recurring quy đổi năm $1.440 (2_Pricing!B96:B98; 4_Channel_Fit!B10), chưa phải thực đo. Cần time log cấu hình catalog/quyền Page/kiểm tra, đơn giá công và chi phí tích hợp trực tiếp; ACV phải cùng khách. | Chuẩn bị time log và đo thử setup trước 23/10; chỉ gọi tỷ lệ thực đo khi có triển khai và giá trị hợp đồng xác nhận. $8/$1.440 ≈0,56% là dự toán, không phải ✅. |
| 8 | O | **Tập trung doanh thu** | ❌ | Chưa có doanh thu khách thực tế. Cần sổ hóa đơn/doanh thu từng shop cùng tháng; lấy doanh thu khách lớn nhất / tổng doanh thu. Tách setup một lần khỏi recurring khi phân tích. | Lấy số ở tháng đầu có doanh thu; mục tiêu 5 shop trả phí đến 06/01/2027 không phải 5 khách hiện tại. Tổng doanh thu chưa có thì N/A. |
| 9 | G | **NRR** | ❌ | Chưa có cohort khách trả phí đầu kỳ và dữ liệu gia hạn, expansion, contraction, churn. NRR = recurring cuối kỳ của chính cohort đầu kỳ / recurring đầu kỳ; không cộng khách mới. | Chuẩn bị ledger từ khách trả phí đầu tiên; đo sau một chu kỳ đủ kỳ hạn, chưa xác định ngày có số vì chưa có khách. Không suy NRR từ mục tiêu gia hạn. |
| 10 | G | **Gross Margin** | ❌ | Chỉ có GM dự toán 68,7329% (2_Pricing!B68). Cần doanh thu thực và hóa đơn API, infra, QA/support, retry, onboarding tương ứng kỳ; không gộp R&D/sales vào recurring COGS. | Có thể đo chi phí pilot trong báo cáo 09/11; pilot miễn phí có Cost/Job nhưng không có GM thương mại. GM có số khi có kỳ doanh thu trả phí. |
| 11 | G | **CAC payback** | ❌ | Chỉ có dự toán CAC $120 và payback 1,4549 tháng (4_Channel_Fit!B48:B49). Cần chi phí toàn cohort acquisition gồm giờ founder và khách thắng đã trả phí, cùng lãi gộp recurring thực; tách onboarding khỏi CAC. | Có CAC/payback ước tính từ thực tế khi cohort có khách trả phí và GM đo được; hoàn vốn thực chỉ xác nhận khi lãi gộp tích lũy bù CAC. Chưa thể hẹn ngày; chưa có runway để đối chiếu. |

**Kết quả kiểm kê:** 11/11 đèn đã đánh dấu — **0 ✅, 4 🔧, 7 ❌**. Không đèn nào được coi là đang xanh từ số dự toán. Các mốc tương lai là lịch chuẩn bị/kiểm chứng, không phải kết quả đã đạt.

**Nguyên liệu cho Trạm 2:** TTFV là đèn Leading ưu tiên; cần thêm đèn chi phí LLM + retry hoặc Cost/Job từ log trước khi chi phí hiện ra ở GM. Chỉ chọn 6–8 đèn ở Trạm 2, không đưa toàn bộ 11 đèn lên dashboard. Danh sách chưa đo ở trên là đầu vào cho mục “Chưa đo được” ở Trạm 5.

**Checkpoint Trạm 1:**

- [x] Có ba câu trả lời theo hiện trạng, ghi rõ chưa có khách thật.
- [x] Có một câu chốt B2B nêu người mua, người vận hành và điểm chạm end-user.
- [x] Đã dùng đúng bảng HANDBOOK §3.2 và đánh dấu đủ mọi đèn.
- [x] Mỗi đèn có chỗ lấy số hoặc dữ liệu/điều kiện còn thiếu; không coi giả định tài chính là dữ liệu vận hành.

## Trạm 2 — Thẻ đèn

**North Star: TTFV của shop chậm nhất trong 3 thỏa thuận triển khai gần nhất (ngày), càng thấp càng tốt.** Hiện tại: **chưa đo**, chưa có thỏa thuận triển khai. Mục tiêu tạm thời **≤14 ngày [TB]** để shop nhận giá trị trong một pilot hai tuần; ngưỡng và lịch đo baseline ở Trạm 3. Đây là mục tiêu vận hành, không phải số lịch sử đã đo.

**Giá trị đầu tiên của shop:** Có ít nhất một yêu cầu mua hàng thật được AI xử lý đúng, đủ, khách xác nhận, không cần người xử lý; shop xác nhận phút lao động tránh được so với cách làm trước đó. Đây là định nghĩa đo pilot, chưa được shop đồng thuận. Nếu có đơn mua, đơn phải hợp lệ và khách xác nhận. Chờ hết cửa sổ mở lại 24h mới công nhận Job hoàn thành; lưu riêng thời điểm xử lý xong và thời điểm bằng chứng được xác nhận. Replay/Eval không thay thế xác nhận của khách thật.

**Cohort TTFV:** Lấy tối đa 3 shop theo ngày ký thỏa thuận triển khai/pilot gần nhất, gồm cả shop chưa go-live và shop ngừng triển khai. Điểm bắt đầu là lúc ký thỏa thuận, không dời sang ngày cấp đủ dữ liệu để che chậm trễ. Khi có dưới 3 shop phải ghi n thực tế. Nếu bất kỳ shop nào trong cohort chưa đạt giá trị, North Star là **“chưa đủ dữ liệu”**, kèm tuổi chờ của từng shop; không tính max chỉ trên các shop thành công để tô xanh.

**Quy ước chung:** Múi giờ Asia/Saigon; tuần từ thứ Hai 00:00 đến thứ Hai kế tiếp, dùng cửa sổ [bắt đầu, kết thúc). Log dùng `shop_id`, `session_id/job_id` và `request_id` để tránh tính trùng. Phiên hợp lệ là phiên khách thật có yêu cầu mua hàng thuộc phạm vi Messenger text; loại test, spam và Eval offline. Mở lại cùng vấn đề trong 24h gộp cùng Job; lỗi kỹ thuật, chuyển người và khách bỏ ngang trong phiên hợp lệ vẫn thuộc mẫu thử. Mẫu số bằng 0 hoặc thiếu log thì N/A, không thay bằng 0. Các quan hệ báo trước bên dưới là giả thuyết vận hành cần kiểm chứng, không phải quan hệ nhân quả đã chứng minh.

| # | Tầng (L/O/G) | Đèn | Định nghĩa (đếm gì · **không** đếm gì) | Công thức | Nhịp · ai lấy số | Báo trước cho |
|---|---|---|---|---|---|---|
| 1 | L | **TTFV shop chậm nhất** ⭐ | Ngày từ ký thỏa thuận đến thời điểm shop xác nhận giá trị đầu tiên theo định nghĩa trên, trong 3 thỏa thuận gần nhất. **Không** coi kết nối API, demo, replay hoặc ngày cài xong là giá trị; không loại shop chưa đạt. | Với từng shop đã đạt: `(first_verified_value_at − agreement_signed_at)/86.400 giây`; North Star = `MAX(TTFV_i)` chỉ khi mọi shop trong cohort đã đạt. Nếu chưa: N/A + tuổi chờ `(as_of − agreement_signed_at)/86.400`. | Kiểm tra mỗi ngày; chốt tuần. Đỗ Trọng Bình lấy timestamp; chủ shop xác nhận giá trị và time study. | **#4 POC → paid**, dự kiến ở cuối pilot/30 ngày sau; qua chuyển đổi đến **#7 CAC payback**. TTFV dài làm khách chậm quyết định trả phí. |
| 2 | L | **p95 chi phí LLM + retry / phiên thử hợp lệ, theo shop** | Tổng USD LLM cho mọi model call/cache read/write và retry của từng phiên thử hợp lệ, kể cả phiên lỗi/chuyển người/bỏ ngang. **Không** chia cho completed Job; không gồm infra, QA, overhead hoặc Eval offline. Không gộp mọi shop trước khi lấy p95. | `c_j = SUM(chi phí LLM và retry gắn session_id j)`; sắp tăng dần trong từng shop/tuần, `p95_shop = c_(CEILING(0,95×n))`. Dashboard = `MAX(p95_shop)` và tên shop tương ứng; n=0: N/A. | Cập nhật ngày, cửa sổ 7 ngày gần nhất cho cảnh báo; chốt theo tuần. Đỗ Trọng Bình lấy usage token từ provider, tính theo giá áp dụng rồi đối soát hóa đơn. | **#6 GM** cuối tháng, khoảng 1–4 tuần: phiên dài/retry tăng chi phí trước khi khóa sổ. Đây là đèn chi phí AI. |
| 3 | O | **Containment có giá trị được xác nhận** | % phiên thử hợp lệ hoàn thành đúng, đủ, khách xác nhận, không có người can thiệp và không mở lại cùng vấn đề trong 24h. **Không** tính test/spam, chỉ mở app, khách bỏ ngang, ca chuyển người hoặc đơn chưa được xác nhận là hoàn thành. | `100 × số Job hoàn thành / số phiên thử hợp lệ`, theo shop. Cohort là phiên có lần phản hồi AI đầu tiên trong tuần; chỉ chốt kết quả sau khi đóng phiên và qua 24h. Dashboard = tỷ lệ thấp nhất trong các shop có cohort đủ dữ liệu, kèm n từng shop; phiên còn mở làm cohort chưa đủ, không âm thầm loại. | Theo tuần; log hoàn thành, handoff, reopen và xác nhận khách. Đỗ Trọng Bình tính; shop xác nhận tính đúng và phút lao động thực. | **#4 POC → paid** ở quyết định mua: Job không hoàn thành làm giảm giá trị thời gian tránh được. Không khẳng định containment thấp tự làm giảm GM Hybrid khi chi phí/volume cố định. |
| 4 | O | **POC → paid trong 30 ngày sau pilot** | % shop hoàn tất pilot có thanh toán recurring đầu tiên trong 30 ngày sau ngày kết thúc. Cohort theo tháng kết thúc pilot, chỉ chốt khi mọi shop đủ 30 ngày. **Không** tính demo, hứa mua, setup fee riêng, hoặc pilot chưa bắt đầu; shop bỏ pilot sau khi bắt đầu tính kết thúc tại ngày dừng và giữ trong mẫu số. | `100 × shop trong cohort có thanh toán recurring trước/đúng end_at+30 ngày / tổng shop trong cohort pilot đã kết thúc hoặc dừng`. Ghi số thắng/tổng; thời hạn 30 ngày là quy ước đo, không phải ngưỡng chuyển đổi. | Cập nhật tuần; chốt cohort tháng khi đủ thời hạn. Đỗ Trọng Bình đối chiếu thỏa thuận, ngày pilot và chứng từ thanh toán. | **#7 CAC payback** của cohort bán hàng: chuyển đổi thấp làm chi phí acquisition chia trên ít khách trả phí hơn. Cohort acquisition được đối chiếu riêng, không lấy POC rate thay win rate mọi cơ hội. |
| 5 | O | **Chi phí triển khai / ACV recurring** | Giờ công import catalog, cấu hình quyền Page, kết nối, kiểm thử và sửa để go-live × loaded rate, cộng phí tích hợp trực tiếp một lần, theo shop. **Không** gồm prospecting/demo thuộc CAC hoặc recurring API/QA đã tính trong COGS; không bỏ công founder. ACV ở đây là recurring quy đổi năm theo đơn giá đã được shop chấp nhận, không mặc định có hợp đồng năm. | `100 × COGS onboarding thực / (12 × recurring tháng đã thống nhất)`; dashboard = tỷ lệ cao nhất của các shop đã hoàn tất triển khai, kèm chi phí lũy kế shop đang triển khai. Chưa thống nhất giá: N/A, không dùng $1.440 dự toán làm hợp đồng thật. | Ghi time log mỗi ngày; chốt mỗi go-live và rà soát tuần. Đỗ Trọng Bình ghi công và chứng từ tích hợp; shop xác nhận phạm vi. | **#6 GM** tháng triển khai, khoảng 1–4 tuần: onboarding tốn công làm giảm biên tháng đầu. Không cộng onboarding vào CAC lần nữa. |
| 6 | G | **Gross Margin theo shop/tháng** | Biên trên doanh thu dịch vụ được ghi nhận trong tháng trừ COGS trực tiếp cùng kỳ: LLM/retry, infra, QA/support và onboarding nếu phát sinh. Theo dõi recurring và tháng đầu gồm setup riêng. **Không** gọi margin sau R&D/sales là GM, không coi hóa đơn chưa cung cấp dịch vụ là doanh thu đã ghi nhận. | `100 × (doanh thu − COGS)/doanh thu`; dashboard = GM thấp nhất của các shop có doanh thu trong tháng hoàn tất gần nhất, n shop đi kèm. Recurring GM dùng recurring revenue/COGS; onboarding và setup được trình bày riêng khi tính GM tháng đầu. Doanh thu=0: N/A, vẫn ghi chi phí pilot. | Cuối tháng; theo shop và tổng đối soát ledger. Đỗ Trọng Bình khóa sổ doanh thu/chi phí từ chứng từ và time log. | **#7 CAC payback**: lãi gộp recurring thấp kéo dài thời gian thu hồi CAC. GM là kết quả xác nhận chuỗi **#2/#5 → #6**, không phải đèn Leading. |
| 7 | G | **CAC payback ước tính từ dữ liệu thực** | Tháng hoàn vốn acquisition của cohort bán hàng đã đóng, dựa trên lãi gộp recurring thực mỗi khách. CAC gồm toàn bộ chi phí cohort (giờ founder, prospecting/demo, pilot phục vụ bán hàng), không chỉ khách thắng. **Không** gồm onboarding khách trả phí đã vào COGS, setup revenue hoặc dùng CAC mục tiêu thay CAC thực. | `CAC_cohort = acquisition_cost_cohort / số shop trả recurring trong cohort`; `payback = CAC_cohort / lãi gộp recurring bình quân mỗi shop mỗi tháng`. Khóa cohort đã đóng, dùng tháng recurring hoàn tất gần nhất; n paid=0: chưa xác định; lãi gộp≤0: không có hoàn vốn hữu hạn. Phân biệt ước tính này với ngày hoàn vốn lũy kế đã xảy ra. | Rà soát tháng, chốt cohort acquisition kết thúc chiến dịch; Đỗ Trọng Bình lấy ledger công/sales và chứng từ recurring. | **Runway/kế hoạch tiền mặt các tháng tiếp theo**: payback dài khiến ngân sách acquisition khó quay vòng; xác nhận chuỗi **#1/#3 → #4 → #7** và **#6 → #7**. Runway là đầu vào tài chính đang thiếu, không thêm thành đèn thứ 8. |

**Đèn chi phí AI là #2.** p95 phản ánh đuôi chi phí phiên và báo shop có rủi ro cao; nó không thay tổng chi phí trong #6. Với ít phiên, p95 gần max, nên luôn ghi n và không coi một phiên đắt là xu hướng ổn định. Giá mô hình đồng nhất 6 calls/phiên trong Day 22 không tạo ra baseline p95 thực; mức $0,0181872 LLM + retry/phiên dự toán là bình quân, không được gắn nhãn p95.

### Cây ba tầng và lý do giữ đèn

```text
LEADING      #1 TTFV ───────────────┐       #2 p95 LLM + retry ───────┐
                                   ▼                                │
OPERATING    #3 Containment ───► #4 POC → paid    #5 Triển khai/ACV ──┤
                                   │                                ▼
LAGGING                            └────────► #7 CAC payback ◄──── #6 GM
```

**Phân bổ:** 2 Leading + 3 Operating + 2 Lagging = **7 đèn**, Lagging chiếm 2/7. North Star là #1 trong 7 đèn, không phải đèn thêm. Liên kết không có nghĩa mọi tầng đều phải đi qua một đèn trung gian: chi phí inference hằng ngày có thể báo trực tiếp GM cuối tháng.

**Những đèn chưa chọn:** Pipeline coverage và sales cycle tạm nằm trong CRM hỗ trợ vì ưu tiên kiểm chứng giá trị/pilot trước mở rộng sales; security/procurement vẫn ghi lý do mất deal trong CRM; usage depth chưa có mẫu workflow đã mua để đếm nhất quán; tập trung doanh thu và NRR chưa có doanh thu/cohort đủ kỳ. Những đèn này vẫn giữ nguyên kiểm kê Trạm 1, không thêm lên dashboard. Bỏ NRR khỏi 7 đèn khiến dashboard chưa phản ánh gia hạn dài hạn; cần xem lại lựa chọn sau khi có cohort trả phí đủ kỳ.

**Kiểm tra theo Prompt 5.1 (tự phản biện định nghĩa):** Không dùng “cài xong” cho TTFV; không lẫn phiên tính phí với Job hoàn thành; không lẫn p95 với bình quân; không loại pilot bỏ ngang; không dùng GM recurring để che chi phí tháng đầu. TTFV → chuyển đổi và p95 chi phí → GM có đích cụ thể, cần kiểm chứng qua log/cohort; chưa khẳng định quan hệ nhân quả. Các đèn G là bảng điểm tài chính, không đổi nhãn thành Leading vì được cập nhật thường xuyên.

**Checkpoint Trạm 2:**

- [x] Một North Star, có quy tắc xử lý shop chưa nhận giá trị.
- [x] Bảy thẻ đèn có định nghĩa, phần không đếm, công thức, nhịp và người lấy số.
- [x] Hai Leading, một đèn chi phí AI và chỉ hai Lagging.
- [x] Mọi thẻ có dòng báo trước/đích quyết định; hai Leading liên kết tới đèn được chọn.
- [x] Ngưỡng ba màu và nguồn — đã bổ sung ở Trạm 3; hai đèn [TB] còn chờ baseline nên chưa được tô màu thực tế.
- [x] Năm luật có cửa sổ quan sát, hành động, chủ trì và vế cấm; R3/R5 được bổ sung nhánh để liên kết đủ cả7 thẻ khi ráp Trạm5.

## Trạm 3 — Ngưỡng

| # | Đèn | 🟢 | 🟡 | 🔴 | Nguồn [BM]/[MH]/[TB] | Lý do (1 câu) · ngày kiểm tra nếu [BM] |
|---|---|---|---|---|---|---|
| 1 | TTFV shop chậm nhất (#1) | ≤14 ngày | >14 và ≤30 ngày | >30 ngày; shop chưa đạt nhưng tuổi chờ >30 ngày cũng kích hoạt cảnh báo đỏ | **[TB] tạm thời**; kế hoạch pilot hai tuần Day 22; lịch baseline bên dưới | Giá trị cần xuất hiện trong pilot hai tuần để kịp báo cáo và quyết định mua; 30 ngày là hạn sửa thêm trước khi mất nhịp quyết định, không phải benchmark hay runway. |
| 2 | p95 LLM + retry / phiên, shop cao nhất (#2) | x ≤ B | B < x ≤ U | x > U | **[TB] chờ baseline**: B=max p95 từng shop, U=max p99 từng shop sau hai tuần; cùng cấu hình/model/giá | So p95 mới với đuôi chi phí đã quan sát thay vì gán bình quân $0,0181872 thành p95; vượt p99 baseline là phiên đắt đã lan tới ít nhất khoảng 5% mẫu mới, cần can thiệp. |
| 3 | Containment xác nhận (#3) | ≥75% | ≥72% và <75% | <72% | **[MH-1]**; 1_Cost_Job!B9:B11; 2_Pricing!B60; B63; B66; B75 | 72% là mức tối thiểu giữ gói $120 ≤25% giá trị thời gian tránh được; 75% giữ đúng giả định mô hình và chỉ có đệm 3 điểm %, không phải bằng chứng pilot. |
| 4 | POC → paid trong 30 ngày (#4) | p ≥ Bp | Lp ≤ p < Bp | p < Lp | **[TB] chờ baseline**: Bp là tỷ lệ gộp hai cohort đủ 30 ngày; Lp là cận dưới Wilson 95% của baseline | Không lấy win rate 25% mọi cơ hội làm tỷ lệ pilot chuyển đổi; giảm dưới cận baseline là tín hiệu cần tìm nguyên nhân, không tự chứng minh quan hệ nhân quả. |
| 5 | Chi phí triển khai / ACV (#5) | ≤0,555556% tại ACV $1.440 (cost ≤$8) | >0,555556% và ≤1,388889% (cost >$8 và ≤$20) | >1,388889% (cost >$20) | **[MH-2]**; 2_Pricing!B96:B98; B101; 4_Channel_Fit!B10 | $8 là dự toán triển khai 2h×$4; vượt phí setup $20 khiến triển khai phải được trợ giá từ recurring nên dừng nhận cùng điều kiện; tính lại tỷ lệ theo ACV thật. |
| 6 | Gross Margin theo shop (#6) | GM ≥60% và GM > F | F < GM <60% | GM ≤ F; tại recurring baseline F=16,666667% | **[MH-3]**; 2_Pricing!B32; B66:B68; 1_Cost_Job!B59 | Dưới mục tiêu 60% phải sửa trong hai tuần; GM chạm F=overhead/doanh thu nghĩa là không còn phần đóng góp sau overhead dự toán, không đợi GM âm mới hành động. |
| 7 | CAC payback từ số thực (#7) | ≤P0, P0≈1,454908 tháng | >P0 và ≤6 tháng | >6 tháng; lãi gộp recurring ≤0 cũng đỏ vì không có hoàn vốn hữu hạn | **[MH-4]**; 4_Channel_Fit!B45:B50; 2_Pricing!B66:B68 | P0 là payback đúng mô hình CAC $120 và lãi gộp $82,479467; 6 tháng là trần nội bộ đã chọn trước khi scale, không dùng mức SMB12 tháng của template. |

**Quy tắc tô màu:** Chưa có số, mẫu số bằng 0 hoặc thiếu dữ liệu thì **N/A — chưa đo**, không phải xanh. Các cận dùng giá trị chính xác trong phụ lục; số làm tròn chỉ để trình bày. Đèn #2/#4 có đủ quy tắc ba màu nhưng **chưa có cận số đo được**, nên chưa vận hành như ngưỡng đã hiệu chuẩn. Màu vàng mở việc điều tra có người phụ trách và hạn 14 ngày; đỏ là đầu vào luật Trạm 4. Số quan sát/thời gian duy trì sẽ được ràng buộc trong luật để tránh phản ứng với mẫu nhỏ.

**Không sử dụng [BM] ở bộ 7 đèn này.** Các con số benchmark trong handbook không được chép làm ngưỡng sản phẩm. Ngày đối chiếu nguồn nội bộ **09/10/2026**; ngày 08/10 trong workbook là ngày kiểm tra do bài Day 22 ghi, không phải lần kiểm tra web mới.

### Lịch đo [TB] — chưa có chuẩn, đo hai chu kỳ rồi lấy làm baseline

| Đèn | Hai chu kỳ / bằng chứng cần thu | Ngày dự kiến khóa baseline | Cách chốt và giới hạn |
|---|---|---|---|
| #1 TTFV | Hai cohort triển khai đề xuất 26/10–08/11 và 09/11–22/11; timestamp ký, xác nhận giá trị đầu tiên và tuổi chờ mọi shop | **23/11/2026**, nếu có hai cohort thật; cohort thứ hai chưa được tuyển | Giữ mốc tạm 14/30 ngày dựa trên nhịp pilot/sửa; đối chiếu phân phối thực, không dời cận để biến shop chậm thành xanh. Chưa có cohort thì công khai hoãn baseline. |
| #2 p95 LLM + retry | Hai tuần 26/10–01/11 và 02/11–08/11; phiên hợp lệ, mọi call/retry/cache có `session_id` và giá áp dụng; chỉ chốt phiên đã đóng, không bỏ phiên lỗi | **09/11/2026**, nếu pilot có log đầy đủ | Gộp hai tuần **trong từng shop**, tính p95/p99 bằng nearest-rank; B=max p95_shop, U=max p99_shop. Không gộp shop trước khi tính phân vị. Hai tuần baseline bị khóa, không cuốn theo tuần đang đánh giá; đổi model/giá/phạm vi phải lập baseline mới và ghi lý do. |
| #4 POC → paid | Hai cohort pilot kết thúc 08/11 và 22/11; tất cả shop trong mỗi cohort phải đủ cửa sổ 30 ngày, gồm ca dừng pilot | **23/12/2026**, sau 08/12 và 22/12; chưa có shop xác nhận nên ngày này có điều kiện | Bp=100×k/n của hai cohort baseline; Lp=100×WilsonLower(k,n). Khóa baseline, chỉ so cohort mới đủ thời hạn; không dùng chính cohort tạo baseline để tuyên bố đạt tăng trưởng. n=0 hoặc Bp=0: chưa hiệu chuẩn được ngưỡng phân biệt, không tự cho xanh. |

Các ngày trên là lịch thực hiện dự kiến, không cam kết có dữ liệu. Chưa tuyển được pilot hoặc mẫu quá nhỏ thì ghi N/A và báo thiếu bằng chứng ở cổng gác. Với #2, n<20 khiến p95 gần max; p99 cần khoảng 100 phiên mới bắt đầu có ý nghĩa phân vị thay vì gần max. Với #4, ít shop làm cận Wilson rất rộng; ghi k/n và cận, không dùng tỷ lệ đẹp để scale.

**Công thức baseline TB:** Nearest-rank `Qq = c_(ceil(q×n))` sau sắp xếp tăng dần. Với POC baseline, `phat=k/n`, `z=1,96`, `WilsonLower = [phat + z²/(2n) − z×sqrt(phat×(1−phat)/n + z²/(4n²))] / [1+z²/n]`. Đây là quy tắc đo được chọn cho dự án, không phải benchmark và chưa có B/U/Bp/Lp thực tế.

### Phụ lục [MH] — phép tính (≥2)

**[MH-1] — Containment: mức giữ neo giá trị cho shop, không phải ngưỡng GM**

```
Đầu vào Day 22:
R = $120/shop/tháng (2_Pricing!B66)
N = 1.000 phiên thử/shop/tháng (1_Cost_Job!B9)
m = 10 phút lao động tránh được/Job hoàn thành (2_Pricing!B60)
w = $4/giờ (1_Cost_Job!B50)
a = 25% giá trị thời gian dùng neo giá (2_Pricing!B63)
r0 = 75% containment dự toán (1_Cost_Job!B10)
Giá trị tránh được = N × r × m/60 × w.
Điều kiện neo giá: R ≤ a × N × r × m/60 × w.
r_min = 120 / (0,25 × 1.000 × 10/60 × 4) = 0,72 = 72%.
Ở 72%: 720 Job ×10/60×$4 = $480; 25%×$480 = $120.
Ở 75%: giá trị $500, trần giá $125; đệm giá chỉ $5.
→ Xanh r≥75%; vàng 72%≤r<75%; đỏ r<72%.
Nếu N/m/w/giá đã thỏa thuận thay đổi: tính lại r_min; không giữ 72% máy móc.
Nếu r_min>100%: offer không giữ được neo giá, không có mức xanh khả thi.
Thời gian tránh được và 25% willingness-to-pay chưa được shop xác nhận.
Hybrid/HITL A giữ hóa đơn theo quota: không dùng công thức Outcome B33.
```

**[MH-2] — Chi phí triển khai / ACV: giữ ngân sách triển khai và không trợ giá setup**

```
Đầu vào: 2 giờ onboarding ×$4/giờ = $8 (2_Pricing!B96:B98).
Phí setup = $20 một lần (2_Pricing!B101).
ACV quy đổi recurring = 12×$120 = $1.440 (4_Channel_Fit!B10).
Ngân sách xanh = $8/$1.440×100 = 0,555555...%.
Trần trước trợ giá = $20/$1.440×100 = 1,388888...%.
→ Xanh cost≤$8; vàng $8<cost≤$20; đỏ cost>$20.
Tương ứng tỷ lệ: ≤0,555556%; (0,555556%;1,388889%]; >1,388889%.
Mỗi shop dùng ACV và phí setup thực đã thống nhất để tính lại cận.
Nếu chi phí tích hợp phát sinh thì cộng vào cost; không coi giờ founder miễn phí.
ACV quy đổi năm không chứng minh có hợp đồng ràng buộc 12 tháng.
Đỏ là dừng nhận cùng điều kiện để sửa cách triển khai/giá, không khẳng định toàn mô hình đã lỗ.
```

**[MH-3] — Gross Margin: mục tiêu COGS và sàn còn trang trải overhead**

```text
Đầu vào: recurring R=$120, COGS=$37,520533333... (2_Pricing!B66:B68);
GM mục tiêu=60% (2_Pricing!B32); overhead O=$20/shop/tháng (1_Cost_Job!B59).
COGS tối đa để đạt mục tiêu = R×(1−0,60) = $48.
GM dự toán = 1−37,520533333/120 = 68,7328889%.
Sàn đóng góp sau overhead: R×GM−O=0 ⇒ F=O/R=20/120=16,6666667%.
→ Xanh GM≥60% và GM>F; vàng F<GM<60%; đỏ GM≤F.
Tại F: COGS=$100, lãi gộp=$20; trừ overhead còn $0.
Không trừ overhead trong công thức GM: overhead chỉ dùng suy sàn hành động.
Baseline margin sau overhead = (120−37,520533333−20)/120 = 52,0662222%.
Tháng đầu: R=$140 gồm setup; COGS=$45,520533333 gồm onboarding;
GM=67,4853333%, F=20/140=14,2857143%; dùng kỳ và nguồn tương ứng.
Nếu R/O thay đổi thì F thay đổi. Nếu F≥60%, vùng vàng như bảng không còn tồn tại:
ưu tiên đỏ khi GM≤F, không tô xanh chỉ vì đã đạt 60%.
Sàn đỏ là điểm không còn đóng góp sau overhead dự toán, không phải runway/NPV.
Lỗ pilot miễn phí: GM N/A, chi phí vẫn ghi ledger và ngân sách pilot.
```

**[MH-4] — CAC payback: bám baseline và trần nội bộ sáu tháng**

```text
Đầu vào: CAC dự toán=$600/(20×25%)=$120 (4_Channel_Fit!B45:B48).
ARPU recurring=$120; GM=68,7328889%; lãi gộp=120−37,520533333=$82,479466667.
P0 = 120/82,479466667 = 1,454907564873 tháng (4_Channel_Fit!B49).
Trần nội bộ T=6 tháng (4_Channel_Fit!B50).
CAC tối đa ở baseline = 6×82,479466667=$494,8768.
→ Xanh payback≤P0; vàng P0<payback≤6; đỏ payback>6.
Với lãi gộp thực GP_real>0: trần CAC thực = 6×GP_real, không giữ $494,8768 nếu GM đổi.
Lãi gộp≤0: không có payback hữu hạn, báo đỏ.
Cohort chưa có khách trả phí: CAC/payback chưa xác định, không ghi 0.
Không cộng setup một lần vào ARPU recurring; không dùng trần12 tháng $989,7536.
Không khẳng định sáu tháng phù hợp runway: runway chưa có và phải bổ sung.
```

**Phản biện theo Prompt 5.2:** Bốn đèn [MH] có công thức và đầu vào truy được về Day 22; #1 là SLA thử nghiệm có lý do theo nhịp pilot, chưa phải lịch sử. #2 và #4 chưa có baseline số nên lịch đo là bằng chứng hiện có, không được giả vờ đã hiệu chuẩn. Ngưỡng dễ sai nhất là containment72%: nó phụ thuộc 10 phút/Job, $4/giờ và neo25% đều chưa được shop xác nhận; time study có thể làm r_min vượt100%. Đèn p95 không bảo đảm ngân sách tổng API vì không đo độ lớn của top5%; phải đối soát tổng cost của #6, không coi p95 xanh là GM chắc xanh. Ngưỡng đỏ GM khá muộn nên dưới60% phải điều tra/sửa ngay ở màu vàng.

**Checkpoint Trạm 3:**

- [x] Bảy đèn có quy tắc xanh/vàng/đỏ, ký hiệu nguồn và câu lý do; dữ liệu thiếu giữ N/A.
- [x] Bốn ngưỡng [MH] có đầu vào, công thức và phép tính đầy đủ, nhiều hơn mức tối thiểu hai.
- [x] Không dùng [BM] nên không có benchmark thiếu ngày kiểm tra; đã ghi ngày đọc nguồn nội bộ.
- [x] Các [TB] ghi chưa có chuẩn, hai chu kỳ và ngày dự kiến; #2/#4 còn thiếu cận số thực cho đến khi có baseline.
- [ ] Chốt các cận baseline [TB] bằng dữ liệu thật theo lịch; hiện chưa thể tuyên bố dashboard đã vận hành.

## Trạm 4 — 5 luật quyết định

**Năm luật ưu tiên:** #1→R1, #2→R2, #3/#4→R3, #5→R4, #6/#7→R5. Khi ráp Trạm 5, bổ sung nhánh POC đỏ vào R3 và GM đỏ vào R5 để mọi thẻ có hành động liên kết, vẫn giữ đúng năm luật. Chủ trì thực thi: **Đỗ Trọng Bình**; chủ shop duyệt mọi thay đổi phạm vi vận hành trên shop của mình. Luật được viết trước, chưa có luật nào đã kích hoạt từ dữ liệu thực. ⏹ là dừng một việc cụ thể, không phải dừng toàn bộ dự án.

**Cách đọc KHÔNG THÌ:** Trong lab, đây là **lời cấm phản xạ sai**, không phải nhánh “nếu điều kiện sai thì làm ngược lại”. Không dùng việc chưa đủ mẫu để tự cho phép scale. Mọi ngưỡng là đúng cận Trạm 3; khi giá/volume/chi phí đã được xác nhận đổi, tính lại cận có lưu phiên bản, không sửa cận chỉ để né đỏ.

1. **⏹ R1 — TTFV: dừng nhận pilot rộng hơn. NẾU** TTFV shop chậm nhất hoặc tuổi chờ của ít nhất một shop trong 3 thỏa thuận gần nhất **>30 ngày**, **TRONG** 3 lần kiểm tra ngày liên tiếp, **VÀ** ngày ký và trạng thái chưa nhận giá trị đã được đối chiếu với shop (không yêu cầu đủ 3 shop mới được hành động), **THÌ** Đỗ Trọng Bình **dừng nhận pilot rộng hơn ngay trong ngày**, trong 48 giờ thống nhất với shop chậm cắt pilot xuống **một workflow hỏi size/tồn kho của một nhóm sản phẩm**, sửa quyền Page/catalog/luồng chuyển người trong 7 ngày và lấy xác nhận giá trị trong 14 ngày; **KHÔNG THÌ** **không giảm giá, tuyển sales hoặc ký thêm pilot rộng để bù việc shop cũ chưa nhận giá trị**.

2. **⏹ R2 — Chi phí AI: dừng luồng tốn token tại shop bị ảnh hưởng. NẾU** p95 LLM + retry/phiên của ít nhất một shop **>U** (đúng cận đỏ [TB] #2), **TRONG** 2 tuần lịch liên tiếp, **VÀ** mỗi tuần của shop đó có **≥100 phiên hợp lệ đã đóng**, baseline B/U được khóa từ hai tuần trước đó với **≥100 phiên/shop baseline**, cùng model/giá/phạm vi, log đã gồm mọi retry/cache và đã đối soát cost, **THÌ** Đỗ Trọng Bình **dừng luồng tạo đơn nhiều tool-call ở shop đó trong 24 giờ**, chuyển yêu cầu thuộc luồng này về nhân viên shop, trong 48 giờ truy vết 10 phiên đắt nhất rồi sửa giới hạn call/cache/context và chạy lại Eval trước mở lại; **KHÔNG THÌ** **không âm thầm thu phí vượt gói, nâng model đắt hơn hoặc bỏ retry/lỗi khỏi log để làm chi phí trông thấp**.

3. **⏹ R3 — Containment: dừng mở rộng offer chưa giữ được giá trị. NẾU** containment được khách xác nhận của ít nhất một shop **<72%** tại đầu vào Day 22 (hoặc **<r_min** đã tính lại theo giá/volume/time study của shop), **TRONG** 2 cohort tuần liên tiếp, **VÀ** mỗi cohort có **≥100 phiên thử hợp lệ**, mọi phiên đã đóng và qua cửa sổ mở lại 24 giờ, **cận trên Wilson 95% của hai cohort gộp vẫn <r_min**, **THÌ** Đỗ Trọng Bình **dừng chào bán cùng offer cho shop mới ngay buổi họp tuần**, trong 48 giờ phân loại 20 Job lỗi/bỏ ngang/chuyển người, cùng shop chọn một nguyên nhân sửa trong 7 ngày, thử phạm vi hẹp thêm 14 ngày rồi tính lại giá trị thời gian tránh được; **KHÔNG THÌ** **không gọi ca chuyển người/bỏ ngang là hoàn thành, đổ thêm tiền tìm khách hoặc hứa tăng doanh thu để thay bằng chứng tiết kiệm**.

4. **⏹ R4 — Triển khai: dừng nhận cùng điều kiện khi setup cần trợ giá. NẾU** chi phí triển khai/ACV recurring của một shop **>1,388889% tại ACV $1.440**, tương đương **COGS triển khai >phí setup $20** (cận tính lại theo ACV và setup fee thực đã thống nhất), **TRÊN** một shop đang triển khai khi chi phí lũy kế đã vượt trần hoặc một shop vừa go-live, **VÀ** time log/cost đã đối soát, có giá recurring và phí setup được shop chấp nhận, **THÌ** Đỗ Trọng Bình **dừng nhận shop mới với cùng phạm vi và phí setup ngay trong ngày**, trong 48 giờ lập mẫu import catalog và checklist quyền Page, cắt một bước tùy biến không cần thiết, báo phạm vi/phí mới để shop mới đồng ý trước khi bắt đầu; hoàn tất nghĩa vụ hiện hữu theo thỏa thuận; **KHÔNG THÌ** **không coi công founder là miễn phí, giảm phí setup hay chuyển chi phí triển khai vào R&D để né ngưỡng**.

5. **⏹ R5 — Payback: đóng băng acquisition khó quay vòng. NẾU** CAC payback từ dữ liệu thực **>6 tháng**, hoặc **lãi gộp recurring ≤0** khiến không có hoàn vốn hữu hạn, **TRÊN** một cohort acquisition đã đóng và một tháng recurring hoàn tất dùng để tính lãi gộp, **VÀ** cohort có **≥1 shop trả recurring**, đã hạch toán toàn bộ chi phí acquisition kể cả cơ hội thua, tách onboarding/setup và đối soát ledger, **THÌ** Đỗ Trọng Bình **đóng băng chi tiêu acquisition mới, tuyển sales và mở thêm ngách trong 24 giờ**, dành 14 ngày sửa một đòn bẩy có số (giờ prospecting, tỷ lệ chuyển đổi hoặc COGS recurring), lập lại CAC budget bằng **6×lãi gộp recurring thực** và chỉ thử lại một cohort nhỏ trong ngân sách được chốt; **KHÔNG THÌ** **không giảm giá để kéo số khách thắng, tăng ngân sách quảng bá, cộng setup vào ARPU hoặc giấu chi phí cơ hội thua để rút ngắn payback**.

### Bằng chứng thực thi và điều kiện gỡ lệnh dừng

| Luật | Bằng chứng phải lưu | Điều kiện gỡ / phạm vi hạn chế tiếp tục |
|---|---|---|
| R1 | Timestamp ký và tuổi chờ, biên bản thu hẹp một workflow, log Job + shop xác nhận phút tiết kiệm | Shop bị chậm đã nhận giá trị và hoàn tất checklist triển khai hẹp; chỉ nhận pilot cùng phạm vi đã sửa. Không sửa TTFV lịch sử hoặc xóa shop chậm khỏi cohort; mở rộng phạm vi phải chờ cổng gác. |
| R2 | Snapshot B/U có phiên bản, số phiên từng tuần, token/cost log, 10 trace đắt nhất, kết quả Eval luồng đã sửa | Chạy lại Eval không có lỗi nghiêm trọng; một tuần có ≥100 phiên cùng phạm vi được phép chạy kiểm chứng với p95≤B và tổng cost đã đối soát. Luồng bị dừng chuyển người hoặc replay/Eval cho đến khi shop đồng ý thử có giám sát; không tự tăng quota. |
| R3 | Hai cohort, k/n và Wilson upper, danh sách 20 ca thất bại, time study trước/sau được shop xác nhận | Một cohort kiểm chứng 14 ngày, ≥200 phiên đủ cửa sổ, tỷ lệ đạt ngưỡng xanh đã tính lại và cận dưới Wilson95%≥r_min; shop xác nhận giá trị. Nếu không đạt sau một lần sửa, đưa vấn đề vào PIVOT/KILL ở cổng Trạm 5, không sửa vô hạn. |
| R4 | Time log gồm công founder, chi phí tích hợp, ACV/setup đã thống nhất, mẫu import/checklist và báo giá mới | Một triển khai phạm vi chuẩn có COGS≤phí setup và ngân sách giờ công được kiểm chứng; chỉ nhận cùng phạm vi/giá đã thỏa thuận, không quay lại offer cũ chưa có lãi setup. |
| R5 | Ledger cohort đã đóng, số khách thắng, recurring GP, CAC/payback và kế hoạch thử cohort nhỏ | Một cohort thử mới đã đóng, có ≥1 khách trả recurring và một tháng recurring đủ dữ liệu, payback≤6 tháng, GP>0; chỉ gỡ ngân sách đã duyệt ở cổng, không coi forecast là hoàn vốn đã xảy ra. |

**Điều kiện mẫu là thiết kế thử nghiệm, không phải benchmark:** Với R2, chọn ≥100 phiên để p95 có khoảng 5 quan sát ở đuôi thay vì sát max; hai tuần không chồng lấn tránh một ngày bất thường. Với R3, ≥100 mỗi tuần và Wilson upper dưới r_min tránh dừng offer chỉ do sai số mẫu; Wilson lower để gỡ yêu cầu bằng chứng mạnh hơn. Wilson upper dùng công thức Trạm 3 thay dấu trừ trước căn bằng dấu cộng. R1/R4 không chờ 3 shop: shop đầu tiên chậm hoặc vượt phí cũng gây tổn thất thật. R5 là phép tính sổ sách, không suy hiệu quả bán hàng từ mẫu một khách để tự scale.

**Bổ sung nhánh khi ráp Trạm 5:** R3 cũng kích hoạt **NẾU #4 POC→paid<Lp TRÊN một cohort mới đủ 30 ngày, VÀ ≥5 shop, Bp/Lp baseline khóa và chứng từ trả recurring đối soát**; Bình dừng chào cùng offer ở họp tuần, chốt một nguyên nhân trong 48 giờ (time study, TTFV hoặc offer), sửa trong 7 ngày và thử phạm vi hẹp 14 ngày; KHÔNG THÌ không hạ giá để che thiếu giá trị. Hai nhánh R3 là **HOẶC**, mỗi nhánh giữ cửa sổ/mẫu riêng, không yêu cầu cả hai cùng đỏ. Gỡ nhánh POC chỉ khi cohort mới đủ kỳ đạt p≥Bp; baseline không được cuốn theo cohort mới. R5 cũng kích hoạt **NẾU #6 GM≤F TRONG một tháng đã khóa sổ có doanh thu, VÀ ledger đối soát**, dù payback chưa xác định hoặc chưa đỏ; hành động/cấm giữ như R5, ưu tiên sửa COGS/giá của shop bị ảnh hưởng. Gỡ nhánh GM khi kỳ mới có GM≥60% và >F; không trộn doanh thu/COGS shop để che shop lỗ. Hai nhánh R5 cũng là HOẶC. Các luật trên và dashboard đọc cùng phần bổ sung này.

**Liên kết thẻ đèn → luật cuối cùng:** #1→R1; #2→R2; #3/#4→R3; #5→R4; #6/#7→R5. Các ngưỡng màu đỏ khớp Trạm 3, không phát sinh luật thứ sáu.

### Phản biện theo Prompt 5.3 và 5.4

| Luật | Tình huống dễ bắn nhầm / không bắn | Cách chống lách và phản xạ bị cấm |
|---|---|---|
| R1 | Shop chậm cấp quyền/dữ liệu làm TTFV>30 dù AI tốt; tác động vẫn là chưa nhận giá trị. Nếu chỉ lấy shop đã thành công thì luật không bao giờ bắn. | Ghi rõ nguyên nhân phía shop, cắt phạm vi theo thỏa thuận; giữ ngày ký và mọi shop trong cohort. Không giảm giá/mua thêm deal để che tắc triển khai. |
| R2 | Một phiên đắt riêng lẻ có thể bình thường; top1% cực đắt vẫn có thể làm tổng cost cao dù p95 chưa đỏ. | Hai tuần ≥100 phiên và baseline khóa; không bỏ retry. GM và tổng cost đối soát vẫn phải đọc, p95 không bảo đảm ngân sách tổng; không âm thầm chuyển phí sang shop. Chưa có baseline thì luật chưa thể kích hoạt, không giả định xanh. |
| R3 | Shop có ít phiên hoặc khách bỏ ngang do lý do ngoài AI; đổi catalog/phạm vi làm mẫu khác nhau. Sai giá/tồn kho nghiêm trọng có thể xảy ra dù containment cao. | Đếm mọi phiên hợp lệ, xác minh điều kiện so sánh và time study; kiểm tra Wilson, không gọi handoff là completed. Correctness/Eval vẫn là điều kiện triển khai theo Day22, không coi tỷ lệ này thay thế kiểm tra lỗi nghiêm trọng. |
| R4 | Shop cố ý mua custom scope có phí cao hơn khiến chi phí>$20 nhưng vẫn được trả đủ. | Tính theo setup fee/ACV đã thống nhất của chính shop, không áp $20 máy móc; cấm giấu giờ founder. Không hủy nghĩa vụ với shop cũ; dừng offer mới có cùng điều kiện không còn phù hợp. |
| R5 | Cohort chưa đóng hoặc lấy doanh thu setup làm ARPU sẽ cho payback sai; chờ hai tháng có thể tiêu tiền quá lâu. | Một kỳ sổ đã hoàn tất đủ kích hoạt; hạch toán cả cơ hội thua, phân biệt ước tính với hoàn vốn lũy kế. Dừng ngân sách mới nhưng vẫn phục vụ khách và thử sửa có giới hạn. |

**Khoảng trống còn thật:** Chưa có luật độc lập cho security/procurement; chưa có runway để bảo đảm trần payback6 tháng phù hợp tiền mặt. Giữ log lý do mất deal và yêu cầu tiền mặt/net burn; không bịa runway hoặc coi 90 ngày kế hoạch là khả năng tài trợ đã xác nhận. R2 và nhánh POC của R3 chưa vận hành được khi baseline chưa có.

**Checkpoint Trạm 4:**

- [x] Đúng 5 luật, mỗi luật có NẾU / TRONG-TRÊN / THÌ / KHÔNG THÌ và điều kiện mẫu cần thiết.
- [x] Cả 5 luật có ⏹ và nêu rõ việc dừng; vượt mức tối thiểu 2.
- [x] Ngưỡng kích hoạt khớp Trạm 3, không dùng benchmark mẫu thay số dự án.
- [x] Mỗi hành động có Đỗ Trọng Bình chủ trì, thời điểm bắt đầu và bằng chứng gỡ lệnh dừng.
- [x] Không vế THÌ nào kết thúc bằng “xem xét lại / cân nhắc / theo dõi thêm”.

## Trạm 5 — Cổng gác 90 ngày và bản in

**Ngày 1 = 09/10/2026**, đếm cả ngày bắt đầu: ngày30 **07/11/2026**, ngày60 **07/12/2026**, ngày90 **06/01/2027**. Ngày 30 là cổng học, không dùng doanh thu. Ngày 90 là hạn cứng của offer hiện tại, không tự gia hạn bởi FIX. Các cổng là kế hoạch quyết định, chưa có bằng chứng đã đạt.

| Cổng | Một metric duy nhất và ngưỡng GO | Định nghĩa/bằng chứng vật lý phải tồn tại | Quyết định khi trượt |
|---|---|---|---|
| Ngày30 · 07/11 | **Số shop có time study hợp lệ ≥2** | `evidence/time-study.csv` và xác nhận shop: mỗi shop ≥20 yêu cầu mua hàng thật có phút lao động trước/sau, nguồn timestamp và công việc tương đương; loại thời gian chờ khách, dùng mẫu đại diện chứ không chỉ Job thành công. Lưu dữ liệu ẩn danh. Pilot có thể đang chạy, chưa cần kết thúc hoặc có doanh thu. | **FIX** một lần trong30 ngày: sửa một nguyên nhân thu dữ liệu (log hoặc quy trình xác nhận). **PIVOT** nếu không xác nhận được nhu cầu ca ngoài giờ/giá trị tiết kiệm; **KILL** nếu vấn đề đã FIX một lần vẫn không tiến bộ. |
| Ngày60 · 07/12 | **Số shop nhận giá trị đầu tiên với TTFV≤14 ngày ≥2** | `evidence/first-value.csv`: shop_id, ngày ký, xác nhận giá trị/Job log, phút tránh được; giữ shop chưa đạt và tuổi chờ. Hai shop độc lập, không đếm hai tài khoản cùng shop. Phải dùng định nghĩa TTFV Trạm2. | **FIX** một lần trong30 ngày: sửa đúng một nút onboarding, phạm vi giữ một workflow. **PIVOT** nếu use case/catalog không tạo được giá trị; **KILL** nếu cùng vấn đề đã FIX vẫn không tiến bộ. |
| Ngày90 · 06/01/2027 | **Số shop thanh toán recurring kỳ thứ hai ≥3** | `evidence/renewals.csv` và chứng từ kỳ1/kỳ2 cùng shop, hai kỳ cung cấp dịch vụ liên tiếp. Không tính phí setup, lời hứa gia hạn, khách trial hoặc khoản thu trước chưa tới kỳ cung cấp dịch vụ. | **KILL offer hiện tại** khi <3 theo hạn cứng; không dùng FIX để kéo quá ngày90. Có ≥3 thì GO bước nhỏ, vẫn phải tôn trọng lệnh dừng ngân sách/cost. |

**Lý do các ngưỡng:** Hai shop giữ quy mô pilot Day22 và tránh chỉ học từ một trường hợp. ≥20 yêu cầu/shop là mức time study tối thiểu đề xuất để bắt đầu so sánh, không là chứng minh đại diện thống kê; phân phối ca vẫn phải báo cáo. TTFV14 ngày bám cửa sổ pilot hai tuần và thử tính lặp lại trên hai shop. Ba shop trả kỳ2 là mức tối thiểu đề xuất để có tín hiệu giá trị lặp lại, thấp hơn mục tiêu năm shop trả phí đầu kỳ của Day22 nhưng không chấp nhận chỉ một khách đặc biệt. Các cổng không phải benchmark hoặc kết quả đã đạt; gia hạn3/5 không được gọi là NRR60%.

**KILL CRITERIA:** Đến **06/01/2027**, nếu có **<3 shop thanh toán recurring kỳ thứ hai**, dừng offer AI trực inbox thời trang hiện tại và chi tiêu acquisition, bàn giao khách theo thỏa thuận.

**Quy tắc GO / FIX / PIVOT / KILL:**

- **GO:** Metric đạt và bằng chứng có thật; sang bước kế tiếp trong ngân sách. Một cổng đạt không gỡ lệnh dừng từ R1–R5. Chưa có runway thì không tự tăng tổng ngân sách/chi tiêu hoặc tuyển người.
- **FIX:** Metric chưa đạt, xác định một nguyên nhân có thể sửa và vấn đề chưa FIX lần nào. Ghi `problem_id`, metric, nguyên nhân, một hành động, người làm, deadline30 ngày và cùng ngưỡng nghiệm thu; kiểm tra lại đúng deadline, song song cổng tiếp theo, không dời ngày90.
- **PIVOT:** Bằng chứng bác bỏ giả định gốc, kể cả sau một lần FIX có tiến bộ nhưng use case/offer vẫn sai. Chốt thay đổi ICP/phạm vi/Value Metric và ngân sách thử nhỏ; không reset FIX bằng đổi tên metric. Một offer mới cần kế hoạch đo riêng, không tiếp tục gọi offer cũ là đã qua cổng.
- **KILL:** Cùng vấn đề đã FIX một lần vẫn không tiến bộ so với giá trị trước sửa, hoặc chạm kill criteria ngày90. Dừng acquisition/triển khai mới, hoàn tất bàn giao/nghĩa vụ hiện hữu; không xóa bằng chứng thất bại. PIVOT là lựa chọn khi có giả định thay thế cụ thể, không phải trì hoãn KILL của offer cũ.

**Nhật ký cổng:** Dự kiến tạo `evidence/gate-log.csv` khi họp, gồm ngày, problem_id, metric/value/sample, link bằng chứng, quyết định, fix_count, người phụ trách và hạn. Các tên file evidence trong bài là yêu cầu đầu ra tương lai, **chưa tồn tại/chưa có kết quả**. Bình chủ trì, mời một người ngoài xem bằng chứng tại cổng; chưa ghi người đó đã tham dự.

**Chưa đo được:** Cả7 đèn; chưa có B/U/Bp/Lp thực. Chuẩn bị CRM/event và time log trước23/10; pilot dự kiến từ26/10; baseline p95 dự kiến09/11, TTFV23/11, POC23/12 đều phụ thuộc hai chu kỳ thật. GM/payback chờ kỳ doanh thu/COGS đủ dữ liệu. Runway cần tiền mặt khả dụng và net burn cùng ngày chốt; không thay thiếu bằng0 hoặc90 ngày kế hoạch. Source Day22 là dự toán, không dùng để xác nhận GO.

**Đóng gói:** dashboard.md là bản nguồn cô đọng; dashboard.pdf trang1 là dashboard A4 ngang, trang2 là phụ lục bốn phép tính [MH]. Bản in HTML được tạo từ cùng dashboard.md để in một mặt giấy. Worksheet giữ định nghĩa chi tiết, phản biện, điều kiện mẫu/gỡ lệnh dừng; không nhồi chúng lên trang1.

**Checkpoint Trạm 5:**

- [x] Ba cổng có ngày cụ thể, mỗi cổng đúng một metric, ngưỡng số và bằng chứng phải tồn tại.
- [x] Cổng30 đo học từ time study, không đo doanh thu.
- [x] Có GO/FIX/PIVOT/KILL, FIX chỉ một lần cho một vấn đề và kill criteria có số/ngày.
- [x] Dashboard có7 đèn/3 tầng,5 luật và Chưa đo được có phương pháp/lịch.
- [x] Đã kiểm tra PDF đúng2 trang: dashboard ở trang1 A4 ngang, bốn phép tính [MH] ở trang2; render không thấy cắt chữ/lỗi font. Bản HTML in thử từ cùng dashboard.md cũng đúng1 trang, đã kiểm tra ảnh.
- [ ] Runway và baseline được xác nhận bằng số thực — chưa có dữ liệu, không tự đánh dấu hoàn tất.
