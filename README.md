# IR Headset

Prototype IR headset built around the Lantronix Open-Q 624A (APQ8053) development
kit. Custom hardware is limited to 2-layer boards.

## Boards

| Board | Status |
|---|---|
| `IR_Headset.kicad_sch` / `.kicad_pcb`: LTE interface board | Schematic done (ERC clean); PCB has all parts, not yet routed |

The LTE interface board connects a NimbeLink Skywire NL-SW-LTE-S7648 modem to the
dev kit's J1 GPIO header over a 40-way ribbon (2.54 mm assumed; verify on your carrier):

- 4-wire UART on BLSP1 (GPIO0 TX, GPIO1 RX, GPIO2 CTS_N, GPIO3 RFR_N), 1.8 V logic via Skywire VREF
- Modem power from the kit's 5 V rail through a 1.1 A polyfuse with 470 uF bulk capacitance
- Open-collector NPN drivers: GPIO96 -> PWR_ON, GPIO98 -> RESET_nIN (GPIO high = asserted)

## Other parts (no custom board)

| Part | Connection |
|---|---|
| Open-Q 624A SOM | Dev kit carrier (its 0.4 mm DF40 connectors need a 6+ layer fab) |
| LITE-ON WCBN3510A Wi-Fi/BT | Built into the SOM; 3 MHF4 antenna ports |
| Taoglas AP.17E GPS | SOM GNSS U.FL, which supplies +2.7 V antenna bias |
| Skywire LTE antennas | Module U.FL: X1 primary, X2 diversity |
| Near-eye display | Prototype: dev kit HDMI -> Sony ECX335 HDMI driver board. Final: 0.49" FHD MIPI DSI micro-OLED on dev kit J2 |
| Camera | 16 mm M12 lens (use the no-IR-cut / 850 nm pass version) on a sensor board on dev kit J4/J5 |

## References

- [NimbeLink NL-SW-LTE-S7648 datasheet](https://www.bipom.com/documents/skywire/1001720_NL-SW-LTE-S7648_Datasheet.pdf)
- [Open-Q 624A SOM datasheet](https://cdn.lantronix.com/wp-content/uploads/pdf/PDS-0011-OpenQ624A_SOM_HW-Datasheet.pdf)
- [Open-Q 624A Development Kit User Guide](https://cdn.lantronix.com/wp-content/uploads/pdf/Open-Q-624A-Development-Kit-User-Guide.pdf)
- [Taoglas AP.17E datasheet](https://www.taoglas.com/datasheets/AP.17E.07.0064A.pdf)
