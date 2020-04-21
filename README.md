# computer-architecture
## ส่วนประกอบของคอมพิวเตอร์
- CPU
- Main memory
- Input/Output

## ส่วนประกอบของ CPU
- ALU
- Register
- Control Unit

## MIPS Instruction Format จะแบ่งเป็น 3 แบบ
- R-Format ใช้ในการคำนวณ เช่น บวก ลบ คูณ หาร
- I-Format ใช้ในการย้ายข้อมูล
- J-Format การ jump ไปทำงานที่ตำแหน่งอื่นและเมื่อเสร็จก็จะ jump กลับมาที่เดิม
   
   <br>![image](https://i.stack.imgur.com/5rgyM.gif)
   
* [CLIP1](https://www.youtube.com/watch?v=mwLfnskcSog) คำสั่งการบวก
   <br>**สรุปเนื้อหา** การทำงานในคำสั่่งการบวกใน R-type นั้นประกอบด้วย register 3 ตัว คือ $1(rd), $2(rs), $3(rt) ซึ่งทั้ง 3 ตัวนี้มีหน้าที่ในการเก็บค่าของตัวเลขค่าหนึ่งๆ คำสั่งนี้มักจะเขียนอยู่ในรูป | **ADD $1, $2, $3** | การทำงานของคำสั่งนี้คือ นำ $2 ไปบวกกับ $3 แล้วนำผลลัพธ์ที่ได้มาเก็บลงใน $1

# Vonneuman และ Harvard
<br>![image](https://vivadifferences.com/wp-content/uploads/2019/10/Von-Neuman-Vs-Harvard-Architecture.png)
* [CLIP2](https://www.youtube.com/watch?v=VXF8znfaz4c&t=2s) การทำงานของ CPU
   <br>**สรุปเนื้อหา** ในการพัฒนาซอฟต์แวร์โดย่วไปเราจะใช้ภาษาชั้นสูงหรือภาษาที่มนุษย์เข้าใจเพื่อเขียนได้ง่าย เช่น ภาษาจาวา ในคลิปนี้เราจะยกตัวอย่างการบวกเลขที่เขียนอยู่ในรูปแบบภาษาจาวาให้แปลงเป็นภาษาเครื่องที่computerสามารถเข้าใจได้

* [CLIP3](https://www.youtube.com/watch?v=DNC7Z_a5DQw&t=2s) ความแตกต่างระหว่าง multi-cycle และ single-cycle
   <br>**สรุปเนื้อหา** single-cycle คือวงจรดิจิตอลที่ทำให้การอ่านและการทำตามคำสั่งที่ป้อนเข้ามาจบภายใน 1 cycle ส่วน multi-cycle ในหนึ่งคำสั่งไม่จำเป็นต้องจบใน 1 cycle ในคลิปนี้จะเปรียบเทียบความแตกต่างระหว่าง multi-cycle และ single-cycle ว่าในทั้งสองวงจรแตกต่างกันอย่างไร

* [CLIP4](https://www.youtube.com/watch?v=5PSLMtB3A4w&t=2s) การทำงานของ multi-cycle ในคำสั่ง lw
   <br>**สรุปเนื้อหา** อธิบายขั้นตอนการทำงานของคำสั่ง loadword ใน multi-cycle ว่ามีขั้นตอนการทำงานยังไงบ้าง

* [CLIP5](https://www.youtube.com/watch?v=LgCJY-U_9ng&t=30s) การทำงานของ multi-cycle ในคำสั่ง beq
   <br>**สรุปเนื้อหา** อธิบายขั้นตอนการทำงานของคำสั่ง beq ใน multi-cycle ว่ามีขั้นตอนการทำงานยังไงบ้าง

* [CLIP6](https://www.youtube.com/watch?v=gHtHq8iDkDg&t=59s) การทำงานของคำสั่ง R-type ใน multi-cycle
   <br>**สรุปเนื้อหา** อธิบายขั้นตอนการทำงานของคำสั่ง R-type ใน multi-cycle ว่ามีขั้นตอนการทำงานยังไงบ้าง
