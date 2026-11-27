# Deadlock Modding

โปรเจกต์ส่วนตัวสำหรับทำม็อดเปลี่ยนตัวละคร/สกินในเกม Deadlock (Valve, Source 2) — ไม่เกี่ยวกับงาน HR

## ที่คุยกันไว้แล้ว (ย้ายมาจากแชทในโปรเจกต์ hr-mobile-connect, 2026-11-24)

ตัวอย่างม็อดที่เห็น: Jacket (Billy Overhaul) — https://deadlocker.net/mod/jacket-billy-overhaul-mod_1764283298192 (ไฟล์ `.vpk`)

### ลงม็อด
- ง่ายสุด: Deadlock Mod Manager (deadlockmods.app)
- ลงเอง: Steam → Properties → Installed Files → Browse
  1. แก้ `game/citadel/gameinfo.gi` ส่วน FileSystem ตาม https://deadlocker.net/install-guide
  2. สร้าง `game/citadel/addons` แล้ววาง `.vpk` ตั้งชื่อ `pak01_dir.vpk`, `pak02_dir.vpk`, … (ชนกันให้สลับเลข)
- ม็อดเห็นแค่เครื่องเรา · ทำแค่ cosmetic ห้ามได้เปรียบ (เสี่ยงแบน) · อัปเดตเกมแล้วม็อดมักพัง

### ทำม็อดเอง
1. Source 2 Viewer (VRF) เปิด `pak01_dir.vpk` ของเกม ดึงโมเดล/texture ตัวละคร
2. แก้ texture (Photoshop/GIMP) หรือโมเดล (Blender)
3. คอมไพล์ด้วย CS2 Workshop Tools (เอนจินเดียวกัน)
4. แพ็กเป็น `.vpk` วางใน addons

แหล่งคู่มือ: GameBanana หมวด Deadlock → Tutorials, Discord กลุ่มม็อด Deadlock

