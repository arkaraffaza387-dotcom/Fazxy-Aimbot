--[[
    ══════════════════════════════════════════════════
      ZetGames-AimLock V4.4 | PREMIUM EDITION
    ══════════════════════════════════════════════════
      Theme    : 🔵 Blue & Black
      Login    : ✅ WAJIB KEY
      Anti-Kick: ✅ SAFE MODE (VPN Locked)
      Fitur    : 🎯 Aimbot | 👁️ ESP | 🔒 VPN
      
      🔒 UPGRADE KE PREMIUM untuk fitur lengkap!
      🛒 Buy: fazxy-store.lovable.app
    ══════════════════════════════════════════════════
--]]

--==============================================================
-- SERVICES
--==============================================================
local Players = game:GetService("Players")
local RunService = game:GetService("RunService")
local UserInputService = game:GetService("UserInputService")
local TweenService = game:GetService("TweenService")
local Lighting = game:GetService("Lighting")
local Workspace = game:GetService("Workspace")
local ReplicatedStorage = game:GetService("ReplicatedStorage")
local SoundService = game:GetService("SoundService")
local HttpService = game:GetService("HttpService")
local TeleportService = game:GetService("TeleportService")
local VirtualUser = game:GetService("VirtualUser")
local Camera = workspace.CurrentCamera

local LocalPlayer = Players.LocalPlayer
local Mouse = LocalPlayer:GetMouse()

pcall(function() SoundService.RespectFilteringEnabled = false end)

print("[ZET] Loading V4.4 PREMIUM...")

--==============================================================
-- THEME
--==============================================================
local ThemePresets = {
    Biru = {MainBG=Color3.fromRGB(8,10,15), PanelBG=Color3.fromRGB(12,15,22), SectionBG=Color3.fromRGB(0,25,60), Accent=Color3.fromRGB(0,150,255), AccentLight=Color3.fromRGB(80,200,255), AccentDark=Color3.fromRGB(0,80,160), ButtonBG=Color3.fromRGB(20,25,35), ButtonActive=Color3.fromRGB(0,90,180), Text=Color3.fromRGB(0,180,255), TextLight=Color3.fromRGB(120,210,255)},
    Merah = {MainBG=Color3.fromRGB(10,10,10), PanelBG=Color3.fromRGB(15,15,15), SectionBG=Color3.fromRGB(40,0,0), Accent=Color3.fromRGB(255,0,0), AccentLight=Color3.fromRGB(255,80,80), AccentDark=Color3.fromRGB(150,0,0), ButtonBG=Color3.fromRGB(25,25,25), ButtonActive=Color3.fromRGB(100,0,0), Text=Color3.fromRGB(255,0,0), TextLight=Color3.fromRGB(255,100,100)},
    Hijau = {MainBG=Color3.fromRGB(8,15,8), PanelBG=Color3.fromRGB(12,22,12), SectionBG=Color3.fromRGB(0,50,0), Accent=Color3.fromRGB(0,255,100), AccentLight=Color3.fromRGB(80,255,150), AccentDark=Color3.fromRGB(0,150,60), ButtonBG=Color3.fromRGB(15,30,15), ButtonActive=Color3.fromRGB(0,120,50), Text=Color3.fromRGB(0,255,100), TextLight=Color3.fromRGB(120,255,180)},
    Ungu = {MainBG=Color3.fromRGB(15,8,20), PanelBG=Color3.fromRGB(22,12,30), SectionBG=Color3.fromRGB(50,0,70), Accent=Color3.fromRGB(180,0,255), AccentLight=Color3.fromRGB(220,120,255), AccentDark=Color3.fromRGB(100,0,150), ButtonBG=Color3.fromRGB(30,15,40), ButtonActive=Color3.fromRGB(120,0,180), Text=Color3.fromRGB(200,100,255), TextLight=Color3.fromRGB(230,180,255)},
    Kuning = {MainBG=Color3.fromRGB(15,15,8), PanelBG=Color3.fromRGB(25,25,12), SectionBG=Color3.fromRGB(60,50,0), Accent=Color3.fromRGB(255,220,0), AccentLight=Color3.fromRGB(255,240,100), AccentDark=Color3.fromRGB(180,150,0), ButtonBG=Color3.fromRGB(35,30,15), ButtonActive=Color3.fromRGB(150,120,0), Text=Color3.fromRGB(255,220,0), TextLight=Color3.fromRGB(255,240,120)},
}

local CurrentThemeName = "Biru"
local THEME = {}
for k, v in pairs(ThemePresets.Biru) do THEME[k] = v end
THEME.YellowDot = Color3.fromRGB(255,220,0)
THEME.GreenDot = Color3.fromRGB(0,255,100)
THEME.RedDot = Color3.fromRGB(255,30,30)
THEME.BlueDot = Color3.fromRGB(0,150,255)
THEME.Shield = Color3.fromRGB(0,255,200)
THEME.Success = Color3.fromRGB(0,255,200)
THEME.Locked = Color3.fromRGB(150,150,150)
THEME.LockedBG = Color3.fromRGB(40,40,40)
THEME.Gold = Color3.fromRGB(255,215,0)

--==============================================================
-- HIGH-SECURITY GAMES
--==============================================================
local HIGH_SECURITY_GAMES = {[920587237]=true,[2788229376]=true,[160331737]=true,[3260590327]=true,[286090429]=true,[142823291]=true}
local function IsHighSecurityGame() return HIGH_SECURITY_GAMES[game.PlaceId] == true end

--==============================================================
-- KEY SYSTEM
--==============================================================
local ValidKeys = {
    ["AzferModz"] = {Expiry = 0, Level = "Premium"},
    ["AzferFree"] = {Expiry = os.time({year=2026, month=9, day=5}), Level = "Free"},
    ["AzferCode"] = {Expiry = os.time({year=2026, month=11, day=26}), Level = "Code"},
    ["AzferHc"] = {Expiry = os.time({year=2027, month=1, day=27}), Level = "Code"},
    ["FazxyFree"] = {Expiry = os.time({year=2027, month=9, day=10}), Level = "Code"},
    ["FreePrem-By-Fazxy"] = {Expiry = 0, Level = "Free"},
}
local KeyWebsite = "https://arkaraffaza387-dotcom.github.io/Key-Zero/"
local PremiumWebsite = "https://fazxy-store.lovable.app"

--==============================================================
-- SCREEN GUI
--==============================================================
local ScreenGui = Instance.new("ScreenGui")
ScreenGui.Name = "ZetGamesV44Premium"
ScreenGui.ResetOnSpawn = false
ScreenGui.ZIndexBehavior = Enum.ZIndexBehavior.Sibling
ScreenGui.IgnoreGuiInset = true
local coreOk = pcall(function() ScreenGui.Parent = game:GetService("CoreGui") end)
if not coreOk or not ScreenGui.Parent then
    pcall(function() ScreenGui.Parent = LocalPlayer:WaitForChild("PlayerGui") end)
end

print("[ZET] GUI Parent: " .. tostring(ScreenGui.Parent and ScreenGui.Parent.Name or "NIL"))

--==============================================================
-- STATE
--==============================================================
local IsLoggedIn = false
local MenuVisible = true
local MenuKey = Enum.KeyCode.RightControl

local ActiveConnections = {}
local function DisconnectKey(key)
    if ActiveConnections[key] then
        pcall(function() ActiveConnections[key]:Disconnect() end)
        ActiveConnections[key] = nil
    end
end

-- ✅ VPN (LOCKED ON — tidak bisa dimatikan)
local VPNActive = true

-- 🎯 AIMBOT
local AimbotEnabled = false
local AimbotTargetPart = "Head"
local AimbotFOV = 250
local AimbotStickyTarget = nil
local AimbotStickyType = nil
local AimbotTeamCheck = false
local AimbotWallCheck = false
local AimbotSmoothness = 1

local SilentAimEnabled = false
local AimKeybindEnabled = false
local AimKeybind = Enum.KeyCode.E
local AimKeyHeld = false
local TargetPriority = "Closest"
local OffScreenArrowEnabled = false

-- 👁️ ESP
local ESPEnabled = false
local ESPObjects = {}
local ChamsObjects = {}
local TracerColor = Color3.fromRGB(0, 150, 255)
local RainbowESPEnabled = false
local RainbowHue = 0

-- Anti-Kick (locked)
local AntiKickEnabled = true

-- FOV Circle (Draw)
local FOVCircle = nil
pcall(function()
    FOVCircle = Drawing.new("Circle")
    FOVCircle.Visible = false
    FOVCircle.Color = Color3.fromRGB(0, 150, 255)
    FOVCircle.Thickness = 2
    FOVCircle.Filled = false
    FOVCircle.Transparency = 1
    FOVCircle.NumSides = 90
end)

local OffScreenArrow = nil
pcall(function()
    OffScreenArrow = Drawing.new("Triangle")
    OffScreenArrow.Visible = false
    OffScreenArrow.Color = Color3.fromRGB(0, 150, 255)
    OffScreenArrow.Filled = true
    OffScreenArrow.Thickness = 2
    OffScreenArrow.Transparency = 1
end)

