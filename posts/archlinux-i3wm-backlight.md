---
title: archlinux i3wm backlight
date: 2022-04-28T20:30:26+08:00
draft: true
---

### Check Your Device

```
ls /sys/class/backlight
```

> intel_backlight

### Install Light

```
sudo pacman -Syy light
```


### Use `Light`

```
sudo light
```

#### Inc backlight

```
sudo light -A 10
```

#### Dec backlight
```
sudo light -U 10
```

#### Set backlight
```
sudo light -S 10
```

### KeyBinding in i3wm

#### Change file permission

> You should change the `intel_backlight` to your device name.
> 
> This is to resolve the permission problems when modifying backlight with light.
>
> If this is not set, it will not work when you press the button.
```
sudo chmod o+w /sys/class/backlight/intel_backlight/brightness
sudo chmod o+w /sys/class/backlight/intel_backlight/max_brightness
```

#### KeyBinding

```
# dec backlight
bindsym XF86MonBrightnessDown exec "light -U 10"
# inc backlight
bindsym XF86MonBrightnessUp exec "light -A 10"
```
