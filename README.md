# XWVassalOTA

## Adding New Content Via OTA
### Ships
To add a new ship dynamically to the module:

1. Update the xwing-data ships file (ships.js) with the new ship.  If this cannot be done for some reason, you can insert the same contents into file dispatcher_ships.json in this repository
2. Upload the ship image to be used on the ship base to the "ships" folder.  Be sure to use the naming convention below.
3. Upload the "dial hide" ship image to the "dial" folder. This is the smaller ship image shown on the dial. Again be sure to use the naming convention below. **Note:** the module will generate the "Dial Mask" image automatically.
4. Update the ship_images.json file with the information about the ship. An example entry is:

```json  
       {
          "xws": "aggressor",
          "image": "Ship_aggressor.png",
          "identifier" : "standard",
          "faction" : ["scumandvillainy"]
        }
```
* "xws" - the xws of the ship
* "image" - the ship image to be used on the base
* "identifier" - this is used for alt-art ships.  If this is standard art, use "standard" as the value.  If this is an alt art image, give any unique identifier to this ship, and be sure to include it in the ship image name.
+ "faction" - a list of factions this ship can be used by.  Be sure it is all lower case, and no spaces.  This should be main factions only, not subfactions.

*Note:* Faction-specific ship bases will be generated for each faction listed


### Pilots
To add a new pilot dynamically to the module:

1. Update the xwing-data pilots file (pilots.js) with the new pilot.  If this cannot be done for some reason, you can insert the same contents into file dispatcher_pilots.json in this repository
2. Upload the pilot image to be used to the "pilots" folder.  Be sure to use the naming convention below.
3. Update the pilot_images.json file with the information about the pilot. An example entry is:

```json   
          {
            "shipxws": "xwing",
            "pilotxws": "wedgeantilles",
            "faction": "rebelalliance",
            "image": "Pilot_rebelalliance_xwing_wedgeantilles.jpg"
          }
```
 * "shipxws" - the xws of the ship
 * "pilotxws" - the xws of the pilot
 * "faction" - a list of factions this ship can be used by.  Be sure it is all lower case, and no spaces.  This might be a subfaction
4. "image" - The image to be used for the pilot card

*Note:* Faction/subfaction specific backs to the cards will be applied automatically

### Upgrades
To add a new upgrade dynamically to the module:

1. Update the xwing-data upgrades file (upgrades.js) with the new upgrade.  If this cannot be done for some reason, you can insert the same contents into file dispatcher_upgrades.json in this repository
2. Upload the upgrade image to be used to the "upgrades" folder.  Be sure to use the naming convention below.
3. Update the upgrade_images.json file with the information about the upgrade. An example entry is:

```json 
         {
            "slot": "Astromech",
            "xws": "bb8",
            "image": "Upgrade_Astromech_bb8.jpg"
          }
```
* "slot" - the name of the upgrade slot. Be sure this matches the slot value in xwing-data.
* "xws" - the xws of the upgrade
* "image" - The image to be used for the upgrade card

*Note:* Slot specific backs will be applied to the card automatically.

If a new slot is introduced, and you need to add a *new* slot back card, add another entry using "back" as the xws, and replace the upgrade xws in the image name with "back".

The system will then add the image as the default back for all upgrades of this new slot.

### Conditions
To add a new condition dynamically to the module:

1. Update the xwing-data conditions file (conditions.js) with the new upgrade.  If this cannot be done for some reason, you can insert the same contents into file dispatcher_conditions.json in this repository
2. Upload the condition image to be used to the "conditions" folder.  Be sure to use the naming convention below.
3. Upload the condition token image to be used to the "conditions" folder.  Be sure to use the naming convention below.
4. Update the condition_images.json file with the information about the condition. An example entry is:

```json 
         {
            "image": "Condition_illshowyouthedarkside.jpg",
            "tokenimage": "ConditionToken_illshowyouthedarkside.png",
            "xws": "illshowyouthedarkside"
          }
```
* "image" - The image to be used for the front of the condition card.
* "tokenimage" - The image to be used for the condition token
* "xws" - The xws of the condition

*Note:* The backs of the condition cards have been completely genericized, so there is no need to bother with that.

DIALHIDE HERE

### Others
You can also add new images for "cardboard" firing arcs and "cardboard" actions (that go on the base ship image).  However, if new actions or arcs are introduced, there most likely will need to be some code changes made to the module.

