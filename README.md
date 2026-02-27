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
7. Deploy ง่าย

*เหมาะกับงานแบบไหน*
1. ใช้ CPU เยอะ หรือ CPU ทำงานตลอดเวลา
2. ไม่ต้องรอ DB หรือ Network
3. AI / ประมวลผลภาพ / คำนวณคณิตศาสตร์หนักๆ / เข้ารหัส
4. งานที่ต้องการความ performance เสถียร มาก



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
