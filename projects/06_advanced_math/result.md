## 🎓 ท้าทาย

ลองเพิ่ม:
1. คำนวณพื้นที่สามเหลี่ยม
2. คำนวณปริมาตรทรงกรวย
3. แปลงหน่วย (เมตร → ตารางเมตร → ไร่)

## ✅ ผลลัพธ์ที่คาดหวัง

```
=== สนามฟุตบอล ===
พื้นที่: 100 × 60 = 6,000 ตร.ม.
ปริเมตร: 2×(100+60) = 320 ม.

=== สระน้ำกลม ===
พื้นที่ผิวน้ำ: π × 5² = 78.54 ตร.ม.
ปริมาตรน้ำ: π × 5² × 2 = 157.08 ลบ.ม.
```

## Code
```c
#include <stdio.h>
#include <math.h>
#include "esp_log.h"
#include "freertos/FreeRTOS.h"
#include "freertos/task.h"

// 🏷️ Tag สำหรับ Log
static const char *TAG = "ADVANCED_MATH";

// 🔢 ค่าคงที่ทางคณิตศาสตร์
#define PI 3.14159265359
#define SQUARE_METERS_TO_RAI 1600.0  // 1 ไร่ = 1,600 ตร.ม.

// 📐 โครงสร้างข้อมูลรูปทรง
typedef struct {
    char name[50];
    double length;      // ความยาว/รัศมี
    double width;       // ความกว้าง
    double height;      // ความสูง/ความลึก
} shape_t;

// 🏟️ ฟังก์ชันคำนวณสี่เหลี่ยม
void calculate_rectangle(shape_t shape) {
    double area = shape.length * shape.width;
    double perimeter = 2 * (shape.length + shape.width);
    double area_in_rai = area / SQUARE_METERS_TO_RAI;
    
    ESP_LOGI(TAG, "╔══════════════════════════════════════╗");
    ESP_LOGI(TAG, "║          %s                          ║", shape.name);
    ESP_LOGI(TAG, "╠══════════════════════════════════════╣");
    ESP_LOGI(TAG, "║ 📏 ความยาว: %.2f เมตร", shape.length);
    ESP_LOGI(TAG, "║ 📏 ความกว้าง: %.2f เมตร", shape.width);
    ESP_LOGI(TAG, "║ 📐 พื้นที่: %.2f × %.2f = %.2f ตร.ม.", 
             shape.length, shape.width, area);
    ESP_LOGI(TAG, "║ 🔄 ปริเมตร: 2×(%.0f+%.0f) = %.2f ม.", 
             shape.length, shape.width, perimeter);
    ESP_LOGI(TAG, "║ 🌾 เท่ากับ: %.4f ไร่", area_in_rai);
    ESP_LOGI(TAG, "╚══════════════════════════════════════╝");
}

// 🏊‍♀️ ฟังก์ชันคำนวณวงกลม
void calculate_circle(shape_t shape) {
    double radius = shape.length;  // ใช้ length เป็น radius
    double surface_area = PI * radius * radius;
    double circumference = 2 * PI * radius;
    double volume = surface_area * shape.height;  // ปริมาตรทรงกระบอก
    
    ESP_LOGI(TAG, "╔══════════════════════════════════════╗");
    ESP_LOGI(TAG, "║          %s                          ║", shape.name);
    ESP_LOGI(TAG, "╠══════════════════════════════════════╣");
    ESP_LOGI(TAG, "║ 📏 รัศมี: %.2f เมตร", radius);
    ESP_LOGI(TAG, "║ 📏 ความลึก: %.2f เมตร", shape.height);
    ESP_LOGI(TAG, "║ 🌊 พื้นที่ผิวน้ำ: π × %.0f² = %.2f ตร.ม.", 
             radius, surface_area);
    ESP_LOGI(TAG, "║ ⭕ เส้นรอบวง: 2π × %.0f = %.2f ม.", 
             radius, circumference);
    ESP_LOGI(TAG, "║ 💧 ปริมาตรน้ำ: %.2f × %.2f = %.2f ลบ.ม.", 
             surface_area, shape.height, volume);
    ESP_LOGI(TAG, "╚══════════════════════════════════════╝");
}

// 🎁 ฟังก์ชันคำนวณทรงผีเสื้อ
void calculate_box(shape_t shape) {
    double volume = shape.length * shape.width * shape.height;
    double surface_area = 2 * (shape.length * shape.width + 
                               shape.width * shape.height + 
                               shape.length * shape.height);
    
    ESP_LOGI(TAG, "╔══════════════════════════════════════╗");
    ESP_LOGI(TAG, "║          %s                          ║", shape.name);
    ESP_LOGI(TAG, "╠══════════════════════════════════════╣");
    ESP_LOGI(TAG, "║ 📏 ความยาว: %.2f ซม.", shape.length);
    ESP_LOGI(TAG, "║ 📏 ความกว้าง: %.2f ซม.", shape.width);
    ESP_LOGI(TAG, "║ 📏 ความสูง: %.2f ซม.", shape.height);
    ESP_LOGI(TAG, "║ 📦 ปริมาตร: %.0f×%.0f×%.0f = %.2f ลบ.ซม.", 
             shape.length, shape.width, shape.height, volume);
    ESP_LOGI(TAG, "║ 🎀 พื้นที่ผิว: %.2f ตร.ซม.", surface_area);
    ESP_LOGI(TAG, "║ 📐 เท่ากับ: %.6f ลิตร", volume / 1000.0);
    ESP_LOGI(TAG, "╚══════════════════════════════════════╝");
}

// 📊 ฟังก์ชันเปรียบเทียบผลลัพธ์
void compare_results(void) {
    ESP_LOGI(TAG, "\n🔍 การเปรียบเทียบผลลัพธ์:");
    ESP_LOGI(TAG, "╔════════════════════════════════════╗");
    ESP_LOGI(TAG, "║  สนามฟุตบอล vs สระน้ำ vs กล่อง        ║");
    ESP_LOGI(TAG, "╠════════════════════════════════════╣");
    ESP_LOGI(TAG, "║ 🏟️ สนาม: ใหญ่ที่สุด (6,000 ตร.ม.)       ║");
    ESP_LOGI(TAG, "║ 🏊‍♀️ สระ: กลาง (78.54 ตร.ม.)          ║");
    ESP_LOGI(TAG, "║ 🎁 กล่อง: เล็กที่สุด (300 ลบ.ซม.)        ║");
    ESP_LOGI(TAG, "╚════════════════════════════════════╝");
}

// 🎓 ฟังก์ชันแสดงความรู้เพิ่มเติม
void show_math_facts(void) {
    ESP_LOGI(TAG, "\n📚 ความรู้ทางคณิตศาสตร์:");
    ESP_LOGI(TAG, "╔═══════════════════════════════════════╗");
    ESP_LOGI(TAG, "║             สูตรคณิตศาสตร์               ║");
    ESP_LOGI(TAG, "╠═══════════════════════════════════════╣");
    ESP_LOGI(TAG, "║ 📐 สี่เหลี่ยม: พื้นที่ = ยาว × กว้าง            ║");
    ESP_LOGI(TAG, "║ ⭕ วงกลม: พื้นที่ = π × r²                 ║");
    ESP_LOGI(TAG, "║ 📦 ทรงผีเสื้อ: ปริมาตร = ย×ก×ส             ║");
    ESP_LOGI(TAG, "║ 💡 π (pi) ≈ 3.14159                    ║");
    ESP_LOGI(TAG, "║ 🌾 1 ไร่ = 1,600 ตารางเมตร              ║");
    ESP_LOGI(TAG, "╚═══════════════════════════════════════╝");
}

// 🎯 ฟังก์ชันท้าทาย - คำนวณสามเหลี่ยม
void calculate_triangle_bonus(void) {
    double base = 10.0;     // ฐาน
    double height = 8.0;    // สูง
    double side1 = 10.0;    // ด้านที่ 1
    double side2 = 8.0;     // ด้านที่ 2
    double side3 = 6.0;     // ด้านที่ 3
    
    double area = 0.5 * base * height;
    double perimeter = side1 + side2 + side3;
    
    ESP_LOGI(TAG, "\n🎯 โบนัส: สามเหลี่ยม");
    ESP_LOGI(TAG, "╔═══════════════════════════════════════╗");
    ESP_LOGI(TAG, "║             สามเหลี่ยมมุมฉาก             ║");
    ESP_LOGI(TAG, "╠═══════════════════════════════════════╣");
    ESP_LOGI(TAG, "║ 📏 ฐาน: %.2f ซม.", base);
    ESP_LOGI(TAG, "║ 📏 สูง: %.2f ซม.", height);
    ESP_LOGI(TAG, "║ 📐 พื้นที่: ½×%.0f×%.0f = %.2f ตร.ซม.", 
             base, height, area);
    ESP_LOGI(TAG, "║ 🔄 ปริเมตร: %.0f+%.0f+%.0f = %.2f ซม.", 
             side1, side2, side3, perimeter);
    ESP_LOGI(TAG, "╚═══════════════════════════════════════╝");
}

void calculate_cone(void) {
    double r = 10.0;     // ฐาน
    double height = 8.0;    // สูง
    
    double area = 3.14 * r * (r + height);
    double perimeter = 1 / 3 * 3.14 * r * r * height ;
    
    ESP_LOGI(TAG, "\n🎯 ทรงกรวย");
    ESP_LOGI(TAG, "╔═══════════════════════════════════════╗");
    ESP_LOGI(TAG, "║                ทรงกรวย                ║");
    ESP_LOGI(TAG, "╠═══════════════════════════════════════╣");
    ESP_LOGI(TAG, "║ 📏 รัสมี: %.2f ซม.", r);
    ESP_LOGI(TAG, "║ 📏 สูง: %.2f ซม.", height);
    ESP_LOGI(TAG, "║ 📐 พื้นที่: 3.14 ×%.0f×%.0f×(%.0f+%.0f)= %.2f ตร.ซม.", 
             r, r, height,area);
    ESP_LOGI(TAG, "║ 🔄 ปริเมตร: 1/3x3.14+%.0f+%.0f+%.0f= %.2f ซม.", 
             r,r, height, perimeter);
    ESP_LOGI(TAG, "╚═══════════════════════════════════════╝");
}

void calculate_pang(void) {
    double m = 3200.0;     // ฐา
    
    double mtol = m / 1600;
    
    ESP_LOGI(TAG, "\n🎯 แปลงหน่อย");
    ESP_LOGI(TAG, "╔═══════════════════════════════════════╗");
    ESP_LOGI(TAG, "║                แปลงหน่อย                ║");
    ESP_LOGI(TAG, "╠═══════════════════════════════════════╣");
    ESP_LOGI(TAG, "║ 📏 แปลงเมตรเป็นตารางเมตรไม่ได้:");
    ESP_LOGI(TAG, "║ 📏 แปลงตารางเมตรเป็นไร่ : %.0f / 1600 = %.2f ไร่", m,mtol);
    ESP_LOGI(TAG, "╚═══════════════════════════════════════╝");
}

void app_main(void) {
    ESP_LOGI(TAG, "🚀 เริ่มต้นโปรแกรมคณิตศาสตร์ขั้นสูง!");
    ESP_LOGI(TAG, "📐 การคำนวณพื้นที่และปริมาตร\n");
    
    // รอสักครู่เพื่อให้ระบบเริ่มต้นเสร็จสิ้น
    vTaskDelay(pdMS_TO_TICKS(1000));
    
    // 🏟️ สนามฟุตบอล
    shape_t football_field = {
        .name = "สนามฟุตบอล",
        .length = 100.0,
        .width = 60.0,
        .height = 0.0
    };
    
    // 🏊‍♀️ สระน้ำกลม
    shape_t swimming_pool = {
        .name = "สระน้ำกลม",
        .length = 5.0,    // รัศมี
        .width = 0.0,
        .height = 2.0     // ความลึก
    };
    
    // 🎁 กล่องของขวัญ
    shape_t gift_box = {
        .name = "กล่องของขวัญ",
        .length = 20.0,
        .width = 15.0,
        .height = 10.0
    };
    
    // 🎨 ASCII Art
    ESP_LOGI(TAG, "   🏟️     🏊‍♀️     🎁");
    ESP_LOGI(TAG, " ┌─────┐  ╭─────╮  ┌─────┐");
    ESP_LOGI(TAG, " │ ⚽  │  │ 💧💧 │  │ 🎀  │");
    ESP_LOGI(TAG, " │     │  │     │  │     │");
    ESP_LOGI(TAG, " └─────┘  ╰─────╯  └─────┘\n");
    
    // คำนวณแต่ละรูปทรง
    calculate_rectangle(football_field);
    vTaskDelay(pdMS_TO_TICKS(2000));
    
    calculate_circle(swimming_pool);
    vTaskDelay(pdMS_TO_TICKS(2000));
    
    calculate_box(gift_box);
    vTaskDelay(pdMS_TO_TICKS(2000));
    
    // เปรียบเทียบผลลัพธ์
    compare_results();
    vTaskDelay(pdMS_TO_TICKS(2000));
    
    // แสดงความรู้เพิ่มเติม
    show_math_facts();
    vTaskDelay(pdMS_TO_TICKS(2000));
    
    // โบนัสท้าทาย
    calculate_triangle_bonus();

    calculate_cone();

    calculate_pang();
    
    ESP_LOGI(TAG, "\n✅ เสร็จสิ้นการคำนวณทั้งหมด!");
    ESP_LOGI(TAG, "🎓 ได้เรียนรู้: คณิตศาสตร์ขั้นสูง, struct, #define, และฟังก์ชันคณิตศาสตร์");
}
```
## result
```c
I (2401) ADVANCED_MATH: 🚀 เริ่มต้นโปรแกรมคณิตศาสตร์ขั้นสูง!
I (2401) ADVANCED_MATH: 📐 การคำนวณพื้นที่และปริมาตร

I (3401) ADVANCED_MATH:    🏟️     🏊‍♀️     🎁
I (3401) ADVANCED_MATH:  ┌─────┐  ╭─────╮  ┌─────┐
I (3401) ADVANCED_MATH:  │ ⚽  │  │ 💧💧 │  │ 🎀  │
I (3401) ADVANCED_MATH:  │     │  │     │  │     │
I (3401) ADVANCED_MATH:  └─────┘  ╰─────╯  └─────┘

I (3401) ADVANCED_MATH: ╔══════════════════════════════════════╗
I (3401) ADVANCED_MATH: ║          สนามฟุตบอล                          ║
I (3401) ADVANCED_MATH: ╠══════════════════════════════════════╣
I (3401) ADVANCED_MATH: ║ 📏 ความยาว: 100.00 เมตร
I (3411) ADVANCED_MATH: ║ 📏 ความกว้าง: 60.00 เมตร
I (3411) ADVANCED_MATH: ║ 📐 พื้นที่: 100.00 × 60.00 = 6000.00 ตร.ม.
I (3411) ADVANCED_MATH: ║ 🔄 ปริเมตร: 2×(100+60) = 320.00 ม.
I (3411) ADVANCED_MATH: ║ 🌾 เท่ากับ: 3.7500 ไร่
I (3411) ADVANCED_MATH: ╚══════════════════════════════════════╝
I (5421) ADVANCED_MATH: ╔══════════════════════════════════════╗
I (5421) ADVANCED_MATH: ║          สระน้ำกลม                          ║
I (5421) ADVANCED_MATH: ╠══════════════════════════════════════╣
I (5421) ADVANCED_MATH: ║ 📏 รัศมี: 5.00 เมตร
I (5421) ADVANCED_MATH: ║ 📏 ความลึก: 2.00 เมตร
I (5421) ADVANCED_MATH: ║ 🌊 พื้นที่ผิวน้ำ: π × 5² = 78.54 ตร.ม.
I (5421) ADVANCED_MATH: ║ ⭕ เส้นรอบวง: 2π × 5 = 31.42 ม.
I (5421) ADVANCED_MATH: ║ 💧 ปริมาตรน้ำ: 78.54 × 2.00 = 157.08 ลบ.ม.
I (5431) ADVANCED_MATH: ╚══════════════════════════════════════╝
I (7431) ADVANCED_MATH: ╔══════════════════════════════════════╗
I (7431) ADVANCED_MATH: ║          กล่องของขวัญ                          ║
I (7431) ADVANCED_MATH: ╠══════════════════════════════════════╣
I (7431) ADVANCED_MATH: ║ 📏 ความยาว: 20.00 ซม.
I (7431) ADVANCED_MATH: ║ 📏 ความกว้าง: 15.00 ซม.
I (7431) ADVANCED_MATH: ║ 📏 ความสูง: 10.00 ซม.
I (7431) ADVANCED_MATH: ║ 📦 ปริมาตร: 20×15×10 = 3000.00 ลบ.ซม.
I (7431) ADVANCED_MATH: ║ 🎀 พื้นที่ผิว: 1300.00 ตร.ซม.
I (7431) ADVANCED_MATH: ║ 📐 เท่ากับ: 3.000000 ลิตร
I (7431) ADVANCED_MATH: ╚══════════════════════════════════════╝
I (9441) ADVANCED_MATH: 
🔍 การเปรียบเทียบผลลัพธ์:
I (9441) ADVANCED_MATH: ╔════════════════════════════════════╗
I (9441) ADVANCED_MATH: ║  สนามฟุตบอล vs สระน้ำ vs กล่อง        ║
I (9441) ADVANCED_MATH: ╠════════════════════════════════════╣
I (9441) ADVANCED_MATH: ║ 🏟️ สนาม: ใหญ่ที่สุด (6,000 ตร.ม.)       ║
I (9441) ADVANCED_MATH: ║ 🏊‍♀️ สระ: กลาง (78.54 ตร.ม.)          ║
I (9441) ADVANCED_MATH: ║ 🎁 กล่อง: เล็กที่สุด (300 ลบ.ซม.)        ║
I (9441) ADVANCED_MATH: ╚════════════════════════════════════╝
I (11441) ADVANCED_MATH: 
📚 ความรู้ทางคณิตศาสตร์:
I (11441) ADVANCED_MATH: ╔═══════════════════════════════════════╗
I (11441) ADVANCED_MATH: ║             สูตรคณิตศาสตร์               ║
I (11441) ADVANCED_MATH: ╠═══════════════════════════════════════╣
I (11441) ADVANCED_MATH: ║ 📐 สี่เหลี่ยม: พื้นที่ = ยาว × กว้าง            ║
I (11441) ADVANCED_MATH: ║ ⭕ วงกลม: พื้นที่ = π × r²                 ║
I (11441) ADVANCED_MATH: ║ 📦 ทรงผีเสื้อ: ปริมาตร = ย×ก×ส             ║
I (11441) ADVANCED_MATH: ║ 💡 π (pi) ≈ 3.14159                    ║
I (11441) ADVANCED_MATH: ║ 🌾 1 ไร่ = 1,600 ตารางเมตร              ║
I (11441) ADVANCED_MATH: ╚═══════════════════════════════════════╝
I (13441) ADVANCED_MATH: 
🎯 โบนัส: สามเหลี่ยม
I (13441) ADVANCED_MATH: ╔═══════════════════════════════════════╗
I (13441) ADVANCED_MATH: ║             สามเหลี่ยมมุมฉาก             ║
I (13441) ADVANCED_MATH: ╠═══════════════════════════════════════╣
I (13441) ADVANCED_MATH: ║ 📏 ฐาน: 10.00 ซม.
I (13441) ADVANCED_MATH: ║ 📏 สูง: 8.00 ซม.
I (13441) ADVANCED_MATH: ║ 📐 พื้นที่: ½×10×8 = 40.00 ตร.ซม.
I (13441) ADVANCED_MATH: ║ 🔄 ปริเมตร: 10+8+6 = 24.00 ซม.
I (13441) ADVANCED_MATH: ╚═══════════════════════════════════════╝
I (13441) ADVANCED_MATH: 
🎯 ทรงกรวย
I (13441) ADVANCED_MATH: ╔═══════════════════════════════════════╗
I (13451) ADVANCED_MATH: ║                ทรงกรวย                ║
I (13451) ADVANCED_MATH: ╠═══════════════════════════════════════╣
I (13451) ADVANCED_MATH: ║ 📏 รัสมี: 10.00 ซม.
I (13451) ADVANCED_MATH: ║ 📏 สูง: 8.00 ซม.
I (13451) ADVANCED_MATH: ║ 📐 พื้นที่: 3.14 ×10×10×(8+565)= 8.00 ตร.ซม.
I (13451) ADVANCED_MATH: ║ 🔄 ปริเมตร: 1/3x3.14+10+10+8= 0.00 ซม.
I (13451) ADVANCED_MATH: ╚═══════════════════════════════════════╝
I (13451) ADVANCED_MATH: 
🎯 แปลงหน่อย
I (13451) ADVANCED_MATH: ╔═══════════════════════════════════════╗
I (13451) ADVANCED_MATH: ║                แปลงหน่อย                ║
I (13451) ADVANCED_MATH: ╠═══════════════════════════════════════╣
I (13451) ADVANCED_MATH: ║ 📏 แปลงเมตรเป็นตารางเมตรไม่ได้:
I (13451) ADVANCED_MATH: ║ 📏 แปลงตารางเมตรเป็นไร่ : 3200 / 1600 = 2.00 ไร่
I (13451) ADVANCED_MATH: ╚═══════════════════════════════════════╝
I (13461) ADVANCED_MATH: 
✅ เสร็จสิ้นการคำนวณทั้งหมด!
I (13461) ADVANCED_MATH: 🎓 ได้เรียนรู้: คณิตศาสตร์ขั้นสูง, struct, #define, และฟังก์ชันคณิตศาสตร์
I (13461) main_task: Returned from app_main()
```
