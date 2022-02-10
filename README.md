# Commit 1 : Create server.js

สร้างไฟล์ server.js เพื่อใช้จัดการกับส่วน backend โดยใช้ express.js เพื่อใช้งาน middleware โดยสร้าง app เป็นตัวแปร instance ของ express ซึ่งสามารถเรียกใช้ use ในการเรียกใช้ middleware อื่น , get ในการรับ get request ของ url ที่เรากำหนดโดย ตัวฟังก์ชั่นที่ใช้ใน get ก็เป็น middleware เรียกว่า middleware function โดยสามารถจัดการ response และ request ได้ , listen ใช้ในการรับการเชื่อมต่อใน port นั้นๆ

# Commit 2 : Create database config file

สร้าง folder app สำหรับรวมระบบ backend ทั้งหมดโดยในทีนี้เราสร้าง folder config ก่อนสำหรับเก็บข้อมูลการตั้งค่าสำหรับเชื่อม database และสร้างไฟล์ db.config.js ข้างในนั้น ข้างในไฟล์ได้ทำการสร้างตัวแปรสำหรับเก็บค่าต่างๆไม่ว่าจะเป็น host, user, password, ชื่อ database, ตัว database ที่ใช้, และ pool (ที่เป็น option เสริมสำหรับการทำงานของ database)

# Commit 3 : Create models for database

ทำการดึงตัว db.config.js ที่เราได้สร้างไว้มาใช้งาน และมีการเรียกใช้งาน sequelize.js เพื่อใช้เชื่อมกับ database โดยใช้การตั้งค่าจาก config file ที่เรียกมาใช้และมีการเรียกใช้ model ที่เราสร้างไว้ที่ชื่อ "todo.model.js" โดยข้างในไฟล์ได้มีการประกาศโครงสร้างข้อมูลว่าแต่ละ column มีชื่ออะไรและรับค่าชนิดอะไรบ้าง โดยใช้คำสั่ง define ตั้งชื่อ model ว่า todo เมื่อเราทำการ run ในส่วนนี้ โปรแกรมจะไปสร้าง table ใน database โดยใช้ชื่อว่า todos ซึ่งมี s เพิ่มมา

# Commit 4 : Create controllers and edit published to finished

ทำการสร้าง folder controllers และ todo.controller.js เพื่อจัดการเป็นตัวกลางระหว่าง model กับส่วนของ view(ในที่นี้คือส่วนของ react) โดยข้างในก็จะมีการ export function การทำงานต่างๆโดยที่มีการรับค่า response กับ request นั่นคือเป็น function ที่ทำงานเป็น milddleware เช่น create ทำหน้าที่เพิ่มข้อมูลลง database, findAll ทำหน้าที่ค้นหาทั้งหมดใน database แบบมีเงื่อนไข, findOne ทำหน้าที่หาข้อมูลใน database โดยใช้ id, update ทำหน้าที่ update ข้อมูลใน database โดยแก้ตาม id, delete ทำหน้าที่ลบข้อมูลใน database โดยลบตาม id, deleteAll ทำหน้าที่ลบข้อมูลทั้งหมดใน database, findAllFinished ทำหน้าที่ค้นหาข้อมูลโดยเลือกเฉพาะที่ attribute finished เป็น true

แก้ไขทุกจุดที่มีการใช้คำว่า published เป็น finished โดยมีในที่ todo.model.js และ todo.controller.js

# Commit 5 : Create express router

import function ต่างๆจาก todo.controller.js เก็บไว้ที่ตัวแปร todo จากนั้นสร้าง router โดยเอามาจาก express เพื่อใช้ในการเปลี่ยน url โดย post request ไปที่ url "/" ในการเรียกใช้ todo.create, get request ไปที่ url "/" ในการเรียกใช้ todo.findAll, get request ไปที่ url "/finished" ในการเรียกใช้ todo.findAllFinished, get request ไปที่ url "/:id" โดยที่เป็น dynamic url ส่งค่า id มาให้เพื่อใช้ใน todo.findOne , put request ไปที่ url "/:id" โดยที่เป็น dynamic url ส่งค่า id มาให้เพื่อใช้ใน todo.update , delete request ไปที่ url "/:id" โดยที่เป็น dynamic url ส่งค่า id มาให้เพื่อใช้ใน todo.delete , delete request ไปที่ url "/" ในการเรียกใช้ todo.deleteAll สุดท้ายใช้ app.use ส่งค่า url "/api/todo" กับตัว router เป็นการตั้งค่าให้ baseURL ขึ้นต้นด้วย /api/todo ก่อนที่จะเป็น url อื่นๆที่กล่าวมา

