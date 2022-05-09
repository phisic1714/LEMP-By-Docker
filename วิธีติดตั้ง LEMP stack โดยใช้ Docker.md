# Introduce LEMP
LEMP Stack ที่เป็นกลุ่มของ Open Source Software สำหรับเขียน Website ด้วยภาษา PHP บน Docker Container ซึ่งประกอบไปด้วย Software ดังต่อไปนี้
   - L = Linux OS
   - E = (E)Nginx Web Server
   - M = MariaDB
   - P = PHP
โดยผมจะแบ่งขั้นตอนการติดตั้งตาม ตัวอักษรย่อ เหล่านี้

# L (Linux OS)
เราจะใช้ตัว Shell ของ Linux หรือที่เรียกว่า Unix shell เพื่อที่จะใช้ในขั้นตอนการติดตั้งส่วน E M P ต่อไป 
ในที่นี้ผมยังใช้ Windows OS อยู่ผมก็จะหาโปรแกรมที่จำลอง Unix shell เช่น WSL และ Git Bash (ในที่นี้ผมใช้ Git Bash เพราะลงไว้อยู่แล้ว :D )

# E ((E)Nginx Web Server)
การติดตั้ง Nginx Web Server
1. เข้า Terminal แล้ว สร้าง Directory(Folder) โดยใช้คำสี่ง mkdir [ชื่อโฟล์เดอร์] และ สร้าง File โดยใช้คำสี่ง touch [ชื่อไฟล์] ตาม list นี้

 - nginx_dock
   - docker-compose.yml
   - static-html/
     * index.html

2. ใน File [docker-compose.yml] ให้เข้าไปเพิ่ม code ตามลิ้งนี้ https://github.com/phisic1714/LEMP-By-Docker/blob/main/nginx_dock/docker-compose.yml
3. ใน File [index.html] ให้เข้าไปเพิ่ม code ตามลิ้งนี้ ให้เข้าไปเพิ่ม code ตามลิ้งนี้ https://github.com/phisic1714/LEMP-By-Docker/blob/main/nginx_dock/static-html/index.html
4. กลับมาที่ Terminal แล้วใช้คำสี่ง *docker-compose up -d* เพื่อรัน Container
5. ตรวจเช็คว่า Web server ใช้ได้หรือยังโดย ใส่ *localhost:80* ในช่อง URL ถ้าได้จะแสดง Hello Nginx ตาม ที่เราแก้ใน File [index.html]
  * Note: สามารถตรวจเช็คได้ใน Docker Desktop ว่า Nginx Server ทำงานหรือไม่

# P (PHP)
การติดตั้ง PHP ก็จะผนวกกับ Nginx เข้าด้วยกัน
1. เข้า Terminal แล้ว สร้าง Directory(Folder) โดยใช้คำสี่ง mkdir [ชื่อโฟล์เดอร์] และ สร้าง File โดยใช้คำสี่ง touch [ชื่อไฟล์] ตาม list นี้ 

 - lemp_dock
   - docker-compose.yml
   - html/
     * index.php
   - nginx/
    - conf/
      * nginx.conf
    - conf.d/
      * default.conf

2. 

# M (MariaDB)




