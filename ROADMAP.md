# SmartNutri KG — Roadmap

> Kế hoạch phát triển 5 giai đoạn — từ Knowledge Graph nền tảng đến AI Nutrition Agent đa ngôn ngữ toàn cầu.

---

## Tổng quan
Phase 1 → Phase 2 → Phase 3 → Phase 4 → Phase 5
KG        Graph     GraphRAG    AI        Open
v1.0       v2.0      v3.0      Agent    Standard
---

## Phase 1 — SmartNutri Open Nutrition KG v1.0
**Mục tiêu:** Xây dựng nền tảng tri thức dinh dưỡng cốt lõi.

**Entity Prefixes:** `FOOD_` `HERB_` `NUT_` `BIO_` `TOX_`

**Data:**
data/jsonld/
├── foods/         # Thực phẩm
├── herbs/         # Dược liệu
├── nutrients/     # Chất dinh dưỡng
├── bioactives/    # Hoạt chất sinh học
└── toxic/         # Độc chất
**Standards hoàn thiện:**
- [x] `entity-ids.md` — Quy tắc ID 15 prefix
- [x] `nutrient-units.json` — Đơn vị 45 nutrients
- [x] `age-groups.json` — 15 nhóm tuổi
- [x] `nutrient-rda.json` — RDA & AI theo IOM
- [x] `nutrient-ul.json` — UL theo IOM
- [x] `nutrient-dv.json` — Daily Values FDA 2020
- [x] `nutrient_amdr.json` — AMDR % năng lượng
- [x] `evidence-levels.json` — Mức bằng chứng A/B/C/D
- [x] `absorption_factors.json` — Hệ số hấp thu 39 mục tiêu
- [x] `gi_gl_tables.json` — Glycemic Index & Load
- [x] `allergens.json` — FDA Big 9 + EU Big 14
- [x] `demographics.json` — Nhóm dân số & BMI
- [x] `categories.json` — Phân loại entity
- [x] `languages.json` — 55 ngôn ngữ
- [x] `dri_tables.json` — Tổng hợp DRI
- [ ] `bioavailability_modifiers.json`
- [ ] `cooking_retention_factors.json`
- [ ] `food_portion_constraints.json`
- [ ] `nutrient_interactions.json`
- [ ] `nutrition_balance_rules.json`
- [ ] `meal_scoring_rules.json`
- [ ] `meal_grade_rules.json`
- [ ] `meal_distribution_rules.json`
- [ ] `optimization_constraints.json`
- [ ] `optimization_weights.json`
- [ ] `bioactive-groups.json`
- [ ] `bioactive-targets.json`

**Ontology:**
- [x] `smartnutri.ttl` — Master ontology
- [x] 11 Classes TTL (Food, Herb, Nutrient, Bioactive, Toxic, Disease, Symptom, Drug, Brand, Anatomy, Metabolism)
- [x] 6 Properties TTL (contains, affects, interactsWith, associatedWith, locatedIn, participatesIn)

**Schemas:**
- [x] 11 JSON Schema files

**Viewer:**
- [ ] D3.js Knowledge Graph viewer hoàn chỉnh
- [ ] GitHub Pages deployment
- [ ] Search & filter theo prefix

**CI/CD:**
- [ ] `validate_json.yml`
- [ ] `validate_ids.yml`
- [ ] `validate_schemas.yml`
- [ ] `nightly_tests.yml`
- [ ] `deploy_pages.yml`

---

## Phase 2 — SmartNutri Open Nutrition KG v2.0
**Mục tiêu:** Liên kết dinh dưỡng với bệnh lý lâm sàng.

**Entity Prefixes:** `DIS_` `SYM_`

**Data:**
data/jsonld/
├── diseases/      # Bệnh lý (ICD-10 mapping)
└── symptoms/      # Triệu chứng lâm sàng
**Deliverables:**
- [ ] JSON-LD datasets cho bệnh lý & triệu chứng
- [ ] Quan hệ: Nutrient ↔ Disease (sn:associatedWith)
- [ ] Quan hệ: Food ↔ Symptom
- [ ] ICD-10 mapping cho tất cả DIS_ entities
- [ ] Neo4j integration — Cypher import scripts
- [ ] REST API v1 — `/api/nutrients`, `/api/foods`, `/api/diseases`
- [ ] Curated datasets từ USDA FDC, INFOODS

