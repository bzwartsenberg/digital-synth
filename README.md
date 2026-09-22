# synth

A digital synthesizer on a WeAct BlackPill (STM32F411CEU6).

## Architecture

Phase-accumulator oscillators driven by a fixed sample-rate tick, mixed into a
PWM output stage that is low-pass filtered into line level.

- 32-bit phase accumulator per oscillator, advanced by `phase += inc` each sample.
- `inc = f * 2^32 / f_s`, giving ~11 µHz frequency resolution.
- Top bits of the phase index a waveform table; lower bits interpolate.
- Audio runs from a DMA block callback. Everything else runs at control rate,
  once per block, and communicates only through a parameter struct.

Target configuration: 96 MHz core, TIM1 PWM at 93.75 kHz (ARR 1023, 10-bit,
center-aligned), sample rate 46875 Hz — 2048 cycles per sample.

## Roadmap

1. **Sine voice** — one oscillator, fixed frequency, PWM out, RC filter, scope.
2. **AR envelope** — gated notes with an attack and release, so nothing clicks.
3. **Internal sequencer** — a hardcoded song stepped at control rate, driving
   `note_on`/`note_off`. No external gear needed to play the thing.
4. **Block processing** — timer-triggered DMA to the PWM compare register,
   double-buffered, audio work moved out of the ISR.
5. **Waveforms** — saw, square, triangle, band-limited with PolyBLEP.
6. **Polyphony** — N voices, allocation, mixing headroom, clipping.
7. **Modulation** — ADC pots via DMA, an LFO, and a `base + sum(depth * source)`
   bus that every modulatable parameter reads from.
8. **Wavetables** — per-octave mipmaps, interpolated between tables.
9. **MIDI in** — UART at 31250 baud through an optocoupler, feeding the same
   `note_on`/`note_off` entry point as the sequencer.
10. **FM** — 4 operators, 8 fixed algorithms, per-operator envelopes.

Note sources are interchangeable by construction: the sequencer and MIDI are two
implementations of one interface, not two modes.

UI is deliberately deferred. Patches live in the source until there's a reason
for them not to.

## Hardware

- WeAct BlackPill, STM32F411CEU6, 96 MHz, 128 KB RAM, 512 KB flash.
- ST-Link V2 for flashing and debugging (no onboard debugger).
- Output: PWM pin → reconstruction filter → AC coupling → jack.

## Toolchain

Bare metal C: CMSIS device headers, no HAL. Existing BlackPill environment to be
supplied.
