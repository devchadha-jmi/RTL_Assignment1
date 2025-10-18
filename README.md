# Assignment 1 — Variable Pulse Generator

## Objective
Design and implement a **Variable Pulse Generator** in Verilog that generates a configurable output pulse based on user-defined pulse duration and pulse period settings.

---

## Problem Description
The circuit operates on a **100 MHz clock (10 ns period)** and generates a pulse whose **on-time** (high duration) and **period** are configured via two 4-bit input ports.  
Each input step corresponds to one clock cycle (10 ns).

The module should generate the correct pulse waveform for all valid configurations and handle invalid configurations gracefully.

---

## Specifications

### Top-Level Ports

| Port Name | Direction | Description |
|------------|------------|--------------|
| `i_clk` | Input | 100 MHz system clock |
| `i_rst` | Input | Synchronous reset |
| `i_pulse_duration` | Input [3:0] | Configurable pulse high time |
| `i_pulse_period` | Input [3:0] | Configurable pulse period |
| `o_pulse` | Output | Generated pulse |
| `o_invalid_config` | Output | High when configuration is invalid |

---

## Functional Requirements

1. **Valid Configuration**
   - When `i_pulse_duration <= i_pulse_period`
   - Output `o_pulse` must be **HIGH** for `i_pulse_duration × 10 ns**
   - Pulse must repeat every `i_pulse_period × 10 ns`
   - `o_invalid_config = 0`

2. **Invalid Configuration**
   - When `i_pulse_duration > i_pulse_period`
   - Output `o_pulse` must generate a **50 MHz square wave** (50% duty cycle)
   - `o_invalid_config = 1`

---

## Expected Behavior

| Case | `i_pulse_duration` | `i_pulse_period` | Expected Output | `o_invalid_config` |
|------|--------------------|------------------|------------------|--------------------|
| Valid | 4’d3 | 4’d5 | Pulse HIGH for 30 ns, period 50 ns | 0 |
| Equal | 4’d5 | 4’d5 | Continuous HIGH output | 0 |
| Invalid | 4’d8 | 4’d5 | 50 MHz square wave | 1 |

---

    output reg         o_invalid_config
);
