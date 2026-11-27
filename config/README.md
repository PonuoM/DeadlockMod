# Deadlock config (ภาพพอดี + FPS สูง)

ไฟล์ `gameinfo.gi` ในโฟลเดอร์นี้ = config ที่ optimize แล้ว
- ทำจากเกม buildid **26907316** (2026-11-26)
- ฐาน: Sqooky's maxfps config v2 — https://gamebanana.com/mods/656341
- License: GPL-3.0 ตามต้นฉบับของ Sqooky — ไฟล์นี้เป็นฉบับดัดแปลง (รายการที่แก้อยู่ในตารางด้านล่าง)
- ผลบนโน้ตบุ๊ก Ryzen AI 7 350 / Radeon 860M: Sandbox ~125 FPS, ตอนสู้ ~80–100 FPS

## วิธีลงที่เครื่องอื่น
1. **ปิดเกมให้หมดก่อน**
2. Steam → คลิกขวา Deadlock → Manage → **Browse local files**
3. เข้า `game\citadel\`
4. เปลี่ยนชื่อ `gameinfo.gi` เดิมเป็น `gameinfo.gi.bak_original` (เก็บไว้เผื่อย้อนกลับ)
5. ก๊อป `gameinfo.gi` จากโฟลเดอร์นี้ไปวางแทน
6. เปิดเกมผ่าน Steam (ไม่ต้องใช้ Mod Manager — มันอาจรีเซ็ตไฟล์นี้)

**ย้อนกลับ:** ลบ `gameinfo.gi` แล้วเปลี่ยนชื่อ `gameinfo.gi.bak_original` กลับเป็น `gameinfo.gi`

## ถ้าเกมอัปเดตแล้วไฟล์ถูกทับ / เปิดเกมไม่ขึ้น
ไฟล์นี้ผูกกับเวอร์ชันเกม ถ้าเกมอัปเดตใหญ่ อย่าวางไฟล์เก่าทับ ให้โหลด Sqooky's maxfps config ตัวใหม่ แล้วปรับตามรายการข้างล่างอีกครั้ง

## สิ่งที่ปรับจาก Sqooky's maxfps config v2
| ค่า | Sqooky | ของเรา | เหตุผล |
|---|---|---|---|
| `r_aspectratio` | 2.5 | ปิด (//) | FOV 100 = ได้เปรียบ |
| ส่วน "Camera Responsivity Tweaks" (`cam_idealdelta`, `cam_ideallag`, `citadel_camera_*`, `citadel_shoot_forward_offset`, `citadel_tightcamera_alternative`) | ปรับ | ปิด (//) | เปลี่ยนกล้อง ไม่เกี่ยว FPS |
| `cl_ragdoll_limit` | 0 | -1 | ไม่งั้นมองไม่เห็นอัลติ Doorman |
| `r_texture_stream_max_resolution` | 128 | 1024 | texture คมขึ้น |
| `r_texture_stream_mip_bias` | 3 | 1 | texture คมขึ้น |
| `r_texture_lod_scale` | 8 | 1 | texture คมขึ้น |
| `r_texturefilteringquality` | 0 | 3 | Aniso 4x |
| `r_texture_pool_size` | 256 | ปิด (//) | ให้เกมกำหนดเอง |
| `citadel_portrait_world_renderer_off` | true | ปิด (//) | ไม่งั้นโมเดลฮีโร่หายในหน้าโหลด/จบเกม MVP/ร้านค้า |
| `r_texture_stream_resolution_bias` | 0.01 | ปิด (//) | ให้เกมกำหนดเอง |
