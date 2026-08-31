# Bring-up — open questions, then the runbook grows here

## Decisions (2026-08-31, Frank)

1. **Host: the Pi 5 (`apogee-gs`)** — it runs many jobs; LePotato stays in
   the parts bin. The RTL-SDR V4 was already wired into the project box via
   USB with its own second antenna.
2. **Antenna: roof Arrow J-pole** for home service (project-box antenna is
   weak in the basement metal box).
3. **RX-only, no digipeat** (area is saturated). SSID **-10**. Beacon at
   deliberately coarse coordinates.
4. **Gain: fixed -g 49.6** — measured 2026-08-31: auto-gain and low fixed
   gains went deaf on the basement coax run; max gain heard 9 carriers in
   75 s. Decode ratio needs tuning (audio levels 72-89 vs the ~50 ideal) —
   OPEN item; the gate forwards whatever decodes meanwhile.

## Verification bar (write results here, dated)

- [x] `rtl_test` sees the dongle — 2026-08-31, "RTL-SDR Blog V4 Detected"
  by Debian 13's packaged rtl-sdr 2.0.2 (no source build needed; udev
  reload required after install)
- [x] Local decode — 2026-08-31, live regional traffic (KV3B-1 et al.)
- [x] APRS-IS login accepted — 2026-08-31, "logresp KC3ZTQ-10 verified,
  server T2CAEAST"
- [x] Own station visible on aprs.fi — 2026-08-31, KC3ZTQ-10 on the map
- [ ] Survives reboot unattended (service enabled; observe at the Pi's
  next reboot)
- [ ] First RF packet actually GATED to APRS-IS (journal [ig] rx line)
- [ ] Decode-ratio tuning (see Decisions #4)
