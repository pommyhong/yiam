# Yiam — Design Rationale

> ชื่อ "Yiam" ยืนยันแล้ว (2026-07-05) — จาก "เยี่ยม"
> Repo ของตัวเอง (~/Desktop/yiam · แยกจาก pmpg 2026-07-05 เพื่อ sync 2 เครื่อง) · Figma ยังทำผ่าน figma-cli ใน pmpg

---

## 1. Objective (โจทย์)
แอปบันทึกรายรับ–รายจ่ายส่วนตัว **ที่เน้นความง่าย** + มี analytics ให้เห็นภาพการใช้เงิน
- ไม่ใช่แอปการเงินครบวงจร — ตั้งใจตัด scope ให้บางที่สุดที่ยัง "มีประโยชน์"
- เป้า: ลองออกแบบแอปการเงินแบบ minimal ดู (แอปการเงินมักรก — อยากลอง simplify)

## 2. User (ใครใช้)
คนทั่วไปที่อยากรู้ว่าเงินหายไปไหน แต่ **เลิกใช้แอปการเงินเพราะมันยุ่งยาก**
- pain: บันทึกแล้วเหนื่อย, field เยอะ, ต้องผูกบัญชี, กราฟอ่านไม่รู้เรื่อง
- need: บันทึก 1 รายการจบใน <5 วิ + เปิดมาเห็นภาพรวมทันที
- mental model: "จด" ไม่ใช่ "ทำบัญชี"

## 3. Core value (ทำไมต้องมี)
```
User value   บันทึกเร็ว + เห็นภาพการใช้เงินโดยไม่ต้องตีความ
exploration  ลอง simplify แอปการเงินที่ปกติรก — เล่นกับ restraint
ความต่าง     คู่แข่งแข่งที่ "ฟีเจอร์" — เราลองแข่งที่ "ความเร็ว + ความสะอาด"
```

## 4. Scope (v1 — ปรับหลัง adopt โครง Finny ทั้งแอป 2026-07-06)
```
มี                              ตัดออก (ไว้ทีหลัง)
──────────────────────────────────────────────────────
✓ บันทึก จ่าย/รับ               ✗ ผูกบัญชีธนาคาร / auto-sync
✓ หมวดหมู่ + วันที่ + note       ✗ AI Log (voice/AI input) — ตัดออกจาก scope เลย
✓ รายการ + ยอดสรุปเดือน          ✗ รายการประจำ (recurring)
✓ analytics by category          ✗ หลายสกุลเงิน
✓ แก้ / ลบ                       ✗ export / รายงาน
✓ Budget tab (shell เฉยๆ)        ✗ Go Pro ใช้งานจริง — เจาะช่องไว้เฉยๆ ยังไม่โชว์/ไม่ wire
  ไม่มี logic คำนวณจริง v1
✓ History แบบ calendar+list       
  (2 mode, toggle ได้)
```
> เหตุผล scope เปลี่ยน: ตัดสินใจ adopt โครง UI/UX ทั้งแอปของ Finny (getfinny.app) มาเป็น template ก่อน แล้วค่อย personalize ทีหลัง — Budget/History กลับเข้า scope เป็น "โครงหน้าตา" ไม่ใช่ฟีเจอร์ทำงานเต็ม, auto-sync ยังตัดออกเหมือนเดิมเพราะทำไม่ได้จริง (ต้อง partnership Apple ระดับธนาคาร) ส่วน "tap to track" ที่ชอบใช้ Quick Log ผ่าน iOS Shortcut แทน

## 5. Success metric (วัดว่าออกแบบสำเร็จ)
```
เวลาในการบันทึก 1 รายการ      < 5 วินาที (จากกด ⊕ ถึง saved)
จำนวน tap ขั้นต่ำต่อ 1 รายการ  ≤ 5 (FAB expand → เลือก income/expense → amount → category → save)
                              — ขยับจาก ≤4 เพราะ FAB expand เพิ่ม 1 tap ก่อนเข้า flow เดิม
เปิดแอปแล้วเข้าใจภาพรวม         ภายใน 1 หน้าจอ ไม่ต้อง scroll
```

