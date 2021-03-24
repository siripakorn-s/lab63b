# การทดลองที่5 เรื่อง การเขียนโปรแกรมเชื่อมต่อไวไฟและเว็บเซอร์เวอร์
## วัตถุประสงค์
1. เพื่อเรียนรู้เกี่ยวกับการเขียนโปรแกรมเชื่อมต่อไวไฟและเว็บเซอร์เวอร์
2. เพื่อเรียนรู้เกี่ยวกับไมโครคอนโทรลเลอร์
## อุปกรณ์ที่ใช้
1. ไมโครคอนโทรล​เลอร์ ESP-01
2. คอมพิวเตอร์
3. USB to serial
## ศึกษาข้อมูลเบื้องต้น
1. 05 run wifi : https://www.youtube.com/watch?v=VX-QNQcO-b4
2. src code ของโปรแกรม 05_Wifi-Web-Server : https://github.com/choompol-boonmee/lab63b/blob/master/examples/05_Wifi-Web-Server/src/main.cpp
## วิธีการทำการทดลอง
1. นำไมโครคอนโทรเลอร์ต่อเข้ากับ USB
2. เปิดโปรแกรม Command prompt
3. เตรียมอัปโหลดตัวอย่างโปรแกรม โดยพิมพ์ vi src/main.cpp จะแสดงออกมา ดังนี้
``` #include <ESP8266WiFi.h>
//#include <WiFiClient.h>
#include <ESP8266WebServer.h>

const char* ssid = "HI_BMFWIFI_2.4G";
const char* password = "0819110933";

ESP8266WebServer server(80);

int cnt = 0;

void setup(void){
	Serial.begin(115200);

	WiFi.mode(WIFI_STA);
	WiFi.begin(ssid, password);
	while (WiFi.status() != WL_CONNECTED) {
		delay(500);
		Serial.print(".");
	}
	Serial.print("\n\nIP address: ");
	Serial.println(WiFi.localIP());

	server.onNotFound([]() {
		server.send(404, "text/plain", "Path Not Found");
	});

	server.on("/", []() {
		cnt++;
		String msg = "Hello cnt: ";
		msg += cnt;
		server.send(200, "text/plain", msg);
	});

	server.begin();
	Serial.println("HTTP server started");
}

void loop(void){
  server.handleClient();
}
```
4. ใส่ชื่อWifiและPassword ลงในไฟล์ตัวอย่าง
5. อัปโหลดโปรแกรมตัวอย่างที่เลือกลงไมโครคอนโทรล​เลอร์
6. กดปุ่มดำบนไมโครคอนโทรล​เลอร์เพื่อติดตั้ง และกดปุ่มแดงบนไมโครคอนโทรล​เลอร์เพื่อรีเซ็ต
7. กดปุ่มรีเซ็ตเพื่อหาWifi โดยจะขึ้น IP Address 
8. ให้คัดลอก IP Address ไปที่บราวเซอร์ทดสอบ
## การบันทึกผลการทดลอง
เมื่อรันโปรแกรม จะแสดงผลคือจะได้ IP Address และเมื่อนำ IP Address นั้นไปที่บราวเซอร์ทดสอบ ก็จะขึ้น Hello 1 โดย cnt จะเปลี่ยนตัวแปรไปเรื่อยๆ
## อภิปรายผล
จากการติดตั้งไฟล์ 05_ Serial-Monitor ลงไมโครคอนโทรลเลอร์เมื่อทำการรัน จะแสดงผลคือจะได้ IP Address ซึ่ง IP Address ที่ได้ก็จะสามารถใช้ได้ และตัวไมโครคอนโทรลเลอร์ที่เชื่อมต่อไวไฟและเว็บเซอร์เวอร์ก็จะสามารถทำงานได้เหมือนกับเว็บเซิร์ฟเวอร์ทั่วไป
## คำถามหลังการทดลอง
* Q: ถ้าเราไม่ได้ใส่ชื่อ WifiและPassword ลงในโปรแกรมตัวอย่างเราจะสามารถรันโปรแกรมได้ไหม
* A: ไม่ได้ เพราะโปรแกรมจะไม่ทราบข้อมูลWifiที่เชื่อมต่ออยู่