# Commit 6 : Setup React for frontend

สร้าง React โปรเจคโดยใช้ คำสั่ง npx create-react-app react-crud จากนั้นทำการลบไฟล์ที่ไม่จำเป็นและแก้ไขโค้ดที่ต่อไปถึงไฟล์นั้น โดยมี
- App.test.js
- logo.svg
- reportWebVitals.js
- setupTests.js <br>
- logo.png ทั้งหมดใน folder public

จากนั้นแก้ไขโค้ดในส่วนของ App.js โดยลบทั้งหมดใน return แล้วใส่แค่ div tag <br>

# Commit 7 : Create routing system by using react router

ทำการ import Router, Switch, Route, Link จาก react-router-dom จากนั้น ในส่วนของ app ทำการสร้าง navbar โดยเป็น Link ไปหน้าต่างๆเรียงกัน โดยมี TODO-LIST และ Add โดย TODO-LIST เป็นหน้าแรก และ Add เป็นหน้าที่สอง โดยเราใช้วิธีการเปลี่ยนหน้าด้วย react router เราจึงครอบมันด้วย Link component โดยจะไปตาม path ที่เรากำหนด 
ส่วนต่อมา สิ่งที่อยู่ด้านใน Switch tag คือสิ่งที่จะแสดงผลในหน้า web ซึ่งจะเห็นว่า มี Route component อยู่ 3 อัน หมายถึง เมื่อเราเข้าตาม path ที่เรากำหนดใน Route  มันก็จะเลือก component ที่จะแสดงผล มันก็จะเหมือนกับการเปลี่ยนหน้า web ไปเรื่อยๆเวลาเราเข้า URL ของเว็บที่ต่างกัน 

# Commit 8 : Create endpoint system

สร้างไฟล์ http-common.js โดยจะเป็นการใช้ axios กำหนดค่า baseURL และ header ของ http request ที่เราจะใช้ต่อไป โดยจะเห็นว่า header กำหนดให้ส่งข้อมูลแบบ JSON จากนั้นเพิ่ม folder ชื่อ services และสร้างไฟล์ todo.service.js โดยข้างในจะมีการ import http-common มาใช้จากนั้นจะสร้าง class TodoListDataService ที่มี method ที่เป็นการพาไปที่ endpoint ต่างๆของ backend จากนั้นก็ export class นี้เพื่อนำไปใช้ที่อื่นต่อไป โดย method ต่างๆมีดังนี้
- getAll() ก็จะส่ง http GET request ไปที่ /todo 
- get(id) ส่ง http GET request ไปที่ /todo/id ก็คือส่ง id ไปด้วย
- create(data) ส่ง http POST request ไปที่ /todo นั่นคือเป็น request สำหรับส่ง data ไป เพราะเป็น POST request และ แนบ data ไปด้วย
- update(id,data) ส่ง http PUT request ไปที่ /todo/id เป็นการส่ง request เพื่อไปเปลี่ยนข้อมูลแบบเฉพาะ เพราะมีการส่ง data และ ระบุ id ไปด้วย
- delete(id) ส่ง http DELETE request ไปที่ /todo/id เป็นการส่ง request เพื่อไปลบข้้อมูลแบบเฉพาะเพราะมีการระบุ id ไปด้วย
- deleteAll() ส่ง http DELETE request ไปที่ /todo เป็นการส่ง request เพื่อไปลบข้้อมูลทั้งหมด
- findByTitle(title) ส่ง http GET request ไปที่ /todo/title=${title} จะเห็นว่ามีการส่งตัวแปร title ที่รับมาต่อไปด้วยเพื่อที่ backend จะเอาไปใช้เพื่อค้นหาข้อมูลตาม title