## ขั้นต่อไป
- เริ่มจากเปลี่ยนสี texture ของตัวละครหนึ่งตัวก่อน (ยังไม่ได้เลือกตัว)
- เช็ก 2026-11-26: ติดตั้ง Steam + Deadlock แล้ว ที่ `C:\Program Files (x86)\Steam\steamapps\common\Deadlock` (~39 GB) · ยังไม่มี Blender/Source 2 Viewer
- 2026-11-26 ลง Potato Lock v1.1.3 (Classic, ไม่ใส่ Heroes) แบบ manual แล้ว: ใน `gameinfo.gi` SearchPaths ใช้ชุด `Game citadel/addons` / `Mod citadel` / `Write citadel` / `Game citadel` / `Write core` / `Mod core` / `Game core` (ถ้าใส่แค่ `Game citadel/addons` อย่างเดียว เกมขึ้น FATAL ERROR user_keys_default เพราะ addons กลายเป็น MOD path) (สำรองเดิมไว้ที่ `gameinfo.gi.bak_original`) + วาง `addons/pak31_dir.vpk` · ม็อดตัวเองให้ใช้เลข pak อื่นที่ไม่ใช่ 31 · เกมอัปเดตแล้ว Steam อาจเขียนทับ gameinfo.gi ต้องเพิ่มบรรทัดใหม่
- 2026-11-26 (บ่าย): พบว่า gameinfo.gi ถูกคืนเป็นของเดิม (ไม่ทราบสาเหตุ, buildid ไม่เปลี่ยน 26907316) → Potato Lock ไม่เคยโหลดจริง · เปลี่ยนไปใช้ **Sqooky's maxfps config v2** (gamebanana.com/mods/656341) แทนทั้งไฟล์ gameinfo.gi (มี addons support ในตัว) โดยปิด `r_aspectratio` (FOV 100 = ได้เปรียบ) + ส่วน "Camera Responsivity Tweaks" และแก้ `cl_ragdoll_limit` เป็น -1 (ไม่งั้นมองไม่เห็นอัลติ Doorman) · สำรอง: `gameinfo.gi.bak_original` (ของแท้), `gameinfo.gi.bak_addons_only` · เปิดเกมได้ปกติ ไฟล์ไม่ถูกทับตอนเปิด
- ผล Potato Lock + maxfps config: ~90–100 FPS (Sandbox) แต่ภาพจืด → ถอด Potato Lock ไปไว้ `addons_disabled/pak31_dir_potatolock_classic.vpk` (กลับมาใช้ได้ด้วยการย้ายคืน `addons/pak31_dir.vpk`)
- ไม่มี Potato Lock: Avg ~112 FPS (Sandbox, ~80 ตอนสู้) ภาพสวยขึ้นมาก → texture ไม่ใช่ตัวทำกระตุก
- ปรับ texture ใน config: `r_texture_stream_max_resolution` 128→1024, `r_texture_stream_mip_bias` 3→1, `r_texture_lod_scale` 8→1, `r_texturefilteringquality` 0→3, ปิด `r_texture_pool_size` / `r_texture_stream_resolution_bias` · สำรองก่อนปรับ: `gameinfo.gi.bak_maxfps_sqooky` · ผล (มุมเดิม Sandbox): Avg 112→125 FPS, เฟรมช้าสุด 10.8→9.4 ms, ป้ายอ่านออก → **ใช้ค่านี้เป็นค่าหลัก** · ถ้าจะปรับต่อ: ลองเปิดเงาระดับต่ำ (กิน FPS มากสุด)
- สำเนา config ที่ใช้อยู่ + วิธีลง + รายการที่ปรับ: [config/](config/) (`gameinfo.gi`, `README.md`) — ใช้ลงเครื่องที่บ้านด้วย
- เกมเปิดอยู่จะล็อกทั้ง `gameinfo.gi` และ vpk ใน addons → ต้องให้ผู้ใช้ออกเกมก่อนแก้
- เกม ClientVersion 6868 (game/citadel/steam.inf) · ผู้ใช้ตั้งเกมเป็นภาษาไทย → หน้า Builds ในเกมโชว์แต่ build ภาษาไทย (คุณภาพต่ำ)
- 2026-11-27: เกมอัปเดตเป็น ClientVersion 6871 (config ยังอยู่ครบ) · **ลง Builds+ แล้ว** เป็น `addons/pak02_dir.vpk` (เว้น pak01 ไว้ให้ม็อดตัวเอง)
- 2026-11-27: ฮีโร่หายในหน้าโหลด/MVP → สาเหตุ `citadel_portrait_world_renderer_off "true"` ใน config → ปิดบรรทัดนี้แล้ว (สำรอง `gameinfo.gi.bak_before_portrait`) · ถ้าฮีโร่ในหน้าพวกนี้ดูมืด แก้ `lb_enable_dynamic_lights` เป็น true (แต่เปิดไฟ dynamic ทั้งเกม กิน FPS)
- วิเคราะห์ 2026-11-26:
  - **Builds+** (gamebanana 736782, `BuildsPlus_dir.vpk`): แก้ `citadel_popup_build_browser` + JS, จัด build ทั่วโลกตามจำนวนแมตช์จริง/แรงค์ Eternus, มีข้อมูลฝังมา (19 พ.ย.) + ดึงสดผ่าน HTML panel ไป pawnxx.github.io และเซิร์ฟเวอร์ IP 179.253.78.167 (sslip.io) ส่ง hero id/sort/lang
  - **Item Assistant** (694954, `pak05_dir.vpk`): override `hud_health` layout + JS recommender, ไม่มี network; ข้อมูลจาก client 6635 (เก่า) ขาดฮีโร่ id 84–88; อ่านชื่อไอเทม/ฮีโร่จากข้อความบนจอเป็นภาษาอังกฤษ → น่าจะใช้กับเกมภาษาไทยไม่ได้; license CC BY-NC-ND (แก้ใช้เองได้ เผยแพร่ต้องขอ)
  - สองม็อดไม่มีไฟล์ซ้ำกัน
- สเปกเครื่อง: Ryzen AI 7 350 + Radeon 860M (การ์ดจอออนบอร์ด), RAM 32 GB → ใช้ม็อด Potato Lock (gamebanana.com/mods/692484) ช่วยลด texture/VRAM
