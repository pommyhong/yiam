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

## 4. Scope (v1 — ปรับรอบ 2 หลังปอมส่ง reference เพิ่ม 2026-07-06)
```
มี                              ตัดออก (ไว้ทีหลัง)
──────────────────────────────────────────────────────
✓ บันทึก จ่าย/รับ               ✗ ผูกบัญชีธนาคาร / auto-sync
✓ หมวดหมู่ + วันที่ + note       ✗ AI Log (voice/AI input) — ตัดออกจาก scope เลย
  + paid with + recurring flag  ✗ หลายสกุลเงิน
✓ รายการ + ยอดสรุปเดือน          ✗ รายการประจำ "auto-detect" — เอาแค่ manual
✓ analytics: donut breakdown      flag พอ (recurring detect ผูกธนาคารไม่ได้อยู่แล้ว)
  + Trend/Compare toggle        ✗ export / รายงาน
✓ แก้ / ลบ (swipe บน list)      ✗ Go Pro ใช้งานจริง — เจาะช่องไว้เฉยๆ ยังไม่โชว์/ไม่ wire
✓ Budget: CRUD เต็ม              ✗ เปลี่ยนภาษา/ฟอนต์ — parked ไว้คุยรอบหน้า
  (name/categories/rollover/
  progress) — ยกเลิก "shell เฉยๆ"
✓ Recurring section (manual      
  flag เท่านั้น ไม่ auto-detect)  
✓ Settings (ชื่อ/avatar/logout)  
✓ History แบบ calendar+list       
  (2 mode, toggle ได้)
```
> **Reversal 2026-07-06 (รอบ 2):** Budget พลิกจาก "shell เฉยๆ ไม่มี logic" (รอบแรก) เป็น **CRUD เต็ม** ตามที่ปอมส่ง reference ครบ flow (New Budget form + progress card) · Recurring ที่เคยตัดออกทั้งหมดกลับมาบางส่วน — แบบ **manual toggle เท่านั้น** (user กดเองว่า "รายการนี้ประจำ") ไม่ใช่ auto-detect จากแบงก์ (อันนั้นยังทำไม่ได้เหมือนเดิม) · เพิ่ม Settings เข้า scope ใหม่ทั้งหมด (ผูกกับ Firebase Auth ที่กำลังต่ออยู่)

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

Budget tab              CRUD เต็ม (New Budget:         พลิกจาก "shell เฉยๆ" รอบแรก — เพิ่ม logic
                        name/categories/rollover/       จริง (rollover คำนวณยอดเหลือข้ามเดือน,
                        start month) + progress card    progress % ต้องอัปเดตตาม transaction จริง)
                        + swipe-to-delete               → effort เพิ่มชัดเจนจากรอบแรก

Recurring               manual flag ต่อรายการ           ไม่ทำ auto-detect (ผูกธนาคารไม่ได้จริง
                        (toggle ตอน add/edit) +          เหมือนเดิม) — ผู้ใช้ต้อง tag เองว่ารายการ
                        section ใน Overview              ไหน "ประจำ" ถึงจะขึ้น section นี้

Settings                ใหม่ทั้งหมด — แก้ชื่อ, avatar   ผูกกับ Firebase Auth ที่กำลังต่ออยู่ —
                        (สี/initial), log out            log out ใน mockup นี้เป็น placeholder
                                                        ก่อน (ยังไม่มี auth จริงให้ออกจากระบบ)

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
- **Budget CRUD (ใหม่ 2026-07-06):** rollover math ผิดพลาดง่าย (ยอดเหลือเดือนก่อนต้องบวกเข้าเดือนถัดไปถูกจังหวะ) → ต้อง test กับข้อมูลหลายเดือนก่อนเชื่อตัวเลข
- Settings ผูกกับ Firebase Auth ที่ยังไม่เสร็จ (รอ config จากปอม) → mockup นี้ log out จะเป็นแค่ placeholder ไปก่อน ยังไม่ตัดการเชื่อมต่อจริง

