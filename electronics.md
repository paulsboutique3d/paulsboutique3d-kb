# Electronics

> This page covers the electronics options for my kits, including differences between Version 2 and Version 3 builds, recommended parts, wiring notes, and firmware pointers.

---

## Quick Links

- **International Shipping (Australia Post)** – international zones & charges:  
  <https://auspost.com.au/sending/send-overseas/international-zones>
- **Storefront**: <https://store.paulsboutique3d.com>

---

## Version 2 Variations

Version 2 (“V2”) electronics are the original, battle-tested setup designed for straightforward assembly with widely available parts.

**Core characteristics**
- **MCU**: ATmega328P (Arduino-class) controller  
- **Audio**: DFPlayer-style MP3 module (UART control), with mono class-D amp  
- **Display/Counter**: Dual 7-segment modules driven via MAX7219/74HC595 (or equivalent)  
- **Sensors**: Hall-effect or microswitch trigger; optional magazine detect (Hall or reed)  
- **Lighting**: Simple MOSFET-switched LED strips or basic WS2812 segments (short runs)  
- **Power**: 2S/3S Li-ion or 5–12 V DC (regulated rails for logic and audio)  
- **Wiring**: Point-to-point harness with JST-XH or Dupont connections

**Pros**
- Very reliable, easy to debug with a multimeter  
- Parts are inexpensive and available everywhere  
- Minimal firmware complexity

**Things to know**
- Limited I/O and RAM constrain fancy animations/effects  
- Audio control is basic (track trigger, volume, simple state machine)  
- No built-in Bluetooth or advanced UI

---

## Version 3 Variations

Version 3 (“V3”) electronics modernise the stack for smoother audio, smarter lighting, and cleaner serviceability.

**Core characteristics**
- **MCU**: RP2040 or ESP32 (more RAM/flash, faster I/O)  
- **Audio**: DF1201S/DFPlayer-Pro-class module with robust serial control and stable playback  
- **Display/Counter**: Option A – classic 7-segment (MAX7219); Option B – compact IPS/TFT for richer UI  
- **Sensors**: Hall-effect trigger & magazine detect with debounced logic; low-battery sense input  
- **Lighting**: Full WS2812/NeoPixel barrel/receiver animations via DMA-friendly drivers  
- **Power**: Integrated low-voltage cutoff and soft-start for audio; separated logic/audio grounds to reduce noise  
- **Wiring**: Modular looms with labelled JST-XH; optional Mini-XLR quick-disconnect to the toolhead

**Advantages over V2**
- Rock-solid audio start/stop and track chaining (no “stutter” when state changes)  
- Smoother, brighter lighting animations with less flicker  
- More inputs/outputs for extras (mode switch, pairing button, diagnostics LED)  
- Easier field-service: modules unplug and swap without full disassembly

**Recommended add-ons**
- Inline blade fuse on main positive lead  
- TVS diode on input to protect against hot-plug spikes  
- Ferrite bead on speaker leads if you notice MCU reset under loud peaks  
- Proper strain relief on Mini-XLR/XT30 connectors

---

## Wiring & Harness Notes

- Keep **power and signal** separated where possible; cross at 90° if they must cross.  
- Home-run **grounds**: star-ground audio amp, MCU, and LED power at a single distribution point.  
- Use **18–22 AWG** for power legs (amp + LED rails), **24–28 AWG** for logic/signal.  
- For WS2812 data lines longer than ~20–30 cm, add a **~330–470 Ω** series resistor near the MCU and a **large reservoir cap** (≥470 µF) across +5 V/GND close to the first LED segment.  
- If using Mini-XLR for printhead/pod power: pin 1 = GND, pin 2 = +V, pin 3 = signal (document your pinout in the build log).

---

## Firmware Tips

- Debounce trigger and magazine inputs in **software** even if using Hall sensors.  
- Gate audio triggers with simple state machines to avoid overlapping tracks.  
- For WS2812 on RP2040/ESP32, use libraries that support **DMA/PIO** to reduce CPU jitter.  
- Implement a **low-battery** threshold that gracefully mutes audio and displays a warning before hard cutoff.

---

## International Shipping — Guide Rates (AUD)

> **Disclaimer:** Prices may change; final shipping is calculated at checkout.  
> These guide rates are based on Australia Post **International Standard parcels**.

| Destination zone                     | Up to 250g | Over 250g up to 500g | Over 500g up to 1kg | Over 1kg up to 1.5kg | Over 1.5kg up to 2kg |
|---|---:|---:|---:|---:|---:|
| **Zone 1: New Zealand**              | $16.30 | $19.65 | $26.40 | $33.15 | $39.90 |
| **Zone 2: Asia Pacific**             | $19.95 | $26.00 | $38.15 | $50.30 | $62.45 |
| **Zone 3: US and Canada**            | $22.30 | $29.00 | $42.20 | $55.55 | $68.85 |
| **Zone 4: UK and Europe**            | $27.50 | $34.40 | $48.30 | $62.15 | $76.00 |
| **Zone 5: Rest of the World**        | $33.50 | $42.40 | $60.50 | $78.55 | $96.65 |

For detailed zone definitions and the most current tables, see Australia Post’s **International zones** page:  
<https://auspost.com.au/sending/send-overseas/international-zones>

---

### Support

If you get stuck, ping me via the store contact page or include a short video/wiring photo when you open an issue—makes troubleshooting heaps faster.
