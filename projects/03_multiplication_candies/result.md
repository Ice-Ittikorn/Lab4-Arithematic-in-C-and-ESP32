### 📝 แบบฝึกหัดที่ 1: เปลี่ยนจำนวนถุงลูกอม
```c
// หาบรรทัดนี้ในโค้ด:
int candy_bags = 5;         // จำนวนถุง
int candies_per_bag = 6;    // ลูกอมต่อถุง

// ลองเปลี่ยนเป็น:
int candy_bags = 7;         // เพิ่มเป็น 7 ถุง
int candies_per_bag = 8;    // ลูกอมถุงละ 8 เม็ด
```

### Result
```c
I (2464) CANDIES_MATH: 🍬 เริ่มต้นโปรแกรมนับลูกอมในถุง 🍬
I (2464) CANDIES_MATH: ====================================
I (2464) CANDIES_MATH: 📖 โจทย์:
I (2464) CANDIES_MATH:    มีถุงลูกอม: 7 ถุง
I (2464) CANDIES_MATH:    ถุงละ: 8 เม็ด
I (2464) CANDIES_MATH:    ❓ มีลูกอมทั้งหมดกี่เม็ด?
I (2464) CANDIES_MATH: 
I (5464) CANDIES_MATH: 🧮 ขั้นตอนการคิด:
I (5464) CANDIES_MATH:    จำนวนถุง × ลูกอมต่อถุง
I (5464) CANDIES_MATH:    = 7 × 8
I (5464) CANDIES_MATH:    = 56 เม็ด
I (5464) CANDIES_MATH: 
I (5464) CANDIES_MATH: ✅ คำตอบ:
I (5464) CANDIES_MATH:    มีลูกอมทั้งหมด 56 เม็ด
I (5464) CANDIES_MATH: 
I (5464) CANDIES_MATH: 🎨 ภาพประกอบ:
I (5464) CANDIES_MATH:    ถุงที่ 1: 🍬🍬🍬🍬🍬🍬 (8 เม็ด)
I (5464) CANDIES_MATH:    ถุงที่ 2: 🍬🍬🍬🍬🍬🍬 (8 เม็ด)
I (5464) CANDIES_MATH:    ถุงที่ 3: 🍬🍬🍬🍬🍬🍬 (8 เม็ด)
I (5464) CANDIES_MATH:    ถุงที่ 4: 🍬🍬🍬🍬🍬🍬 (8 เม็ด)
I (5464) CANDIES_MATH:    ถุงที่ 5: 🍬🍬🍬🍬🍬🍬 (8 เม็ด)
I (5464) CANDIES_MATH:    รวม:     56 เม็ด
I (5464) CANDIES_MATH: 
I (5464) CANDIES_MATH: 🔄 เปรียบเทียบกับการบวกซ้ำๆ:
I (5464) CANDIES_MATH:    การคูณ: 7 × 8 = 56
I (5464) CANDIES_MATH:    การบวกซ้ำๆ:
I (5464) CANDIES_MATH:                   8
I (5474) CANDIES_MATH:                 + 8
I (5474) CANDIES_MATH:                 + 8
I (5474) CANDIES_MATH:                 + 8
I (5474) CANDIES_MATH:                 + 8
I (5474) CANDIES_MATH:                 + 8
I (5474) CANDIES_MATH:                 + 8 = 56
I (5474) CANDIES_MATH:    ผลลัพธ์เหมือนกัน! การคูณคือการบวกซ้ำๆ
I (5474) CANDIES_MATH: 
I (5474) CANDIES_MATH: 📊 ตารางสูตรคูณ 8:
I (5474) CANDIES_MATH:    1 × 8 = 8
I (5774) CANDIES_MATH:    2 × 8 = 16
I (6074) CANDIES_MATH:    3 × 8 = 24
I (6374) CANDIES_MATH:    4 × 8 = 32
I (6674) CANDIES_MATH:    5 × 8 = 40
I (6974) CANDIES_MATH:    6 × 8 = 48
I (7274) CANDIES_MATH:    7 × 8 = 56
I (7574) CANDIES_MATH:    8 × 8 = 64
I (7874) CANDIES_MATH:    9 × 8 = 72
I (8174) CANDIES_MATH:    10 × 8 = 80
I (8474) CANDIES_MATH: 
I (8474) CANDIES_MATH: 💡 ตัวอย่างเพิ่มเติม:
I (8474) CANDIES_MATH:    ถ้ามีถุงลูกอม 3 ถุง ถุงละ 8 เม็ด
I (8474) CANDIES_MATH:    จะได้ลูกอม 3 × 8 = 24 เม็ด
I (8474) CANDIES_MATH: 
I (8474) CANDIES_MATH:    ถ้ามีถุงลูกอม 7 ถุง ถุงละ 4 เม็ด
I (8474) CANDIES_MATH:    จะได้ลูกอม 7 × 4 = 28 เม็ด
I (8474) CANDIES_MATH: 
I (8474) CANDIES_MATH: 🔄 เปรียบเทียบการดำเนินการ:
I (8474) CANDIES_MATH:    การบวก (+): เพิ่มจำนวน (เช่น ไข่ 4 + 2 = 6)
I (8474) CANDIES_MATH:    การลบ (-): ลดจำนวน (เช่น ของเล่น 8 - 3 = 5)
I (8474) CANDIES_MATH:    การคูณ (×): บวกซ้ำๆ (เช่น ลูกอม 5 × 6 = 30)
I (8474) CANDIES_MATH: 
I (8474) CANDIES_MATH: 🎓 แนวคิดขั้นสูง:
I (8474) CANDIES_MATH:    1. การคูณมีคุณสมบัติการสับเปลี่ยน:
I (8484) CANDIES_MATH:       7 × 8 = 8 × 7 = 56
I (8484) CANDIES_MATH:    2. การคูณด้วย 0 จะได้ 0 เสมอ:
I (8484) CANDIES_MATH:       7 × 0 = 0 (ไม่มีถุงลูกอม)
I (8484) CANDIES_MATH:    3. การคูณด้วย 1 จะได้ตัวเลขเดิม:
I (8484) CANDIES_MATH:       8 × 1 = 8 (มีถุงเดียว)
I (8484) CANDIES_MATH: 
I (8484) CANDIES_MATH: 📚 สิ่งที่เรียนรู้:
I (8484) CANDIES_MATH:    1. การคูณเลข (Multiplication): a × b = c
I (8484) CANDIES_MATH:    2. การใช้ for loop สำหรับการทำซ้ำ
I (8484) CANDIES_MATH:    3. ความสัมพันธ์ระหว่างการคูณและการบวกซ้ำๆ
I (8484) CANDIES_MATH:    4. คุณสมบัติพิเศษของการคูณ
I (8484) CANDIES_MATH:    5. การแสดงผลแบบตาราง
I (8484) CANDIES_MATH: 
I (8484) CANDIES_MATH: 🎉 จบโปรแกรมนับลูกอมในถุง!
I (8484) CANDIES_MATH: 📖 อ่านต่อในโปรเจคถัดไป: 04_division_cookies
I (10484) main_task: Returned from app_main()
```

