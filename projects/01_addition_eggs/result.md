### 📝 แบบฝึกหัดที่ 1: เปลี่ยนจำนวนไข่
```c
// หาบรรทัดนี้ในโค้ด:
int eggs_already_have = 4;    // ไข่ไก่ที่แม่มีอยู่แล้ว
int eggs_new_today = 2;       // ไข่ไก่ที่ไก่ออกวันนี้

// ลองเปลี่ยนเป็น:
int eggs_already_have = 8;    // เพิ่มเป็น 8 ฟอง
int eggs_new_today = 3;       // เพิ่มเป็น 3 ฟอง
```

## result
```c
I (2304) EGGS_MATH: 🥚 เริ่มต้นโปรแกรมนับไข่ไก่ของแม่ 🥚
I (2304) EGGS_MATH: =====================================
I (2304) EGGS_MATH: 📖 โจทย์:
I (2304) EGGS_MATH:    แม่มีไข่ไก่อยู่แล้ว: 8 ฟอง
I (2304) EGGS_MATH:    เมื่อเช้าไก่ออกไข่เพิ่ม: 3 ฟอง
I (2304) EGGS_MATH:    ❓ วันนี้แม่มีไข่ไก่รวมกี่ฟอง?
I (2304) EGGS_MATH: 
I (5304) EGGS_MATH: 🧮 ขั้นตอนการคิด:
I (5304) EGGS_MATH:    ไข่ไก่ที่มีอยู่ + ไข่ไก่ที่ออกใหม่
I (5304) EGGS_MATH:    = 8 + 3
I (5304) EGGS_MATH:    = 11 ฟอง
I (5304) EGGS_MATH: 
I (5304) EGGS_MATH: ✅ คำตอบ:
I (5304) EGGS_MATH:    วันนี้แม่มีไข่ไก่ทั้งหมด 11 ฟอง
I (5304) EGGS_MATH: 
I (5304) EGGS_MATH: 🎨 ภาพประกอบ:
I (5304) EGGS_MATH:    ไข่เดิม: 🥚🥚🥚🥚 (8 ฟอง)
I (5304) EGGS_MATH:    ไข่ใหม่: 🥚🥚 (3 ฟอง)
I (5304) EGGS_MATH:    รวม:    🥚🥚🥚🥚🥚🥚 (11 ฟอง)
I (5304) EGGS_MATH: 
I (5314) EGGS_MATH: 💡 ตัวอย่างเพิ่มเติม:
I (5314) EGGS_MATH:    ถ้าแม่มีไข่ 7 ฟอง และไก่ออกไข่ 3 ฟอง
I (5314) EGGS_MATH:    จะได้ไข่ทั้งหมด 7 + 3 = 10 ฟอง
I (5314) EGGS_MATH: 
I (5314) EGGS_MATH:    ถ้าแม่มีไข่ 10 ฟอง และไก่ออกไข่ 5 ฟอง
I (5314) EGGS_MATH:    จะได้ไข่ทั้งหมด 10 + 5 = 15 ฟอง
I (5314) EGGS_MATH: 
I (5314) EGGS_MATH: 📚 สิ่งที่เรียนรู้:
I (5314) EGGS_MATH:    1. การบวกเลข (Addition): a + b = c
I (5314) EGGS_MATH:    2. การใช้ตัวแปร (Variables) เก็บค่า
I (5314) EGGS_MATH:    3. การแสดงผลด้วย ESP_LOGI
I (5314) EGGS_MATH:    4. การแก้โจทย์แบบมีขั้นตอน
I (5314) EGGS_MATH: 
I (5314) EGGS_MATH: 🎉 จบโปรแกรมนับไข่ไก่ของแม่!
I (5314) EGGS_MATH: 📖 อ่านต่อในโปรเจคถัดไป: 02_subtraction_toys
I (7314) main_task: Returned from app_main()
```
### 📝 แบบฝึกหัดที่ 2: เพิ่มไข่เป็ด
เพิ่มโค้ดนี้หลังบรรทัด `int total_eggs;`:
```c
int duck_eggs = 3;            // ไข่เป็ดที่แม่มี
int total_all_eggs;           // ไข่ทั้งหมด (ไก่ + เป็ด)
```

