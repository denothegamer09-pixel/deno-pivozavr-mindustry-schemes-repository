## Flare keeper

*this page is not finished! Do not use it!*

This scheme allows you to store unused flares near the core.
#### usage
To turn on the scheme, just use the switch. After turning it on, the scheme will do everything for you.
#### how it works
After building and turning on the scheme, all flares that are not in use will be directed to the core and arranged in a neat circle (if a few flares are in use, there will be gaps in the circle). But if a unit has an item in its inventory, it will drop it. And if its health is below full, the unit will look for a repair point, and if it does not find one, it will go to the core and take its place in the circle.
#### where it can be used
The scheme can be used anywhere, but it is recommended to use it in survival and sandbox modes.
#### source code
Processor code
```
set num 0
set used 0
select time-plased equal time-plased null @second time-plased
printflush message1
ubind @flare
sensor enabled switch1 @enabled
jump 16 equal enabled 1
jump 9 equal enabled 0
control enabled switch1 0 0 0 0
print "      [orange]Flare[] keeper\nBy [#ffff][#DBA9]_Pivo[gold]zavR_[#ffff][white]\nStatus: [#f] disabled"
set time-plased null
set core null
sensor ctrler @unit @controller
jump 15 notEqual ctrler @this
ucontrol unbind 0 0 0 0 [gold]ByPivozavr
end
jump 19 notEqual @unit null
print "      [orange]Flare[] keeper\nBy [#ffff][#DBA9]_Pivo[gold]zavR_[#ffff][white]\nStatus: [#ffff] paused\n[#afafafaf]Flares not found!"
end
set arch @unit
ubind @flare
sensor ctrl @unit @controlled
jump 32 equal ctrl 0
sensor ctrler @unit @controller
jump 32 equal ctrler @this
jump 32 equal ctrler @flare
read ctrl-check ctrler "time-plased"
jump 31 equal ctrl-check null
jump 31 greaterThan ctrl-check time-plased
print "      [orange]Flare[] keeper\nBy [#ffff][#DBA9]_Pivo[gold]zavR_[#ffff][white]\nStatus: [#ffff] paused\n[#afafafaf]Another keeper\nalready working!"
end
op add used used 1
op add num num 1
jump 36 equal @unit arch
sensor dead arch @dead
jump 20 strictEqual dead 0
op sub free num used
jump 40 equal core null
sensor dead core @dead
jump 41 strictEqual dead 0
ulocate building core 0 @copper cx cy 0 core
sensor max core @maxUnits
select max equal max null "-" max
print "      [orange]Flare[] keeper\nBy [#ffff][#DBA9]_Pivo[gold]zavR_[#ffff][white]\nStatus: [#00ff] enabled\n[white]Total: [orange]{0} []/[orange] {1}\n[]Free: [orange]{2} []/[orange] {3}"
format num
format max
format free
format num
set i 0
op mul r num 1.125
op div r r 6.283
op mul r r 1.5
select r greaterThanEq r 7 r 7
select r lessThanEq r 26.85 r 26.85
op div angle 360 num
jump 57 equal @unit arch
ubind @flare
sensor flag @unit @flag
jump 62 equal flag 0
sensor ctrl @unit @controlled
jump 88 notEqual ctrl 0
ucontrol flag 0 0 0 0 0
sensor fitem @unit @firstItem
jump 70 equal fitem null
ucontrol pathfind cx cy 0 0 0
sensor corecap core @itemCapacity
sensor itemcap core fitem
select pos lessThan itemcap corecap core @air
ucontrol itemDrop pos 999 0 0 0
jump 88 always 0 0
sensor hp @unit @health
jump 76 equal hp 70
ulocate building repair 0 @copper rx ry found 0
jump 76 equal found 0
ucontrol pathfind rx ry 0 0 0
jump 88 always 0 0
op mul unitangle angle i
op sin sin unitangle 0
op cos cos unitangle 0
op mul xp r cos
op add x xp cx
select x greaterThanEq x 0 x 0
select x lessThanEq x @mapw x @mapw
op mul yp r sin
op add y yp cy
select y greaterThanEq y 0 y 0
select y lessThanEq y @maph y @maph
ucontrol move x y 0 0 0
op add i i 1
jump 56 lessThan i num
```
Links to GitHub pages:

[Scheme (copy+paste)](https://github.com/denothegamer09-pixel/deno-pivozavr-mindustry-schemes-repository/blob/main/schematic/Flare%20keeper/scheme%20source%20code.txt "Copy the contents of the file to the clipboard and click Import, paste from clipboard in the schematic menu")

[Scheme file](https://github.com/denothegamer09-pixel/deno-pivozavr-mindustry-schemes-repository/raw/refs/heads/main/schematic/Flare%20keeper/Flare%20keeper.msch "Import this .msav file in schematic folder")

Scheme ver.: 1.4
Support: [extended](https://github.com/denothegamer09-pixel/deno-pivozavr-mindustry-schemes-repository/blob/main/schematic/Support%20type%20info.txt)
Min. game ver.: build 157.1 (V8)