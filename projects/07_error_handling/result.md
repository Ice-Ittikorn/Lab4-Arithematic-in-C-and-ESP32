## Code
```c
#include <stdio.h>
#include <stdlib.h>
#include <string.h>
#include <math.h>
#include <limits.h>
#include <float.h>
#include "esp_log.h"
#include "freertos/FreeRTOS.h"
#include "freertos/task.h"

// 🏷️ Tag สำหรับ Log
static const char *TAG = "ERROR_HANDLING";

// 🚨 enum สำหรับประเภทข้อผิดพลาด
typedef enum {
    ERROR_NONE = 0,           // ไม่มีข้อผิดพลาด
    ERROR_DIVISION_BY_ZERO,   // หารด้วยศูนย์
    ERROR_INVALID_INPUT,      // ข้อมูลผิดประเภท
    ERROR_OUT_OF_RANGE,       // ข้อมูลเกินขอบเขต
    ERROR_NEGATIVE_VALUE,     // ค่าติดลบไม่เหมาะสม
    ERROR_OVERFLOW,           // ข้อมูลล้น
    ERROR_UNDERFLOW           // ข้อมูลต่ำเกินไป
} error_code_t;

// 📊 โครงสร้างผลลัพธ์
typedef struct {
    double result;
    error_code_t error;
    char message[100];
} calculation_result_t;

// 🎨 ฟังก์ชันแสดง ASCII Art ตามสถานการณ์
void show_ascii_art(error_code_t error) {
    switch(error) {
        case ERROR_NONE:
            ESP_LOGI(TAG, "   ✅ SUCCESS ✅");
            ESP_LOGI(TAG, "      🎉🎉🎉");
            ESP_LOGI(TAG, "    สำเร็จแล้ว!");
            break;
        case ERROR_DIVISION_BY_ZERO:
            ESP_LOGI(TAG, "   🍕 ÷ 0 = ❌");
            ESP_LOGI(TAG, "   😱 โอ้ะโอ!");
            ESP_LOGI(TAG, "  ไม่มีลูกค้า!");
            break;
        case ERROR_INVALID_INPUT:
            ESP_LOGI(TAG, "   📝 ABC บาท?");
            ESP_LOGI(TAG, "   🤔 งง...");
            ESP_LOGI(TAG, "  ตัวเลขหายไป");
            break;
        case ERROR_OUT_OF_RANGE:
            ESP_LOGI(TAG, "   📈 ∞∞∞∞∞");
            ESP_LOGI(TAG, "   😵 เกินขีด!");
            ESP_LOGI(TAG, "  ใหญ่เกินไป");
            break;
        default:
            ESP_LOGI(TAG, "   ❓ ERROR ❓");
            ESP_LOGI(TAG, "   🔧 แก้ไข");
            ESP_LOGI(TAG, "  ต้องตรวจสอบ");
    }
}

// 🛡️ ฟังก์ชันตรวจสอบการหารด้วยศูนย์
calculation_result_t safe_divide(double dividend, double divisor, const char* context) {
    calculation_result_t result = {0};
    
    ESP_LOGI(TAG, "\n🔍 ตรวจสอบการหาร: %s", context);
    ESP_LOGI(TAG, "📊 %g ÷ %g = ?", dividend, divisor);
    
    // ตรวจสอบหารด้วยศูนย์
    if (divisor == 0.0) {
        result.error = ERROR_DIVISION_BY_ZERO;
        ESP_LOGE(TAG, "%s", result.message);
        show_ascii_art(ERROR_DIVISION_BY_ZERO);
        ESP_LOGI(TAG, "💡 แนะนำ: ตรวจสอบจำนวนลูกค้าก่อนแบ่งพิซซ่า");
        return result;
    }
    
    // ตรวจสอบผลลัพธ์ล้น
    result.result = dividend / divisor;
    if (isinf(result.result)) {
        result.error = ERROR_OVERFLOW;
        strcpy(result.message, "⚠️ เตือน: ผลลัพธ์เป็น infinity!");
        ESP_LOGW(TAG, "%s", result.message);
        return result;
    }
    
    // สำเร็จ
    result.error = ERROR_NONE;
    sprintf(result.message, "✅ สำเร็จ: %.2f ÷ %.2f = %.2f", dividend, divisor, result.result);
    ESP_LOGI(TAG, "%s", result.message);
    show_ascii_art(ERROR_NONE);
    
    return result;
}

// 💰 ฟังก์ชันตรวจสอบค่าเงิน
calculation_result_t validate_money(double amount, const char* description) {
    calculation_result_t result = {0};
    
    ESP_LOGI(TAG, "\n💰 ตรวจสอบเงิน: %s", description);
    ESP_LOGI(TAG, "💵 จำนวน: %.2f บาท", amount);
    
    // ตรวจสอบค่าติดลบ
    if (amount < 0) {
        result.error = ERROR_NEGATIVE_VALUE;
        ESP_LOGE(TAG, "%s", result.message);
        ESP_LOGI(TAG, "💡 แนะนำ: ตรวจสอบการคิดเงินใหม่");
        return result;
    }
    
    // ตรวจสอบเกินขีดจำกัด (1 ล้านล้าน)
    if (amount > 1000000000000.0) {
        result.error = ERROR_OUT_OF_RANGE;
        ESP_LOGW(TAG, "%s", result.message);
        show_ascii_art(ERROR_OUT_OF_RANGE);
        ESP_LOGI(TAG, "💡 แนะนำ: ใช้ระบบธนาคารกลาง");
        return result;
    }
    
    // ตรวจสอบทศนิยมมากเกินไป
    double rounded = round(amount * 100) / 100;  // ปัดเศษสตางค์
    if (fabs(amount - rounded) > 0.001) {
        ESP_LOGW(TAG, "⚠️ เตือน: ปัดเศษจาก %.4f เป็น %.2f บาท", amount, rounded);
        amount = rounded;
    }
    
    result.result = amount;
    result.error = ERROR_NONE;
    sprintf(result.message, "✅ จำนวนเงินถูกต้อง: %.2f บาท", amount);
    ESP_LOGI(TAG, "%s", result.message);
    
    return result;
}

// 🔢 ฟังก์ชันตรวจสอบข้อมูลตัวเลข
calculation_result_t validate_number(const char* input, const char* field_name) {
    calculation_result_t result = {0};
    
    ESP_LOGI(TAG, "\n🔢 ตรวจสอบตัวเลข: %s", field_name);
    ESP_LOGI(TAG, "📝 ข้อมูลที่ป้อน: '%s'", input);
    
    // ตรวจสอบ NULL หรือ empty
    if (input == NULL || strlen(input) == 0) {
        result.error = ERROR_INVALID_INPUT;
        strcpy(result.message, "❌ ข้อผิดพลาด: ไม่มีข้อมูล!");
        ESP_LOGE(TAG, "%s", result.message);
        return result;
    }
    
    // ลองแปลงเป็นตัวเลข
    char* endptr;
    double value = strtod(input, &endptr);
    
    // ตรวจสอบว่าแปลงได้ทั้งหมดหรือไม่
    if (*endptr != '\0') {
        result.error = ERROR_INVALID_INPUT;
        sprintf(result.message, "❌ ข้อผิดพลาด: '%s' ไม่ใช่ตัวเลข!", input);
        ESP_LOGE(TAG, "%s", result.message);
        show_ascii_art(ERROR_INVALID_INPUT);
        ESP_LOGI(TAG, "💡 แนะนำ: ใช้เฉพาะตัวเลข 0-9 และจุดทศนิยม");
        return result;
    }
    
    // ตรวจสอบ NaN หรือ infinite
    if (isnan(value) || isinf(value)) {
        result.error = ERROR_INVALID_INPUT;
        strcpy(result.message, "❌ ข้อผิดพลาด: ตัวเลขไม่ถูกต้อง!");
        ESP_LOGE(TAG, "%s", result.message);
        return result;
    }
    
    result.result = value;
    result.error = ERROR_NONE;
    sprintf(result.message, "✅ ตัวเลขถูกต้อง: %.2f", value);
    ESP_LOGI(TAG, "%s", result.message);
    
    return result;
}

// 📊 ฟังก์ชันคำนวณดอกเบี้ยอย่างปลอดภัย
calculation_result_t calculate_interest(double principal, double rate, int years) {
    calculation_result_t result = {0};
    
    ESP_LOGI(TAG, "\n🏦 คำนวณดอกเบี้ย");
    ESP_LOGI(TAG, "💰 เงินต้น: %.2f บาท", principal);
    ESP_LOGI(TAG, "📈 อัตราดอกเบี้ย: %.2f%% ต่อปี", rate);
    ESP_LOGI(TAG, "⏰ ระยะเวลา: %d ปี", years);
    
    // ตรวจสอบเงินต้น
    if (principal <= 0) {
        result.error = ERROR_NEGATIVE_VALUE;
        strcpy(result.message, "❌ เงินต้นต้องมากกว่าศูนย์!");
        ESP_LOGE(TAG, "%s", result.message);
        return result;
    }
    
    // ตรวจสอบอัตราดอกเบี้ย
    if (rate < -100 || rate > 100) {
        result.error = ERROR_OUT_OF_RANGE;
        strcpy(result.message, "❌ อัตราดอกเบี้ยไม่สมเหตุสมผล!");
        ESP_LOGE(TAG, "%s", result.message);
        ESP_LOGI(TAG, "💡 แนะนำ: ใช้อัตรา -100% ถึง 100%");
        return result;
    }
    
    // ตรวจสอบระยะเวลา
    if (years < 0 || years > 100) {
        result.error = ERROR_OUT_OF_RANGE;
        strcpy(result.message, "❌ ระยะเวลาไม่สมเหตุสมผล!");
        ESP_LOGE(TAG, "%s", result.message);
        return result;
    }
    
    // คำนวณดอกเบี้ยแบบง่าย
    double interest = principal * (rate / 100.0) * years;
    double total = principal + interest;
    
    // ตรวจสอบ overflow
    if (total > DBL_MAX / 2) {
        result.error = ERROR_OVERFLOW;
        strcpy(result.message, "⚠️ เตือน: ผลลัพธ์ใหญ่เกินไป!");
        ESP_LOGW(TAG, "%s", result.message);
        return result;
    }
    
    result.result = total;
    result.error = ERROR_NONE;
    sprintf(result.message, "✅ ดอกเบี้ย: %.2f บาท, รวม: %.2f บาท", interest, total);
    ESP_LOGI(TAG, "%s", result.message);
    
    return result;
}

// 🍕 ฟังก์ชันจำลองสถานการณ์ร้านพิซซ่า
void pizza_shop_scenario(void) {
    ESP_LOGI(TAG, "\n🍕 === สถานการณ์ร้านพิซซ่า ===");
    ESP_LOGI(TAG, "📖 วันนี้ฝนตก ไม่มีลูกค้ามากิน");
    
    calculation_result_t result;
    
    // กรณีปกติ
    result = safe_divide(12, 4, "แบ่งพิซซ่า 12 ชิ้นให้ลูกค้า 4 คน");
    vTaskDelay(pdMS_TO_TICKS(2000));
    
    // กรณีมีปัญหา
    result = safe_divide(12, 0, "แบ่งพิซซ่า 12 ชิ้นให้ลูกค้า 0 คน");
    vTaskDelay(pdMS_TO_TICKS(2000));
    
    // กรณีฟื้นตัว
    ESP_LOGI(TAG, "\n🌞 ฝนหยุดแล้ว! มีลูกค้ามา 3 คน");
    result = safe_divide(12, 3, "แบ่งพิซซ่า 12 ชิ้นให้ลูกค้า 3 คน");
}

// 💰 ฟังก์ชันจำลองสถานการณ์ร้านขายของ
void shop_scenario(void) {
    ESP_LOGI(TAG, "\n🛒 === สถานการณ์ร้านขายของ ===");
    ESP_LOGI(TAG, "📖 เจ้าของร้านป้อนข้อมูลผิด");
    
    calculation_result_t result;
    
    // ตรวจสอบข้อมูลผิดประเภท
    result = validate_number("ABC", "ราคาสินค้า");
    vTaskDelay(pdMS_TO_TICKS(2000));
    
    result = validate_number("12.50", "ราคาสินค้า");
    vTaskDelay(pdMS_TO_TICKS(1000));
    
    // ตรวจสอบเงินทอน
    result = validate_money(-50.0, "เงินทอน");
    vTaskDelay(pdMS_TO_TICKS(2000));
    
    result = validate_money(25.75, "เงินทอน");
}

// 🏦 ฟังก์ชันจำลองสถานการณ์ธนาคาร
void bank_scenario(void) {
    ESP_LOGI(TAG, "\n🏦 === สถานการณ์ธนาคาร ===");
    ESP_LOGI(TAG, "📖 ลูกค้าฝากเงินและคำนวณดอกเบี้ย");
    
    calculation_result_t result;
    
    // กรณีปกติ
    result = calculate_interest(100000, 2.5, 5);
    vTaskDelay(pdMS_TO_TICKS(2000));
    
    // กรณีอัตราดอกเบี้ยติดลบ
    result = calculate_interest(100000, -5.0, 5);
    vTaskDelay(pdMS_TO_TICKS(2000));
    
    // กรณีเงินเกินขีดจำกัด
    result = validate_money(999999999999.0, "เงินฝาก");
    vTaskDelay(pdMS_TO_TICKS(2000));
    
    // กรณีแก้ไขแล้ว
    result = calculate_interest(100000, 3.0, 10);
}

// 📊 ฟังก์ชันสรุปความรู้
void show_error_handling_summary(void) {
    ESP_LOGI(TAG, "\n📚 === สรุปการจัดการข้อผิดพลาด ===");
    ESP_LOGI(TAG, "╔════════════════════════════════════════════╗");
    ESP_LOGI(TAG, "║              ประเภทข้อผิดพลาด             ║");
    ESP_LOGI(TAG, "╠════════════════════════════════════════════╣");
    ESP_LOGI(TAG, "║ 🚫 Division by Zero - หารด้วยศูนย์        ║");
    ESP_LOGI(TAG, "║ 📝 Invalid Input - ข้อมูลผิดประเภท       ║");
    ESP_LOGI(TAG, "║ 📊 Out of Range - เกินขอบเขต             ║");
    ESP_LOGI(TAG, "║ ➖ Negative Value - ค่าติดลบไม่เหมาะสม   ║");
    ESP_LOGI(TAG, "║ ⬆️ Overflow - ข้อมูลล้น                  ║");
    ESP_LOGI(TAG, "╚════════════════════════════════════════════╝");
    
    ESP_LOGI(TAG, "\n🛡️ === หลักการจัดการข้อผิดพลาด ===");
    ESP_LOGI(TAG, "✅ 1. ตรวจสอบข้อมูลก่อนคำนวณ");
    ESP_LOGI(TAG, "✅ 2. แสดงข้อความที่เข้าใจง่าย");
    ESP_LOGI(TAG, "✅ 3. ให้คำแนะนำในการแก้ไข");
    ESP_LOGI(TAG, "✅ 4. ป้องกันโปรแกรมค้างหรือ crash");
    ESP_LOGI(TAG, "✅ 5. ใช้ enum และ struct จัดการสถานะ");
}

#include <regex.h>

// ตรวจสอบอีเมล
bool validate_email_format(const char* email) {
    regex_t regex;
    const char *pattern = "^[A-Za-z0-9._%+-]+@[A-Za-z0-9.-]+\\.[A-Za-z]{2,}$";
    if (regcomp(&regex, pattern, REG_EXTENDED | REG_NOSUB) != 0) return false;
    int result = regexec(&regex, email, 0, NULL, 0);
    regfree(&regex);
    return result == 0;
}

// ตรวจสอบเบอร์โทรศัพท์ไทย
bool validate_thai_phone(const char* phone) {
    regex_t regex;
    const char *pattern = "^(0)[0-9]{9}$";
    if (regcomp(&regex, pattern, REG_EXTENDED | REG_NOSUB) != 0) return false;
    int result = regexec(&regex, phone, 0, NULL, 0);
    regfree(&regex);
    return result == 0;
}

// ตรวจสอบรหัสประชาชนไทย
bool validate_thai_id(const char* id) {
    if (strlen(id) != 13) return false;
    int sum = 0;
    for (int i = 0; i < 12; ++i) {
        if (id[i] < '0' || id[i] > '9') return false;
        sum += (id[i] - '0') * (13 - i);
    }
    int check_digit = (11 - (sum % 11)) % 10;
    return check_digit == (id[12] - '0');
}

// Retry Mechanism สำหรับ operation
typedef calculation_result_t (*operation_func)(void);
calculation_result_t retry_operation(operation_func func, int max_retries, int delay_ms) {
    calculation_result_t result;
    for (int attempt = 1; attempt <= max_retries; ++attempt) {
        ESP_LOGI(TAG, "🔁 Attempt %d...", attempt);
        result = func();
        if (result.error == ERROR_NONE) {
            ESP_LOGI(TAG, "✅ Operation สำเร็จในรอบที่ %d", attempt);
            return result;
        }
        vTaskDelay(pdMS_TO_TICKS(delay_ms));
    }
    ESP_LOGW(TAG, "❌ ล้มเหลวหลังจากพยายาม %d ครั้ง", max_retries);
    return result;
}

// ฟังก์ชันจำลองสถานการณ์ validation
void validation_scenario(void) {
    ESP_LOGI(TAG, "\n📨 === ตรวจสอบข้อมูลฟอร์ม ===");

    const char* emails[] = { "test@example.com", "invalid-email@", "user@domain.co.th" };
    const char* phones[] = { "0912345678", "12345", "0899999999" };
    const char* ids[] = { "1101700203451", "1234567890123", "abcdefghijklm" };

    for (int i = 0; i < 3; ++i) {
        ESP_LOGI(TAG, "\n📧 ตรวจสอบอีเมล: %s", emails[i]);
        ESP_LOGI(TAG, "✅ ผลลัพธ์: %s", validate_email_format(emails[i]) ? "ถูกต้อง" : "❌ ผิดพลาด");
        vTaskDelay(pdMS_TO_TICKS(1000));
    }

    for (int i = 0; i < 3; ++i) {
        ESP_LOGI(TAG, "\n📞 ตรวจสอบเบอร์: %s", phones[i]);
        ESP_LOGI(TAG, "✅ ผลลัพธ์: %s", validate_thai_phone(phones[i]) ? "ถูกต้อง" : "❌ ผิดพลาด");
        vTaskDelay(pdMS_TO_TICKS(1000));
    }

    for (int i = 0; i < 3; ++i) {
        ESP_LOGI(TAG, "\n🆔 ตรวจสอบบัตรประชาชน: %s", ids[i]);
        ESP_LOGI(TAG, "✅ ผลลัพธ์: %s", validate_thai_id(ids[i]) ? "ถูกต้อง" : "❌ ผิดพลาด");
        vTaskDelay(pdMS_TO_TICKS(1000));
    }
}


void app_main(void) {
    ESP_LOGI(TAG, "🚀 เริ่มต้นโปรแกรมจัดการข้อผิดพลาด!");
    ESP_LOGI(TAG, "🛡️ การตรวจสอบและป้องกันข้อผิดพลาด\n");
    
    // รอสักครู่เพื่อให้ระบบเริ่มต้นเสร็จสิ้น
    vTaskDelay(pdMS_TO_TICKS(1000));
    
    // จำลองสถานการณ์ต่างๆ
    pizza_shop_scenario();
    vTaskDelay(pdMS_TO_TICKS(3000));
    
    shop_scenario();
    vTaskDelay(pdMS_TO_TICKS(3000));
    
    bank_scenario();
    vTaskDelay(pdMS_TO_TICKS(3000));
    validate_email_format();
    validate_thai_phone();
    validate_thai_id();
    // สรุปความรู้
    show_error_handling_summary();
    
    ESP_LOGI(TAG, "\n✅ เสร็จสิ้นการเรียนรู้การจัดการข้อผิดพลาด!");
    ESP_LOGI(TAG, "🎓 ได้เรียนรู้: enum, struct, error codes, และการตรวจสอบข้อมูล");
    ESP_LOGI(TAG, "🏆 ตอนนี้คุณสามารถเขียนโค้ดที่ปลอดภัยและน่าเชื่อถือแล้ว!");
}
```

