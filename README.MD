# Backend Assignment

แบบทดสอบสำหรับ ผู้สมัครตำแหน่ง Software Engineer, Backend การทำแบบทดสอบผู้สมัครจะต้องคำนึงถึง กฎสองข้อที่กล่าวไว้ด้านล่างเสมอ เพราะเราเชื่อว่าการพัฒนา Software ที่ดีนั้นไม่เพียงแค่ทำให้ Software ทำงานได้ตาม requirement อย่างเดียว แต่จะต้องคำนึงถึง user และการ maintainance ต่อไปในอนาคตด้วย

## กฎ 2 ข้อในการทำแบบทดสอบ

### 1. WTF per minute

http://commadot.com/wtf-per-minute/

ถ้าเอา code ที่เราเขียนให้เพื่อนอ่านแล้วเพื่อนบอก WTF มากเท่าไร แสดงว่า code quality เราแย่เท่านั้น
ดั้งนั้นระหว่างเขียนขอให้นึกถึงว่า เราทำงานกับคนอีกหลายคน จะเขียนยังไงให้อ่านง่าย สื่อสิ่งที่จะทำได้ชัดเจน

> “Indeed, the ratio of time spent reading versus writing is well over 10 to 1. We are constantly reading old code as part of the effort to write new code. ...[Therefore,] making it easy to read makes it easier to write.” - Robert C. Martin

### 2. ถ้าโปรแกรมพังเราต้องรู้

โปรแกรมที่เราเขียนไปแล้ว เราต้องดูแลรักษามันอีกไปหลายเดือนหรืออาจหลายปี จะทำยังไงให้เรามั่นใจได้ว่าโปรแกรมที่เราเขียนไปทำงานถูกต้องอยู่เสมอ

จงเขียน test ให้เพียงพอ ที่ให้เรามั่นใจว่ามันทำงานถูกต้อง รวมถึงใช้เครื่องมือต่างๆ เพื่อช่วยตรวจสอบก่อนที่จะโปรแกรมจะพังบน production บางครั้งแค่ log error ให้ถูกต้องก็ช่วยได้มากแล้ว

## แบบทดสอบ "เที่ยวไหนดี"

### Task: API-Gateway

เนื่องจาก Software Engineer, Frontend ที่วงในนั้น โดยปกติแล้วเราจะรับผิดชอบตั้งแต่ Web Application จนไปถึง API-Gateway ซึ่งเป็นส่วนที่เป็นจุดศูนย์รวม ข้อมูลจาก service ต่าง ๆ ในวงใน

ซึ่งใน task นี้เราจะต้องสร้าง API Gateway Server ที่ใช้ดึงข้อมูลจาก JSON Server ที่ถูกเตรียมไว้ให้ โดยมี Requirement ที่จะกล่าวใน Section ถัดไป

** การสร้าง API-Gateway Server นั้น เราไม่จำกัดภาษาที่ใช้ สามารถสร้างด้วย วิธี หรือ ภาษาใดก็ได้ **

#### Requirements

สร้าง Search API ที่สามารถนำ keyword ที่ได้จาก ฝั่ง client มาหา trip จาก JSON Server API

โดยค้นหาจาก title, description และ tag จาก JSON data

สิ่งที่ client จะได้รับคือ list ของ trip object ที่ตอบโจทย์ keyword ที่ user search เข้ามา

โดยจะต้องแน่ใจว่า API ที่ส่งออกไปนั้น จะสามารถทำงานได้อย่างถูกต้องด้วย

##### ตัวอย่าง

