# 🛠️ Hardware guide

**Purpose of this document:** Understand what you need to buy, why you need it, and how much it costs.

This isn't just a shopping list. Each component is explained so you understand its role in the system. If you've never built anything like this before—perfect. This guide assumes zero prior knowledge.

---

## 🎯 Content Strategy First

**Before buying hardware, decide your mission:**

### 🏥 Strategy 1: Emergency medical pack (~5.5 GB)
**Best for:** Disaster response, humanitarian missions, field clinics

**Hardware needs:**
- 64GB SD card (minimum)
- 8GB RAM Pi (medical databases benefit from RAM)
- Standard power system

**What you get:**
- Post-disaster medical protocols
- Emergency medicine wiki
- Complete medical encyclopedia
- Water & food safety guides
- Wikipedia medicine (EN + FR)

**Total cost:** ~555€

---

### 📚 Strategy 2: Full knowledge base (~120-150 GB)
**Best for:** Permanent installations, educational centers, remote communities

**Hardware needs:**
- 256GB SD card (required)
- 8GB RAM Pi (Wikipedia searches are RAM-intensive)
- Standard power system

**What you get:**
- Complete Wikipedia (EN + FR)
- All medical content from Strategy 1
- Comprehensive educational resources

**Total cost:** ~570€

---

### 🎒 Strategy 3: Minimal emergency kit (~750 MB)
**Best for:** Rapid deployment, testing, ultra-portable

**Hardware needs:**
- 32GB SD card (sufficient)
- 4GB RAM Pi acceptable (saves €25)
- Lighter power system possible

**What you get:**
- Core disaster medicine
- Emergency procedures
- Water safety guide

**Total cost:** ~430€ (budget optimized)

---

**This guide assumes Strategy 1 (Emergency Medical) for humanitarian missions.** You can scale up or down based on your needs.

---

## 💡 Understanding the system architecture

Before diving into components, let's understand how Prometheus Station works:

```
┌─────────────────────────────────────────────────────────┐
│                   PROMETHEUS STATION                     │
│                                                          │
│  ┌──────────────┐         ┌─────────────┐              │
│  │ Solar Panel  │────────▶│   Battery   │              │
│  │ (captures    │         │ (stores     │              │
│  │  sunlight)   │         │  energy)    │              │
│  └──────────────┘         └──────┬──────┘              │
│                                   │                      │
│                                   ▼                      │
│                          ┌────────────────┐             │
│                          │  Raspberry Pi  │             │
│                          │  (the brain)   │             │
│                          │                │             │
│                          │ • Runs Kiwix   │             │
│                          │ • Serves WiFi  │             │
│                          └────────┬───────┘             │
│                                   │                      │
│         ┌─────────────────────────┴──────────┐          │
│         ▼                                    ▼          │
│  ┌─────────────┐                    ┌──────────────┐   │
│  │ WiFi Radio  │                    │  LoRa Radio  │   │
│  │ (short      │                    │  (long       │   │
│  │  range)     │                    │   range)     │   │
│  └─────────────┘                    └──────────────┘   │
│         │                                    │          │
└─────────┼────────────────────────────────────┼──────────┘
          │                                    │
          ▼                                    ▼
    (Your phone                         (Other LoRa
     connects here                       devices talk
     to access                           over km)
     Wikipedia)
```

**In simple terms:**
1. **Sun** powers the **battery**
2. **Battery** powers the **Raspberry Pi** (the computer)
3. **Raspberry Pi** does two things:
   - Shares Wikipedia via **WiFi** (short range, 50-300m)
   - Enables messaging via **LoRa** (long range, 1-15km+)

Now let's look at each component and understand WHY it's needed.

---

## 🧠 The brain: Computing system

### Raspberry pi 4 (8GB RAM)

**What it is:** A credit-card-sized computer. Like a tiny laptop without screen/keyboard.

