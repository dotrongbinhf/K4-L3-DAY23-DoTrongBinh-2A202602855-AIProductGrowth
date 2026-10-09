# OPERATING DASHBOARD — AI trực inbox shop thời trang

**Đỗ Trọng Bình · 2A202602855 · 09/10/2026.** **B2B:** chủ shop là người mua mục tiêu, shop/nhân viên vận hành; điểm chạm người mua cuối dự kiến trong Messenger của shop, chưa có quyền tiếp cận độc lập/thương hiệu riêng. Ý tưởng, chưa có MVP/pilot xác nhận.

**NORTH STAR:** TTFV shop chậm nhất trong 3 thỏa thuận gần nhất; mục tiêu **≤14 ngày [TB]**. Hiện **chưa đo**. Shop chưa nhận giá trị: giữ tuổi chờ, không loại khỏi cohort. Giá trị = Job thật đúng/khách xác nhận/không cần người, shop xác nhận phút tiết kiệm, qua cửa sổ mở lại 24h.

### Leading — kiểm tra ngày, chốt tuần

| Đèn · hiện tại | 🟢 / 🟡 / 🔴 | Nguồn · lý do · báo trước / luật |
|---|---|---|
| **#1 TTFV**, chưa đo | ≤14 / >14–30 / >30 ngày, kể cả tuổi chờ | [TB] tạm: nhận giá trị trong pilot 2 tuần, hạn sửa đến 30 ngày; →#4/#7, **R1** |
| **#2 p95 LLM + retry/phiên**, shop cao nhất; chưa đo | x≤B / B<x≤U / x>U | [TB] B=max p95_shop, U=max p99_shop của 2 tuần baseline; bắt đuôi chi phí →#6, **R2** |

### Operating — kiểm tra tuần / cohort

| Đèn · hiện tại | 🟢 / 🟡 / 🔴 | Nguồn · lý do · báo trước / luật |
|---|---|---|
| **#3 Containment xác nhận**, shop thấp nhất; chưa đo | ≥75% / 72–<75% / <72% | [MH-1] 72%=120/(1.000×10/60×4×25%); giữ neo giá trị, 75% bám mô hình →#4, **R3** |
| **#4 POC→paid sau 30 ngày**, chưa có cohort | p≥Bp / Lp≤p<Bp / p<Lp | [TB] Bp=tỷ lệ 2 cohort, Lp=Wilson lower 95%; tránh lẫn win rate →#7, **R3** |
| **#5 Triển khai/ACV**, shop cao nhất; chưa đo | ≤0,555556% / >0,555556–1,388889% / >1,388889% | [MH-2] $8/$1.440 là ngân sách; $20/$1.440 là setup hòa vốn; →#6, **R4** |

### Lagging — chốt tháng / cohort

| Đèn · hiện tại | 🟢 / 🟡 / 🔴 | Nguồn · lý do · đích / luật |
|---|---|---|
| **#6 GM/shop**, shop thấp nhất; chưa đo | ≥60% và >F / F<GM<60% / GM≤F | [MH-3] F=overhead/revenue=16,666667% recurring baseline; sàn đóng góp →#7, **R5** |
| **#7 CAC payback**, chưa đo | ≤P0 / P0<p≤6 / >6 tháng hoặc GP≤0 | [MH-4] P0=120/82,479467≈1,454908 tháng; CAC trần 6 tháng=$494,8768; tiền mặt, **R5** |

**Cận dùng số chính xác.** #3/#5/#6 tính lại khi đầu vào đổi; GP=lãi gộp recurring. Thiếu số/cận: **N/A**, không xanh. Vàng: Bình điều tra trong 14 ngày. Chi tiết: worksheet.md; nguồn Day 22 đối chiếu 09/10/2026, không dùng [BM].

### 5 luật — Bình chủ trì; ⏹ = dừng; shop duyệt phạm vi

