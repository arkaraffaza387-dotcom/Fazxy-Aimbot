--[[
    ══════════════════════════════════════════════════
      ZetGames-AimLock V4.4 | OFFICIAL RESMI
    ══════════════════════════════════════════════════
      Theme    : 🔵 Blue & Black
      Login    : ✅ WAJIB KEY
      Night Lock: ✅ ACTIVE (Auto Kick)
      Anti-Kick: ✅ SAFE MODE
      
      ⭐ FOLLOW @ZetGames di rscripts.net
      ⭐ Link: rscripts.net/@ZetGames
      ⭐ Update V4.5, V4.6, dst coming soon!
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

print("[ZET] Loading V4.4 RESMI...")

--==============================================================
-- MENU ICON CONFIG
--==============================================================
-- Opsi A: Pakai Cloudinary (coba dulu, kalau gak muncul pakai Opsi B/C)
local MENU_ICON_ID = "rbxassetid://0"  -- KOSONG dulu biar aman
-- Kalau mau pakai gambar: isi dengan link di bawah ini
-- local MENU_ICON_ID = "https://res.cloudinary.com/opyeeh5w/image/upload/f_auto,q_auto/1000236060"
-- Atau pakai Roblox asset ID (upload dulu di roblox.com/create → Decals):
-- local MENU_ICON_ID = "rbxassetid://1234567890"  -- Ganti dengan ID asli lu

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

--==============================================================
-- SCREEN GUI
--==============================================================
local ScreenGui = Instance.new("ScreenGui")
ScreenGui.Name = "ZetGamesV44Resmi"
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

local FOVCircleEnabled = false
local FOVRadius = 250
local FOVMaxRadius = 5000
local FOVColor = Color3.fromRGB(0, 150, 255)
local FOVThickness = 2
local FOVFilled = false
local FOVFillTransparency = 0.85

local NPCDetectionEnabled = false
local NPCEspEnabled = false
local NPCFilterName = ""
local NPCMaxDistance = 500
local NPCMaxCount = 50
local NPCWhitelistKeywords = {"pet", "shop", "vendor", "trainer"}
local NPCESPObjects = {}

local ESPEnabled = false
local ESPObjects = {}
local ChamsObjects = {}
local TracerColor = Color3.fromRGB(0, 150, 255)
local RainbowESPEnabled = false
local RainbowHue = 0

local FlyNormalEnabled = false
local FlyNormalSpeed = 100
local FlyNormalMode = "Free"
local FlyNormalVelocity = nil
local FlyNormalGyro = nil
local FlyKeys = {W=false, A=false, S=false, D=false, Space=false, Ctrl=false}

local FlyVoidEnabled = false
local FlyVoidHideMode = false
local FlyVoidOriginalY = nil
local OriginalTransparency = {}
local OriginalCanCollide = {}

local FullbrightEnabled = false
local OriginalLighting = {}
local FPSBoostEnabled = false
local OriginalSettings = {}
local SpeedHackEnabled = false
local SpeedMultiplier = 100
local MaxSpeed = 500
local DefaultWalkSpeed = 16
local NoclipEnabled = false
local InfiniteJumpEnabled = false

local ChatSpamEnabled = false
local ChatSpamText = "ZETGAMES-RESMI"
local ChatSpamDelay = 3

local SoundESPEnabled = false
local SoundESPRadius = 100
local SoundESPBeep = nil
local LastBeepTime = 0

local MusicPlayerEnabled = false
local MusicSound = nil
local MusicPlaylist = {
    {Name = "Kelingan Mantan", ID = "78450316593213"},
    {Name = "Teh Hijau", ID = "111485011584825"},
}
local MusicCurrentIndex = 1
local MusicVolume = 1
local MusicShuffle = false
local MusicRepeatAll = true

local AutoRespawnEnabled = false
local AntiFlingEnabled = false
local AntiAFKEnabled = false
local HitboxEnabled = false
local HitboxSize = 5
local DashEnabled = false
local DashCooldown = 0
local InvisibleEnabled = false
local InvisibleOriginalTransparency = {}
local AutoShootEnabled = false
local AutoShootDelay = 100
local DroneModeEnabled = false
local KillNotifEnabled = false
local LastPlayerHealth = {}
local InfoPanelEnabled = false
local InfoPanelFrame = nil
local Waypoints = {}

local AntiKickEnabled = true
local AutoReconnectEnabled = true
local ReconnectAttempts = 0
local MaxReconnectAttempts = 5
local WatchdogLastPing = tick()
local WatchdogPingThreshold = 60

local NightLockActive = true
local NightLockKickLog = {}
local NightLockScanInterval = 1
local NightLockLastScan = 0

local TeleportPlayerList = {}
local TeleportListFrame = nil
local TeleportListContainer = nil
local SavedLocation = nil
local ServerHopRunning = false

local FOVCircle
pcall(function()
    FOVCircle = Drawing.new("Circle")
    FOVCircle.Visible = false
    FOVCircle.Color = FOVColor
    FOVCircle.Thickness = FOVThickness
    FOVCircle.Filled = FOVFilled
    FOVCircle.Transparency = 1
    FOVCircle.NumSides = 90
end)

local OffScreenArrow
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
            FOVCircle.Radius = FOVRadius
            FOVCircle.Color = FOVColor
            FOVCircle.Thickness = FOVThickness
            FOVCircle.Filled = FOVFilled
            FOVCircle.Transparency = FOVFilled and FOVFillTransparency or 1
            FOVCircle.NumSides = 90
            FOVCircle.Visible = true
        end)
    end)
    ActiveConnections["FOV"] = conn
end

local function DisableFOVLoop()
    DisconnectKey("FOV")
    if FOVCircle then pcall(function() FOVCircle.Visible = false end) end
end

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
                        OffScreenArrow.Color = Color3.fromRGB(0, 150, 255)
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
-- ANTI-KICK
--==============================================================
local BlockedKeywords = {"exploit", "cheat", "hack", "aimbot", "ban", "detect", "script", "injector", "banned", "violation", "suspicious", "anti-cheat", "anticheat"}
local LegitKeywords = {"shutdown", "restart", "update", "maintenance", "rejoin"}

local function ActivateAntiKick()
    if IsHighSecurityGame() then
        Notify("🛡️ Anti-Kick", "> SKIP (game AC kuat)", 3)
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
                    Notify("🛡️ Anti-Kick", "> Kick diblokir: " .. kw, 3)
                    return
                end
            end
            return _G._ZET_OrigKick(self, message)
        end
    end)
    Notify("🛡️ Anti-Kick", "> ACTIVE (SAFE)", 2)
end

--==============================================================
-- AUTO-RECONNECT
--==============================================================
local function AttemptReconnect()
    if ReconnectAttempts >= MaxReconnectAttempts then ReconnectAttempts = 0; return end
    ReconnectAttempts = ReconnectAttempts + 1
    pcall(function() TeleportService:TeleportToPlaceInstance(game.PlaceId, game.JobId, LocalPlayer) end)
end

local function ActivateAutoReconnect()
    DisconnectKey("AutoReconnect")
    WatchdogLastPing = tick()
    local conn = RunService.Heartbeat:Connect(function()
        if not AutoReconnectEnabled then return end
        local now = tick()
        if now - WatchdogLastPing > WatchdogPingThreshold then
            WatchdogLastPing = now
            AttemptReconnect()
        else WatchdogLastPing = now end
    end)
    ActiveConnections["AutoReconnect"] = conn
end

--==============================================================
-- NIGHT LOCK
--==============================================================
local function ActivateNightLock()
    DisconnectKey("NightLock")
    NightLockActive = true
    local conn = RunService.Heartbeat:Connect(function()
        if not NightLockActive then return end
        local now = tick()
        if now - NightLockLastScan < NightLockScanInterval then return end
        NightLockLastScan = now
        for _, plr in pairs(Players:GetPlayers()) do
            if plr ~= LocalPlayer then
                local name = string.lower(plr.Name)
                local sus, reason = false, ""
                if string.find(name, "bot", 1, true) then sus=true; reason="Name:bot" end
                if string.find(name, "exploit", 1, true) then sus=true; reason="Name:exploit" end
                if string.find(name, "hack", 1, true) then sus=true; reason="Name:hack" end
                if string.find(name, "cheat", 1, true) then sus=true; reason="Name:cheat" end
                if string.find(name, "aimbot", 1, true) then sus=true; reason="Name:aimbot" end
                if plr.Character then
                    local root = plr.Character:FindFirstChild("HumanoidRootPart")
                    local hum = plr.Character:FindFirstChild("Humanoid")
                    if root and hum then
                        if root.AssemblyLinearVelocity.Magnitude > 1000 then sus=true; reason="Fling" end
                        if hum.WalkSpeed > 200 then sus=true; reason="Speed:"..math.floor(hum.WalkSpeed) end
                    end
                end
                if sus and not NightLockKickLog[plr.UserId] then
                    NightLockKickLog[plr.UserId] = true
                    Notify("🔒 NIGHT LOCK", "> " .. plr.Name .. " | " .. reason, 5)
                    task.wait(0.5)
                    pcall(function()
                        LocalPlayer:Kick("[NIGHT LOCK] " .. plr.Name .. " | " .. reason .. "\nOfficial Build V4.4")
                    end)
                    break
                end
            end
        end
    end)
    ActiveConnections["NightLock"] = conn
    Notify("🔒 Night Lock", "> ACTIVE (AUTO KICK)", 3)
end

--==============================================================
-- NPC DETECTION
--==============================================================
local function IsNPC(model)
    if not model or not model:IsA("Model") then return false end
    if Players:GetPlayerFromCharacter(model) then return false end
    if model == LocalPlayer.Character then return false end
    if not model:FindFirstChild("Humanoid") then return false end
    if not model:FindFirstChild("HumanoidRootPart") then return false end
    if model.Humanoid.Health <= 0 then return false end
    local nameLower = string.lower(model.Name)
    for _, keyword in ipairs(NPCWhitelistKeywords) do
        if string.find(nameLower, keyword, 1, true) then return false end
    end
    if NPCFilterName ~= "" then
        if not string.find(nameLower, string.lower(NPCFilterName), 1, true) then return false end
    end
    local myRoot = LocalPlayer.Character and LocalPlayer.Character:FindFirstChild("HumanoidRootPart")
    local npcRoot = model:FindFirstChild("HumanoidRootPart")
    if myRoot and npcRoot and (npcRoot.Position - myRoot.Position).Magnitude > NPCMaxDistance then return false end
    return true
end

local function GetNPCs()
    local list, count = {}, 0
    for _, obj in pairs(Workspace:GetChildren()) do
        if IsNPC(obj) then table.insert(list, obj); count = count + 1; if count >= NPCMaxCount then break end end
    end
    return list
end