**Why we need it:**
- Runs the Kiwix software (serves Wikipedia)
- Creates the WiFi hotspot
- Manages the whole system
- Coordinates communication between components

**Why 8GB specifically:**
- Wikipedia databases are HUGE (90GB+ files)
- 8GB RAM lets the system search them quickly
- 4GB would work but searches would be slower
- 2GB or less: forget it, too slow

**Cost:** ~75€

**Alternatives:**
- Raspberry Pi 4 (4GB): Works but slower searches (~50€, saves 25€)
- Raspberry Pi 5: Newer but more expensive, not necessary
- Other mini computers: Possible but this guide is tested on Pi 4

**What comes with it:**
- The board itself
- Power supply (USB-C, 5V 3A minimum—this is CRITICAL)
- Case with fan (keeps it cool)
- microSD card (this is where everything is stored)

---

### Microsd card: Sandisk extreme 256GB (A2 class)

**What it is:** The "hard drive" of your Raspberry Pi. Everything lives here.

**Why we need it:**
- Stores the operating system (Raspberry Pi OS)
- Stores medical/educational content (size depends on strategy)
- Stores all software and configurations

**Size requirements by strategy:**

**Strategy 1: Emergency medical pack (recommended)**
- Post-disaster protocols + Medical encyclopedia: ~5.5 GB
- Operating system + software: ~10 GB
- **Minimum SD card:** 32GB
- **Recommended:** 64GB (room for growth)

**Strategy 2: Full knowledge base**
- Complete Wikipedia (EN + FR): ~115 GB
- Medical content: ~5.5 GB
- Operating system + software: ~10 GB
- **Minimum SD card:** 256GB ⭐

**Strategy 3: Minimal emergency kit**
- Core medical guides: ~750 MB
- Operating system + software: ~10 GB
- **Minimum SD card:** 16GB
- **Recommended:** 32GB

**Why 256GB recommended:**
- Accommodates ANY strategy
- Room for future content additions
- Handles system logs and cache
- Can store full Wikipedia if needed later

**Why "A2 Class" specifically:**
- A2 = faster random read/write (critical for medical database searches)
- A1 or lower = Searches will be painfully slow
- This isn't about megabytes per second, it's about how fast it can find random pieces of data

**Cost:** ~35€ (256GB) or ~20€ (64GB)

**Don't cheap out here:** A slow SD card makes the ENTIRE system frustrating to use, especially in emergency situations where every second counts.

---

### 📦 Content Strategy Decision

**Which SD card size should you buy?**

| Your Mission | SD Card Size | Cost | Strategy |
|--------------|--------------|------|----------|
| 🏥 **Humanitarian/Disaster Response** | 64GB | ~20€ | Emergency Medical Pack |
| 🎒 **Rapid Deployment/Testing** | 32GB | ~15€ | Minimal Emergency Kit |
| 🏫 **Educational/Permanent Install** | 256GB | ~35€ | Full Knowledge Base |
| 💾 **Flexible/Future-Proof** | 256GB | ~35€ | Can do any strategy |
| 💰 **Budget-Conscious** | 64GB | ~20€ | Best value for field use |

**Recommendation:** Start with **64GB for medical missions** or **256GB if budget allows** (gives you flexibility to add full Wikipedia later).

---

### E-ink display (2.13", 250x122)

**What it is:** A tiny screen like on a Kindle. Uses almost zero power.

**Why we need it:**
- Shows system status at a glance
- Battery level
- Uptime
- Number of connected users
- Works in bright sunlight (unlike LCD screens)

**Why E-Ink specifically:**
- Only uses power when changing the display
- Once something is displayed, it stays there with ZERO power draw
- LCD screens constantly drain power—deal breaker for solar

**Cost:** ~17€

**Is it essential?** 
- No, system works without it
- But extremely useful for monitoring without connecting to WiFi
- Recommended for field deployment

---

## 📡 Communication: LoRa Mesh Network

### Lilygo T-beam LORA32 (868MHz, ESP32 + GPS)

