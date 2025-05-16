local Window = Rayfield:CreateWindow({
   Name = "blue script",
   Icon = 0, -- Icon in Topbar. Can use Lucide Icons (string) or Roblox Image (number). 0 to use no icon (default).
   LoadingTitle = "nil",
   LoadingSubtitle = "by m_h_1",
   Theme = "Default", -- Check https://docs.sirius.menu/rayfield/configuration/themes

   DisableRayfieldPrompts = false,
   DisableBuildWarnings = false, -- Prevents Rayfield from warning when the script has a version mismatch with the interface

   ConfigurationSaving = {
      Enabled = true,
      FolderName = nil, -- Create a custom folder for your hub/game
      FileName = "Big Hub"
   },

   Discord = {
      Enabled = false, -- Prompt the user to join your Discord server if their executor supports it
      Invite = "noinvitelink", -- The Discord invite code, do not include discord.gg/. E.g. discord.gg/ ABCD would be ABCD
      RememberJoins = true -- Set this to false to make them join the discord every time they load it up
   },

   KeySystem = false, -- Set this to true to use our key system
   KeySettings = {
      Title = "Untitled",
      Subtitle = "Key System",
      Note = "No method of obtaining the key is provided", -- Use this to tell the user how to get a key
      FileName = "Key", -- It is recommended to use something unique as other scripts using Rayfield may overwrite your key file
      SaveKey = true, -- The user's key will be saved, but if you change the key, they will be unable to use your script
      GrabKeyFromSite = false, -- If this is true, set Key below to the RAW site you would like Rayfield to get the key from
      Key = {"Hello"} -- List of keys that will be accepted by the system, can be RAW file links (pastebin, github etc) or simple strings ("hello","key22")
   }
})

    local MainTab = Window:CreateTab("home", 4483362458) -- Title, Image
    local Section = MainTab:CreateSection("farms")

    local Button = Tab:CreateButton({
   Name = "farm level",
   Callback = function()
   -- Auto Farm Level Script for Blox Fruits
-- صنع من قبل ChatGPT لغرض تعليمي فقط

-- تحقق من وجود اللاعب والخصم
local player = game.Players.LocalPlayer
local character = player.Character or player.CharacterAdded:Wait()
local humanoid = character:WaitForChild("Humanoid")

-- إعداد الهدف (الوحش)
local targetName = "Bandit" -- غير اسم الوحش حسب المستوى الخاص بك
local distance = 100

-- دالة البحث عن أقرب عدو
function getClosestEnemy()
    local closest = nil
    local shortestDistance = distance

    for _, v in pairs(game.Workspace.Enemies:GetChildren()) do
        if v.Name == targetName and v:FindFirstChild("Humanoid") and v.Humanoid.Health > 0 then
            local dist = (v.HumanoidRootPart.Position - character.HumanoidRootPart.Position).magnitude
            if dist < shortestDistance then
                closest = v
                shortestDistance = dist
            end
        end
    end
    return closest
end

-- بدء المزراعة التلقائية
while true do
    wait(0.5)
    local enemy = getClosestEnemy()
    if enemy then
        repeat
            wait(0.1)
            character.HumanoidRootPart.CFrame = enemy.HumanoidRootPart.CFrame * CFrame.new(0, 0, 2)
            game:GetService("VirtualInputManager"):SendKeyEvent(true, "F", false, game)
            wait(0.1)
            game:GetService("VirtualInputManager"):SendKeyEvent(false, "F", false, game)
        until enemy.Humanoid.Health <= 0 or not enemy:FindFirstChild("Humanoid")
    end
end

   end,
})

    local Slider = MineTab:CreateSlider({
   Name = "walk speed",
   Range = {16, 300},
   Increment = 1,
   Suffix = "speed",
   CurrentValue = 16,
   Flag = "Slider1", -- A flag is the identifier for the configuration file, make sure every element has a different flag if you're using configuration saving to ensure no overlaps
   Callback = function(Value)
   -- كود لتغيير سرعة اللاعب
-- صنع لأغراض تعليمية

local player = game.Players.LocalPlayer
local character = player.Character or player.CharacterAdded:Wait()
local humanoid = character:WaitForChild("Humanoid")

-- غيّر الرقم 100 إلى السرعة التي تريدها
humanoid.WalkSpeed = (Value)

    end,
})
