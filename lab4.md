# การทดลองที่ 4 เรื่อง การเขียนโปรแกรมอินพุทสัญญาณดิจิทัล
## วัตถุประสงค์
1. เพื่อเรียนรู้วิธีการเขียนโปรแกรมอินพุทสัญญาณดิจิทัล
2. เพื่อศึกษาการทำงานของเซนเซอร์
## อุปกรณ์ที่ใช้
1. ไมโครคอนโทรเลอร์ (ESP-01)
2. อแดปเตอร์ที่ต่อสายพอร์ท 
3. อุปกรณ์ต่อ USB to serial
4. หลอดไฟ LED
5. CPU
6. ตัวโปรแกรมเอ้าพุทสัญญาณ (04_Input-Port)
7. เซนเซอร์แสง
## ศึกษาข้อมูลเบื้องต้น
1. 04 run example 4 : https://www.youtube.com/watch?v=nFqoZT26U5k
2. src code ของโปรแกรม 04_Input-Port : https://github.com/choompol-boonmee/lab63b/blob/master/examples/04_Input-Port/src/main.cpp
## วิธีการทำการทดลอง
1. นำอแดปเตอร์ต่อเข้ากับUSB 
2. นำไมโครคอนโทรลเลอร์ต่อเข้ากับพอร์ท
3. เปิดโปรแกรม Command prompt ค้นหาโปรแกรมโดยใช้คำสั่ง cd pattani
4. รันคำสั่ง vi src/main.cpp จะแสดงตัวอย่างโปรแกรมดังนี้
``` #include <Arduino.h>
#include <ESP8266WiFi.h>

int cnt = 0;

void setup()
{
	Serial.begin(115200);
	pinMode(0, INPUT);
	pinMode(2, OUTPUT);
	Serial.println("\n\n\n");
}

void loop()
{
	int val = digitalRead(0);
	Serial.printf("======= read %d\n", val);
	if(val==1) {
		digitalWrite(2, LOW);
	} else {
		digitalWrite(2, HIGH);
	}
	delay(100);
}
```
5. อัปโหลดโปรแกรมในไมโครคอนโทรลเลอร์ โดยใช้คำสั่ง pio run -t upload
6. กดปุ่มอัปโหลด ![image](https://user-images.githubusercontent.com/80880047/112278047-fc4f7600-8cb4-11eb-90d1-7d0b21076d56.png)

7. รันคำสั่ง pio device monitor ![image](https://user-images.githubusercontent.com/80880047/112278583-944d5f80-8cb5-11eb-873f-26595edf3364.png)

8. เสียบสายไฟเส้นสีดำไปในช่องสีขาว สังเกตการเปลี่ยนแปลงของหลอด LED  ![image](https://user-images.githubusercontent.com/80880047/112278610-9b746d80-8cb5-11eb-866c-6b2fde90dd1e.png)

9. กดปุ่มสีดำที่ต่อกับพอร์ต สังเกตการเปลี่ยนแปลง ![image](https://user-images.githubusercontent.com/80880047/112278653-a4fdd580-8cb5-11eb-83fc-0fd23676f051.png)

10. นำเซนเซอร์แสงต่อเข้ากับ CPU
11. เสียบสายไฟเส้นสีขาวต่อเข้ากับเซนเซอร์ ![image](https://user-images.githubusercontent.com/80880047/112278928-eaba9e00-8cb5-11eb-9891-4dc38d79d232.png)

12. ทำการบังแสงและเปิดรับแสงบริเวณเซนเซอร์ สังเกตการเปลี่ยนแปลง ![image](https://user-images.githubusercontent.com/80880047/112278973-f8702380-8cb5-11eb-8ec1-1acaaf5535a4.png)
![image](https://user-images.githubusercontent.com/80880047/112279033-06be3f80-8cb6-11eb-8d0f-178e3f01dfaf.png)


## การบันทึกผลการทดลอง 
จากการทดลอง เมื่อเราทำการรันโปรแกรมลงบนไมโครคอนโทรลเลอร์ หน้าต่าง command prompt จะแสดงผล input เป็น 1 และ 0 ซึ่งเมื่อ input เป็น 1 หลอดไฟ LED จะดับ และเมื่อinput เป็น 0 หลอดไฟก็จะติด และเมื่อเรานำตัวไมโครคอนโทรลเลอร์ที่ได้ลงโปรแกรมแล้วมาต่อกับตัวเซนเซอร์แสง จากนั้นทำการบังแสงและเปิดรับแสง จะเห็นว่าเมื่อเราทำการบังแสง input ที่ได้จะเป็น 1 นั่นก็คือไฟจะดับ และเมื่อเราทำการเปิดรับแสง จะได้ค่าinput เป็น 0 ไฟก็จะติดนั่นเอง
## อภิปรายผลการทดลอง
เมื่อเราทดลองรันโปรแกรมลงบนตัวไมโครคอนโทรลเลอร์ แล้วสังเกตinput ที่ได้ สรุปได้ว่า เมื่อ input ออกมาเป็น 0 หลอดไฟจะติดและเมื่อ input ที่ได้เป็น 1 หลอดไฟจะดับ
## คำถามหลังการทดลอง
* Q: เมื่อเรานำเซนเซอร์แสงมาต่อเข้ากับ CPU แล้วทำการบังแสง ทำไมหลอดไฟจึงดับ
* A: มีค่าความต้านทานสูงขึ้น หลอดไฟจึงดับ
