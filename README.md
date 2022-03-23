/*
# esp32-net-radio
Example code for esp32 and I2S module
ตัวอย่างการเขียนโปรแกรมบน ESP32 โดยใช้ Arduino IDE
ESp32  -->    I2S
G25    -->    LRC
G26    -->    BCK
G27    -->    DIN
GND    -->    GAIN
3.3V   -->    VIN
GND    -->    GND

การเปลี่ยนสถานีใช้ Serial Monitor ของ Arduino IDE
พิมพ์คำสั่ง    สถานี
CCH1 -->    http://vis.media-ice.musicradio.com/CapitalMP3
CCH2 -->    http://0n-80s.radionetz.de:8000/0n-70s.mp3
CCH3 -->    http://streaming510.radionomy.com/FanRadioX
CCH4 -->    edge.audio.3qsdn.com/senderkw-mp3

สามารถเพิ่มสถานีได้ แต่ต้องเป็น Streaming MP3 หรือ สร้างสถานีของตัวเองโดยไปตั้งสถานีที่
https://zeno.fm/

**Coding:**
*/
#include "Arduino.h"
#include "WiFi.h"
#include "Audio.h"

#define I2S_DOUT    27 //25
#define I2S_BCLK    26 //27
#define I2S_LRC     25//26
Audio audio;
String ssid =    "your network name";
String password = "your network password";
char * myMusic = "https://node-12.zeno.fm/qkzm7ev2bf9uv?rj-ttl=5&rj-tok=AAABfZRP9RgADi0V6VeDkKgmLg";
char * myMusic2= "https://node-20.zeno.fm/qkzm7ev2bf9uv?rj-ttl=5&rj-tok=AAABfZRK5BoAJc9Y6Sxz1oQGnQ";
void setup() {
  WiFi.disconnect();
  WiFi.mode(WIFI_STA);
  WiFi.begin(ssid.c_str(), password.c_str());
  while (WiFi.status() != WL_CONNECTED)
  Serial.println("Wi-Fi Connected...");
  delay(1500);
  Serial.begin(115200);
  Serial.println("Key in Channel:");
  Serial.println("CH1 =  http://vis.media-ice.musicradio.com/CapitalMP3");
  Serial.println("CH2 =  http://0n-80s.radionetz.de:8000/0n-70s.mp3");
  Serial.println("CH3 =  http://streaming510.radionomy.com/FanRadioX");
  Serial.println("CH4 =  edge.audio.3qsdn.com/senderkw-mp3");
    
  audio.setPinout(I2S_BCLK, I2S_LRC, I2S_DOUT);
  audio.setVolume(10);
  audio.connecttohost("http://vis.media-ice.musicradio.com/CapitalMP3");
}
void loop()
{
  if(Serial.available()){
    String channel = Serial.readString();
    if(channel.indexOf("CH1")>0){
      Serial.println("Channel 1");
      audio.setPinout(I2S_BCLK, I2S_LRC, I2S_DOUT);
      audio.connecttohost("http://vis.media-ice.musicradio.com/CapitalMP3");
    }
    else if(channel.indexOf("CH2")>0){
      Serial.println("Channel 2");
      audio.setPinout(I2S_BCLK, I2S_LRC, I2S_DOUT);
      audio.connecttohost("http://0n-80s.radionetz.de:8000/0n-70s.mp3");
    }
     else if(channel.indexOf("CH3")>0){
      Serial.println("Channel 3");
      audio.setPinout(I2S_BCLK, I2S_LRC, I2S_DOUT);
      audio.connecttohost("http://streaming510.radionomy.com/FanRadioX");
    }
     else if(channel.indexOf("CH4")>0){
      Serial.println("Channel 4");
      audio.setPinout(I2S_BCLK, I2S_LRC, I2S_DOUT);
      audio.connecttohost("edge.audio.3qsdn.com/senderkw-mp3");
    }
    else if(channel.indexOf("Vol1")>0){
      Serial.println("Volume 10%");
      audio.setVolume(10);
    }
    else if(channel.indexOf("Vol5")>0){
      Serial.println("Volume 50%");
      audio.setVolume(50);
    }
    else if(channel.indexOf("VolA")>0){
      Serial.println("Volume 100%");
      audio.setVolume(100);
    }
  }
  audio.loop();
}
