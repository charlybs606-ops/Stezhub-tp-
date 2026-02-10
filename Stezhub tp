-- ============================================================
-- STEZ HUB | TP LEFT (F) & TP RIGHT (R) - VERSION FINALE V5 (SANS AUTO-BLOCK)
-- ============================================================

local Players = game:GetService("Players")
local player = Players.LocalPlayer
local UserInputService = game:GetService("UserInputService")
local ReplicatedStorage = game:GetService("ReplicatedStorage")
local StarterGui = game:GetService("StarterGui")

-- 1. WHITELIST
local whitelist = {
    "charlyto68",
    "HugoSous16kJNR",
    "liorrrrrrrrrr0",
    "bestmalix_2",
}

local function checkWhitelist()
    local myName = string.lower(player.Name)
    for _, name in ipairs(whitelist) do
        if myName == string.lower(name) then return true end
    end
    return false
end

if not checkWhitelist() then
    local sg = Instance.new("ScreenGui", player.PlayerGui)
    local txt = Instance.new("TextLabel", sg)
    txt.Size = UDim2.new(1, 0, 1, 0)
    txt.BackgroundColor3 = Color3.fromRGB(0, 0, 0)
    txt.BackgroundTransparency = 0.3
    txt.Text = "ACCÈS REFUSÉ : @" .. player.Name
    txt.TextColor3 = Color3.fromRGB(255, 50, 50)
    txt.Font = Enum.Font.GothamBold
    txt.TextSize = 22
    task.wait(4)
    sg:Destroy()
    return 
end

-- 2. VARIABLES & SPOTS
local char = player.Character or player.CharacterAdded:Wait()
local hrp = char:WaitForChild("HumanoidRootPart")
local hum = char:WaitForChild("Humanoid")
local REQUIRED_TOOL = "Flying Carpet"

-- TP LEFT (Script 1 - 3 points)
local spotsLeft = {
    CFrame.new(-402.18, -6.34, 131.83) * CFrame.Angles(0, math.rad(-20.08), 0),
    CFrame.new(-416.66, -6.34, -2.05) * CFrame.Angles(0, math.rad(-62.89), 0),
    CFrame.new(-329.37, -4.68, 18.12) * CFrame.Angles(0, math.rad(-30.53), 0),
}

-- TP RIGHT (Script 2 - 2 points)
local spotsRight = {
    CFrame.new(-400.36, -6.62, 43.62),
    CFrame.new(-335.19, -5.10, 103.43)
}

-- 3. INTERFACE
local ScreenGui = Instance.new("ScreenGui", player.PlayerGui)
ScreenGui.Name = "VonsTeleport"
ScreenGui.ResetOnSpawn = false

local Frame = Instance.new("Frame", ScreenGui)
Frame.Size = UDim2.new(0, 220, 0, 240)
Frame.Position = UDim2.new(0.85, -110, 0.5, -110) 
Frame.BackgroundColor3 = Color3.fromRGB(2, 2, 2)
Frame.Active = true
Frame.Draggable = true 
Frame.BorderSizePixel = 0
Instance.new("UICorner", Frame).CornerRadius = UDim.new(0, 15)

local Title = Instance.new("TextLabel", Frame)
Title.Size = UDim2.new(1, -20, 0, 35)
Title.Position = UDim2.new(0, 10, 0, 5)
Title.Text = "Stez Hub | TP System"
Title.TextColor3 = Color3.new(1, 1, 1)
Title.Font = Enum.Font.GothamBold
Title.TextSize = 16
Title.BackgroundTransparency = 1

-- BOUTONS TP
local btnLeft = Instance.new("TextButton", Frame)
btnLeft.Size = UDim2.new(0, 90, 0, 40)
btnLeft.Position = UDim2.new(0, 15, 0, 45)
btnLeft.Text = "TP LEFT"
btnLeft.BackgroundColor3 = Color3.fromRGB(255, 255, 255)
btnLeft.Font = Enum.Font.GothamBold
btnLeft.TextSize = 13
Instance.new("UICorner", btnLeft).CornerRadius = UDim.new(0, 8)

local btnRight = Instance.new("TextButton", Frame)
btnRight.Size = UDim2.new(0, 90, 0, 40)
btnRight.Position = UDim2.new(0, 115, 0, 45)
btnRight.Text = "TP RIGHT"
btnRight.BackgroundColor3 = Color3.fromRGB(255, 255, 255)
btnRight.Font = Enum.Font.GothamBold
btnRight.TextSize = 13
Instance.new("UICorner", btnRight).CornerRadius = UDim.new(0, 8)

