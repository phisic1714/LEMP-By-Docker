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

 - nginx_dock/
   - docker-compose.yml
   - static-html/
     * index.html

2. ใน File [docker-compose.yml] ให้เข้าไปเพิ่ม script ตามลิ้งนี้ https://github.com/phisic1714/LEMP-By-Docker/blob/main/nginx_dock/docker-compose.yml
3. ใน File [index.html] ให้เข้าไปเพิ่ม script ตามลิ้งนี้ https://github.com/phisic1714/LEMP-By-Docker/blob/main/nginx_dock/static-html/index.html
4. กลับมาที่ Terminal ใช้คำสั่ง *CD* ไปยัง โฟล์เดอร์ nginx_dock 
5. ใช้คำสี่ง *docker network create [ชื่อที่จะตั้ง]* เพื่อสร้าง Bridge network
6. จากนั้นใช้คำสั่ง *docker-compose up -d* เพื่อรัน Container
7. ตรวจเช็คว่า Web server ใช้ได้หรือยังโดย ใส่ *localhost:80* ในช่อง URL ถ้าได้จะแสดงข้อความ Hello Nginx บนหน้า Website ตามที่เราแก้ใน File [index.html]
   * Note: สามารถตรวจเช็คได้ใน Docker Desktop ว่า Nginx Server ทำงานหรือไม่

# P (PHP)
การติดตั้ง PHP ก็จะผนวกกับ Nginx เข้าด้วยกัน
1. เข้า Terminal แล้ว สร้าง Directory(Folder) โดยใช้คำสี่ง mkdir [ชื่อโฟล์เดอร์] และ สร้าง File โดยใช้คำสี่ง touch [ชื่อไฟล์] ตาม list นี้ 

 - lemp_dock/
   - docker-compose.yml
   - html/
     * index.php
   - nginx/
    - conf/
      * nginx.conf
    - conf.d/
      * default.conf

2. ใน File [docker-compose.yml] ให้เข้าไปเพิ่ม script ตามลิ้งนี้ https://github.com/phisic1714/LEMP-By-Docker/blob/main/docker-compose.yml
3. ใน File [index.html] ให้เข้าไปเพิ่ม script ตามลิ้งนี้ https://github.com/phisic1714/LEMP-By-Docker/blob/main/index.html
4. ใน File [nginx.conf] ให้เข้าไปเพิ่ม script ตามลิ้งนี้ https://github.com/phisic1714/LEMP-By-Docker/blob/main/lemp_dock/nginx/conf/nginx.conf
5. ใน File [default.conf] ให้เข้าไปเพิ่ม script ตามลิ้งนี้ https://github.com/phisic1714/LEMP-By-Docker/blob/main/lemp_dock/nginx/conf.d/default.conf
6. กลับมาที่ Terminal ใช้คำสั่ง *CD* ไปยัง โฟล์เดอร์ lemp_dock 
7. ใช้คำสั่ง *docker-compose up -d* เพื่อรัน Container และใช้คำสั่ง *docker-compose ps* เพื่อดู Containers ที่รันทั้งหมด
8. ตรวจเช็คว่า Web server ใช้ได้หรือยังโดย ใส่ *localhost:81* ในช่อง URL ถ้าได้จะแสดง หน้า Website ของ PHP
   * Note: สามารถตรวจเช็คได้ใน Docker Desktop ว่า lemp_dock ทำงานหรือไม่
   
# M (MariaDB)
การติดตั้งก็จะผนวกกับ Nginx , PHP และ MariaDB เข้าด้วยกัน
1. Download File [titanic.sql] หรือ สร้าง File [titanic.sql] และ Copy script บรรทัดที่ 1-45 จากลิ้งนี้ https://github.com/phisic1714/LEMP-By-Docker/blob/main/lemp_dock/mariadb/initdb/titanic.sql
2. นำ Directory(Folder) เดิมจากข้อ P (PHP) หรือ โฟล์เดอร์ lemp_dock มาเพิ่ม Directory(Folder) และ File ตาม list นี้

   - mariadb/
     - data/
     - initdb/
     - backup/
   - php/
     * Dockerfile
  
3. นำ File [titanic.sql] มาวางใน โฟล์เดอร์ [initdb] จะได้ list แบบนี้

- lemp_dock/
   - docker-compose.yml
   - html/
     * index.php
   - nginx/
    - conf/
      * nginx.conf
    - conf.d/
      * default.conf
   - mariadb/
     - data/
     - initdb/
       * titanic.sql
     - backup/
   - php/
     * Dockerfile

4. ใน File [docker-compose.yml] ให้เข้าไปเพิ่ม script ตามลิ้งนี้ https://github.com/phisic1714/LEMP-By-Docker/blob/main/lemp_dock/docker-compose.yml
5. ใน File [index.html] ให้เข้าไปเพิ่ม script ตามลิ้งนี้ https://github.com/phisic1714/LEMP-By-Docker/blob/main/lemp_dock/html/index.php
6. ใน File [Dockerfile] ให้เข้าไปเพิ่ม script ตามลิ้งนี้ https://github.com/phisic1714/LEMP-By-Docker/blob/main/lemp_dock/php/Dockerfile
7. กลับมาที่ Terminal ใช้คำสั่ง *CD* ไปยัง โฟล์เดอร์ lemp_dock 
8. ใช้คำสี่ง *docker-compose build* เพื่อสร้าง PHP image
9. จากนั้นใช้คำสี่ง *docker-compose up -d* เพื่อรัน Container และใช้คำสั่ง *docker-compose ps* เพื่อดู Containers ที่รันทั้งหมด
10. ตรวจเช็คว่า Web server ใช้ได้หรือยังโดย ใส่ *localhost:81* ในช่อง URL ถ้าได้จะแสดงข้อความ Connected database server Selected database บนหน้า Website
   * Note: สามารถตรวจเช็คได้ใน Docker Desktop ว่า lemp_dock ทำงานหรือไม่    




