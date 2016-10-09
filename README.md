# FuelRats-mIRC-Ratsignal-Tracker
![mIRC custom window](http://i.imgur.com/CIdh8cE.png)

[more screenshots in wiki](https://github.com/MDB4/mIRC-Ratsignal-Tracker/wiki)

Novice/hobbyist work in progress. Warning: this code may burn retinas and/or infuriate you.

The original idea that spawned this script was born of my laziness. I didn't want to tab out of game to copy the system name from IRC. I came up with a disgusting line of mIRC code that seemed to work, and shared it with some rats.
Many thanks to Clapton for seeing that, and giving me a nice regex function to parse out the system name, which I eventually modified to grab additional info from the signal, and now I have this hideous script. /me fires the snickers cannon @ Clapton

# Installation
Right-click and save [fuelrats.ini](https://raw.githubusercontent.com/MDB4/mIRC-Ratsignal-Tracker/master/fuelrats.ini) to your mIRC script folder, open the script editor (alt+r), click File->Load (ctrl+l), locate & open fuelrats.ini.

## Features (bugs?)
Parses ratsignals, stores details in hashtables, logs to a custom mIRC window & keeps its listbox populated with current cases. Cleared case details additionally include clear time, case duration, 1st limpet, and paperwork. Referenced upon new signals to indicate repeat clients, and the number of times they've been back >:D

####Options:
- Copy system name to clipboard on new ratsignal (and !sys)
- Open paperwork when your nick is on the paperwork output line from MechaSqueak[BOT]

####Optional audible text-to-speech notification of most Ratsignal events:
- PC Ratsignals
- XB Ratsignals
- CR Indication (with custom phrasing)
- !cleared cases
- !cmdr updates
- !cr updates
- !sys updates
- !pc !xb platform updates
- Current client IRC quit/part
- Current client IRC rejoin
- Repeat clients
- Clients in frequently reported systems

New Ratsignals are displayed in the left pane of the @Ratsignal window as follows:   
 **[TIME] CMDR • Case # • Platform • System • Language**

Current cases are listed in a listbox in the right pane of the @Ratsignal window, sorted newest first:     
 **CMDR | Case # | Platform | System | Language | Signal Time**

Code red cases indicated with a bold red case #    
Inactive cases indicated with gray CMDR names    

Cleared cases are removed from the listbox and displayed in the left pane of the @Ratsignal window as follows:   
 **[TIME] CMDR • Case Duration • 1st Limpet • Paperwork**

## @Ratsignal custom window right-click context menu lists:
###### (see wiki for screenshots)
- Current "quiet" duration: time since last signal, and the maximum quiet record
- Cases in the past 1hr, and the maximum 1hr record
- Cases in the past 24hrs and the maximum 24hr record
- Hourly breakdown of number of cases in the past 24 hours
- Option Toggle: Copy system name to clipboard on new ratsignals
- Option Toggle: Open paperwork link when you get 1st limpet
- Option Toggle: Display hourly Ratsignal counts & records
- Option Toggle: Listbox display of PC, XB, and inactive cases
- Option Toggle: Text-to-speech events
- If you have a case UUID in your clipboard, an option to view the case on API will exist

## @Ratsignal LISTBOX custom window right-click context menu lists:
###### note: these are local updates only, they do not trigger any !commands to the bot.
- Toggle Case Active/Inactive
- Toggle Case Code Red
- Toggle Case Platform
- Duration since case was opened

## PM Window MechaSqueak[BOT] right-click items:
- !list (and the various switches)
- !search last Ratsignal reported system
- !search user-input system
- !quote user-input case
- !help

## Known issues
- I have zero programming / scripting training. Many functions are written poorly and are probably inefficient, or outright stupid - like why did he write it that way when you could just...
- Relies on constant connection to #fuelrats and #RatChat. i.e: it can't log what you're not in channel to see broadcast.
- If the script is loaded when the board is not clear, those current cases will obviously not have thier origin details logged upon !clear.
- Duplicate ratsignals (under the same CMDR) are basically ignored. If a dupe happens, a counter is incremented and the signal is ignored. Upon !clear of a cmdr with >0 dupes, the count is decremented. On !clear with 0 dupes, the info is saved. This info will be inaccurate if the final !clear is not done on the actual case.
- Some !commands used in PM do not broadcast to channels, these will be missed. In the case of !cmdr, this results in a stray case on the active list, and the actual clear containing dummy origin info.
- A board refresh in and of itself shouldn't prevent !clear tracking, but if new cases come in before all existing cases at the time of a refresh have been cleared, and !CMDR is used on a case, I'll lose track of the new CMDR.
- I probably forgot some things as well

## Unknown issues
- Likely exist

#### TODO
- Add listbox context menu items to update CMDR and System
- Verify and update current case numbers when anyone does a !list or !quote
- Identify and remove old unused code
- Is it possible to read API and list all rescue details? Create a hashtable for ultimate repeat client notification
- There's more I don't remember at the moment