### 📝 แบบฝึกหัดที่ 2: เพิ่มลูกอมหลายรส
เพิ่มลูกอมหลายรส:
```c
int strawberry_bags = 3;    // ถุงรสสตรอเบอร์รี่
int orange_bags = 2;        // ถุงรสส้ม
int grape_bags = 4;         // ถุงรสองุ่น

int total_bags = strawberry_bags + orange_bags + grape_bags;
int total_candies = total_bags * candies_per_bag;

ESP_LOGI(TAG, "🍓 สตรอเบอร์รี่: %d ถุง = %d เม็ด", 
         strawberry_bags, strawberry_bags * candies_per_bag);
ESP_LOGI(TAG, "🍊 รสส้ม: %d ถุง = %d เม็ด", 
         orange_bags, orange_bags * candies_per_bag);
ESP_LOGI(TAG, "🍇 รสองุ่น: %d ถุง = %d เม็ด", 
         grape_bags, grape_bags * candies_per_bag);
```

##resullt
```c
I (2458) CANDIES_MATH: 🍬 เริ่มต้นโปรแกรมนับลูกอมในถุง 🍬
I (2458) CANDIES_MATH: ====================================
I (2458) CANDIES_MATH: 📖 โจทย์:
I (2458) CANDIES_MATH:    มีถุงลูกอม: 7 ถุง
I (2458) CANDIES_MATH:    ถุงละ: 8 เม็ด
I (2458) CANDIES_MATH:    ❓ มีลูกอมทั้งหมดกี่เม็ด?
I (2458) CANDIES_MATH: 
I (5458) CANDIES_MATH: 🧮 ขั้นตอนการคิด:
I (5458) CANDIES_MATH:    จำนวนถุง × ลูกอมต่อถุง
I (5458) CANDIES_MATH:    = 7 × 8
I (5458) CANDIES_MATH:    = 56 เม็ด
I (5458) CANDIES_MATH: 
I (5458) CANDIES_MATH: ✅ คำตอบ:
I (5458) CANDIES_MATH:    มีลูกอมทั้งหมด 56 เม็ด
I (5458) CANDIES_MATH: 
I (5458) CANDIES_MATH: 🎨 ภาพประกอบ:
I (5458) CANDIES_MATH:    ถุงที่ 1: 🍬🍬🍬🍬🍬🍬 (8 เม็ด)
I (5458) CANDIES_MATH:    ถุงที่ 2: 🍬🍬🍬🍬🍬🍬 (8 เม็ด)
I (5458) CANDIES_MATH:    ถุงที่ 3: 🍬🍬🍬🍬🍬🍬 (8 เม็ด)
I (5458) CANDIES_MATH:    ถุงที่ 4: 🍬🍬🍬🍬🍬🍬 (8 เม็ด)
I (5458) CANDIES_MATH:    ถุงที่ 5: 🍬🍬🍬🍬🍬🍬 (8 เม็ด)
I (5458) CANDIES_MATH:    รวม:     56 เม็ด
I (5458) CANDIES_MATH: 
I (5458) CANDIES_MATH: 🔄 เปรียบเทียบกับการบวกซ้ำๆ:
I (5458) CANDIES_MATH:    การคูณ: 7 × 8 = 56
I (5458) CANDIES_MATH:    การบวกซ้ำๆ:
I (5458) CANDIES_MATH:                   8
I (5458) CANDIES_MATH:                 + 8
I (5458) CANDIES_MATH:                 + 8
I (5468) CANDIES_MATH:                 + 8
I (5468) CANDIES_MATH:                 + 8
I (5468) CANDIES_MATH:                 + 8
I (5468) CANDIES_MATH:                 + 8 = 56
I (5468) CANDIES_MATH:    ผลลัพธ์เหมือนกัน! การคูณคือการบวกซ้ำๆ
I (5468) CANDIES_MATH: 
I (5468) CANDIES_MATH: 📊 ตารางสูตรคูณ 8:
I (5468) CANDIES_MATH:    1 × 8 = 8
I (5768) CANDIES_MATH:    2 × 8 = 16
I (6068) CANDIES_MATH:    3 × 8 = 24
I (6368) CANDIES_MATH:    4 × 8 = 32
I (6668) CANDIES_MATH:    5 × 8 = 40
I (6968) CANDIES_MATH:    6 × 8 = 48
I (7268) CANDIES_MATH:    7 × 8 = 56
I (7568) CANDIES_MATH:    8 × 8 = 64
I (7868) CANDIES_MATH:    9 × 8 = 72
I (8168) CANDIES_MATH:    10 × 8 = 80
I (8468) CANDIES_MATH: 
I (8468) CANDIES_MATH: 💡 ตัวอย่างเพิ่มเติม:
I (8468) CANDIES_MATH:    ถ้ามีถุงลูกอม 3 ถุง ถุงละ 8 เม็ด
I (8468) CANDIES_MATH:    จะได้ลูกอม 3 × 8 = 24 เม็ด
I (8468) CANDIES_MATH: 
I (8468) CANDIES_MATH:    ถ้ามีถุงลูกอม 7 ถุง ถุงละ 4 เม็ด
I (8468) CANDIES_MATH:    จะได้ลูกอม 7 × 4 = 28 เม็ด
I (8468) CANDIES_MATH: 
I (8468) CANDIES_MATH: 🍭 ลูกอมหลายรส:
I (8468) CANDIES_MATH: 🍓 สตรอเบอร์รี่: 3 ถุง = 24 เม็ด
I (8468) CANDIES_MATH: 🍊 รสส้ม: 2 ถุง = 16 เม็ด
I (8468) CANDIES_MATH: 🍇 รสองุ่น: 4 ถุง = 32 เม็ด
I (8468) CANDIES_MATH: 🧮 รวมทั้งหมด: 9 ถุง × 8 เม็ด = 72 เม็ด
I (8468) CANDIES_MATH: 
I (8468) CANDIES_MATH: 🔄 เปรียบเทียบการดำเนินการ:
I (8468) CANDIES_MATH:    การบวก (+): เพิ่มจำนวน (เช่น ไข่ 4 + 2 = 6)
I (8478) CANDIES_MATH:    การลบ (-): ลดจำนวน (เช่น ของเล่น 8 - 3 = 5)
I (8478) CANDIES_MATH:    การคูณ (×): บวกซ้ำๆ (เช่น ลูกอม 5 × 6 = 30)
I (8478) CANDIES_MATH: 
I (8478) CANDIES_MATH: 🎓 แนวคิดขั้นสูง:
I (8478) CANDIES_MATH:    1. การคูณมีคุณสมบัติการสับเปลี่ยน:
I (8478) CANDIES_MATH:       7 × 8 = 8 × 7 = 56
I (8478) CANDIES_MATH:    2. การคูณด้วย 0 จะได้ 0 เสมอ:
I (8478) CANDIES_MATH:       7 × 0 = 0 (ไม่มีถุงลูกอม)
I (8478) CANDIES_MATH:    3. การคูณด้วย 1 จะได้ตัวเลขเดิม:
I (8478) CANDIES_MATH:       8 × 1 = 8 (มีถุงเดียว)
I (8478) CANDIES_MATH: 
I (8478) CANDIES_MATH: 📚 สิ่งที่เรียนรู้:
I (8478) CANDIES_MATH:    1. การคูณเลข (Multiplication): a × b = c
I (8478) CANDIES_MATH:    2. การใช้ for loop สำหรับการทำซ้ำ
I (8478) CANDIES_MATH:    3. ความสัมพันธ์ระหว่างการคูณและการบวกซ้ำๆ
I (8478) CANDIES_MATH:    4. คุณสมบัติพิเศษของการคูณ
I (8478) CANDIES_MATH:    5. การแสดงผลแบบตาราง
I (8478) CANDIES_MATH: 
I (8478) CANDIES_MATH: 🎉 จบโปรแกรมนับลูกอมในถุง!
I (8478) CANDIES_MATH: 📖 อ่านต่อในโปรเจคถัดไป: 04_division_cookies
I (10478) main_task: Returned from app_main()
```

