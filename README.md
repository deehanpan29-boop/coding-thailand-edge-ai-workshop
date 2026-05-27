# 🤖 Coding Thailand 2026 — Edge AI Workshop

> **Day 1 Workshop Materials**
> Arduino UNO Q × Modulino × Edge Impulse
> Regional Coding & AI Competition — ห้อง Edge AI

[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)
[![Arduino UNO Q](https://img.shields.io/badge/Arduino-UNO%20Q-00979D)](https://www.arduino.cc/)
[![Edge Impulse](https://img.shields.io/badge/Edge%20Impulse-Studio-3B4252)](https://edgeimpulse.com/)

---

## 📋 ภาพรวม Workshop

Workshop 6 ชั่วโมง (09:00–17:00) ที่สอนให้นักเรียนสร้าง Edge AI prototype ด้วย Arduino UNO Q + Modulino + Edge Impulse จบใน 1 วัน — เพื่อเตรียมไปแข่ง Prototype Day ในวันถัดไป

### 🎯 เป้าหมายการเรียนรู้

หลังจบ Day 1 นักเรียนจะ:
- เข้าใจ pipeline ของ Edge AI: **Data → Train → Deploy → Inference**
- ออกแบบ class & dataset ที่ลดอคติ (bias-aware)
- Train โมเดลผ่าน Edge Impulse Studio + Deploy ลง UNO Q
- จดบันทึก Prediction Log อย่างเป็นระบบ
- ใช้ Git/GitHub ในการเก็บหลักฐานและ version model

### 📊 เกณฑ์คะแนน Skill Assessment (30 คะแนน)

| หัวข้อ | น้ำหนัก | คะแนนเต็ม |
|---|---|---|
| Setup & Safety | 1.25 | 5 |
| Core Implementation | 2.5 | 10 |
| Data & Testing | 1.25 | 5 |
| Debug & Explain | 1.25 | 5 |
| Participation & Collaboration | 1.25 | 5 |

---

## 🗂️ โครงสร้าง Repository

```
coding-thailand-edge-ai-workshop/
├── README.md                          ← คุณอยู่ที่นี่
├── docs/                              ← เอกสารหลัก
│   ├── 01-schedule.md                 ← Timeline 6 ชม.
│   ├── 02-tracks.md                   ← 4 Tracks ให้เลือก
│   ├── 03-rubric.md                   ← เกณฑ์ให้คะแนน
│   ├── 04-git-basics.md               ← Git 101 สำหรับนักเรียน
│   └── 05-troubleshooting.md          ← ปัญหาที่พบบ่อย
├── slides/                            ← Slide outline
│   └── day1-outline.md
├── worksheets/                        ← ใบงานนักเรียน
│   ├── W1-class-design.md
│   ├── W2-data-collection-log.md
│   ├── W3-prediction-log.md
│   └── W4-idea-canvas.md
├── labs/                              ← Lab manual แต่ละ track
│   ├── anchor-demo/                   ← Gesture Wand (demo เปิด)
│   ├── track-a-motion/                ← Motion classification
│   ├── track-b-vision/                ← Vision classification
│   ├── track-c-environment/           ← Multi-sensor fusion
│   └── track-d-audio/                 ← Audio classification
├── templates/                         ← Template ให้นักเรียน fork
│   ├── team-repo-template/            ← Template repo ของทีม
│   └── pull-request-template.md
└── assets/                            ← รูป diagram
```

---

## 🚀 เริ่มต้นใช้งาน (สำหรับครู/ผู้จัด)

### 1. Fork repo นี้

คลิก **Fork** ที่มุมขวาบน เพื่อสร้างสำเนาในบัญชี GitHub ของคุณ

### 2. ปรับแต่งให้เหมาะกับ session ของคุณ

แก้ไฟล์ใน `docs/` และ `slides/` ตามต้องการ

### 3. เตรียมอุปกรณ์

ดู [`docs/00-equipment-checklist.md`](docs/00-equipment-checklist.md)

---

## 👨‍🎓 สำหรับนักเรียน

### Quick Start

1. ดู [Timeline วันนี้](docs/01-schedule.md)
2. เลือก [Track ของทีม](docs/02-tracks.md)
3. เรียน [Git พื้นฐาน 15 นาที](docs/04-git-basics.md)
4. สร้าง repo ทีมใหม่จาก [Team Repo Template](templates/team-repo-template/)
5. ทำตาม Lab manual ของ track ที่เลือก

เริ่มจากคัดลอกไฟล์ในโฟลเดอร์ template ไปใส่ repo ใหม่ของทีมบน GitHub แล้วค่อย clone repo นั้นลงเครื่อง

### Submission Checklist

ก่อนจบวัน ทุกทีมต้องมีใน repo:

- [ ] Dataset ที่ใช้ train (อยู่ใน `dataset/` หรือ link Edge Impulse project)
- [ ] Model V1 และ V2 (export จาก Edge Impulse)
- [ ] Prediction Log อย่างน้อย 10 cases (`logs/predictions.csv`)
- [ ] Idea Canvas สำหรับ Day 2 (`worksheets/W4-idea-canvas.md`)
- [ ] README ของทีม อธิบายโจทย์, classes, ผลลัพธ์

---

## 🛠️ Tech Stack

- **Hardware**: Arduino UNO Q (Qualcomm Dragonwing QRB2210) + Modulino nodes
- **ML Platform**: Edge Impulse Studio
- **Deploy**: Arduino App Lab
- **Version Control**: Git + GitHub

---

## 📜 License

MIT — ใช้สอนต่อ ปรับแต่งได้อย่างเสรี

## 🙏 Credits

จัดทำสำหรับ **โครงการ Coding Thailand 2026 — AI Inspires the Future** โดย DEPA และทีมงานวิทยากร

---

**Questions?** เปิด [Issue](https://github.com/SANCHAIE/coding-thailand-edge-ai-workshop/issues) หรือ [Discussion](https://github.com/SANCHAIE/coding-thailand-edge-ai-workshop/discussions)