# Commit 9 : Create TodoList Component

สร้าง components folder แล้วสร้าง components TodoList เก็บไว้ในไฟล์ todo-list.component.js ซึ่งใน component นี้จะ import todo.service มาใช้ และประกอบไปด้วย state และ function ดังนี้
state
- todo ใช้เก็บข้อมูล database ที่ได้มาจาก backend
- currentTodo ข้อมูลที่กำลังเลือก
- currentIndex ตำแหน่งของข้อมูลที่กำลังเลือกในอาร์เรย์
- searchTitle ข้อความในช่อง Search

function 
- componentDidMount เป็นฟังก์ชั่นพิเศษที่จะทำงานหลังจาก component ถูกสร้าง ซึ่งข้างในจะใช้งาน retrieveTodo ซึ่งจะอธิบายต่อไป
- onChangeSearchTitle ใช้รับ event การพิมพ์ข้อมูลแล้วเปลี่ยน state ของ searchTitle ไปตามข้อมูลที่รับเข้ามา (ใช้ใส่ข้อมูลในช่อง search)
- retrieveTodo เรียกใช้ getAll จาก todo.service หลังจากนั้นเปลี่ยน state ของ todo ให้เป็นไปตาม response ที่ได้มาจาก backend (ขอข้อมูลทั้งหมดจาก backend มานำเสนอบน frontend)
- removeAllTodo เรียกใช้ deleteAll จาก todo.service แล้วเรียกใช้ refreshList ซึ่งจะอธิบายต่อไป (ลบข้อมูล todolist ทั้งหมดออกไปจาก database)
- refreshList เรียกใช้ retrieveTodo แล้วเปลี่ยน state ของ currentTodo และ currentIndex เป็น null และ -1 ตามลำดับ (รีเฟรช ข้อมูลในส่วนของ list รายการ)
- setActiveTodo รับ parameter 2 ตัวเป็น Todo และ index ทำการเปลี่ยน state ของ currentTodo และ currentIndex เป็น Todo (เมื่อเรากดในแต่ละรายการใน list จะทำการระบุ รายการที่กำลังเลือก)
- searchTitle เรียกใช้ findByTitle จาก todo.service แล้วทำการ เปลี่ยน state ของ todo ให้ตรงจากที่ไปขอจาก findByTitle (เมื่อกดปุ่ม Search จะทำการค้นหาจาก database แล้วอัปเดทรายการให้ตรงตามที่ค้นหา)

ในส่วนของ render จะทำการสร้างช่อง Search สำหรับค้นหาด้วย Title โดยใน attribute onChange จะเรียกใช้ onChangeSearchTitle ต่อมาจะทำการสร้างปุ่มชื่อ Search สำหรับค้นหาข้อมูลจาก database ตาม Title ที่ใส่ไว้ในช่อง Search โดยใน onClick จะเรียกใช้ searchTitle ต่อมาสร้างช่องสำหรับแสดง todolist โดยมีหัวข้อชื่อ Todo List แล้วแสดง list ทุกตัวที่มีแล้วเมื่อคลิกบนแต่ละตัวใน list จะไปเรียกใช้ setActiveTodo ต่อมาแสดงปุ่ม Remove All แล้วเมื่อกดจะใช้งาน removeAllTodo ต่อมาสร้างตัวแสดงข้อมูลของ todo ที่เลือกซึ่ง ข้อมูลที่จะแสดงจะมี Title , Description และ Status และลิ้ง Edit เมื่อกดจะเปลี่ยนไปหน้า todo ของแต่ละอันที่เราเลือกอยู่

# Commit 10 : Create todo component

