/*
# esp32-net-radio
Example code for esp32 and I2S module
ตัวอย่างการเขียนโปรแกรมบน ESP32 โดยใช้ Arduino IDE
ESp32  -->    I2S
G25    -->    LRC
G26    -->    BCK
G22    -->    DIN
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

Coding: esp32netRadio-github.ino
Libraries: WiFiEspAT.zip, ESP32-audioI2S-master.zip
