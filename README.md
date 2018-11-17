# esx_kr_staminasystem
This script was not intended to be released. The script was stolen from me and i don't wanna risk anything. Enjoy the script.
Installation is as usual.
If there is any issues with the script feel free to contact me on discord: KRILLE#9026

**Use TriggerServerEvent('skill:GymUpdate') in your gym script. This adds 3% gym-skill, you lose 5% everyday.**

**For those who use esx_gym by Panda can use the following example**

**ROW ~224, make sure to use TriggerServerEvent('skill:GymUpdate') on ALL the exercises AND not only the example below!**
```
Citizen.CreateThread(function()
    while true do
        Citizen.Wait(0)

        for k in pairs(arms) do

            local plyCoords = GetEntityCoords(GetPlayerPed(-1), false)
            local dist = Vdist(plyCoords.x, plyCoords.y, plyCoords.z, arms[k].x, arms[k].y, arms[k].z)

            if dist <= 0.5 then
				hintToDisplay('Press ~INPUT_CONTEXT~ to train your ~g~arms')
				
				if IsControlJustPressed(0, Keys['E']) then
					if training == false then
					
						TriggerServerEvent('esx_gym:checkChip')
						ESX.ShowNotification("Preparing the exercise...")
						Citizen.Wait(1000)					
					
						if membership == true then
							local playerPed = GetPlayerPed(-1)
							TaskStartScenarioInPlace(playerPed, "world_human_muscle_free_weights", 0, true)
							Citizen.Wait(30000)
							ClearPedTasksImmediately(playerPed)
							TriggerServerEvent('skill:GymUpdate')
							ESX.ShowNotification("You have to rest for ~r~60 seconds~w~ before you can continue")
							
							--TriggerServerEvent('esx_gym:trainArms') ## COMING SOON...
							
							training = true
						elseif membership == false then
							ESX.ShowNotification("You must have a membership to be able to exercise")
						end
					elseif training == true then
						ESX.ShowNotification("You need to rest...")
						
						resting = true
						
						CheckTraining()
					end
				end			
            end
        end
    end
end)
```