print("[ZET] State ready")

--==============================================================
-- NOTIFY
--==============================================================
local Notifications = Instance.new("Frame")
Notifications.Size = UDim2.new(0, 250, 1, 0)
Notifications.Position = UDim2.new(1, -260, 0, 10)
Notifications.BackgroundTransparency = 1
Notifications.ZIndex = 500
Notifications.Parent = ScreenGui

local function Notify(title, message, duration)
    duration = duration or 2
    local Notif = Instance.new("Frame")
    Notif.Size = UDim2.new(1, 0, 0, 55)
    Notif.Position = UDim2.new(0, 0, 0, -55)
    Notif.BackgroundColor3 = THEME.PanelBG
    Notif.BorderColor3 = THEME.Accent
    Notif.BorderSizePixel = 2
    Notif.ZIndex = 501
    Notif.Parent = Notifications
    Instance.new("UICorner", Notif).CornerRadius = UDim.new(0, 8)
    local T = Instance.new("TextLabel")
    T.Size = UDim2.new(1, -16, 0, 22)
    T.Position = UDim2.new(0, 8, 0, 4)
    T.BackgroundTransparency = 1
    T.Text = title
    T.TextColor3 = THEME.Text
    T.Font = Enum.Font.Code
    T.TextSize = 12
    T.TextXAlignment = Enum.TextXAlignment.Left
    T.ZIndex = 502
    T.Parent = Notif
    local M = Instance.new("TextLabel")
    M.Size = UDim2.new(1, -16, 0, 22)
    M.Position = UDim2.new(0, 8, 0, 28)
    M.BackgroundTransparency = 1
    M.Text = message
    M.TextColor3 = THEME.TextLight
    M.Font = Enum.Font.Code
    M.TextSize = 10
    M.TextXAlignment = Enum.TextXAlignment.Left
    M.ZIndex = 502
    M.Parent = Notif
    TweenService:Create(Notif, TweenInfo.new(0.3), {Position = UDim2.new(0, 0, 0, 0)}):Play()
    task.delay(duration, function()
        local tw = TweenService:Create(Notif, TweenInfo.new(0.3), {Position = UDim2.new(0, 0, 0, -55)})
        tw:Play()
        tw.Completed:Connect(function() Notif:Destroy() end)
    end)
end

--==============================================================
-- ANTI-KICK (LOCKED)
--==============================================================
local BlockedKeywords = {"exploit", "cheat", "hack", "aimbot", "ban", "detect", "script", "injector", "banned", "violation", "suspicious", "anti-cheat", "anticheat"}
local LegitKeywords = {"shutdown", "restart", "update", "maintenance", "rejoin"}

local function ActivateAntiKick()
    if IsHighSecurityGame() then
        Notify("🔒 VPN", "> AUTO ON (SAFE)", 3)
        return
    end
    pcall(function()
        if not _G._ZET_OrigKick then _G._ZET_OrigKick = LocalPlayer.Kick end
        LocalPlayer.Kick = function(self, message)
            if not AntiKickEnabled then return _G._ZET_OrigKick(self, message) end
            if not message then return end
            local msgLower = string.lower(tostring(message))
            for _, kw in ipairs(LegitKeywords) do
                if string.find(msgLower, kw, 1, true) then return _G._ZET_OrigKick(self, message) end
            end
            for _, kw in ipairs(BlockedKeywords) do
                if string.find(msgLower, kw, 1, true) then
                    Notify("🔒 VPN", "> Blocked: " .. kw, 3)
                    return
                end
            end
            return _G._ZET_OrigKick(self, message)
        end
    end)
    Notify("🔒 VPN", "> ACTIVE (SAFE)", 2)
end

--==============================================================
-- FOV LOOP
--==============================================================
local function EnableFOVLoop()
    DisconnectKey("FOV")
    local conn = RunService.RenderStepped:Connect(function()
        if not FOVCircle then return end
        if not FOVCircleEnabled or not LocalPlayer.Character then
            pcall(function() FOVCircle.Visible = false end)
            return
        end
        pcall(function()
            FOVCircle.Position = Vector2.new(Camera.ViewportSize.X/2, Camera.ViewportSize.Y/2)
            FOVCircle.Radius = AimbotFOV
            FOVCircle.Color = THEME.Accent
            FOVCircle.Visible = true
        end)
    end)
    ActiveConnections["FOV"] = conn
end

local function DisableFOVLoop()
    DisconnectKey("FOV")
    if FOVCircle then pcall(function() FOVCircle.Visible = false end) end
end

local FOVCircleEnabled = false

--==============================================================
-- OFF-SCREEN ARROW
--==============================================================
local function EnableOffScreenArrow()
    DisconnectKey("OffScreenArrow")
    local conn = RunService.RenderStepped:Connect(function()
        if not OffScreenArrow then return end
        if not OffScreenArrowEnabled or not LocalPlayer.Character then
            pcall(function() OffScreenArrow.Visible = false end)
            return
        end
        local nearest, nearestDist = nil, math.huge
        local myPos = LocalPlayer.Character:FindFirstChild("HumanoidRootPart") and LocalPlayer.Character.HumanoidRootPart.Position
        if not myPos then return end
        for _, player in pairs(Players:GetPlayers()) do
            if player ~= LocalPlayer and player.Character and player.Character:FindFirstChild("HumanoidRootPart") then
                local d = (player.Character.HumanoidRootPart.Position - myPos).Magnitude
                if d < nearestDist then nearest = player; nearestDist = d end
            end
        end
        if nearest then
            local root = nearest.Character:FindFirstChild("HumanoidRootPart")
            if root then
                local sp, onScreen = Camera:WorldToViewportPoint(root.Position)
                if not onScreen then
                    local dir = (root.Position - Camera.CFrame.Position).Unit
                    local camDir = Camera.CFrame.LookVector
                    local angle = math.atan2(dir.X, dir.Z) - math.atan2(camDir.X, camDir.Z)
                    local vpSize = Camera.ViewportSize
                    local center = Vector2.new(vpSize.X/2, vpSize.Y/2)
                    local radius = math.min(vpSize.X, vpSize.Y) / 2 - 60
                    local px = center.X + math.sin(angle) * radius
                    local py = center.Y - math.cos(angle) * radius
                    pcall(function()
                        OffScreenArrow.PointA = Vector2.new(px, py - 15)
                        OffScreenArrow.PointB = Vector2.new(px - 10, py + 5)
                        OffScreenArrow.PointC = Vector2.new(px + 10, py + 5)
                        OffScreenArrow.Color = THEME.Accent
                        OffScreenArrow.Visible = true
                    end)
                else
                    pcall(function() OffScreenArrow.Visible = false end)
                end
            end
        else
            pcall(function() OffScreenArrow.Visible = false end)
        end
    end)
    ActiveConnections["OffScreenArrow"] = conn
end

local function DisableOffScreenArrow()
    DisconnectKey("OffScreenArrow")
    if OffScreenArrow then pcall(function() OffScreenArrow.Visible = false end) end
end

--==============================================================
-- ESP
--==============================================================
local function HSVToRGB(h, s, v)
    local r, g, b
    local i = math.floor(h * 6)
    local f = h * 6 - i
    local p = v * (1 - s)
    local q = v * (1 - f * s)
    local t = v * (1 - (1 - f) * s)
    i = i % 6
    if i == 0 then r, g, b = v, t, p
    elseif i == 1 then r, g, b = q, v, p
    elseif i == 2 then r, g, b = p, v, t
    elseif i == 3 then r, g, b = p, q, v
    elseif i == 4 then r, g, b = t, p, v
    elseif i == 5 then r, g, b = v, p, q
    end
    return Color3.new(r, g, b)
end

local function EnableRainbowESP()
    DisconnectKey("Rainbow")
    local conn = RunService.RenderStepped:Connect(function(dt)
        if not RainbowESPEnabled then return end
        RainbowHue = (RainbowHue + dt * 0.3) % 1
        local c = HSVToRGB(RainbowHue, 1, 1)
        for _, d in pairs(ESPObjects) do
            if d.Box then d.Box.Color = c end
            if d.Name then d.Name.Color = c end
            if d.Distance then d.Distance.Color = c end
            if d.Tracer then d.Tracer.Color = c end
            if d.HealthBar then d.HealthBar.Color = c end
        end
    end)
    ActiveConnections["Rainbow"] = conn
end

local function DisableRainbowESP() DisconnectKey("Rainbow"); RainbowESPEnabled = false end

