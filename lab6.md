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
4. รันคำสั่ง vi src/main.cpp จะแสดงตัวอย่างโปรแกรมดังนี้
#include <ESP8266WiFi.h>
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
## การบันทึกผลการทดลอง
## อภิปรายผลการทดลอง
## คำถามหลังการทดลอง
