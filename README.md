# **DARVIEW RENDER**
## คำอธิบาย
---------------------------------
**DARVIEW RENDER** - คือชุดพัฒนาซอฟต์แวร์ (SDK) สำหรับการใช้งานระบบการสื่อสารด้วยเสียงในภาษา Pawn สำหรับเซิร์ฟเวอร์ SA:MP

#### เวอร์ชันที่รองรับ
----------------------------------
* ไคลเอนต์ : SA:MP 0.3.7 (R1, R3)
* เซิร์ฟเวอร์ : SA:MP 0.3.7 (R2)

## คุณสมบัติ
---------------------------------
* ควบคุมการส่งผ่านเสียง
* การควบคุมไมโครโฟนของผู้เล่น
* เชื่อมโยง stream ของเสียงกับวัตถุในเกม
* และคุณสมบัติอื่น ๆ อีกมากมาย ...

## การติดตั้ง
---------------------------------
เพื่อให้ปลั๊กอินทำงานได้ จะต้องติดตั้งโดยผู้เล่นและบนเซิร์ฟเวอร์ มีส่วนไคลเอนต์และเซิร์ฟเวอร์ของปลั๊กอินสำหรับสิ่งนี้

#### สำหรับผู้เล่น
---------------------------------
ผู้เล่นสามารถเข้าถึงตัวเลือกการติดตั้ง 2 แบบ: อัตโนมัติ (ผ่านตัวติดตั้ง) และด้วยตนเอง (ผ่านไฟล์เก็บถาวร)