--==============================================================
-- FLY NORMAL
--==============================================================
local function EnableFlyNormal()
    DisconnectKey("FlyNormal")
    if FlyNormalVelocity then pcall(function() FlyNormalVelocity:Destroy() end); FlyNormalVelocity = nil end
    if FlyNormalGyro then pcall(function() FlyNormalGyro:Destroy() end); FlyNormalGyro = nil end
    local char = LocalPlayer.Character
    if not char then return end
    local root = char:FindFirstChild("HumanoidRootPart")
    if not root then return end
    FlyNormalVelocity = Instance.new("BodyVelocity")
    FlyNormalVelocity.Velocity = Vector3.new(0,0,0)
    FlyNormalVelocity.MaxForce = Vector3.new(1e9,1e9,1e9)
    FlyNormalVelocity.P = 1e5
    FlyNormalVelocity.Parent = root
    FlyNormalGyro = Instance.new("BodyGyro")
    FlyNormalGyro.MaxTorque = Vector3.new(1e9,1e9,1e9)
    FlyNormalGyro.P = 1e5
    FlyNormalGyro.CFrame = root.CFrame
    FlyNormalGyro.Parent = root
    local conn = RunService.RenderStepped:Connect(function()
        if not FlyNormalEnabled then return end
        local c = LocalPlayer.Character
        if not c then return end
        local r = c:FindFirstChild("HumanoidRootPart")
        local h = c:FindFirstChild("Humanoid")
        if not r or not h then return end
        if FlyNormalVelocity and FlyNormalVelocity.Parent ~= r then FlyNormalVelocity.Parent = r end
        if FlyNormalGyro and FlyNormalGyro.Parent ~= r then FlyNormalGyro.Parent = r end
        local camCF = Camera.CFrame
        local dir = Vector3.new(0,0,0)
        if FlyKeys.W then dir = dir + camCF.LookVector end
        if FlyKeys.S then dir = dir - camCF.LookVector end
        if FlyKeys.A then dir = dir - camCF.RightVector end
        if FlyKeys.D then dir = dir + camCF.RightVector end
        if FlyKeys.Space then dir = dir + Vector3.new(0,1,0) end
        if FlyKeys.Ctrl then dir = dir - Vector3.new(0,1,0) end
        if h.MoveDirection.Magnitude > 0 then dir = dir + h.MoveDirection end
        local moveDir = dir.Magnitude > 0 and dir.Unit * FlyNormalSpeed or Vector3.new(0,0,0)
        FlyNormalVelocity.Velocity = moveDir
        FlyNormalGyro.CFrame = CFrame.new(r.Position, r.Position + camCF.LookVector)
    end)
    ActiveConnections["FlyNormal"] = conn
end

local function DisableFlyNormal()
    DisconnectKey("FlyNormal")
    if FlyNormalVelocity then pcall(function() FlyNormalVelocity:Destroy() end); FlyNormalVelocity = nil end
    if FlyNormalGyro then pcall(function() FlyNormalGyro:Destroy() end); FlyNormalGyro = nil end
end

--==============================================================
-- FLY VOID
--==============================================================
local function EnableFlyVoid()
    DisconnectKey("FlyVoid")
    local char = LocalPlayer.Character
    if not char then return end
    local root = char:FindFirstChild("HumanoidRootPart")
    if not root then return end
    FlyVoidOriginalY = root.Position.Y
    local rp = RaycastParams.new()
    rp.FilterType = Enum.RaycastFilterType.Blacklist
    rp.FilterDescendantsInstances = {char}
    local ray = workspace:Raycast(Vector3.new(root.Position.X, 1000, root.Position.Z), Vector3.new(0,-3000,0), rp)
    local floorY = ray and ray.Position.Y or -60
    local targetY = floorY - 5
    pcall(function() root.CFrame = CFrame.new(root.Position.X, targetY, root.Position.Z) end)
    local conn = RunService.Heartbeat:Connect(function()
        if not FlyVoidEnabled then return end
        local c = LocalPlayer.Character
        if not c then return end
        local r = c:FindFirstChild("HumanoidRootPart")
        local h = c:FindFirstChild("Humanoid")
        if not r or not h then return end
        local pos = r.Position
        if pos.Y > targetY + 2 then
            pcall(function()
                r.CFrame = CFrame.new(pos.X, targetY, pos.Z)
                r.AssemblyLinearVelocity = Vector3.new(r.AssemblyLinearVelocity.X, 0, r.AssemblyLinearVelocity.Z)
            end)
        end
        if pos.Y < targetY - 15 then
            pcall(function()
                r.CFrame = CFrame.new(pos.X, targetY, pos.Z)
                r.AssemblyLinearVelocity = Vector3.new(0,0,0)
            end)
        end
        if math.abs(r.AssemblyLinearVelocity.Y) > 5 then
            pcall(function()
                r.AssemblyLinearVelocity = Vector3.new(r.AssemblyLinearVelocity.X, 0, r.AssemblyLinearVelocity.Z)
            end)
        end
        if h.Health <= 0 then pcall(function() LocalPlayer:LoadCharacter() end) end
        if FlyVoidHideMode then
            for _, part in pairs(c:GetDescendants()) do
                if part:IsA("BasePart") then
                    if not OriginalTransparency[part] then
                        OriginalTransparency[part] = part.Transparency
                        OriginalCanCollide[part] = part.CanCollide
                    end
                    part.Transparency = 0.85
                    part.CanCollide = false
                end
            end
        end
    end)
    ActiveConnections["FlyVoid"] = conn
end

local function DisableFlyVoid()
    DisconnectKey("FlyVoid")
    local char = LocalPlayer.Character
    if char then
        for _, part in pairs(char:GetDescendants()) do
            if part:IsA("BasePart") then
                if OriginalTransparency[part] then part.Transparency = OriginalTransparency[part] end
                if OriginalCanCollide[part] ~= nil then part.CanCollide = OriginalCanCollide[part] end
            end
        end
        local root = char:FindFirstChild("HumanoidRootPart")
        if root then
            pcall(function()
                local rp = RaycastParams.new()
                rp.FilterType = Enum.RaycastFilterType.Blacklist
                rp.FilterDescendantsInstances = {char}
                local ray = workspace:Raycast(Vector3.new(root.Position.X, 1000, root.Position.Z), Vector3.new(0,-3000,0), rp)
                if ray then root.CFrame = CFrame.new(ray.Position.X, ray.Position.Y + 5, ray.Position.Z)
                elseif FlyVoidOriginalY then root.CFrame = CFrame.new(root.Position.X, FlyVoidOriginalY, root.Position.Z) end
            end)
        end
    end
    OriginalTransparency = {}
    OriginalCanCollide = {}
    FlyVoidOriginalY = nil
end

--==============================================================
-- FULLBRIGHT / FPS
--==============================================================
local function EnableFullbright()
    OriginalLighting.Ambient = Lighting.Ambient
    OriginalLighting.OutdoorAmbient = Lighting.OutdoorAmbient
    OriginalLighting.Brightness = Lighting.Brightness
    OriginalLighting.ClockTime = Lighting.ClockTime
    OriginalLighting.FogEnd = Lighting.FogEnd
    OriginalLighting.FogStart = Lighting.FogStart
    OriginalLighting.GlobalShadows = Lighting.GlobalShadows
    Lighting.Ambient = Color3.fromRGB(255,255,255)
    Lighting.OutdoorAmbient = Color3.fromRGB(255,255,255)
    Lighting.Brightness = 3
    Lighting.ClockTime = 12
    Lighting.FogEnd = 100000
    Lighting.FogStart = 0
    Lighting.GlobalShadows = false
end

local function DisableFullbright()
    pcall(function()
        if OriginalLighting.Ambient then Lighting.Ambient = OriginalLighting.Ambient end
        if OriginalLighting.OutdoorAmbient then Lighting.OutdoorAmbient = OriginalLighting.OutdoorAmbient end
        if OriginalLighting.Brightness then Lighting.Brightness = OriginalLighting.Brightness end
        if OriginalLighting.ClockTime then Lighting.ClockTime = OriginalLighting.ClockTime end
        if OriginalLighting.FogEnd then Lighting.FogEnd = OriginalLighting.FogEnd end
        if OriginalLighting.FogStart then Lighting.FogStart = OriginalLighting.FogStart end
        if OriginalLighting.GlobalShadows ~= nil then Lighting.GlobalShadows = OriginalLighting.GlobalShadows end
    end)
end

local function EnableFPSBoost()
    OriginalSettings.Shadows = Lighting.GlobalShadows
    OriginalSettings.FogEnd = Lighting.FogEnd
    OriginalSettings.Brightness = Lighting.Brightness
    Lighting.GlobalShadows = false
    Lighting.FogEnd = 100000
    Lighting.Brightness = 2
    for _, effect in pairs(Lighting:GetChildren()) do
        if effect:IsA("PostEffect") then pcall(function() effect.Enabled = false end) end
    end
end

local function DisableFPSBoost()
    pcall(function()
        if OriginalSettings.Shadows ~= nil then Lighting.GlobalShadows = OriginalSettings.Shadows end
        if OriginalSettings.FogEnd ~= nil then Lighting.FogEnd = OriginalSettings.FogEnd end
        if OriginalSettings.Brightness ~= nil then Lighting.Brightness = OriginalSettings.Brightness end
    end)
end

--==============================================================
-- NOCLIP
--==============================================================
local function EnableNoclip()
    DisconnectKey("Noclip")
    local conn = RunService.Stepped:Connect(function()
        if not NoclipEnabled then return end
        local char = LocalPlayer.Character
        if not char then return end
        for _, p in pairs(char:GetDescendants()) do
            if p:IsA("BasePart") then p.CanCollide = false end
        end
    end)
    ActiveConnections["Noclip"] = conn
end

local function DisableNoclip()
    DisconnectKey("Noclip")
    NoclipEnabled = false
    task.wait(0.1)
    local char = LocalPlayer.Character
    if char then
        for _, p in pairs(char:GetDescendants()) do
            if p:IsA("BasePart") then
                pcall(function()
                    if p.Name == "HumanoidRootPart" then
                        p.CanCollide = false
                    else
                        p.CanCollide = true
                    end
                end)
            end
        end
    end
end

--==============================================================
-- SPEED / JUMP / DASH / INVISIBLE
--==============================================================
local function EnableSpeedHack()
    DisconnectKey("Speed")
    local conn = RunService.Heartbeat:Connect(function()
        if not SpeedHackEnabled then return end
        local char = LocalPlayer.Character
        if not char then return end
        local hum = char:FindFirstChild("Humanoid")
        if hum then hum.WalkSpeed = SpeedMultiplier end
    end)
    ActiveConnections["Speed"] = conn
end

local function DisableSpeedHack()
    DisconnectKey("Speed")
    SpeedHackEnabled = false
    task.wait(0.05)
    local char = LocalPlayer.Character
    if char then
        local hum = char:FindFirstChild("Humanoid")
        if hum then hum.WalkSpeed = DefaultWalkSpeed end
    end
end

local function EnableInfiniteJump()
    DisconnectKey("Jump")
    local conn = UserInputService.JumpRequest:Connect(function()
        if not InfiniteJumpEnabled then return end
        if LocalPlayer.Character then
            local hum = LocalPlayer.Character:FindFirstChild("Humanoid")
            if hum then hum:ChangeState(Enum.HumanoidStateType.Jumping) end
        end
    end)
    ActiveConnections["Jump"] = conn
