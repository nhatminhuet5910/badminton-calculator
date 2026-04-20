# UI Redesign: Theme Giỗ Tổ Hùng Vương 10/3

## Overview

Redesign giao dien app tinh tien cau long "CLB DOT TIEN CAU" voi theme mung Gio To Hung Vuong. Giu nguyen toan bo tinh nang va JavaScript logic, chi thay doi CSS styling, them SVG decorative elements va CSS animations.

**Approach:** Pure CSS — tat ca texture, hoa van, animation deu bang CSS thuan + SVG inline. Khong them file anh hay thu vien ngoai.

## 1. Bang mau (Color Palette)

| Token | Hex | Muc dich |
|-------|-----|----------|
| `--primary` | `#8B0000` | Do son — header, button, text quan trong |
| `--primary-light` | `#C41E3A` | Do nhat — hover states, accent |
| `--gold` | `#D4A017` | Vang dong — vien, divider, highlight |
| `--gold-light` | `#F0D060` | Glow effect, badge |
| `--brown` | `#5D3A1A` | Nau go — text phu, shadow |
| `--cream` | `#FFF8E7` | Kem giay do — nen card |
| `--male` | `#0984e3` | Xanh — QR nam (giu nguyen) |
| `--female` | `#e84393` | Hong — QR nu (giu nguyen) |

## 2. Background & Texture

### Background ngoai (go truyen thong)
- CSS gradient pattern mo phong van go nau dam
- `repeating-linear-gradient` ket hop nhieu layer voi `#3E2410`, `#5D3A1A`, `#4A2E14`
- Them subtle noise texture bang CSS `radial-gradient` lap

### Card nen (giay do)
- Nen `#FFF8E7` voi gradient nhe tao vet loang tu nhien
- Border: `2px solid var(--gold)` + `border-radius: 12px`
- Box shadow am: `0 4px 20px rgba(93, 58, 26, 0.3)`

## 3. Banner & Header

### Banner mung le
- Dong chu: "Mung Gio To Hung Vuong 10/3" voi hoa tiet 2 ben
- Font: Pangolin, mau `--gold`, `font-size: 14px`
- Hai ben co hoa van may co SVG inline (nho, doi xung)
- Background: `--primary` voi gradient nhe, `border-radius: 8px 8px 0 0`
- Padding nho gon

### Title chinh
- Giu nguyen text "CLB DOT TIEN CAU" + subtitle
- Doi mau sang `--gold` tren nen `--primary`
- Hai ben title co icon rong/phuong SVG nho doi xung
- Text-shadow vang kim nhe: `0 0 10px rgba(212, 160, 23, 0.3)`

### Divider duoi header
- SVG hoa van trong dong Dong Son lap lai, cao ~20px
- Mau `--gold` tren nen trong suot

## 4. Form & Input Elements

### Input fields
- Background: `#FFF8E7` (kem giay do)
- Border: `1px solid var(--gold)`
- Focus state: `box-shadow: 0 0 8px rgba(212, 160, 23, 0.4)` + border dam hon
- Label: mau `--primary`, font-weight 600

### Buttons
- Primary button (Tinh tien): `background: linear-gradient(135deg, #8B0000, #6B1010)`, text `--gold`
- Hover: sang hon + `box-shadow: 0 0 12px rgba(212, 160, 23, 0.4)` (glow vang kim)
- Border: `1px solid var(--gold)`

### Switch toggles (Auto/Manual QR)
- Active state: background `--primary`
- Inactive: background nau nhat `#CD853F`

### Section dividers
- Hoa van song nuoc/may co SVG mong, `opacity: 0.4`, cao ~10px
- Mau `--gold`

### Emoji
- Giu nguyen emoji hien tai (🧧🏮👦👧) — da hop vibe
- 🔥 thay bang 🏛️ (Den Hung) cho hop theme

## 5. Hoa tiet trang tri (Ornaments)

### Hoa van trong dong Dong Son
- Dung lam vien trang tri, divider giua cac section
- SVG inline, pattern lap lai

### May co / Song nuoc
- Vien mem mai, trang tri goc card
- 4 goc card chinh co SVG may co cuon, `position: absolute`
- Mau `--gold` voi `opacity: 0.2`, ~40x40px moi goc

### Hoa sen
- 1 bong sen SVG nho (~30px) dat giua, giua banner va title
- Mau `--primary` + `--gold`

### Rong / Phuong
- SVG nho doi xung 2 ben tieu de chinh

### Banh chung / Banh giay
- Icon nho co the dung thay the mot so emoji

## 6. Animations

### Canh hoa sen bay
- 8-10 phan tu `<div>` absolute positioned
- CSS `clip-path` tao hinh canh hoa sen
- Mau: hong nhat `rgba(200, 100, 120, 0.3)`
- `@keyframes petalFall`: roi tu tren xuong + xoay nhe + lac ngang (sine wave translateX)
- Duration: 8-15s, stagger, `infinite`
- `pointer-events: none` + `z-index: 0`

### Khoi huong tram
- 3-4 dai khoi mong tu goc duoi cung
- `border-radius: 50%` + `filter: blur(20px)`
- Mau: trang duc `rgba(255, 255, 255, 0.08)`
- `@keyframes smokeRise`: bay len cham + scale lon dan + fade out
- Duration: 10-20s, subtle
- `pointer-events: none` + `z-index: 0`

### Performance
- `will-change: transform` cho animation elements
- `@media (prefers-reduced-motion: reduce)` — tat animation cho nguoi nhay cam
- Tong cong ~12-14 phan tu animation

## 7. Invoice / Hoa don

- Giu layout hoa don hien tai (dashed border, monospace font)
- Doi border color sang `--gold`
- Con dau "DA THU TIEN" doi sang `--primary` (do son) — hop voi dau trien
- Them hoa van trong dong nho lam watermark mo o goc, `opacity: 0.1`
- QR code nam/nu giu nguyen mau xanh/hong

## 8. Nhung thu KHONG thay doi

- Toan bo JavaScript logic (tinh tien, QR, localStorage, html2canvas)
- Cau truc HTML semantic (cac section, id, class name)
- Flow tinh nang: input -> tinh toan -> ket qua -> QR -> capture
- VietQR API integration
- Responsive layout (max-width 450px)
- Font Roboto cho body text
- Mau xanh/hong cho nam/nu QR

## 9. Tech constraints

- Single-file HTML — giu nguyen kien truc hien tai
- Pure CSS + SVG inline — khong them file ngoai
- Khong them thu vien JS moi
- Compatible voi html2canvas (animation elements phai co `pointer-events: none` va khong anh huong capture)
