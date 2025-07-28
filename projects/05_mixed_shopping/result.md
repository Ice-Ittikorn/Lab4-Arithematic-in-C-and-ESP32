## ท้าทาย
ลองเปลี่ยนโจทย์:

เพิ่มสินค้าชอบที่คุณชอบ
เปลี่ยนส่วนลดเป็นเปอร์เซ็นต์ (10%)
เพิ่มภาษี VAT 7%

## code 
```c
#include <stdio.h>
#include <string.h>
#include "esp_log.h"
#include "freertos/FreeRTOS.h"
#include "freertos/task.h"

static const char *TAG = "SHOPPING_MATH";

typedef struct {
    char name[20];
    int quantity;
    float price_per_unit;
    float total_price;
} product_t;

void calculate_product_total(product_t *product) {
    product->total_price = product->quantity * product->price_per_unit;
}

void display_product(const product_t *product) {
    ESP_LOGI(TAG, "   %s: %d × %.0f = %.0f บาท", 
             product->name, product->quantity, product->price_per_unit, product->total_price);
}

float calculate_total_bill(product_t products[], int count) {
    float total = 0.0;
    for (int i = 0; i < count; i++) {
        calculate_product_total(&products[i]);
        total += products[i].total_price;
    }
    return total;
}

float apply_discount(float total, float discount) {
    return total - discount;
}

float calculate_vat(float amount) {
    return amount * 0.07;
}

float split_payment(float amount, int people) {
    if (people <= 0) {
        ESP_LOGE(TAG, "Error: จำนวนคนต้องมากกว่า 0");
        return 0.0;
    }
    return amount / people;
}

void app_main(void)
{
    ESP_LOGI(TAG, "🛒 เริ่มต้นโปรแกรมซื้อของที่ตลาด 🛒");
    ESP_LOGI(TAG, "=====================================");
    
    product_t products[] = {
        {"แอปเปิ้ล", 6, 15.0, 0.0},
        {"กล้วย", 12, 8.0, 0.0},
        {"ส้ม", 8, 12.0, 0.0},
        {"ทุเรียน", 5, 50.0, 0.0},
        {"มังคุด", 10, 2.0, 0.0}
    };
    int product_count = sizeof(products) / sizeof(products[0]);
    
    float discount = 10.0;
    int people = 3;
    
    ESP_LOGI(TAG, "📖 โจทย์:");
    ESP_LOGI(TAG, "   แม่ไปซื้อของที่ตลาด:");
    for (int i = 0; i < product_count; i++) {
        ESP_LOGI(TAG, "   - %s: %d หน่วย หน่วยละ %.0f บาท", 
                 products[i].name, products[i].quantity, products[i].price_per_unit);
    }
    ESP_LOGI(TAG, "   - มีส่วนลด: %.0f บาท", discount);
    ESP_LOGI(TAG, "   - แบ่งจ่าย: %d คน", people);
    ESP_LOGI(TAG, "");
    
    vTaskDelay(3000 / portTICK_PERIOD_MS);
    
    ESP_LOGI(TAG, "🧮 ขั้นตอนการคิด:");
    ESP_LOGI(TAG, "   1. คำนวณราคาแต่ละสินค้า (การคูณ):");
    float subtotal = calculate_total_bill(products, product_count);
    for (int i = 0; i < product_count; i++) {
        ESP_LOGI(TAG, "      %s: %d × %.0f = %.0f บาท", 
                 products[i].name, products[i].quantity, 
                 products[i].price_per_unit, products[i].total_price);
    }
    ESP_LOGI(TAG, "");

    ESP_LOGI(TAG, "   2. รวมราคาทั้งหมด (การบวก): %.0f บาท", subtotal);
    ESP_LOGI(TAG, "");

    float vat = calculate_vat(subtotal);
    float total_with_vat = subtotal + vat;
    ESP_LOGI(TAG, "   3. เพิ่มภาษีมูลค่าเพิ่ม (7%%): %.0f × 0.07 = %.2f บาท", subtotal, vat);
    ESP_LOGI(TAG, "      รวมหลังภาษี: %.0f + %.2f = %.2f บาท", subtotal, vat, total_with_vat);
    ESP_LOGI(TAG, "");

    float discounted_total = apply_discount(total_with_vat, discount);
    ESP_LOGI(TAG, "   4. หักส่วนลด (การลบ): %.2f - %.0f = %.2f บาท", total_with_vat, discount, discounted_total);
    ESP_LOGI(TAG, "");

    float per_person = split_payment(discounted_total, people);
    ESP_LOGI(TAG, "   5. แบ่งจ่าย (การหาร): %.2f ÷ %d = %.2f บาท/คน", discounted_total, people, per_person);
    ESP_LOGI(TAG, "");
    
    ESP_LOGI(TAG, "🧾 ใบเสร็จรับเงิน:");
    ESP_LOGI(TAG, "   ==========================================");
    ESP_LOGI(TAG, "   🏪 ตลาดสดใหม่ 🏪");
    ESP_LOGI(TAG, "   ==========================================");
    for (int i = 0; i < product_count; i++) {
        display_product(&products[i]);
    }
    ESP_LOGI(TAG, "   ----------------------------------------");
    ESP_LOGI(TAG, "   ยอดรวม:                    %.0f บาท", subtotal);
    ESP_LOGI(TAG, "   ภาษี 7%%:                   +%.2f บาท", vat);
    ESP_LOGI(TAG, "   รวมหลังภาษี:               %.2f บาท", total_with_vat);
    ESP_LOGI(TAG, "   ส่วนลด:                     -%.0f บาท", discount);
    ESP_LOGI(TAG, "   ========================================");
    ESP_LOGI(TAG, "   ยอดสุทธิ:                   %.2f บาท", discounted_total);
    ESP_LOGI(TAG, "   แบ่งจ่าย %d คน:              %.2f บาท/คน", people, per_person);
    ESP_LOGI(TAG, "   ========================================");
    ESP_LOGI(TAG, "   ขอบคุณที่ใช้บริการ 😊");
    ESP_LOGI(TAG, "");

    // ตัวอย่างเพิ่มเติม
    ESP_LOGI(TAG, "💡 ตัวอย่างเพิ่มเติม:");

    // เพิ่มมะม่วง
    ESP_LOGI(TAG, "   📝 ถ้าเพิ่มมะม่วง 4 ผล ผลละ 25 บาท:");
    float mango_total = 4 * 25;
    float new_subtotal = subtotal + mango_total;
    float new_vat = calculate_vat(new_subtotal);
    float new_total_with_vat = new_subtotal + new_vat;
    float new_discounted = apply_discount(new_total_with_vat, discount);
    float new_per_person = split_payment(new_discounted, people);
    ESP_LOGI(TAG, "      มะม่วง: 4 × 25 = %.0f บาท", mango_total);
    ESP_LOGI(TAG, "      ยอดรวมใหม่: %.0f บาท", new_subtotal);
    ESP_LOGI(TAG, "      ภาษี: %.2f บาท", new_vat);
    ESP_LOGI(TAG, "      รวมหลังภาษี: %.2f บาท", new_total_with_vat);
    ESP_LOGI(TAG, "      หักส่วนลด: %.2f บาท", new_discounted);
    ESP_LOGI(TAG, "      แบ่งจ่าย: %.2f ÷ %d = %.2f บาท/คน", new_discounted, people, new_per_person);
    ESP_LOGI(TAG, "");

    // ส่วนลดแบบเปอร์เซ็นต์
    ESP_LOGI(TAG, "   🏷️ ถ้าใช้ส่วนลด 10%% แทน:");
    float percent_discount = total_with_vat * 0.10;
    float percent_discounted = apply_discount(total_with_vat, percent_discount);
    float percent_per_person = split_payment(percent_discounted, people);
    ESP_LOGI(TAG, "      ส่วนลด 10%%: %.2f บาท", percent_discount);
    ESP_LOGI(TAG, "      ยอดสุทธิ: %.2f บาท", percent_discounted);
    ESP_LOGI(TAG, "      แบ่งจ่าย: %.2f ÷ %d = %.2f บาท/คน", percent_discounted, people, percent_per_person);
    ESP_LOGI(TAG, "");

    ESP_LOGI(TAG, "🌟 การประยุกต์ใช้ในชีวิตจริง:");
    ESP_LOGI(TAG, "   1. การซื้อของเป็นกลุ่ม - ต้องคำนวณค่าใช้จ่าย");
    ESP_LOGI(TAG, "   2. การแบ่งบิลในร้านอาหาร");
    ESP_LOGI(TAG, "   3. การคำนวณค่าใช้จ่ายท่องเที่ยว");
    ESP_LOGI(TAG, "   4. การวางแผนงบประมาณ");
    ESP_LOGI(TAG, "   5. การคิดราคาขายสินค้า");
    ESP_LOGI(TAG, "");

    ESP_LOGI(TAG, "🔍 วิเคราะห์การดำเนินการที่ใช้:");
    ESP_LOGI(TAG, "   ✓ การคูณ (×): คำนวณราคาสินค้าแต่ละชนิด");
    ESP_LOGI(TAG, "   ✓ การบวก (+): รวมราคาทั้งหมด");
    ESP_LOGI(TAG, "   ✓ การคูณ VAT (+): คิดภาษี");
    ESP_LOGI(TAG, "   ✓ การลบ (-): หักส่วนลด");
    ESP_LOGI(TAG, "   ✓ การหาร (÷): แบ่งจ่ายค่าใช้จ่าย");
    ESP_LOGI(TAG, "   ➜ การรวมการดำเนินการทำให้แก้โจทย์ซับซ้อนได้!");
    ESP_LOGI(TAG, "");

    ESP_LOGI(TAG, "📚 สิ่งที่เรียนรู้:");
    ESP_LOGI(TAG, "   1. การใช้ struct เก็บข้อมูลที่เกี่ยวข้องกัน");
    ESP_LOGI(TAG, "   2. การแบ่งปัญหาใหญ่เป็นปัญหาย่อยๆ");
    ESP_LOGI(TAG, "   3. การรวมการดำเนินการทางคณิตศาสตร์");
    ESP_LOGI(TAG, "   4. การสร้างฟังก์ชันเฉพาะงาน");
    ESP_LOGI(TAG, "   5. การแสดงผลในรูปแบบที่เข้าใจง่าย");
    ESP_LOGI(TAG, "   6. การประยุกต์ใช้ในชีวิตจริง");
    ESP_LOGI(TAG, "");

    ESP_LOGI(TAG, "🎉 จบโปรแกรมซื้อของที่ตลาด!");
    ESP_LOGI(TAG, "📖 อ่านต่อในโปรเจคถัดไป: 06_advanced_math");
    
    vTaskDelay(2000 / portTICK_PERIOD_MS);
}
```

