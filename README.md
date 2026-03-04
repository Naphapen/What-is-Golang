# What-is-Golang
เนื่องจากมีความสนใจในภาษา Golang จึงได้ทำขึ้นมาเพื่อนสรุปความเข้าใจ (Because I am interested in the Golang programming language, I created this to summarize my understanding.)

# Go Lang
เป็นภาษาที่สร้างและสนับสนุนโดย Google เป็นภาษาที่ถูกสร้างมาเพื่อการทำ(เหมาะ) Logic หรือ back-end
go land คล้ายกับภาษา C แต่ลดความซับซ้อน อ่านง่าน กระชับ มากกว่า C แต่ยังไม่สามารถ สู้ rust ได้

*จุดเด่น*
1. ทำงานได้รวดเร็ว
2. ไม่ซับซ้อน เข้าใจง่าย (ใกล้เคียง C/C++)
3. ไฟล์มีขนาดเล็ก (.bit) Deploy ง่าย
4. ทำงานแบบ Concurrency* ได้ดีมาก
5. ใช้ CPU และ RAM น้อย

*เหมาะกับงานแบบไหน*
1. AI / ประมวลผลภาพ / คำนวณคณิตศาสตร์หนักๆ / เข้ารหัส
2. งานที่ต้องการความ performance สูง
3. รับ request จำนวนมาก 
4. Microservices*
5. ระบบระดับ Enterprise**

*การทำงานพร้อมกัน (Concurrency)*
1. ใช้ channel สื่อสารระหว่าง thread
2. มี goroutine
3. ใช้ channel สื่อสารระหว่าง thread

# การประกาศตัวแปรใน Go
การประกาศตัวแปร แต่ไม่เรียกใช้งานจะทำให้การ Compile Error
ใช้ var ในการประกาศ 
var ชื่อตัวแปร ประเภท = ค่าเริ่มต้น หรือ var age = 10 (var จะเข้าใจว่าตัวเองเป็น int)
ประกาศตัวแปรแบบ short จะใช้ := (ชื่อตัวแปร := ค่าเริ่มต้น)
name := "pink" / age := 20 / check := true

ถ้าไม่ได้กำหนดค่าเริ่มต้น int จะเท่ากับ 0 และ string จะเท่ากับ "" (ค่าว่าง) และสามารถเข้าถึงตัวแปรได้เฉพาะภายในบล็อกโค้ดที่ประกาศตัวแปรไว้เท่านั้นเท่านั้น {}
การ import ก็เช่นกัน ถ้าไม่มีการเรียกใช้ จะไม่โชว์

*Struct*
ใช้แทน object
type User struct {
	ID   int
	Name string
}

**Package และ Export**
# ทุกโปรแกรมใน Go ต้องอยู่ในแพ็กเกจ

package main
import "fmt"
func main() {
	fmt.PrintLn("Hello word")
}

func = ประกาศฟังก์ชัน
เมื่อเราสั่ง go run main.go โปรแกรมจะเริ่มทำงานที่ฟังก์ชัน main() เสมอ

*ประเภทของ Package*

- ใช้สำหรับโปรแกรมที่รันได้ (executable program (.exe))
func main()

- Import Package
import "fmt"
fmt = format
เป็น package มาตราฐานของ Go ใช้สำหรับ output / input / text style
ถ้าต้องการ import แบบหลายตัว
import (
	"fmt"
	"net/http"
)

- Package อื่น ๆ (library)
package user
ชื่อจะเป็นตัวเล็ก ใช้เก็บ logic แยกออกจาก main

*Export คืออะไร?*
Export = การเปิดให้ package อื่นเรียกใช้ได้ 

# go routine & go channel

*go routine*
ตัวช่วยให้โปรแกรมเราทำงานไวขึ้น โดยการใส่ “go” ไว้หน้าบรรทัดที่เราต้องการจะให้ มันทำงานคู่ขนานไปด้วยกัน ซึ้งปกติโปรแกรมจะทำงานจากบนลงล่าง แต่ "go" จะทำให้ คำสั่งหรือ func สามารถทำงานพร้อมกันได้

*go channel*
channel = ท่อส่งข้อมูล เพื่อให้ *go routine* สื่อสารกัน
แทนที่จะให้หลาย thread แก้ตัวแปรเดียวกัน (เสี่ยง race condition) ให้ส่งข้อมูลผ่าน channel แทน

*Ex.*
Goroutine A ผลิตข้อมูล
Goroutine B รับข้อมูลไปใช้
ทั้งสองตัวคุยกันผ่าน channel เหมือนส่งของผ่านท่อ 📦➡️📦
package main

import "fmt"

func main() {
    ch := make(chan string)

    go func() {
        ch <- "Hello"
    }()

    msg := <-ch
    fmt.Println(msg)
}
*make(chan string) → สร้าง channel รอรับ string
*ch <- "Hello" → ส่งข้อมูลเข้า channel
*msg := <-ch → รับข้อมูลจาก channel

*จากโค้ดด้านบน*
รอรับ string ซึ่งจากโค้ดจะได้ค่า string มาจาก func ที่ถ่ายค่า "Hello" เข้า ch และ ถ่ายค่า ch เข้า msg เพื่อแสดงผล

* *Microservices และ Enterprise*
*Microservices* = การออกแบบซอฟต์แวร์ที่แบ่งระบบขนาดใหญ่ (Monolith) ออกเป็นบริการย่อยๆ (Services) หลายๆตัว ที่ทำงานอิสระต่อกัน มุ่งเน้นฟังก์ชันทางธุรกิจเฉพาะด้าน สื่อสารผ่าน API แต่ละ Services มีฐานข้อมูลของตัวเอง
ตัวอย่างบริษัทที่ใช้ Microservices -> Netflix, Amazon, Uber

*Enterprise* = ระบบระดับองค์กรขนาดใหญ่ เช่น ธนาคาร, โรงงาน, โลจิสตืกส์, ERP, บริษัทที่มีหลายแผนก / หลายสาขา ที่ต้องรองรับผู้ใช้งานจำนวนมาก ความเสถียรสูง ขยายระบบได้ ฯลฯ

Microservices Enterprise = ระบบองค์กรขนาดใหญ่ ที่มีการแบ่งบริการเล็ก ๆ หลายตัว เพื่อความเสถียร ขยายง่ายและรองรับผู้ใช้งานจำนวนมาก