end

local function DisableInfiniteJump()
    DisconnectKey("Jump")
    InfiniteJumpEnabled = false
end

local function PerformDash()
    if not DashEnabled then return end
    local now = tick()
    if now - DashCooldown < 2 then return end
    DashCooldown = now
    local char = LocalPlayer.Character
    if not char then return end
    local root = char:FindFirstChild("HumanoidRootPart")
    if not root then return end
    local camDir = Camera.CFrame.LookVector
    local dashVel = Instance.new("BodyVelocity")
    dashVel.Velocity = Vector3.new(camDir.X * 150, 0, camDir.Z * 150)
    dashVel.MaxForce = Vector3.new(1e9,0,1e9)
    dashVel.P = 1e5
    dashVel.Parent = root
    game:GetService("Debris"):AddItem(dashVel, 0.2)
end

local function EnableInvisible()
    DisconnectKey("Invisible")
    local char = LocalPlayer.Character
    if not char then return end
    for _, part in pairs(char:GetDescendants()) do
        if part:IsA("BasePart") and part.Name ~= "HumanoidRootPart" then
            if not InvisibleOriginalTransparency[part] then InvisibleOriginalTransparency[part] = part.Transparency end
            part.Transparency = 0.95
        elseif part:IsA("Decal") then
            if not InvisibleOriginalTransparency[part] then InvisibleOriginalTransparency[part] = part.Transparency end
            part.Transparency = 1
        end
    end
end

local function DisableInvisible()
    DisconnectKey("Invisible")
    InvisibleEnabled = false
    local char = LocalPlayer.Character
    if char then
        for _, part in pairs(char:GetDescendants()) do
            if InvisibleOriginalTransparency[part] then part.Transparency = InvisibleOriginalTransparency[part] end
        end
    end
    InvisibleOriginalTransparency = {}
end

--==============================================================
-- HITBOX
--==============================================================
local function ApplyHitbox(player)
    if not player.Character then return end
    local head = player.Character:FindFirstChild("Head")
    local hrp = player.Character:FindFirstChild("HumanoidRootPart")
    if not head or not hrp then return end
    if not head:GetAttribute("OriginalSize") then
        head:SetAttribute("OriginalSize", head.Size)
        hrp:SetAttribute("OriginalSize", hrp.Size)
    end
    if HitboxEnabled then
        head.Size = Vector3.new(HitboxSize, HitboxSize, HitboxSize)
        head.Transparency = 1
        head.CanCollide = false
        hrp.Size = Vector3.new(HitboxSize, HitboxSize, HitboxSize)
        hrp.Transparency = 1
        hrp.CanCollide = false
    else
        local os = head:GetAttribute("OriginalSize")
        local oh = hrp:GetAttribute("OriginalSize")
        if os then head.Size = os end
        if oh then hrp.Size = oh end
        head.Transparency = 0
        head.CanCollide = true
        hrp.Transparency = 1
    end
end

local function EnableHitboxExpander()
    DisconnectKey("Hitbox")
    local conn = RunService.Heartbeat:Connect(function()
        if not HitboxEnabled then return end
        for _, player in pairs(Players:GetPlayers()) do
            if player ~= LocalPlayer then pcall(ApplyHitbox, player) end
        end
    end)
    ActiveConnections["Hitbox"] = conn
end

local function DisableHitboxExpander()
    DisconnectKey("Hitbox")
    HitboxEnabled = false
    task.wait(0.05)
    for _, player in pairs(Players:GetPlayers()) do
        if player ~= LocalPlayer and player.Character then
            local head = player.Character:FindFirstChild("Head")
            local hrp = player.Character:FindFirstChild("HumanoidRootPart")
            if head and head:GetAttribute("OriginalSize") then
                head.Size = head:GetAttribute("OriginalSize")
                head.Transparency = 0
                head.CanCollide = true
            end
            if hrp and hrp:GetAttribute("OriginalSize") then
                hrp.Size = hrp:GetAttribute("OriginalSize")
            end
        end
    end
end

--==============================================================
-- CHAT / SOUND / MUSIC
--==============================================================
local function SendChatMessage(message)
    pcall(function()
        local chatEvents = ReplicatedStorage:FindFirstChild("DefaultChatSystemChatEvents")
        if chatEvents then
            local sayReq = chatEvents:FindFirstChild("SayMessageRequest")
            if sayReq then sayReq:FireServer(message, "All") end
        end
    end)
end

local function EnableChatSpam()
    DisconnectKey("ChatSpam")
    task.spawn(function()
        while ChatSpamEnabled do
            task.wait(ChatSpamDelay)
            if not ChatSpamEnabled then break end
            SendChatMessage(ChatSpamText)
        end
    end)
end

local function DisableChatSpam()
    DisconnectKey("ChatSpam")
    ChatSpamEnabled = false
end

local function EnableSoundESP()
    DisconnectKey("SoundESP")
    if SoundESPBeep then pcall(function() SoundESPBeep:Destroy() end) end
    SoundESPBeep = Instance.new("Sound")
    SoundESPBeep.SoundId = "rbxassetid://4790566870"
    SoundESPBeep.Volume = 1
    SoundESPBeep.Parent = SoundService
    local conn = RunService.Heartbeat:Connect(function()
        if not SoundESPEnabled then return end
        local char = LocalPlayer.Character
        if not char or not char:FindFirstChild("HumanoidRootPart") then return end
        local myPos = char.HumanoidRootPart.Position
        local nearestDist = math.huge
        for _, player in pairs(Players:GetPlayers()) do
            if player ~= LocalPlayer and player.Character and player.Character:FindFirstChild("HumanoidRootPart") and player.Character:FindFirstChild("Humanoid") and player.Character.Humanoid.Health > 0 then
                local d = (player.Character.HumanoidRootPart.Position - myPos).Magnitude
                if d < nearestDist then nearestDist = d end
            end
        end
        if nearestDist <= SoundESPRadius then
            local now = tick()
            local cooldown = math.clamp(nearestDist / 85, 0.15, 1.2)
            if now - LastBeepTime >= cooldown then
                LastBeepTime = now
                pcall(function()
                    SoundESPBeep.Volume = math.clamp(1 - (nearestDist / SoundESPRadius) + 0.3, 0.3, 1)
                    SoundESPBeep:Play()
                end)
            end
        end
    end)
    ActiveConnections["SoundESP"] = conn
end

local function DisableSoundESP()
    DisconnectKey("SoundESP")
    SoundESPEnabled = false
    if SoundESPBeep then pcall(function() SoundESPBeep:Destroy() end); SoundESPBeep = nil end
end

local function PlayMusic()
    if MusicSound then pcall(function() MusicSound:Stop(); MusicSound:Destroy() end); MusicSound = nil end
    local track = MusicPlaylist[MusicCurrentIndex]
    if not track then return end
    MusicSound = Instance.new("Sound")
    MusicSound.SoundId = "rbxassetid://" .. track.ID
    MusicSound.Volume = MusicVolume
    MusicSound.Parent = SoundService
    pcall(function() MusicSound:Play() end)
end

local function StopMusic()
    if MusicSound then pcall(function() MusicSound:Stop(); MusicSound:Destroy() end); MusicSound = nil end
end

