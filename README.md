# 💡 IKEA Styrbar Control: Refined Dimming, Temp & 9-Color Cycle

This Home Assistant Blueprint provides advanced, fine-tuned control over multiple light and switch entities using the IKEA STYRBAR remote integrated via **Zigbee2MQTT**.

It is based on an original concept by <a href="https://github.com/jtosic" target="_blank">jtosic</a> but has been heavily modified to include:
* **Precise Brightness Limits** (Min/Max).
* **Smooth Continuous** dimming and color temperature changes.
* A user-friendly, **graphical 9-Color Cycle** mode.

## ✨ Features

* **Multi-Entity Control:** Control a single light, a light group, or a mix of lights and switches with a single automation.
* **Custom Brightness Limits:** Define `Minimum` and `Maximum` brightness percentages (e.g., limit dimming to never go below 10% or above 90%).
* **Smooth Dimming:** Continuous increase/decrease of brightness when holding the Up/Down buttons, with customizable speed and step size.
* **Precise Color Temperature Control:** Continuous adjustment of color temperature when holding the Left/Right arrows, with defined Kelvin limits (Warmer/Cooler).
* **Graphical Color Cycle:** Use the Left/Right click actions to cycle through **9 custom colors** defined via a graphical Color Wheel selector in the automation settings.

## 🛠️ Requirements

1.  **IKEA STYRBAR** Remote.
2.  **Zigbee2MQTT** integration for the remote.
3.  A dedicated **Home Assistant Input Number Helper** (e.g., `input_number.styrbar_color_index`) to track the current color index.

## 💾 Installation

1.  In Home Assistant, go to **Settings** → **Automations & Scenes** → **Blueprints**

2.  Click **"Import Blueprint"** and paste the URL of the .yaml file: https://github.com/Gemeur/Home-assistant/blob/main/automation/ikea_styrbar_control.yaml

3.  Create a new Automation using this Blueprint.

## ⚙️ Blueprint Configuration

| Input Field | Description | Default | Notes |
| :--- | :--- | :--- | :--- |
| **Styrbar Switch Remote** | The Zigbee2MQTT device for the STYRBAR remote. | (Required) | |
| **Light/Switch Entities** | Select the lights and/or switches to control. | (Required) | |
| **Color Cycle Index Helper** | The `input_number` helper used for the color cycling index (0-8). | (Required) | |
| **Left Arrow Hold (Action on release)** | Optional action to execute **once** when the Left arrow is released after a hold. | (Empty) | Use for secondary actions (e.g., scene setting). |
| **Right Arrow Hold (Action on release)** | Optional action to execute **once** when the Right arrow is released after a hold. | (Empty) | Use for secondary actions (e.g., scene setting). |
| **Minimum Brightness (%)** | The lowest brightness level the remote will dim down to (1-100%). | `1` | Enforced during Hold action. |
| **Maximum Brightness (%)** | The highest brightness level the remote will dim up to (1-100%). | `100` | Enforced during Hold action. |
| **Delay for brightness step (ms)** | Delay between each brightness adjustment iteration. Controls dimming speed. | `50` | Faster dimming. |
| **Brightness Level step (%)** | The size of the step (in percent) applied during continuous dimming. | `20` | Larger steps mean quicker changes. |
| **Delay for color temp step (ms)** | Delay between each color temperature change iteration. | `70` | |
| **Color Temperature step (Kelvin)** | The size of the step (in Kelvin) applied during continuous temperature change. | `250` | |
| **Color 0** to **Color 8** | The 9 colors in the cycle, selected via the graphical color wheel. | Custom RGB Defaults | |


## 🕹️ Remote Control Mapping

| Button Action | Function |
| :--- | :--- |
| **Center Click (ON)** | Toggles ON and sets lights to `Max Brightness`. |
| **Center Click (OFF)** | Toggles OFF. |
| **Up Button (Hold)** | **Increases Brightness** continuously, respecting the defined `Max Brightness (%)` limit. |
| **Down Button (Hold)** | **Decreases Brightness** continuously, respecting the defined `Min Brightness (%)` limit. |
| **Right Arrow (Click)** | Cycles to the **Next Color** in the 9-color list. |
| **Left Arrow (Click)** | Cycles to the **Previous Color** in the 9-color list. |
| **Right Arrow (Hold)** | **Increases Color Temperature (Cooler)** continuously, respecting the defined `Max Kelvin` limit. |
| **Left Arrow (Hold)** | **Decreases Color Temperature (Warmer)** continuously, respecting the defined `Min Kelvin` limit. |
| **Left/Right Arrow (Release)** | Executes optional custom action (configured in blueprint settings). |

---
