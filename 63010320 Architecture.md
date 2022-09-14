### MatplotLib

MatplotLib เป็นไลบรารีที่ครอบคลุมสำหรับการสร้างการแสดงภาพแบบ static ภาพเคลื่อนไหว และ Python Matplotlib ทำให้เรื่องง่ายและยากสามารถทำได้

#### Architecture Styles

โครงสร้างของ MatplotLib ปะกอบด้วย 3 ขั้น

1. Backend layer: เตรียมการใช้งาน interface class 3 classes 1. figureCanvas 2. Renderer 3. Event
2. Artist layer: ประกอบด้วย 1 object เรียกว่า Artist FigureCanvas จาก backend layer เป็นกระดาษ Artist layer จะรู้วิธี Renderer เพื่อวาดบน canvas
3. Scripting layer: layer นี้มีน้ำหนักมากในการใช้จริง เพราะ layer นี้จะช่วยให้ความซับซ้อนของงานนั้นน้อยลง ส่วนใหญ่จึงใช้ในงานสำรวจต่างๆ

#### 3 Attribute scenario

1. Useability
   Source of stimulus: User
   Stimulus: ต้องการใช้ระบบอย่างมีประสิทธิภาพ
   Environment: Runtime
   Artifact: Systems
   Response: code ที่เข้าใจง่าย
   Response measure: ความพอใจของ User,ความรู้
2. Modifiablity
   Source of stimulus: ผู้ออกแบบและสร้าง Matplotlib
   Stimulus: เพิ่มฟังก์ชั่นการใช้งาน
   Environment: Runtime
   Artifact: Systems ทั้งหมด
   Response: การใช้งานของฟังก์ชั่นที่เพิ่มมา
   Response measure: การใช้งานง่ายของฟังก์ชั่นและเงินที่เสียไป
3. Performance
   Source of stimulus: User
   Stimulus: คำสั่งจาก User
   Environment: Normal mode
   Artifact: System
   Response: เวลาในการใข้งาน
   Response measure: เวลา

### Audacity

เป็นโปรแกรม OpenSource ที่ใช้ตัดต่อและบันทึกเสียงด้วยการใช้ Effect ต่างๆ ซึ่งมีอยู่มากมายและครบครัน เช่น Noise Reduction (ลดเสียง) Amplify (เพิ่มเสียง) ปรับระดับของเดซิเบล ฯลฯ ถึงแม้ว่า Audacity จะเป็นโปรแกรมที่มีเครื่องมือในการใช้งานเป็นจำนวนมาก แต่ก็เป็นโปรแกรมที่สามารถใช้ง่าย เพราะโปรแกรมนี้ได้แปลเป็นหลายๆภาษาทั่ว Audacity สามารถดาวน์โหลดฟรีได้ในทุกๆแพลตฟอร์ม ไม่ว่าจะเป็น Windows, Macs,

#### Architecture Styles

<img
  src="https://wiki.audacityteam.org/w/images/1/13/AudacityBlocks.png"
  alt="Alt text"
  style="display: inline-block; margin: 0 auto; max-width: 300px">
Audacity ใช้ libraries มากมาย library หลักสำหรับอินเทอร์เฟซผู้ใช้คือ wxWidgets ซึ่งเป็นแพลตฟอร์มข้ามแพลตฟอร์ม (Windows, Mac, Linux) แผนภาพด้านบนแสดงให้เห็นว่า Audacity จัดวางบนไลบรารีพื้นฐานได้อย่างไร
-BlockFile ใช้ระบบไฟล์ OS ผ่าน wxWidgets wxFile เพื่อจัดเตรียมวิธีการจัดเก็บเสียงในส่วนเล็กๆ ทำให้สามารถตัด วาง และจัดเรียงเสียงได้อย่างรวดเร็ว โดยไม่ต้องคัดลอกและแก้ไขไฟล์เสียงทั้งหมดสำหรับการเปลี่ยนแปลงเล็กๆ น้อยๆ แต่ละครั้ง
-ShuttleGui ใช้กล่องโต้ตอบ ปุ่ม และการควบคุมอื่นๆ ของ wxWidgets จัดระเบียบด้วยโครงสร้างเพิ่มเติมที่ช่วยลดโค้ดที่ซ้ำซ้อน ซึ่งส่วนใหญ่ใช้เพื่อ "ส่ง" ค่าจากที่หนึ่งไปยังอีกที่หนึ่ง ที่สำคัญที่สุดคือการตั้งค่าของผู้ใช้เช่นคุณภาพเสียงจะถูกเก็บไว้ในไฟล์ ข้อมูลต้องได้รับการถ่ายโอนจากไฟล์ไปยังตัวแปร จากตัวแปรไปยังวิดเจ็ตที่แสดงค่า และในทิศทางย้อนกลับด้วย
-การจัดการคำสั่งใน Audacity จะเชื่อมโยงการกดแป้นและรายการเมนูเข้ากับคำสั่งภายในภายใน Audacity มันใช้ wxMenu จาก wxWWidgets
แม้ว่า PortAudio จะไม่ได้เป็นส่วนหนึ่งของ wxWidgets แต่ก็มี 'การสะท้อน' ใน Audacity ด้วยเช่นกัน
-AudioIO จัดการกระบวนการย้ายเสียงระหว่างการ์ดเสียง หน่วยความจำ และฮาร์ดดิสก์ ให้นามธรรมเพิ่มเติมเหนือการจัดการการ์ดเสียงข้ามแพลตฟอร์มใน PortAudio

