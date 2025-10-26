 Weyland-Yutani CRT Theme for Home Assistant

> *"Building Better Worlds."*  
> A retro-futuristic Home Assistant theme emulating the interface of the **USCSS Nostromo**.  
> Designed for fans of the *Alien* universe — monochrome phosphor glow, subtle scanlines, and Weyland-Yutani terminal typography.

---

 Overview

The Weyland CRT Theme recreates the 1970s computer aesthetic of the Nostromo’s on-board computer, MU/TH/UR, while retaining full modern Home Assistant readability and performance.  
It’s ideal for dashboards on wall-mounted tablets or dark ambient setups.

---

 Installation

1. Copy `nostromo_crt.yaml` into your `/config/themes/` folder.  
2. Add this to your `configuration.yaml` (if you haven’t already):

   ```yaml
   frontend:
     themes: !include_dir_merge_named themes


Restart Home Assistant.
Go to your Profile → Theme and select Nostromo CRT.

<p align="center">
  <img src="Weyland.png" alt="Weyland-Yutani CRT Theme Preview" width="900"><br>
  <em>USCSS Nostromo // MU/TH/UR 6000 Interface Display</em>
</p>

