# ERP Accounting Survey – SME Vietnam

Khảo sát nghiệp vụ kế toán dành cho doanh nghiệp vừa và nhỏ, thu thập dữ liệu đủ để viết **user stories & business rules** cho từng module kế toán trong ERP.

## Modules được hỏi (conditional)

Người dùng chọn module họ phụ trách ở Phần 1 — survey tự ẩn/hiện các section liên quan:

| Section | Module | Dữ liệu thu thập |
|---------|--------|-----------------|
| 1 | Setup | Quy mô, ngành, TT200/TT133, module scope |
| 2 | Phân quyền | Roles, approval levels, approval limits |
| 3 | AR | Trigger, fields, credit limit, aging, dunning, reports |
| 4 | AP | 3-way matching, approval flow, payment terms |
| 5 | Cash & Bank | Quỹ, hạn mức, bank recon, payment methods |
| 6 | Tax & HĐĐT | Tax types, VAT period, e-invoice flow, adjustments |
| 7 | Payroll | Salary structure, approval, cost allocation |
| 8 | Fixed Assets | Depreciation method, asset lifecycle events |
| 9 | Inventory | Costing method (FIFO/avg), perpetual/periodic |
| 10 | GL & BCTC | Close checklist, financial statements, mgmt reports |
| 11 | Integration | Cross-module data flows, history migration, export |

## Output JSON → User Stories

Mỗi response JSON có thể map thẳng sang user stories:

```json
{
  "role": "kt_cong_no",            → Actor: "As an AR accountant"
  "ar_trigger": "on_delivery",     → Trigger: "when goods are delivered"
  "ar_credit_limit": "yes_hard",   → Rule: "system must block orders exceeding credit limit"
  "ar_terms": "net30",             → Constraint: "payment due within 30 days"
  "ar_aging": ["1_30","31_60","61_90","90plus"], → Report: aging buckets
  "approval_level": "two_level",   → Rule: "amounts above limit require director approval"
}
```

## Deploy lên GitHub Pages

```bash
# 1. Tạo repo mới trên GitHub (public)
# 2. Push code
git init && git add . && git commit -m "Initial survey"
git remote add origin https://github.com/YOUR_USERNAME/sme-accounting-survey.git
git push -u origin main

# 3. Bật GitHub Pages: Settings → Pages → Deploy from branch: main → /root → Save
# URL: https://YOUR_USERNAME.github.io/sme-accounting-survey/
```

## Nhận response qua email (Formspree)

1. Đăng ký miễn phí tại https://formspree.io
2. Tạo New Form → lấy Form ID (dạng `xabc1234`)
3. Trong `index.html`, tìm và thay:
   ```
   action="https://formspree.io/f/YOUR_FORM_ID"
   ```
4. Commit & push → mỗi lần submit sẽ gửi email cho bạn

## Fallback khi Formspree chưa cấu hình

Người dùng vẫn có thể **Download JSON** sau khi submit. Bạn thu thập file này qua email hoặc Google Drive để tổng hợp.
