# 🔌 Power Outlet Monitor – LED Only (Arduino Nano)

En enkel och pålitlig **strömövervakningsindikator** byggd med **Arduino Nano**.  
Projektet använder två lysdioder (röd och grön) och en knapp för att indikera **strömstatus** och **bekräfta larm** — helt utan skärm.

---

## ✨ Funktioner

- 🔴 **Röd LED**
  - Börjar blinka snabbt (~10 Hz) när systemet startas.  
  - Blinkfrekvensen saktar gradvis ner till 1 Hz under en timme.  
  - Indikerar aktivt larm eller opålitlig strömkälla.

- 🟢 **Grön LED**
  - Tänds med konstant ljusstyrka när användaren bekräftar larmet.  
  - Använder PWM-pin D10 för att kunna justera ljusnivå.

- 🔘 **Knapp (A2)**
  - Bekräftar larmet när den trycks in (intern pull-up).  
  - Stänger av röd LED och aktiverar grön LED.

---

## ⚙️ Hårdvaruanslutningar

| Komponent | Arduino-pin | Funktion |
|------------|-------------|----------|
| Röd LED    | D11         | Blinkande larmindikator |
| Grön LED   | D10 (PWM)   | Konstant ljus efter bekräftelse |
| Intern LED | D13         | Speglar röd LED |
| Knapp      | A2          | Alarm-bekräftelse (pull-up) |

---

## 💡 Justerbara parametrar

I koden kan du enkelt ändra:

```cpp
const int GREEN_BRIGHTNESS = 80;   // ljusstyrka 0–255
const unsigned long RAMP_DURATION = 3600000UL; // tid till långsam blinkning (1 h)