### 📝 แบบฝึกหัดที่ 3: สร้างตารางสูตรคูณ
เพิ่มการแสดงตารางสูตรคูณ:
```c
ESP_LOGI(TAG, "📊 ตารางสูตรคูณของ %d:", candies_per_bag);
for (int i = 1; i <= 10; i++) {
    ESP_LOGI(TAG, "   %d x %d = %d", i, candies_per_bag, i * candies_per_bag);
}
```

##resullt
```c
I (2385) CANDIES_MATH: 🍬 เริ่มต้นโปรแกรมนับลูกอมในถุง 🍬
I (2385) CANDIES_MATH: ====================================
I (2385) CANDIES_MATH: 📖 โจทย์:
I (2385) CANDIES_MATH:    มีถุงลูกอม: 7 ถุง
I (2385) CANDIES_MATH:    ถุงละ: 8 เม็ด
I (2385) CANDIES_MATH:    ❓ มีลูกอมทั้งหมดกี่เม็ด?
I (2385) CANDIES_MATH: 
I (5385) CANDIES_MATH: 🧮 ขั้นตอนการคิด:
I (5385) CANDIES_MATH:    จำนวนถุง × ลูกอมต่อถุง
I (5385) CANDIES_MATH:    = 7 × 8
I (5385) CANDIES_MATH:    = 56 เม็ด
I (5385) CANDIES_MATH: 
I (5385) CANDIES_MATH: ✅ คำตอบ:
I (5385) CANDIES_MATH:    มีลูกอมทั้งหมด 56 เม็ด
I (5385) CANDIES_MATH: 
I (5385) CANDIES_MATH: 🎨 ภาพประกอบ:
I (5385) CANDIES_MATH:    ถุงที่ 1: 🍬🍬🍬🍬🍬🍬 (8 เม็ด)
I (5385) CANDIES_MATH:    ถุงที่ 2: 🍬🍬🍬🍬🍬🍬 (8 เม็ด)
I (5385) CANDIES_MATH:    ถุงที่ 3: 🍬🍬🍬🍬🍬🍬 (8 เม็ด)
I (5385) CANDIES_MATH:    ถุงที่ 4: 🍬🍬🍬🍬🍬🍬 (8 เม็ด)
I (5385) CANDIES_MATH:    ถุงที่ 5: 🍬🍬🍬🍬🍬🍬 (8 เม็ด)
I (5395) CANDIES_MATH:    รวม:     56 เม็ด
I (5395) CANDIES_MATH: 
I (5395) CANDIES_MATH: 🔄 เปรียบเทียบกับการบวกซ้ำๆ:
I (5395) CANDIES_MATH:    การคูณ: 7 × 8 = 56
I (5395) CANDIES_MATH:    การบวกซ้ำๆ:
I (5395) CANDIES_MATH:                   8
I (5395) CANDIES_MATH:                 + 8
I (5395) CANDIES_MATH:                 + 8
I (5395) CANDIES_MATH:                 + 8
I (5395) CANDIES_MATH:                 + 8
I (5395) CANDIES_MATH:                 + 8
I (5395) CANDIES_MATH:                 + 8 = 56
I (5395) CANDIES_MATH:    ผลลัพธ์เหมือนกัน! การคูณคือการบวกซ้ำๆ
I (5395) CANDIES_MATH: 
I (5395) CANDIES_MATH: 📊 ตารางสูตรคูณ 8:
I (5395) CANDIES_MATH:    1 × 8 = 8
I (5695) CANDIES_MATH:    2 × 8 = 16
I (5995) CANDIES_MATH:    3 × 8 = 24
I (6295) CANDIES_MATH:    4 × 8 = 32
I (6595) CANDIES_MATH:    5 × 8 = 40
I (6895) CANDIES_MATH:    6 × 8 = 48
I (7195) CANDIES_MATH:    7 × 8 = 56
I (7495) CANDIES_MATH:    8 × 8 = 64
I (7795) CANDIES_MATH:    9 × 8 = 72
I (8095) CANDIES_MATH:    10 × 8 = 80
I (8395) CANDIES_MATH: 
I (8395) CANDIES_MATH: 💡 ตัวอย่างเพิ่มเติม:
I (8395) CANDIES_MATH:    ถ้ามีถุงลูกอม 3 ถุง ถุงละ 8 เม็ด
I (8395) CANDIES_MATH:    จะได้ลูกอม 3 × 8 = 24 เม็ด
I (8395) CANDIES_MATH: 
I (8395) CANDIES_MATH:    ถ้ามีถุงลูกอม 7 ถุง ถุงละ 4 เม็ด
I (8395) CANDIES_MATH:    จะได้ลูกอม 7 × 4 = 28 เม็ด
I (8395) CANDIES_MATH: 
I (8395) CANDIES_MATH: 🍭 ลูกอมหลายรส:
I (8395) CANDIES_MATH: 🍓 สตรอเบอร์รี่: 3 ถุง = 24 เม็ด
I (8395) CANDIES_MATH: 🍊 รสส้ม: 2 ถุง = 16 เม็ด
I (8395) CANDIES_MATH: 🍇 รสองุ่น: 4 ถุง = 32 เม็ด
I (8395) CANDIES_MATH: 🧮 รวมทั้งหมด: 9 ถุง × 8 เม็ด = 72 เม็ด
I (8395) CANDIES_MATH: 
I (8395) CANDIES_MATH: 📊 ตารางสูตรคูณของ 8:
I (8395) CANDIES_MATH:    1 x 8 = 8
I (8395) CANDIES_MATH:    2 x 8 = 16
I (8395) CANDIES_MATH:    3 x 8 = 24
I (8395) CANDIES_MATH:    4 x 8 = 32
I (8395) CANDIES_MATH:    5 x 8 = 40
I (8395) CANDIES_MATH:    6 x 8 = 48
I (8395) CANDIES_MATH:    7 x 8 = 56
I (8395) CANDIES_MATH:    8 x 8 = 64
I (8395) CANDIES_MATH:    9 x 8 = 72
I (8395) CANDIES_MATH:    10 x 8 = 80
I (8405) CANDIES_MATH: 🔄 เปรียบเทียบการดำเนินการ:
I (8405) CANDIES_MATH:    การบวก (+): เพิ่มจำนวน (เช่น ไข่ 4 + 2 = 6)
I (8405) CANDIES_MATH:    การลบ (-): ลดจำนวน (เช่น ของเล่น 8 - 3 = 5)
I (8405) CANDIES_MATH:    การคูณ (×): บวกซ้ำๆ (เช่น ลูกอม 5 × 6 = 30)
I (8405) CANDIES_MATH: 
I (8405) CANDIES_MATH: 🎓 แนวคิดขั้นสูง:
I (8405) CANDIES_MATH:    1. การคูณมีคุณสมบัติการสับเปลี่ยน:
I (8405) CANDIES_MATH:       7 × 8 = 8 × 7 = 56
I (8405) CANDIES_MATH:    2. การคูณด้วย 0 จะได้ 0 เสมอ:
I (8405) CANDIES_MATH:       7 × 0 = 0 (ไม่มีถุงลูกอม)
I (8405) CANDIES_MATH:    3. การคูณด้วย 1 จะได้ตัวเลขเดิม:
I (8405) CANDIES_MATH:       8 × 1 = 8 (มีถุงเดียว)
I (8405) CANDIES_MATH: 
I (8405) CANDIES_MATH: 📚 สิ่งที่เรียนรู้:
I (8405) CANDIES_MATH:    1. การคูณเลข (Multiplication): a × b = c
I (8405) CANDIES_MATH:    2. การใช้ for loop สำหรับการทำซ้ำ
I (8405) CANDIES_MATH:    3. ความสัมพันธ์ระหว่างการคูณและการบวกซ้ำๆ
I (8405) CANDIES_MATH:    4. คุณสมบัติพิเศษของการคูณ
I (8415) CANDIES_MATH:    5. การแสดงผลแบบตาราง
I (8415) CANDIES_MATH: 
I (8415) CANDIES_MATH: 🎉 จบโปรแกรมนับลูกอมในถุง!
I (8415) CANDIES_MATH: 📖 อ่านต่อในโปรเจคถัดไป: 04_division_cookies
I (10415) main_task: Returned from app_main()
```

