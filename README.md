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

## Vonneuman และ Harvard
<br>![image](https://vivadifferences.com/wp-content/uploads/2019/10/Von-Neuman-Vs-Harvard-Architecture.png)
- Vonneuman จะเก็บข้อมูล(Data)และชุดคำสั่ง(Instruction)ในหน่วยความจำเดียวกัน
- Harvard จะเก็บข้อมูล(Data)และชุดคำสั่ง(Instruction)แยกกันคนละหน่วยความจำ

## ความแตกต่างระหว่าง Single cycle กับ Multi-cycle
### Single cycle
- Single cycle คือวงจรดิจิตอลที่ทำให้การอ่านและการทำตามคำสั่งที่ป้อนเข้ามาจบภายใน 1 cycle
- ความแตกต่างจาก Multi-cycle คือ ALU 3 ตัว, Memory 2 ตัว, 1 คำสั่ง = 1 Cycle  
<br>![image](https://i.stack.imgur.com/vCvw1.png)

### Multi-cycle
- multi-cycle คือในหนึ่งคำสั่งไม่จำเป็นต้องจบใน 1 cycle
- ความแตกต่างจาก Single cycle คือ ALU 1 ตัว, Memory 1 ตัว, 1 คำสั่ง อาจจะใช้เวลาน้อยกว่าหรือมากกว่า 1 Cycle ก็ได้, มี register a,b ไว้พักข้อมูล และมี ALUout ที่เก็บค่าหลังจากคำนวณ
<br>![image](https://camo.githubusercontent.com/3a759f503101d7359e3b9e88a79a64b022814d5a/68747470733a2f2f692e696d6775722e636f6d2f6d5758485770542e706e67)

## การทำงานของ multi-cycle ในคำสั่ง lw
คำสั่ง lw ใน Multi Cycle นั้นมีทั้งหมด 5 ขั้นตอน
    
    1.อ่านคำสั่งจาก Memory มาเก็บใน Instruction Register และทำ PC = PC + 4 พร้อมๆกัน
    
    2.Instruction Register แบ่งออกเป็น 2 ส่วน คือ $rs และ $rt โดยจะนำค่า $rs ไปเก็บไว้ใน A และ $rt ไปเก็บไว้ใน B นำค่า offset จาก 16 บิท มาแปลงเป็น 
      32 บิท แล้วนำไปที่ ALU เพื่อบวกกับ PC แล้วนำไปเก็บที่ ALUout
   
    3.นำค่า A เข้ามาบวกกับ offset และนำค่าไปเก็บไว้ที่ ALUout
    
    4.ค่าที่ได้จาก ALUout คือ address ของ memory และอ่านค่าออกมา
    
    5.นำค่าที่อ่านมาจาก Memory ไปเก็บไว้ใน $rt
* [CLIP2](https://www.youtube.com/watch?v=VXF8znfaz4c&t=2s) การทำงานของ CPU
   <br>**สรุปเนื้อหา** ในการพัฒนาซอฟต์แวร์โดย่วไปเราจะใช้ภาษาชั้นสูงหรือภาษาที่มนุษย์เข้าใจเพื่อเขียนได้ง่าย เช่น ภาษาจาวา ในคลิปนี้เราจะยกตัวอย่างการบวกเลขที่เขียนอยู่ในรูปแบบภาษาจาวาให้แปลงเป็นภาษาเครื่องที่computerสามารถเข้าใจได้

* [CLIP3](https://www.youtube.com/watch?v=DNC7Z_a5DQw&t=2s) ความแตกต่างระหว่าง multi-cycle และ single-cycle
   <br>**สรุปเนื้อหา** single-cycle คือวงจรดิจิตอลที่ทำให้การอ่านและการทำตามคำสั่งที่ป้อนเข้ามาจบภายใน 1 cycle ส่วน multi-cycle ในหนึ่งคำสั่งไม่จำเป็นต้องจบใน 1 cycle ในคลิปนี้จะเปรียบเทียบความแตกต่างระหว่าง multi-cycle และ single-cycle ว่าในทั้งสองวงจรแตกต่างกันอย่างไร

* [CLIP4](https://www.youtube.com/watch?v=5PSLMtB3A4w&t=2s) การทำงานของ multi-cycle ในคำสั่ง lw
   <br>**สรุปเนื้อหา** อธิบายขั้นตอนการทำงานของคำสั่ง loadword ใน multi-cycle ว่ามีขั้นตอนการทำงานยังไงบ้าง

## beq ใน Multi-cycle
- beq เป็นคำสั่งประเภท I- format เป็นคำสั่ง jump แบบมีเงื่อนไข โดยจะดูว่าข้อมูลของ register rs และ register rt เท่ากันหรือไม่ หากเท่ากันจะทำการ jump ไปยังตำแหน่งถัดไป โดยจะมีทั้งหมด 3 ขั้นตอนดังนี้
    
    1.อ่านคำสั่งจาก Memory มาเก็บใน IR (Instruction Register) และนำ PC = PC + 4 พร้อมๆกัน
    
    2.นำค่า $rs และ $rt ไปเก็บไว้ที่ A,B ตามลำดับ (A = Reg[IR[25-21]]) (B = Reg[IR[20-16]])
   
    3.นำค่าจาก A และ B มาเปรียบเทียบกัน หากเท่ากันจะเก็บผลลัพธ์ที่ได้ไว้ใน ALUout แล้ว JUMP ไปยัง Address ต่อไป 
    
      หากไม่เท่ากันจะข้ามไปทำคำสั่งถัดไปทันที
* [CLIP5](https://www.youtube.com/watch?v=LgCJY-U_9ng&t=30s) การทำงานของ multi-cycle ในคำสั่ง beq
   <br>**สรุปเนื้อหา** อธิบายขั้นตอนการทำงานของคำสั่ง beq ใน multi-cycle ว่ามีขั้นตอนการทำงานยังไงบ้าง

* [CLIP6](https://www.youtube.com/watch?v=gHtHq8iDkDg&t=59s) การทำงานของคำสั่ง R-type ใน multi-cycle
   <br>**สรุปเนื้อหา** อธิบายขั้นตอนการทำงานของคำสั่ง R-type ใน multi-cycle ว่ามีขั้นตอนการทำงานยังไงบ้าง
