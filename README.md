# 💡 IKEA Styrbar Control (Home Assistant Blueprints)

Advanced Home Assistant blueprints for the **IKEA STYRBAR** 4-button remote (E2001/E2002) integrated via **Zigbee2MQTT**.

---

## 🚀 Available Versions

### 1. Version 2.0: Multi-Target Cycle & Direct MQTT (Recommended)
**File:** [`automation/ikea_styrbar_control_v2.yaml`](automation/ikea_styrbar_control_v2.yaml)

- **Direct MQTT Triggers:** Listens to base Zigbee2MQTT device topic (`zigbee2mqtt/<device>`). Decoupled from Home Assistant device registry changes.
- **Zero-Delay Single Target:** When only one target light is configured, click actions fire instantly without `double_click_timeout` delay.
- **Stateful Multi-Target Cycling:** Double-click Left/Right arrows to cycle between multiple light entities or groups with confirmation blink.
- **Double-Click State Helper:** Uses an `input_text` helper (`<button>:<timestamp>`) to prevent button race conditions and sticky flags.
- **All-Targets Toggle:** Double-click ON or OFF toggles all configured lights simultaneously.
- **Continuous Dimming & Kelvin:** Smooth brightness and color temperature adjustment while holding buttons.
- **9-Color Cycle:** 8 custom RGB colors + centered white color temperature.

### 2. Version 1.0: Refined Dimming & 9-Color Cycle
**File:** [`automation/ikea_styrbar_control.yaml`](automation/ikea_styrbar_control.yaml)

- Device-based trigger automation.
- Single group / multi-entity control (lights & switches).
- Continuous dimming and Kelvin temp with min/max bounds.
- 9-color cycle (8 RGB + white).
- Action-on-release hooks for left and right arrows.

---

## 🕹️ Remote Mapping (v2.0)

| Button | Action | Function |
| :--- | :--- | :--- |
| **ON (Top)** | Single Click | Turn ON active target |
| **ON (Top)** | Double Click | Turn ON ALL targets (if multiple targets configured) |
| **ON (Top)** | Hold | Smoothly increase brightness up to maximum limit |
| **OFF (Bottom)** | Single Click | Turn OFF active target |
| **OFF (Bottom)** | Double Click | Turn OFF ALL targets (if multiple targets configured) |
| **OFF (Bottom)** | Hold | Smoothly decrease brightness down to minimum limit |
| **Right Arrow (►)** | Single Click | Next color in 9-color cycle |
| **Right Arrow (►)** | Double Click | Next target entity in targets list (with optional confirmation blink) |
| **Right Arrow (►)** | Hold | Increase color temperature (cooler daylight) |
| **Left Arrow (◄)** | Single Click | Previous color in 9-color cycle |
| **Left Arrow (◄)** | Double Click | Previous target entity in targets list (with optional confirmation blink) |
| **Left Arrow (◄)** | Hold | Decrease color temperature (warmer white) |

---

## 🛠️ Requirements (v2.0)

1. **IKEA STYRBAR** Remote paired via **Zigbee2MQTT**.
2. **Color Cycle Helper:** `input_number.styrbar_color_index` (range: `0..8`, step: `1`).
3. *(Optional, only if multiple targets are used)*:
   - **Active Target Helper:** `input_number.styrbar_active_group` (range: `0..10`, step: `1`).
   - **Double-Click Helper:** `input_text.styrbar_click_pending`.

---

## 💾 Installation

1. In Home Assistant, go to **Settings** → **Automations & Scenes** → **Blueprints**.
2. Click **Import Blueprint** and paste the raw URL:
   ```
   https://github.com/Gemeur/Home-assistant/blob/main/automation/ikea_styrbar_control_v2.yaml
   ```
3. Create a new automation using the imported blueprint and configure your entities.