## 9. Backend (ตัดสินใจ 2026-07-06 — เปลี่ยนจาก Google Sheets)
```
เดิม (rejected)   Google Sheet + Apps Script Web App        เหตุผลที่เปลี่ยน:
                  — สร้าง Sheet ไว้แล้ว ("pmpg - yiam DB")   - deploy versioning gotcha (ลืมกด
                  แต่ยังไม่ deploy Apps Script จริง            "New version" = รันโค้ดเก่าค้าง)
                                                            - เจอปัญหาเข้า Sheet บนคอมบริษัทไม่ได้
                                                            - multi-user ต้อง duplicate setup
                                                            ให้เพื่อนแต่ละคนเอง ไม่มี auth จริง

เลือกใหม่          Firebase (Firestore + Auth)               - ฟรีตลอดไป ไม่ "หลับ" เหมือน Supabase
                                                            - Auth สำเร็จรูป (Google sign-in) ไม่ต้อง
                                                            เขียนเอง — แก้โจทย์ multi-user ได้ตรง
                                                            - ไม่มี deploy-versioning gotcha แบบ
                                                            Apps Script
```
> เหตุผลเปลี่ยนใจ: กลัวว่าวันหนึ่งจะมีคนใช้มากกว่าแค่ 2-3 เพื่อน — ถ้าเกิดขึ้นจริง อยากมี auth กลางที่ scale ได้ทันทีไม่ต้อง migrate อีกรอบ · ตัดสินใจตอน sunk cost ยังต่ำ (ยังไม่ได้ deploy Apps Script จริง) จึงเปลี่ยนตอนนี้คุ้มกว่าเปลี่ยนทีหลัง
> Sheet "pmpg - yiam DB" ที่สร้างไว้ — ปล่อยทิ้งได้เลย ไม่ต้องลบ ไม่กระทบอะไร (ไม่เคยต่อกับอะไรจริง)

## 9b. Firebase ต่อจริงแล้ว (2026-07-07)
```
Auth      Google sign-in ผ่าน Firebase Auth — มีหน้า login ก่อนเข้าแอป (ไม่ auth ไม่เห็นข้อมูล)
Data      1 doc ต่อ user ที่ users/{uid} — field: transactions[], budgets[], settings{}
          (ไม่ normalize เป็น subcollection แยกต่อรายการ — เอกสารเดียวพอสำหรับ scale
          ระดับเพื่อนไม่กี่คน ไม่ over-engineer)
Sync      onSnapshot realtime — แก้เครื่องนึง อีกเครื่อง/มือถือเห็นสดเลยไม่ต้อง refresh
Offline   enableIndexedDbPersistence — เปิดแอปตอนเน็ตหลุดยังเห็นข้อมูลเดิม (cache)
```
> localStorage เดิมถูกถอดออกจาก mockup แล้ว (เคยใช้ตอนยังไม่มี backend) — ข้อมูลทั้งหมดอยู่ Firestore
> **ต้องทำเพิ่มก่อนใช้งานจริง:** (1) วาง Firestore security rules (2) เพิ่ม `pommyhong.github.io` ใน Authorized domains ของ Firebase Auth — ไม่งั้น sign-in จะ error `unauthorized-domain`
> Sign-in ทดสอบได้เฉพาะบน URL จริง (pommyhong.github.io/yiam) เท่านั้น — เปิดไฟล์ local (file://) ผ่าน Google OAuth ไม่ได้

## 10. Polish round (2026-07-07 — ตาม reference เพิ่มเติมจากปอม)
```
Font              Noto Sans Thai (UI ทั้งหมด) + Noto Serif Thai (เฉพาะ headline "เงินของเรา...")
i18n              th/en toggle ใน Settings — แปล chrome หลักครบ (nav, header, ปุ่ม, empty state,
                  ชื่อหมวด/วิธีจ่าย, ชื่อเดือน/วันในสัปดาห์) · โน้ต/ชื่อ budget ที่ผู้ใช้พิมพ์เองไม่แปล
Period nav        ‹ › เปลี่ยนช่วงเวลาได้ (week/month/year) ตาม reference "swipe charts to browse periods"
                  (ใช้ปุ่มลูกศรแทน swipe จริงเพื่อความเร็ว)
Donut toggle      ⇄ สลับ expense/income breakdown ได้ + ‹ › cycle โฟกัสรายหมวดกลางวงกลม
                  (Recurring card มี toggle เดียวกัน)
Splash + icon     หน้า splash สั้นๆ (~900ms) ตอนเปิด + app icon (icon.svg/icon-180.png/icon-512.png
                  + manifest.json) ให้ "Add to Home Screen" ได้ไอคอนจริงไม่ใช่ screenshot
Micro-interaction bar/donut entrance animation, number count-up, FAB press bounce, chip select
                  bounce, success checkmark burst ตอน save, budget card stagger-in
```
> ยังไม่ทำ: swipe gesture จริงบนกราฟ (ใช้ปุ่มลูกศรแทนก่อน), แปลชื่อหมวด custom (v2 ยังไม่มี custom category)

---
_living doc — อัปเดตเมื่อ decision เปลี่ยน_