## Result
```c
I (2453) SHOPPING_MATH: 🛒 เริ่มต้นโปรแกรมซื้อของที่ตลาด 🛒
I (2453) SHOPPING_MATH: =====================================
I (2453) SHOPPING_MATH: 📖 โจทย์:
I (2453) SHOPPING_MATH:    แม่ไปซื้อของที่ตลาด:
I (2453) SHOPPING_MATH:    - แอปเปิ�: 6 หน่วย หน่วยละ 15 บาท
I (2463) SHOPPING_MATH:    - กล้วย: 12 หน่วย หน่วยละ 8 บาท
I (2463) SHOPPING_MATH:    - ส้ม: 8 หน่วย หน่วยละ 12 บาท
I (2463) SHOPPING_MATH:    - ทุเรีย�: 5 หน่วย หน่วยละ 50 บาท
I (2463) SHOPPING_MATH:    - มังคุด: 10 หน่วย หน่วยละ 2 บาท
I (2463) SHOPPING_MATH:    - มีส่วนลด: 10 บาท
I (2463) SHOPPING_MATH:    - แบ่งจ่าย: 3 คน
I (2463) SHOPPING_MATH: 
I (5463) SHOPPING_MATH: 🧮 ขั้นตอนการคิด:
I (5463) SHOPPING_MATH:    1. คำนวณราคาแต่ละสินค้า (การคูณ):
I (5463) SHOPPING_MATH:       แอปเปิ�: 6 × 15 = 90 บาท
I (5483) SHOPPING_MATH:       กล้วย: 12 × 8 = 96 บาท
I (5483) SHOPPING_MATH:       ส้ม: 8 × 12 = 96 บาท
I (5483) SHOPPING_MATH:       ทุเรีย�: 5 × 50 = 250 บาท
I (5483) SHOPPING_MATH:       มังคุด: 10 × 2 = 20 บาท
I (5483) SHOPPING_MATH: 
I (5493) SHOPPING_MATH:    2. รวมราคาทั้งหมด (การบวก): 552 บาท
I (5493) SHOPPING_MATH: 
I (5493) SHOPPING_MATH:    3. เพิ่มภาษีมูลค่าเพิ่ม (7%): 552 × 0.07 = 38.64 บาท
I (5493) SHOPPING_MATH:       รวมหลังภาษี: 552 + 38.64 = 590.64 บาท
I (5493) SHOPPING_MATH: 
I (5493) SHOPPING_MATH:    4. หักส่วนลด (การลบ): 590.64 - 10 = 580.64 บาท
I (5493) SHOPPING_MATH: 
I (5493) SHOPPING_MATH:    5. แบ่งจ่าย (การหาร): 580.64 ÷ 3 = 193.55 บาท/คน
I (5493) SHOPPING_MATH: 
I (5493) SHOPPING_MATH: 🧾 ใบเสร็จรับเงิน:
I (5493) SHOPPING_MATH:    ==========================================
I (5493) SHOPPING_MATH:    🏪 ตลาดสดใหม่ 🏪
I (5493) SHOPPING_MATH:    ==========================================
I (5493) SHOPPING_MATH:    แอปเปิ�: 6 × 15 = 90 บาท
I (5493) SHOPPING_MATH:    กล้วย: 12 × 8 = 96 บาท
I (5493) SHOPPING_MATH:    ส้ม: 8 × 12 = 96 บาท
I (5493) SHOPPING_MATH:    ทุเรีย�: 5 × 50 = 250 บาท
I (5493) SHOPPING_MATH:    มังคุด: 10 × 2 = 20 บาท
I (5493) SHOPPING_MATH:    ----------------------------------------
I (5493) SHOPPING_MATH:    ยอดรวม:                    552 บาท
I (5493) SHOPPING_MATH:    ภาษี 7%:                   +38.64 บาท
I (5493) SHOPPING_MATH:    รวมหลังภาษี:               590.64 บาท
I (5493) SHOPPING_MATH:    ส่วนลด:                     -10 บาท
I (5493) SHOPPING_MATH:    ========================================
I (5493) SHOPPING_MATH:    ยอดสุทธิ:                   580.64 บาท
I (5503) SHOPPING_MATH:    แบ่งจ่าย 3 คน:              193.55 บาท/คน
I (5503) SHOPPING_MATH:    ========================================
I (5503) SHOPPING_MATH:    ขอบคุณที่ใช้บริการ 😊
I (5503) SHOPPING_MATH: 
I (5503) SHOPPING_MATH: 💡 ตัวอย่างเพิ่มเติม:
I (5503) SHOPPING_MATH:    📝 ถ้าเพิ่มมะม่วง 4 ผล ผลละ 25 บาท:
I (5503) SHOPPING_MATH:       มะม่วง: 4 × 25 = 100 บาท
I (5503) SHOPPING_MATH:       ยอดรวมใหม่: 652 บาท
I (5503) SHOPPING_MATH:       ภาษี: 45.64 บาท
I (5503) SHOPPING_MATH:       รวมหลังภาษี: 697.64 บาท
I (5503) SHOPPING_MATH:       หักส่วนลด: 687.64 บาท
I (5503) SHOPPING_MATH:       แบ่งจ่าย: 687.64 ÷ 3 = 229.21 บาท/คน
I (5503) SHOPPING_MATH: 
I (5503) SHOPPING_MATH:    🏷️ ถ้าใช้ส่วนลด 10% แทน:
I (5503) SHOPPING_MATH:       ส่วนลด 10%: 59.06 บาท
I (5503) SHOPPING_MATH:       ยอดสุทธิ: 531.58 บาท
I (5503) SHOPPING_MATH:       แบ่งจ่าย: 531.58 ÷ 3 = 177.19 บาท/คน
I (5503) SHOPPING_MATH: 
I (5503) SHOPPING_MATH: 🌟 การประยุกต์ใช้ในชีวิตจริง:
I (5503) SHOPPING_MATH:    1. การซื้อของเป็นกลุ่ม - ต้องคำนวณค่าใช้จ่าย
I (5503) SHOPPING_MATH:    2. การแบ่งบิลในร้านอาหาร
I (5503) SHOPPING_MATH:    3. การคำนวณค่าใช้จ่ายท่องเที่ยว
I (5503) SHOPPING_MATH:    4. การวางแผนงบประมาณ
I (5503) SHOPPING_MATH:    5. การคิดราคาขายสินค้า
I (5503) SHOPPING_MATH: 
I (5503) SHOPPING_MATH: 🔍 วิเคราะห์การดำเนินการที่ใช้:
I (5503) SHOPPING_MATH:    ✓ การคูณ (×): คำนวณราคาสินค้าแต่ละชนิด
I (5503) SHOPPING_MATH:    ✓ การบวก (+): รวมราคาทั้งหมด
I (5503) SHOPPING_MATH:    ✓ การคูณ VAT (+): คิดภาษี
I (5503) SHOPPING_MATH:    ✓ การลบ (-): หักส่วนลด
I (5503) SHOPPING_MATH:    ✓ การหาร (÷): แบ่งจ่ายค่าใช้จ่าย
I (5503) SHOPPING_MATH:    ➜ การรวมการดำเนินการทำให้แก้โจทย์ซับซ้อนได้!
I (5513) SHOPPING_MATH: 
I (5513) SHOPPING_MATH: 📚 สิ่งที่เรียนรู้:
I (5513) SHOPPING_MATH:    1. การใช้ struct เก็บข้อมูลที่เกี่ยวข้องกัน
I (5513) SHOPPING_MATH:    2. การแบ่งปัญหาใหญ่เป็นปัญหาย่อยๆ
I (5513) SHOPPING_MATH:    3. การรวมการดำเนินการทางคณิตศาสตร์
I (5513) SHOPPING_MATH:    4. การสร้างฟังก์ชันเฉพาะงาน
I (5513) SHOPPING_MATH:    5. การแสดงผลในรูปแบบที่เข้าใจง่าย
I (5513) SHOPPING_MATH:    6. การประยุกต์ใช้ในชีวิตจริง
I (5513) SHOPPING_MATH: 
I (5513) SHOPPING_MATH: 🎉 จบโปรแกรมซื้อของที่ตลาด!
I (5513) SHOPPING_MATH: 📖 อ่านต่อในโปรเจคถัดไป: 06_advanced_math
I (7513) main_task: Returned from app_main()

```
