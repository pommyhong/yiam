# Yiam — Navigation Map & Roadmap

playground · ลองคิดให้ครบ flow + เผื่ออนาคต

---

## 1. Navigation map — ปรับหลัง adopt โครง Finny ทั้งแอป (2026-07-06)

```
nav หลัก: 3 tab — Overview | History | Budget  +  FAB expand (Income เขียว / Expense แดง)
          (เดิม 2 tab + FAB เดี่ยว — ตัด AI Log ปุ่มที่ 3 ของ Finny ออก ไม่เข้า scope)

Overview (เดิม Home/Stats รวมกัน — analytics dashboard)
 ├─ FAB expand → Income/Expense → Add sheet ──save──> Success toast ──> กลับ Overview
 ├─ card Expense vs Income + Total Expenditure (จาก Stats เดิม)
 ├─ ช่องเจาะไว้สำหรับ Go Pro banner — ไม่โชว์จริงตอนนี้ (dark launch)
 ├─ avatar ................ Settings / profile                    [future]
 └─ nav 📅 ................ History

History (🆕 แทน "รายการล่าสุด" เดิม — จุดที่ปอมชอบสุด)
 ├─ toggle ที่ collapsible header ... สลับ calendar view ↔ list view
 ├─ calendar view ......... ช่องวันที่โชว์ตัวเลขย่อ (เช่น "1.2k") ไม่ใช่แค่ dot
 ├─ list view ............. group by วัน (Today/Yesterday) พร้อม icon สีต่อหมวด
 ├─ tap แถวรายการ ......... Transaction detail ─┬─ แก้ไข → Add (prefilled)
 │                                              └─ ลบ → confirm → กลับ History
 ├─ tap หมวดในลิสต์ ........ Category detail (รายการในหมวดนั้น)     [next]
 └─ "ดูอินไซต์" ........... Insights (plain-language)            [ทำรอบนี้]

Budget (🆕 shell เฉยๆ v1 — ไม่มี logic คำนวณจริง)
 ├─ segmented เดือน (this month / ย้อนหลัง)
 └─ empty state "ยังไม่มี budget" — CTA ยังไม่ wire

Add sheet (full-screen, slide-up — เดิมเรียก bottom sheet)
 ├─ tap "เปลี่ยน" หมวด ..... Category picker (🟢 ทำรอบนี้)
 ├─ tap วันที่ ............. Date picker (calendar sheet ทับอีกที ตาม Finny)
 └─ amount → keypad

States ที่ผูกกับหน้า
 ├─ Overview ว่าง ......... Empty / first run (🟢 ทำรอบนี้)
 ├─ History ข้อมูล < 3 .... ซ่อนกราฟ โชว์ list (decision #6)
 ├─ Budget ............... empty state เสมอ v1 (ไม่มี logic)
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
7  Dark mode                  adopt จาก Finny ตั้งแต่ v1 เลย         🟢 ทำแล้ว (ไม่ใช่ mono อีกต่อไป —
                              (ไม่ต้องรอ token เผื่อแบบเดิม)          ดู rationale.md principle #1 ใหม่)
```

> หัวใจ: คู่แข่งแข่งที่ "ข้อมูลครบ" — Yiam แข่งที่ "ทำให้จดเป็นนิสัย + เข้าใจง่าย"
> ทุก feature ใหม่ต้องผ่านเกณฑ์: ไม่เพิ่ม friction การบันทึก + ไม่ทำให้รู้สึกผิด

---

## 3. ลำดับแนะนำ (ปรับหลัง adopt Finny 2026-07-06)
```
รอบนี้   nav 3-tab (Overview/History/Budget) + FAB expand · History calendar↔list toggle
        · Transaction detail · Empty · Success toast · Category picker · Insights
ถัดไป    Category detail · All transactions (search) · quick-add chips · Budget shell polish
อนาคต    Recurring · Weekly recap · Date picker · Settings · เปิด Go Pro จริง (ถ้าจะทำ)
```
> nav restructure ทำก่อนสุด เพราะกระทบทุกหน้าอื่น (ยิ่งช้ายิ่งต้อง retrofit)