**What it is:** A specialized board for long-range radio communication.

**Why we need it:**
- Creates the mesh network for text messaging
- Has GPS built-in (tracks location)
- Acts as the "gateway" between Raspberry Pi and LoRa network

**Why LoRa (not regular radio):**
- **Range:** 1-15km+ depending on terrain (vs WiFi's 50-300m)
- **Power:** Sips battery (can run weeks on small battery)
- **No infrastructure:** Works when cell towers don't
- **Mesh networking:** Messages hop through other devices to reach destination

**Why 868MHz specifically:**
- You're in Europe → 868MHz is the legal frequency
- US/Canada uses 915MHz
- Using wrong frequency is illegal and won't work

**What's inside:**
- ESP32 chip (handles the radio logic)
- LoRa SX1276 radio module
- GPS chip (NEO-6M or NEO-M8N)
- 18650 battery holder
- Antenna connector

**Cost:** ~47€

**Critical note:** You MUST have an antenna connected before powering on, or you'll damage the radio.

---

### 868MHz Omnidirectional Antenna

**What it is:** The "stick" that sends/receives radio signals.

**Why we need it:**
- Without antenna, radio signals go nowhere
- Omnidirectional = sends in all directions (not just one way)

**Why this specific antenna:**
- Tuned to 868MHz (matching the T-Beam frequency)
- IP66 rated (weatherproof)
- 2-7dBi gain (decent range without being huge)

**Cost:** Varies (~20-40€)

**Understanding "dBi" (antenna gain):**
- Higher dBi = more range BUT more directional
- 2-3 dBi = short, sends everywhere equally
- 5-7 dBi = medium, slight preference for horizontal
- 10+ dBi = very directional, like a flashlight beam

For a portable station, 2-7dBi is ideal.

---

### T-echo meshtastic terminals (868MHz) × 2

**What it is:** Handheld walkie-talkie-like devices for the mesh network.

**Why we need them:**
- Mobile devices to communicate with the station
- Built-in E-Ink screen (shows messages, battery, signal)
- Can work standalone (don't need the Pi nearby)

**Why 2 of them:**
- One for testing communication
- One as backup or for another person
- Can test mesh networking (messages hopping between devices)

**Cost:** ~97€ (2× ~48.49 USD)

**Are they essential?**
- No, you can use your phone with Meshtastic app + cheap LoRa board
- But these are purpose-built, very convenient
- Good for field use (rugged, long battery life)

---

## ⚡ Power System: Solar Independence

### Anker solix PS30 (30W foldable solar panel)

**What it is:** Foldable solar panel that outputs USB-C power.

**Why we need it:**
- Converts sunlight into electricity
- Charges the battery during the day
- Foldable = portable, easy to transport

**Why 30W specifically:**
- Raspberry Pi uses ~3-8W on average
- T-Beam uses ~0.5W
- Total system: ~4-9W
- 30W panel in good sun = 15-25W realistic output
- Enough to run system + charge battery simultaneously

**Understanding solar power:**
- "30W" is PEAK in perfect conditions
- Real-world average: 50-70% of rated power
- Cloudy day: 10-30% of rated power
- Night: 0W (that's what the battery is for)

**Cost:** ~73€

**Could you use less?**
- 20W panel: Would work but slower charging
- 50W panel: Overkill and heavier to carry

---

### Anker powercore 737 (24,000mAh / 140W)

**What it is:** A massive USB battery bank with smart charging.

**Why we need it:**
- Stores energy from solar panel
- Powers the system at night
- Regulates power delivery (prevents damage from fluctuations)

**Understanding the capacity:**
- 24,000mAh at 3.7V = ~89Wh (watt-hours)
- System uses ~4-6W average
- **Runtime:** 89Wh ÷ 5W = ~18 hours
- With solar: infinite (as long as sun comes back)

**Why this specific battery:**
- 140W output (can power hungry devices if needed)
- Multiple ports (can charge T-Beam simultaneously)
- Digital display (shows remaining %)
- Smart charging (won't overcharge from solar)

**Cost:** ~73€

**Could you use less?**
- Smaller capacity: Less runtime on cloudy days
- But you could use a 10,000mAh bank (~40€) if weight is critical

---

### Samsung 18650 batteries (3,450mAh) × 4

**What it is:** Rechargeable cylindrical batteries (like big AA batteries).

**Why we need them:**
- Power the T-Beam LoRa device
- Backup power for portable terminals

**Why 18650 specifically:**
- T-Beam has a built-in holder for this size
- Rechargeable thousands of times
- High energy density (small but powerful)

**Cost:** ~14€ (4× ~3.39€)

**Safety note:** Buy quality brands (Samsung, Panasonic, LG). Cheap 18650s can be dangerous.

---

### Xtar MC2 battery charger

**What it is:** Smart charger for 18650 batteries.

**Why we need it:**
- Safely charges 18650s (prevents overcharge/fire)
- Charges 2 batteries at once
- Auto-shutoff when full

**Cost:** ~15-25€

**Could you skip it?**
- Technically yes (charge via T-Beam USB)
- But having dedicated charger is safer and faster

---

## 🏗️ Infrastructure: Mounting & Cables

### Spiderbeam 7m telescopic fiberglass mast

**What it is:** Lightweight pole that extends to 7 meters.

**Why we need it:**
- Height = better signal range (both WiFi and LoRa)
- Telescopic = collapses for transport
- Fiberglass = doesn't conduct electricity (safe in storms)

**Understanding height and range:**
- Ground level: Obstacles block signals (buildings, trees, hills)
- 3m high: Clear most obstacles
- 7m high: Near line-of-sight for km around
- **LoRa at 7m** can reach 5-15km in open terrain

**Cost:** ~55€

**Is it essential?**
- No, you can operate from ground level
- But you'll lose 50-80% of potential range
- For fixed installation: absolutely worth it
- For portable use: depends on your needs

---

### USB cables (various lengths and specs)

**What we need:**
- **90° angle USB-C (30cm):** Space-efficient connections
- **Standard USB-C (50cm):** Pi to battery
- **Long USB-C (2m, 100W PD 3.0):** Solar panel to battery
- **Micro-USB (30cm):** For older devices if needed

**Why quality matters:**
- Cheap cables = voltage drop = Pi reboots randomly
- 100W PD rating = handles solar charging properly
- Wrong cable = system instability

**Cost:** ~34€ total

**Don't cheap out:** One bad cable can make the whole system unreliable.

---

## 💰 Complete Cost Breakdown

| Category | Item | Price | Why This Matters |
|----------|------|-------|------------------|
| **Computing** | Raspberry Pi 4 (8GB) | ~75€ | The brain—no compromise here |
| | MicroSD 256GB A2 | ~35€ | Full capacity for any strategy |
| | *OR MicroSD 64GB A2* | *~20€* | *For medical pack only (saves 15€)* |
| | E-Ink Display | ~17€ | Monitor without WiFi, minimal power |
| **Communication** | T-Beam 868MHz | ~47€ | LoRa gateway, GPS included |
| | Omnidirectional Antenna | ~30€ | Critical for range, weatherproof |
| | T-Echo Terminals (×2) | ~97€ | Handheld mesh devices |
| **Power** | Solar Panel 30W | ~73€ | Generate electricity from sun |
| | PowerCore 737 24K | ~73€ | Store energy, regulate output |
| | 18650 Batteries (×4) | ~14€ | Power T-Beam and backups |
| | Xtar MC2 Charger | ~20€ | Safe battery charging |
| **Infrastructure** | 7m Fiberglass Mast | ~55€ | Height = range multiplier |
| | USB Cables (various) | ~34€ | Quality cables prevent failures |
| **TOTAL (Full)** | | **~570€** | Full Wikipedia capacity |
| **TOTAL (Medical)** | | **~555€** | With 64GB SD (medical pack only) |

**Budget optimization options:**
- **Use 64GB SD instead of 256GB: -15€** (medical pack only)
- Use 4GB Pi instead of 8GB: **-25€** (slower but functional)
- Skip E-Ink display initially: **-17€**
- Single T-Echo instead of two: **-48€**
- Smaller solar panel (20W): **-20€**
- **Minimum viable medical build: ~430€** (64GB SD, 4GB Pi, no display, 1 T-Echo)
- **Minimum viable full Wikipedia build: ~445€** (256GB SD, 4GB Pi, no display, 1 T-Echo)

---

## 🔧 What's NOT Included (But You Might Want)

### Nice to have:
- **Weatherproof enclosure** for Raspberry Pi (~30-50€)
- **Portable monitor** for setup (any HDMI screen works)
- **USB keyboard/mouse** for initial config (~20€)
- **Multimeter** for debugging power issues (~15€)
- **Antenna extension cable** for better positioning (~10€)

### For permanent installation:
- **Grounding rod** for lightning protection (~30€)
- **Waterproof cable glands** (~10€)
- **Guy wires** for mast stability (~15€)
- **Mounting brackets** for solar panel (~20€)

---

## 📍 Where to Buy (Europe)

**Raspberry pi components:**
- [Kubii.com](https://www.kubii.com) (France-based, official reseller)
- [BerryBase.de](https://www.berrybase.de) (Germany)
- [ThePiHut.com](https://thepihut.com) (UK)
- Local electronics shops (check stock first)

**Lora / meshtastic:**
- [Aliexpress](https://aliexpress.com) (cheapest, slower shipping)
- [Banggood](https://banggood.com)
- [Rokland](https://store.rokland.com) (ships to EU)

**Solar / power:**
- [Amazon.fr](https://amazon.fr) (Anker official)
- Local outdoor/camping stores

**Antennas & mast:**
- [Passion Radio](https://www.passion-radio.com) (France)
- [Spiderbeam.com](https://www.spiderbeam.com) (Germany)
- [DX Engineering](https://www.dxengineering.com) (ships worldwide)

**General electronics:**
- [Conrad.fr](https://www.conrad.fr)
- [Reichelt.de](https://www.reichelt.de)
- [Farnell](https://fr.farnell.com)

---

## ⚠️ Critical Warnings

### 1. Frequency regulations
**868MHz is legal in Europe. DO NOT:**
- Use 915MHz equipment in Europe (illegal)
- Use 868MHz equipment in US/Canada (illegal)
- Transmit without antenna (damages radio)

**Check your local regulations** before buying.

### 2. Power requirements
**Raspberry Pi is SENSITIVE to power quality:**
- Needs stable 5V 3A minimum
- Undervoltage = random reboots = SD card corruption
- Use official power supply or quality USB-C cable rated 3A+

### 3. SD card quality
**Cheap SD cards WILL fail:**
- Use A2 rated cards only
- Fake capacities are common (especially on AliExpress)
- SD card failure = lost system, start over

Buy from reputable sellers (Amazon, official stores).

### 4. Battery safety
**18650 batteries can be dangerous if mishandled:**
- Never short-circuit
- Don't overcharge
- Don't puncture or disassemble
- Use protected cells from known brands

---

## 🎯 Next Steps

Now that you understand the hardware, you're ready to:

1. **Create a shopping list** based on your budget
2. **Order components** (allow 2-4 weeks for everything to arrive)
3. **While waiting:** Read the [installation guides](docs/README.md)
4. **When parts arrive:** Start with [01 - Raspberry Pi Setup](docs/01-raspberry-setup.md)

**Questions about component choices?** Open an issue on GitHub—I'm happy to explain trade-offs!

---

**Last updated:** December 2025  
**Hardware list verified by:** Guillain Mejane (actual purchased components)


