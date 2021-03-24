# การทดลองที่ 6 เรื่อง การเขียนโปรแกรมสร้างไวไฟแอคเซสพอยต์ (Wifi AP)
## วัตถุประสงค์
1. เพื่อเรียนรู้การเขียนโปรแกรมสร้าง Wifi AP
## อุปกรณ์ที่ใช้
1. ไมโครคอนโทรเลอร์ (ESP-01)
2. อุปกรณ์ต่อ USB to serial
3. CPU
4. ตัวโปรแกรมสร้างไวไฟแอคเซสพอยต์ (06_Wifi-AP-Web-Server)
## ศึกษาข้อมูลเบื้องต้น
1. 06 run wiri AP : https://www.youtube.com/watch?v=T26DVHePlTs
2. src code ของโปรแกรม 06_Wifi-AP-Web-Server : https://github.com/choompol-boonmee/lab63b/blob/master/examples/06_Wifi-AP-Web-Server/src/main.cpp
## วิธีการทำการทดลอง
1. นำอแดปเตอร์ต่อเข้ากับUSB
2. นำไมโครคอนโทรลเลอร์ต่อเข้ากับพอร์ท
3. เปิดโปรแกรม Command prompt ค้นหาโปรแกรมโดยใช้คำสั่ง cd pattani
4. รันคำสั่ง vi src/main.cpp ตั้งชื่อWifi และ Password จะแสดงตัวอย่างโปรแกรมดังนี้
``` #include <ESP8266WiFi.h>
//#include <WiFiClient.h>
#include <ESP8266WebServer.h>

const char* ssid = "TUENG-ESP-WIFI";
const char* password = "choompol";

IPAddress local_ip(192, 168, 1, 1);
IPAddress gateway(192, 168, 1, 1);
IPAddress subnet(255, 255, 255, 0);

ESP8266WebServer server(80);

int cnt = 0;

void setup(void){
	Serial.begin(115200);

	WiFi.softAP(ssid, password);
	WiFi.softAPConfig(local_ip, gateway, subnet);
	delay(100);

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
5. สร้างIP Address,gateway,subnet และ เตรียมweb server ![image](https://user-images.githubusercontent.com/80880047/112279580-a54aa080-8cb6-11eb-9946-3a565cc7323e.png)

6. อัปโหลดโปรแกรมในไมโครคอนโทรลเลอร์ โดยใช้คำสั่ง pio run -t upload
7. กดปุ่มอัปโหลด
 ![image](https://user-images.githubusercontent.com/80880047/112279476-8ba95900-8cb6-11eb-98dd-50089e40a16c.png)

8. รันคำสั่ง pio device monitor เพื่อดูผลลัพธ์
9. ทดสอบโปรแกรมโดยค้นหา Wifi ผ่านโทรศัพท์มือถือ โดยใส่ Password ที่เราตั้งไว้ ![image](https://user-images.githubusercontent.com/80880047/112279505-9368fd80-8cb6-11eb-8be4-156cc51bb480.png)

## การบันทึกผลการทดลอง
จากการทดลองเมื่อเรารันโปรแกรมสร้าง Wifi ลงบนตัวไมโครคอนโทรลเลอร์ จะสามารถแสกนหา Wifi ที่เราสร้างไว้บนโทรศัพท์มือถือจากการเขียนโปรแกรม
## อภิปรายผลการทดลอง
เราสามารถสร้าง Wifi ขึ้นมาใช้เองได้ โดยสามารถตั้งชื่อ password ขึ้นได้ตามปกติ
## คำถามหลังการทดลอง
* Q: เราสามารถใช้อุปกรณ์ใดเพื่อทดสอบว่า Wifiที่สร้างขึ้นนั้นใช้งานได้หรือไม่
* A: คอมพิวเตอร์หรือโทรศัพท์มือถือ
