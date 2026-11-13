# CS2 Viewmodel script for (originally) Launders
### This script allows one to create individual settings for each inventory slot while preserving quickswitching functionality. 

### Intended for Counter-Strike 2 - Feel free to tinker with for other source-engine games 

## Limitations: 
• Script cannot tell when a slot is empty or occupied due to write-only memory.

• Script cannot tell when round is over, thus if your knife is out during round-end/death, round-start/spawn will default to slot1/2. You need to press your eq_slot1/2 or buy_menu key to re-sync the script. 

• If you find yourself with your hand on the wrong side, simply press the eq_slot-key again that you're on. This is a known bug when switching from slot5/10. 
 
## Installation instructions:
1. Create backup/copy of current autoexec.cfg
2. Modify the Binds & Settings sections of the script to your liking - No other section needs to be modified.
3. Place in your autoexec.cfg - Which should be placed within 'C:\Program Files (x86)\Steam\steamapps\common\Counter-Strike Global Offensive\game\csgo\cfg' as well as make sure you have '+exec autoexec.cfg' within CS2's launch options.
4. (Optional - not recommended) Delete backup of autoexec/config after verifying that it works. 

## Optional options: 
1. If you wish you use the NOR-gate for automatic switching to previous slot when using a grenade uncomment (remove the two /'s) from lines 65 & 66. It is a bit buggy due to how commands seem to be registered before the grenade is actually thrown at times as well as it doesn't work well with middle-click throw. 

## Logic path:
```
Example - switching from secondary (Slot 2) to primary (Slot 1)
eq_slot2 -> eq_slot1
eq_slot1    "slot1; set_slot1; weapon_slot; switchhandsright/switchhandsleft;"
  slot1 - takes out your primary (normal game bind)
  set_slot1    "alias eq_invnext eq_slot2; alias eq_invprev eq_slot10; set_lastinv2-10_reset; set_lastinv1_slot; grenade_reset;"
    alias eq_invnext eq_slot2
    alias eq_invprev eq_slot10
    set_lastinv2-10_reset "set_lastinv2_reset; set_lastinv3_reset; set_lastinv5_reset; set_lastinv6_reset; set_lastinv7_reset; set_lastinv8_reset; set_lastinv9_reset; set_lastinv10_reset;"
      set_lastinv2_reset alias set_lastinv2_slot set_lastinv2_reset_slot
        alias set_lastinv2_reset_slot "set_lastinv; base_lastinvs; set_lastinv2; alias set_lastinv2_slot;"
    set_lastinv1_slot "set_lastinv; base_lastinvs; set_lastinv1; alias set_lastinv1_slot;"
      alias eq_lastinv eq_slot2
      alias set_lastinv ""
      set_lastinv1 "alias set_lastinv alias eq_lastinv eq_slot1"
        alias set_lastinv alias eq_lastinv eq_slot1
      alias set_lastinv1_slot ""
    grenade_reset  "alias grenade_key grenade_slots;"
      alias grenade_key grenade_slots;
      grenade_slot "eq_slot10; eq_slot9; eq_slot8; eq_slot7; eq_slot6"
  weapon_slot "bind MOUSE1 "+attack"; bind MOUSE2 "+attack2";"
  switchhandsright/switchhandsleft
```

## Credits
• By akaEcho ([YouTube](https://youtube.com/@akaEch0) | [pastebin](https://pastebin.com/q655J5W5) | [Steam](https://steamcommunity.com/id/akaEchoCS))

• Based on a TF2 script by /u/genemilder (http://pastebin.com/7beau8BP). 

• Modified for CSGO by /u/Flapadiddle (https://pastebin.com/NV4qhDaU | http://steamcommunity.com/id/flapadiddle) 2014/12/29

• Modified for CS2 originally by /u/daFARKA (https://pastebin.com/mQfg91mt | https://steamcommunity.com/id/daFARKA) 2024/04/26

• Modified to fix functionality, condense logic & be made more readable - 2024/05/02

• Add multiple fixes & further reduce redundant logic - 2024/05/03

• Add Grenade-cycle functionality - 2024/05/04

• Revised Grenade-cycle functionality & remove unnecessary aliases - 2024/05/06

• Major overhaul for quickswitching & grenade throwing - 2024/05/07

    Previously quickswitch would bug if you pressed a eq_slotX twice in succession. It would think that your previous and current slot were the same. This Major overhaul fixes the bug. 

    Previously the grenade throw fix didn't allow you to change your mind mid-throw, like letting go of left or right click while still holding the other. This fixes that. 

• Hotfix since switchhandsright/left were added - 2024/05/23