## Result
```c
I (2477) ERROR_HANDLING: 🚀 เริ่มต้นโปรแกรมจัดการข้อผิดพลาด!
I (2477) ERROR_HANDLING: 🛡️ การตรวจสอบและป้องกันข้อผิดพลาด

I (3477) ERROR_HANDLING: 
🍕 === สถานการณ์ร้านพิซซ่า ===
I (3477) ERROR_HANDLING: 📖 วันนี้ฝนตก ไม่มีลูกค้ามากิน
I (3477) ERROR_HANDLING: 
🔍 ตรวจสอบการหาร: แบ่งพิซซ่า 12 ชิ้นให้ลูกค้า 4 คน
I (3477) ERROR_HANDLING: 📊 12 ÷ 4 = ?
I (3487) ERROR_HANDLING: ✅ สำเร็จ: 12.00 ÷ 4.00 = 3.00
I (3497) ERROR_HANDLING:    ✅ SUCCESS ✅
I (3497) ERROR_HANDLING:       🎉🎉🎉
I (3497) ERROR_HANDLING:     สำเร็จแล้ว!
I (5497) ERROR_HANDLING: 
🔍 ตรวจสอบการหาร: แบ่งพิซซ่า 12 ชิ้นให้ลูกค้า 0 คน
I (5497) ERROR_HANDLING: 📊 12 ÷ 0 = ?
E (5497) ERROR_HANDLING: 
I (5497) ERROR_HANDLING:    🍕 ÷ 0 = ❌
I (5497) ERROR_HANDLING:    😱 โอ้ะโอ!
I (5497) ERROR_HANDLING:   ไม่มีลูกค้า!
I (5497) ERROR_HANDLING: 💡 แนะนำ: ตรวจสอบจำนวนลูกค้าก่อนแบ่งพิซซ่า
I (7497) ERROR_HANDLING: 
🌞 ฝนหยุดแล้ว! มีลูกค้ามา 3 คน
I (7497) ERROR_HANDLING: 
🔍 ตรวจสอบการหาร: แบ่งพิซซ่า 12 ชิ้นให้ลูกค้า 3 คน
I (7497) ERROR_HANDLING: 📊 12 ÷ 3 = ?
I (7497) ERROR_HANDLING: ✅ สำเร็จ: 12.00 ÷ 3.00 = 4.00
I (7497) ERROR_HANDLING:    ✅ SUCCESS ✅
I (7497) ERROR_HANDLING:       🎉🎉🎉
I (7497) ERROR_HANDLING:     สำเร็จแล้ว!
I (10497) ERROR_HANDLING: 
🛒 === สถานการณ์ร้านขายของ ===
I (10497) ERROR_HANDLING: 📖 เจ้าของร้านป้อนข้อมูลผิด
I (10497) ERROR_HANDLING: 
🔢 ตรวจสอบตัวเลข: ราคาสินค้า
I (10497) ERROR_HANDLING: 📝 ข้อมูลที่ป้อน: 'ABC'
E (10497) ERROR_HANDLING: ❌ ข้อผิดพลาด: 'ABC' ไม่ใช่ตัวเลข!
I (10497) ERROR_HANDLING:    📝 ABC บาท?
I (10497) ERROR_HANDLING:    🤔 งง...
I (10497) ERROR_HANDLING:   ตัวเลขหายไป
I (10497) ERROR_HANDLING: 💡 แนะนำ: ใช้เฉพาะตัวเลข 0-9 และจุดทศนิยม
I (12497) ERROR_HANDLING: 
🔢 ตรวจสอบตัวเลข: ราคาสินค้า
I (12497) ERROR_HANDLING: 📝 ข้อมูลที่ป้อน: '12.50'
I (12497) ERROR_HANDLING: ✅ ตัวเลขถูกต้อง: 12.50
I (13497) ERROR_HANDLING: 
💰 ตรวจสอบเงิน: เงินทอน
I (13497) ERROR_HANDLING: 💵 จำนวน: -50.00 บาท
E (13497) ERROR_HANDLING: 
I (13497) ERROR_HANDLING: 💡 แนะนำ: ตรวจสอบการคิดเงินใหม่
I (15497) ERROR_HANDLING: 
💰 ตรวจสอบเงิน: เงินทอน
I (15497) ERROR_HANDLING: 💵 จำนวน: 25.75 บาท
I (15497) ERROR_HANDLING: ✅ จำนวนเงินถูกต้อง: 25.75 บาท
I (18497) ERROR_HANDLING: 
🏦 === สถานการณ์ธนาคาร ===
I (18497) ERROR_HANDLING: 📖 ลูกค้าฝากเงินและคำนวณดอกเบี้ย
I (18497) ERROR_HANDLING: 
🏦 คำนวณดอกเบี้ย
I (18497) ERROR_HANDLING: 💰 เงินต้น: 100000.00 บาท
I (18497) ERROR_HANDLING: 📈 อัตราดอกเบี้ย: 2.50% ต่อปี
I (18497) ERROR_HANDLING: ⏰ ระยะเวลา: 5 ปี
I (18497) ERROR_HANDLING: ✅ ดอกเบี้ย: 12500.00 บาท, รวม: 112500.00 บาท
I (20497) ERROR_HANDLING: 
🏦 คำนวณดอกเบี้ย
I (20497) ERROR_HANDLING: 💰 เงินต้น: 100000.00 บาท
I (20497) ERROR_HANDLING: 📈 อัตราดอกเบี้ย: -5.00% ต่อปี
I (20497) ERROR_HANDLING: ⏰ ระยะเวลา: 5 ปี
I (20497) ERROR_HANDLING: ✅ ดอกเบี้ย: -25000.00 บาท, รวม: 75000.00 บาท
I (22497) ERROR_HANDLING: 
💰 ตรวจสอบเงิน: เงินฝาก
I (22497) ERROR_HANDLING: 💵 จำนวน: 999999999999.00 บาท
I (22497) ERROR_HANDLING: ✅ จำนวนเงินถูกต้อง: 999999999999.00 บาท
I (24497) ERROR_HANDLING: 
🏦 คำนวณดอกเบี้ย
I (24497) ERROR_HANDLING: 💰 เงินต้น: 100000.00 บาท
I (24497) ERROR_HANDLING: 📈 อัตราดอกเบี้ย: 3.00% ต่อปี
I (24497) ERROR_HANDLING: ⏰ ระยะเวลา: 10 ปี
I (24497) ERROR_HANDLING: ✅ ดอกเบี้ย: 30000.00 บาท, รวม: 130000.00 บาท
I (27497) ERROR_HANDLING: 
📚 === สรุปการจัดการข้อผิดพลาด ===
I (27497) ERROR_HANDLING: ╔════════════════════════════════════════════╗
I (27497) ERROR_HANDLING: ║              ประเภทข้อผิดพลาด             ║
I (27497) ERROR_HANDLING: ╠════════════════════════════════════════════╣
I (27497) ERROR_HANDLING: ║ 🚫 Division by Zero - หารด้วยศูนย์        ║
I (27497) ERROR_HANDLING: ║ 📝 Invalid Input - ข้อมูลผิดประเภท       ║
I (27497) ERROR_HANDLING: ║ 📊 Out of Range - เกินขอบเขต             ║
I (27497) ERROR_HANDLING: ║ ➖ Negative Value - ค่าติดลบไม่เหมาะสม   ║
I (27497) ERROR_HANDLING: ║ ⬆️ Overflow - ข้อมูลล้น                  ║
I (27497) ERROR_HANDLING: ╚════════════════════════════════════════════╝
I (27507) ERROR_HANDLING: 
🛡️ === หลักการจัดการข้อผิดพลาด ===
I (27507) ERROR_HANDLING: ✅ 1. ตรวจสอบข้อมูลก่อนคำนวณ
I (27507) ERROR_HANDLING: ✅ 2. แสดงข้อความที่เข้าใจง่าย
I (27507) ERROR_HANDLING: ✅ 3. ให้คำแนะนำในการแก้ไข
I (27507) ERROR_HANDLING: ✅ 4. ป้องกันโปรแกรมค้างหรือ crash
I (27507) ERROR_HANDLING: ✅ 5. ใช้ enum และ struct จัดการสถานะ
I (27507) ERROR_HANDLING: 
✅ เสร็จสิ้นการเรียนรู้การจัดการข้อผิดพลาด!
I (27507) ERROR_HANDLING: 🎓 ได้เรียนรู้: enum, struct, error codes, และการตรวจสอบข้อมูล
I (27507) ERROR_HANDLING: 🏆 ตอนนี้คุณสามารถเขียนโค้ดที่ปลอดภัยและน่าเชื่อถือแล้ว!
I (27507) main_task: Returned from app_main()
```