local function NextMusic()
    if MusicShuffle then MusicCurrentIndex = math.random(1, #MusicPlaylist)
    else MusicCurrentIndex = MusicCurrentIndex + 1; if MusicCurrentIndex > #MusicPlaylist then MusicCurrentIndex = 1 end end
    if MusicPlayerEnabled then PlayMusic() end
end

local function PrevMusic()
    MusicCurrentIndex = MusicCurrentIndex - 1
    if MusicCurrentIndex < 1 then MusicCurrentIndex = #MusicPlaylist end
    if MusicPlayerEnabled then PlayMusic() end
end

--==============================================================
-- INPUT
--==============================================================
UserInputService.InputBegan:Connect(function(input, gp)
    if gp then return end
    if input.KeyCode == Enum.KeyCode.W then FlyKeys.W = true end
    if input.KeyCode == Enum.KeyCode.A then FlyKeys.A = true end
    if input.KeyCode == Enum.KeyCode.S then FlyKeys.S = true end
    if input.KeyCode == Enum.KeyCode.D then FlyKeys.D = true end
    if input.KeyCode == Enum.KeyCode.Space then FlyKeys.Space = true end
    if input.KeyCode == Enum.KeyCode.LeftControl then FlyKeys.Ctrl = true end
    if AimKeybindEnabled and input.KeyCode == AimKeybind then AimKeyHeld = true end
    if DashEnabled and input.KeyCode == Enum.KeyCode.LeftShift then PerformDash() end
end)

UserInputService.InputEnded:Connect(function(input, gp)
    if input.KeyCode == Enum.KeyCode.W then FlyKeys.W = false end
    if input.KeyCode == Enum.KeyCode.A then FlyKeys.A = false end
    if input.KeyCode == Enum.KeyCode.S then FlyKeys.S = false end
    if input.KeyCode == Enum.KeyCode.D then FlyKeys.D = false end
    if input.KeyCode == Enum.KeyCode.Space then FlyKeys.Space = false end
    if input.KeyCode == Enum.KeyCode.LeftControl then FlyKeys.Ctrl = false end
    if input.KeyCode == AimKeybind then AimKeyHeld = false end
end)

--==============================================================
-- SURVIVAL
--==============================================================
local function EnableAutoRespawn()
    DisconnectKey("AutoRespawn")
    local conn = RunService.Heartbeat:Connect(function()
        if not AutoRespawnEnabled then return end
        if LocalPlayer.Character then
            local hum = LocalPlayer.Character:FindFirstChild("Humanoid")
            if hum and hum.Health <= 0 then pcall(function() LocalPlayer:LoadCharacter() end) end
        end
    end)
    ActiveConnections["AutoRespawn"] = conn
end
local function DisableAutoRespawn() DisconnectKey("AutoRespawn"); AutoRespawnEnabled = false end

local function EnableAntiFling()
    DisconnectKey("AntiFling")
    local conn = RunService.Heartbeat:Connect(function()
        if not AntiFlingEnabled then return end
        if LocalPlayer.Character then
            local root = LocalPlayer.Character:FindFirstChild("HumanoidRootPart")
            if root and root.AssemblyLinearVelocity.Magnitude > 500 then
                pcall(function() root.AssemblyLinearVelocity = Vector3.new(0,0,0) end)
            end
        end
    end)
    ActiveConnections["AntiFling"] = conn
end
local function DisableAntiFling() DisconnectKey("AntiFling"); AntiFlingEnabled = false end

local function EnableAntiAFK()
    DisconnectKey("AntiAFK")
    local conn = RunService.Heartbeat:Connect(function()
        if not AntiAFKEnabled then return end
        pcall(function()
            VirtualUser:CaptureController()
            VirtualUser:ClickButton2(Vector2.new())
        end)
    end)
    ActiveConnections["AntiAFK"] = conn
end
local function DisableAntiAFK() DisconnectKey("AntiAFK"); AntiAFKEnabled = false end

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

local function CreateNPCEsp(model)
    if NPCESPObjects[model] then return end
    if not Drawing then return end
    local d = {}
    d.Box = Drawing.new("Square"); d.Box.Visible = false; d.Box.Color = THEME.YellowDot; d.Box.Thickness = 2; d.Box.Filled = false; d.Box.Transparency = 1
    d.Name = Drawing.new("Text"); d.Name.Visible = false; d.Name.Color = THEME.YellowDot; d.Name.Size = 11; d.Name.Center = true; d.Name.Outline = true; d.Name.OutlineColor = Color3.fromRGB(0,0,0)
    d.Distance = Drawing.new("Text"); d.Distance.Visible = false; d.Distance.Color = THEME.YellowDot; d.Distance.Size = 9; d.Distance.Center = true; d.Distance.Outline = true; d.Distance.OutlineColor = Color3.fromRGB(0,0,0)
    NPCESPObjects[model] = d
end

local function RemoveNPCEsp(model)
    if NPCESPObjects[model] then
        local d = NPCESPObjects[model]
        for _, v in pairs(d) do pcall(function() v:Remove() end) end
        NPCESPObjects[model] = nil
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

local function UpdateNPCEsp()
    if not NPCEspEnabled then
        for model, _ in pairs(NPCESPObjects) do RemoveNPCEsp(model) end
        return
    end
    local npcs = GetNPCs()
    local seen = {}
    for _, model in ipairs(npcs) do
        seen[model] = true
        local root = model:FindFirstChild("HumanoidRootPart")
        local hum = model:FindFirstChild("Humanoid")
        if root and hum and hum.Health > 0 then
            if not NPCESPObjects[model] then CreateNPCEsp(model) end
            local d = NPCESPObjects[model]
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
                d.Name.Text = "[NPC] " .. model.Name
                d.Name.Position = Vector2.new(sp.X, bY-15)
                d.Distance.Visible = true
                d.Distance.Text = math.floor(dist).."m"
                d.Distance.Position = Vector2.new(sp.X, bY+bSize.Y+5)
            else
                for _, v in pairs(d) do pcall(function() v.Visible = false end) end
            end
        else RemoveNPCEsp(model) end
    end
    for model, _ in pairs(NPCESPObjects) do
        if not seen[model] then RemoveNPCEsp(model) end
    end
end

local function EnableESPLoop()
    DisconnectKey("ESPLoop")
    local conn = RunService.RenderStepped:Connect(function()
        UpdateESP()
        UpdateNPCEsp()
    end)
    ActiveConnections["ESPLoop"] = conn
end

local function DisableESPLoop()
    DisconnectKey("ESPLoop")
    ESPEnabled = false
    for _, d in pairs(ESPObjects) do
        for _, v in pairs(d) do pcall(function() v.Visible = false end) end
    end
    for model, _ in pairs(NPCESPObjects) do RemoveNPCEsp(model) end
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
    local bestTarget, bestScore, bestType = nil, math.huge, nil
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
                        local score = math.huge
                        if TargetPriority == "Closest" then score = screenDist
                        elseif TargetPriority == "Lowest" then score = hp
                        elseif TargetPriority == "Farthest" then score = -screenDist
                        elseif TargetPriority == "Crosshair" then score = screenDist end
                        if screenDist <= AimbotFOV and score < bestScore then
                            bestTarget = player; bestScore = score; bestType = "player"
                        end
                    end
                end
            end
        end
    end
    if NPCDetectionEnabled then
        for _, model in ipairs(GetNPCs()) do
            local hum = model:FindFirstChild("Humanoid")
            local root = model:FindFirstChild("HumanoidRootPart")
            if hum and root and hum.Health > 0 then
                local part = model:FindFirstChild(AimbotTargetPart) or root
                if part and not HasWallBetween(camPos, part.Position, model) then
                    local sp, on = Camera:WorldToViewportPoint(part.Position)
                    if on then
                        local screenDist = (Vector2.new(sp.X, sp.Y) - screenCenter).Magnitude
                        if screenDist <= AimbotFOV and screenDist < bestScore then
                            bestTarget = model; bestScore = screenDist; bestType = "npc"
                        end
                    end
                end
            end
        end
    end
    return bestTarget, bestType
end

local function IsTargetValid(target, targetType)
    if not target or not target.Parent then return false end
    if targetType == "player" then
        local char = target.Character
        if not char then return false end
        local hum = char:FindFirstChild("Humanoid")
        return hum and hum.Health > 0
    elseif targetType == "npc" then
        local hum = target:FindFirstChild("Humanoid")
        return hum and hum.Health > 0
    end
    return false
end

local function GetTargetPart(target, targetType)
    if targetType == "player" then
        if not target.Character then return nil end
        return target.Character:FindFirstChild(AimbotTargetPart) or target.Character:FindFirstChild("HumanoidRootPart")
    elseif targetType == "npc" then
        return target:FindFirstChild(AimbotTargetPart) or target:FindFirstChild("HumanoidRootPart")
    end
    return nil
end

local function RunAimbot()
    if not AimbotEnabled then return end
    if AimKeybindEnabled and not AimKeyHeld then return end
    local char = LocalPlayer.Character
    if not char or not char:FindFirstChild("HumanoidRootPart") then return end
    if AimbotStickyTarget and IsTargetValid(AimbotStickyTarget, AimbotStickyType) then
        if AimbotWallCheck then
            local tPart = GetTargetPart(AimbotStickyTarget, AimbotStickyType)
            local tChar = AimbotStickyType == "player" and AimbotStickyTarget.Character or AimbotStickyTarget
            if tPart and HasWallBetween(Camera.CFrame.Position, tPart.Position, tChar) then
                AimbotStickyTarget = nil; AimbotStickyType = nil
            end
        end
    else
        AimbotStickyTarget = nil; AimbotStickyType = nil
    end
    if not AimbotStickyTarget then
        local t, tType = FindTarget()
        AimbotStickyTarget = t; AimbotStickyType = tType
    end
    if not AimbotStickyTarget then return end
    if not IsTargetValid(AimbotStickyTarget, AimbotStickyType) then
        AimbotStickyTarget = nil; AimbotStickyType = nil; return
    end
    local targetPart = GetTargetPart(AimbotStickyTarget, AimbotStickyType)
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

local function TryAutoShoot()
    if not AutoShootEnabled then return end
    local char = LocalPlayer.Character
    if not char then return end
    local tool = char:FindFirstChildOfClass("Tool")
    if not tool then return end
    local screenCenter = Vector2.new(Camera.ViewportSize.X/2, Camera.ViewportSize.Y/2)
    for _, player in pairs(Players:GetPlayers()) do
        if player ~= LocalPlayer and player.Character then
            local hum = player.Character:FindFirstChild("Humanoid")
            local root = player.Character:FindFirstChild("HumanoidRootPart")
            if hum and root and hum.Health > 0 then
                local sp, on = Camera:WorldToViewportPoint(root.Position)
                if on then
                    local dist = (Vector2.new(sp.X, sp.Y) - screenCenter).Magnitude
                    if dist < 50 then
                        pcall(function() tool:Activate() end)
                        break
                    end
                end
            end
        end
    end
end

local AutoShootLast = 0
local function EnableAimbotLoop()
    DisconnectKey("Aimbot")
    local conn = RunService.RenderStepped:Connect(function()
        if AimbotEnabled then RunAimbot() end
        if AutoShootEnabled then
            local now = tick()
            if now - AutoShootLast >= AutoShootDelay/1000 then
                AutoShootLast = now
                TryAutoShoot()
            end
        end
    end)
    ActiveConnections["Aimbot"] = conn
end

--==============================================================
-- DRONE MODE
--==============================================================
local function EnableDroneMode()
    DisconnectKey("DroneMode")
    local conn = RunService.RenderStepped:Connect(function()
        if not DroneModeEnabled then return end
        if not LocalPlayer.Character then return end
        local root = LocalPlayer.Character:FindFirstChild("HumanoidRootPart")
        if not root then return end
        pcall(function()
            Camera.CameraSubject = nil
            Camera.CameraType = Enum.CameraType.Scriptable
            Camera.CFrame = CFrame.new(root.Position + Vector3.new(0, 30, 0), root.Position)
        end)
    end)
    ActiveConnections["DroneMode"] = conn
end

local function DisableDroneMode()
    DisconnectKey("DroneMode")
    DroneModeEnabled = false
    pcall(function()
        Camera.CameraSubject = LocalPlayer.Character and LocalPlayer.Character:FindFirstChild("Humanoid")
        Camera.CameraType = Enum.CameraType.Custom
    end)
end

--==============================================================
-- KILL NOTIF
--==============================================================
local function EnableKillNotif()
    DisconnectKey("KillNotif")
    for _, player in pairs(Players:GetPlayers()) do
        if player ~= LocalPlayer and player.Character then
            local hum = player.Character:FindFirstChild("Humanoid")
            if hum then LastPlayerHealth[player] = hum.Health end
        end
    end
    local conn = RunService.Heartbeat:Connect(function()
        if not KillNotifEnabled then return end
        for _, player in pairs(Players:GetPlayers()) do
            if player ~= LocalPlayer and player.Character then
                local hum = player.Character:FindFirstChild("Humanoid")
                if hum then
                    local lastHp = LastPlayerHealth[player] or 100
                    if hum.Health <= 0 and lastHp > 0 then
                        Notify("💀 KILL", "> " .. player.Name .. " mati!", 3)
                    end
                    LastPlayerHealth[player] = hum.Health
                end
            end
        end
    end)
    ActiveConnections["KillNotif"] = conn
end
local function DisableKillNotif() DisconnectKey("KillNotif"); KillNotifEnabled = false end

--==============================================================
-- INFO PANEL
--==============================================================
local function CreateInfoPanel()
    if InfoPanelFrame then pcall(function() InfoPanelFrame:Destroy() end) end
    InfoPanelFrame = Instance.new("Frame")
    InfoPanelFrame.Name = "ZetInfoPanel"
    InfoPanelFrame.Size = UDim2.new(0, 180, 0, 70)
    InfoPanelFrame.Position = UDim2.new(1, -190, 1, -80)
    InfoPanelFrame.BackgroundColor3 = THEME.PanelBG
    InfoPanelFrame.BackgroundTransparency = 0.2
    InfoPanelFrame.BorderColor3 = THEME.Accent
    InfoPanelFrame.BorderSizePixel = 2
    InfoPanelFrame.ZIndex = 100
    InfoPanelFrame.Parent = ScreenGui
    Instance.new("UICorner", InfoPanelFrame).CornerRadius = UDim.new(0, 8)

    local InfoPanelLabel = Instance.new("TextLabel")
    InfoPanelLabel.Size = UDim2.new(1, -10, 1, -10)
    InfoPanelLabel.Position = UDim2.new(0, 5, 0, 5)
    InfoPanelLabel.BackgroundTransparency = 1
    InfoPanelLabel.Text = "Ping: -- | Players: --\nTime: --"
    InfoPanelLabel.TextColor3 = THEME.Text
    InfoPanelLabel.Font = Enum.Font.Code
    InfoPanelLabel.TextSize = 10
    InfoPanelLabel.TextXAlignment = Enum.TextXAlignment.Left
    InfoPanelLabel.TextYAlignment = Enum.TextYAlignment.Top
    InfoPanelLabel.ZIndex = 101
    InfoPanelLabel.Parent = InfoPanelFrame

    task.spawn(function()
        while task.wait(1) do
            if not InfoPanelFrame or not InfoPanelFrame.Parent then break end
            pcall(function()
                local ping = math.floor(LocalPlayer:GetNetworkPing() * 1000)
                local pc = #Players:GetPlayers()
                local time = os.date("%H:%M:%S")
                InfoPanelLabel.Text = "Ping: " .. ping .. "ms | Players: " .. pc .. "\nTime: " .. time
            end)
        end
    end)
end

local function DestroyInfoPanel()
    if InfoPanelFrame then
        pcall(function() InfoPanelFrame:Destroy() end)
        InfoPanelFrame = nil
    end
end

--==============================================================
-- SERVER HOP / TELEPORT
--==============================================================
local function FetchServerList(placeId)
    local servers, cursor = {}, ""
    for i = 1, 2 do
        local url = "https://games.roblox.com/v1/games/" .. placeId .. "/servers/Public?sortOrder=Asc&limit=100"
        if cursor ~= "" then url = url .. "&cursor=" .. cursor end
        local ok, result = pcall(function() return HttpService:JSONDecode(game:HttpGet(url)) end)
        if ok and result and result.data then
            for _, srv in ipairs(result.data) do
                if srv.playing and srv.maxPlayers and srv.playing < srv.maxPlayers and srv.id ~= game.JobId then
                    table.insert(servers, srv)
                end
            end
            cursor = result.nextPageCursor or ""
            if cursor == "" then break end
        else break end
    end
    return #servers > 0, servers
end

local function DoServerHop()
    if ServerHopRunning then return end
    ServerHopRunning = true
    Notify("Server Hop", "> MENCARI...", 3)
    task.spawn(function()
        local ok, servers = FetchServerList(game.PlaceId)
        if not ok then Notify("Server Hop", "> GAGAL", 3); ServerHopRunning = false; return end
        local target = servers[math.random(1, #servers)]
        pcall(function() TeleportService:TeleportToPlaceInstance(game.PlaceId, target.id, LocalPlayer) end)
    end)
end

local function DoBestServerHop()
    if ServerHopRunning then return end
    ServerHopRunning = true
    task.spawn(function()
        local ok, servers = FetchServerList(game.PlaceId)
        if not ok then Notify("Server Hop", "> TIDAK ADA", 3); ServerHopRunning = false; return end
        table.sort(servers, function(a, b) return (a.playing or 0) < (b.playing or 0) end)
        pcall(function() TeleportService:TeleportToPlaceInstance(game.PlaceId, servers[1].id, LocalPlayer) end)
    end)
end

local function DoRejoin()
    pcall(function() TeleportService:TeleportToPlaceInstance(game.PlaceId, game.JobId, LocalPlayer) end)
end

local function TeleportToPlayer(targetPlayer)
    if not targetPlayer or not targetPlayer.Character then return end
    local tRoot = targetPlayer.Character:FindFirstChild("HumanoidRootPart")
    local lRoot = LocalPlayer.Character and LocalPlayer.Character:FindFirstChild("HumanoidRootPart")
    if not tRoot or not lRoot then return end
    pcall(function()
        lRoot.CFrame = CFrame.new(tRoot.Position + Vector3.new(0, 3, 0))
        Notify("Teleport", "> TO: " .. targetPlayer.Name, 2)
    end)
end

local function RefreshTeleportList()
    if not TeleportListContainer then return end
    for _, item in pairs(TeleportPlayerList) do pcall(function() item:Destroy() end) end
    TeleportPlayerList = {}
    local y = 0
    local count = 0
    for _, player in pairs(Players:GetPlayers()) do
        if player ~= LocalPlayer then
            local btn = Instance.new("TextButton")
            btn.Size = UDim2.new(1, 0, 0, 28)
            btn.Position = UDim2.new(0, 0, 0, y)
            btn.BackgroundColor3 = THEME.ButtonBG
            btn.BorderColor3 = THEME.Accent
            btn.BorderSizePixel = 1
            btn.Text = "> " .. player.Name
            btn.TextColor3 = THEME.Text
            btn.Font = Enum.Font.Code
            btn.TextSize = 11
            btn.TextXAlignment = Enum.TextXAlignment.Left
            btn.ZIndex = 14
            btn.Parent = TeleportListContainer
            Instance.new("UICorner", btn).CornerRadius = UDim.new(0, 3)
            btn.MouseButton1Click:Connect(function() TeleportToPlayer(player) end)
            table.insert(TeleportPlayerList, btn)
            y = y + 32
            count = count + 1
        end
    end
    if count == 0 then
        local empty = Instance.new("TextLabel")
        empty.Size = UDim2.new(1, 0, 0, 28)
        empty.BackgroundTransparency = 1
        empty.Text = "> Tidak ada player lain"
        empty.TextColor3 = THEME.TextLight
        empty.Font = Enum.Font.Code
        empty.TextSize = 10
        empty.ZIndex = 14
        empty.Parent = TeleportListContainer
        y = 32
    end
    if TeleportListFrame then TeleportListFrame.CanvasSize = UDim2.new(0, 0, 0, y + 10) end
end

local function TeleportToMouse()
    if not LocalPlayer.Character then return end
    local r = LocalPlayer.Character:FindFirstChild("HumanoidRootPart")
    if not r then return end
    local hit = Mouse.Hit
    if hit then
        pcall(function()
            r.CFrame = CFrame.new(hit.Position + Vector3.new(0, 3, 0))
            Notify("Teleport", "> TO MOUSE", 2)
        end)
    end
end

local function SaveLocation()
    if LocalPlayer.Character and LocalPlayer.Character:FindFirstChild("HumanoidRootPart") then
        SavedLocation = LocalPlayer.Character.HumanoidRootPart.CFrame
        Notify("Save", "> SAVED", 2)
    end
end

local function LoadLocation()
    if SavedLocation and LocalPlayer.Character and LocalPlayer.Character:FindFirstChild("HumanoidRootPart") then
        pcall(function()
            LocalPlayer.Character.HumanoidRootPart.CFrame = SavedLocation
            Notify("Save", "> TELEPORTED", 2)
        end)
    else Notify("Save", "> NO SAVED", 2) end
end

local function AddWaypoint(name)
    if not LocalPlayer.Character or not LocalPlayer.Character:FindFirstChild("HumanoidRootPart") then return end
    table.insert(Waypoints, {Name = name, CFrame = LocalPlayer.Character.HumanoidRootPart.CFrame})
    Notify("Waypoint", "> Added: " .. name, 2)
end

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

    local BgPattern = Instance.new("Frame")
    BgPattern.Size = UDim2.new(1, 0, 1, 0)
    BgPattern.BackgroundColor3 = Color3.fromRGB(0, 5, 15)
    BgPattern.BackgroundTransparency = 0.3
    BgPattern.BorderSizePixel = 0
    BgPattern.ZIndex = 501
    BgPattern.Parent = LoadingScreen

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
    LTitle.Text = "ZETGAMES V4.4 RESMI"
    LTitle.TextColor3 = THEME.Text
    LTitle.Font = Enum.Font.Code
    LTitle.TextSize = 20
    LTitle.ZIndex = 503
    LTitle.Parent = LoadingBg

    local LTag = Instance.new("TextLabel")
    LTag.Size = UDim2.new(1, -20, 0, 20)
    LTag.Position = UDim2.new(0, 10, 0, 58)
    LTag.BackgroundTransparency = 1
    LTag.Text = "[ OFFICIAL RELEASE ]"
    LTag.TextColor3 = Color3.fromRGB(0, 255, 200)
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
    LVersion.Text = "V4.4 | rscripts.net/@ZetGames"
    LVersion.TextColor3 = Color3.fromRGB(60, 100, 140)
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
    LTopTxt.Text = "● ZETGAMES-AIMLOCK V4.4"
    LTopTxt.TextColor3 = THEME.Text
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
    LTag2.Text = "[ RESMI + NIGHT LOCK ACTIVE ]"
    LTag2.TextColor3 = Color3.fromRGB(0, 255, 200)
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
    TitleText.Text = "● V4.4 RESMI [NIGHT LOCK]"
    TitleText.TextColor3 = THEME.Text
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
    ScrollFrame.CanvasSize = UDim2.new(0, 0, 0, 5600)
    ScrollFrame.ScrollingEnabled = true
    ScrollFrame.ElasticBehavior = Enum.ElasticBehavior.WhenScrollable
    ScrollFrame.ZIndex = 101
    ScrollFrame.Parent = MainHub

    local ScrollContent = Instance.new("Frame")
    ScrollContent.Size = UDim2.new(1, 0, 0, 5600)
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
        btn.MouseButton1Click:Connect(function() Notify("🔒 Locked", "> Tidak bisa dimatiin", 2) end)
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

    -- SAFE MODE
    Section("=== 🛡️ SAFE MODE (LOCKED) ===", 10)
    LockedToggle("> 🛡️ ANTI-KICK: ON (SAFE)", 42)
    LockedToggle("> 🔄 AUTO-RECONNECT: ON", 82)
    LockedToggle("> 🔒 NIGHT LOCK: ON (AUTO KICK)", 122)

    -- THEME
    Section("=== 🎨 THEME SWITCHER ===", 170)
    local ThemeLbl = Instance.new("TextLabel")
    ThemeLbl.Size = UDim2.new(1, -20, 0, 18)
    ThemeLbl.Position = UDim2.new(0, 10, 0, 202)
    ThemeLbl.BackgroundTransparency = 1
    ThemeLbl.Text = "> THEME: BIRU"
    ThemeLbl.TextColor3 = THEME.Text
    ThemeLbl.Font = Enum.Font.Code
    ThemeLbl.TextSize = 10
    ThemeLbl.TextXAlignment = Enum.TextXAlignment.Left
    ThemeLbl.ZIndex = 102
    ThemeLbl.Parent = ScrollContent

    local ThemeBtnFrame = Instance.new("Frame")
    ThemeBtnFrame.Size = UDim2.new(1, -20, 0, 30)
    ThemeBtnFrame.Position = UDim2.new(0, 10, 0, 224)
    ThemeBtnFrame.BackgroundTransparency = 1
    ThemeBtnFrame.ZIndex = 102
    ThemeBtnFrame.Parent = ScrollContent

    local function ThemeBtn(text, themeName, xPos)
        local b = Instance.new("TextButton")
        b.Size = UDim2.new(0.19, 0, 1, 0)
        b.Position = UDim2.new(xPos, 0, 0, 0)
        b.BackgroundColor3 = THEME.ButtonBG
        b.BorderColor3 = THEME.Accent
        b.BorderSizePixel = 1
        b.Text = text
        b.TextColor3 = THEME.Text
        b.Font = Enum.Font.Code
        b.TextSize = 9
        b.ZIndex = 103
        b.Parent = ThemeBtnFrame
        Instance.new("UICorner", b).CornerRadius = UDim.new(0, 3)
        b.MouseButton1Click:Connect(function()
            local preset = ThemePresets[themeName]
            if preset then
                for k, v in pairs(preset) do THEME[k] = v end
                CurrentThemeName = themeName
                ThemeLbl.Text = "> THEME: " .. string.upper(themeName)
                Notify("Theme", "> " .. themeName, 2)
            end
        end)
    end
    ThemeBtn("BIRU", "Biru", 0)
    ThemeBtn("MERAH", "Merah", 0.205)
    ThemeBtn("HIJAU", "Hijau", 0.41)
    ThemeBtn("UNGU", "Ungu", 0.615)
    ThemeBtn("KUNING", "Kuning", 0.82)

    -- USER INFO
    Section("=== USER INFORMATION ===", 268)
    local UIF = Instance.new("Frame")
    UIF.Size = UDim2.new(1, -20, 0, 80)
    UIF.Position = UDim2.new(0, 10, 0, 300)
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
    BuildLbl.Text = "> BUILD: V4.4 RESMI"
    BuildLbl.TextColor3 = Color3.fromRGB(0, 255, 200)
    BuildLbl.Font = Enum.Font.Code
    BuildLbl.TextSize = 11
    BuildLbl.TextXAlignment = Enum.TextXAlignment.Left
    BuildLbl.ZIndex = 103
    BuildLbl.Parent = UIF

    -- MAIN FEATURES
    Section("=== MAIN FEATURES ===", 393)

    Toggle("> FPS BOOST: OFF", 425, function(btn)
        FPSBoostEnabled = not FPSBoostEnabled
        btn.Text = FPSBoostEnabled and "> FPS BOOST: ON" or "> FPS BOOST: OFF"
        btn.BackgroundColor3 = FPSBoostEnabled and THEME.ButtonActive or THEME.ButtonBG
        if FPSBoostEnabled then EnableFPSBoost() else DisableFPSBoost() end
    end)

    Toggle("> FULLBRIGHT: OFF", 465, function(btn)
        FullbrightEnabled = not FullbrightEnabled
        btn.Text = FullbrightEnabled and "> FULLBRIGHT: ON" or "> FULLBRIGHT: OFF"
        btn.BackgroundColor3 = FullbrightEnabled and THEME.ButtonActive or THEME.ButtonBG
        if FullbrightEnabled then EnableFullbright() else DisableFullbright() end
    end)

    Toggle("> SPEED HACK: OFF", 505, function(btn)
        SpeedHackEnabled = not SpeedHackEnabled
        btn.Text = SpeedHackEnabled and "> SPEED HACK: ON" or "> SPEED HACK: OFF"
        btn.BackgroundColor3 = SpeedHackEnabled and THEME.ButtonActive or THEME.ButtonBG
        if SpeedHackEnabled then EnableSpeedHack() else DisableSpeedHack() end
    end)

    local SpeedInput = Input("> Speed (16-500)", 545, tostring(SpeedMultiplier))
    SpeedInput.FocusLost:Connect(function(enterPressed)
        if enterPressed then
            local ns = tonumber(SpeedInput.Text)
            if ns then SpeedMultiplier = math.clamp(ns, 16, MaxSpeed) end
            SpeedInput.Text = tostring(SpeedMultiplier)
        end
    end)

    Toggle("> INFINITE JUMP: OFF", 581, function(btn)
        InfiniteJumpEnabled = not InfiniteJumpEnabled
        btn.Text = InfiniteJumpEnabled and "> INFINITE JUMP: ON" or "> INFINITE JUMP: OFF"
        btn.BackgroundColor3 = InfiniteJumpEnabled and THEME.ButtonActive or THEME.ButtonBG
        if InfiniteJumpEnabled then EnableInfiniteJump() else DisableInfiniteJump() end
    end)

    Toggle("> NOCLIP: OFF", 621, function(btn)
        NoclipEnabled = not NoclipEnabled
        btn.Text = NoclipEnabled and "> NOCLIP: ON" or "> NOCLIP: OFF"
        btn.BackgroundColor3 = NoclipEnabled and THEME.ButtonActive or THEME.ButtonBG
        if NoclipEnabled then EnableNoclip() else DisableNoclip() end
    end)

    Toggle("> 👻 INVISIBLE: OFF", 661, function(btn)
        InvisibleEnabled = not InvisibleEnabled
        btn.Text = InvisibleEnabled and "> 👻 INVISIBLE: ON" or "> 👻 INVISIBLE: OFF"
        btn.BackgroundColor3 = InvisibleEnabled and THEME.ButtonActive or THEME.ButtonBG
        if InvisibleEnabled then EnableInvisible() else DisableInvisible() end
    end)

    Toggle("> ⚡ DASH: OFF (SHIFT)", 701, function(btn)
        DashEnabled = not DashEnabled
        btn.Text = DashEnabled and "> ⚡ DASH: ON (SHIFT)" or "> ⚡ DASH: OFF (SHIFT)"
        btn.BackgroundColor3 = DashEnabled and THEME.ButtonActive or THEME.ButtonBG
    end)

    -- FLY NORMAL
    Section("=== 🛫 FLY NORMAL ===", 749)
    Toggle("> FLY NORMAL: OFF", 781, function(btn)
        FlyNormalEnabled = not FlyNormalEnabled
        if FlyNormalEnabled then btn.Text = "> FLY NORMAL: ON"; btn.BackgroundColor3 = THEME.ButtonActive; EnableFlyNormal()
        else btn.Text = "> FLY NORMAL: OFF"; btn.BackgroundColor3 = THEME.ButtonBG; DisableFlyNormal() end
    end)
    Half("> MODE: FREE", 821, 0, function(btn)
        FlyNormalMode = FlyNormalMode == "Free" and "Hover" or "Free"
        btn.Text = "> MODE: " .. string.upper(FlyNormalMode)
    end)
    Half("> KEY: WASD", 821, 0.5, function(btn) Notify("Fly", "> WASD + Space", 2) end)
    local FlySpeedInput = Input("> Fly Speed (10-500)", 857, tostring(FlyNormalSpeed))
    FlySpeedInput.FocusLost:Connect(function(enterPressed)
        if enterPressed then
            local ns = tonumber(FlySpeedInput.Text)
            if ns then FlyNormalSpeed = math.clamp(ns, 10, 500) end
            FlySpeedInput.Text = tostring(FlyNormalSpeed)
        end
    end)

    -- AIMBOT
    Section("=== 🎯 AIMBOT + FOV + SILENT ===", 901)

    local AimbotBtn = Instance.new("TextButton")
    AimbotBtn.Size = UDim2.new(1, -20, 0, 42)
    AimbotBtn.Position = UDim2.new(0, 10, 0, 933)
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
        if AimbotEnabled then AimbotBtn.Text = "> AIMBOT: ON"; AimbotBtn.BackgroundColor3 = THEME.ButtonActive; EnableAimbotLoop()
        else AimbotBtn.Text = "> AIMBOT: OFF"; AimbotBtn.BackgroundColor3 = THEME.ButtonBG; AimbotStickyTarget = nil; AimbotStickyType = nil; DisconnectKey("Aimbot") end
    end)

    Toggle("> 🎯 SILENT AIM: OFF", 985, function(btn)
        SilentAimEnabled = not SilentAimEnabled
        btn.Text = SilentAimEnabled and "> 🎯 SILENT AIM: ON" or "> 🎯 SILENT AIM: OFF"
        btn.BackgroundColor3 = SilentAimEnabled and THEME.ButtonActive or THEME.ButtonBG
    end)

    Half("> FOV: OFF", 1025, 0, function(btn)
        FOVCircleEnabled = not FOVCircleEnabled
        btn.Text = FOVCircleEnabled and "> FOV: ON" or "> FOV: OFF"
        btn.BackgroundColor3 = FOVCircleEnabled and THEME.ButtonActive or THEME.ButtonBG
        if FOVCircleEnabled then EnableFOVLoop() else DisableFOVLoop() end
    end)
    Half("> TEAM: OFF", 1025, 0.5, function(btn)
        AimbotTeamCheck = not AimbotTeamCheck
        btn.Text = AimbotTeamCheck and "> TEAM: ON" or "> TEAM: OFF"
        btn.BackgroundColor3 = AimbotTeamCheck and THEME.ButtonActive or THEME.ButtonBG
    end)

    local FOVInput = Input("> FOV Radius (50-5000)", 1063, tostring(FOVRadius))
    FOVInput.FocusLost:Connect(function(enterPressed)
        if enterPressed then
            local nf = tonumber(FOVInput.Text)
            if nf then FOVRadius = math.clamp(nf, 50, FOVMaxRadius); AimbotFOV = FOVRadius end
            FOVInput.Text = tostring(FOVRadius)
        end
    end)

    Toggle("> KEYBIND AIMBOT (E): OFF", 1099, function(btn)
        AimKeybindEnabled = not AimKeybindEnabled
        btn.Text = AimKeybindEnabled and "> KEYBIND (E): ON" or "> KEYBIND (E): OFF"
        btn.BackgroundColor3 = AimKeybindEnabled and THEME.ButtonActive or THEME.ButtonBG
    end)

    Toggle("> WALL CHECK: OFF", 1139, function(btn)
        AimbotWallCheck = not AimbotWallCheck
        btn.Text = AimbotWallCheck and "> WALL: ON" or "> WALL: OFF"
        btn.BackgroundColor3 = AimbotWallCheck and THEME.ButtonActive or THEME.ButtonBG
    end)

    Toggle("> 🔫 AUTO SHOOT: OFF", 1179, function(btn)
        AutoShootEnabled = not AutoShootEnabled
        btn.Text = AutoShootEnabled and "> AUTO SHOOT: ON" or "> AUTO SHOOT: OFF"
        btn.BackgroundColor3 = AutoShootEnabled and THEME.ButtonActive or THEME.ButtonBG
        if AutoShootEnabled then EnableAimbotLoop() end
    end)

    Toggle("> 📡 OFF-SCREEN ARROW: OFF", 1219, function(btn)
        OffScreenArrowEnabled = not OffScreenArrowEnabled
        btn.Text = OffScreenArrowEnabled and "> OFF-ARROW: ON" or "> OFF-ARROW: OFF"
        btn.BackgroundColor3 = OffScreenArrowEnabled and THEME.ButtonActive or THEME.ButtonBG
        if OffScreenArrowEnabled then EnableOffScreenArrow() else DisableOffScreenArrow() end
    end)

    -- ESP
    Section("=== 👁️ FULL ESP ===", 1267)
    Toggle("> ESP MASTER: OFF", 1299, function(btn)
        ESPEnabled = not ESPEnabled
        btn.Text = ESPEnabled and "> ESP MASTER: ON" or "> ESP MASTER: OFF"
        btn.BackgroundColor3 = ESPEnabled and THEME.ButtonActive or THEME.ButtonBG
        if ESPEnabled then EnableESPLoop() else DisableESPLoop() end
    end)
    Toggle("> 🌈 RAINBOW ESP: OFF", 1339, function(btn)
        RainbowESPEnabled = not RainbowESPEnabled
        btn.Text = RainbowESPEnabled and "> 🌈 RAINBOW: ON" or "> 🌈 RAINBOW: OFF"
        btn.BackgroundColor3 = RainbowESPEnabled and THEME.ButtonActive or THEME.ButtonBG
        if RainbowESPEnabled then EnableRainbowESP() else DisableRainbowESP() end
    end)
    Toggle("> NPC ESP: OFF", 1379, function(btn)
        NPCEspEnabled = not NPCEspEnabled
        btn.Text = NPCEspEnabled and "> NPC ESP: ON" or "> NPC ESP: OFF"
        btn.BackgroundColor3 = NPCEspEnabled and THEME.ButtonActive or THEME.ButtonBG
        if not NPCEspEnabled then for model, _ in pairs(NPCESPObjects) do RemoveNPCEsp(model) end end
    end)
    Toggle("> NPC DETECTION: OFF", 1419, function(btn)
        NPCDetectionEnabled = not NPCDetectionEnabled
        btn.Text = NPCDetectionEnabled and "> NPC DETECTION: ON" or "> NPC DETECTION: OFF"
        btn.BackgroundColor3 = NPCDetectionEnabled and THEME.ButtonActive or THEME.ButtonBG
    end)

    -- HITBOX
    Section("=== 🎯 HITBOX ===", 1467)
    Toggle("> HITBOX: OFF", 1499, function(btn)
        HitboxEnabled = not HitboxEnabled
        if HitboxEnabled then btn.Text = "> HITBOX: ON"; btn.BackgroundColor3 = THEME.ButtonActive; EnableHitboxExpander()
        else btn.Text = "> HITBOX: OFF"; btn.BackgroundColor3 = THEME.ButtonBG; DisableHitboxExpander() end
    end)
    local HitboxInput = Input("> Size (1-1000)", 1539, tostring(HitboxSize))
    HitboxInput.FocusLost:Connect(function(enterPressed)
        if enterPressed then
            local nh = tonumber(HitboxInput.Text)
            if nh then HitboxSize = math.clamp(nh, 1, 1000) end
            HitboxInput.Text = tostring(HitboxSize)
        end
    end)

    -- DRONE
    Section("=== 🚁 DRONE MODE ===", 1585)
    Toggle("> DRONE CAMERA: OFF", 1617, function(btn)
        DroneModeEnabled = not DroneModeEnabled
        btn.Text = DroneModeEnabled and "> DRONE: ON" or "> DRONE: OFF"
        btn.BackgroundColor3 = DroneModeEnabled and THEME.ButtonActive or THEME.ButtonBG
        if DroneModeEnabled then EnableDroneMode() else DisableDroneMode() end
    end)

    -- SURVIVAL
    Section("=== SURVIVAL ===", 1665)
    Toggle("> AUTO RESPAWN: OFF", 1697, function(btn)
        AutoRespawnEnabled = not AutoRespawnEnabled
        btn.Text = AutoRespawnEnabled and "> AUTO RESPAWN: ON" or "> AUTO RESPAWN: OFF"
        btn.BackgroundColor3 = AutoRespawnEnabled and THEME.ButtonActive or THEME.ButtonBG
        if AutoRespawnEnabled then EnableAutoRespawn() else DisableAutoRespawn() end
    end)
    Toggle("> ANTI-FLING: OFF", 1737, function(btn)
        AntiFlingEnabled = not AntiFlingEnabled
        btn.Text = AntiFlingEnabled and "> ANTI-FLING: ON" or "> ANTI-FLING: OFF"
        btn.BackgroundColor3 = AntiFlingEnabled and THEME.ButtonActive or THEME.ButtonBG
        if AntiFlingEnabled then EnableAntiFling() else DisableAntiFling() end
    end)
    Toggle("> ANTI-AFK: OFF", 1777, function(btn)
        AntiAFKEnabled = not AntiAFKEnabled
        btn.Text = AntiAFKEnabled and "> ANTI-AFK: ON" or "> ANTI-AFK: OFF"
        btn.BackgroundColor3 = AntiAFKEnabled and THEME.ButtonActive or THEME.ButtonBG
        if AntiAFKEnabled then EnableAntiAFK() else DisableAntiAFK() end
    end)

    -- FLY-VOID
    Section("=== 🕳️ FLY-VOID V2 ===", 1825)
    Toggle("> FLY-VOID: OFF", 1857, function(btn)
        FlyVoidEnabled = not FlyVoidEnabled
        if FlyVoidEnabled then btn.Text = "> FLY-VOID: ON"; btn.BackgroundColor3 = THEME.ButtonActive; EnableFlyVoid()
        else btn.Text = "> FLY-VOID: OFF"; btn.BackgroundColor3 = THEME.ButtonBG; DisableFlyVoid() end
    end)
    Half("> HIDE: OFF", 1897, 0, function(btn)
        FlyVoidHideMode = not FlyVoidHideMode
        btn.Text = FlyVoidHideMode and "> HIDE: ON" or "> HIDE: OFF"
        btn.BackgroundColor3 = FlyVoidHideMode and THEME.ButtonActive or THEME.ButtonBG
    end)
    Half("> KEY: V", 1897, 0.5, function(btn) Notify("Fly-Void", "> Tekan V", 2) end)

    -- SOUND
    Section("=== SOUND ESP ===", 1945)
    Toggle("> SOUND ESP: OFF", 1977, function(btn)
        SoundESPEnabled = not SoundESPEnabled
        btn.Text = SoundESPEnabled and "> SOUND ESP: ON" or "> SOUND ESP: OFF"
        btn.BackgroundColor3 = SoundESPEnabled and THEME.ButtonActive or THEME.ButtonBG
        if SoundESPEnabled then EnableSoundESP() else DisableSoundESP() end
    end)

    -- MUSIC
    Section("=== 🎵 MUSIC PLAYLIST V2 ===", 2025)
    Toggle("> MUSIC: OFF", 2057, function(btn)
        MusicPlayerEnabled = not MusicPlayerEnabled
        btn.Text = MusicPlayerEnabled and "> MUSIC: ON" or "> MUSIC: OFF"
        btn.BackgroundColor3 = MusicPlayerEnabled and THEME.ButtonActive or THEME.ButtonBG
        if MusicPlayerEnabled then PlayMusic() else StopMusic() end
    end)
    Half("> ⏮ PREV", 2097, 0, function(btn) PrevMusic() end)
    Half("> ⏭ NEXT", 2097, 0.5, function(btn) NextMusic() end)
    Half("> SHUFFLE: OFF", 2134, 0, function(btn)
        MusicShuffle = not MusicShuffle
        btn.Text = MusicShuffle and "> SHUFFLE: ON" or "> SHUFFLE: OFF"
        btn.BackgroundColor3 = MusicShuffle and THEME.ButtonActive or THEME.ButtonBG
    end)
    Half("> REPEAT: ON", 2134, 0.5, function(btn)
        MusicRepeatAll = not MusicRepeatAll
        btn.Text = MusicRepeatAll and "> REPEAT: ON" or "> REPEAT: OFF"
        btn.BackgroundColor3 = MusicRepeatAll and THEME.ButtonActive or THEME.ButtonBG
    end)

    -- KILL NOTIF
    Section("=== 🔔 KILL/DEATH NOTIF ===", 2182)
    Toggle("> KILL NOTIF: OFF", 2214, function(btn)
        KillNotifEnabled = not KillNotifEnabled
        btn.Text = KillNotifEnabled and "> KILL NOTIF: ON" or "> KILL NOTIF: OFF"
        btn.BackgroundColor3 = KillNotifEnabled and THEME.ButtonActive or THEME.ButtonBG
        if KillNotifEnabled then EnableKillNotif() else DisableKillNotif() end
    end)

    -- INFO PANEL
    Section("=== 📊 INFO PANEL ===", 2262)
    Toggle("> INFO PANEL: OFF", 2294, function(btn)
        InfoPanelEnabled = not InfoPanelEnabled
        btn.Text = InfoPanelEnabled and "> INFO PANEL: ON" or "> INFO PANEL: OFF"
        btn.BackgroundColor3 = InfoPanelEnabled and THEME.ButtonActive or THEME.ButtonBG
        if InfoPanelEnabled then CreateInfoPanel() else DestroyInfoPanel() end
    end)

    -- WAYPOINT
    Section("=== 🗺️ WAYPOINT ===", 2342)
    local WPInput = Input("> Waypoint name", 2374, "Base")
    Toggle("> ➕ ADD WAYPOINT", 2411, function(btn) AddWaypoint(WPInput.Text) end)

    -- CHAT SPAM
    Section("=== CHAT SPAM ===", 2459)
    Toggle("> CHAT SPAM: OFF", 2491, function(btn)
        ChatSpamEnabled = not ChatSpamEnabled
        btn.Text = ChatSpamEnabled and "> CHAT SPAM: ON" or "> CHAT SPAM: OFF"
        btn.BackgroundColor3 = ChatSpamEnabled and THEME.ButtonActive or THEME.ButtonBG
        if ChatSpamEnabled then EnableChatSpam() else DisableChatSpam() end
    end)
    local ChatInput = Input("> Message", 2531, ChatSpamText)
    ChatInput.FocusLost:Connect(function(enterPressed)
        if enterPressed and ChatInput.Text ~= "" then ChatSpamText = ChatInput.Text end
    end)

    -- SERVER HOP
    Section("=== 🌐 SERVER HOP ===", 2577)
    Toggle("> 🌐 SERVER HOP (RANDOM)", 2609, function(btn) DoServerHop() end)
    Half("> 🎯 BEST SERVER", 2649, 0, function(btn) DoBestServerHop() end)
    Half("> 🔄 REJOIN", 2649, 0.5, function(btn) DoRejoin() end)

    -- TELEPORT KE ORANG
    Section("=== 🆕 TELEPORT KE ORANG ===", 2697)
    TeleportListFrame = Instance.new("ScrollingFrame")
    TeleportListFrame.Size = UDim2.new(1, -20, 0, 130)
    TeleportListFrame.Position = UDim2.new(0, 10, 0, 2729)
    TeleportListFrame.BackgroundColor3 = THEME.PanelBG
    TeleportListFrame.BorderColor3 = THEME.Accent
    TeleportListFrame.BorderSizePixel = 1
    TeleportListFrame.ScrollBarThickness = 5
    TeleportListFrame.ScrollBarImageColor3 = THEME.Accent
    TeleportListFrame.CanvasSize = UDim2.new(0, 0, 0, 0)
    TeleportListFrame.ZIndex = 102
    TeleportListFrame.Parent = ScrollContent
    Instance.new("UICorner", TeleportListFrame).CornerRadius = UDim.new(0, 4)
    TeleportListContainer = Instance.new("Frame")
    TeleportListContainer.Size = UDim2.new(1, -10, 1, -10)
    TeleportListContainer.Position = UDim2.new(0, 5, 0, 5)
    TeleportListContainer.BackgroundTransparency = 1
    TeleportListContainer.ZIndex = 103
    TeleportListContainer.Parent = TeleportListFrame
    task.spawn(function()
        while task.wait(2) do
            if IsLoggedIn then RefreshTeleportList() end
        end
    end)

    -- TELEPORT
    Section("=== TELEPORT ===", 2879)
    Toggle("> TELEPORT TO MOUSE", 2911, function(btn) TeleportToMouse() end)
    Half("> SAVE LOC", 2951, 0, function(btn) SaveLocation() end)
    Half("> LOAD LOC", 2951, 0.5, function(btn) LoadLocation() end)

    -- ⭐ SOCIAL SECTION
    Section("=== ⭐ ZETGAMES OFFICIAL ===", 2999)

    local SocialInfo = Instance.new("TextLabel")
    SocialInfo.Size = UDim2.new(1, -20, 0, 60)
    SocialInfo.Position = UDim2.new(0, 10, 0, 3031)
    SocialInfo.BackgroundColor3 = THEME.PanelBG
    SocialInfo.BorderColor3 = THEME.Accent
    SocialInfo.BorderSizePixel = 1
    SocialInfo.Text = "> Follow: rscripts.net/@ZetGames\n> Update tiap 2 minggu\n> V4.5 coming soon!"
    SocialInfo.TextColor3 = THEME.TextLight
    SocialInfo.Font = Enum.Font.Code
    SocialInfo.TextSize = 10
    SocialInfo.TextXAlignment = Enum.TextXAlignment.Left
    SocialInfo.TextYAlignment = Enum.TextYAlignment.Top
    SocialInfo.ZIndex = 102
    SocialInfo.Parent = ScrollContent
    Instance.new("UICorner", SocialInfo).CornerRadius = UDim.new(0, 4)

    local PromoteBtn = Instance.new("TextButton")
    PromoteBtn.Size = UDim2.new(1, -20, 0, 42)
    PromoteBtn.Position = UDim2.new(0, 10, 0, 3097)
    PromoteBtn.BackgroundColor3 = Color3.fromRGB(30, 100, 200)
    PromoteBtn.BorderColor3 = Color3.fromRGB(100, 200, 255)
    PromoteBtn.BorderSizePixel = 2
    PromoteBtn.Text = "⭐ FOLLOW @ZetGames NOW"
    PromoteBtn.TextColor3 = Color3.fromRGB(255, 255, 255)
    PromoteBtn.Font = Enum.Font.Code
    PromoteBtn.TextSize = 13
    PromoteBtn.ZIndex = 102
    PromoteBtn.Parent = ScrollContent
    Instance.new("UICorner", PromoteBtn).CornerRadius = UDim.new(0, 5)
    PromoteBtn.MouseButton1Click:Connect(function()
        Notify("⭐ ZetGames", "rscripts.net/@ZetGames", 8)
        Notify("💙 Thanks!", "Dukung creator biar update terus", 6)
    end)

    local PromoteBtn2 = Instance.new("TextButton")
    PromoteBtn2.Size = UDim2.new(0.5, -15, 0, 34)
    PromoteBtn2.Position = UDim2.new(0, 10, 0, 3147)
    PromoteBtn2.BackgroundColor3 = Color3.fromRGB(100, 30, 150)
    PromoteBtn2.BorderColor3 = Color3.fromRGB(180, 100, 255)
    PromoteBtn2.BorderSizePixel = 1
    PromoteBtn2.Text = "🎁 BONUS"
    PromoteBtn2.TextColor3 = Color3.fromRGB(255, 255, 255)
    PromoteBtn2.Font = Enum.Font.Code
    PromoteBtn2.TextSize = 11
    PromoteBtn2.ZIndex = 102
    PromoteBtn2.Parent = ScrollContent
    Instance.new("UICorner", PromoteBtn2).CornerRadius = UDim.new(0, 4)
    PromoteBtn2.MouseButton1Click:Connect(function()
        Notify("🎁 Bonus Follower", "Follower dapet preview V4.5!", 5)
    end)

    local PromoteBtn3 = Instance.new("TextButton")
    PromoteBtn3.Size = UDim2.new(0.5, -15, 0, 34)
    PromoteBtn3.Position = UDim2.new(0.5, 5, 0, 3147)
    PromoteBtn3.BackgroundColor3 = Color3.fromRGB(150, 30, 30)
    PromoteBtn3.BorderColor3 = Color3.fromRGB(255, 100, 100)
    PromoteBtn3.BorderSizePixel = 1
    PromoteBtn3.Text = "📢 SHARE"
    PromoteBtn3.TextColor3 = Color3.fromRGB(255, 255, 255)
    PromoteBtn3.Font = Enum.Font.Code
    PromoteBtn3.TextSize = 11
    PromoteBtn3.ZIndex = 102
    PromoteBtn3.Parent = ScrollContent
    Instance.new("UICorner", PromoteBtn3).CornerRadius = UDim.new(0, 4)
    PromoteBtn3.MouseButton1Click:Connect(function()
        Notify("📢 Share ke Teman", "rscripts.net/@ZetGames", 6)
    end)

    -- ⭐ MENU BUTTON (PAKAI GAMBAR + SAFE ZONE)
    local ToggleMenuButton = Instance.new("TextButton")
    ToggleMenuButton.Name = "ZetMenuButton"
    ToggleMenuButton.Size = UDim2.new(0, 55, 0, 55)
    ToggleMenuButton.Position = UDim2.new(0, 120, 0.5, -27)
    ToggleMenuButton.BackgroundColor3 = Color3.fromRGB(15, 25, 45)
    ToggleMenuButton.BorderColor3 = THEME.Accent
    ToggleMenuButton.BorderSizePixel = 2
    ToggleMenuButton.Text = "≡"  -- Fallback kalau gambar gak load
    ToggleMenuButton.TextColor3 = THEME.Text
    ToggleMenuButton.Font = Enum.Font.Code
    ToggleMenuButton.TextSize = 28
    ToggleMenuButton.TextTransparency = 0  -- Akan di-transparent-kan kalau gambar berhasil
    ToggleMenuButton.ZIndex = 200
    ToggleMenuButton.Visible = false
    ToggleMenuButton.Parent = ScreenGui
    Instance.new("UICorner", ToggleMenuButton).CornerRadius = UDim.new(0, 27)

    -- ⭐ IMAGE LABEL UNTUK LOGO
    if MENU_ICON_ID ~= "" and MENU_ICON_ID ~= "rbxassetid://0" then
        local MenuIcon = Instance.new("ImageLabel")
        MenuIcon.Name = "MenuIcon"
        MenuIcon.Size = UDim2.new(1, -8, 1, -8)
        MenuIcon.Position = UDim2.new(0, 4, 0, 4)
        MenuIcon.BackgroundTransparency = 1
        MenuIcon.Image = MENU_ICON_ID
        MenuIcon.ScaleType = Enum.ScaleType.Fit
        MenuIcon.ZIndex = 201
        MenuIcon.Parent = ToggleMenuButton
        Instance.new("UICorner", MenuIcon).CornerRadius = UDim.new(0, 23)
        
        -- Sembunyikan text kalau gambar berhasil load
        MenuIcon.Visible = true
        ToggleMenuButton.TextTransparency = 1
        
        -- Kalau gambar gagal load, tetap tampilkan simbol ≡
        MenuIcon:GetPropertyChangedSignal("IsLoaded"):Connect(function()
            if not MenuIcon.IsLoaded then
                ToggleMenuButton.TextTransparency = 0
            end
        end)
    end

    -- ✅ SAFE ZONE: hindari area Leave button
    local menuBtnDragging = false
    local menuBtnDragStart = nil
    local menuBtnStartPos = nil
    local menuBtnMoved = false
    local menuBtnLastTap = 0
    local DEFAULT_MENU_POS = UDim2.new(0, 120, 0.5, -27)

    -- ✅ ZONA AMAN (hindari Leave button + chat)
    local SAFE_TOP = 90       -- minimal 90px dari atas
    local SAFE_LEFT = 100     -- minimal 100px dari kiri

    local function clampMenuButtonPos(pos)
        local vp = Camera.ViewportSize
        local btnSize = 55
        local margin = 5
        
        local x = pos.X.Offset
        local y = pos.Y.Offset
        
        -- Clamp dengan safe zone
        x = math.clamp(x, SAFE_LEFT, vp.X - btnSize - margin)
        y = math.clamp(y, SAFE_TOP, vp.Y - btnSize - margin)
        
        return UDim2.new(0, x, 0, y)
    end

    local function resetMenuButtonPos(silent)
        local newPos = clampMenuButtonPos(DEFAULT_MENU_POS)
        TweenService:Create(ToggleMenuButton, TweenInfo.new(0.3, Enum.EasingStyle.Quad), {Position = newPos}):Play()
        if not silent then Notify("📍 Menu Button", "> Posisi di-reset", 2) end
    end

    -- Auto-check: kalau keluar layar → reset
    local lastViewportSize = Camera.ViewportSize
    RunService.Heartbeat:Connect(function()
        local vp = Camera.ViewportSize
        if vp ~= lastViewportSize then
            lastViewportSize = vp
            task.wait(0.1)
            resetMenuButtonPos(true)
        end
        local pos = ToggleMenuButton.AbsolutePosition
        local size = ToggleMenuButton.AbsoluteSize
        if pos.X < -size.X or pos.Y < -size.Y or pos.X > vp.X + size.X or pos.Y > vp.Y + size.Y then
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
        end
    end)

    ToggleMenuButton.InputChanged:Connect(function(input)
        if not menuBtnDragging then return end
        if input.UserInputType == Enum.UserInputType.MouseMovement or input.UserInputType == Enum.UserInputType.Touch then
            local delta = input.Position - menuBtnDragStart
            if math.abs(delta.X) > 10 or math.abs(delta.Y) > 10 then menuBtnMoved = true end
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
            "> Memuat resource...",
            "> Menghubungkan ke server...",
            "> Memuat konfigurasi...",
            "> Memverifikasi build...",
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
        Notify("V4.4 RESMI", "> Silakan login dengan key", 3)
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
            Notify("✅ Success", "WELCOME V4.4 RESMI", 3)
            pcall(ActivateAntiKick)
            pcall(ActivateAutoReconnect)
            pcall(ActivateNightLock)
            Notify("🔒 NIGHT LOCK", "> AUTO KICK ACTIVE", 3)
            task.wait(0.5)
            Notify("⭐ ZetGames", "Follow rscripts.net/@ZetGames", 6)
            task.wait(1)
            Notify("🎁 Bonus", "Update V4.5 coming soon!", 5)
            task.wait(0.3)
            RefreshTeleportList()
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
print("[ZET] V4.4 RESMI loaded!")