## General on the Module Behavior with OTA
OnLoad of the module, it will:
* Download and save a new copy of the ships, pilots, upgrades and conditions files from xwing-data to the module
* Download and save a new copy of the dispatcher ships, pilots, upgrades and conditions files from OTA
* Parse the _images.json files in OTA and download any images referenced if they don't already exist in the module
* Generate any missing DialMask images (the blank dial the opponent sees). This will have the "dial hide" ship image in the corner, and the dial color will be faction-correct
* Generate any missing ShipBase images (the image used as the ship in the game).
 * This image will have (faction-correct) firing arcs (from xwing-data)
 * It will have the correct actions (from xwing-data)
 * It will use the proper Ship image (ship_images.json) 

<h3>Dials</h3>
All dials will be automatically generated by the module during Squad Spawn.  Each dial:
<ul><li>Will have the faction-correct face</li>
    <li>Will have the "dial hide" ship image in the upper left corner</li>
    <li>Will have the faction-correct back image</li></ul>

<h3>Ships</h3>
All ship game pieces will be automatically generated by the module during Squad Spawn.  They will:
<ul><li>Have the faction-correct "Show Target Lock" trait</li>
    <li>Have the ability to drop bombs, if the ship has a bomb slot, or if an upgrade grants it (from xwing-data)</li>
    <li>Have the ability to drop cargo, if the ship is a large ship</li>
    <li>Have the faction-correct firing arcs appropriate for the ship (from xwing-data)</li></ul>
If a ship exists in xwing-data, but does not exist in OTA, the module will generate a WIP (Work in Process) ship base.  This WIP ship will be faction-correct, and will have the appropriate actions and firing arcs.
<h3>Pilots</h3>
All pilot cards will be automatically generated by the module during Squad Spawn.  They will:
<ul><li>Have sub-faction correct backs</li></ul>
If a pilot exists in xwing-data, but does not exist in OTA, the module will generate a WIP (Work in Process) pilot card.
<h3>Upgrades</h3>
All Upgrade cards will be automatically generated by the module during Squad Spawn.  They will:
<ul><li>Have slot-specific backs</li>
</ul>
If an upgrade exists in xwing-data, but does not exist in OTA, the module will generate a WIP (Work in Process) upgrade card.  This WIP upgrade will be slot-specific.
<h3>Conditions</h3>
All condition card and tokens will be automatically generated by the module during Squad Spawn.  They will:
<ul><li>Have a neutral back</li></ul>
If a condition exists in xwing-data, but does not exist in OTA, the module will generate a WIP (Work in Process) condition card and a WIP condition token.


<h2>Naming Conventions</h2>
<h3>Ships</h3>
<b>Standard ship images:</b> Ship_&lt;ship-xws&gt;.png<br>
<b>Alt art ship images:</b> Ship_&lt;ship-xws&gt_&lt;identifier&gt;.png

<h3>Base Firing Arcs</h3>
Firing_Arc_&lt;xws firing_arc, lower case, remove spaces&gt;_&lt;xws size&gt;_&lt;xws faction, lower case, remove spaces&gt;.svg
<br>Note: "Resistance" needs to be "rebelalliance" and "First Order" needs to be "galacticempire"

<h3>Actions</h3>
Action_&lt;xws action, lower case, remove spaces&gt;.png

<h3>Pilots</h3>
Pilot_&lt;faction, lower case, remove spaces&gt;_&lt;ship xws&gt;_&lt;pilot xws&gt;.jpg

<h3>Upgrades</h3>
<b>For card fronts:</b> Upgrade_&lt;slotName, lowercase, remove spaces&gt;_&lt;xws&gt;.jpg
<br><b>For unique card backs:</b> Upgrade_&lt;slotName, lowercase, remove spaces&gt;_&lt;xws&gt;_back.jpg
<br><b>For generic card backs:</b> Upgrade_&lt;slotName, lowercase, remove spaces&gt;_back.jpg

<h3>Condition</h3>
<b>Cards:</b> Condition_&lt;xws&gt;.jpg
<br><b>Tokens:</b> ConditionToken_&lt;xws&gt;.png

<h3>Dial Hide Ship Images</h3>
DialHide_%lt;shipxws&gt;.png
