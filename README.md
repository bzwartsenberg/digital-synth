# synth

A digital synthesizer on a WeAct BlackPill (STM32F411CEU6).

## Architecture

Phase-accumulator oscillators driven by a fixed sample-rate tick, mixed into a
PWM output stage that is low-pass filtered into line level.

- 32-bit phase accumulator per oscillator, advanced by `phase += inc` each sample.
- `inc = f * 2^32 / f_s`, giving ~11 µHz frequency resolution.
- One timer defines the sample rate; one timer drives PWM output.
- Top bits of the phase index a waveform table; lower bits interpolate.

## Roadmap

1. **Sine voice** — one oscillator, fixed frequency, PWM out, RC filter, scope.
2. **Waveforms** — saw, square, triangle. Band-limiting so they don't alias.
3. **Wavetables** — table-per-octave mipmaps, interpolation between tables.
4. **Voltage control** — ADC-read pots and CV for pitch and timbre.
5. **Polyphony** — N voices, mixing, headroom and clipping.
6. **Envelopes** — ADSR at control rate, applied per voice.
7. **FM** — operators, phase modulation, algorithms.

## Hardware

- WeAct BlackPill, STM32F411CEU6, 96 MHz, 128 KB RAM, 512 KB flash.
- ST-Link V2 for flashing and debugging (no onboard debugger).
- Output: PWM pin → reconstruction filter → AC coupling → jack.