#### 3 Attribute scenario

1. Useability
   Source of stimulus: User
   Stimulus: ต้องการที่จะเข้าใจระบบ
   Environment: Runtime
   Artifact: GUI
   Response: ใช้งานง่าย
   Response measure: ความรู้ของ User
2. Modifiablity
   Source of stimulus: ผู้ออกแบบและสร้าง Audacity
   Stimulus: เพิ่มฟังก์ชั่นการใช้งาน
   Environment: Runtime
   Artifact: Systems ทั้งหมด
   Response: การใช้งานของฟังก์ชั่นที่เพิ่มมา
   Response measure: การใช้งานง่ายของฟังก์ชั่นและเงินที่เสียไป
3. Performance
   Source of stimulus: User
   Stimulus: คำสั่งจาก User
   Environment: Normal mode
   Artifact: System
   Response: เวลาในการใข้งาน
   Response measure: เวลาที่ใช้

### Kill Bill

Kill Bill เป็นแพลตฟอร์มการเรียกเก็บเงินและการชำระเงินแบบ opensource ที่ขับเคลื่อนหัวใจของธุรกิจ

#### Architecture Styles

<img
  src="https://killbill.io/wp-content/uploads/2014/01/kbcoreservices1.png?w=300"
  alt="Alt text"
  style="display: inline-block; margin: 0 auto; max-width: 300px">
-Catalog Service มีหน้าที่ให้ข้อมูลแค็ตตาล็อกที่เกี่ยวข้องกับผู้เช่าที่กำหนด บริการแค็ตตาล็อกเสนอ API เพื่อดึงข้อมูลผลิตภัณฑ์ กฎการจัดตำแหน่ง ราคา
-The entitlement service ให้สิทธิ์มี API สำหรับจัดการข้อมูล การให้สิทธิ์ทั้งหมดที่เกี่ยวข้องกับการสมัครรับข้อมูลที่กำหนด — สถานะ (เริ่มต้น หยุดชั่วคราว ดำเนินการต่อ หยุด ... ) ความเป็นเจ้าของ วันที่ต่างๆ ที่สถานะเปลี่ยน ระบบการให้สิทธิ์เสนอมุมมองที่แตกต่างกัน
-The invoice service มี API เพื่อดึงใบแจ้งหนี้ที่ผ่านมา ทำการปรับปรุง หรือแม้แต่เรียกใบแจ้งหนี้ในอนาคต
-The payment system มี API เพื่อดึงข้อมูลการชำระเงิน/การคืนเงินที่ผ่านมา หรือเพื่อเรียกการชำระเงิน/การคืนเงินใหม่
-The overdue system เป็นระบบทั่วไปที่ขับเคลื่อนผ่านการกำหนดค่า เพื่อดำเนินการเมื่อการชำระเงินล้มเหลวและผู้ใช้ไม่ได้ชำระเงิน สามารถใช้ชุดเฟสที่ซับซ้อนเพื่อค่อยๆ ยุติบริการ แจ้งให้ผู้ใช้ทราบ

#### 3 Attribute scenario

1. Useability
   Source of stimulus: User
   Stimulus: ต้องการที่จะเข้าใจระบบ
   Environment: Runtime
   Artifact: System
   Response: ใช้งานง่าย
   Response measure: ความรู้ของ User
2. Modifiablity
   Source of stimulus: ผู้ออกแบบและสร้าง Kill bill
   Stimulus: เพิ่มฟังก์ชั่นการใช้งาน
   Environment: Runtime
   Artifact: Systems ทั้งหมด
   Response: การใช้งานของฟังก์ชั่นที่เพิ่มมา
   Response measure: การใช้งานง่ายของฟังก์ชั่นและเงินที่เสียไป
3. Performance
   Source of stimulus: User
   Stimulus: คำสั่งจาก User
   Environment: Normal mode
   Artifact: System
   Response: การเก็บและชำระเงิน
   Response measure: เวลาที่ใช้
