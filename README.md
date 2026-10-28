NeatWork 1.0.0

A mod loader for **Devices Tycoon** that runs beside the game instead of inside its files.

Nothing is patched, renamed or deleted in your game folder. NeatWork opens the game with its
own debug door and hands the mods to the game's own screens, so a mod lives inside the Sandbox
window, inside the Settings screen, inside the office - not floating on top of them. Turn
NeatWork off and the game is the game.

Made by **Neat11/Neat3**.

---

## What you get

**The console** - NeatWork.bat
Installs, enables, reloads and removes mods. Every mod starts switched off, yours included;
you decide what runs. The note pad is the same one you have in game, so you can read your
goals with the game closed.

**The editor** - NeatWork Editor.bat
Write a mod in a real window: dry run, live test on the running game before you enable it,
autocomplete over the game's own arrays and tables, a reference for every API call, and a
Build step that seals your `.neatw` source into a `.neat` pack you can hand to other players.

**Into the game** - NeatWork Install.bat, or the button in the console
Puts a *Devices Tycoon* shortcut on your Desktop and in the Start menu. Click it and NeatWork
asks first: **Normal** runs the game alone, **Modded** starts it with NeatWork loaded. Your
original shortcut is kept, so *Remove* puts it back exactly as it was.

## Mods that ship with it

- **Status HUD** - money, fans, date and stock on the game's own corner, always readable.
- **Sandbox Extender** - the game's Sandbox window, extended: full control of arrays, tables,
  employees, companies, countries, dates and the office, in the game's own layout.
- **Notepad** - a draggable note in game with a tickable goal list, saved to disk.
- **Mod Creator** - makes a working player mod from the starter template without opening a
  text editor.
- **Better Gameplay** - four numbers the Steam reviews keep complaining about: a bad launch
  stops digging a hole, bank credit costs less, released apps and older hardware keep earning,
  and idle staff take contract work. Each one is a switch on the game's Settings screen and
  none of them is on by default.
- **Custom Speed** - the engine clock from 0.25x to 16x, with the button in the game's own
  speed control moved along with it.
- **Chaos Clock** - an example of `api.notify`: a countdown, a card with clickable choices,
  and random money, fan and stock events. Read it if you want to see how the notify API is
  used, play it if you want a bad day.

## Making your own

`NeatWork.register({ ... })`, one file, no build step, no framework.

```js
NeatWork.register({
  name: 'My First Mod',
  version: '1.0',
  onLoad(api) {
    api.every(1000, () => api.toast('still here, $' + api.bigNum(api.gv('Budget'))));
  }
});
```

The API covers the game's numbers (`gv`, `array`, `table`, `bigNum`), the game's screens
(`settingsToggle`, `settingsSlider`, `panel`, `onLayout`, `screen`), timing (`every`, `after`,
`onKey`), the game's clock (`speed`, `gameSpeed`), and asking the player things (`notify` with
clickable choices, `toast`, `float`). The editor's reference page lists all of them with a
copy-paste snippet each.

## Safety

- Game files are never modified. Saves are backed up before NeatWork writes to one.
- No mod is enabled by default, and mods cannot enable themselves.
- Anything that throws gets switched off with its own error kept, so one bad mod does not take
  the game down with it.
- NeatWork needs Node.js 22 or newer and nothing else. No installer, no admin, no internet.

## Requirements

Windows 10 or 11, Devices Tycoon on PC, [Node.js 22+](https://nodejs.org).

## Known limits

- The game has to be started as **Modded**. If you start it from Steam instead of the shortcut,
  NeatWork cannot get in front of it and will tell you so rather than half-loading.
- A mod cannot change how many stars a launch earns - that roll lives in the game's own event
  script. NeatWork can change what a score is *paid out*, which is what Better Gameplay does.
- One game window at a time.
