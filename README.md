 local Rayfield = loadstring(game:HttpGet('https://sirius.menu/rayfield'))()

local Window = Rayfield:CreateWindow({
   Name = "🤓animal sim script like APX lol🤓",
   LoadingTitle = "zen hub",
   LoadingSubtitle = "by zen",
   ConfigurationSaving = {
      Enabled = false,
      FolderName = nil, -- Create a custom folder for your hub/game
      FileName = "animalsimhub"
   },
   Discord = {
      Enabled = false,
      Invite = "noinvitelink", -- The Discord invite code, do not include discord.gg/. E.g. discord.gg/ABCD would be ABCD
      RememberJoins = true -- Set this to false to make them join the discord every time they load it up
   },
   KeySystem = false, -- Set this to true to use our key system
   KeySettings = {
      Title = "animal simulator | key",
      Subtitle = "Key System",
      Note = "No method of obtaining the key is provided",
      FileName = "Key", -- It is recommended to use something unique as other scripts using Rayfield may overwrite your key file
      SaveKey = true, -- The user's key will be saved, but if you change the key, they will be unable to use your script
      GrabKeyFromSite = false, -- If this is true, set Key below to the RAW site you would like Rayfield to get the key from
      Key = {"Hello"} -- List of keys that will be accepted by the system, can be RAW file links (pastebin, github etc) or simple strings ("hello","key22")
   }
})

local MainTab = Window:CreateTab("EXP", nil) -- Title, Image
    local MainSection = MainTab:CreateSection("Farm")

    local ToggleDamageLoop = MainTab:CreateToggle({
    Name = "kill all fireball 🔥",
    CurrentValue = false,
    Flag = "damageaction_loop", -- Assurez-vous que chaque élément a un Flag différent si vous utilisez la sauvegarde de configuration
    Callback = function(value)
        if value then
            print("Boucle d'actions de dégâts activée")
            while true do
                local localPlayer = game:GetService("Players").LocalPlayer
                local players = game:GetService("Players"):GetPlayers()

                for , player in ipairs(players) do
                    if player ~= localPlayer then
                        local args = {
                            [1] = "damage",
                            [2] = {
                                ["EnemyHumanoid"] = player.Character.Humanoid
                            }
                        }

                        game:GetService("ReplicatedStorage").SkillsInRS.RemoteEvent:FireServer(unpack(args))
                    end
                end

                -- Optionnel: Ajoutez une pause entre chaque itération pour éviter de surcharger le serveur.
                wait() -- Attendez 1 seconde avant de continuer à la prochaine itération
            end
        else
            print("Boucle d'actions de dégâts désactivée.")
        end
    end,
})
