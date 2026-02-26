# What-is-Golang
เนื่องจากมีความสนใจในภาษา Golang จึงได้ทำขึ้นมาเพื่อนสรุปความเข้าใจ (Because I am interested in the Golang programming language, I created this to summarize my understanding.)

# Go Lang
เป็นภาษาที่สร้างและสนับสนุนโดย Google เป็นภาษาที่ถูกสร้างมาเพื่อการทำ(เหมาะ) Logic หรือ back-end
go land คล้ายกับภาษา C แต่ลดความซับซ้อน อ่านง่าน กระชับ มากกว่า C แต่ยังไม่สามารถ สู้ rust ได้

*จุดเด่น*
1. ทำงานได้รวดเร็ว
2. ไม่ซับซ้อน เข้าใจง่าย
3. รองรับผู้ใช้งานจำนวนมาก
4. มีประสิทธิภาพสูง
5. ไฟล์มีขนาดเล็ก (.bit)
6. ทำงานแบบ Concurrency* ได้


# ทุกโปรแกรมใน Go ต้องอยู่ในแพ็กเกจ
-------------------------------
package main

import "fmt"

func main() {
	fmt.Println("Hello, 世界")
}
------------------------------

ถ้ามี file package main และมี func mina() = executable program (.exe)
import "fmt"
fmt = format
เป็น package มาตราฐานของ Go ใช้สำหรับ output / input / text style

func = ประกาศฟังก์ชัน
เมื่อเราสั่ง go run main.go โปรแกรมจะเริ่มทำงานที่ฟังก์ชัน main() เสมอ

# การประกาศตัวแปรใน Go

