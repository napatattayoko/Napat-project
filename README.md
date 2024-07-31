# โปรเจกต์ของ Napat
โปรเจกต์นี้เกี่ยวกับระบบการขายสินค้า

วงจรการทำงานของ Git (Git WorkFlow)

    1.Working Directory(Untracked) ไฟล์ Project ที่ยังไม่ถูก Track หรือตรวจสอบ
    |    git init 
    2.Working Directory(Tracked) ใช้ Git มาตรวจสอบไฟล์ในโฟลเดอร์
    |    git add
    3.Staging Area พื้้นที่จัดเก็บเวอร์ชั่น หรือ เก็บประวัติการแก้ไข
    |    git commit
    4.Local Repository เก็บข้อมูลการแก้ไขไว้ที่เครื่องของผู้พัฒนา
    |    git push
    5.Remore Repository นำการแก้ไขทุกเวอร์ชั่นที่อยู่ในเครื่องผู้พัฒนาขึ้น Server

________________________________________________________________________________________________________

สร้าง Local Git Repository
    git init

การเพิ่มไฟล์เข้าไปใน Staging Area (Check-in)
    git add <file_name> => ระบุไฟล์ เช่น git add index.html
    git add *.html => เพิ่มหลายๆไฟล์พร้อมระบุนามสกุล
    git add . => เพิ่มทุกไฟล์ที่อยู่ภายใต้ Directory ปัจจุบัน

ลบไฟล์หรือโฟลเดอร์ออกจาก Git Repository (Remove)
    git rm -r --cached . => ลบทั้งหมด
    git rm --cached <file_name> =>  ระบุไฟล์

ตรวจสอบสถานะ (status) ดูสถานะการเปลี่ยนแปลงของ Repository
บนเครื่องของเรา (Local) เช่น การเพิ่ม ,แก้ไข ,ลบ ไฟล์ต่างๆ
    git status

ดูประวัติการ Commit (log)
โดยจะแสดง Commit ID, Message, ชื่อผู้เขียน , อีเมล , และเวลาที่ commit
    git log
    git log --oneline = แสดงแต่ละ log  เหลือบรรทัดเดียว
    git log --graph = แสดงเป็นเส้น Branch ให้ดูง่าย

________________________________________________________________________________________________________

สถานะการติดตาม (Tracked Status)
    Modified หมายถึง มีการแก้ไขไฟล์แล้วแต่ยังไม่เริ่มต้นจัดเก็บลงบน Repository
    Staged หมายถึง ได้ทำเครื่องหมาย File ที่ได้ถูกแก้ไขเพื่อบันทึกในเวอร์ชั่นหน้า
    Committed หมายถึง ข้อมูลถูกบันทึกลงใน Repository เรียนร้อยแล้ว

________________________________________________________________________________________________________

***Git Commit , Git Log***
    เก็บประวัติการแก้ไขถาวร (Commit)
    git commit -m "Log Message"
    
Option
    m เป็นพารามิเตอร์สำหรับใส่ข้อความช่วยจำ (Log Message) เพื่ออธิบายการ commit แต่ละเวอร์ชั่น
    เมื่อ Commit ไปแล้ว จะได้ SHA-1 Hash เป็น Commit ID (รหัสประจำเวอร์ชั้น) (SHA-1 Hash = 40 ตัวอักษร แต่ตอนอ้างอิงใช้แค่ 7 ตัวอักษรแรก)
________________________________________________________________________________________________________

เปรียบเทียบเวอร์ชั่น (diff)
    ใช้สำหรับตรวจสอบและเปรียบเทียบไฟล์โค้ดว่ามีอะไรเปลี่ยนแปลงและแตกต่างออกไปจากเดิมบ้างเมื่อเทียบกับ Commit ที่ผ่านมา

    git diff <commit_id> = แบบระบุ Commit ID
    git diff <commit_id><commit_id> = เปรียบเทียบระหว่างสอง Commit

    *สีสถานะ
    แสดงเครื่องหมาย - และตัวอักษรสีแดงในบรรทัดเดิมก่อนถูกแก้ไขและถูกลบ
    แสดงเครื่องหมาย + และตัวอักษรสีเขียวและโค้ดใหม่ที่ถูกแก้ไขและเพิ่มใหม่

________________________________________________________________________________________________________

ยกเลิกการแก้ไขไฟล์ (Check-out)
    คำสั่งย้อนกลับไปยัง Commit ล่าสุด หรือยกเลิกการแก้ไขไฟล์
        git checkout <file-name>

_______________________________________________________________________________________________________

Git Reset
    เป็นการย้อนเวอร์ชั่นให้กลับไปอยู่ในสภาพก่อนที่จะ add ไฟล์เข้าสู่ Staging Area ซึ่งบางครั้ง มีการเพิ่มไฟล์ลงใน Staging Area โดยไม่ตั้งใจ สามารถเอาออกได้ โดยใช้ Git reset

    git show head = โชว์ไฟล์ที่เพิ่งเพิ่มเข้าไปล่าสุด สามารถบอกว่าใครเพิ่มไฟล์นี้ไป เวลาเท่าไหร่

    git Reset (สำหรับย้อนคืนเวอร์ชั่น)
        git reset -- option <commit_id>
            soft ใช้เพื่อลบ Commit ทั้งหมดที่อยู่หลัง Commit ID แล้วนำไฟล์ที่เคยอยู่ใน Commit นั้นกลับมายัง Staging Area
            mixed ใช้เพื่อลบ Commit ทั้งหมดที่อยู่หลัง Commit ID แล้วนำไฟล์ที่เคยอยู่ใน Commit นั้นกลับมายัง Working Directory
            hard ใช้เพื่อลบ Commit ทั้งหมดที่อยู่หลัง Commit ID และจะทำลายไฟล์ที่เคยอยู่ใน Commit เหล่านั้น

_______________________________________________________________________________________________________

Git Branching
    การเพิ่มและลดกิ่ง(Branch)

    ***คำสั่งที่เกี่ยวกับ Git Branching***
        git branch
        git checkout
        git merge

    *การแสดงชื่อ Branch
        git branch
    *การสลับและสร้าง Branch
        git checkout -b <ชื่อ branch> (ห้ามตั้งชื่อเว้นวรรค)
    *การลบ Branch
        git branch -d <ชื่อ branch>
    *สลับไป Branch ที่ต้องการ
        git checkout <ชื่อ branch>
    *สลับ Branch หลัก
        git checkout master
    *การรวม Branch
        git merge <ชื่อ branch>
    *การร่วมกิ่ง (Merge)
        git merge <ชื่อ branch ที่ต้องการจะเอามาร่วมกับไฟล์หลัก>

_______________________________________________________________________________________________________

Git Push (ผลัก)
    เป็นคำสั่งที่ใช้สำหรับนำสิ่งที่อยู่ในเครื่องของเรา (Local Repository) ไปอัพเดตให้กับ Remote Repository (Server)

_______________________________________________________________________________________________________

Git pull (ดีง+รวม)
เป็นคำสั่งที่ใช้สำหรับนำสิ่งที่อยู่บน Remote Repository (Server) มาอัพเดตในเครื่องของเรา (Local Repository)
    
_______________________________________________________________________________________________________

Readme (เอกสารคู่มือ) 

