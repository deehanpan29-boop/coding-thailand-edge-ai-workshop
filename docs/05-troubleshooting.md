# 🆘 Troubleshooting Guide

> ปัญหาที่พบบ่อยและวิธีแก้ — อ่านก่อนเรียก TA

---

## 🔌 ปัญหา Hardware

### UNO Q ไม่ boot / ไฟไม่ติด

**ลองตามลำดับ:**
1. ถอด USB-C แล้วเสียบใหม่
2. ลองใช้ USB cable เส้นอื่น (cable เสียได้ง่าย!)
3. เช็ค power adapter — ต้อง 5V/3A
4. ลองเสียบเข้า USB port อื่นของ laptop
5. ถ้ายังไม่ได้ → เปลี่ยนบอร์ดสำรอง

### Modulino ไม่อ่านค่า

```
[ ] เช็คว่า Qwiic cable เสียบสนิททั้ง 2 ฝั่ง
[ ] เช็คว่าเสียบใน Qwiic port ของ UNO Q ไม่ใช่ port อื่น
[ ] ลองรัน sample sketch ของ Modulino library
[ ] ถ้าใช้หลาย module → เสียบทีละตัวเช็คว่าตัวไหนเสีย
```

⚠️ **สำคัญ:** Qwiic cable มี polarity (เสียบผิดด้านเสียบไม่ได้) — ถ้ารู้สึกฝืน อย่าฝืน

### USB Camera ไม่เจอบน UNO Q

```bash
# SSH เข้า UNO Q แล้วเช็ค
ls /dev/video*
# ถ้าไม่มี /dev/video0 → camera ไม่ถูกตรวจพบ

# เช็ค USB devices
lsusb
```

**สาเหตุที่พบบ่อย:**
- USB Hub ไม่จ่ายไฟพอ → ใช้ powered hub
- Camera ต้องใช้ UVC standard
- ลอง reboot UNO Q

### USB Microphone ไม่ทำงาน

```bash
# เช็คว่า mic ถูกตรวจพบ
arecord -l

# ทดสอบ record
arecord -d 5 test.wav
```

---

## 🌐 ปัญหา Network/Edge Impulse

### เชื่อม Edge Impulse ไม่ได้

```bash
# บน UNO Q terminal
edge-impulse-linux

# ถ้า error → ลอง install ใหม่
sudo npm install edge-impulse-linux -g --unsafe-perm
```

**Checklist:**
- [ ] UNO Q connect Wi-Fi ได้
- [ ] Login Edge Impulse account
- [ ] เลือก project ถูก

### Upload data ไม่ขึ้น

- ตรวจ Wi-Fi signal
- ลด batch size (อัพทีละน้อย)
- เช็ค disk space ของ Edge Impulse free tier

### Train ค้าง / error

**Common fix:**
1. Training processor ต้องเลือก **GPU** ไม่ใช่ CPU
2. ลด model size = **nano (2.4M)**
3. ลด epochs ถ้าใช้ free tier เกิน quota
4. ลด input data resolution (vision)

---

## 🧠 ปัญหา Model / Deploy

### Build ลง UNO Q ไม่ได้

```
Error: model too large for target
```
→ ลด model size เป็น **nano** หรือ **micro**

```
Error: incompatible architecture
```
→ เช็ค deployment target = **Arduino UNO Q** (ไม่ใช่ UNO R4)

### Inference ช้า/กระตุก

- Vision: ลด input resolution (96x96 พอแล้ว)
- Audio: ลด sample rate (16kHz พอ)
- Motion: เพิ่ม window size, ลด frequency

### Accuracy ต่ำมาก (<60%)

**Diagnose:**
1. ดู confusion matrix → class ไหนสับสน?
2. ดู data balance → แต่ละ class จำนวนใกล้กันไหม?
3. ทดสอบบน data ที่ไม่ได้ train → overfit หรือเปล่า?

**Common fixes:**
- เก็บข้อมูลเพิ่มใน class ที่ accuracy ต่ำ
- เพิ่ม variation (แสง/มุม/สภาพแวดล้อม)
- แก้ class boundary ถ้าซ้อนกัน