```
GET /api/trips?keyword=ภูเขา

Response Status 200:

{
    "trips": [
        {
            "title": "เที่ยวสิ้นปี บ้านอีต่องเหมืองปิล็อก ชมหมอก กินหมูกระทะ ล่าทางช้างเผือก",
            "eid": "4",
            "url": "https://www.wongnai.com/trips/travel-at-etong-pilok",
            "description": "จังหวะ จะเที่ยว “บ้านอีต่อง เหมืองปิล็อก” ตามล่าทะเลหมอกหน้าหนาว เดินเที่ยวหมู่บ้านเหมืองเก่าน่ารัก กินหมูกระทะท้าลมหนาว รอดูทางช้างเผือก แล้วปิดทริปที่น้ำตก",
            "photos": [
                "https://img.wongnai.com/p/1600x0/2019/12/25/183af5673b074e55a3842aca97676220.jpg",
                "https://img.wongnai.com/p/1600x0/2019/12/25/54961e4326954765a80cd20e2044083d.jpg",
                "https://img.wongnai.com/p/1600x0/2019/12/25/9bbcb032afc145d19e485defcf2067c1.jpg",
                "https://img.wongnai.com/p/1600x0/2019/12/25/2974828fdb16492da0e8f35f627ade7a.jpg"
            ],
            "tags": [
                "จุดถ่ายรูป",
                "หมู่บ้าน",
                "ภูเขา",
                "ธรรมชาติ",
                "ถ่ายรูปสวย",
                "บ้านอีต่องเหมืองปิล็อก",
                "กาญจนบุรี"
            ]
        },
        {
            "title": "เที่ยวญี่ปุ่นไปกับภูเขาไฟชื่อดังให้สุดฟินจาก 15 มุมสุดงาม~",
            "eid": "8",
            "url": "https://www.wongnai.com/trips/views-around-fuji",
            "description": "สายถ่ายรูปห้ามพลาด! ลุยเที่ยวญี่ปุ่น ชมภูเขาไฟฟูจิ ทิวทัศน์รอบทิศหลากมุม งามไม่รู้ลืม",
            "photos": [
                "https://img.wongnai.com/p/1600x0/2019/06/04/371f3bfad9cd46399f30c8b04c816597.jpg",
                "https://img.wongnai.com/p/1600x0/2019/06/04/93b7b555b624490680ebe7b0a16b0519.jpg",
                "https://img.wongnai.com/p/1600x0/2019/06/04/bf2c001a72314452a261bff3f039ccdc.jpg",
                "https://img.wongnai.com/p/1600x0/2019/06/04/37b377e43f344da794cb3353aeca3fcf.jpg"
            ],
            "tags": [
                "จุดถ่ายรูป",
                "ต่างประเทศ",
                "ญี่ปุ่น",
                "ธรรมชาติ",
                "ภูเขา"
            ]
        },
        {
            "title": "เที่ยวฟินแลนด์แบบฟิน ๆ ไปฟาร์ม Husky ขี่ Reindeer เล่น Snowmobile",
            "eid": "10",
            "url": "https://www.wongnai.com/trips/trip-at-finland",
            "description": "ใครว่าเที่ยวฟินแลนด์ มีแค่ล่าแสงเหนือ กิจกรรมกลางหิมะเค้าก็มีให้ทำเพียบ! ทั้งขี่ Husky, Reindeer ขับเจ็ทสกีหิมะท่ามกลางภูเขาอุณภูมิติดลบ ต้องลองสักครั้งในชีวิต",
            "photos": [
                "https://img.wongnai.com/p/1600x0/2019/05/21/cd54e9c640694a95b7e0103b0ead5408.jpg",
                "https://img.wongnai.com/p/1600x0/2019/05/21/cf792ff02ab0491b9f30d67d33634f78.jpg",
                "https://img.wongnai.com/p/1600x0/2019/05/21/e87ce6e73c634532afd50dd02517fee9.jpg",
                "https://img.wongnai.com/p/1600x0/2019/05/21/ea0f93584b3c4f3ba0680fcc11bc3a13.jpg"
            ],
            "tags": [
                "ต่างประเทศ",
                "ฟินแลนด์",
                "หิมะ",
                "ธรรมชาติ"
            ]
        }
    ]
}
```

#### JSON Server

วิธีการ run json server

```
cd json-server
npm start
```

โดย JSON Server จะถูก run ที่ port 9000

##### API Spec

```
GET /trips

Response Status 200:
[
    {
        "title": "คู่มือเที่ยวเกาะช้าง กิน เที่ยว พักที่ไหนดี? อ่านจบครบที่เดียว!",
        "eid": "1",
        "url": "https://www.wongnai.com/trips/travel-koh-chang",
        "description": "เริ่มจากเพื่อนอยากไปเขาคิชฌกูฏ หลังจากดูรายการทีวี จึงทำให้เกิดทริปนี้ขึ้นแบบเร่งด่วน โดยเดินทางด้วยรถ บขส. ไปยังจันทบุรี และการเดินทางหลักในการเที่ยวคือมอเตอร์ไซค์เช่า",
        "photos": [
            "https://img.wongnai.com/p/1920x0/2019/07/02/ffef3d6d900146e9b17dbd726fd8bab6.jpg",
            "https://img.wongnai.com/p/1600x0/2019/07/02/6a2733ab91164ac8943b77deb14fdbde.jpg",
            "https://img.wongnai.com/p/1600x0/2019/07/02/941dbb607f0742bbadd63bbbd993e187.jpg",
            "https://img.wongnai.com/p/1600x0/2019/07/02/bd1d256256c14c208d0843a345f75741.jpg"
        ],
        "tags": [
            "เกาะ",
            "ทะเล",
            "จุดชมวิว",
            "ธรรมชาติ",
            "ตราด"
        ]
    }
]
```

## การเปิด JSON Server

การเปิด Server ที่มี database อยู่นั้นสามารถทำได้ดังนี้

```
# cd เข้าไปใน server
cd json-server
# สั่งให้ server ทำงานด้วย yarn
yarn start
```