local function CreateESP(player)
    if ESPObjects[player] then return end
    if not Drawing then return end
    local d = {}
    d.Box = Drawing.new("Square"); d.Box.Visible = false; d.Box.Color = THEME.Accent; d.Box.Thickness = 2; d.Box.Filled = false; d.Box.Transparency = 1
    d.Name = Drawing.new("Text"); d.Name.Visible = false; d.Name.Color = THEME.Accent; d.Name.Size = 12; d.Name.Center = true; d.Name.Outline = true; d.Name.OutlineColor = Color3.fromRGB(0,0,0)
    d.Distance = Drawing.new("Text"); d.Distance.Visible = false; d.Distance.Color = THEME.Accent; d.Distance.Size = 10; d.Distance.Center = true; d.Distance.Outline = true; d.Distance.OutlineColor = Color3.fromRGB(0,0,0)
    d.HealthBg = Drawing.new("Line"); d.HealthBg.Visible = false; d.HealthBg.Color = Color3.fromRGB(0,50,100); d.HealthBg.Thickness = 3
    d.HealthBar = Drawing.new("Line"); d.HealthBar.Visible = false; d.HealthBar.Color = THEME.Accent; d.HealthBar.Thickness = 3
    d.Tracer = Drawing.new("Line"); d.Tracer.Visible = false; d.Tracer.Color = TracerColor; d.Tracer.Thickness = 2; d.Tracer.Transparency = 0.5
    ESPObjects[player] = d
end

local function RemoveESP(player)
    if ESPObjects[player] then
        local d = ESPObjects[player]
        for _, v in pairs(d) do pcall(function() v:Remove() end) end
        ESPObjects[player] = nil
    end
    if ChamsObjects[player] then
        for _, h in pairs(ChamsObjects[player]) do pcall(function() if h then h:Destroy() end end) end
        ChamsObjects[player] = nil
    end
end

local function CreateChams(player)
    if ChamsObjects[player] or not player.Character then return end
    ChamsObjects[player] = {}
    for _, part in pairs(player.Character:GetChildren()) do
        if part:IsA("BasePart") or part:IsA("MeshPart") then
            local h = Instance.new("Highlight")
            h.Adornee = part
            h.FillColor = THEME.Accent
            h.FillTransparency = 0.7
            h.OutlineColor = THEME.AccentLight
            h.OutlineTransparency = 0
            h.DepthMode = Enum.HighlightDepthMode.AlwaysOnTop
            h.Parent = part
            table.insert(ChamsObjects[player], h)
        end
    end
end

local function RemoveChams(player)
    if ChamsObjects[player] then
        for _, h in pairs(ChamsObjects[player]) do pcall(function() if h then h:Destroy() end end) end
        ChamsObjects[player] = nil
    end
end

local function UpdateESP()
    if not ESPEnabled then
        for _, d in pairs(ESPObjects) do
            for _, v in pairs(d) do pcall(function() v.Visible = false end) end
        end
        return
    end
    for _, player in pairs(Players:GetPlayers()) do
        if player ~= LocalPlayer and player.Character and player.Character:FindFirstChild("HumanoidRootPart") and player.Character:FindFirstChild("Humanoid") then
            local hum = player.Character.Humanoid
            local root = player.Character.HumanoidRootPart
            if hum.Health > 0 and root then
                if not ESPObjects[player] then CreateESP(player) end
                local d = ESPObjects[player]
                if not d then continue end
                local sp, on = Camera:WorldToViewportPoint(root.Position)
                if on then
                    local dist = (root.Position - Camera.CFrame.Position).Magnitude
                    local bSize = Vector2.new(2000/dist, 3500/dist)
                    local bX, bY = sp.X - bSize.X/2, sp.Y - bSize.Y/2
                    d.Box.Visible = true
                    d.Box.Position = Vector2.new(bX, bY)
                    d.Box.Size = bSize
                    d.Name.Visible = true
                    d.Name.Text = player.Name
                    d.Name.Position = Vector2.new(sp.X, bY-15)
                    d.Distance.Visible = true
                    d.Distance.Text = math.floor(dist).."m"
                    d.Distance.Position = Vector2.new(sp.X, bY+bSize.Y+5)
                    local hp = hum.Health / hum.MaxHealth
                    d.HealthBg.Visible = true
                    d.HealthBg.From = Vector2.new(bX, bY+bSize.Y+20)
                    d.HealthBg.To = Vector2.new(bX+bSize.X, bY+bSize.Y+20)
                    d.HealthBar.Visible = true
                    d.HealthBar.From = Vector2.new(bX, bY+bSize.Y+20)
                    d.HealthBar.To = Vector2.new(bX+bSize.X*hp, bY+bSize.Y+20)
                    d.Tracer.Visible = true
                    if not RainbowESPEnabled then d.Tracer.Color = TracerColor end
                    d.Tracer.From = Vector2.new(Camera.ViewportSize.X/2, Camera.ViewportSize.Y)
                    d.Tracer.To = Vector2.new(sp.X, sp.Y)
                    if not ChamsObjects[player] then CreateChams(player) end
                else
                    for _, v in pairs(d) do pcall(function() v.Visible = false end) end
                end
            else RemoveESP(player) end
        else RemoveESP(player) end
    end
end

local function EnableESPLoop()
    DisconnectKey("ESPLoop")
    local conn = RunService.RenderStepped:Connect(UpdateESP)
    ActiveConnections["ESPLoop"] = conn
end

local function DisableESPLoop()
    DisconnectKey("ESPLoop")
    ESPEnabled = false
    for _, d in pairs(ESPObjects) do
        for _, v in pairs(d) do pcall(function() v.Visible = false end) end
    end
    for p, _ in pairs(ChamsObjects) do RemoveChams(p) end
end

--==============================================================
-- AIMBOT
--==============================================================
local function IsSameTeam(player)
    if not AimbotTeamCheck then return false end
    if LocalPlayer.Team and player.Team and LocalPlayer.Team == player.Team then return true end
    return false
end

local function HasWallBetween(camPos, targetPos, targetChar)
    if not AimbotWallCheck then return false end
    local dir = targetPos - camPos
    local dist = dir.Magnitude
    if dist < 1 then return false end
    local rp = RaycastParams.new()
    rp.FilterType = Enum.RaycastFilterType.Blacklist
    rp.FilterDescendantsInstances = {LocalPlayer.Character, targetChar}
    local result = workspace:Raycast(camPos, dir.Unit * dist, rp)
    return result ~= nil
end

local function FindTarget()
    local bestTarget, bestScore = nil, math.huge
    local screenCenter = Vector2.new(Camera.ViewportSize.X/2, Camera.ViewportSize.Y/2)
    local camPos = Camera.CFrame.Position
    for _, player in pairs(Players:GetPlayers()) do
        if player ~= LocalPlayer and player.Character then
            local hum = player.Character:FindFirstChild("Humanoid")
            local root = player.Character:FindFirstChild("HumanoidRootPart")
            if hum and root and hum.Health > 0 and not IsSameTeam(player) then
                local part = player.Character:FindFirstChild(AimbotTargetPart) or root
                if part and not HasWallBetween(camPos, part.Position, player.Character) then
                    local sp, on = Camera:WorldToViewportPoint(part.Position)
                    if on then
                        local screenDist = (Vector2.new(sp.X, sp.Y) - screenCenter).Magnitude
                        local hp = hum.Health / hum.MaxHealth
                        local score = screenDist
                        if TargetPriority == "Lowest" then score = hp
                        elseif TargetPriority == "Farthest" then score = -screenDist end
                        if screenDist <= AimbotFOV and score < bestScore then
                            bestTarget = player; bestScore = score
                        end
                    end
                end
            end
        end
    end
    return bestTarget
end

local function IsTargetValid(target)
    if not target or not target.Parent or not target.Character then return false end
    local hum = target.Character:FindFirstChild("Humanoid")
    return hum and hum.Health > 0
end

local function GetTargetPart(target)
    if not target or not target.Character then return nil end
    return target.Character:FindFirstChild(AimbotTargetPart) or target.Character:FindFirstChild("HumanoidRootPart")
end

local function RunAimbot()
    if not AimbotEnabled then return end
    if AimKeybindEnabled and not AimKeyHeld then return end
    local char = LocalPlayer.Character
    if not char or not char:FindFirstChild("HumanoidRootPart") then return end
    if AimbotStickyTarget and IsTargetValid(AimbotStickyTarget) then
        if AimbotWallCheck then
            local tPart = GetTargetPart(AimbotStickyTarget)
            if tPart and HasWallBetween(Camera.CFrame.Position, tPart.Position, AimbotStickyTarget.Character) then
                AimbotStickyTarget = nil
            end
        end
    else
        AimbotStickyTarget = nil
    end
    if not AimbotStickyTarget then
        AimbotStickyTarget = FindTarget()
    end
    if not AimbotStickyTarget then return end
    if not IsTargetValid(AimbotStickyTarget) then
        AimbotStickyTarget = nil; return
    end
    local targetPart = GetTargetPart(AimbotStickyTarget)
    if not targetPart then return end
    local camPos = Camera.CFrame.Position
    local dir = (targetPart.Position - camPos).Unit
    if SilentAimEnabled then
        pcall(function()
            if LocalPlayer.Character and LocalPlayer.Character:FindFirstChildOfClass("Tool") then
                LocalPlayer.Character:FindFirstChildOfClass("Tool"):Activate()
            end
        end)
    else
        local newCF = CFrame.new(camPos, camPos + dir)
        local smooth = math.clamp(AimbotSmoothness, 1, 20)
        if smooth <= 1 then Camera.CFrame = newCF
        else Camera.CFrame = Camera.CFrame:Lerp(newCF, 1/smooth) end
    end