### Accuracy ดีบน Studio แต่ใช้จริงห่วย

= **Distribution shift** — data จริงต่างจาก data train

**แก้:**
- เก็บข้อมูล **ในสภาพแวดล้อมจริงที่จะใช้**
- เพิ่ม augmentation (Edge Impulse มีให้)
- เก็บข้อมูล "noise/background" เป็นอีก class

---

## 💻 ปัญหา Git/GitHub

### Push ไม่ขึ้น

```
error: failed to push some refs
```
→ ทีมอื่นเพิ่ง push มา ทำตามนี้:
```bash
git pull --rebase
git push
```

### Commit ผิด อยากแก้ message

```bash
# แก้ commit ล่าสุดที่ยังไม่ push
git commit --amend -m "new message"

# ถ้า push ไปแล้ว
git commit --amend -m "new message"
git push --force-with-lease
# ⚠️ ระวัง ทับงานเพื่อน!
```

### Merge conflict

```bash
git pull
# เห็น CONFLICT (content): ...

# เปิดไฟล์ที่ conflict
# ลบ marker <<<<<<<, =======, >>>>>>>
# เก็บ version ที่ต้องการ
git add <conflicted-file>
git commit
git push
```

### เผลอ commit dataset ขนาดใหญ่

```bash
# ลบจาก tracking (ไฟล์ยังอยู่)
git rm --cached big-data.zip

# เพิ่มใน .gitignore
echo "*.zip" >> .gitignore
echo "dataset/raw/" >> .gitignore

git commit -m "fix: ลบไฟล์ใหญ่ออก, ใช้ Edge Impulse host แทน"
git push
```

**Best practice:** Dataset เก็บที่ Edge Impulse, repo เก็บแค่ link

---

## 🎤 ปัญหา Workshop Flow

### ทีมเก็บข้อมูลช้ามาก ใกล้พักเที่ยงยังไม่เสร็จ

**Plan B:**
- ลด class ลงเป็น 2 (จาก 3)
- ลด samples ต่อ class เป็น 30
- ใช้ backup dataset ของ track เป็น base + เก็บเพิ่ม 10-20 samples ของตัวเอง

### ทีมทะเลาะกัน

- ครู step in ทันที
- แยก discuss กับแต่ละคน
- แบ่งบทบาท 3H ให้ชัด — Hacker ห้ามแก้ design ของ Hipster โดยไม่คุย

### นักเรียนคนเดียวทำทุกอย่าง

- ครู intervene → กำหนดให้บทบาทอื่นทำ part เฉพาะ:
  - Hipster ต้อง present Data Collection
  - Hustler ต้อง present Idea Canvas

### Demo จริงไม่ได้แล้วถึงเวลา Cross-Track

- Show screen Edge Impulse Studio แทน
- Present V1→V2 improvement แทน live demo
- ครูให้คะแนน participation ตามที่ทำได้จริง ไม่ใช่ผลลัพธ์ปลายทาง

---

## 📞 เมื่อไหร่ควรเรียก TA?

✅ **เรียก TA เมื่อ:**
- ลองในคู่มือนี้แล้ว 5+ นาที ยังไม่ได้
- Hardware เสียจริง (UNO Q ไม่ติด, Modulino พัง)
- Edge Impulse account มีปัญหา
- ติด conflict ใน Git แก้ไม่หาย

❌ **อย่าเพิ่งเรียก TA ถ้า:**
- ยังไม่ได้อ่านคู่มือ
- ยังไม่ได้ลองด้วยตัวเอง
- เป็นเรื่อง design choice (ทีมตัดสินใจเอง)

**Pro tip:** เปิด GitHub Issue ใน repo ทีม เขียนปัญหา + สิ่งที่ลองมาแล้ว → TA review จาก issue ได้

---

## 🏥 Emergency Contact

ถ้า TA ไม่ว่าง:
1. ดูใน [GitHub Discussions](https://github.com/SANCHAIE/coding-thailand-edge-ai-workshop/discussions) ของ workshop repo
2. ถามทีมข้างๆ
3. ลอง Edge Impulse forum: https://forum.edgeimpulse.com/
