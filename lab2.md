# การทดลองที่ 2 การเขียนโปรแกรมค้นหาไวไฟ
## วัตถุประสงค์
1. เพื่อเรียนรู้วิธีการเขียนโปรแกรมค้นหาไวไฟ
2. เพื่อเรียนรู้วิธีการรันโปรแกรมบนไมโครคอนโทรเลอร์ ESP-01
## อุปกรณ์ที่ใช้
1. ไมโครคอนโทรเลอร์ (ESP-01)
2. อุปกรณ์ต่อ USB
3. CPU
4. เสาอากาศสำหรับ WIFI
## ศึกษาข้อมูลเบื้องต้น
1. 02 run example 2 https://youtu.be/yBjab0UNuB8
2. src code 02_Scan-Wifi https://github.com/choompol-boonmee/lab63b/blob/master/examples/02_Scan-Wifi/src/main.cpp
## วิธีการทำการทดลอง 
1. นำไมโครคอนโทรเลอร์ต่อเข้ากับ USB
2. เปิดโปรแกรม Command prompt
3. เตรียมอัปโหลดตัวอย่างโปรแกรม โดยพิมพ์ vi src/main.cpp จะแสดงออกมา ดังนี้
``` #include <Arduino.h>
#include <ESP8266WiFi.h>

int cnt = 0;

void setup()
{
	Serial.begin(115200);
	WiFi.mode(WIFI_STA);
	WiFi.disconnect();
	delay(100);
	Serial.println("\n\n\n");
}

void loop()
{
	Serial.println("========== เริ่มต้นแสกนหา Wifi ===========");
	int n = WiFi.scanNetworks();
	if(n == 0) {
		Serial.println("NO NETWORK FOUND");
	} else {
		for(int i=0; i<n; i++) {
			Serial.print(i + 1);
			Serial.print(": ");
			Serial.print(WiFi.SSID(i));
			Serial.print(" (");
			Serial.print(WiFi.RSSI(i));
			Serial.println(")");
			delay(10);
		}
	}
	Serial.println("\n\n");
}
```
4. พิมพ์คำสั่ง pio run -t upload เพื่ออัปโหลดโปรแกรมเข้าไมโครคอนโทรเลอร์
5. กดปุ่มบู๊ธ และกดปุ่มรีเซตที่ตัวไมโครคอนโทรเลอร์ และทำการอัปโหลดโปรแกรม
6. เมื่ออัปโหลดโปรแกรมสำเร็จแล้ว จะแสดงดังภาพ ![image](https://user-images.githubusercontent.com/80880047/112277739-a11d8380-8cb4-11eb-8289-ed996455a34a.png)

7. พิมพ์คำสั่ง pio device monitor จะแสดงผลการแสกน Wifi ดังภาพ ![image](https://user-images.githubusercontent.com/80880047/112277775-aaa6eb80-8cb4-11eb-9317-66a6c3878c2b.png)

## การบันทึกผลการทดลอง 
เมื่อทำการรันคำสั่ง pio device monitor บนหน้าต่าง command prompt จะแสดงชื่อWifiที่ได้แสกนออกมา ซึ่งจะปรากฏออกมาบนหน้าต่างหรือไม่นั้น ขึ้นอยู่กับความแรงของสัญญาณ
## อภิปรายผลการทดลอง
จากการทดลอง จะพบว่าเมื่อเราทำการอัปโหลดโปรแกรมที่สามารถแสกนหาWifiลงบนตัวไมโครคอนโทรเลอร์และใช้คำสั่ง pio device monitor เราจะเห็นตัวสัญญาณWifi ที่อยู่รอบๆตัวได้
## คำถามหลังการทดลอง
* Q: ทำไมเมื่อเริ่มแสกนหา Wifi ในเวลาไล่เลี่ยกันจะมีจำนวนสัญญาณขึ้นมาไม่เท่ากัน
* A: ขึ้นอยู่กับความแรงของสัญญาณที่ได้รับ
