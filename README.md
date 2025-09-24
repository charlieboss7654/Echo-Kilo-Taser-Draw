# EKS Taser Outfit Swap

Simple, realisitc and minimal taser drawing script with realistic sound effects!

## Features

* Exact A to B clothing swap per slot )
* Strict gender rules: every entry must specify male or female
* Supports components (0 - 11) and props (0, 1, 2, 6, 7)
* Safe restore on resource stop or ped model change
* realisitc sound effects

## Installation

1. Drop the folder into resources/.

2. Add to server.cfg:

    ensure eks_taser_outfit
   
3. Edit config.lua (see Configuration).

## Configuration

Minimal example (gender required):

Config = {}

-- Check rate (ms)
Config.PollInterval = 120

-- Taser weapons
Config.TaserWeapons = { 'WEAPON_STUNGUN', 'WEAPON_STUNGUN_MP' }

-- Set true if your �A must match texture� exactly
Config.RequireTextureMatch = false

-- A ? B swaps (must include gender = "male" or "female")
Config.List = {
  -- Accessories (belts/holsters) � component 7
  { component = 7, holstered = 78, drawn = 80, gender = "male"   },
  { component = 7, holstered = 78, drawn = 80, gender = "female" },

  -- Tops (shirts/jackets) � component 11
  { component = 11, holstered = 19, drawn = 20, gender = "male"   },
  { component = 11, holstered = 21, drawn = 22, gender = "female" },

  -- Optional example (prop swap; never cleared�just style A?B)
  -- { prop = 0, holstered = 12, drawn = 14, gender = "male"   },
  -- { prop = 0, holstered = 12, drawn = 14, gender = "female" },
}


How it works (quick):

* When your selected weapon is a Taser, the script checks each rule.
* If your current drawable (and texture, if enforced) matches holstered, it stores the exact original and applies drawn.
* When holstered (switched off Taser), it restores every stored slot.
* If your ped model changes (for example, outfit changed elsewhere), the stored cache clears safely.

## Troubleshooting

* Not swapping? Double-check the slot ID (see reference below) and your holstered number matches what you�re actually wearing.
* No sounds? Ensure filenames and paths are exactly html/sounds/draw\.ogg and html/sounds/holster.ogg.
* Wrong slot moving? Confirm you�re using 7 = Accessories (belts/holsters), not 8 (Undershirt).

## Component and Prop ID Reference (2025)

These freemode slots are engine constants and current as of 2025.

Components (0�11)

* 0 Face
* 1 Mask
* 2 Hair
* 3 Torso (arms)
* 4 Legs (pants)
* 5 Parachute / Bag / Task
* 6 Shoes
* 7 Accessories (belts/holsters/ties)
* 8 Undershirt (inner layer)
* 9 Body Armor (vests/plates)
* 10 Decals (badges/patches)
* 11 Tops (shirts/jackets/coats)

Props

* 0 Hats/Helmets
* 1 Glasses
* 2 Ears (earpiece)
* 6 Watches
* 7 Bracelets

Tip: to quickly read your current drawable/texture for a slot, you can add a short debug command that prints GetPedDrawableVariation(ped, slot) and GetPedTextureVariation(ped, slot).

## Support

For help or customization, open a ticket on Discord:
https://discord.gg/busQ9w6dqa