### 📝 แบบฝึกหัดที่ 4: แจกลูกอมให้เพื่อน
คำนวณการแจกลูกอม:
```c
int friends = 12;           // จำนวนเพื่อน
int candies_per_friend = total_candies / friends;  // ลูกอมต่อคน
int remaining_candies = total_candies % friends;   // ลูกอมที่เหลือ

ESP_LOGI(TAG, "👥 แจกให้เพื่อน %d คน:", friends);
ESP_LOGI(TAG, "   คนละ %d เม็ด", candies_per_friend);
ESP_LOGI(TAG, "   เหลือ %d เม็ด", remaining_candies);
```

##result
```c
I (2435) CANDIES_MATH: 🍬 เริ่มต้นโปรแกรมนับลูกอมในถุง 🍬
I (2435) CANDIES_MATH: ====================================
I (2435) CANDIES_MATH: 📖 โจทย์:
I (2435) CANDIES_MATH:    มีถุงลูกอม: 7 ถุง
I (2435) CANDIES_MATH:    ถุงละ: 8 เม็ด
I (2435) CANDIES_MATH:    ❓ มีลูกอมทั้งหมดกี่เม็ด?
I (2435) CANDIES_MATH: 
I (5435) CANDIES_MATH: 🧮 ขั้นตอนการคิด:
I (5435) CANDIES_MATH:    จำนวนถุง × ลูกอมต่อถุง
I (5435) CANDIES_MATH:    = 7 × 8
I (5435) CANDIES_MATH:    = 56 เม็ด
I (5435) CANDIES_MATH: 
I (5435) CANDIES_MATH: ✅ คำตอบ:
I (5435) CANDIES_MATH:    มีลูกอมทั้งหมด 56 เม็ด
I (5435) CANDIES_MATH: 
I (5435) CANDIES_MATH: 🎨 ภาพประกอบ:
I (5435) CANDIES_MATH:    ถุงที่ 1: 🍬🍬🍬🍬🍬🍬 (8 เม็ด)
I (5435) CANDIES_MATH:    ถุงที่ 2: 🍬🍬🍬🍬🍬🍬 (8 เม็ด)
I (5435) CANDIES_MATH:    ถุงที่ 3: 🍬🍬🍬🍬🍬🍬 (8 เม็ด)
I (5435) CANDIES_MATH:    ถุงที่ 4: 🍬🍬🍬🍬🍬🍬 (8 เม็ด)
I (5435) CANDIES_MATH:    ถุงที่ 5: 🍬🍬🍬🍬🍬🍬 (8 เม็ด)
I (5435) CANDIES_MATH:    รวม:     56 เม็ด
I (5435) CANDIES_MATH: 
I (5435) CANDIES_MATH: 🔄 เปรียบเทียบกับการบวกซ้ำๆ:
I (5435) CANDIES_MATH:    การคูณ: 7 × 8 = 56
I (5435) CANDIES_MATH:    การบวกซ้ำๆ:
I (5435) CANDIES_MATH:                   8
I (5435) CANDIES_MATH:                 + 8
I (5435) CANDIES_MATH:                 + 8
I (5435) CANDIES_MATH:                 + 8
I (5435) CANDIES_MATH:                 + 8
I (5435) CANDIES_MATH:                 + 8
I (5435) CANDIES_MATH:                 + 8 = 56
I (5435) CANDIES_MATH:    ผลลัพธ์เหมือนกัน! การคูณคือการบวกซ้ำๆ
I (5435) CANDIES_MATH: 
I (5435) CANDIES_MATH: 📊 ตารางสูตรคูณ 8:
I (5435) CANDIES_MATH:    1 × 8 = 8
I (5735) CANDIES_MATH:    2 × 8 = 16
I (6035) CANDIES_MATH:    3 × 8 = 24
I (6335) CANDIES_MATH:    4 × 8 = 32
I (6635) CANDIES_MATH:    5 × 8 = 40
I (6935) CANDIES_MATH:    6 × 8 = 48
I (7235) CANDIES_MATH:    7 × 8 = 56
I (7535) CANDIES_MATH:    8 × 8 = 64
I (7835) CANDIES_MATH:    9 × 8 = 72
I (8135) CANDIES_MATH:    10 × 8 = 80
I (8435) CANDIES_MATH: 
I (8435) CANDIES_MATH: 💡 ตัวอย่างเพิ่มเติม:
I (8435) CANDIES_MATH:    ถ้ามีถุงลูกอม 3 ถุง ถุงละ 8 เม็ด
I (8435) CANDIES_MATH:    จะได้ลูกอม 3 × 8 = 24 เม็ด
I (8435) CANDIES_MATH: 
I (8435) CANDIES_MATH:    ถ้ามีถุงลูกอม 7 ถุง ถุงละ 4 เม็ด
I (8435) CANDIES_MATH:    จะได้ลูกอม 7 × 4 = 28 เม็ด
I (8435) CANDIES_MATH: 
I (8435) CANDIES_MATH: 🍭 ลูกอมหลายรส:
I (8435) CANDIES_MATH: 🍓 สตรอเบอร์รี่: 3 ถุง = 24 เม็ด
I (8435) CANDIES_MATH: 🍊 รสส้ม: 2 ถุง = 16 เม็ด
I (8435) CANDIES_MATH: 🍇 รสองุ่น: 4 ถุง = 32 เม็ด
I (8435) CANDIES_MATH: 🧮 รวมทั้งหมด: 9 ถุง × 8 เม็ด = 72 เม็ด
I (8435) CANDIES_MATH: 
I (8445) CANDIES_MATH: 📊 ตารางสูตรคูณของ 8:
I (8445) CANDIES_MATH:    1 x 8 = 8
I (8445) CANDIES_MATH:    2 x 8 = 16
I (8445) CANDIES_MATH:    3 x 8 = 24
I (8445) CANDIES_MATH:    4 x 8 = 32
I (8445) CANDIES_MATH:    5 x 8 = 40
I (8445) CANDIES_MATH:    6 x 8 = 48
I (8445) CANDIES_MATH:    7 x 8 = 56
I (8445) CANDIES_MATH:    8 x 8 = 64
I (8445) CANDIES_MATH:    9 x 8 = 72
I (8445) CANDIES_MATH:    10 x 8 = 80
I (8445) CANDIES_MATH: 👥 แจกให้เพื่อน 12 คน:
I (8445) CANDIES_MATH:    คนละ 4 เม็ด
I (8445) CANDIES_MATH:    เหลือ 8 เม็ด
I (8445) CANDIES_MATH: 🔄 เปรียบเทียบการดำเนินการ:
I (8445) CANDIES_MATH:    การบวก (+): เพิ่มจำนวน (เช่น ไข่ 4 + 2 = 6)
I (8445) CANDIES_MATH:    การลบ (-): ลดจำนวน (เช่น ของเล่น 8 - 3 = 5)
I (8445) CANDIES_MATH:    การคูณ (×): บวกซ้ำๆ (เช่น ลูกอม 5 × 6 = 30)
I (8445) CANDIES_MATH: 
I (8445) CANDIES_MATH: 🎓 แนวคิดขั้นสูง:
I (8445) CANDIES_MATH:    1. การคูณมีคุณสมบัติการสับเปลี่ยน:
I (8445) CANDIES_MATH:       7 × 8 = 8 × 7 = 56
I (8445) CANDIES_MATH:    2. การคูณด้วย 0 จะได้ 0 เสมอ:
I (8455) CANDIES_MATH:       7 × 0 = 0 (ไม่มีถุงลูกอม)
I (8455) CANDIES_MATH:    3. การคูณด้วย 1 จะได้ตัวเลขเดิม:
I (8455) CANDIES_MATH:       8 × 1 = 8 (มีถุงเดียว)
I (8455) CANDIES_MATH: 
I (8455) CANDIES_MATH: 📚 สิ่งที่เรียนรู้:
I (8455) CANDIES_MATH:    1. การคูณเลข (Multiplication): a × b = c
I (8455) CANDIES_MATH:    2. การใช้ for loop สำหรับการทำซ้ำ
I (8455) CANDIES_MATH:    3. ความสัมพันธ์ระหว่างการคูณและการบวกซ้ำๆ
I (8455) CANDIES_MATH:    4. คุณสมบัติพิเศษของการคูณ
I (8455) CANDIES_MATH:    5. การแสดงผลแบบตาราง
I (8455) CANDIES_MATH: 
I (8455) CANDIES_MATH: 🎉 จบโปรแกรมนับลูกอมในถุง!
I (8455) CANDIES_MATH: 📖 อ่านต่อในโปรเจคถัดไป: 04_division_cookies
I (10455) main_task: Returned from app_main()

```