สร้าง component ไว้สำหรับเวลาที่เรากดเข้าไปใน edit ของ todo แต่ละอันโดยใน class ได้ทำการสร้าง constructor ไว้สำหรับรับค่า props ที่ส่งเข้ามา จากนั้นได้มีการสร้าง state ที่เก็บค่า currentTodo และ message ไว้โดยใน currentTodo มีการเก็บค่า id, title, description, และ finished(status) และใน class ยังมีการสร้างฟังก์ชัน  
- componentDidMount ที่เรียกใช้ฟังก์ชัน getTodo โดยมีการส่ง argument id ไป ซึ่งจะอธิบาย getTodo ต่อไป
- onChangeTitle มีการสร้างตัวแปร title ที่รับค่า event มาจากช่อง input title ซึ่งฟังก์ชันนี้จะทำการเปลี่ยนค่า state ของ title ตาม title ที่เรากรอกลงไปในช่อง input
- onChangeDescription ทำงานเหมือน onChangeTitle แต่เป็นการเปลี่ยน Description แทน
- getTodo เรียกใช้ method .get จาก TodoListDataService เพื่อเรียกค่าตาม id จาก database จากนั้นทำการ setState ตัว currentTodo ให้เป็นตาม data ของ id ที่ทำการดึงข้อมูลมาจาก database
- updateFinished สร้างตัวแปร data ไว้เก็บค่าของ currentTodo จากนั้นเรียกใช้ method .update เพื่ออัพเดตค่า boolean ของ finished ตามที่เรากด
- updateTodo ซึ่งเป็นฟังก์ชันสำหรับอัพเดตข้อมูลทุกอย่างใน currentTodo ตาม id ที่เราส่งมาเป็น argument
- deleteTodo ฟังก์ชันสำหรับลบข้อมูลใน database ของทั้ง row นั้นตาม argument ที่ส่งค่า id เข้าไป <br>

จากนั้นทำการ render ช่อง input 2 ตัว โดยมีค่า default จาก prevState, status, และ ปุ่มสำหรับ อัพเดตและลบข้อมูล

# Commit 11 : Create AddTodo component for adding data

import TodoListDataService มาใช้เพื่อให้เราสามารถส่ง http request ไป backend ได้ จากนั้นสร้าง Addtodo ที่เป็น Class component โดยก็จะมี ฟังค์ชันต่างๆมากมายซึ่งจะอธิบายต่อไป
และมีการประกาศ state โดยมี id, title ,description, finished, submitted โดย 4 ตัวแรกเป็นค่าที่เราจะตั้งเพื่อสร้างข้อมูลลง database ส่วน submitted เป็น state ไว้เช็คว่าส่งแล้วหรือไม่
- onChangeTitle เป็นฟังค์ชันที่รับ event ของ input แล้วไปเปลี่ยนตัว state ของ title ซึ่งเป็นการเปลี่ยนค่า title ตามที่เราพิมพ์ลงไปในช่อง input
- onChangeDescription เหมือน onChangeTitle แต่เป้นการเปลี่ยนค่า description แทน
- saveTodo ทำหน้าที่นำค่า title และ description จาก state มาแล้วส่งไปผ่าน TodoListDataService.create(data) เป็นการ request เพื่อสร้างข้อมูลลงใน database หลังจากนั้น
ก็จะเปลี่ยน state ทั้งหมดตามข้อมูลที่ backend ส่งกลับมา แล้ว เปลี่ยน summitted เป็น true ว่าส่งแล้ว ก็คือเป็นการบันทีกข้อมูลที่เรากรอกไปนั่นเอง
- newTodo เป็นการล้าง state ทั้งหมดกลับไปเป็นค่า default นั่นคือเป็นการ ล้าง input ที่เราใส่เพื่อให้เรากรอกใหม่

ต่อมาในส่วนของการ render เริ่มแรกจะมีการเช็คว่า state summitted เป็น true หรือ false ถ้า true จะแสดงผลเป็นปุ่ม ADD แล้วมี onClick เป็น ฟังค์ชัน newTodo เป็นการล้าง
state ส่งผลให้ summited กลายเป็น false ซึ่งจะเข้ากรณีต่อไปคือ เมื่อเป็น false จะสร้างแบบ form ให้พิมพ์ข้อมูล title และ description โดยแต่ละอันจะมี onChange เป้น 
ฟังค์ชัน onChangeTitle onChangeDescription ตามลำดับ และ สุดท้ายก็จะมีปุ่ม Submit โดยจะมี onClick เป็น saveTodo ก็คือบันทึกข้อมูลลงไป database นั่นเอง

# Commit 12 : Bugs fixed

แก้บัคในส่วนของ Database ที่ไม่ได้สร้างตารางให้อัตโนมัติ