1. **⏹ R1 NẾU** TTFV/tuổi chờ >30 ngày **TRONG** 3 kiểm tra ngày **VÀ** timestamp xác minh, **THÌ** dừng nhận pilot rộng ngay ngày đó, thu hẹp 1 workflow trong 48h, lấy giá trị trong 14 ngày; **KHÔNG THÌ** không giảm giá/tuyển sales/ký pilot rộng để bù chậm.
2. **⏹ R2 NẾU** p95>U **TRONG** 2 tuần liên tiếp **VÀ** mỗi tuần ≥100 phiên, baseline khóa/log đủ/cùng cấu hình, **THÌ** dừng luồng nhiều call ở shop đó trong 24h, chuyển người, sửa 10 trace đắt nhất; **KHÔNG THÌ** không thu vượt gói âm thầm/nâng model/bỏ retry khỏi log.
3. **⏹ R3 NẾU** containment<72% (hoặc r_min mới) **TRONG** 2 cohort tuần **VÀ** mỗi cohort ≥100 phiên đủ 24h, Wilson upper gộp<r_min; **HOẶC** POC→paid<Lp **TRÊN** 1 cohort mới đủ 30 ngày, ≥5 shop và baseline khóa, **THÌ** dừng chào cùng offer ở họp tuần, chốt 1 nguyên nhân trong 48h, sửa 7 ngày/thử hẹp 14 ngày; **KHÔNG THÌ** không tính handoff thành completed/mua thêm khách/hạ giá để che thiếu giá trị.
4. **⏹ R4 NẾU** triển khai/ACV>1,388889% (cost>setup thực) **TRÊN** 1 shop **VÀ** time log/giá đối soát, **THÌ** dừng nhận cùng điều kiện trong ngày, chuẩn hóa catalog/quyền Page và chốt scope/phí mới trong 48h; **KHÔNG THÌ** không miễn phí công founder/giảm setup/giấu công vào R&D.
5. **⏹ R5 NẾU** payback>6 tháng hoặc GP≤0 **TRÊN** 1 cohort đóng + 1 tháng recurring đủ số, có ≥1 shop trả phí; **HOẶC** GM≤F **TRONG** 1 tháng có doanh thu, **VÀ** ledger đối soát, **THÌ** đóng băng acquisition/tuyển sales/ngách mới trong 24h, sửa 1 đòn bẩy trong 14 ngày, budget=6×GP thực; **KHÔNG THÌ** không tăng quảng bá/giảm giá/cộng setup vào ARPU/giấu chi phí.

### Cổng 90 ngày — một metric/cổng; Ngày 1 = 09/10/2026

| Ngày | Metric · ngưỡng GO | Bằng chứng phải có | Nếu trượt |
|---|---|---|---|
| **30 · 07/11** | Số shop có time study hợp lệ **≥2** | time-study.csv: ≥20 yêu cầu thật/shop, phút trước/sau, shop xác nhận | FIX 30 ngày: sửa thu time study; giả định sai: PIVOT; đã FIX vẫn không tiến bộ: KILL |
| **60 · 07/12** | Số shop có TTFV≤14 ngày **≥2** | first-value.csv: timestamp ký/xác nhận, Job log; giữ shop chưa đạt | FIX 30 ngày: sửa 1 nút onboarding; giả định sai: PIVOT; đã FIX vẫn không tiến bộ: KILL |
| **90 · 06/01/2027** | Số shop trả recurring kỳ 2 **≥3** | renewals.csv + chứng từ kỳ 1/2, không tính setup/lời hứa | Trượt: KILL offer hiện tại theo kill criteria |

**FIX tối đa 1 lần/vấn đề**, lưu problem_id và bằng chứng; đổi tên metric không reset. GO chỉ mở bước tiếp theo trong ngân sách, không tự cho phép scale. Hạn ngày 90 cố định.

**KILL CRITERIA:** Đến **06/01/2027**, nếu có **<3 shop thanh toán recurring kỳ thứ hai**, dừng offer AI trực inbox thời trang hiện tại và acquisition, bàn giao khách theo thỏa thuận.

**CHƯA ĐO ĐƯỢC:** Cả 7 đèn; cần CRM, Job/reopen/token log, time study và ledger. Pilot dự kiến 26/10; baseline #2:09/11, #1:23/11, #4:23/12 có điều kiện sau 2 chu kỳ, B/U/Bp/Lp chưa có số. #6/#7 chờ doanh thu/kỳ đủ dữ liệu. Runway thiếu: cần tiền mặt + net burn; kế hoạch 90 ngày không phải runway.
