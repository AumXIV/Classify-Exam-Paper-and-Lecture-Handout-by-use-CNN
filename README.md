# Classify-Exam-Paper-and-Lecture-Handout-by-use-CNN

## เกี่ยวกับโปรเจ็ค

- โปรเจ็คนี้ใช้ Convolutional Neural Network(CNN) มาแยกประเภทเอกสารสองประเภทคือ เอกสารประกอบการสอน และกระดาษข้อสอบที่มีหน้าปกตามแบบฟอร์มที่มหาวิทยาลัยเทคโนโลยีพระจอมเกล้าธนบุรี(มจธ.)กำหนด  โดยสกุลไฟล์ต้องเป็น PDF เท่านั้น
- เราจะทำการแปลงไฟล์ PDF ให้เป็นรูปภาพ แล้วจากนั้นจึงป้อนเข้า CNN Model เพื่อทำการแยกประเภทไฟล์
- ในโปรเจ็คนี้ได้เตรียม dataset สำหรับการ Train และ Test ไว้ที่ 1260 ภาพ โดยแบ่งเป็น Train 1200 ภาพ และ Test 60 ภาพ


### ตัวอย่างหน้าปกข้อสอบตามแบบฟอร์มของมหาวิทยาลัย

![](Readme_image/example_exam.jpg)


### ตัวอย่างเอกสารประกอบการสอน

![](Readme_image/example_lecture.jpg)



## ขั้นตอนการทำงานของโมเดล

1. รับไฟล์ PDF เข้ามาแล้วแปลงหน้าแรกให้เป็นรูปภาพ
2. ย่อขนาดภาพให้เล็กลงเหลือ 150x150x3
3. นำภาพเข้าสู่ CNN ทำการใส่ filter แล้ว convolve เพื่อหา feature ต่างๆจากภาพ
4. Pooling เพื่อดึงค่าจาก bit ที่แข็งแรงของภาพออกมา
5. Flatten bit แล้วป้อนเข้า Neural Network
6. Neural Network ให้ผลเป็นชื่อ class ออกมาว่าเป็นเอกสารประเภทใด


## โครงสร้างของโมเดล

![](Readme_image/model_structure.jpg)

## การทดสอบ

1. นำไฟล์ PDF มาแปลงหน้าแรกให้เป็นรูปภาพโดยใช้ code จากไฟล์ [create_image.py](create_image.py)
2. โหลด weight (100EPOCH.h5) มาใช้กับโมเดลในไฟล์ [model.py](model.py)
3. ใช้ฟังก์ชั่น show_test() ที่เขียนไว้ด้านล่างของไฟล์ [model.py](model.py) เพื่อแสดงผลการทดสอบ


### ภาพตัวอย่างการทดสอบ
#### หน้าปกข้อสอบ ให้ผลลัพท์เป็น exam

![](Readme_image/test_exam.jpg)


#### หน้าแรกของเอกสารประกอบการเรียนการสอน ให้ผลการทดสอบเป็น lecture


![](Readme_image/test_lecture.jpg)



## ปัญหาของโครงงาน

- การลดขนาดภาพลงทำให้ภาพเสีย detail ไป model จึงไม่สามารถแยกแยะได้ถูกต้อง 100%
- ภาพเอกสารประกอบการเรียนการสอนที่เป็นแนวตั้งแล้วเป็นขาวดำ มักถูกแยกผิดเป็นหน้าปกข้อสอบ