แล้วเพิ่มการคำนวณหลังบรรทัด `total_eggs = eggs_already_have + eggs_new_today;`:
```c
total_all_eggs = total_eggs + duck_eggs;

// แสดงผลไข่เป็ด
ESP_LOGI(TAG, "🦆 และแม่มีไข่เป็ด: %d ฟอง", duck_eggs);
ESP_LOGI(TAG, "🥚 ไข่ทั้งหมด (ไก่+เป็ด): %d ฟอง", total_all_eggs);
```
## result
```c
I (2402) EGGS_MATH: 🥚 เริ่มต้นโปรแกรมนับไข่ไก่ของแม่ 🥚
I (2402) EGGS_MATH: =====================================
I (2402) EGGS_MATH: 📖 โจทย์:
I (2402) EGGS_MATH:    แม่มีไข่ไก่อยู่แล้ว: 8 ฟอง
I (2402) EGGS_MATH:    เมื่อเช้าไก่ออกไข่เพิ่ม: 3 ฟอง
I (2402) EGGS_MATH:    ❓ วันนี้แม่มีไข่ไก่รวมกี่ฟอง?
I (2402) EGGS_MATH: 
I (5402) EGGS_MATH: 🦆 และแม่มีไข่เป็ด: 3 ฟอง
I (5402) EGGS_MATH: 🥚 ไข่ทั้งหมด (ไก่+เป็ด): 14 ฟอง
I (5402) EGGS_MATH: 🧮 ขั้นตอนการคิด:
I (5402) EGGS_MATH:    ไข่ไก่ที่มีอยู่ + ไข่ไก่ที่ออกใหม่
I (5402) EGGS_MATH:    = 8 + 3
I (5402) EGGS_MATH:    = 11 ฟอง
I (5402) EGGS_MATH: 
I (5402) EGGS_MATH: ✅ คำตอบ:
I (5402) EGGS_MATH:    วันนี้แม่มีไข่ไก่ทั้งหมด 11 ฟอง
I (5402) EGGS_MATH: 
I (5402) EGGS_MATH: 🎨 ภาพประกอบ:
I (5402) EGGS_MATH:    ไข่เดิม: 🥚🥚🥚🥚 (8 ฟอง)
I (5402) EGGS_MATH:    ไข่ใหม่: 🥚🥚 (3 ฟอง)
I (5402) EGGS_MATH:    รวม:    🥚🥚🥚🥚🥚🥚 (11 ฟอง)
I (5402) EGGS_MATH: 
I (5402) EGGS_MATH: 💡 ตัวอย่างเพิ่มเติม:
I (5402) EGGS_MATH:    ถ้าแม่มีไข่ 7 ฟอง และไก่ออกไข่ 3 ฟอง
I (5402) EGGS_MATH:    จะได้ไข่ทั้งหมด 7 + 3 = 10 ฟอง
I (5402) EGGS_MATH: 
I (5402) EGGS_MATH:    ถ้าแม่มีไข่ 10 ฟอง และไก่ออกไข่ 5 ฟอง
I (5402) EGGS_MATH:    จะได้ไข่ทั้งหมด 10 + 5 = 15 ฟอง
I (5402) EGGS_MATH: 
I (5402) EGGS_MATH: 📚 สิ่งที่เรียนรู้:
I (5402) EGGS_MATH:    1. การบวกเลข (Addition): a + b = c
I (5402) EGGS_MATH:    2. การใช้ตัวแปร (Variables) เก็บค่า
I (5402) EGGS_MATH:    3. การแสดงผลด้วย ESP_LOGI
I (5402) EGGS_MATH:    4. การแก้โจทย์แบบมีขั้นตอน
I (5402) EGGS_MATH: 
I (5402) EGGS_MATH: 🎉 จบโปรแกรมนับไข่ไก่ของแม่!
I (5402) EGGS_MATH: 📖 อ่านต่อในโปรเจคถัดไป: 02_subtraction_toys
I (7402) main_task: Returned from app_main()
```

### 📝 แบบฝึกหัดที่ 3: สร้างโจทย์ของตัวเอง
ลองเปลี่ยนเป็นโจทย์อื่น เช่น:
- 🍎 แอปเปิ้ลในตะกร้า
- 📚 หนังสือบนชั้น  
- 🚗 รถในลานจอด
- 🌟 ดาวในท้องฟ้า

## result
```c
I (2371) str_MATH: 🌟เริ่มต้นโปรแกรมนับ🌟
I (2371) str_MATH: =====================================
I (2371) str_MATH: 📖 โจทย์:
I (2371) str_MATH:    มีดาวอยู่แล้ว: 5 ดวง
I (2371) str_MATH:    ดาวตก: 3 ดวง
I (2371) str_MATH:    ❓ วันนี้มีดาวกี่ดวง?
I (2371) str_MATH: 
I (5371) str_MATH: 🧮 ขั้นตอนการคิด:
I (5371) str_MATH:    ดาวที่มีอยู่ - ดาวตก
I (5371) str_MATH:    = 5 - 3
I (5371) str_MATH:    = 2 ดวง
I (5371) str_MATH: 
I (5371) str_MATH: ✅ คำตอบ:
I (5371) str_MATH:    วันนี้มีดาวทั้งหมด 2 ดวง
I (5371) str_MATH: 
I (5371) str_MATH: 🎨 ภาพประกอบ:
I (5371) str_MATH:    ดาวเดิม: 🌟🌟🌟🌟🌟 (5 ดวง)
I (5371) str_MATH:    ไข่ใหม่: 🌟🌟🌟 (3 ดวง)
I (5371) str_MATH:    รวม:    🌟🌟 (2 ดวง)
I (5371) str_MATH: 
I (7371) main_task: Returned from app_main()
```
