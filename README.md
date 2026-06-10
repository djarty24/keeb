# Keeb Journal
Hack Club Keeb custom keyboard.

## Table of Contents
* [6/8](#68)

## 6/8
Just found out about Hack Club Keeb! I wanted to get started with this challenge.

### Planning Your Keyboard
I first read through the [Planning Your Keyboard](https://keeb.hackclub.com/docs/planning/) section in the docs and started brainstorming what I wanted my keyboard to look like. After doing some research, I've decided on a 75% layout for my Mac. I want it to look pretty standard, like this image:

![Keyboard Inspo Image](/img/1.jpg)

The personalization will be through the keycaps! I'll also add fun illustrations on the PCB silkscreen. I'm thinking of designing my own Monet themed keycaps or purchasing custom ones off of Etsy like the following:

![Keycaps Inspo Image](/img/2.webp)
![Keycaps Inspo Image](/img/3.jpg)

As for the case, I want it to have slight borders around everything and larger borders to separate the arrow keys and function row like the first image displayed.

```
Esc   F1 F2 F3 F4   F5 F6 F7 F8   F9 F10 F11 F12   Power

`  1  2  3  4  5  6  7  8  9  0  -  =   Backspace     Home
Tab Q  W  E  R  T  Y  U  I  O  P  [  ]   \          PgUp
Caps A  S  D  F  G  H  J  K  L  ;  '   Return       PgDn
Shift Z  X  C  V  B  N  M  ,  .  /   Shift   ↑      End
Ctrl Opt Cmd        Space        Cmd Opt     ← ↓ →
```

Design Time: ~90 min

### Designing the PCB (day 1)
Next, I moved on to the [Desighing the PCB](https://keeb.hackclub.com/docs/pcb-design/) section in the docs.

I've decided on linear switches since they seem to be the quietest and best for wrist health.

Initially I was pretty confused with how to even get started. So I headed over to YouTube and watched a tutorial by [Joe Scotto](https://www.youtube.com/watch?v=7LyziNdFlew) that explained direct vs. matrix wiring. Looking at my reference image, my keyboard needs 15 columns and 6 rows, which means my microcontroller needs at least 21 pins. This fits perfectly within the Raspberry Pi Pico's 26 GPIO pins!

Now, it was time to open up KiCAD and get started.

In the tutorial, it said I would need stabilizers for keys larger than 2u. So what I did next was identify the size of each key. Most keys were 1u, however some exceptions:

Tab: 1.5u
Caps Lock: 1.75u
Left Shift: 2.25u
Right Shift: 1.75u
Backslash: 1.5u
Return: 2.25u
Backspace: 2u
Space: 6.25u
Ctrl/Opt/Cmd/Right Cmd/1.25u

My eyes hurt really bad after squinting over the reference image but I believe this is right. So, the only keys that I need stabilizers for are Left Shift, Return, Backspace, and Space.

Then I created one row of keys.

## 6/9

Today, I continued working on the PCB. I finished up adding all of the key-diode units and orienting them to match my physical keyboard inspo. Although it isn't perfectly aligned it should be good enough to move on to the next step. Here's what my matrix looked like:

![Schematic](/img/schematic.png)

Next, I added in the Pico and added labels to its GPIO pins. I also added the stabilizers and 5 mounting holes as well.

![Schematic](/img/schematic-2.png)

Now, it was time to move on to the next step!

### Designing the PCB (day 2)

THIS TOOK ME 8 HOURS. I don't have many screenshots since I was pretty locked in but I had to manually orient every single switch-diode unit to match the exact layout I wanted. The grid system in KiCad is pretty bad, so I calculated all of the X-Y coordinates of all 81 keys using a formula I made on Desmos and positioned them accordingly. Then, I placed the diodes and routed all of my traces. This is what it looks like now:

![PCB](/img/pcb.png)

The orientation of stuff is a little ugly but I'm not too picky about how it will look as long as it functions. In the future I will most probably remake this with a different MCU that's more compact than the Pico. This is what the 3d view looks like:

![3D View](/img/3d.png)

I went to GrabCAD and downloaded some 3D models of the Cherry MX keycaps and switches that were 1u. However, I got tired of adding them all in because I couldn't find a way to globally update their footprints to link to the model, so I added enough to just get an idea of what it would look like. I also added in a 1.5u stabilizer to test how that would look.

Final step for this part was running the Design Rules Checker (DRC) to make sure everything was good. I cleaned up some connections, ran the DRC again, and the PCB was ready to go! I also committed and pushed all of this to GitHub.