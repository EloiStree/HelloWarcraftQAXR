![image](https://github.com/EloiStree/HelloWarcraftQAXR/assets/20149493/840fdc25-a14b-434f-af39-5c4b9c3ff3e3)
![image](https://github.com/EloiStree/HelloWarcraftQAXR/assets/20149493/82903588-4e7e-4126-b8af-637d69b8cdb5)



``` lua

function()
    
    -- Player Information
    local playerName = UnitName("player") or "No Player"
    local playerHealth = UnitHealth("player") or 0
    local maxPlayerHealth = UnitHealthMax("player") or 1
    local playerCastingSpell = UnitCastingInfo("player") or "Not Casting"
    
    -- Pet Information
    local petName = UnitName("pet") or "No Pet"
    local petHealth = UnitHealth("pet") or 0
    local maxPetHealth = UnitHealthMax("pet") or 1
    local petCastingSpell = UnitCastingInfo("pet") or "Not Casting"
    
    -- Target Information
    local targetName = UnitName("target") or "No Target"
    local targetHealth = UnitHealth("target") or 0
    local maxHealth = UnitHealthMax("target") or 1
    local castingSpell = UnitCastingInfo("target") or "Not Casting"
    
    
    
    -- START
    -- CODE THAT FETCH THE MAP INFORMATION OF PLAYER POSITION
    local map = C_Map.GetBestMapForUnit("player");
    local pos = C_Map.GetPlayerMapPosition(map,"player");
    local posX,posY = pos:GetXY()
    
    posX = string.format("%.3f",posX*100)
    posY = string.format("%.3f",posY*100)
    
    
    
    
    
    local tposX,tposY 
    
    
    local name, realm = UnitName("player")
    if realm==nil then
        
        realm=""
    end
    
    --local played = GetTimePlayed()
    
    
    -- END
    
    player_level=  UnitLevel("player")
    current_xp= UnitXP("player")
    max_xp= UnitXPMax("player")
    
    
    local global_cooldown = select(2, GetSpellCooldown(61304))
    local spell_queue_window = GetCVar("SpellQueueWindow") / 1000
    
    
    local array = {
        "Name:"..name,
        "Realm:"..realm,
        "Map X:"..posX,
        "Map Y:"..posY,
        "XP:"..current_xp,
        "XP Max:"..max_xp,
        "Level:"..player_level,
        -- "Played:"..played,
        "GlobalCooldown:"..global_cooldown,
        "Spell Queue Window:"..spell_queue_window,
        "Player Name:"..playerName,
        "Player Health:"..playerHealth,
        "Player Max Health:"..maxPlayerHealth,
        "Player Casting Spell:"..playerCastingSpell,
        "Pet Name:"..petName,
        "Pet Health:"..petHealth,
        "Pet Max Health:"..maxPetHealth,
        "Pet Casting Spell:"..petCastingSpell,
        "Target Name:"..targetName,
        "Target Health:"..targetHealth,
        "Target Max Health:"..maxHealth,
        "Target Casting Spell:"..castingSpell
    }
    
    
    
    
    local separator = "\n"
    
    local resultString = table.concat(array, separator)
    
    return resultString
    
    
end
```



``` lua

function()
    
    local screenWidth = UIParent:GetWidth()
    local screenHeight = UIParent:GetHeight()
    local mouseX, mouseY = GetCursorPosition()
    
    
    
    local array = {
        "Mouse X:"..mouseX,
        "Mouse Y:".. mouseY,
        "Screen width:"..screenWidth,
        "Screen height:"..screenHeight,
        "-"
        
    }
    
    
    
    
    local separator = "\n"
    
    local resultString = table.concat(array, separator)
    
    return resultString
    
    
end





```




``` lua

function()
    
    
    local zoneName = GetZoneText() or ""
    local subzoneName = GetSubZoneText() or ""
    local facing = GetPlayerFacing()
    
    local px, py,pz = UnitPosition("player")
    
    local x, y, z = 0, 0, 0
    
    -- Check if there is a target
    if UnitExists("target") then
        x, y, z = UnitPosition("target")
    end
    
    
    if x==nil then
        x=0
        y=0
        z=0
    end
    
    
    local array = {
        "p X:"..px,
        "p Y:"..py,
        "p Z:"..pz,
        "t X:"..x,
        "t Y:"..y,
        "t z:"..z,
        "facing:"..facing,
        "zoneName"..zoneName,
        "subzoneName"..subzoneName,
        "-"
        
    }
    
    
    
    
    local separator = "\n"
    
    local resultString = table.concat(array, separator)
    
    return resultString
    
    
end






```






``` lua

function()
    
    local p ="player"
    local gold =  GetMoney()
    
    local startTime, duration, _ = GetSpellCooldown(109304)
    local remainingTime = startTime + duration - GetTime()
    
    
    
    local s1= UnitStat(p, 1)
    local s2= UnitStat(p, 2)
    local s3= UnitStat(p, 3)
    local s4= UnitStat(p, 4)
    local armor = UnitArmor(p)
    local mastery, coefficient = GetMasteryEffect()
    local x, y = Minimap:GetPingPosition()
    local mapID, _, _ = Minimap:GetPingPosition()
    local worldX =0
    local worldY =0
    
    worldX = floor(x*10000)/100;
    worldY = floor(y*10000)/100;
    
    local array = {
        "Heal Timer:"..remainingTime,
        "Base 1:"..s1,
        "Base 2:"..s2,
        "Base 3:"..s3,
        "Base 4:"..s4,
        "gold:"..gold,
        "armor"..armor,
        "mastery"..mastery,
        "coefficient"..coefficient,
        "x"..x,
        "y"..y,
        "wx"..worldX,
        "wy"..worldY,
        ""        
    }
    
    
    
    
    local separator = "\n"
    
    local resultString = table.concat(array, separator)
    
    return resultString
    
    
end








```





``` lua
function(...)
    local informationString = ""
    
    -- Target Information
    local targetName = UnitName("target") or "No Target"
    local targetHealth = UnitHealth("target") or 0
    local maxHealth = UnitHealthMax("target") or 1
    local healthPercentage = math.floor(targetHealth / maxHealth * 100)
    local targetPower = UnitPower("target") or 0
    local maxPower = UnitPowerMax("target") or 1
    local powerPercentage = math.floor(targetPower / maxPower * 100)
    local targetLevel = UnitLevel("target") or 0
    local targetClassification = UnitClassification("target") or "Normal"
    local targetCreatureType = UnitCreatureType("target") or "Unknown"
    local targetFaction = UnitFactionGroup("target") or "Unknown"
    local targetReaction = UnitReaction("target", "player") or "Neutral"
    local targetIsPlayer = UnitIsPlayer("target")
    local targetIsDead = UnitIsDead("target")
    local targetIsGhost = UnitIsGhost("target")
    local targetIsTapDenied = UnitIsTapDenied("target")
    local targetIsQuestBoss = UnitIsQuestBoss("target")
    local targetIsElite = UnitClassification("target") == "elite"
    local targetIsRare = UnitClassification("target") == "rare" or UnitClassification("target") == "rareelite"
    local targetIsBoss = UnitClassification("target") == "worldboss" or UnitClassification("target") == "rareelite"
    
    -- Player Information
    local playerName = UnitName("player") or "No Player"
    local playerHealth = UnitHealth("player") or 0
    local maxPlayerHealth = UnitHealthMax("player") or 1
    local playerPower = UnitPower("player") or 0
    local maxPlayerPower = UnitPowerMax("player") or 1
    local playerLevel = UnitLevel("player") or 0
    local playerClassification = UnitClassification("player") or "Normal"
    local playerCreatureType = UnitCreatureType("player") or "Unknown"
    local playerFaction = UnitFactionGroup("player") or "Unknown"
    local playerReaction = UnitReaction("player", "target") or "Neutral"
    local playerIsDead = UnitIsDead("player")
    local playerIsGhost = UnitIsGhost("player")
    local playerIsTapDenied = UnitIsTapDenied("player")
    local playerIsQuestBoss = UnitIsQuestBoss("player")
    local playerIsElite = UnitClassification("player") == "elite"
    local playerIsRare = UnitClassification("player") == "rare" or UnitClassification("player") == "rareelite"
    local playerIsBoss = UnitClassification("player") == "worldboss" or UnitClassification("player") == "rareelite"
    
    -- General Information
    local isInCombat = UnitAffectingCombat("player")
    local isMounted = IsMounted()
    local isStealthed = IsStealthed()
    local isInParty = IsInGroup()
    local isInRaid = IsInRaid()
    
    -- Concatenate information into a single string
    informationString = informationString ..
    "Target Name: " .. targetName .. "\n" ..
    "Target Health: " .. targetHealth .. " / " .. maxHealth .. " (" .. healthPercentage .. "%)\n" ..
    "Target Power: " .. targetPower .. " / " .. maxPower .. " (" .. powerPercentage .. "%)\n" ..
    "Target Level: " .. targetLevel .. "\n" ..
    "Target Classification: " .. targetClassification .. "\n" ..
    "Target Creature Type: " .. targetCreatureType .. "\n" ..
    "Target Faction: " .. targetFaction .. "\n" ..
    "Target Reaction: " .. targetReaction .. "\n" ..
    "Target is Player: " .. tostring(targetIsPlayer) .. "\n" ..
    "Target is Dead: " .. tostring(targetIsDead) .. "\n" ..
    "Target is Ghost: " .. tostring(targetIsGhost) .. "\n" ..
    "Target is Tap Denied: " .. tostring(targetIsTapDenied) .. "\n" ..
    "Target is Quest Boss: " .. tostring(targetIsQuestBoss) .. "\n" ..
    "Target is Elite: " .. tostring(targetIsElite) .. "\n" ..
    "Target is Rare: " .. tostring(targetIsRare) .. "\n" ..
    "Target is Boss: " .. tostring(targetIsBoss) .. "\n\n" ..
    
    "Player Name: " .. playerName .. "\n" ..
    "Player Health: " .. playerHealth .. " / " .. maxPlayerHealth .. "\n" ..
    "Player Power: " .. playerPower .. " / " .. maxPlayerPower .. "\n" ..
    "Player Level: " .. playerLevel .. "\n" ..
    "Player Classification: " .. playerClassification .. "\n" ..
    "Player Creature Type: " .. playerCreatureType .. "\n" ..
    "Player Faction: " .. playerFaction .. "\n" ..
    "Player Reaction: " .. playerReaction .. "\n" ..
    "Player is Dead: " .. tostring(playerIsDead) .. "\n" ..
    "Player is Ghost: " .. tostring(playerIsGhost) .. "\n" ..
    "Player is Tap Denied: " .. tostring(playerIsTapDenied) .. "\n" ..
    "Player is Quest Boss: " .. tostring(playerIsQuestBoss) .. "\n" ..
    "Player is Elite: " .. tostring(playerIsElite) .. "\n" ..
    "Player is Rare: " .. tostring(playerIsRare) .. "\n" ..
    "Player is Boss: " .. tostring(playerIsBoss) .. "\n\n" ..
    
    "General Information:\n" ..
    "Is in Combat: " .. tostring(isInCombat) .. "\n" ..
    "Is Mounted: " .. tostring(isMounted) .. "\n" ..
    "Is Stealthed: " .. tostring(isStealthed) .. "\n" ..
    "Is in Party: " .. tostring(isInParty) .. "\n" ..
    "Is in Raid: " .. tostring(isInRaid)
    
    return informationString
end




```




![image](https://github.com/EloiStree/HelloWarcraftQAXR/assets/20149493/26ee603e-9fb0-40ed-8525-36537dcd316d)
![image](https://github.com/EloiStree/HelloWarcraftQAXR/assets/20149493/5680a50f-d9bc-4a0f-91e5-aa0dfb791a6f)

``` WeakAura
!WA:2!1rv3Unsnu4mksSsJqu2GOcK4Iq4hLwYwOzPRwaTiYKM0euAtKt6skALY6zStgZoXEKTNs6EfQcb7nCtEcq5AUkVaG2NGrvCps9rOVaWXEsBkiXi5X(yF()8DoonlmTaPa5fvxOIXYN9nmIo8nxWce8(Ieza9DYjN1D8yfv36Rc(1C)qUC5KNT6I)G(7)nqNBjMhekK9emUwoOBVonAo4cR6qcnwZeCN47(VOpuqOE1oEqxpJLcpxlztMqLQx7dLRo(tliu)KXJhCwmv2QrNEnpUJNgiq4ejU65QyAuuBIY9svIp9ukx3h4MnB5O616pyu)b1qd8s4mTFCe(mQeXXtPkxKLv)wuCKo8gr7jPGOO(9A0PZ8e(kxWn(U4an7u6GmAJt)B5S5MrbIiH8RZdFxs5y)i6bsmHbQkCoMZMAdYhGuASu38LuSI2xlP8j6W7KUHhxWPxqGWWW1itqjvuqRe15gwnHCAjVPyg)ff8TwcL)8R5VWEzx5LpB)G8PB4hKO0IPPFqAjFvaoIol)8efnZlFkchfhIDYE5S8foZPWmN039oZTpBT2hLDUzcpyMZ2JHnJPkhlftKuLQsr5Uvkobw(WcdlzvGgw(WcxDl3IW36FrcWufNIJl(OI1hDioENdOApQsdhBkKhdLLYLYQlL26lULiXc1TfPNLfGONqXSEeOZk)FsoSc87eqEy7ZbPhEs5TUfhJXbm(e45Y3O5M2RkVvXpUy5QBF)D29t39HBzLzDSiP6ejFT(RKPNk76s5eFPbqtDsFV03pRCulV)ygNPcBcz40nslzEYuyo3hlRNHACCCa0TcRnLuA4lTTgz9udDUn1jolaikIobcD12BMUXfaPpo4ztKIeoz1fJfsA2fXVXKvWWUsZFlGzrRUO2FB3JguRJxKatA6RbCaxVjAAsKM56bTsbBMwZffeHvkZjpf75uZHlToJhWoXG(RwB)9JFDazvJ8DaIJsOKdXZcxowcnxachRX5xY4GdL1b4kXwGK6bPfDt3Z1dYm6nNteJYaSHZv0OX25gPVY)vXmE4cPn0TZamT9qkml9mGodsE04YT5AQeQi0NuhR0qDXdlFYXTV3AQ713iWf4enmIQBS1DCNBBIvmcfHAFqRbvtyKLpmUEC323F)H6YlTwPfJqOC0rnECd0QBOSjH6hj1z2h1xeXiOV3m08hFvVNletDqwgdxOfbNc91G5ElNFoSeJe)22YFXESGNzaIdpP41JdZM9w)MzkP7K)QSzQnnzwt873VoQrJJUAD1pJDalzgeWhZM4kzCJjPp1p06N)1sXAyq6xUWmIHTkbCnASkyqhNRyM8ihh94mx(xkOq7TZNTZNu40)C4)8
```

``` lua
function(progress, r1, g1, b1, a1, r2, g2, b2, a2)
    
    
    local map = C_Map.GetBestMapForUnit("player");
    local pos = C_Map.GetPlayerMapPosition(map,"player");
    local posX,posY = pos:GetXY()
    local facing = (GetPlayerFacing() / (2*3.1418))
   
    
    return posX,posY,facing,1
end

```
