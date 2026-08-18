Welcome to the official repository for **JavaMotion v7.00** and the **MUFACE v6 Framework**.

JavaMotion is a high-precision framework for discrete time-and-frequency $f-t$ trajectory calculations, numerical trajectory solving, and NCO hardware mapping for stepper motor drives. MUFACE (Motor User interFACE), which enables PLC functions with a stepper controller, was originally developed in September 1994.
Starting in 2026, the MUFACE v6 hardware will be adapted for use on multiple hardware platforms.

## 📄 Documentation & Whitepaper

The full technical paper detailing the evolution from analog frequency modulation (SMIK / Pierre Boillat, ETHZ 1987) to discrete-time $f-t$ calculations in JavaMotion is available directly in this repository:

* **[MUFACE v6 Whitepaper (PDF)](./MUFACE-v6_Stepper-Motor-Controller_Whitepaper_v8.1.pdf)**

## 🚀 Download JavaMotion v7.00

Pre-compiled files and release packages for **JavaMotion v7.00** will be available in the **[Releases Section](../../releases)**.

*Note: Source code repository structure is currently being updated for the public release.*


# JavaMotion MUFACE-V4/V6 Serial Communication Protocol (v2.42)

Offizielle Protokoll-Spezifikation für die serielle Schnittstelle (RS-232 / Virtueller USB-COM-Port) zwischen der Steuerungssoftware **JavaMotion** und den Schrittmotor-Controllern **MUFACE v4**, **MUFACE v6** sowie modernen Portierungen (ESP32 / Arduino Nano R4 / Cortex-M).

---

## Quick Overview

* **Physical Layer:** RS-232 / USB-CDC, 9600 Baud (Standard), 8N1, kein HW-Handshake
* **Framing:** Universeller Transport-Rahmen mit Command-ID, 16-Bit Big-Endian Länge, variabler Payload und Modulo-256 Prüfsumme
* **Handshake:** 4-Byte Status-Pakete (`ACK = 0x01`, `NACK = 0x15`)
* **Control Principle:** Pre-Compiled Math – Rampenprofile und NCO-Timerwerte (Teiler & Phasenakkumulator) werden vom PC vorberechnet
* **Persistence:** Autostart-Unterstützung über batteriegepuffertes NV-RAM (BatRAM)

---

## 1. Transport-Frame Struktur

Jedes Datenpaket zwischen PC und Controller ist in einen festen Transport-Rahmen gekapselt:

```text
+------------------ GESAMTER TRANSPORT-FRAME (Len_H : Len_L Bytes) -----------------------+
| Byte 0: Cmd ID | Byte 1..2: Total Len | Byte 3..(N+2): Payload | Byte (N+3): Checksum   |
+----------------+----------------------+------------------------+------------------------+
                                        | Typ | SubLen | SeqNr | Sequenzspezifische Daten |
                                        +-----+--------+-------+--------------------------+
## 🏢 Contact & Maintainers

* **Reinton Audio Lab** – [reinton.ch](https://reinton.ch)
* **Authors:** René Merz, Review: Martin Habenicht.
---
*(Editorial preparation and mathematical documentation synthesis supported also by digital assistance.)*
