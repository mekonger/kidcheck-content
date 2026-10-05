# kidcheck-content

[Tiếng Việt](#tiếng-việt) · [English](#english)

---

## Tiếng Việt

Danh mục chăm sóc trẻ (vắc xin, vitamin, khám định kỳ, mốc phát triển…) mà
ứng dụng **KidCheck** tải về. Kho này **chỉ chứa nội dung, không có dữ liệu
người dùng**.

> ⚠️ KidCheck chỉ nhắc lịch, không thay thế tư vấn y tế. Nội dung đang được
> chuyên gia y tế rà soát (`reviewStatus: "pending"`).

### Kho này dùng để làm gì

1. Ứng dụng có sẵn một bản danh mục bên trong, nên mở được ngay, kể cả khi
   không có mạng.
2. Khi mở ứng dụng, nó tải ngầm tệp của vùng mình từ địa chỉ raw của nhánh
   `main`, ví dụ
   `https://raw.githubusercontent.com/mekonger/kidcheck-content/main/vi-VN/checklist.json`.
3. Ứng dụng chỉ dùng tệp tải về khi tệp **hợp lệ** và có **phiên bản khác**
   bản đang dùng. Mất mạng, lỗi 404 hay JSON hỏng thì ứng dụng giữ bản cũ;
   tệp hỏng được ghi vào báo cáo lỗi.

**Mọi thứ đưa lên `main` đến tay mọi phụ huynh** ngay lần mở ứng dụng tiếp
theo. Vì vậy mọi thay đổi đều đi qua một Pull Request đã được kiểm tra.

### Thư mục

Mỗi thư mục là một **mã vùng** theo chuẩn BCP 47, dạng `ngôn ngữ-QUỐC GIA`:
lịch chăm sóc của một quốc gia, viết bằng một ngôn ngữ.

```
kidcheck-content/
├── README.md
├── LICENSE
└── vi-VN/
    └── checklist.json     # Việt Nam, tiếng Việt
```

Vùng mới sau này (ví dụ `en-VN/`, `th-TH/`) là một thư mục cùng cấu trúc.

### Định dạng tệp và phiên bản

Chi tiết các trường ở phần English bên dưới. Những điểm chính:

- `version` có dạng `YYYY-MM-DD.N` (ví dụ `2026-10-04.1`) và **phải tăng**
  mỗi lần nội dung thay đổi. Các phần được so sánh như số, nên `.10` mới hơn
  `.9`.
- Không xóa hay đổi `id` của mục đã có (ví dụ `VN-021`): lịch sử “đã làm” của
  phụ huynh gắn với `id` này.
- `items` không được rỗng: tệp không có mục nào bị coi là hỏng.

### Cập nhật nội dung

Nội dung **không sửa tay ở đây**. Nguồn gốc là bảng tính và công cụ chuyển đổi
trong kho riêng `childcare-checklist` (thư mục `content/`).

1. Sửa bảng tính và chạy công cụ chuyển đổi (xem `content/README.md` trong kho
   `childcare-checklist`). Công cụ dừng lại và liệt kê lỗi nếu có, và tự tăng
   `version` khi các mục thay đổi.
2. Chép tệp tạo ra vào `vi-VN/checklist.json` trên một **nhánh mới** của kho
   này.
3. Mở Pull Request, kiểm tra `version` đã tăng và phần thay đổi đúng như mong
   muốn, rồi merge vào `main`.
4. Mở ứng dụng: phiên bản mới hiện trong **Cài đặt → Cập nhật nội dung**.

Muốn quay lại bản trước: revert commit đó, rồi tăng `version` thêm một lần để
ứng dụng nhận bản đã sửa.

### Lưu ý, nguồn và giấy phép

- KidCheck chỉ nhắc lịch, không thay thế tư vấn y tế. Hãy hỏi bác sĩ nhi của
  con bạn.
- Mỗi mục có danh sách `citations`: các nguồn chính thức (Bộ Y tế, WHO,
  chương trình Tiêm chủng mở rộng…). Các trang được dẫn thuộc quyền của bên
  đăng tải.
- © 2026 Mekong Developer. **Bảo lưu mọi quyền**: được đọc, nhưng không được
  sao chép, sửa đổi hay dùng lại khi chưa có sự đồng ý bằng văn bản. Xem
  [LICENSE](LICENSE).

---

## English

The child-care checklist (vaccines, vitamins, check-ups, milestones, …)
downloaded by the **KidCheck** app. This repository holds **content only, no
user data**.

> ⚠️ KidCheck reminds; it does not replace medical advice. The content is still
> being reviewed by health professionals (`reviewStatus: "pending"`).

### What it is and how the app uses it

1. The app ships with its own copy of the checklist, so it opens instantly,
   also offline.
2. On start, the app downloads its region's file in the background from the
   raw URL of the `main` branch, e.g.
   `https://raw.githubusercontent.com/mekonger/kidcheck-content/main/vi-VN/checklist.json`.
3. The app uses a download only if it is **valid** and its **version
   differs** from the one in use. Offline, 404 or broken JSON means it keeps
   what it has; a broken file is sent to the app's crash reports.

**Whatever lands on `main` reaches every parent** the next time they open the
app. Every change therefore goes through a reviewed pull request.

### Folders

Each folder is a **locale** (BCP 47, `language-REGION`): one country's care
schedule, written in one language.

```
kidcheck-content/
├── README.md
├── LICENSE
└── vi-VN/
    └── checklist.json     # Vietnam, Vietnamese
```

New regions (e.g. `en-VN/`, `th-TH/`) are added as folders with the same
structure.

### File format

`checklist.json` is UTF-8 JSON:

```json
{
  "country": "VN",
  "version": "2026-10-04.1",
  "disclaimerVi": "Ứng dụng chỉ nhắc lịch, không thay thế tư vấn y tế. …",
  "items": [ … ]
}
```

Each item:

| Field | Meaning |
|---|---|
| `id` | Stable id, e.g. `VN-021`. **Never change or reuse it**: the parent's history is stored by id |
| `type` / `typeVi` | Category (`Vaccine`, `Vitamin`, `Drug`, `Nutrition`, `Milestone`, `Check-up`, `Screening`, `Safety`, `Hygiene`, `Lifestyle`) and its label |
| `nameVi`, `nameEn` | Item name |
| `ageFromMonths`, `ageToMonths`, `ageLabelVi` | Age window in months, and how it is shown |
| `requirement` / `requirementVi` | `required` (national programme), `recommended`, `recommended_paid`, `optional`, `conditional` or `info`, and its label |
| `schedule` | When reminders happen, see below |
| `defaultEnabled` | On for every new child unless the parent turns it off |
| `condition` | `"not_formula"` = off by default for formula-fed children; otherwise `null` |
| `group` | Links alternatives (e.g. free vs paid vaccine); informational only |
| `howVi`, `benefitsVi`, `riskOveruseVi`, `riskMissedVi` | Texts on the item's detail page |
| `citations` | Source URLs (Ministry of Health, WHO, national immunization programme, …) |
| `samples` | Example products or links, may be empty |
| `reviewStatus` | `pending` until a health professional has approved the item |
| `catchUp` | Vaccines: whether a missed dose can still be given later; `null` = not reviewed yet |

`schedule.kind`:

| kind | Meaning | Fields |
|---|---|---|
| `doses` | One reminder per dose, at the given ages | `atMonths` (e.g. `[2, 3, 4]`) |
| `daily` | Every day inside the age window | – |
| `interval` | Every N months inside the age window | `everyMonths` |
| `info` | Guidance only, never a reminder | – |

### Versioning

- `version` is `YYYY-MM-DD.N` and **must go up** with every content change.
  Parts are compared as numbers, so `.10` is newer than `.9`.
- After an app update, the app uses whichever is newer: its bundled copy or
  the last download.
- Don't delete or rename existing `id`s, and keep `items` non-empty: a file
  with no items is treated as broken and ignored.

### How to publish an update

Content is **not edited by hand here**. The source of truth is the spreadsheet
and converter in the private `childcare-checklist` repository (`content/`).

1. Edit the spreadsheet and run the converter (see `content/README.md` in
   `childcare-checklist`). It stops with a list of problems if anything is
   wrong, and bumps `version` when items changed.
2. Copy the generated file to `vi-VN/checklist.json` on a **new branch** of
   this repository.
3. Open a pull request, check that `version` went up and that the diff is what
   you expect, then merge into `main`.
4. Open the app: the new version shows under **Cài đặt → Cập nhật nội dung**.

To roll back: revert the commit, then bump `version` once more so the app
picks up the corrected file.

### Disclaimer, sources and license

- KidCheck reminds; it does not replace medical advice. Parents should ask
  their child's pediatrician.
- Every item lists its `citations`. Linked pages remain under their
  publishers' own terms.
- © 2026 Mekong Developer. **All rights reserved**: you may read this content,
  but not copy, modify or reuse it without written permission. See
  [LICENSE](LICENSE).
