# HAcore_QNAP
 Home Assistant configuration files for QNAP
# Home Assistant configuration - HAQNAP by svkowalski:
## This is what I produced after about a year and a half of tinkering...</h4>

#### The system consists of:
* Hardware
  * [Raspberry PI 3 Model B](https://www.raspberrypi.org/products/raspberry-pi-3-model-b/) running moOdeaudio (see below)
  * [QNAP TS-251+](https://www.qnap.com/en-us/product/ts-251+) running Docker/Container with HAcore and MQTT images
  * [Logitech Harmony Hub (2)](https://www.logitech.com/en-us/product/harmony-hub) 1 in Office to control music (Denon) and PC (Sony) amps; 1 in Family room controls media center devices:
    * [Onkyo AV-Receiver TX-NR525](https://www.onkyousa.com/Products/model.php?m=TX-NR525&class=Receiver) Zone 2 extends analog sound to other rooms and outdoor porch using a Pyle PCA3 amplifier
    * [Roku Ultra](https://www.roku.com/products/roku-ultra) directly attached to an older (not smart) HDTV (see next)
    * [Panasonic TC-P50U50 Plasma HDTV](https://shop.panasonic.com/support-only/TC-P50U50.html)
    * [Sony BDP-S5200 Blu-ray Disk DVD Player](https://www.sony.com/electronics/support/home-video-blu-ray-disc-players-recorders/bdp-s5200)
    * [Google Chromecast/Chrome Audio:](https://support.google.com/chromecast/?hl=en) Casts Youtube videos to Family room HDTV...
  * [TP-Link:](https://www.tp-link.com/us/home-networking/smart-home/smart-switches) several smart plugs, switches, bulbs...
  * ~~[Wink hub](http://status.winkapp.com) control z-wave devices, including Philips and GE switches~~
  * Lights are controlled by Philips Hue hub, MQTT controls Sonoff switches with Tasmota firmware, Z-wave and TP-Link via Wifi:
    * [Philips Hue bulbs, motion/temperature/light sensor, control buttons & hub](https://www2.meethue.com/en-us) several bulbs in Office, Family room and Kitchen
    * [TorchStar Led Strip Light IP65](https://www.torchstar.us/16-4ft-led-strip-light-compatible-with-alexa-wifi-wireless-smart-phone-app-flexible-warm-white-36w-lighting-kit-ip65-waterproof-ul-listed-12v-power-supply-in-party-kitchen.html) using SmartLife/Tuya integration
    * [Sonoff Basic Switches](https://sonoff.tech) reflashed with Tasmota
    * [Aeotec Z-Stick Gen5](http://aeotec.com/z-wave-gen5) connected to HAcore via QNAP USB port; controls 3 GE/Jasco dimmer switches.
    * [WyzeSense](https://wyze.com/wyze-sense.html) used to second-guess the state of my garage door; motion detector does a Wake-on-Lan to my computer
    * [LiftMaster Wi-Fi Garage Door Opener](https://www.liftmaster.com/828lm-internet-gateway/p/G828LM) controlled by MyQ sensor & hub.
    * [InkBird C929](https://www.ebay.com/itm/254573599524?ViewItem=&item=254573599524) Temperature sensor that controls exhaust fan in server closet

#### 
* Software
  * Home Assistant version 0.110.5: I try to stay current, unless the new version is causing errors.
  * [Lovelace UI](https://www.home-assistant.io/lovelace) is now the default UI; augmented by these HACS add-ins:
    * [mini-media-player](https://github.com/kalkih/mini-media-player) nice HACS add-in that gives me greater control over the appearance and options available for media devices
    * [roku-card](https://github.com/custom-cards/roku-card) another nice custom card that is used to control the Roku via on-screen remote button layout
    * [Emulated Roku](https://gitlab.com/mindig.marton/ha-emulated_roku) used to integrate controls on Harmony remotes for Bookcase lights and pausing the moOdeaudio player
    * [Bar card](https://github.com/custom-cards/bar-card) used to create more compact view of loudness on Onkyo receiver
    * [CCH - Customize header](https://github.com/maykar/compact-custom-header) to tailor the chevrons and control visibility
    * [Circadian Lighting](https://community.home-assistant.io/t/circadian-lighting-custom-component/61246): still working the kinks out of this light brightness/color control
    * [lovelace layout card](https://github.com/thomasloven/lovelace-layout-card) to get more control over tab layouts
    * [Nexia/Trane thermostat](https://github.com/ryannazaretian/hacs-nexia-climate-integration)
    * [Weather Card](https://github.com/bramkragten/weather-card)
    * Themes, including Dark Mint and Google night mode
  * [moOdeaudio](http://moodeaudio.org/) used to manage my music collection, as well as stream music: SOMA FM Groove Salad, Drone Zone, et al.; A.M. Ambient, Ambient Sleeping Pill; KMFA, KUT/KUTX (Austin), WFMT (Chicago), WQXR (NYC).

#### Automations implemented:
* _Just before dawn_: 30 minutes before sunrise, turn on bathroom light
* _Just before dusk_: 45 minutes before sunset, turn on several lamps, lights & candles(!)
* _Turn Bookcase lights on/off_: either manually, or triggered when TV is turned on.
* _Turn candles on/off_: I converted some battery-operated candles to use wall power. TP-Link switches turn them on & off as a group.
* _Toggle MPD_: Pause/restart moOde music via Harmony remotes & UI
* _Start Harmony Activity from Input Select_: I depend on the Harmony Hub to control my Onkyo receiver and Panasonic HDTV, as well as the Roku Ultra. These actions are all defined as Activities to the Harmony Hub.
* _Set Receiver volume slider_: The volume slider is scaled to match the number that appears on the receiver display. The HA Community provided the necessary clues for this.
* _Play/Pause moOdeAudio_: Issue MPD play/pause command to enable music to be muted in other rooms when the TV is turned on
* _Toggle Bookcase lights_: Turns on Bookcase lights when watching TV--but only after sunset
* _Turn off all lights_: Make sure everything is turned off 15 minutes after midnight
* ...plus several others implemented through the front-end
#### Resources:
I found these YouTube channels and websites to be helpful in getting me pointed in the right direction:
* [SmartHomeBeginner](www.smarthomebeginner.com/configure-google-assistant-for-home-assistant/)
* [BRUH3-Home-Assistant-Configuration](https://github.com/bruhautomation/BRUH3-Home-Assistant-Configuration)
* [JuanM: juanmtech.com](https://www.youtube.com/channel/UCR7Xa7cU9wfkSY9v3yN2Vtw) has some really helpful videos to get started with Lovelace
#### TBD:
* ~~Fix some nagging incorrect behaviors that occur when directing Onkyo AV receiver to play music~~ (fixed?)
*   Add option for selecting Zone 2 Cast input
*   Open/Close garage door using MYQ
* ~~Get SSL & DnDNS working. Got it working on Hasspian, got tangled up in Docker issues on QNAP.~~ Set aside for now. May try new remote access through Nabu Casa
* Improve light behavior to turn on when the weather is cloudy. (someday)