end

local function EnableAimbotLoop()
    DisconnectKey("Aimbot")
    local conn = RunService.RenderStepped:Connect(function()
        if AimbotEnabled then RunAimbot() end
    end)
    ActiveConnections["Aimbot"] = conn
end

--==============================================================
-- INPUT
--==============================================================
UserInputService.InputBegan:Connect(function(input, gp)
    if gp then return end
    if AimKeybindEnabled and input.KeyCode == AimKeybind then AimKeyHeld = true end
end)

UserInputService.InputEnded:Connect(function(input, gp)
    if input.KeyCode == AimKeybind then AimKeyHeld = false end
end)

--==============================================================
-- UI BUILDER
--==============================================================
local function CreateUI()
    print("[ZET] Creating UI...")

    -- LOADING
    local LoadingScreen = Instance.new("Frame")
    LoadingScreen.Name = "LoadingScreen"
    LoadingScreen.Size = UDim2.new(1, 0, 1, 0)
    LoadingScreen.Position = UDim2.new(0, 0, 0, 0)
    LoadingScreen.BackgroundColor3 = Color3.fromRGB(0, 3, 10)
    LoadingScreen.BorderSizePixel = 0
    LoadingScreen.ZIndex = 500
    LoadingScreen.Parent = ScreenGui

    local LoadingBg = Instance.new("Frame")
    LoadingBg.Size = UDim2.new(0, 400, 0, 240)
    LoadingBg.Position = UDim2.new(0.5, -200, 0.5, -120)
    LoadingBg.BackgroundColor3 = THEME.MainBG
    LoadingBg.BorderColor3 = THEME.Accent
    LoadingBg.BorderSizePixel = 2
    LoadingBg.ZIndex = 502
    LoadingBg.Parent = LoadingScreen
    Instance.new("UICorner", LoadingBg).CornerRadius = UDim.new(0, 12)

    local LTitle = Instance.new("TextLabel")
    LTitle.Size = UDim2.new(1, -20, 0, 36)
    LTitle.Position = UDim2.new(0, 10, 0, 20)
    LTitle.BackgroundTransparency = 1
    LTitle.Text = "ZETGAMES V4.4 PREMIUM"
    LTitle.TextColor3 = THEME.Accent
    LTitle.Font = Enum.Font.Code
    LTitle.TextSize = 20
    LTitle.ZIndex = 503
    LTitle.Parent = LoadingBg

    local LTag = Instance.new("TextLabel")
    LTag.Size = UDim2.new(1, -20, 0, 20)
    LTag.Position = UDim2.new(0, 10, 0, 58)
    LTag.BackgroundTransparency = 1
    LTag.Text = "[ PREMIUM EDITION V4.4 ]"
    LTag.TextColor3 = THEME.Gold
    LTag.Font = Enum.Font.Code
    LTag.TextSize = 10
    LTag.ZIndex = 503
    LTag.Parent = LoadingBg

    local LStatus = Instance.new("TextLabel")
    LStatus.Size = UDim2.new(1, -20, 0, 20)
    LStatus.Position = UDim2.new(0, 10, 0, 88)
    LStatus.BackgroundTransparency = 1
    LStatus.Text = "> Menginisialisasi sistem..."
    LStatus.TextColor3 = THEME.TextLight
    LStatus.Font = Enum.Font.Code
    LStatus.TextSize = 11
    LStatus.TextXAlignment = Enum.TextXAlignment.Left
    LStatus.ZIndex = 503
    LStatus.Parent = LoadingBg

    local LBarBg = Instance.new("Frame")
    LBarBg.Size = UDim2.new(1, -20, 0, 18)
    LBarBg.Position = UDim2.new(0, 10, 0, 120)
    LBarBg.BackgroundColor3 = Color3.fromRGB(10, 25, 40)
    LBarBg.BorderColor3 = THEME.Accent
    LBarBg.BorderSizePixel = 1
    LBarBg.ZIndex = 503
    LBarBg.Parent = LoadingBg
    Instance.new("UICorner", LBarBg).CornerRadius = UDim.new(0, 9)

    local LBarFill = Instance.new("Frame")
    LBarFill.Size = UDim2.new(0, 0, 1, 0)
    LBarFill.BackgroundColor3 = THEME.Accent
    LBarFill.BorderSizePixel = 0
    LBarFill.ZIndex = 504
    LBarFill.Parent = LBarBg
    Instance.new("UICorner", LBarFill).CornerRadius = UDim.new(0, 9)

    local LPercent = Instance.new("TextLabel")
    LPercent.Size = UDim2.new(1, -20, 0, 22)
    LPercent.Position = UDim2.new(0, 10, 0, 148)
    LPercent.BackgroundTransparency = 1
    LPercent.Text = "0%"
    LPercent.TextColor3 = THEME.Text
    LPercent.Font = Enum.Font.Code
    LPercent.TextSize = 13
    LPercent.ZIndex = 503
    LPercent.Parent = LoadingBg

    local LTimeLeft = Instance.new("TextLabel")
    LTimeLeft.Size = UDim2.new(1, -20, 0, 20)
    LTimeLeft.Position = UDim2.new(0, 10, 0, 178)
    LTimeLeft.BackgroundTransparency = 1
    LTimeLeft.Text = "Waktu tersisa: 10 detik"
    LTimeLeft.TextColor3 = THEME.TextLight
    LTimeLeft.Font = Enum.Font.Code
    LTimeLeft.TextSize = 10
    LTimeLeft.ZIndex = 503
    LTimeLeft.Parent = LoadingBg

    local LVersion = Instance.new("TextLabel")
    LVersion.Size = UDim2.new(1, -20, 0, 18)
    LVersion.Position = UDim2.new(0, 10, 0, 205)
    LVersion.BackgroundTransparency = 1
    LVersion.Text = "V4.4 PREMIUM | rscripts.net/@ZetGames"
    LVersion.TextColor3 = THEME.Gold
    LVersion.Font = Enum.Font.Code
    LVersion.TextSize = 9
    LVersion.ZIndex = 503
    LVersion.Parent = LoadingBg

    -- LOGIN FRAME
    local LoginFrame = Instance.new("Frame")
    LoginFrame.Size = UDim2.new(0, 320, 0, 400)
    LoginFrame.Position = UDim2.new(0.5, -160, 0.5, -200)
    LoginFrame.BackgroundColor3 = THEME.MainBG
    LoginFrame.BorderColor3 = THEME.Accent
    LoginFrame.BorderSizePixel = 2
    LoginFrame.Visible = false
    LoginFrame.ZIndex = 100
    LoginFrame.Parent = ScreenGui
    Instance.new("UICorner", LoginFrame).CornerRadius = UDim.new(0, 10)

    local LTopBar = Instance.new("Frame")
    LTopBar.Size = UDim2.new(1, 0, 0, 35)
    LTopBar.BackgroundColor3 = THEME.SectionBG
    LTopBar.BorderSizePixel = 0
    LTopBar.ZIndex = 101
    LTopBar.Parent = LoginFrame
    Instance.new("UICorner", LTopBar).CornerRadius = UDim.new(0, 10)

    local LTopTxt = Instance.new("TextLabel")
    LTopTxt.Size = UDim2.new(1, -16, 1, 0)
    LTopTxt.Position = UDim2.new(0, 8, 0, 0)
    LTopTxt.BackgroundTransparency = 1
    LTopTxt.Text = "● ZETGAMES V4.4 PREMIUM"
    LTopTxt.TextColor3 = THEME.Accent
    LTopTxt.Font = Enum.Font.Code
    LTopTxt.TextSize = 11
    LTopTxt.TextXAlignment = Enum.TextXAlignment.Left
    LTopTxt.ZIndex = 102
    LTopTxt.Parent = LTopBar

    local LTitle2 = Instance.new("TextLabel")
    LTitle2.Size = UDim2.new(1, -30, 0, 30)
    LTitle2.Position = UDim2.new(0, 15, 0, 50)
    LTitle2.BackgroundTransparency = 1
    LTitle2.Text = "> ACCESS VERIFICATION"
    LTitle2.TextColor3 = THEME.Text
    LTitle2.Font = Enum.Font.Code
    LTitle2.TextSize = 16
    LTitle2.ZIndex = 102
    LTitle2.Parent = LoginFrame

    local LTag2 = Instance.new("TextLabel")
    LTag2.Size = UDim2.new(1, -30, 0, 18)
    LTag2.Position = UDim2.new(0, 15, 0, 82)
    LTag2.BackgroundTransparency = 1
    LTag2.Text = "[ PREMIUM + VPN AUTO-ON ]"
    LTag2.TextColor3 = THEME.Gold
    LTag2.Font = Enum.Font.Code
    LTag2.TextSize = 9
    LTag2.TextXAlignment = Enum.TextXAlignment.Left
    LTag2.ZIndex = 102
    LTag2.Parent = LoginFrame

    local KeyLbl = Instance.new("TextLabel")
    KeyLbl.Size = UDim2.new(1, -30, 0, 18)
    KeyLbl.Position = UDim2.new(0, 15, 0, 108)
    KeyLbl.BackgroundTransparency = 1
    KeyLbl.Text = "> KEY_INPUT:"
    KeyLbl.TextColor3 = THEME.Text
    KeyLbl.Font = Enum.Font.Code
    KeyLbl.TextSize = 12
    KeyLbl.TextXAlignment = Enum.TextXAlignment.Left
    KeyLbl.ZIndex = 102
    KeyLbl.Parent = LoginFrame

    local KeyInput = Instance.new("TextBox")
    KeyInput.Size = UDim2.new(1, -30, 0, 40)
    KeyInput.Position = UDim2.new(0, 15, 0, 130)
    KeyInput.BackgroundColor3 = THEME.PanelBG
    KeyInput.BorderColor3 = THEME.Accent
    KeyInput.BorderSizePixel = 2
    KeyInput.PlaceholderText = "> Type key..."
    KeyInput.PlaceholderColor3 = Color3.fromRGB(50, 80, 100)
    KeyInput.Text = ""
    KeyInput.TextColor3 = THEME.Text
    KeyInput.Font = Enum.Font.Code
    KeyInput.TextSize = 13
    KeyInput.ClearTextOnFocus = false
    KeyInput.ZIndex = 102
    KeyInput.Parent = LoginFrame
    Instance.new("UICorner", KeyInput).CornerRadius = UDim.new(0, 5)

    local LoginBtn = Instance.new("TextButton")
    LoginBtn.Size = UDim2.new(1, -30, 0, 45)
    LoginBtn.Position = UDim2.new(0, 15, 0, 185)
    LoginBtn.BackgroundColor3 = THEME.ButtonActive
    LoginBtn.BorderColor3 = THEME.Accent
    LoginBtn.BorderSizePixel = 2
    LoginBtn.Text = "> AUTHENTICATE"
    LoginBtn.TextColor3 = Color3.fromRGB(255, 255, 255)
    LoginBtn.Font = Enum.Font.Code
    LoginBtn.TextSize = 14
    LoginBtn.ZIndex = 102
    LoginBtn.Parent = LoginFrame
    Instance.new("UICorner", LoginBtn).CornerRadius = UDim.new(0, 5)

    local GetKeyBtn = Instance.new("TextButton")
    GetKeyBtn.Size = UDim2.new(1, -30, 0, 45)
    GetKeyBtn.Position = UDim2.new(0, 15, 0, 240)
    GetKeyBtn.BackgroundColor3 = Color3.fromRGB(0, 60, 120)
    GetKeyBtn.BorderColor3 = THEME.AccentDark
    GetKeyBtn.BorderSizePixel = 2
    GetKeyBtn.Text = "> GET KEY"
    GetKeyBtn.TextColor3 = THEME.TextLight
    GetKeyBtn.Font = Enum.Font.Code
    GetKeyBtn.TextSize = 14
    GetKeyBtn.ZIndex = 102
    GetKeyBtn.Parent = LoginFrame
    Instance.new("UICorner", GetKeyBtn).CornerRadius = UDim.new(0, 5)

    local StatusTxt = Instance.new("TextLabel")
    StatusTxt.Size = UDim2.new(1, -30, 0, 25)
    StatusTxt.Position = UDim2.new(0, 15, 0, 295)
    StatusTxt.BackgroundTransparency = 1
    StatusTxt.Text = "> SYSTEM READY..."
    StatusTxt.TextColor3 = THEME.Text
    StatusTxt.Font = Enum.Font.Code
    StatusTxt.TextSize = 10
    StatusTxt.TextXAlignment = Enum.TextXAlignment.Left
    StatusTxt.ZIndex = 102
    StatusTxt.Parent = LoginFrame

    local Instr = Instance.new("TextLabel")
    Instr.Size = UDim2.new(1, -30, 0, 60)
    Instr.Position = UDim2.new(0, 15, 0, 325)
    Instr.BackgroundTransparency = 1
    Instr.Text = "> STEPS:\n> 1. Klik GET KEY\n> 2. Ambil key di website\n> 3. Masukkan key\n> 4. AUTHENTICATE"
    Instr.TextColor3 = THEME.TextLight
    Instr.Font = Enum.Font.Code
    Instr.TextSize = 9
    Instr.TextXAlignment = Enum.TextXAlignment.Left
    Instr.TextYAlignment = Enum.TextYAlignment.Top
    Instr.ZIndex = 102
    Instr.Parent = LoginFrame

    -- MAIN HUB
    local MainHub = Instance.new("Frame")
    MainHub.Size = UDim2.new(0, 360, 0, 500)
    MainHub.Position = UDim2.new(0.5, -180, 0.5, -250)
    MainHub.BackgroundColor3 = THEME.MainBG
    MainHub.BorderColor3 = THEME.Accent
    MainHub.BorderSizePixel = 2
    MainHub.Visible = false
    MainHub.ZIndex = 100
    MainHub.Parent = ScreenGui
    Instance.new("UICorner", MainHub).CornerRadius = UDim.new(0, 10)

    local TitleBar = Instance.new("Frame")
    TitleBar.Size = UDim2.new(1, 0, 0, 38)
    TitleBar.BackgroundColor3 = THEME.SectionBG
    TitleBar.BorderSizePixel = 0
    TitleBar.ZIndex = 101
    TitleBar.Parent = MainHub
    Instance.new("UICorner", TitleBar).CornerRadius = UDim.new(0, 10)

    local TitleText = Instance.new("TextLabel")
    TitleText.Size = UDim2.new(1, -50, 1, 0)
    TitleText.Position = UDim2.new(0, 10, 0, 0)
    TitleText.BackgroundTransparency = 1
    TitleText.Text = "● V4.4 PREMIUM [VPN ON]"
    TitleText.TextColor3 = THEME.Gold
    TitleText.Font = Enum.Font.Code
    TitleText.TextSize = 10
    TitleText.TextXAlignment = Enum.TextXAlignment.Left
    TitleText.ZIndex = 102
    TitleText.Parent = TitleBar

    local CloseBtn = Instance.new("TextButton")
    CloseBtn.Size = UDim2.new(0, 28, 0, 28)
    CloseBtn.Position = UDim2.new(1, -34, 0, 5)
    CloseBtn.BackgroundColor3 = Color3.fromRGB(0, 80, 160)
    CloseBtn.BorderColor3 = THEME.Accent
    CloseBtn.BorderSizePixel = 1
    CloseBtn.Text = "X"
    CloseBtn.TextColor3 = Color3.fromRGB(255, 255, 255)
    CloseBtn.Font = Enum.Font.Code
    CloseBtn.TextSize = 14
    CloseBtn.ZIndex = 103
    CloseBtn.Parent = TitleBar
    Instance.new("UICorner", CloseBtn).CornerRadius = UDim.new(0, 14)

    local ScrollFrame = Instance.new("ScrollingFrame")
    ScrollFrame.Size = UDim2.new(1, 0, 1, -38)
    ScrollFrame.Position = UDim2.new(0, 0, 0, 38)
    ScrollFrame.BackgroundTransparency = 1
    ScrollFrame.BorderSizePixel = 0
    ScrollFrame.ScrollBarThickness = 6
    ScrollFrame.ScrollBarImageColor3 = THEME.Accent
    ScrollFrame.CanvasSize = UDim2.new(0, 0, 0, 1500)
    ScrollFrame.ScrollingEnabled = true
    ScrollFrame.ElasticBehavior = Enum.ElasticBehavior.WhenScrollable
    ScrollFrame.ZIndex = 101
    ScrollFrame.Parent = MainHub

    local ScrollContent = Instance.new("Frame")
    ScrollContent.Size = UDim2.new(1, 0, 0, 1500)
    ScrollContent.BackgroundTransparency = 1
    ScrollContent.ZIndex = 101
    ScrollContent.Parent = ScrollFrame

    local function Section(title, y)
        local f = Instance.new("Frame")
        f.Size = UDim2.new(1, -20, 0, 26)
        f.Position = UDim2.new(0, 10, 0, y)
        f.BackgroundColor3 = THEME.SectionBG
        f.BorderColor3 = THEME.Accent
        f.BorderSizePixel = 1
        f.ZIndex = 102
        f.Parent = ScrollContent
        Instance.new("UICorner", f).CornerRadius = UDim.new(0, 4)
        local t = Instance.new("TextLabel")
        t.Size = UDim2.new(1, -10, 1, 0)
        t.Position = UDim2.new(0, 6, 0, 0)
        t.BackgroundTransparency = 1
        t.Text = title
        t.TextColor3 = THEME.Text
        t.Font = Enum.Font.Code
        t.TextSize = 11
        t.TextXAlignment = Enum.TextXAlignment.Left
        t.ZIndex = 103
        t.Parent = f
    end

    local function Toggle(text, y, callback)
        local btn = Instance.new("TextButton")
        btn.Size = UDim2.new(1, -20, 0, 36)
        btn.Position = UDim2.new(0, 10, 0, y)
        btn.BackgroundColor3 = THEME.ButtonBG
        btn.BorderColor3 = THEME.Accent
        btn.BorderSizePixel = 1
        btn.Text = text
        btn.TextColor3 = THEME.Text
        btn.Font = Enum.Font.Code
        btn.TextSize = 11
        btn.ZIndex = 102
        btn.Parent = ScrollContent
        Instance.new("UICorner", btn).CornerRadius = UDim.new(0, 4)
        btn.MouseButton1Click:Connect(function() callback(btn) end)
        return btn
    end

    local function LockedToggle(text, y)
        local btn = Instance.new("TextButton")
        btn.Size = UDim2.new(1, -20, 0, 36)
        btn.Position = UDim2.new(0, 10, 0, y)
        btn.BackgroundColor3 = THEME.LockedBG
        btn.BorderColor3 = THEME.Locked
        btn.BorderSizePixel = 1
        btn.Text = text
        btn.TextColor3 = THEME.Locked
        btn.Font = Enum.Font.Code
        btn.TextSize = 11
        btn.ZIndex = 102
        btn.Parent = ScrollContent
        Instance.new("UICorner", btn).CornerRadius = UDim.new(0, 4)
        btn.MouseButton1Click:Connect(function() Notify("🔒 VPN Locked", "> Tidak bisa dimatiin (Anti-Ban)", 2) end)
        return btn
    end

    local function Input(placeholder, y, defaultText)
        local tb = Instance.new("TextBox")
        tb.Size = UDim2.new(1, -20, 0, 30)
        tb.Position = UDim2.new(0, 10, 0, y)
        tb.BackgroundColor3 = THEME.PanelBG
        tb.BorderColor3 = THEME.Accent
        tb.BorderSizePixel = 1
        tb.PlaceholderText = placeholder
        tb.PlaceholderColor3 = Color3.fromRGB(50, 80, 100)
        tb.Text = defaultText or ""
        tb.TextColor3 = THEME.Text
        tb.Font = Enum.Font.Code
        tb.TextSize = 11
        tb.ZIndex = 102
        tb.Parent = ScrollContent
        Instance.new("UICorner", tb).CornerRadius = UDim.new(0, 4)
        return tb
    end

    local function Half(text, y, xPos, callback)
        local b = Instance.new("TextButton")
        b.Size = UDim2.new(0.5, -15, 0, 30)
        b.Position = UDim2.new(xPos, 0, 0, y)
        b.BackgroundColor3 = THEME.ButtonBG
        b.BorderColor3 = THEME.Accent
        b.BorderSizePixel = 1
        b.Text = text
        b.TextColor3 = THEME.Text
        b.Font = Enum.Font.Code
        b.TextSize = 10
        b.ZIndex = 102
        b.Parent = ScrollContent
        Instance.new("UICorner", b).CornerRadius = UDim.new(0, 4)
        b.MouseButton1Click:Connect(function() callback(b) end)
        return b
    end

    -- ═══════════════ VPN SECTION (LOCKED) ═══════════════
    Section("=== 🔒 VPN AUTO-PROTECT ===", 10)
    LockedToggle("> 🔒 VPN: ON (LOCKED - ANTI BAN)", 42)

    -- ═══════════════ AIMBOT SECTION ═══════════════
    Section("=== 🎯 AIMBOT ===", 90)

    local AimbotBtn = Instance.new("TextButton")
    AimbotBtn.Size = UDim2.new(1, -20, 0, 42)
    AimbotBtn.Position = UDim2.new(0, 10, 0, 122)
    AimbotBtn.BackgroundColor3 = THEME.ButtonBG
    AimbotBtn.BorderColor3 = THEME.Accent
    AimbotBtn.BorderSizePixel = 2
    AimbotBtn.Text = "> AIMBOT: OFF"
    AimbotBtn.TextColor3 = THEME.Text
    AimbotBtn.Font = Enum.Font.Code
    AimbotBtn.TextSize = 13
    AimbotBtn.ZIndex = 102
    AimbotBtn.Parent = ScrollContent
    Instance.new("UICorner", AimbotBtn).CornerRadius = UDim.new(0, 5)
    AimbotBtn.MouseButton1Click:Connect(function()
        AimbotEnabled = not AimbotEnabled
        if AimbotEnabled then
            AimbotBtn.Text = "> AIMBOT: ON"
            AimbotBtn.BackgroundColor3 = THEME.ButtonActive
            EnableAimbotLoop()
        else
            AimbotBtn.Text = "> AIMBOT: OFF"
            AimbotBtn.BackgroundColor3 = THEME.ButtonBG
            AimbotStickyTarget = nil
            DisconnectKey("Aimbot")
        end
    end)

    Toggle("> 🎯 SILENT AIM: OFF", 174, function(btn)
        SilentAimEnabled = not SilentAimEnabled
        btn.Text = SilentAimEnabled and "> 🎯 SILENT AIM: ON" or "> 🎯 SILENT AIM: OFF"
        btn.BackgroundColor3 = SilentAimEnabled and THEME.ButtonActive or THEME.ButtonBG
    end)

    Half("> FOV: OFF", 214, 0, function(btn)
        FOVCircleEnabled = not FOVCircleEnabled
        btn.Text = FOVCircleEnabled and "> FOV: ON" or "> FOV: OFF"
        btn.BackgroundColor3 = FOVCircleEnabled and THEME.ButtonActive or THEME.ButtonBG
        if FOVCircleEnabled then EnableFOVLoop() else DisableFOVLoop() end
    end)
    Half("> TEAM: OFF", 214, 0.5, function(btn)
        AimbotTeamCheck = not AimbotTeamCheck
        btn.Text = AimbotTeamCheck and "> TEAM: ON" or "> TEAM: OFF"
        btn.BackgroundColor3 = AimbotTeamCheck and THEME.ButtonActive or THEME.ButtonBG
    end)

    local FOVInput = Input("> FOV Radius (50-5000)", 252, tostring(AimbotFOV))
    FOVInput.FocusLost:Connect(function(enterPressed)
        if enterPressed then
            local nf = tonumber(FOVInput.Text)
            if nf then AimbotFOV = math.clamp(nf, 50, 5000) end
            FOVInput.Text = tostring(AimbotFOV)
        end
    end)

    Toggle("> KEYBIND AIMBOT (E): OFF", 288, function(btn)
        AimKeybindEnabled = not AimKeybindEnabled
        btn.Text = AimKeybindEnabled and "> KEYBIND (E): ON" or "> KEYBIND (E): OFF"
        btn.BackgroundColor3 = AimKeybindEnabled and THEME.ButtonActive or THEME.ButtonBG
    end)

    Toggle("> WALL CHECK: OFF", 328, function(btn)
        AimbotWallCheck = not AimbotWallCheck
        btn.Text = AimbotWallCheck and "> WALL: ON" or "> WALL: OFF"
        btn.BackgroundColor3 = AimbotWallCheck and THEME.ButtonActive or THEME.ButtonBG
    end)

    -- ═══════════════ ESP SECTION ═══════════════
    Section("=== 👁️ ESP ===", 376)

    Toggle("> ESP MASTER: OFF", 408, function(btn)
        ESPEnabled = not ESPEnabled
        btn.Text = ESPEnabled and "> ESP MASTER: ON" or "> ESP MASTER: OFF"
        btn.BackgroundColor3 = ESPEnabled and THEME.ButtonActive or THEME.ButtonBG
        if ESPEnabled then EnableESPLoop() else DisableESPLoop() end
    end)

    Toggle("> 🌈 RAINBOW ESP: OFF", 448, function(btn)
        RainbowESPEnabled = not RainbowESPEnabled
        btn.Text = RainbowESPEnabled and "> 🌈 RAINBOW: ON" or "> 🌈 RAINBOW: OFF"
        btn.BackgroundColor3 = RainbowESPEnabled and THEME.ButtonActive or THEME.ButtonBG
        if RainbowESPEnabled then EnableRainbowESP() else DisableRainbowESP() end
    end)

    Toggle("> 📡 OFF-SCREEN ARROW: OFF", 488, function(btn)
        OffScreenArrowEnabled = not OffScreenArrowEnabled
        btn.Text = OffScreenArrowEnabled and "> OFF-ARROW: ON" or "> OFF-ARROW: OFF"
        btn.BackgroundColor3 = OffScreenArrowEnabled and THEME.ButtonActive or THEME.ButtonBG
        if OffScreenArrowEnabled then EnableOffScreenArrow() else DisableOffScreenArrow() end
    end)

    -- ═══════════════ UPGRADE TO PREMIUM ═══════════════
    Section("=== 🔒 FITUR TERKUNCI ===", 546)

    local LockedInfo = Instance.new("TextLabel")
    LockedInfo.Size = UDim2.new(1, -20, 0, 100)
    LockedInfo.Position = UDim2.new(0, 10, 0, 578)
    LockedInfo.BackgroundColor3 = THEME.PanelBG
    LockedInfo.BorderColor3 = THEME.Locked
    LockedInfo.BorderSizePixel = 1
    LockedInfo.Text = "> ❌ Speed Hack\n> ❌ Fly / Fly-Void\n> ❌ Noclip + InfJump\n> ❌ Hitbox Expander\n> ❌ Fullbright + FPS Boost\n> ❌ Server Hop + Teleport\n> ❌ Music Player + Sound ESP"
    LockedInfo.TextColor3 = THEME.Locked
    LockedInfo.Font = Enum.Font.Code
    LockedInfo.TextSize = 10
    LockedInfo.TextXAlignment = Enum.TextXAlignment.Left
    LockedInfo.TextYAlignment = Enum.TextYAlignment.Top
    LockedInfo.ZIndex = 102
    LockedInfo.Parent = ScrollContent
    Instance.new("UICorner", LockedInfo).CornerRadius = UDim.new(0, 4)

    -- 🔥 UPGRADE NOW BUTTON
    local UpgradeBtn = Instance.new("TextButton")
    UpgradeBtn.Size = UDim2.new(1, -20, 0, 55)
    UpgradeBtn.Position = UDim2.new(0, 10, 0, 690)
    UpgradeBtn.BackgroundColor3 = Color3.fromRGB(200, 150, 0)
    UpgradeBtn.BorderColor3 = THEME.Gold
    UpgradeBtn.BorderSizePixel = 3
    UpgradeBtn.Text = "🔥 UPGRADE SEKARANG KE PREMIUM 🔥"
    UpgradeBtn.TextColor3 = Color3.fromRGB(255, 255, 255)
    UpgradeBtn.Font = Enum.Font.GothamBold
    UpgradeBtn.TextSize = 13
    UpgradeBtn.ZIndex = 102
    UpgradeBtn.Parent = ScrollContent
    Instance.new("UICorner", UpgradeBtn).CornerRadius = UDim.new(0, 6)

    -- Animasi pulse pada tombol upgrade
    task.spawn(function()
        while UpgradeBtn.Parent do
            pcall(function()
                TweenService:Create(UpgradeBtn, TweenInfo.new(0.8), {BackgroundColor3 = Color3.fromRGB(255, 200, 0)}):Play()
                task.wait(0.8)
                TweenService:Create(UpgradeBtn, TweenInfo.new(0.8), {BackgroundColor3 = Color3.fromRGB(200, 150, 0)}):Play()
                task.wait(0.8)
            end)
        end
    end)

    UpgradeBtn.MouseButton1Click:Connect(function()
        Notify("🔥 Upgrade Premium", "Unlock 15+ fitur eksklusif!", 4)
        task.wait(1)
        Notify("🛒 Buy Now", PremiumWebsite, 8)
    end)

    -- 🛒 BUY BUTTON (langsung buka browser)
    local BuyBtn = Instance.new("TextButton")
    BuyBtn.Size = UDim2.new(1, -20, 0, 50)
    BuyBtn.Position = UDim2.new(0, 10, 0, 754)
    BuyBtn.BackgroundColor3 = Color3.fromRGB(0, 200, 100)
    BuyBtn.BorderColor3 = Color3.fromRGB(0, 255, 150)
    BuyBtn.BorderSizePixel = 2
    BuyBtn.Text = "🛒 BUY PREMIUM NOW - $5"
    BuyBtn.TextColor3 = Color3.fromRGB(255, 255, 255)
    BuyBtn.Font = Enum.Font.GothamBold
    BuyBtn.TextSize = 13
    BuyBtn.ZIndex = 102
    BuyBtn.Parent = ScrollContent
    Instance.new("UICorner", BuyBtn).CornerRadius = UDim.new(0, 6)

    BuyBtn.MouseButton1Click:Connect(function()
        Notify("🛒 Membuka Browser...", PremiumWebsite, 5)
        -- Coba buka browser dengan berbagai metode
        pcall(function()
            if setclipboard then setclipboard(PremiumWebsite) end
        end)
        -- Coba langsung buka
        pcall(function()
            game:GetService("GuiService"):OpenBrowserWindow(PremiumWebsite)
        end)
        task.wait(0.3)
        Notify("💳 Website", "Sudah dibuka di browser!\nLink juga di-copy", 6)
    end)

    -- Info tambahan
    local InfoLabel = Instance.new("TextLabel")
    InfoLabel.Size = UDim2.new(1, -20, 0, 60)
    InfoLabel.Position = UDim2.new(0, 10, 0, 814)
    InfoLabel.BackgroundTransparency = 1
    InfoLabel.Text = "> Premium: 15+ fitur lengkap\n> Support: 24/7\n> Payment: All methods"
    InfoLabel.TextColor3 = THEME.TextLight
    InfoLabel.Font = Enum.Font.Code
    InfoLabel.TextSize = 9
    InfoLabel.TextXAlignment = Enum.TextXAlignment.Left
    InfoLabel.TextYAlignment = Enum.TextYAlignment.Top
    InfoLabel.ZIndex = 102
    InfoLabel.Parent = ScrollContent

    -- ═══════════════ USER INFO ═══════════════
    Section("=== USER INFORMATION ===", 884)

    local UIF = Instance.new("Frame")
    UIF.Size = UDim2.new(1, -20, 0, 80)
    UIF.Position = UDim2.new(0, 10, 0, 916)
    UIF.BackgroundColor3 = THEME.PanelBG
    UIF.BorderColor3 = THEME.Accent
    UIF.BorderSizePixel = 1
    UIF.ZIndex = 102
    UIF.Parent = ScrollContent
    Instance.new("UICorner", UIF).CornerRadius = UDim.new(0, 4)

    local NameLbl = Instance.new("TextLabel")
    NameLbl.Size = UDim2.new(1, -15, 0, 22)
    NameLbl.Position = UDim2.new(0, 10, 0, 5)
    NameLbl.BackgroundTransparency = 1
    NameLbl.Text = "> NAME: " .. LocalPlayer.DisplayName
    NameLbl.TextColor3 = THEME.Text
    NameLbl.Font = Enum.Font.Code
    NameLbl.TextSize = 11
    NameLbl.TextXAlignment = Enum.TextXAlignment.Left
    NameLbl.ZIndex = 103
    NameLbl.Parent = UIF

    local UserLbl = Instance.new("TextLabel")
    UserLbl.Size = UDim2.new(1, -15, 0, 22)
    UserLbl.Position = UDim2.new(0, 10, 0, 28)
    UserLbl.BackgroundTransparency = 1
    UserLbl.Text = "> USER: " .. LocalPlayer.Name
    UserLbl.TextColor3 = THEME.Text
    UserLbl.Font = Enum.Font.Code
    UserLbl.TextSize = 11
    UserLbl.TextXAlignment = Enum.TextXAlignment.Left
    UserLbl.ZIndex = 103
    UserLbl.Parent = UIF

    local BuildLbl = Instance.new("TextLabel")
    BuildLbl.Size = UDim2.new(1, -15, 0, 22)
    BuildLbl.Position = UDim2.new(0, 10, 0, 51)
    BuildLbl.BackgroundTransparency = 1
    BuildLbl.Text = "> BUILD: V4.4 PREMIUM"
    BuildLbl.TextColor3 = THEME.Gold
    BuildLbl.Font = Enum.Font.Code
    BuildLbl.TextSize = 11
    BuildLbl.TextXAlignment = Enum.TextXAlignment.Left
    BuildLbl.ZIndex = 103
    BuildLbl.Parent = UIF

    -- ═══════════════ MENU BUTTON ═══════════════
    local ToggleMenuButton = Instance.new("TextButton")
    ToggleMenuButton.Name = "ZetMenuButton"
    ToggleMenuButton.Size = UDim2.new(0, 50, 0, 50)
    ToggleMenuButton.Position = UDim2.new(0, 120, 0.5, -25)
    ToggleMenuButton.BackgroundColor3 = THEME.ButtonActive
    ToggleMenuButton.BorderColor3 = THEME.Accent
    ToggleMenuButton.BorderSizePixel = 2
    ToggleMenuButton.Text = "≡"
    ToggleMenuButton.TextColor3 = Color3.fromRGB(0, 180, 255)
    ToggleMenuButton.Font = Enum.Font.GothamBold
    ToggleMenuButton.TextSize = 26
    ToggleMenuButton.AutoButtonColor = true
    ToggleMenuButton.Active = true
    ToggleMenuButton.ZIndex = 200
    ToggleMenuButton.Visible = false
    ToggleMenuButton.Parent = ScreenGui
    Instance.new("UICorner", ToggleMenuButton).CornerRadius = UDim.new(0, 25)

    -- SAFE ZONE
    local BTN_SIZE = 50
    local SAFE_TOP = 90
    local SAFE_LEFT = 100
    local SAFE_MARGIN = 5
    local DEFAULT_POS = UDim2.new(0, 120, 0.5, -25)

    local menuBtnDragging = false
    local menuBtnDragStart = nil
    local menuBtnStartPos = nil
    local menuBtnMoved = false
    local menuBtnLastTap = 0
    local menuBtnHoldTimer = nil

    local function clampMenuButtonPos(pos)
        local vp = Camera.ViewportSize
        local x = pos.X.Offset
        local y = pos.Y.Offset
        x = math.clamp(x, SAFE_LEFT, vp.X - BTN_SIZE - SAFE_MARGIN)
        y = math.clamp(y, SAFE_TOP, vp.Y - BTN_SIZE - SAFE_MARGIN)
        return UDim2.new(0, x, 0, y)
    end

    local function resetMenuButtonPos(silent)
        TweenService:Create(ToggleMenuButton, TweenInfo.new(0.3, Enum.EasingStyle.Quad), {Position = DEFAULT_POS}):Play()
        if not silent then Notify("📍 Menu Button", "> Posisi di-reset", 2) end
    end

    local lastVp = Camera.ViewportSize
    RunService.Heartbeat:Connect(function()
        local vp = Camera.ViewportSize
        if vp ~= lastVp then
            lastVp = vp
            task.wait(0.1)
            resetMenuButtonPos(true)
        end
        local pos = ToggleMenuButton.AbsolutePosition
        if pos.X < -BTN_SIZE or pos.Y < -BTN_SIZE or pos.X > vp.X or pos.Y > vp.Y then
            resetMenuButtonPos(true)
        end
    end)

    ToggleMenuButton.InputBegan:Connect(function(input)
        if input.UserInputType == Enum.UserInputType.MouseButton1 or input.UserInputType == Enum.UserInputType.Touch then
            menuBtnDragging = true
            menuBtnMoved = false
            menuBtnDragStart = input.Position
            menuBtnStartPos = ToggleMenuButton.Position

            local now = tick()
            if now - menuBtnLastTap < 0.4 then
                resetMenuButtonPos(false)
                menuBtnDragging = false
                menuBtnLastTap = 0
                return
            end
            menuBtnLastTap = now

            if menuBtnHoldTimer then pcall(function() menuBtnHoldTimer:Cancel() end) end
            menuBtnHoldTimer = task.delay(2, function()
                if menuBtnDragging and not menuBtnMoved then
                    resetMenuButtonPos(false)
                    menuBtnDragging = false
                end
            end)
        end
    end)

    ToggleMenuButton.InputChanged:Connect(function(input)
        if not menuBtnDragging then return end
        if input.UserInputType == Enum.UserInputType.MouseMovement or input.UserInputType == Enum.UserInputType.Touch then
            local delta = input.Position - menuBtnDragStart
            if math.abs(delta.X) > 8 or math.abs(delta.Y) > 8 then
                menuBtnMoved = true
                if menuBtnHoldTimer then pcall(function() menuBtnHoldTimer:Cancel() end); menuBtnHoldTimer = nil end
            end
            if menuBtnMoved then
                local newPos = UDim2.new(
                    menuBtnStartPos.X.Scale, menuBtnStartPos.X.Offset + delta.X,
                    menuBtnStartPos.Y.Scale, menuBtnStartPos.Y.Offset + delta.Y
                )
                ToggleMenuButton.Position = clampMenuButtonPos(newPos)
            end
        end
    end)

    UserInputService.InputEnded:Connect(function(input)
        if input.UserInputType == Enum.UserInputType.MouseButton1 or input.UserInputType == Enum.UserInputType.Touch then
            menuBtnDragging = false
            if menuBtnHoldTimer then pcall(function() menuBtnHoldTimer:Cancel() end); menuBtnHoldTimer = nil end
        end
    end)

    ToggleMenuButton.MouseButton1Click:Connect(function()
        if menuBtnMoved then return end
        MenuVisible = not MenuVisible
        MainHub.Visible = MenuVisible
    end)

    CloseBtn.MouseButton1Click:Connect(function()
        MenuVisible = false
        MainHub.Visible = false
    end)

    UserInputService.InputBegan:Connect(function(input, gp)
        if gp then return end
        if input.KeyCode == MenuKey and IsLoggedIn then
            MenuVisible = not MenuVisible
            MainHub.Visible = MenuVisible
        end
    end)

    local function MakeDraggable(frame)
        local dragging, dragInput, dragStart, startPos = false, nil, nil, nil
        frame.InputBegan:Connect(function(input)
            if input.UserInputType == Enum.UserInputType.MouseButton1 or input.UserInputType == Enum.UserInputType.Touch then
                dragging = true; dragStart = input.Position; startPos = frame.Position
            end
        end)
        frame.InputChanged:Connect(function(input)
            if input.UserInputType == Enum.UserInputType.MouseMovement or input.UserInputType == Enum.UserInputType.Touch then dragInput = input end
        end)
        UserInputService.InputChanged:Connect(function(input)
            if input == dragInput and dragging then
                local delta = input.Position - dragStart
                frame.Position = UDim2.new(startPos.X.Scale, startPos.X.Offset + delta.X, startPos.Y.Scale, startPos.Y.Offset + delta.Y)
            end
        end)
        UserInputService.InputEnded:Connect(function(input)
            if input.UserInputType == Enum.UserInputType.MouseButton1 or input.UserInputType == Enum.UserInputType.Touch then dragging = false end
        end)
    end
    MakeDraggable(LoginFrame)
    MakeDraggable(MainHub)

    -- ⭐ AUTO PROMOTE NOTIF (tiap 5 menit)
    task.spawn(function()
        task.wait(30)
        while task.wait(300) do
            pcall(function()
                Notify("⭐ ZetGames", "Follow rscripts.net/@ZetGames", 4)
            end)
        end
    end)

    -- LOADING 10 DETIK
    task.spawn(function()
        local totalTime = 10
        local startTime = tick()
        local messages = {
            "> Menginisialisasi sistem...",
            "> Memuat VPN...",
            "> Menghubungkan ke server...",
            "> Memuat konfigurasi...",
            "> Verifikasi premium...",
            "> Menyiapkan UI...",
            "> Memuat fitur...",
            "> Sinkronisasi data...",
            "> Finalisasi...",
            "> Selesai!",
        }
        for i = 1, 100 do
            local elapsed = tick() - startTime
            local remaining = math.max(0, totalTime - elapsed)
            LBarFill.Size = UDim2.new(i / 100, 0, 1, 0)
            LPercent.Text = i .. "%"
            LTimeLeft.Text = "Waktu tersisa: " .. math.ceil(remaining) .. " detik"
            local msgIdx = math.min(10, math.ceil(i / 10))
            LStatus.Text = messages[msgIdx]
            task.wait(totalTime / 100)
        end
        task.wait(0.3)
        LoadingScreen.Visible = false
        LoadingScreen:Destroy()
        LoginFrame.Visible = true
        Notify("V4.4 PREMIUM", "> Silakan login dengan key", 3)
    end)

    -- LOGIN LOGIC
    LoginBtn.MouseButton1Click:Connect(function()
        local key = KeyInput.Text
        local kd = ValidKeys[key]
        if kd and (kd.Expiry == 0 or os.time() < kd.Expiry) then
            IsLoggedIn = true
            LoginFrame.Visible = false
            MainHub.Visible = true
            ToggleMenuButton.Visible = true
            MenuVisible = true
            StatusTxt.Text = "> ACCESS GRANTED..."
            Notify("✅ Success", "WELCOME V4.4 PREMIUM", 3)
            pcall(ActivateAntiKick)
            Notify("🔒 VPN", "> AUTO-PROTECT ACTIVE", 3)
            task.wait(0.5)
            Notify("🔥 Premium", "Upgrade untuk 15+ fitur!", 5)
        else
            StatusTxt.Text = "> ERROR: KEY INVALID"
            Notify("❌ Failed", "> KEY INVALID", 2)
        end
    end)

    -- GET KEY
    GetKeyBtn.MouseButton1Click:Connect(function()
        StatusTxt.Text = "> Buka website key di browser..."
        Notify("🔑 Get Key", "Buka: " .. KeyWebsite, 8)
        Notify("📋 Steps", "1. Copy link di atas\n2. Buka di browser\n3. Ambil key", 6)
    end)
end

--==============================================================
-- RUN
--==============================================================
print("[ZET] Starting UI...")
pcall(CreateUI)
print("[ZET] V4.4 PREMIUM loaded!")
