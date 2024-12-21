# Fully automated breeder reactor

Reactor design

![Reactor design](https://github.com/MCNaOtlichnoYT/IC2_Classic/blob/main/screenshots/2024-12-21_12.13.14.png?raw=true)

Reactor setup

![Reactor design](https://github.com/MCNaOtlichnoYT/IC2_Classic/blob/main/screenshots/2024-12-21_12.13.11.png?raw=true)

![Reactor design](https://github.com/MCNaOtlichnoYT/IC2_Classic/blob/main/screenshots/2024-12-21_12.13.25.png?raw=true)

Set filtered extraction tube to re-enriched rods. CC Monitor isn't connected to anything.

One point of durability from uranium rod adds 44 points to each isotopic rod. 

CC Computer isn't really necessary, it is just used to make sure that all 4 rods are ready to be enriched (in facts it checks bottom one because it's the last one to be inputted/outpputted). Without it efficiency will be only a bit lower.

And yes, software does not support having 4 different types of isotopic rods being bred at the same time (anyway depleted rods are crafted in batches of 8, which is dividable by 4).

CC Computer program:

    reactor = peripheral.wrap("left")
    while 1 do
        fuelrod = reactor.getItemDetail(11)
        if not fuelrod then
            fuel = 0
        else
            fuel = fuelrod["maxDamage"] - fuelrod["damage"]
        end
        isorod = reactor.getItemDetail(20)
        print(dn)
        if not isorod then
            progress = 'No isotopic rod'
        elseif string.find(isorod['displayName'], 'Isotopic')~=nil then
            d = isorod['damage']
            f = isorod['maxDamage']
            progress = tostring(f-d)..'/'..tostring(f)
        else
            progress = 'Done!'
        end
        st = string.find(progress, '/')~=nil
        if st then
            state = 15
        else
            state = 0
        end
        term.clear()
        term.setCursorPos(1,1)
        term.write('Breeder Reactor')
        term.setCursorPos(1,2)
        term.write('Fuel: '..tostring(fuel))
        term.setCursorPos(1,3)
        term.write('Progress: '..progress)
        redstone.setAnalogOutput('left', state)
        sleep(0.5)
    end

