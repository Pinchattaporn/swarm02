# swarm02 django
Ref. awaresome-compose
    
- https://github.com/docker/awesome-compose/tree/master/django

Wakatime project
- https://wakatime.com/@spcn07/projects/yajbpohslz?start=2023-02-27&end=2023-03-05

Url django
- https://spcn07django.xops.ipv9.xyz/


## ขั้นตอนการสร้าง
 - [1.Create django](#1create-django)
 - [2.Images On Dockerfile](#2build-images-on-dockerfile)
 - [3.แก้ไขข้อมูลไฟล์](#3แก้ไขข้อมูลไฟล์)
 - [4.deploy stack](#4-deploy-stack)
 - [5.เช็คการเข้าใช้งาน Url.](#5เช็คการเข้าใช้งาน-url)


 # **1.Create django**
- ทำการ Clone github จาก Ref.
    * https://github.com/docker/awesome-compose/tree/master/django

    <center><img src="images/django-ct.png" alt="center"></center>

- ทำการแก้ไขข้อมูลไฟล์ compose.yaml
    * แก้ไขเลข port จาก 8000 : 8000 เป็น 
  <font color="red"> 8800 : 8000 </font>
  <center><img src="images/com-django.png" alt="center"></center>

# **2.build Images On Dockerfile**
* โดยการเข้าที่ Docker hub -> Create repository -> ตั้ง Name = <font color="red"> django</font>

<center><img src="images/create-Repo.png"></center>

 * copy path : chattaporn/django
โดยใช้คำสั่ง
     
        docker build . -t chattaporn/django:v4

 * push ขึ้น Dockerhub
    * ใช้คำสั่ง docker login เพื่อเข้าสู่ระบบก่อน
    * ใช้คำสั่ง docker push chattaporn/django:v4

 * ผลลัพธ์

    <center><img src="images/Dochub-django.png" alt="center"></center>

# **3.แก้ไขข้อมูลไฟล์**

- ทำการอนุญาติการเข้าถึงด้วย IP อื่น
  * แก้ไขที่ไฟล์ settings.py 

    <center><img src="images/ip.png"></center>

- แก้ไขข้อมูล docker-compose.yaml

<details>
<summary>Show code</summary>

```ruby
#django
version: "3"  #version compose ต้องมากกว่า 3
services:
  web: 
    image: chattaporn/django:v4 #image service on dockerhub
    ports: 
      - '8800'
    networks:
      - webproxy #network traefik
    logging:
      driver: json-file # ที่เก็บข้อมูล เก็บไว้ใน json-file
    deploy: # set ข้อมูล deploy for swarm
      replicas: 1
      labels: #set ข้อมูล label เพื่อเชื่อมต่อกับ traefik
        - traefik.docker.network=webproxy
        - traefik.enable=true
        - traefik.http.routers.spcn07django-https.entrypoints=websecure
        - traefik.http.routers.spcn07django-https.rule=Host("spcn07django.xops.ipv9.xyz")
        - traefik.http.routers.spcn07django-https.tls.certresolver=default
        - traefik.http.services.spcn07django.loadbalancer.server.port=80
      resources:
        reservations:
          cpus: '0.1'
          memory: 10M
        limits:
          cpus: '0.4'
          memory: 50M
networks:
  webproxy:
    external: true
```
</details>


# **4.deploy stack**

    * https://portainer.ipv9.me/

โดยทำการ กด Aff Stack -> ตั้งชื่อ django-spcn07 -> วางโค้ด docker- compose.yaml ที่ wab editor -> Deploy the stack

<center><img src="images/stc-dj.png" alt="center"></center>

<center><img src="images/detail.png" alt="center"></center>
 
 - ผลลัพธ์จากการ deploy stack

<center><img src="images/list-st.png" alt="center"></center>

# **5.เช็คการเข้าใช้งาน Url.**

- เช็คว่า Url เข้าใช้งานได้จริงมั้ย แสดงผลจริงมั้ย
    * https://spcn07django.xops.ipv9.xyz/

ผลลัพธ์

<center><img src="images/End.png" alt="center"></center>

Ref.ทั้งหมด
    
* https://github.com/pitimon/dockerswarm-inhoure
    
* https://youtu.be/UGEs5P5pKZ8
    
 * https://github.com/docker/awesome-compose/tree/master/django