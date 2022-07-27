# MMM-Cam

Taking a Selfie with USB cam on MagicMirror.

## Installation

### Dependencies

```sh
sudo apt install fswebcam 
```

### Install

```sh
cd ~/MagicMirror/modules
git clone https://github.com/SmartMirrorUmbrella/MMM-Cam
cd MMM-Cam
npm install
```

## Configuration

### Simple

> This module doesn't need `position` of module unless you're using the touch button.

```js
{
  disabled: false,
  module: "MMM-Cam",
  config: {}
}
```

### Touch-Enabled

To place a button on the mirror that you can click or touch, you will have to include a position and the name of the [Font Awesome](https://fontawesome.com/icons?d=gallery&q=selfie) icon.

```js
{
  disabled: false,
  module: "MMM-Cam",
  position: "bottom_left",
  config: {
    displayButton: "portrait"
  }
}
```

### Defaults and Details

> These values are set as default, you don't need to copy all of these. Just pick what you need only and add it into your `config:{}`

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

### Note

- `width` & `height` : In some environment, resolution would be fixed so these value couldn't affect.

## How to use

By `notification` **TAKE-SELFIE**

Your other module can make an order to take a picture (Button, Voice Commander, Sensors,...)

```js
this.sendNotification("TAKE-SELFIE")
//or
this.sendNotification("TAKE-SELFIE", {
  option: {
    shootCountdown: 1,
    playShutter: false,
    displayCountdown: false,
    // only these 3 properties are available.
  }
})
//or
this.sendNotification("TAKE-SELFIE", {
  option: { ... },
  callback: (result) => {
    console.log(result) // It will have result.path and result.uri
    this.doSomething(result)
  }
})
```

`SELFIE-LAST` : You can display last photo taken on screen.

Photos will be stored in `/photos` directory.
