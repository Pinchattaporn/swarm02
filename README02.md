# swarm02 django

## ขั้นตอนการสร้าง
 - [1.สร้างและใช้งาน Vm](#1สร้างและใช้งาน-vm)
 - 2.[Stack และ Portainer](#2.portainer)
 - 3.[Revert proxy](#3revert-proxy)
 - 4.[Create django](#4create-django)

 # 1.สร้างและใช้งาน Vm
- สร้าง Vm เบื้องต้นได้ที่
   * https://github.com/Pinchattaporn/SPCN-011
   * Vm spec
        * Ubuntu 22.04
        * CPU 2 cores
        * Ram 2 GB
        * HDD 32 GB
        
- เมื่อสร้าง Vm เสร็จแล้วทำการ clone ออกมา 3  Node ได้แก่
    * mannger (spcn-manager)
    * work1 (spcn-worker1)
    * work2 (spcn-worker2)

- ทำการ Set Hostname ใหม่ ด้วยคำสั่ง
    *  hostnamectl set-hostname " ชื่อชื่อใหม่ที่เราต้องการตั้ง"
        * hostname ใหม่ของดิฉัน ได้แก่
            * spcn-manager
            * spcn-worker1
            * spcn-worker2
- เช็คเลข ip ไม่ให้ซ้ำกันเพื่อทำการ Remote ssh ที่ Vscode
    * ติดตั้ง Extension ที่เกี่ยวกับงาน(ssh,wakatime)
    * เชื่อม ssh ไปยัง Vm ที่เราจะทำ Remote ssh
        * ssh root@172.31.1.176 (manager)
        * ssh root@172.31.1.163 (worker1)
        * ssh root@172.31.1.142 (worker2)

# 2.Stack และ Portainer
    ในการสร้าง Docker swarm ถ้าสร้างโดยการใช้ CT อาจจะไม่รองรับ swarm ได้ครบถ้วน จึงต้องใช้ Vm แทน


 # 3.Revert proxy

 # 4.Create django