##### ติดตั้งอัตโนมัติ
---------------------------------
1. หากต้องการดาวน์โหลดตัวติดตั้ง, ไปที่ [หน้า `การเผยแพร่`](https://github.com/darviewyrl/darrender/releases) และเลือกเวอร์ชันของปลั๊กอินที่ต้องการ
2. หลังจากดาวน์โหลดแล้ว ให้เปิดตัวติดตั้ง โปรแกรมติดตั้งจะค้นหาโฟลเดอร์ GTA San Andreas ของคุณโดยอัตโนมัติ
3. หากไดเร็กทอรีถูกต้อง คลิก "ถัดไป" และรอให้การติดตั้งเสร็จสิ้น หลังจากนั้นคลิก "เสร็จสิ้น" เพื่อปิดตัวติดตั้ง

##### ติดตั้งด้วยตนเอง
---------------------------------
1. ไปที่ [หน้า `การเผยแพร่`](https://github.com/darviewyrl/darrender/releases) และดาวน์โหลดไฟล์เก็บถาวรด้วยเวอร์ชันไคลเอนต์ที่ต้องการ
2. แยกไฟล์เก็บถาวรไปยังโฟลเดอร์ GTA San Andreas ของคุณด้วยการแทนที่ไฟล์

#### สำหรับนักพัฒนา
---------------------------------
1. ดาวน์โหลดจาก [หน้า `การเผยแพร่`](https://github.com/darviewyrl/darrender/releases) ปลั๊กอินเวอร์ชันที่ต้องการสำหรับแพลตฟอร์มของคุณ
2. แตกไฟล์เก็บถาวรไปยังไดเร็กทอรีของเซิร์ฟเวอร์
3. เพิ่มลงในไฟล์การกำหนดค่าเซิร์ฟเวอร์ *server.cfg* บรรทัด *"plugins darrender"* สำหรับ *Win32* และ *"plugins darrender.so"* สำหรับ *Linux x86*. **(หากคุณมีปลั๊กอิน Pawn.RakNet อย่าลืมวาง Darview Render ไว้ข้างหลัง)**

## การใช้งาน
---------------------------------
หากต้องการเริ่มต้นใช้งานปลั๊กอิน โปรดอ่านเอกสารประกอบที่มาพร้อมกับฝั่งเซิร์ฟเวอร์ ในการดำเนินการนี้ ให้เปิดไฟล์ *darrender.chm* โดยใช้ข้อมูลอ้างอิงของ Windows **(หากเอกสารไม่เปิดขึ้นมา ให้คลิกขวาที่ไฟล์เอกสาร จากนั้นคลิก Properties -> Unblock -> OK)**

หากต้องการเริ่มใช้ฟังก์ชันปลั๊กอิน ให้รวมไฟล์ส่วนหัวด้วย:
```c
#include <darrender>
```

#### การอ้างอิงฉบับย่อ
---------------------------------
คุณจำเป็นต้องรู้ว่าปลั๊กอินใช้ประเภทของตัวเองและระบบคงที่ แม้ว่านี่จะเป็นเพียงส่วนสรุปของ Pawn ประเภทพื้นฐาน แต่ก็ช่วยนำทางประเภทต่างๆ ของปลั๊กอินได้ และไม่ทำให้ pointers สับสน

หากต้องการเปลี่ยนเส้นทางการรับส่งข้อมูลเสียงจากผู้เล่น A ไปยังผู้เล่น B คุณต้องสร้างสตรีมเสียง (โดยใช้ **DrCreateStream**), แล้วต่อเข้ากับช่องลำโพงของผู้เล่น A (โดยใช้ **DrAttachStream**), จากนั้นแนบผู้เล่น B เข้ากับสตรีมเสียง (โดยใช้ **DrAttachListener**) เสร็จแล้ว, ตอนนี้เมื่อไมโครโฟนของผู้เล่น A ถูกเปิดใช้งาน (เช่น ด้วยฟังก์ชัน **DrPlay**), การรับส่งข้อมูลเสียงของเขาจะถูกส่งและฟังโดยผู้เล่น B

สตรีมเสียงมีประโยชน์มาก เห็นได้จากใช้ตัวอย่างของ Discord:
* Stream คือ อะนาล็อกของห้อง (หรือช่อง)
* Speakers คือ ผู้เข้าร่วมในห้องโดยปิดลำโพงแต่เปิดไมโครโฟนอยู่
* Listeners คือ ผู้เข้าร่วมในห้องโดยปิดไมโครโฟนแต่เปิดลำโพง

ผู้เล่นสามารถเป็นทั้งผู้พูดและผู้ฟังได้ในเวลาเดียวกัน ในกรณีนี้, การรับส่งข้อมูลเสียงของผู้เล่นจะไม่ถูกส่งต่อไปยังเขา

#### ตัวอย่าง
---------------------------------
ลองมาดูคุณสมบัติบางอย่างของปลั๊กอินพร้อมตัวอย่างที่ใช้งานได้จริง ด้านล่างนี้ เราจะสร้างเซิร์ฟเวอร์ที่จะเชื่อมโยงผู้เล่นที่เชื่อมต่อทั้งหมดเข้ากับสตรีมทั่วโลก และยังสร้างสตรีมท้องถิ่นสำหรับผู้เล่นแต่ละคนด้วย ดังนั้น ผู้เล่นจะสามารถสื่อสารผ่านการแชททั่วโลก (ได้ยินเท่ากันทุกจุดบนแผนที่) และแชทท้องถิ่น (ได้ยินเฉพาะผู้เล่นที่อยู่ใกล้กันเท่านั้น)
```cpp
#include <darrender>

#define GLOBAL_CHANNEL 0
#define  LOCAL_CHANNEL 1

new DR_UINT:gstream = DR_NONE;
new DR_UINT:lstream[MAX_PLAYERS] = { DR_NONE, ... };

public OnPlayerConnect(playerid)
{
    if (DrGetVersion(playerid) == 0) // Checking for plugin availability
    {
        SendClientMessage(playerid, -1, "Failed to find plugin.");
    }
    else if (DrHasMicro(playerid) == DR_FALSE) // Checking for microphone availability
    {
        SendClientMessage(playerid, -1, "Failed to find microphone.");
    }
    else
    {
        if (gstream != DR_NONE)
        {
            DrSetKey(playerid, 0x5A, GLOBAL_CHANNEL); // Z key
            DrAttachStream(playerid, gstream, GLOBAL_CHANNEL);
            DrAttachListener(gstream, playerid);
            DrSetIcon(gstream, "speaker");

            SendClientMessage(playerid, -1, "Press Z to talk to global chat.");
        }
        if ((lstream[playerid] = DrCreateStream(40.0)) != DR_NONE)
        {
            DrSetKey(playerid, 0x42, LOCAL_CHANNEL); // B key
            DrAttachStream(playerid, lstream[playerid], LOCAL_CHANNEL);
            DrSetTarget(lstream[playerid], DrMakePlayer(playerid));
            DrSetIcon(lstream[playerid], "speaker");

            SendClientMessage(playerid, -1, "Press B to talk to local chat.");
        }
    }
}

public OnPlayerDisconnect(playerid, reason)
{
    // Removing the player's local stream after disconnecting
    if (lstream[playerid] != DR_NONE)
    {
        DrDeleteStream(lstream[playerid]);
        lstream[playerid] = DR_NONE;
    }
}

public OnGameModeInit()
{
    // Uncomment the line to enable debug mode
    // DrEnableDebug();

    gstream = DrCreateStream();
}

public OnGameModeExit()
{
    if (gstream != DR_NONE)
    {
        DrDeleteStream(gstream);
        gstream = DR_NONE;
    }
}
```

## การคอมไพล์
---------------------------------
ปลั๊กอินคอมไพล์สำหรับแพลตฟอร์ม *Win32* และ *Linux x86*
ไฟล์ที่คอมไพล์สำเร็จจะอยู่ในไดเร็กทอรี *darrender/binaries*

ด้านล่างนี้เป็นคำแนะนำเพิ่มเติม:

โคลนพื้นที่เก็บข้อมูลลงในคอมพิวเตอร์ของคุณและไปที่ไดเร็กทอรีปลั๊กอิน:
```sh
git clone https://github.com/darviewyrl/darrender.git
cd darrender
```

### Windows (ไคลเอนต์/เซิร์ฟเวอร์)
---------------------------------
หากต้องการคอมไพล์ฝั่งไคลเอ็นต์ของปลั๊กอิน คุณต้องมี *DirectX SDK* ตามค่าเริ่มต้น ส่วนของไคลเอ็นต์จะถูกคอมไพล์สำหรับเวอร์ชัน **SA: MP 0.3.7 (R1)** แต่คุณยังสามารถบอกคอมไพเลอร์ถึงเวอร์ชันสำหรับบิลด์ได้อย่างชัดเจนโดยใช้มาโคร **SAMP_R1** และ **SAMP_R3** ในการสร้างไคลเอนต์และเซิร์ฟเวอร์ส่วนของปลั๊กอินสำหรับแพลตฟอร์ม *Win32* ให้เปิดโปรเจ็กต์ *darrender.sln* ใน Visual Studio 2019 (หรือสูงกว่า) และคอมไพล์:
> Build -> Build Solution (F7)

### Linux (Ubuntu 20.04) (เซิร์ฟเวอร์)
---------------------------------
ตรวจสอบให้แน่ใจว่าคุณได้ติดตั้งการอ้างอิงทั้งหมดแล้ว:
```sh
sudo apt install make gcc g++ gcc-multilib g++-multilib
```
หากต้องการสร้าง **control-server** สำหรับแพลตฟอร์ม *Linux x86* ให้ทำตามคำแนะนำเหล่านี้:
```sh
cd control
make
cd ..
```
หากต้องการสร้าง **voice-server** สำหรับแพลตฟอร์ม *Linux x86* ให้ทำตามคำแนะนำเหล่านี้:
```sh
cd voice
make
cd ..
```
