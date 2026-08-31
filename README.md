# aprs-igate — the field APRS I-Gate, rebuilt

Resurrection of the V1 LePotato ground station's APRS role: a software TNC
I-Gate (and eventually digipeater) for rocket launches at remote sites
outside APRS network coverage. The V1 build — hardware list, sprint
history, the `rtl_fm | direwolf` pipeline — is preserved as reference at
[`lora-rocket-telemetry/GroundStation/readme.md`](../lora-rocket-telemetry/GroundStation/readme.md);
this repo is the V2: reproducible from a fresh card, config in git,
secrets out of it.

## Mission

1. **RX I-Gate**: hear APRS on 144.390 MHz via RTL-SDR, decode with
   Direwolf, forward to APRS-IS — so a LightAPRS tracker on the rocket
   reaches aprs.fi even from a field with no infrastructure.
2. **Digipeat (later)**: requires a transmitter (V1 validated a Baofeng
   UV-5R + APRS-K1 cable path); RX-only gating needs none.

## The V1→V2 deltas (decided up front)

| V1 did | V2 does | why |
|---|---|---|
| Direwolf built from source | `apt install direwolf` | packaged on Debian 12/13; reproducible |
| crontab autostart | systemd unit (`systemd/`) | supervised restart, journal, the apogee-services pattern |
| Ubuntu Desktop + VNC + Xastir on-box | headless Lite OS; maps live on aprs.fi / a laptop | the box is an appliance, not a workstation |
| callsign/passcode in live config only | `config/igate.conf.example` committed, real one NOT | same rule as the rocket repo's `callsign_binding`: operator identity is field config, never committed |

## Hardware (candidate — confirm what survives from V1)

- SBC: **TBD** — the original LePotato, or any spare Pi
- RTL-SDR V4 dongle (V1 unit, if still on hand)
- NA-701 dual-band antenna (one of the V1 pair)
- APRS frequency: 144.390 MHz (North America)

## The pipeline (V1's, still the standard shape)

```bash
rtl_fm -f 144.39M - | direwolf -c sdr.conf -r 24000 -D 1 -
```

## Status

**LIVE 2026-08-31** on `apogee-gs` (the Pi 5 — decided over the LePotato,
which stays benched): `aprs-igate.service` enabled, RX-only, KC3ZTQ-10
verified on APRS-IS and visible on aprs.fi, roof Arrow J-pole. Live config
at `/etc/aprs-igate/igate.conf` on the box (identity + passcode, not in
git). Remaining items + measured bring-up detail: `docs/BRINGUP.md`.
