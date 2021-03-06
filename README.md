# [Tic-80](https://github.com/nesbox/TIC-80/) Experiments

Mostly for my own entertainment, but there might be some useful tips or dev processes for someone else as tic-80 is generally wired up for creating games within the app but that's not my bag.

## [DEMO 🎮](https://entozoon.github.io/tic-80-experiments/dist/example.html)

## New Programme

Copy `/src/example.js` and create a new file, then use similar commands to below:

## Dev

    ./tic80 -code-watch src/example.js > debug.log

### Refresh - it auto syncs but not refresh

    Ctrl-R

## Compile (.exe, .html, .tic cartridge, respectively)

As above, but then hit escape and type:

    export native
    export html
    save example
    folder (to find where the last .tic one is output)

Copy all those bad boys to `/dist`

## Run Compiled

Open .exe or .html as normal, or to run compiled cartridge:

    ./tic80 dist/example.tic

## Source of Other Games

The .tic cartridge files are actually totally uncompiled.
Within tic80 you can do, say `load witch.tic` and alt-3, alt-5, etc through it all!

## Sprites and Maps

Looks to me like the sprite and map editor is simple but powerful AF so totally worth learning.

## Music

All music is made within Tic-80 (there are no viable converters ATOW)
play first track...

    music 0 0 0 false

### Music Editor

### Notes:

* A pattern must be 01+ (rather than default 00) before you can edit notes.
* Effects are in development :( (but I reckon Witch 'em up uses them..)

### Keys

| Key   | Command      |
| ----- | ------------ |
| Alt-5 | Music Editor |
| Alt-4 | SFX Editor   |
| Enter | Play frame   |
| A     | Break        |
| ZXC.. | Notes        |
| SDF.. | Sharps       |

## Reference (tic80.exe)

https://github.com/nesbox/TIC-80/wiki

NOTE: These don't frickin work, at least on windows:

    tic80 .                                  will use current directory as storage
    tic80 ../path/to/cart.tic                will use ../path/to/ as storage and load cart.tic

These are fine:

    tic80 -code game.lua                     load and run the code without startup animation
    tic80 -code-watch game.lua               same as -code but also reload it when TIC is focused

Not convinced about this one though:

    tic80 game.tic -code game.lua            load cartridge, inject the code and run without startup animation
    tic80 > log.txt                          all trace output is redirect to file log.txt
    tic80 | Out-File log.txt                 same as upper one but in case of PowerShell
    tic80 cart.tic -sprites blahblah.gif     inject sprites to cart.tic

    tic80 -surf                              to start in SURF mode
    tic80 -nosound                           to start in silent mode
    tic80 -fullscreen                        to start in fullscreen mode
    tic80 -skip                              to skip startup animation (0.60.0)

## Origin story (obsolete)

Create a blank js game [swap js for lua if that's your thing]:

    tic80
    folder  (can't escape this folder, trust)
    new js
    save example
    edit
    [copy all code to, say src/example.js]

## Lua to JS Conversation (yeah boi!)

Say you want to convert tic-80 examples, because they're typically in Lua (which is okay, but JS is my maître d), this command converts .lua files from `/lua-js-convert-input` to `/lua-js-convert-output`

    npm run convert

Then you must also:

#### Add to header

    // script: js

#### Now..

The converter is pretty garbage. They all are (trust). So if I ever end up writing my own, I'll jot down a few notes:

| Lua              | JS                                 |
| ---------------- | ---------------------------------- |
| ~=               | !=                                 |
| then             | {                                  |
| end              | }                                  |
| if foo=2         | if (foo=2)                         |
| foo=2            | var foo=2                          |
| math.random(a,b) | `a + Math.random() * (b - a) * 2`? |
|                  |                                    |

^ Enough for shake.js
