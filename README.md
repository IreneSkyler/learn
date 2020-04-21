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
   
* [CLIP1](https://www.youtube.com/watch?v=mwLfnskcSog)

## Vonneuman และ Harvard
<br>![image](https://vivadifferences.com/wp-content/uploads/2019/10/Von-Neuman-Vs-Harvard-Architecture.png)
- Vonneuman จะเก็บข้อมูล(Data)และชุดคำสั่ง(Instruction)ในหน่วยความจำเดียวกัน
- Harvard จะเก็บข้อมูล(Data)และชุดคำสั่ง(Instruction)แยกกันคนละหน่วยความจำ
lass Test { 
## การทำงานของ CPU
- ในการพัฒนา software โดยทั่วไปเราจะใช้ภาษาชั้นสูงหรือภาษาที่มนุษย์เข้าใจเพื่อเขียนได้ง่าย เราจะยกตัวอย่างเป็นภาษา Java ในตัวอย่างนี้จะเป็นคำสั่งที่ให้เอาตัวเลขมาบวกกัน
            public static void main(String[] args){

                     int a = 10;

                     int b = 20;

                     int c = a+b;
             }
    }

- เมื่อแปลเป็นภาษาที่คอมพิวเตอร์เข้าใจ หรือ Machine Language

      00000000:           08400000        //j 01000000 

      00000004:           1A000000        //data
       ...
      01000000:           8C090004        //lw $9,$0(4)

      01000004:           8D210000       //lw $1,$9(0)

      01000008:           8D220004       //lw $2,$9(4)

      0100000C:           00221820        //add $3,$1,$2 

      01000010:           AD230008        //sw $9,$0(4)
      ...
      1A000000:           0000000A        //a = 10

      1A000004:           00000014        //b = 20

      1A000008:           0000001E        //c = 30
* [CLIP2](https://www.youtube.com/watch?v=VXF8znfaz4c&t=2s)

## ความแตกต่างระหว่าง Single cycle กับ Multi-cycle
### Single cycle
- Single cycle คือวงจรดิจิตอลที่ทำให้การอ่านและการทำตามคำสั่งที่ป้อนเข้ามาจบภายใน 1 cycle
- ความแตกต่างจาก Multi-cycle คือ ALU 3 ตัว, Memory 2 ตัว, 1 คำสั่ง = 1 Cycle  
   <br>![image](https://i.stack.imgur.com/vCvw1.png)

### Multi-cycle
- multi-cycle คือในหนึ่งคำสั่งไม่จำเป็นต้องจบใน 1 cycle
- ความแตกต่างจาก Single cycle คือ ALU 1 ตัว, Memory 1 ตัว, 1 คำสั่ง อาจจะใช้เวลาน้อยกว่าหรือมากกว่า 1 Cycle ก็ได้, มี register a,b ไว้พักข้อมูล และมี ALUout ที่เก็บค่าหลังจากคำนวณ
<br>![image](https://camo.githubusercontent.com/3a759f503101d7359e3b9e88a79a64b022814d5a/68747470733a2f2f692e696d6775722e636f6d2f6d5758485770542e706e67)

* [CLIP3](https://www.youtube.com/watch?v=DNC7Z_a5DQw&t=2s)

## การทำงานของ multi-cycle ในคำสั่ง lw
คำสั่ง lw ใน Multi Cycle นั้นมีทั้งหมด 5 ขั้นตอน
    
    1.อ่านคำสั่งจาก Memory มาเก็บใน Instruction Register และทำ PC = PC + 4 พร้อมๆกัน
    
    2.Instruction Register แบ่งออกเป็น 2 ส่วน คือ $rs และ $rt โดยจะนำค่า $rs ไปเก็บไว้ใน A และ $rt ไปเก็บไว้ใน B นำค่า offset จาก 16 บิท มาแปลงเป็น 
      32 บิท แล้วนำไปที่ ALU เพื่อบวกกับ PC แล้วนำไปเก็บที่ ALUout
   
    3.นำค่า A เข้ามาบวกกับ offset และนำค่าไปเก็บไว้ที่ ALUout
    
    4.ค่าที่ได้จาก ALUout คือ address ของ memory และอ่านค่าออกมา
    
    5.นำค่าที่อ่านมาจาก Memory ไปเก็บไว้ใน $rt

* [CLIP4](https://www.youtube.com/watch?v=5PSLMtB3A4w&t=2s)

## beq ใน Multi-cycle
- beq เป็นคำสั่งประเภท I- format เป็นคำสั่ง jump แบบมีเงื่อนไข โดยจะดูว่าข้อมูลของ register rs และ register rt เท่ากันหรือไม่ หากเท่ากันจะทำการ jump ไปยังตำแหน่งถัดไป โดยจะมีทั้งหมด 3 ขั้นตอนดังนี้
    
    1.อ่านคำสั่งจาก Memory มาเก็บใน Instruction Register และทำ PC = PC + 4 พร้อมๆกัน
    
    2.Instruction Register แบ่งออกเป็น 2 ส่วน คือ $rs และ $rt โดยจะนำค่า $rs ไปเก็บไว้ใน A และ $rt ไปเก็บไว้ใน B
   
    3.นำค่าที่ A และ B มาเปรียบเทียบกัน หากเท่ากันจะเก็บผลลัพธ์ที่ได้ไว้ใน ALUout ถ้าไม่เท่าจะข้ามไปทำคำสั่งถัดไปทันที
    
* [CLIP5](https://www.youtube.com/watch?v=LgCJY-U_9ng&t=30s)
   
## State Machine ของคำสั่ง R-Type
<br>![image](https://media.discordapp.net/attachments/702190327771168791/702190402400419980/T1.jpg?width=949&height=671)
      T1 - MemRead = 1                   อ่านค่าจาก Memory
           IorD = 1                      อ่านว่าปัจจุบัน PC ชี้ไปที่ Address ใดใน Memory
           IRWrite = 1                   นำค่าจาก Memory ไปเก็บไว้ที่ Instruction Register
           ALUSrcA = 0                   นำค่า PC ผ่าน MUX ไปที่ ALU เพื่อคำนวณ
           ALUSrcB = 1                   นำค่า 4 ผ่าน MUX ไปที่ ALU เพื่อคำนวณ
           ALUOP = ADD                   นำค่า PC ไปบวก 4 
           PCWrite = 1, PCSource = 1     นำค่ากลับไปใส่ที่ PC
           
<br>![image](https://media.discordapp.net/attachments/702190327771168791/702192044948324462/T2.jpg?width=949&height=671)
      T2 - ALUSrcA = 0                   นำค่า PC ผ่าน MUX ไปที่ ALU เพื่อคำนวณ
           ALUSrcB = 3                   นำค่า 3 ผ่าน MUX ไปที่ ALU เพื่อคำนวณ
           ALUOP = 0                     ทำการคำนวณโดยการบวกค่า PC กับ offset แต่ใน r-type ไม่มี opset จึงไม่ทำการคำนวณ

<br>![image](https://media.discordapp.net/attachments/702190327771168791/702192054440296580/T3.jpg?width=949&height=671)
      T3 - ALUSrcA = 1                   นำค่าจาก Rs มาเก็บใน A จากนั้น นำค่า A ผ่าน MUX ไปที่ ALU
           ALUSrcB = 0                   นำค่าจาก Rt มาเก็บใน B จากนั้น นำค่า A ผ่าน MUX ไปที่ ALU
           ALUOP = 2                     นำค่า  rs และ rt มาคำนวณกัน แล้วนำค่าที่ได้ไปเก็บใน ALUout

<br>![image](https://media.discordapp.net/attachments/702190327771168791/702192053978791996/T4.jpg?width=949&height=671)
      T4 - RegWrite = 1                  นำ ALUout ไปเก็บใน register rd
           MemtoReg = 0                  นำค่าจาก ALUout ไปใส่ใน register
           RegDst = 1                    นำค่าจาก register rd ไปใส่ใน register
           
* [CLIP6](https://www.youtube.com/watch?v=gHtHq8iDkDg&t=59s)
   
## Pipelining
- เราจะยกตัวอย่าง A,B,C,D คือคำสั่ง ในวงจรนี้เราจะกำหนดให้มีทั้งหมด 4 คำสั่ง ซึ่งแต่ละคำสั่งจะแบ่งออกเป็น 4 step คือ washer dryer folder stasher ดังภาพด้านล่าง
<br>![image](http://3.bp.blogspot.com/-6RQaYhlYk2k/UKTYQVX9csI/AAAAAAAAAGQ/0xF1OxF_N_Y/s1600/02-What-is-pipelining-01.png)
- วงจรนี้เปรียบเทียบเหมือนกับ single cycle คือทำงานทีละคำสั่งกล่าวคือต้องทำคำสั่ง A เสร็จก่อนจึงไปทำคำสั่ง B ต่อได้ ซึ่งการทำเช่นนี้ทำให้เสียเวลา

<br>![image](http://2.bp.blogspot.com/-4YXOlZ30iCQ/UKTYR4Y4FLI/AAAAAAAAAGk/pCdSkaaazVA/s1600/02-What-is-pipelining-02.png)
- ภาพนี้จะทำให้เห็นถึงการทำงานของ pipelining คือในกรณีที่คำสั่ง A washer เสร็จแล้ว แล้วกำลัง dryer ระบบก็สามารถนำคำสั่ง B มา washer ได้เลย โดยไม่ต้องรอให้ทำคำสั่ง A เสร็จก่อน หรือกล่าวคือเมื่อมีอุปกรณ์ในวงจรว่างก็สามารถนำคำสั่งอื่นมาทำต่อได้เลย

* [CLIP7](https://www.youtube.com/watch?v=nbCyIxsHY40&t=59s)
