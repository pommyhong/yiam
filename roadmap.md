# Yiam — Navigation Map & Roadmap

playground · ลองคิดให้ครบ flow + เผื่ออนาคต

---

## 1. Navigation map — กดจากไหน ไปไหนได้

```
Home (🏠)
 ├─ ⊕ FAB ................. Add sheet ──save──> Success toast ──> กลับ Home
 ├─ tap แถวรายการ ......... Transaction detail ─┬─ แก้ไข → Add (prefilled)
 │                                              └─ ลบ → confirm → Home
 ├─ "รายการล่าสุด" ดูทั้งหมด . All transactions (search + filter)   [future]
 ├─ balance card .......... Cashflow / accounts detail            [future]
 ├─ avatar ................ Settings / profile                    [future]
 └─ nav 📊 ................ Stats (🟢 ทำแล้ว)

Stats (📊)
 ├─ tap หมวดในลิสต์ ........ Category detail (รายการในหมวดนั้น)     [next]
 ├─ period selector ....... สลับช่วงเวลา (in-place)
 └─ "ดูอินไซต์" ........... Insights (plain-language)            [ทำรอบนี้]

Add sheet
 ├─ tap "เปลี่ยน" หมวด ..... Category picker (🟢 ทำรอบนี้)
 ├─ tap วันที่ ............. Date picker                          [future]
 └─ amount → keypad

States ที่ผูกกับหน้า
 ├─ Home ว่าง ............. Empty / first run (🟢 ทำรอบนี้)
 ├─ Stats ข้อมูล < 3 ...... ซ่อนกราฟ โชว์ list (decision #6)
 └─ หลังบันทึก ............ Success toast + undo (🟢 ทำรอบนี้)
```

---

## 2. ทำให้ดีกว่าแอปคนอื่น (differentiators)

คู่แข่ง (Rocket Money / Copilot / Monarch / Revolut) = ทรงพลังแต่ **หนัก, ต้องผูกบัญชี, เสียเงิน, ซับซ้อน**
wedge ของ Yiam = **"แอปที่คุณใช้ต่อไม่เลิก"** — ปัญหาจริงของ tracker แบบจด manual คือคนเลิกจด

```
#  differentiator              ทำไมชนะ                              สถานะ
──────────────────────────────────────────────────────────────────────────────
1  บันทึก < 5 วิ + quick-add   จาก Home แตะ chip หมวดที่ใช้บ่อย      core (มีแล้ว)
   (ข้ามขั้นเลือกหมวด)         → ใส่เลข → จบ                          → ทำ quick-add [future]
2  Insight ภาษาคน             ไม่ใช่ "ใช้ ฿4,560" แต่ "อาหารมากกว่า   ทำรอบนี้
                              เดือนก่อน 18% ส่วนใหญ่มื้อเย็น"
3  โทนไม่ตัดสิน (no-judgment)  ไม่ทำให้รู้สึกผิด → ใช้ต่อได้นาน        design principle
   (banking stigma aware)     "เดินทางลด 12% เก่งมาก"
4  Habit / streak             "จดต่อเนื่อง 7 วัน" สร้างนิสัย          ทำรอบนี้ (ใน Insights)
5  Recurring detect ไม่ผูกธนาคาร "เหมือนมี Netflix ทุกวันที่ 5 →        ทำรอบนี้ (ใน Insights)
                              ตั้งเป็นรายการประจำ?"
6  Weekly recap               สรุปสัปดาห์ย่อยง่าย (Peak-End)          [future]
7  Dark mode                  mono อยู่แล้ว → ทำง่าย, token เผื่อไว้   [future]
```

> หัวใจ: คู่แข่งแข่งที่ "ข้อมูลครบ" — Yiam แข่งที่ "ทำให้จดเป็นนิสัย + เข้าใจง่าย"
> ทุก feature ใหม่ต้องผ่านเกณฑ์: ไม่เพิ่ม friction การบันทึก + ไม่ทำให้รู้สึกผิด

---

## 3. ลำดับแนะนำ (ถ้าทำต่อ)
```
รอบนี้   Empty · Success toast · Category picker · Transaction detail · Insights
ถัดไป    Category detail · All transactions (search) · quick-add chips
อนาคต    Recurring · Weekly recap · Dark mode · Date picker · Settings
```