## 6. Design principles (anchor ที่ใช้ตัดสินใจ) — ปรับหลัง adopt Finny 2026-07-06
1. **สีสื่อหมวดหมู่ ตัวเลขยังใหญ่สุดในลำดับชั้นเสมอ** (เดิม "ตัวเลขเป็นพระเอก ไม่ใช่สี") — สีหลากหลายต่อหมวดใช้เพื่อ recognition ไม่ใช่ตกแต่ง, ตัวเลขยังคงเป็น element ใหญ่สุดในทุกหน้าจอเสมอ — คนละหน้าที่กัน ไม่ได้แข่งกัน
2. **Default ฉลาด** — จ่าย=default, วันนี้=default, ลดการตัดสินใจ
3. **ตัด > เพิ่ม** — ทุก field ต้อง defend ได้ว่าทำไมไม่ตัด (เหตุผลที่ตัด AI Log ปุ่มที่ 3 ออก)
4. **เห็นผลทันที** — บันทึกเสร็จเห็นรายการขึ้น, เปิด stats เห็นภาพเลย
> framework: NN/g (recognition over recall, aesthetic-minimalist) + Peak-End (จังหวะ "saved ✓")

## 7. Key decisions (พร้อม trade-off) — ปรับหลัง adopt โครง Finny ทั้งแอป (2026-07-06)
```
decision                เลือก                        trade-off
────────────────────────────────────────────────────────────────────
nav                     3 tab (Overview/History/     ขยาย IA จาก 2 tab เดิม — AI Log ปุ่มที่ 3
                        Budget) + FAB expand           ของ Finny ตัดออก เหลือ Income/Expense
                        (Income เขียว/Expense แดง)     2 ปุ่มพอ

เพิ่มรายการ              full-screen sheet             ยังนับเป็น "sheet" (slide-up transition)
                        (slide-up)                     แค่ปรับคำอธิบายจาก bottom sheet ครึ่งจอ

สี                      หลากสีต่อหมวด + dark theme     เปลี่ยนจาก mono เดิม — ต้องคุมด้วย principle #1
                        (adopt จาก Finny)               ใหม่ไม่งั้นตัวเลขจะแย่งซีนกับสีหมวด

History                 2 mode: calendar (เปิด) /      calendar cell โชว์ตัวเลขย่อ (เช่น "1.2k")
                        list (ปิด) — toggle ที่         ไม่ใช่แค่ dot — รกกว่าแต่เห็นภาพไวกว่า
                        collapsible header

Budget tab              shell เฉยๆ (segmented เดือน   ไม่มี logic คำนวณจริง v1 — ทำแค่ให้ "รู้สึกครบ"
                        + empty state)                  เหมือน Finny โดยไม่ over-engineer

Go Pro                  เจาะช่องไว้ในเลย์เอาต์          ไม่โชว์/ไม่ wire ตอนนี้ — กันไม่ให้แย่ง
                        Overview แต่ไม่โชว์จริง          attention จากตัวเลขจริง, เปิดทีหลังง่ายกว่า
                                                        ลบแล้วออกแบบใหม่

category                preset list                    ยังไม่ให้ custom (v2, ตรงกับ [PRO] gate ของ
                                                        Finny ที่เราปิดไว้ก่อน)
```

## 8. Risks / open questions
- บันทึก manual ล้วน → user จะขยันจดไหม? (mitigate: เร็วที่สุดเท่าที่ทำได้ + Quick Log ผ่าน iOS Shortcut)
- "ง่าย" กับ "มี analytics ลึก" ขัดกันเอง → analytics ต้อง progressive (ภาพรวมก่อน เจาะทีหลัง)
- **Adopt-then-personalize (ใหม่ 2026-07-06):** รอบแรก clone โครง Finny เกือบทั้งหมด (nav, สี, Budget shell, Go Pro slot) — เสี่ยงไม่เหลือ "รสนิยมปอมเอง" ถ้าไม่ personalize จริงจังรอบสอง → ต้อง treat รอบนี้เป็น skeleton ชั่วคราว ไม่ใช่ final
- Budget shell + Go Pro slot ที่ไม่ wire อะไรจริง อาจดู "ครึ่งๆ กลางๆ" ถ้าโชว์ไม่ระวัง → คุมด้วย empty state ที่ชัดเจนว่า "ยังไม่เปิดใช้" ไม่ใช่ bug

---
_living doc — อัปเดตเมื่อ decision เปลี่ยน_
