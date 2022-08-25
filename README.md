# MMM-Cam

Taking a Selfie with webcam on MagicMirror controlled by Mycroft.

## Installation

### Dependencies

```bash
sudo apt install fswebcam 
mycroft-pip install mailjet-rest
git clone git@github.com:krukle-cam-skill.git ~/mycroft-core/skills/cam-skill
git clone git@github.com:oenstrom/contacts-skill.git ~/mycroft-core/skills/contacts-skill
git clone git@github.com:oenstrom/MMM-mycroft-bridge.git ~/MagicMirror/modules/MMM-mycroft-bridge
```

> **Note**
>
> Change git clone destination according to your setup.

### Install

```bash
git clone https://github.com/SmartMirrorUmbrella/MMM-Cam ~/MagicMirror/modules/MMM-Cam
npm --prefix ~/MagicMirror/modules/MMM-Cam install ~/MagicMirror/modules/MMM-Cam
```

## Configuration

These values are set as default, you don't need to copy all of these. Just pick what you need only and add it into your `config:{}`.

```js
debug: true,
width:1280,
height:720, // In some webcams, resolution ratio might be fixed so these values might not be applied.
quality: 100, //Of course.
device: null, // For default camera. Or,
// device: "USB Camera" <-- See the backend log to get your installed camera name.
shootMessage: "Smile!",
shootCountdown: 1,
displayCountdown: true,
displayResult: true,
displayButton: null, // null = no button or name of FontAwesome icon
playShutter: true,
shutterSound: "shutter.mp3",
resultDuration: 120,
photoDir: "photos",
```

## Messages

### Emitted

| Message | Data | About |
| ------- | ---- | ----- |
| cam-skill:selfie_taken | `{selfie: str, resultDuration: int}` | Emitted when a photo has been taken. `selfie` is path to picture and `resultDuration` decides how long selfie should be shown before cam is closed. |

### Subscribed

#### Mycroft bridge

| Message | Data | About |
| ------- | ---- | ----- |
| TAKE-SELFIE | `{"option": {"shootCountdown": int, "playShutter": boolean, "displayCountdown": boolean}}` | Received when a photo should be taken. |
| EXIT-CAM | `{}` | Received when cam interface should close. |

#### MagicMirror bus

| Message | Data | About |
| ------- | ---- | ----- |
| SELFIE-LAST | `{}` | Received when the last photo taken should be shown. |
