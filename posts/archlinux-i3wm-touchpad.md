---
title: archlinux i3wm touchpad config
date: 2022-04-28T19:25:32+08:00
draft: true
---

### Install libinput

```
sudo pacman -Syy libinput xf86-input-libinput xorg-xinput
```

### Show Touchpad devices 

```
sudo xinput list | grep Touchpad
```

>⎜   ↳ ETD2303:00 04F3:3083 Touchpad           	id=12	[slave  pointer  (2)]
>⎜   ↳ ETPS/2 Elantech Touchpad                	id=17	[slave  pointer  (2)]

### Show List Props

```
sudo xinput list-props 12
```

> Device 'ETD2303:00 04F3:3083 Touchpad':
>	Device Enabled (187):	1
>	Coordinate Transformation Matrix (189):	1.000000, 0.000000, 0.000000, 0.000000, 1.000000, 0.000000, 0.000000, 0.000000, 1.000000
>	libinput Tapping Enabled (344):	1
>	libinput Tapping Enabled Default (345):	0
>	libinput Tapping Drag Enabled (346):	1
>	libinput Tapping Drag Enabled Default (347):	1
>	libinput Tapping Drag Lock Enabled (348):	0
>	libinput Tapping Drag Lock Enabled Default (349):	0
>	libinput Tapping Button Mapping Enabled (350):	0, 1
>	libinput Tapping Button Mapping Default (351):	1, 0
>	libinput Natural Scrolling Enabled (323):	1
>	libinput Natural Scrolling Enabled Default (324):	0
>	libinput Disable While Typing Enabled (352):	1
>	libinput Disable While Typing Enabled Default (353):	1
>	libinput Scroll Methods Available (325):	1, 1, 0
>	libinput Scroll Method Enabled (326):	1, 0, 0
>	libinput Scroll Method Enabled Default (327):	1, 0, 0
>	libinput Click Methods Available (354):	1, 1
>	libinput Click Method Enabled (355):	1, 0
>	libinput Click Method Enabled Default (356):	1, 0
>	libinput Middle Emulation Enabled (357):	0
>	libinput Middle Emulation Enabled Default (358):	0
>	libinput Accel Speed (332):	0.000000
>	libinput Accel Speed Default (333):	0.000000
>	libinput Accel Profiles Available (334):	1, 1
>	libinput Accel Profile Enabled (335):	1, 0
>	libinput Accel Profile Enabled Default (336):	1, 0
>	libinput Left Handed Enabled (337):	0
>	libinput Left Handed Enabled Default (338):	0
>	libinput Send Events Modes Available (308):	1, 1
>	libinput Send Events Mode Enabled (309):	0, 0
>	libinput Send Events Mode Enabled Default (310):	0, 0
>	Device Node (311):	"/dev/input/event5"
>	Device Product ID (312):	1267, 12419
>	libinput Drag Lock Buttons (339):	<no items>
>	libinput Horizontal Scroll Enabled (340):	1
>	libinput Scrolling Pixel Distance (341):	15
>	libinput Scrolling Pixel Distance Default (342):	15
>	libinput High Resolution Wheel Scroll Enabled (343):	1

### Set device props

#### Natural Scrolling
> libinput Natural Scrolling Enabled (323):	1

```
xinput set-prop 12 323 1
```

#### Tap to click
> libinput Tapping Enabled (344):	1

```
xinput set-prop 12 344 1
```