-- TOUCHES INDICATEURS
local keyLeft = Instance.new("TextLabel", Frame)
keyLeft.Size = UDim2.new(0, 90, 0, 40)
keyLeft.Position = UDim2.new(0, 15, 0, 95)
keyLeft.Text = "Keybind: [F]"
keyLeft.BackgroundColor3 = Color3.fromRGB(255, 255, 255)
keyLeft.Font = Enum.Font.GothamBold
keyLeft.TextSize = 13
Instance.new("UICorner", keyLeft).CornerRadius = UDim.new(0, 8)

local keyRight = Instance.new("TextLabel", Frame)
keyRight.Size = UDim2.new(0, 90, 0, 40)
keyRight.Position = UDim2.new(0, 115, 0, 95)
keyRight.Text = "Keybind: [R]"
keyRight.BackgroundColor3 = Color3.fromRGB(255, 255, 255)
keyRight.Font = Enum.Font.GothamBold
keyRight.TextSize = 13
Instance.new("UICorner", keyRight).CornerRadius = UDim.new(0, 8)

-- ALLOW/DISALLOW
local btnAllow = Instance.new("TextButton", Frame)
btnAllow.Size = UDim2.new(0, 190, 0, 40)
btnAllow.Position = UDim2.new(0, 15, 0, 145)
btnAllow.Text = "ALLOW/DISALLOW"
btnAllow.TextColor3 = Color3.new(1, 1, 1)
btnAllow.BackgroundColor3 = Color3.fromRGB(220, 40, 40)
btnAllow.Font = Enum.Font.GothamBold
Instance.new("UICorner", btnAllow).CornerRadius = UDim.new(0, 8)

local Footer = Instance.new("TextLabel", Frame)
Footer.Size = UDim2.new(1, -20, 0, 20)
Footer.Position = UDim2.new(0, 10, 1, -25)
Footer.Text = ".gg/rE5FjgJVHr"
Footer.TextColor3 = Color3.fromRGB(0, 255, 0)
Footer.Font = Enum.Font.GothamBold
Footer.TextSize = 12
Footer.BackgroundTransparency = 1

-- 4. LOGIQUE TP (Système Auto-Block Retiré)
local function runTP(spotList)
    local tool = player.Backpack:FindFirstChild(REQUIRED_TOOL) or (player.Character and player.Character:FindFirstChild(REQUIRED_TOOL))
    if tool then 
        local humanoid = player.Character:FindFirstChild("Humanoid")
        local root = player.Character:FindFirstChild("HumanoidRootPart")
        if humanoid and root then
            humanoid:EquipTool(tool)
            task.wait(0.1)
            for _, spot in ipairs(spotList) do
                root.CFrame = spot
                task.wait(0.12)
            end
        end
    end
end

-- Events Souris
btnLeft.MouseButton1Click:Connect(function() runTP(spotsLeft) end)
btnRight.MouseButton1Click:Connect(function() runTP(spotsRight) end)

-- Logic Allow avec Timer
local allowActive = false
local allowDeb = false
btnAllow.MouseButton1Click:Connect(function()
    if allowDeb then return end
    allowDeb = true
    allowActive = not allowActive
    
    pcall(function() ReplicatedStorage.Packages.Net["RE/PlotService/ToggleFriends"]:FireServer() end)
    
    local s = tick()
    while tick() - s < 1 do
        btnAllow.Text = string.format("%.2fs", 1 - (tick() - s))
        btnAllow.BackgroundColor3 = Color3.fromRGB(35, 35, 35)
        task.wait()
    end
    
    btnAllow.Text = "ALLOW/DISALLOW"
    btnAllow.BackgroundColor3 = allowActive and Color3.fromRGB(0, 180, 80) or Color3.fromRGB(220, 40, 40)
    allowDeb = false
end)

-- Keybinds (F pour Left, R pour Right)
UserInputService.InputBegan:Connect(function(input, gpe)
    if gpe then return end
    if input.KeyCode == Enum.KeyCode.F then
        runTP(spotsLeft)
    elseif input.KeyCode == Enum.KeyCode.R then
        runTP(spotsRight)
    end
end)
