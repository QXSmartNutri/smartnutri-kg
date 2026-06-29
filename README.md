# ⬡ SmartNutri Knowledge Graph

> **SmartNutri Open Nutrition Knowledge Graph** — Hệ thống tri thức dinh dưỡng mở, xây dựng theo chuẩn JSON-LD / RDF / OWL. Thiết kế để AI tạo thực đơn tối ưu & cá nhân hóa dinh dưỡng.

[

![Validate JSON](https://github.com/QXSmartNutri/smartnutri-kg/actions/workflows/validate_json.yml/badge.svg)

](https://github.com/QXSmartNutri/smartnutri-kg/actions/workflows/validate_json.yml)
[

![Validate IDs](https://github.com/QXSmartNutri/smartnutri-kg/actions/workflows/validate_ids.yml/badge.svg)

](https://github.com/QXSmartNutri/smartnutri-kg/actions/workflows/validate_ids.yml)
[

![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)

](LICENSE)

---

## Phiên bản hiện tại

**v1.0.0 — Phase 1** · Nutrients · Foods · Herbs · Bioactives · Toxics

---

## Cấu trúc hệ thống
smartnutri-kg/
├── ontology/         # RDF/OWL schema — class & property definitions
├── schemas/          # JSON Schema validation cho từng loại entity
├── data/jsonld/      # Dữ liệu tri thức theo chuẩn JSON-LD
├── standards/        # Quy chuẩn hệ thống (ID, đơn vị, RDA, hấp thu...)
├── src/viewer/       # Interactive Knowledge Graph viewer (D3.js)
├── docs/             # Tài liệu kỹ thuật
└── tests/            # Validation scripts
---

## Roadmap 5 giai đoạn

| Phase | Version | Nội dung | Prefixes |
|---|---|---|---|
| 1 | v1.0 | Foods, Herbs, Nutrients, Bioactives, Toxics | FOOD_ HERB_ NUT_ BIO_ TOX_ |
| 2 | v2.0 | Diseases, Symptoms | DIS_ SYM_ |
| 3 | v3.0 | Drugs, Brands | DRUG_ BRAND_ |
| 4 | v4.0 | Anatomy (Systems, Organs, Tissues, Cells) | SYS_ ORG_ TIS_ CELL_ |
| 5 | v5.0 | Metabolism (Processes, Pathways) | PROC_ PATH_ |

---

## Entity ID Standard
{PREFIX}{YYYYMMDD}{SEQ6}             ← Entity cha
{PREFIX}{YYYYMMDD}{SEQ6}_{SEQ6}      ← Entity con
Ví dụ:
NUT_20260601_000001                    ← Vitamin K (cha)
NUT_20260601_000001_000001             ← Vitamin K1 (con)
NUT_20260601_000001_000003             ← Vitamin K2 MK-7 (con)
Xem đầy đủ: [standards/entity-ids.md](standards/entity-ids.md)

---

## Bắt đầu nhanh

### Xem Knowledge Graph
Mở: src/viewer/index.html
Hoặc: https://QXSmartNutri.github.io/smartnutri-kg/src/viewer/
### Validate dữ liệu
```bash
# Validate JSON-LD
node tests/data/validate-jsonld.js

# Validate Entity IDs
node tests/data/validate-ids.js

# Validate Schema
node tests/data/validate-schema.js
Validate Ontology (Turtle)
bash tests/ontology/validate-nutrient.sh
Standards đã thiết lập
File
Mô tả
entity-ids.md
Quy tắc đặt ID — đọc trước tiên
nutrient-units.json
Đơn vị đo lường — 45 nutrients
age-groups.json
15 nhóm tuổi chuẩn
nutrient-rda.json
RDA & AI theo IOM
nutrient-ul.json
UL theo IOM
nutrient-dv.json
Daily Values theo FDA 2020
nutrient_amdr.json
AMDR % năng lượng
evidence-levels.json
Mức bằng chứng A/B/C/D
absorption_factors.json
Hệ số hấp thu 39 mục tiêu
gi_gl_tables.json
Glycemic Index & Load
allergens.json
Dị ứng FDA Big 9 + EU Big 14
demographics.json
Nhóm dân số & BMI
categories.json
Phân loại entity
languages.json
55 ngôn ngữ hỗ trợ
dri_tables.json
Tổng hợp DRI
Đóng góp
Xem docs/contributing.md trước khi tạo entity mới.
Trích dẫn
Xem CITATION.cff
License
MIT License — Xem LICENSE
