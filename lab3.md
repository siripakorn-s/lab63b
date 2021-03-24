# การทดลองที่3 เรื่อง การเขียนโปรแกรมเอ้าพุทสัญญาญาณดิจิทัล
## วัตถุประสงค์
1. เพื่อเรียนรู้เกี่ยวกับรีเลย์
2. เพื่อเรียนรู้เกี่ยวกับไมโครคอนโทรลเลอร์
## อุปกรณ์ที่ใช้
1. ไมโครคอนโทรล​เลอร์ ESP-01
2. คอมพิวเตอร์
3. อแดปเตอร์เพื่อรองรับพอร์ท0กับ1
4. สาย USB
5. serial port
6. รีเลย์
7. ชุดหลอดไฟLED
## ศึกษาข้อมูลเบื้องต้น
1. 03 run example 3 : https://www.youtube.com/watch?v=CCnN1WJsXQY
2. src code ของโปรแกรม 03_Output-Port : https://github.com/choompol-boonmee/lab63b/blob/master/examples/03_Output-Port/src/main.cpp
## วิธีการทำการทดลอง
1. ต่อไมโครคอนโทรล​เลอร์และอแดปเตอร์เข้า serial port
2. เปิดโปรแกรม Command prompt
3. เตรียมอัปโหลดตัวอย่างโปรแกรม โดยพิมพ์ vi src/main.cpp จะแสดงออกมา ดังนี้ 
 ```#include <Arduino.h>
#include <ESP8266WiFi.h>

int cnt = 0;

void setup()
{
	Serial.begin(115200);
	pinMode(0, OUTPUT);
	Serial.println("\n\n\n");
}

void loop()
{
	cnt++;
	if(cnt % 2) {
		Serial.println("========== ON ===========");
		digitalWrite(0, HIGH);
	} else {
		Serial.println("========== OFF ===========");
		digitalWrite(0, LOW);
	}
	delay(500);
}
```
4. กดปุ่มดำบนไมโครคอนโทรล​เลอร์เพื่อติดตั้ง และกดปุ่มแดงบนไมโครคอนโทรล​เลอร์เพื่อรีเซ็ต 
![image](https://user-images.githubusercontent.com/80880047/112281039-353d1a00-8cb8-11eb-8d1d-befe0bd8d1d7.png)

5. พิมพ์คำสั่ง pio device monitor เพื่อแสดงผล   ![image](https://user-images.githubusercontent.com/80880047/112282021-476b8800-8cb9-11eb-87fb-5511e8b21f97.png)
![image](https://user-images.githubusercontent.com/80880047/112282075-54887700-8cb9-11eb-8e67-2e1ecda769dc.png)

6. ต่อไมโครคอนโทรลเลอร์เข้ากับรีเลย์   ![image](https://user-images.githubusercontent.com/80880047/112281797-0a9f9100-8cb9-11eb-899a-b55be324b779.png)

7. ต่อรีเลย์เข้ากับขั้วชาร์ต  ![image](https://user-images.githubusercontent.com/80880047/112281824-125f3580-8cb9-11eb-941f-d78450483228.png)


## การบันทึกผลการทดลอง
เมื่อรันโปรแกรม จะแสดงผลเป็นonกับoffทุกครึ่งวินาที และเมื่อดูที่ไฟLEDที่พอร์ท0จะเปล่งแสงออกมาตอนที่เป็นonและดับตอนเป็นoffตามคำสั่ง
## อภิปรายผล
จากการติดตั้งไฟล์ 03_ Serial-Monitor ลงไมโครคอนโทรลเลอร์เมื่อทำการรัน จะแสดงผล คือเมื่อonหน้าสัมผัสของรีเลย์จะเคลื่อนที่ทำให้ไฟLEDติด แต่เมื่อoffจะไม่มีการจ่ายไฟทำให้ไฟLEDไม่ติด และจะแสดงผลสลับกันไปเรื่อยๆ
## คำถามหลังการทดลอง
* Q: ถ้าจะต้องอัปโหลดไฟล์ตัวอย่าง จะต้องใช้คำสั่งใด
* A: pio run -t upload