---

## Phase 3 — SmartNutri Open Nutrition KG v3.0
**Mục tiêu:** Tương tác thuốc — dinh dưỡng — bệnh lý.

**Entity Prefixes:** `DRUG_` `BRAND_`

**Data:**
data/jsonld/
├── drugs/         # Hoạt chất thuốc (DrugBank mapping)
└── brands/        # Biệt dược thương mại
**Deliverables:**
- [ ] JSON-LD datasets cho hoạt chất & biệt dược
- [ ] Quan hệ: Drug ↔ Nutrient (sn:interactsWith)
- [ ] Quan hệ: Drug ↔ Disease
- [ ] DrugBank & ATC code mapping
- [ ] GraphRAG Engine — semantic retrieval
- [ ] Qdrant / Vector DB integration
- [ ] Embeddings generation cho tất cả entities

---

## Phase 4 — SmartNutri Open Nutrition KG v4.0
**Mục tiêu:** Ánh xạ dinh dưỡng đến cơ quan & mô đích.

**Entity Prefixes:** `SYS_` `ORG_` `TIS_` `CELL_`

**Data:**
data/jsonld/
└── anatomy/
├── systems/   # Hệ cơ quan
├── organs/    # Cơ quan
├── tissues/   # Mô
└── cells/     # Tế bào
**Deliverables:**
- [ ] JSON-LD datasets cho hệ cơ quan, cơ quan, mô, tế bào
- [ ] Quan hệ: Nutrient → Organ (sn:locatedIn, sn:affects)
- [ ] AI Nutrition Agent — meal recommendation
- [ ] Disease Agent — nutrient-disease analysis
- [ ] Drug Interaction Agent
- [ ] Personalization engine theo demographics

---

## Phase 5 — SmartNutri Open Nutrition Standard v5.0
**Mục tiêu:** Chuẩn dinh dưỡng mở toàn cầu & AI đa ngôn ngữ.

**Entity Prefixes:** `PROC_` `PATH_`

**Data:**
data/jsonld/
└── metabolism/
├── processes/ # Quá trình sinh học
└── pathways/  # Con đường chuyển hóa
**Deliverables:**
- [ ] JSON-LD datasets cho metabolic processes & pathways
- [ ] KEGG Pathway & Reactome mapping
- [ ] Multi-Agent system (Nutrition + Disease + Drug + Meal + Supplement)
- [ ] Personalization theo genome, microbiome, wearable data
- [ ] Multilingual support — 55 ngôn ngữ
- [ ] SmartNutri Open Nutrition Standard publication
- [ ] Public API — open access
- [ ] Community contribution platform

---

## Milestone Timeline

| Milestone | Target | Status |
|---|---|---|
| Phase 1 Standards hoàn chỉnh | Q3 2026 | 🔄 In Progress |
| Phase 1 Data — Nutrients đầy đủ | Q3 2026 | 🔄 In Progress |
| Phase 1 Viewer & GitHub Pages | Q3 2026 | ⏳ Pending |
| Phase 2 — Diseases & Symptoms | Q4 2026 | ⏳ Pending |
| Phase 3 — Drugs & GraphRAG | Q1 2027 | ⏳ Pending |
| Phase 4 — Anatomy & AI Agents | Q2 2027 | ⏳ Pending |
| Phase 5 — Open Standard | Q4 2027 | ⏳ Pending |

---

## Đóng góp

Xem [docs/contributing.md](docs/contributing.md) để biết cách đóng góp vào từng phase.

**Ưu tiên hiện tại (Phase 1):**
1. Hoàn thiện `standards/` — các file còn pending
2. Tạo entity đầu tiên trong `data/jsonld/nutrients/`
3. Hoàn thiện `src/viewer/` và deploy GitHub Pages
4. Viết tests validation đầy đủ
5. 
