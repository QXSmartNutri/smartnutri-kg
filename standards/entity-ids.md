# SmartNutri Entity ID Standard

> **Phiên bản:** 1.0.0 · **Trạng thái:** Active
> **Phạm vi:** Toàn bộ hệ thống SmartNutri KG — JSON-LD, RDF/OWL, Neo4j, Vector DB, API

---

## 1. Nguyên tắc

- **Bất biến:** ID một khi đã gán, không bao giờ thay đổi kể cả khi entity đổi tên.
- **Duy nhất toàn cục:** Không có hai entity nào dùng cùng ID, kể cả khác loại.
- **Máy đọc được:** Chỉ dùng `A–Z`, `0–9`, `_`. Không dấu, không khoảng trắng.
- **Có thể mở rộng:** SEQ6 cho phép tối đa 999.999 entity mỗi loại.

---

## 2. Cú pháp
{PREFIX}{YYYYMMDD}{SEQ6}_{SEQ6_CON}

| Thành phần | Bắt buộc | Mô tả |
|---|---|---|
| `PREFIX` | ✅ | Mã loại entity |
| `YYYYMMDD` | ✅ | Ngày tạo (UTC) |
| `SEQ6` | ✅ | Số thứ tự entity cha (6 chữ số) |
| `SEQ6_CON` | ⚠️ tùy chọn | Số thứ tự entity con (6 chữ số) |

**Ví dụ:**
NUT_20260601_000001                 ← Vitamin K (cha)
NUT_20260601_000001_000001          ← Vitamin K1 (con)
NUT_20260601_000001_000002          ← Vitamin K2 MK-4 (con)
FOOD_20260601_000001                ← Natto (cha)
FOOD_20260601_000001_000001         ← Natto nguyên hạt (con)
---

## 3. Bảng 15 prefix chính thức

| # | Prefix | Loại entity | Phase |
|---|---|---|---|
| 1 | `FOOD_` | Thực phẩm | 1 |
| 2 | `HERB_` | Dược liệu | 1 |
| 3 | `NUT_` | Nutrients | 1 |
| 4 | `BIO_` | Bioactive compounds | 1 |
| 5 | `TOX_` | Độc chất | 1 |
| 6 | `DIS_` | Bệnh lý | 2 |
| 7 | `SYM_` | Triệu chứng | 2 |
| 8 | `DRUG_` | Hoạt chất thuốc | 3 |
| 9 | `BRAND_` | Biệt dược thuốc | 3 |
| 10 | `SYS_` | Hệ cơ quan | 4 |
| 11 | `ORG_` | Cơ quan | 4 |
| 12 | `TIS_` | Mô | 4 |
| 13 | `CELL_` | Tế bào | 4 |
| 14 | `PROC_` | Quá trình sinh học | 5 |
| 15 | `PATH_` | Con đường sinh học | 5 |

> **Quy tắc cứng:** Chỉ 15 prefix trên được công nhận. Prefix mới phải tạo PR vào file này và được review trước khi dùng.

---

## 4. URI đầy đủ
Base: https://smartnutri.org/entity/
JSON-LD:  { "@id": "https://smartnutri.org/entity/NUT_20260601_000001" }
Turtle:   sn:NUT_20260601_000001 a sn:Nutrient .
---

## 5. Quy tắc cha — con
✅ Tạo cha trước, con sau
✅ Con chỉ 1 cấp (không lồng tiếp)
❌ NUT_20260601_000001_000001_000001  ← 3 cấp, không cho phép
---

## 6. Ánh xạ sang hệ thống ngoài

| Hệ thống | Property | Áp dụng cho |
|---|---|---|
| Wikidata | `owl:sameAs` | Tất cả |
| PubChem | `skos:closeMatch` | NUT_, BIO_, TOX_, DRUG_ |
| USDA FDC | `skos:exactMatch` | FOOD_, NUT_ |
| ICD-10 | `owl:sameAs` | DIS_ |
| DrugBank | `skos:exactMatch` | DRUG_, BRAND_ |
| MeSH | `skos:closeMatch` | DIS_, SYM_, PROC_ |

---

## 7. KHÔNG được làm
❌ NUT_1                    — thiếu ngày và SEQ6
❌ NUT_VitaminK             — dùng tên thay số thứ tự
❌ nut_20260601_000001      — prefix phải viết HOA
❌ NUT_20260601_1           — phải là 000001 (6 chữ số)
❌ PROT_20260601_000001     — không trong 15 prefix
❌ Xóa hoặc tái sử dụng ID — ID đã tạo là vĩnh viễn
---

## 8. Deprecation

```json
{
  "@id": "https://smartnutri.org/entity/NUT_20260601_000099",
  "owl:deprecated": true,
  "rdfs:comment": "Deprecated 2026-09-01. Merged into NUT_20260601_000001.",
  "owl:sameAs": "https://smartnutri.org/entity/NUT_20260601_000001"
}
□ Kiểm tra entity chưa tồn tại trong registry
□ Chọn đúng PREFIX trong 15 prefix chính thức
□ Lấy ngày tạo UTC (YYYYMMDD)
□ Lấy SEQ6 tiếp theo của prefix đó
□ Tạo cha trước nếu là entity con
□ Cập nhật file .jsonld / .ttl với @id đúng URI
□ Nếu có alias ngoài, thêm sameAs / exactMatch
