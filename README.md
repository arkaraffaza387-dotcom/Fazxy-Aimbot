--[[
    ZetGames-AimLock V4.4 | OFFICIAL RESMI (FULL FIX)
    Theme: Blue & Black
    Login: ✅ WAJIB KEY
    Anti-Kick: ✅ SAFE MODE
    Night Lock: ✅ ACTIVE (Auto Kick)
    All Features: 100% WORK
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
print("[ZET] Loading V4.4 RESMI (FULL FIX)...")

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
THEME.Shield = Color3.fromRGB(0,255,200)
THEME.Locked = Color3.fromRGB(150,150,150)
THEME.LockedBG = Color3.fromRGB(40,40,40)

--==============================================================
-- HIGH SECURITY
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
-- SCREEN GUI (MULTI-FALLBACK)
--==============================================================
local ScreenGui = Instance.new("ScreenGui")
ScreenGui.Name = "ZetGamesV44Resmi"
ScreenGui.ResetOnSpawn = false
ScreenGui.ZIndexBehavior = Enum.ZIndexBehavior.Sibling
ScreenGui.IgnoreGuiInset = true
ScreenGui.DisplayOrder = 999

local parentOk = false
pcall(function()
    ScreenGui.Parent = LocalPlayer:WaitForChild("PlayerGui", 3)
    parentOk = true
end)
if not parentOk or not ScreenGui.Parent then
    pcall(function()
        ScreenGui.Parent = game:GetService("CoreGui")
        parentOk = true
    end)
end
if not parentOk or not ScreenGui.Parent then
    warn("[ZET] GAGAL SET PARENT SCREENGUI!")
    return
end
print("[ZET] ScreenGui parent =", ScreenGui.Parent.Name)

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

-- Feature flags
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
local FOVThickness = 2
local NPCDetectionEnabled = false
local NPCEspEnabled = false
local NPCWhitelistKeywords = {"pet","shop","vendor","trainer"}
local NPCMaxDistance = 500
local NPCMaxCount = 50
local NPCESPObjects = {}
local ESPEnabled = false
local ESPObjects = {}
local ChamsObjects = {}
local TracerColor = Color3.fromRGB(0,150,255)
local RainbowESPEnabled = false
local RainbowHue = 0
local FlyNormalEnabled = false
local FlyNormalSpeed = 100
local FlyNormalVelocity = nil
local FlyNormalGyro = nil
local FlyKeys = {W=false,A=false,S=false,D=false,Space=false,Ctrl=false}
local FlyVoidEnabled = false
local FlyVoidHideMode = false
local FlyVoidOriginalY = nil
local OrigTrans = {}
local OrigCollide = {}
local FullbrightEnabled = false
local OrigLight = {}
local FPSBoostEnabled = false
local OrigSettings = {}
local SpeedHackEnabled = false
local SpeedMultiplier = 100
local MaxSpeed = 500
local DefaultWalkSpeed = 16
local NoclipEnabled = false
local InfiniteJumpEnabled = false
local ChatSpamEnabled = false
local ChatSpamText = "ZETGAMES-AIMLOCK"
local ChatSpamDelay = 3
local SoundESPEnabled = false
local SoundESPRadius = 100
local SoundESPBeep = nil
local LastBeepTime = 0
local MusicPlayerEnabled = false
local MusicSound = nil
local MusicPlaylist = {
    {Name="Kelingan Mantan", ID="78450316593213"},
    {Name="Teh Hijau", ID="111485011584825"},
}
local MusicCurrentIndex = 1
local MusicVolume = 1
local MusicShuffle = false
local AutoRespawnEnabled = false
local AntiFlingEnabled = false
local AntiAFKEnabled = false
local HitboxEnabled = false
local HitboxSize = 5
local DashEnabled = false
local DashCooldown = 0
local InvisibleEnabled = false
local InvisibleOrigTrans = {}
local AutoShootEnabled = false
local AutoShootDelay = 100
local AutoShootLast = 0
local DroneModeEnabled = false
local KillNotifEnabled = false
local LastPlayerHealth = {}
local InfoPanelEnabled = false
local InfoPanelFrame = nil
local LookAtEnabled = false
local Waypoints = {}
local AntiKickEnabled = true
local AutoReconnectEnabled = true
local WatchdogLastPing = tick()
local WatchdogPingThreshold = 60
local ReconnectAttempts = 0
local MaxReconnectAttempts = 5
local NightLockActive = true
local NightLockKickLog = {}
local NightLockLastScan = 0
local NightLockScanInterval = 1
local TeleportPlayerList = {}
local TeleportListFrame = nil
local TeleportListContainer = nil
local SavedLocation = nil
local ServerHopRunning = false

local FOVCircle = nil
pcall(function()
    FOVCircle = Drawing.new("Circle")
    FOVCircle.Visible = false
    FOVCircle.Thickness = 2
    FOVCircle.NumSides = 90
end)

local OffScreenArrow = nil
pcall(function()
    OffScreenArrow = Drawing.new("Triangle")
    OffScreenArrow.Visible = false
    OffScreenArrow.Filled = true
end)

print("[ZET] State OK")

--==============================================================
-- NOTIFY
--==============================================================
local NotifContainer = Instance.new("Frame")
NotifContainer.Size = UDim2.new(0, 240, 1, 0)
NotifContainer.Position = UDim2.new(1, -250, 0, 10)
NotifContainer.BackgroundTransparency = 1
NotifContainer.ZIndex = 5000
NotifContainer.Parent = ScreenGui

local function Notify(title, msg, dur)
    dur = dur or 2
    local n = Instance.new("Frame")
    n.Size = UDim2.new(1, 0, 0, 50)
    n.Position = UDim2.new(0, 0, 0, -50)
    n.BackgroundColor3 = THEME.PanelBG
    n.BorderColor3 = THEME.Accent
    n.BorderSizePixel = 2
    n.ZIndex = 5001
    n.Parent = NotifContainer
    Instance.new("UICorner", n).CornerRadius = UDim.new(0, 6)
    local t = Instance.new("TextLabel")
    t.Size = UDim2.new(1, -10, 0, 20)
    t.Position = UDim2.new(0, 5, 0, 3)
    t.BackgroundTransparency = 1
    t.Text = title
    t.TextColor3 = THEME.Text
    t.Font = Enum.Font.Code
    t.TextSize = 11
    t.TextXAlignment = Enum.TextXAlignment.Left
    t.ZIndex = 5002
    t.Parent = n
    local m = Instance.new("TextLabel")
    m.Size = UDim2.new(1, -10, 0, 20)
    m.Position = UDim2.new(0, 5, 0, 25)
    m.BackgroundTransparency = 1
    m.Text = msg
    m.TextColor3 = THEME.TextLight
    m.Font = Enum.Font.Code
    m.TextSize = 9
    m.TextXAlignment = Enum.TextXAlignment.Left
    m.ZIndex = 5002
    m.Parent = n
    TweenService:Create(n, TweenInfo.new(0.25), {Position = UDim2.new(0,0,0,0)}):Play()
    task.delay(dur, function()
        local tw = TweenService:Create(n, TweenInfo.new(0.25), {Position = UDim2.new(0,0,0,-50)})
        tw:Play()
        tw.Completed:Connect(function() n:Destroy() end)
    end)
end

--==============================================================
-- FEATURE FUNCTIONS
--==============================================================

--========== FOV ==========
local function EnableFOVLoop()
    DisconnectKey("FOV")
    ActiveConnections["FOV"] = RunService.RenderStepped:Connect(function()
        if not FOVCircle then return end
        if not FOVCircleEnabled or not LocalPlayer.Character then
            pcall(function() FOVCircle.Visible = false end)
            return
        end
        pcall(function()
            FOVCircle.Position = Vector2.new(Camera.ViewportSize.X/2, Camera.ViewportSize.Y/2)
            FOVCircle.Radius = FOVRadius
            FOVCircle.Color = THEME.Accent
            FOVCircle.Thickness = FOVThickness
            FOVCircle.Visible = true
        end)
    end)
end

local function DisableFOVLoop()
    DisconnectKey("FOV")
    if FOVCircle then pcall(function() FOVCircle.Visible = false end) end
end

--========== OFF-SCREEN ARROW ==========
local function EnableOffScreenArrow()
    DisconnectKey("OffScreenArrow")
    ActiveConnections["OffScreenArrow"] = RunService.RenderStepped:Connect(function()
        if not OffScreenArrow then return end
        if not OffScreenArrowEnabled or not LocalPlayer.Character then
            pcall(function() OffScreenArrow.Visible = false end)
            return
        end
        local myRoot = LocalPlayer.Character:FindFirstChild("HumanoidRootPart")
        if not myRoot then return end
        local nearest, nearestDist = nil, math.huge
        for _, p in pairs(Players:GetPlayers()) do
            if p ~= LocalPlayer and p.Character then
                local root = p.Character:FindFirstChild("HumanoidRootPart")
                if root then
                    local d = (root.Position - myRoot.Position).Magnitude
                    if d < nearestDist then nearest = root; nearestDist = d end
                end
            end
        end
        if nearest then
            local sp, onScreen = Camera:WorldToViewportPoint(nearest.Position)
            if not onScreen then
                local dir = (nearest.Position - Camera.CFrame.Position).Unit
                local camDir = Camera.CFrame.LookVector
                local angle = math.atan2(dir.X, dir.Z) - math.atan2(camDir.X, camDir.Z)
                local vp = Camera.ViewportSize
                local cx, cy = vp.X/2, vp.Y/2
                local rad = math.min(vp.X, vp.Y)/2 - 60
                local px = cx + math.sin(angle) * rad
                local py = cy - math.cos(angle) * rad
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
        else
            pcall(function() OffScreenArrow.Visible = false end)
        end
    end)
end

local function DisableOffScreenArrow()
    DisconnectKey("OffScreenArrow")
    if OffScreenArrow then pcall(function() OffScreenArrow.Visible = false end) end
end

--========== ANTI-KICK ==========
local BlockedKw = {"exploit","cheat","hack","aimbot","ban","detect","script","injector","banned","violation","suspicious","anticheat"}
local LegitKw = {"shutdown","restart","update","maintenance","rejoin"}

local function ActivateAntiKick()
    if IsHighSecurityGame() then
        Notify("🛡️ Anti-Kick", "SKIP (game AC kuat)", 3)
        return
    end
    pcall(function()
        if not _G._ZET_OrigKick then _G._ZET_OrigKick = LocalPlayer.Kick end
        LocalPlayer.Kick = function(self, message)
            if not AntiKickEnabled then return _G._ZET_OrigKick(self, message) end
            if not message then return end
            local ml = string.lower(tostring(message))
            for _, kw in ipairs(LegitKw) do
                if string.find(ml, kw, 1, true) then return _G._ZET_OrigKick(self, message) end
            end
            for _, kw in ipairs(BlockedKw) do
                if string.find(ml, kw, 1, true) then
                    Notify("🛡️ Anti-Kick", "Blocked: "..kw, 3)
                    return
                end
            end
            return _G._ZET_OrigKick(self, message)
        end
    end)
    Notify("🛡️ Anti-Kick", "ACTIVE (SAFE)", 2)
end

--========== AUTO-RECONNECT ==========
local function ActivateAutoReconnect()
    DisconnectKey("AutoReconnect")
    WatchdogLastPing = tick()
    ActiveConnections["AutoReconnect"] = RunService.Heartbeat:Connect(function()
        if not AutoReconnectEnabled then return end
        local now = tick()
        if now - WatchdogLastPing > WatchdogPingThreshold then
            WatchdogLastPing = now
            if ReconnectAttempts < MaxReconnectAttempts then
                ReconnectAttempts = ReconnectAttempts + 1
                pcall(function() TeleportService:TeleportToPlaceInstance(game.PlaceId, game.JobId, LocalPlayer) end)
            end
        else
            WatchdogLastPing = now
        end
    end)
end

--========== NIGHT LOCK ==========
local function ActivateNightLock()
    DisconnectKey("NightLock")
    NightLockActive = true
    ActiveConnections["NightLock"] = RunService.Heartbeat:Connect(function()
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
                    Notify("🔒 NIGHT LOCK", plr.Name.." | "..reason, 5)
                    task.wait(0.5)
                    pcall(function()
                        LocalPlayer:Kick("[NIGHT LOCK] "..plr.Name.." | "..reason.."\nOfficial Build V4.4")
                    end)
                    break
                end
            end
        end
    end)
    Notify("🔒 Night Lock", "ACTIVE (AUTO KICK)", 3)
end

--========== NPC ==========
local function IsNPC(model)
    if not model or not model:IsA("Model") then return false end
    if Players:GetPlayerFromCharacter(model) then return false end
    if model == LocalPlayer.Character then return false end
    if not model:FindFirstChild("Humanoid") then return false end
    if not model:FindFirstChild("HumanoidRootPart") then return false end
    if model.Humanoid.Health <= 0 then return false end
    local nl = string.lower(model.Name)
    for _, kw in ipairs(NPCWhitelistKeywords) do
        if string.find(nl, kw, 1, true) then return false end
    end
    local myRoot = LocalPlayer.Character and LocalPlayer.Character:FindFirstChild("HumanoidRootPart")
    local npcRoot = model:FindFirstChild("HumanoidRootPart")
    if myRoot and npcRoot and (npcRoot.Position - myRoot.Position).Magnitude > NPCMaxDistance then return false end
    return true
end

local function GetNPCs()
    local list, count = {}, 0
    for _, obj in pairs(Workspace:GetChildren()) do
        if IsNPC(obj) then
            table.insert(list, obj)
            count = count + 1
            if count >= NPCMaxCount then break end
        end
    end
    return list
end

--========== FLY NORMAL ==========
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
    ActiveConnections["FlyNormal"] = RunService.RenderStepped:Connect(function()
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
        local mv = dir.Magnitude > 0 and dir.Unit * FlyNormalSpeed or Vector3.new(0,0,0)
        FlyNormalVelocity.Velocity = mv
        FlyNormalGyro.CFrame = CFrame.new(r.Position, r.Position + camCF.LookVector)
    end)
end

local function DisableFlyNormal()
    DisconnectKey("FlyNormal")
    if FlyNormalVelocity then pcall(function() FlyNormalVelocity:Destroy() end); FlyNormalVelocity = nil end
    if FlyNormalGyro then pcall(function() FlyNormalGyro:Destroy() end); FlyNormalGyro = nil end
end

--========== FLY VOID ==========
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
    local ray = workspace:Raycast(Vector3.new(root.Position.X,1000,root.Position.Z), Vector3.new(0,-3000,0), rp)
    local floorY = ray and ray.Position.Y or -60
    local targetY = floorY - 5
    pcall(function() root.CFrame = CFrame.new(root.Position.X, targetY, root.Position.Z) end)
    ActiveConnections["FlyVoid"] = RunService.Heartbeat:Connect(function()
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
        if h.Health <= 0 then pcall(function() LocalPlayer:LoadCharacter() end) end
        if FlyVoidHideMode then
            for _, part in pairs(c:GetDescendants()) do
                if part:IsA("BasePart") then
                    if not OrigTrans[part] then
                        OrigTrans[part] = part.Transparency
                        OrigCollide[part] = part.CanCollide
                    end
                    part.Transparency = 0.85
                    part.CanCollide = false
                end
            end
        end
    end)
end

local function DisableFlyVoid()
    DisconnectKey("FlyVoid")
    local char = LocalPlayer.Character
    if char then
        for _, part in pairs(char:GetDescendants()) do
            if part:IsA("BasePart") then
                if OrigTrans[part] then part.Transparency = OrigTrans[part] end
                if OrigCollide[part] ~= nil then part.CanCollide = OrigCollide[part] end
            end
        end
        local root = char:FindFirstChild("HumanoidRootPart")
        if root then
            pcall(function()
                local rp = RaycastParams.new()
                rp.FilterType = Enum.RaycastFilterType.Blacklist
                rp.FilterDescendantsInstances = {char}
                local ray = workspace:Raycast(Vector3.new(root.Position.X,1000,root.Position.Z), Vector3.new(0,-3000,0), rp)
                if ray then root.CFrame = CFrame.new(ray.Position.X, ray.Position.Y + 5, ray.Position.Z)
                elseif FlyVoidOriginalY then root.CFrame = CFrame.new(root.Position.X, FlyVoidOriginalY, root.Position.Z) end
            end)
        end
    end
    OrigTrans = {}; OrigCollide = {}; FlyVoidOriginalY = nil
end

--========== FULLBRIGHT / FPS ==========
local function EnableFullbright()
    OrigLight.Ambient = Lighting.Ambient
    OrigLight.OutdoorAmbient = Lighting.OutdoorAmbient
    OrigLight.Brightness = Lighting.Brightness
    OrigLight.ClockTime = Lighting.ClockTime
    OrigLight.FogEnd = Lighting.FogEnd
    OrigLight.FogStart = Lighting.FogStart
    OrigLight.GlobalShadows = Lighting.GlobalShadows
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
        if OrigLight.Ambient then Lighting.Ambient = OrigLight.Ambient end
        if OrigLight.OutdoorAmbient then Lighting.OutdoorAmbient = OrigLight.OutdoorAmbient end
        if OrigLight.Brightness then Lighting.Brightness = OrigLight.Brightness end
        if OrigLight.ClockTime then Lighting.ClockTime = OrigLight.ClockTime end
        if OrigLight.FogEnd then Lighting.FogEnd = OrigLight.FogEnd end
        if OrigLight.FogStart then Lighting.FogStart = OrigLight.FogStart end
        if OrigLight.GlobalShadows ~= nil then Lighting.GlobalShadows = OrigLight.GlobalShadows end
    end)
end

local function EnableFPSBoost()
    OrigSettings.Shadows = Lighting.GlobalShadows
    OrigSettings.FogEnd = Lighting.FogEnd
    OrigSettings.Brightness = Lighting.Brightness
    Lighting.GlobalShadows = false
    Lighting.FogEnd = 100000
    Lighting.Brightness = 2
    for _, e in pairs(Lighting:GetChildren()) do
        if e:IsA("PostEffect") then pcall(function() e.Enabled = false end) end
    end
end

local function DisableFPSBoost()
    pcall(function()
        if OrigSettings.Shadows ~= nil then Lighting.GlobalShadows = OrigSettings.Shadows end
        if OrigSettings.FogEnd ~= nil then Lighting.FogEnd = OrigSettings.FogEnd end
        if OrigSettings.Brightness ~= nil then Lighting.Brightness = OrigSettings.Brightness end
    end)
end

--========== NOCLIP ==========
local function EnableNoclip()
    DisconnectKey("Noclip")
    ActiveConnections["Noclip"] = RunService.Heartbeat:Connect(function()
        if not NoclipEnabled then return end
        local char = LocalPlayer.Character
        if not char then return end
        local hum = char:FindFirstChildOfClass("Humanoid")
        if hum then pcall(function() hum:ChangeState(Enum.HumanoidStateType.Physics) end) end
        for _, p in pairs(char:GetDescendants()) do
            if p:IsA("BasePart") then p.CanCollide = false end
        end
    end)
end

local function DisableNoclip()
    DisconnectKey("Noclip")
    task.wait(0.1)
    local char = LocalPlayer.Character
    if char then
        local hum = char:FindFirstChildOfClass("Humanoid")
        if hum then pcall(function() hum:ChangeState(Enum.HumanoidStateType.GettingUp) end) end
        for _, p in pairs(char:GetDescendants()) do
            if p:IsA("BasePart") then
                pcall(function()
                    if p.Name == "HumanoidRootPart" then p.CanCollide = false
                    else p.CanCollide = true end
                end)
            end
        end
    end
end

--========== SPEED / JUMP ==========
local function EnableSpeedHack()
    DisconnectKey("Speed")
    ActiveConnections["Speed"] = RunService.Heartbeat:Connect(function()
        if not SpeedHackEnabled then return end
        local char = LocalPlayer.Character
        if not char then return end
        local hum = char:FindFirstChild("Humanoid")
        if hum then hum.WalkSpeed = SpeedMultiplier end
    end)
end

local function DisableSpeedHack()
    DisconnectKey("Speed")
    task.wait(0.05)
    local char = LocalPlayer.Character
    if char then
        local hum = char:FindFirstChild("Humanoid")
        if hum then hum.WalkSpeed = DefaultWalkSpeed end
    end
end

local function EnableInfiniteJump()
    DisconnectKey("Jump")
    ActiveConnections["Jump"] = UserInputService.JumpRequest:Connect(function()
        if not InfiniteJumpEnabled then return end
        if LocalPlayer.Character then
            local hum = LocalPlayer.Character:FindFirstChild("Humanoid")
            if hum then hum:ChangeState(Enum.HumanoidStateType.Jumping) end
        end
    end)
end

local function DisableInfiniteJump() DisconnectKey("Jump") end

--========== DASH ==========
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

--========== INVISIBLE ==========
local function EnableInvisible()
    DisconnectKey("Invisible")
    local char = LocalPlayer.Character
    if not char then return end
    for _, part in pairs(char:GetDescendants()) do
        if part:IsA("BasePart") and part.Name ~= "HumanoidRootPart" then
            if not InvisibleOrigTrans[part] then InvisibleOrigTrans[part] = part.Transparency end
            part.Transparency = 0.95
        elseif part:IsA("Decal") then
            if not InvisibleOrigTrans[part] then InvisibleOrigTrans[part] = part.Transparency end
            part.Transparency = 1
        end
    end
end

local function DisableInvisible()
    DisconnectKey("Invisible")
    local char = LocalPlayer.Character
    if char then
        for _, part in pairs(char:GetDescendants()) do
            if InvisibleOrigTrans[part] then part.Transparency = InvisibleOrigTrans[part] end
        end
    end
    InvisibleOrigTrans = {}
end

--========== HITBOX ==========
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
    ActiveConnections["Hitbox"] = RunService.Heartbeat:Connect(function()
        if not HitboxEnabled then return end
        for _, p in pairs(Players:GetPlayers()) do
            if p ~= LocalPlayer then pcall(ApplyHitbox, p) end
        end
    end)
end

local function DisableHitboxExpander()
    DisconnectKey("Hitbox")
    task.wait(0.05)
    for _, p in pairs(Players:GetPlayers()) do
        if p ~= LocalPlayer and p.Character then
            local head = p.Character:FindFirstChild("Head")
            local hrp = p.Character:FindFirstChild("HumanoidRootPart")
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

--========== ANTI FLING / AFK ==========
local function EnableAntiFling()
    DisconnectKey("AntiFling")
    ActiveConnections["AntiFling"] = RunService.Heartbeat:Connect(function()
        if not AntiFlingEnabled then return end
        if LocalPlayer.Character then
            local r = LocalPlayer.Character:FindFirstChild("HumanoidRootPart")
            if r and r.AssemblyLinearVelocity.Magnitude > 500 then
                pcall(function() r.AssemblyLinearVelocity = Vector3.new(0,0,0) end)
            end
        end
    end)
end
local function DisableAntiFling() DisconnectKey("AntiFling") end

local function EnableAntiAFK()
    DisconnectKey("AntiAFK")
    ActiveConnections["AntiAFK"] = RunService.Heartbeat:Connect(function()
        if not AntiAFKEnabled then return end
        pcall(function()
            VirtualUser:CaptureController()
            VirtualUser:ClickButton2(Vector2.new())
        end)
    end)
end
local function DisableAntiAFK() DisconnectKey("AntiAFK") end

local function EnableAutoRespawn()
    DisconnectKey("AutoRespawn")
    ActiveConnections["AutoRespawn"] = RunService.Heartbeat:Connect(function()
        if not AutoRespawnEnabled then return end
        if LocalPlayer.Character then
            local hum = LocalPlayer.Character:FindFirstChild("Humanoid")
            if hum and hum.Health <= 0 then pcall(function() LocalPlayer:LoadCharacter() end) end
        end
    end)
end
local function DisableAutoRespawn() DisconnectKey("AutoRespawn") end

--========== SOUND / MUSIC / CHAT ==========
local function EnableSoundESP()
    DisconnectKey("SoundESP")
    if SoundESPBeep then pcall(function() SoundESPBeep:Destroy() end) end
    SoundESPBeep = Instance.new("Sound")
    SoundESPBeep.SoundId = "rbxassetid://4790566870"
    SoundESPBeep.Volume = 1
    SoundESPBeep.Parent = SoundService
    ActiveConnections["SoundESP"] = RunService.Heartbeat:Connect(function()
        if not SoundESPEnabled then return end
        local char = LocalPlayer.Character
        if not char or not char:FindFirstChild("HumanoidRootPart") then return end
        local myPos = char.HumanoidRootPart.Position
        local nearest = math.huge
        for _, p in pairs(Players:GetPlayers()) do
            if p ~= LocalPlayer and p.Character and p.Character:FindFirstChild("HumanoidRootPart") and p.Character:FindFirstChild("Humanoid") and p.Character.Humanoid.Health > 0 then
                local d = (p.Character.HumanoidRootPart.Position - myPos).Magnitude
                if d < nearest then nearest = d end
            end
        end
        if nearest <= SoundESPRadius then
            local now = tick()
            local cd = math.clamp(nearest / 85, 0.15, 1.2)
            if now - LastBeepTime >= cd then
                LastBeepTime = now
                pcall(function()
                    SoundESPBeep.Volume = math.clamp(1 - (nearest / SoundESPRadius) + 0.3, 0.3, 1)
                    SoundESPBeep:Play()
                end)
            end
        end
    end)
end

local function DisableSoundESP()
    DisconnectKey("SoundESP")
    if SoundESPBeep then pcall(function() SoundESPBeep:Destroy() end); SoundESPBeep = nil end
end

local function PlayMusic()
    if MusicSound then pcall(function() MusicSound:Stop(); MusicSound:Destroy() end); MusicSound = nil end
    local track = MusicPlaylist[MusicCurrentIndex]
    if not track then return end
    MusicSound = Instance.new("Sound")
    MusicSound.SoundId = "rbxassetid://"..track.ID
    MusicSound.Volume = MusicVolume
    MusicSound.Parent = SoundService
    pcall(function() MusicSound:Play() end)
end

local function StopMusic()
    if MusicSound then pcall(function() MusicSound:Stop(); MusicSound:Destroy() end); MusicSound = nil end
end

local function NextMusic()
    if MusicShuffle then MusicCurrentIndex = math.random(1, #MusicPlaylist)
    else
        MusicCurrentIndex = MusicCurrentIndex + 1
        if MusicCurrentIndex > #MusicPlaylist then MusicCurrentIndex = 1 end
    end
    if MusicPlayerEnabled then PlayMusic() end
end

local function PrevMusic()
    MusicCurrentIndex = MusicCurrentIndex - 1
    if MusicCurrentIndex < 1 then MusicCurrentIndex = #MusicPlaylist end
    if MusicPlayerEnabled then PlayMusic() end
end

local function SendChatMessage(msg)
    pcall(function()
        local ce = ReplicatedStorage:FindFirstChild("DefaultChatSystemChatEvents")
        if ce then
            local sr = ce:FindFirstChild("SayMessageRequest")
            if sr then sr:FireServer(msg, "All") end
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

local function DisableChatSpam() DisconnectKey("ChatSpam") end

--========== DRONE / KILL / INFO ==========
local function EnableDroneMode()
    DisconnectKey("DroneMode")
    ActiveConnections["DroneMode"] = RunService.RenderStepped:Connect(function()
        if not DroneModeEnabled then return end
        if not LocalPlayer.Character then return end
        local root = LocalPlayer.Character:FindFirstChild("HumanoidRootPart")
        if not root then return end
        pcall(function()
            Camera.CameraSubject = nil
            Camera.CameraType = Enum.CameraType.Scriptable
            Camera.CFrame = CFrame.new(root.Position + Vector3.new(0,30,0), root.Position)
        end)
    end)
end

local function DisableDroneMode()
    DisconnectKey("DroneMode")
    pcall(function()
        Camera.CameraSubject = LocalPlayer.Character and LocalPlayer.Character:FindFirstChild("Humanoid")
        Camera.CameraType = Enum.CameraType.Custom
    end)
end

local function EnableKillNotif()
    DisconnectKey("KillNotif")
    for _, p in pairs(Players:GetPlayers()) do
        if p ~= LocalPlayer and p.Character then
            local hum = p.Character:FindFirstChild("Humanoid")
            if hum then LastPlayerHealth[p] = hum.Health end
        end
    end
    ActiveConnections["KillNotif"] = RunService.Heartbeat:Connect(function()
        if not KillNotifEnabled then return end
        for _, p in pairs(Players:GetPlayers()) do
            if p ~= LocalPlayer and p.Character then
                local hum = p.Character:FindFirstChild("Humanoid")
                if hum then
                    local last = LastPlayerHealth[p] or 100
                    if hum.Health <= 0 and last > 0 then
                        Notify("💀 KILL", p.Name.." mati!", 3)
                    end
                    LastPlayerHealth[p] = hum.Health
                end
            end
        end
        if LocalPlayer.Character then
            local myHum = LocalPlayer.Character:FindFirstChild("Humanoid")
            if myHum and myHum.Health > 0 and myHum.Health <= myHum.MaxHealth * 0.3 then
                if not _G._ZET_LowHPWarned or tick() - _G._ZET_LowHPWarned > 10 then
                    _G._ZET_LowHPWarned = tick()
                    Notify("⚠️ LOW HP", "HP: "..math.floor(myHum.Health).."/"..myHum.MaxHealth, 3)
                end
            end
        end
    end)
end
local function DisableKillNotif() DisconnectKey("KillNotif") end

local function CreateInfoPanel()
    if InfoPanelFrame then pcall(function() InfoPanelFrame:Destroy() end) end
    InfoPanelFrame = Instance.new("Frame")
    InfoPanelFrame.Name = "ZetInfoPanel"
    InfoPanelFrame.Size = UDim2.new(0, 180, 0, 65)
    InfoPanelFrame.Position = UDim2.new(1, -190, 1, -90)
    InfoPanelFrame.BackgroundColor3 = THEME.PanelBG
    InfoPanelFrame.BackgroundTransparency = 0.2
    InfoPanelFrame.BorderColor3 = THEME.Accent
    InfoPanelFrame.BorderSizePixel = 2
    InfoPanelFrame.ZIndex = 200
    InfoPanelFrame.Parent = ScreenGui
    Instance.new("UICorner", InfoPanelFrame).CornerRadius = UDim.new(0, 8)
    local lbl = Instance.new("TextLabel")
    lbl.Size = UDim2.new(1, -10, 1, -10)
    lbl.Position = UDim2.new(0, 5, 0, 5)
    lbl.BackgroundTransparency = 1
    lbl.Text = "> Loading..."
    lbl.TextColor3 = THEME.Text
    lbl.Font = Enum.Font.Code
    lbl.TextSize = 10
    lbl.TextXAlignment = Enum.TextXAlignment.Left
    lbl.TextYAlignment = Enum.TextYAlignment.Top
    lbl.ZIndex = 201
    lbl.Parent = InfoPanelFrame
    task.spawn(function()
        while task.wait(1) do
            if not InfoPanelFrame or not InfoPanelFrame.Parent then break end
            pcall(function()
                local ping = math.floor(LocalPlayer:GetNetworkPing() * 1000)
                local pc = #Players:GetPlayers()
                lbl.Text = "> Ping: "..ping.."ms\n> Players: "..pc.."\n> "..os.date("%H:%M:%S")
            end)
        end
    end)
end

--========== ESP ==========
local function HSVToRGB(h,s,v)
    local r,g,b
    local i = math.floor(h*6)
    local f = h*6-i
    local p = v*(1-s)
    local q = v*(1-f*s)
    local t = v*(1-(1-f)*s)
    i = i%6
    if i==0 then r,g,b=v,t,p
    elseif i==1 then r,g,b=q,v,p
    elseif i==2 then r,g,b=p,v,t
    elseif i==3 then r,g,b=p,q,v
    elseif i==4 then r,g,b=t,p,v
    else r,g,b=v,p,q end
    return Color3.new(r,g,b)
end

local function EnableRainbowESP()
    DisconnectKey("Rainbow")
    ActiveConnections["Rainbow"] = RunService.RenderStepped:Connect(function(dt)
        if not RainbowESPEnabled then return end
        RainbowHue = (RainbowHue + dt * 0.3) % 1
        local c = HSVToRGB(RainbowHue, 1, 1)
        for _, d in pairs(ESPObjects) do
            if d.Box then d.Box.Color = c end
            if d.Name then d.Name.Color = c end
            if d.Distance then d.Distance.Color = c end
            if d.Tracer then d.Tracer.Color = c end
        end
    end)
end

local function DisableRainbowESP() DisconnectKey("Rainbow") end

local function CreateESP(player)
    if ESPObjects[player] then return end
    if not Drawing then return end
    local d = {}
    d.Box = Drawing.new("Square"); d.Box.Visible=false; d.Box.Color=THEME.Accent; d.Box.Thickness=2; d.Box.Filled=false; d.Box.Transparency=1
    d.Name = Drawing.new("Text"); d.Name.Visible=false; d.Name.Color=THEME.Accent; d.Name.Size=12; d.Name.Center=true; d.Name.Outline=true; d.Name.OutlineColor=Color3.new(0,0,0)
    d.Distance = Drawing.new("Text"); d.Distance.Visible=false; d.Distance.Color=THEME.Accent; d.Distance.Size=10; d.Distance.Center=true; d.Distance.Outline=true; d.Distance.OutlineColor=Color3.new(0,0,0)
    d.HealthBg = Drawing.new("Line"); d.HealthBg.Visible=false; d.HealthBg.Color=Color3.fromRGB(0,50,100); d.HealthBg.Thickness=3
    d.HealthBar = Drawing.new("Line"); d.HealthBar.Visible=false; d.HealthBar.Color=THEME.Accent; d.HealthBar.Thickness=3
    d.Tracer = Drawing.new("Line"); d.Tracer.Visible=false; d.Tracer.Color=TracerColor; d.Tracer.Thickness=2; d.Tracer.Transparency=0.5
    ESPObjects[player] = d
end

local function RemoveESP(player)
    if ESPObjects[player] then
        for _, v in pairs(ESPObjects[player]) do pcall(function() v:Remove() end) end
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
    d.Box = Drawing.new("Square"); d.Box.Visible=false; d.Box.Color=THEME.YellowDot; d.Box.Thickness=2; d.Box.Filled=false; d.Box.Transparency=1
    d.Name = Drawing.new("Text"); d.Name.Visible=false; d.Name.Color=THEME.YellowDot; d.Name.Size=11; d.Name.Center=true; d.Name.Outline=true; d.Name.OutlineColor=Color3.new(0,0,0)
    d.Distance = Drawing.new("Text"); d.Distance.Visible=false; d.Distance.Color=THEME.YellowDot; d.Distance.Size=9; d.Distance.Center=true; d.Distance.Outline=true; d.Distance.OutlineColor=Color3.new(0,0,0)
    NPCESPObjects[model] = d
end

local function RemoveNPCEsp(model)
    if NPCESPObjects[model] then
        for _, v in pairs(NPCESPObjects[model]) do pcall(function() v:Remove() end) end
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
                if d then
                    local sp, on = Camera:WorldToViewportPoint(root.Position)
                    if on then
                        local dist = (root.Position - Camera.CFrame.Position).Magnitude
                        local bs = Vector2.new(2000/dist, 3500/dist)
                        local bx, by = sp.X-bs.X/2, sp.Y-bs.Y/2
                        d.Box.Visible = true; d.Box.Position = Vector2.new(bx,by); d.Box.Size = bs
                        d.Name.Visible = true; d.Name.Text = player.Name; d.Name.Position = Vector2.new(sp.X, by-15)
                        d.Distance.Visible = true; d.Distance.Text = math.floor(dist).."m"; d.Distance.Position = Vector2.new(sp.X, by+bs.Y+5)
                        local hp = hum.Health / hum.MaxHealth
                        d.HealthBg.Visible = true; d.HealthBg.From = Vector2.new(bx, by+bs.Y+20); d.HealthBg.To = Vector2.new(bx+bs.X, by+bs.Y+20)
                        d.HealthBar.Visible = true; d.HealthBar.From = Vector2.new(bx, by+bs.Y+20); d.HealthBar.To = Vector2.new(bx+bs.X*hp, by+bs.Y+20)
                        d.Tracer.Visible = true
                        if not RainbowESPEnabled then d.Tracer.Color = TracerColor end
                        d.Tracer.From = Vector2.new(Camera.ViewportSize.X/2, Camera.ViewportSize.Y)
                        d.Tracer.To = Vector2.new(sp.X, sp.Y)
                        if not ChamsObjects[player] then CreateChams(player) end
                    else
                        for _, v in pairs(d) do pcall(function() v.Visible = false end) end
                    end
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
            if d then
                local sp, on = Camera:WorldToViewportPoint(root.Position)
                if on then
                    local dist = (root.Position - Camera.CFrame.Position).Magnitude
                    local bs = Vector2.new(2000/dist, 3500/dist)
                    local bx, by = sp.X-bs.X/2, sp.Y-bs.Y/2
                    d.Box.Visible = true; d.Box.Position = Vector2.new(bx,by); d.Box.Size = bs
                    d.Name.Visible = true; d.Name.Text = "[NPC] "..model.Name; d.Name.Position = Vector2.new(sp.X, by-15)
                    d.Distance.Visible = true; d.Distance.Text = math.floor(dist).."m"; d.Distance.Position = Vector2.new(sp.X, by+bs.Y+5)
                else
                    for _, v in pairs(d) do pcall(function() v.Visible = false end) end
                end
            end
        else RemoveNPCEsp(model) end
    end
    for model, _ in pairs(NPCESPObjects) do
        if not seen[model] then RemoveNPCEsp(model) end
    end
end

local function EnableESPLoop()
    DisconnectKey("ESPLoop")
    ActiveConnections["ESPLoop"] = RunService.RenderStepped:Connect(function()
        UpdateESP()
        UpdateNPCEsp()
    end)
end

local function DisableESPLoop()
    DisconnectKey("ESPLoop")
    for _, d in pairs(ESPObjects) do
        for _, v in pairs(d) do pcall(function() v.Visible = false end) end
    end
    for model, _ in pairs(NPCESPObjects) do RemoveNPCEsp(model) end
    for p, _ in pairs(ChamsObjects) do RemoveChams(p) end
end

--========== AIMBOT ==========
local function HasWallBetween(cp, tp, tc)
    if not AimbotWallCheck then return false end
    local dir = tp - cp
    local dist = dir.Magnitude
    if dist < 1 then return false end
    local rp = RaycastParams.new()
    rp.FilterType = Enum.RaycastFilterType.Blacklist
    rp.FilterDescendantsInstances = {LocalPlayer.Character, tc}
    return workspace:Raycast(cp, dir.Unit*dist, rp) ~= nil
end

local function FindTarget()
    local best, bestScore, bType = nil, math.huge, nil
    local sc = Vector2.new(Camera.ViewportSize.X/2, Camera.ViewportSize.Y/2)
    local cp = Camera.CFrame.Position
    for _, player in pairs(Players:GetPlayers()) do
        if player ~= LocalPlayer and player.Character then
            local hum = player.Character:FindFirstChild("Humanoid")
            local root = player.Character:FindFirstChild("HumanoidRootPart")
            if hum and root and hum.Health > 0 then
                if AimbotTeamCheck and LocalPlayer.Team and player.Team and LocalPlayer.Team == player.Team then
                    -- skip
                else
                    local part = player.Character:FindFirstChild(AimbotTargetPart) or root
                    if part and not HasWallBetween(cp, part.Position, player.Character) then
                        local sp, on = Camera:WorldToViewportPoint(part.Position)
                        if on then
                            local sd = (Vector2.new(sp.X,sp.Y)-sc).Magnitude
                            local hp = hum.Health / hum.MaxHealth
                            local score = sd
                            if TargetPriority == "Lowest" then score = hp
                            elseif TargetPriority == "Farthest" then score = -sd end
                            if sd <= AimbotFOV and score < bestScore then
                                best = player; bestScore = score; bType = "player"
                            end
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
                if part and not HasWallBetween(cp, part.Position, model) then
                    local sp, on = Camera:WorldToViewportPoint(part.Position)
                    if on then
                        local sd = (Vector2.new(sp.X,sp.Y)-sc).Magnitude
                        if sd <= AimbotFOV and sd < bestScore then
                            best = model; bestScore = sd; bType = "npc"
                        end
                    end
                end
            end
        end
    end
    return best, bType
end

local function IsTargetValid(t, tt)
    if not t or not t.Parent then return false end
    if tt == "player" then
        local c = t.Character
        if not c then return false end
        local h = c:FindFirstChild("Humanoid")
        return h and h.Health > 0
    elseif tt == "npc" then
        local h = t:FindFirstChild("Humanoid")
        return h and h.Health > 0
    end
    return false
end

local function GetTargetPart(t, tt)
    if tt == "player" then
        if not t.Character then return nil end
        return t.Character:FindFirstChild(AimbotTargetPart) or t.Character:FindFirstChild("HumanoidRootPart")
    elseif tt == "npc" then
        return t:FindFirstChild(AimbotTargetPart) or t:FindFirstChild("HumanoidRootPart")
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
        AimbotStickyTarget, AimbotStickyType = FindTarget()
    end
    if not AimbotStickyTarget then return end
    if not IsTargetValid(AimbotStickyTarget, AimbotStickyType) then
        AimbotStickyTarget = nil; AimbotStickyType = nil
        return
    end
    local tp = GetTargetPart(AimbotStickyTarget, AimbotStickyType)
    if not tp then return end
    local cp = Camera.CFrame.Position
    local dir = (tp.Position - cp).Unit
    if SilentAimEnabled then
        pcall(function()
            if LocalPlayer.Character then
                local tool = LocalPlayer.Character:FindFirstChildOfClass("Tool")
                if tool then tool:Activate() end
            end
        end)
    else
        local newCF = CFrame.new(cp, cp + dir)
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
    local sc = Vector2.new(Camera.ViewportSize.X/2, Camera.ViewportSize.Y/2)
    for _, player in pairs(Players:GetPlayers()) do
        if player ~= LocalPlayer and player.Character then
            local hum = player.Character:FindFirstChild("Humanoid")
            local root = player.Character:FindFirstChild("HumanoidRootPart")
            if hum and root and hum.Health > 0 then
                local sp, on = Camera:WorldToViewportPoint(root.Position)
                if on then
                    local d = (Vector2.new(sp.X,sp.Y)-sc).Magnitude
                    if d < 50 then
                        pcall(function() tool:Activate() end)
                        break
                    end
                end
            end
        end
    end
end

local function EnableAimbotLoop()
    DisconnectKey("Aimbot")
    ActiveConnections["Aimbot"] = RunService.RenderStepped:Connect(function()
        if AimbotEnabled then RunAimbot() end
        if LookAtEnabled then
            local t, tt = FindTarget()
            if t then
                local tp = GetTargetPart(t, tt)
                if tp then
                    local cp = Camera.CFrame.Position
                    pcall(function() Camera.CFrame = CFrame.new(cp, cp + (tp.Position - cp).Unit) end)
                end
            end
        end
        if AutoShootEnabled then
            local now = tick()
            if now - AutoShootLast >= AutoShootDelay/1000 then
                AutoShootLast = now
                TryAutoShoot()
            end
        end
    end)
end

--========== SERVER HOP / TELEPORT ==========
local function FetchServerList(pid)
    local servers, cursor = {}, ""
    for i = 1, 2 do
        local url = "https://games.roblox.com/v1/games/"..pid.."/servers/Public?sortOrder=Asc&limit=100"
        if cursor ~= "" then url = url.."&cursor="..cursor end
        local ok, res = pcall(function() return HttpService:JSONDecode(game:HttpGet(url)) end)
        if ok and res and res.data then
            for _, s in ipairs(res.data) do
                if s.playing and s.maxPlayers and s.playing < s.maxPlayers and s.id ~= game.JobId then
                    table.insert(servers, s)
                end
            end
            cursor = res.nextPageCursor or ""
            if cursor == "" then break end
        else break end
    end
    return #servers > 0, servers
end

local function DoServerHop()
    if ServerHopRunning then return end
    ServerHopRunning = true
    Notify("Server Hop", "MENCARI...", 3)
    task.spawn(function()
        local ok, servers = FetchServerList(game.PlaceId)
        if not ok then Notify("Server Hop", "GAGAL", 3); ServerHopRunning = false; return end
        local t = servers[math.random(1, #servers)]
        pcall(function() TeleportService:TeleportToPlaceInstance(game.PlaceId, t.id, LocalPlayer) end)
    end)
end

local function DoBestServerHop()
    if ServerHopRunning then return end
    ServerHopRunning = true
    task.spawn(function()
        local ok, servers = FetchServerList(game.PlaceId)
        if not ok then Notify("Server Hop", "TIDAK ADA", 3); ServerHopRunning = false; return end
        table.sort(servers, function(a,b) return (a.playing or 0) < (b.playing or 0) end)
        pcall(function() TeleportService:TeleportToPlaceInstance(game.PlaceId, servers[1].id, LocalPlayer) end)
    end)
end

local function DoRejoin()
    pcall(function() TeleportService:TeleportToPlaceInstance(game.PlaceId, game.JobId, LocalPlayer) end)
end

local function TeleportToPlayer(tp)
    if not tp or not tp.Character then return end
    local tr = tp.Character:FindFirstChild("HumanoidRootPart")
    local lr = LocalPlayer.Character and LocalPlayer.Character:FindFirstChild("HumanoidRootPart")
    if not tr or not lr then return end
    pcall(function()
        lr.CFrame = CFrame.new(tr.Position + Vector3.new(0,3,0))
        Notify("Teleport", "TO: "..tp.Name, 2)
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
            btn.Text = "> "..player.Name
            btn.TextColor3 = THEME.Text
            btn.Font = Enum.Font.Code
            btn.TextSize = 11
            btn.TextXAlignment = Enum.TextXAlignment.Left
            btn.ZIndex = 15
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
        empty.ZIndex = 15
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
            r.CFrame = CFrame.new(hit.Position + Vector3.new(0,3,0))
            Notify("Teleport", "TO MOUSE", 2)
        end)
    end
end

local function SaveLocation()
    if LocalPlayer.Character and LocalPlayer.Character:FindFirstChild("HumanoidRootPart") then
        SavedLocation = LocalPlayer.Character.HumanoidRootPart.CFrame
        Notify("Save", "SAVED", 2)
    end
end

local function LoadLocation()
    if SavedLocation and LocalPlayer.Character and LocalPlayer.Character:FindFirstChild("HumanoidRootPart") then
        pcall(function()
            LocalPlayer.Character.HumanoidRootPart.CFrame = SavedLocation
            Notify("Save", "TELEPORTED", 2)
        end)
    else Notify("Save", "NO SAVED", 2) end
end

--========== WAYPOINT ==========
local function AddWaypoint(name)
    if not LocalPlayer.Character or not LocalPlayer.Character:FindFirstChild("HumanoidRootPart") then return end
    table.insert(Waypoints, {Name=name, CFrame=LocalPlayer.Character.HumanoidRootPart.CFrame})
    Notify("Waypoint", "Added: "..name, 2)
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

print("[ZET] Features OK")

--==============================================================
-- CREATE UI (FULL FIX - GUARANTEED)
--==============================================================

--========== LOGIN FRAME ==========
local LoginFrame = Instance.new("Frame")
LoginFrame.Name = "ZetLogin"
LoginFrame.Size = UDim2.new(0, 320, 0, 400)
LoginFrame.Position = UDim2.new(0.5, -160, 0.5, -200)
LoginFrame.BackgroundColor3 = THEME.MainBG
LoginFrame.BorderColor3 = THEME.Accent
LoginFrame.BorderSizePixel = 2
LoginFrame.Visible = true
LoginFrame.ZIndex = 100
LoginFrame.Parent = ScreenGui
Instance.new("UICorner", LoginFrame).CornerRadius = UDim.new(0, 10)

local LoginTopBar = Instance.new("Frame")
LoginTopBar.Size = UDim2.new(1, 0, 0, 35)
LoginTopBar.BackgroundColor3 = THEME.SectionBG
LoginTopBar.BorderSizePixel = 0
LoginTopBar.ZIndex = 101
LoginTopBar.Parent = LoginFrame
Instance.new("UICorner", LoginTopBar).CornerRadius = UDim.new(0, 10)

local LoginTopTxt = Instance.new("TextLabel")
LoginTopTxt.Size = UDim2.new(1, -10, 1, 0)
LoginTopTxt.Position = UDim2.new(0, 10, 0, 0)
LoginTopTxt.BackgroundTransparency = 1
LoginTopTxt.Text = "● ZETGAMES-AIMLOCK V4.4"
LoginTopTxt.TextColor3 = THEME.Text
LoginTopTxt.Font = Enum.Font.Code
LoginTopTxt.TextSize = 11
LoginTopTxt.TextXAlignment = Enum.TextXAlignment.Left
LoginTopTxt.ZIndex = 102
LoginTopTxt.Parent = LoginTopBar

local LoginTitle = Instance.new("TextLabel")
LoginTitle.Size = UDim2.new(1, -30, 0, 30)
LoginTitle.Position = UDim2.new(0, 15, 0, 50)
LoginTitle.BackgroundTransparency = 1
LoginTitle.Text = "> ACCESS VERIFICATION"
LoginTitle.TextColor3 = THEME.Text
LoginTitle.Font = Enum.Font.Code
LoginTitle.TextSize = 16
LoginTitle.ZIndex = 102
LoginTitle.Parent = LoginFrame

local LoginTag = Instance.new("TextLabel")
LoginTag.Size = UDim2.new(1, -30, 0, 18)
LoginTag.Position = UDim2.new(0, 15, 0, 82)
LoginTag.BackgroundTransparency = 1
LoginTag.Text = "[ RESMI + NIGHT LOCK ACTIVE ]"
LoginTag.TextColor3 = Color3.fromRGB(0, 255, 200)
LoginTag.Font = Enum.Font.Code
LoginTag.TextSize = 9
LoginTag.TextXAlignment = Enum.TextXAlignment.Left
LoginTag.ZIndex = 102
LoginTag.Parent = LoginFrame

local KeyLabel = Instance.new("TextLabel")
KeyLabel.Size = UDim2.new(1, -30, 0, 18)
KeyLabel.Position = UDim2.new(0, 15, 0, 108)
KeyLabel.BackgroundTransparency = 1
KeyLabel.Text = "> KEY_INPUT:"
KeyLabel.TextColor3 = THEME.Text
KeyLabel.Font = Enum.Font.Code
KeyLabel.TextSize = 12
KeyLabel.TextXAlignment = Enum.TextXAlignment.Left
KeyLabel.ZIndex = 102
KeyLabel.Parent = LoginFrame

local KeyBox = Instance.new("TextBox")
KeyBox.Size = UDim2.new(1, -30, 0, 40)
KeyBox.Position = UDim2.new(0, 15, 0, 130)
KeyBox.BackgroundColor3 = THEME.PanelBG
KeyBox.BorderColor3 = THEME.Accent
KeyBox.BorderSizePixel = 2
KeyBox.PlaceholderText = "> Type key..."
KeyBox.PlaceholderColor3 = Color3.fromRGB(50, 80, 100)
KeyBox.Text = ""
KeyBox.TextColor3 = THEME.Text
KeyBox.Font = Enum.Font.Code
KeyBox.TextSize = 13
KeyBox.ClearTextOnFocus = false
KeyBox.ZIndex = 102
KeyBox.Parent = LoginFrame
Instance.new("UICorner", KeyBox).CornerRadius = UDim.new(0, 5)

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
GetKeyBtn.Text = "> GET KEY (COPY)"
GetKeyBtn.TextColor3 = THEME.TextLight
GetKeyBtn.Font = Enum.Font.Code
GetKeyBtn.TextSize = 14
GetKeyBtn.ZIndex = 102
GetKeyBtn.Parent = LoginFrame
Instance.new("UICorner", GetKeyBtn).CornerRadius = UDim.new(0, 5)

local LoginStatus = Instance.new("TextLabel")
LoginStatus.Size = UDim2.new(1, -30, 0, 25)
LoginStatus.Position = UDim2.new(0, 15, 0, 295)
LoginStatus.BackgroundTransparency = 1
LoginStatus.Text = "> SYSTEM READY..."
LoginStatus.TextColor3 = THEME.Text
LoginStatus.Font = Enum.Font.Code
LoginStatus.TextSize = 10
LoginStatus.TextXAlignment = Enum.TextXAlignment.Left
LoginStatus.ZIndex = 102
LoginStatus.Parent = LoginFrame

local LoginInstr = Instance.new("TextLabel")
LoginInstr.Size = UDim2.new(1, -30, 0, 60)
LoginInstr.Position = UDim2.new(0, 15, 0, 325)
LoginInstr.BackgroundTransparency = 1
LoginInstr.Text = "> STEPS:\n> 1. Click GET KEY\n> 2. Generate key\n> 3. Enter key\n> 4. AUTHENTICATE"
LoginInstr.TextColor3 = THEME.TextLight
LoginInstr.Font = Enum.Font.Code
LoginInstr.TextSize = 9
LoginInstr.TextXAlignment = Enum.TextXAlignment.Left
LoginInstr.ZIndex = 102
LoginInstr.Parent = LoginFrame

print("[ZET] LoginFrame created")

--========== MAIN HUB ==========
local MainHub = Instance.new("Frame")
MainHub.Name = "ZetMain"
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
ScrollFrame.CanvasSize = UDim2.new(0, 0, 0, 3500)
ScrollFrame.ZIndex = 101
ScrollFrame.Parent = MainHub

local Content = Instance.new("Frame")
Content.Name = "Content"
Content.Size = UDim2.new(1, 0, 0, 3500)
Content.BackgroundTransparency = 1
Content.ZIndex = 101
Content.Parent = ScrollFrame

print("[ZET] ScrollFrame created")

--========== HELPER FUNCTIONS ==========
local currentY = 10

local function AddSection(title)
    local f = Instance.new("Frame")
    f.Size = UDim2.new(1, -20, 0, 26)
    f.Position = UDim2.new(0, 10, 0, currentY)
    f.BackgroundColor3 = THEME.SectionBG
    f.BorderColor3 = THEME.Accent
    f.BorderSizePixel = 1
    f.ZIndex = 102
    f.Parent = Content
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
    currentY = currentY + 30
end

local function AddToggle(text, callback)
    local btn = Instance.new("TextButton")
    btn.Size = UDim2.new(1, -20, 0, 34)
    btn.Position = UDim2.new(0, 10, 0, currentY)
    btn.BackgroundColor3 = THEME.ButtonBG
    btn.BorderColor3 = THEME.Accent
    btn.BorderSizePixel = 1
    btn.Text = text
    btn.TextColor3 = THEME.Text
    btn.Font = Enum.Font.Code
    btn.TextSize = 11
    btn.ZIndex = 102
    btn.Parent = Content
    Instance.new("UICorner", btn).CornerRadius = UDim.new(0, 4)
    btn.MouseButton1Click:Connect(function() callback(btn) end)
    currentY = currentY + 38
    return btn
end

local function AddLockedToggle(text)
    local btn = Instance.new("TextButton")
    btn.Size = UDim2.new(1, -20, 0, 34)
    btn.Position = UDim2.new(0, 10, 0, currentY)
    btn.BackgroundColor3 = THEME.LockedBG
    btn.BorderColor3 = THEME.Locked
    btn.BorderSizePixel = 1
    btn.Text = text
    btn.TextColor3 = THEME.Locked
    btn.Font = Enum.Font.Code
    btn.TextSize = 11
    btn.ZIndex = 102
    btn.Parent = Content
    Instance.new("UICorner", btn).CornerRadius = UDim.new(0, 4)
    btn.MouseButton1Click:Connect(function() Notify("🔒 Locked", "Tidak bisa dimatiin", 2) end)
    currentY = currentY + 38
    return btn
end

local function AddInput(placeholder, defaultText)
    local tb = Instance.new("TextBox")
    tb.Size = UDim2.new(1, -20, 0, 28)
    tb.Position = UDim2.new(0, 10, 0, currentY)
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
    tb.Parent = Content
    Instance.new("UICorner", tb).CornerRadius = UDim.new(0, 4)
    currentY = currentY + 32
    return tb
end

local function AddButton(text, callback)
    local b = Instance.new("TextButton")
    b.Size = UDim2.new(1, -20, 0, 32)
    b.Position = UDim2.new(0, 10, 0, currentY)
    b.BackgroundColor3 = THEME.ButtonBG
    b.BorderColor3 = THEME.Accent
    b.BorderSizePixel = 1
    b.Text = text
    b.TextColor3 = THEME.Text
    b.Font = Enum.Font.Code
    b.TextSize = 11
    b.ZIndex = 102
    b.Parent = Content
    Instance.new("UICorner", b).CornerRadius = UDim.new(0, 4)
    b.MouseButton1Click:Connect(function() callback(b) end)
    currentY = currentY + 36
    return b
end

local function AddHalfRow(text1, callback1, text2, callback2)
    local b1 = Instance.new("TextButton")
    b1.Size = UDim2.new(0.5, -15, 0, 32)
    b1.Position = UDim2.new(0, 10, 0, currentY)
    b1.BackgroundColor3 = THEME.ButtonBG
    b1.BorderColor3 = THEME.Accent
    b1.BorderSizePixel = 1
    b1.Text = text1
    b1.TextColor3 = THEME.Text
    b1.Font = Enum.Font.Code
    b1.TextSize = 10
    b1.ZIndex = 102
    b1.Parent = Content
    Instance.new("UICorner", b1).CornerRadius = UDim.new(0, 4)
    b1.MouseButton1Click:Connect(function() callback1(b1) end)

    local b2 = Instance.new("TextButton")
    b2.Size = UDim2.new(0.5, -15, 0, 32)
    b2.Position = UDim2.new(0.5, 5, 0, currentY)
    b2.BackgroundColor3 = THEME.ButtonBG
    b2.BorderColor3 = THEME.Accent
    b2.BorderSizePixel = 1
    b2.Text = text2
    b2.TextColor3 = THEME.Text
    b2.Font = Enum.Font.Code
    b2.TextSize = 10
    b2.ZIndex = 102
    b2.Parent = Content
    Instance.new("UICorner", b2).CornerRadius = UDim.new(0, 4)
    b2.MouseButton1Click:Connect(function() callback2(b2) end)

    currentY = currentY + 36
    return b1, b2
end

--==============================================================
-- BUILD MENU
--==============================================================

--===== SAFE MODE =====
AddSection("=== 🛡️ SAFE MODE (LOCKED) ===")
AddLockedToggle("> 🛡️ ANTI-KICK: ON (SAFE)")
AddLockedToggle("> 🔄 AUTO-RECONNECT: ON")
AddLockedToggle("> 🔒 NIGHT LOCK: ON (AUTO KICK)")

--===== THEME =====
AddSection("=== 🎨 THEME SWITCHER ===")
local themeLbl = Instance.new("TextLabel")
themeLbl.Size = UDim2.new(1, -20, 0, 18)
themeLbl.Position = UDim2.new(0, 10, 0, currentY)
themeLbl.BackgroundTransparency = 1
themeLbl.Text = "> THEME: BIRU"
themeLbl.TextColor3 = THEME.Text
themeLbl.Font = Enum.Font.Code
themeLbl.TextSize = 10
themeLbl.TextXAlignment = Enum.TextXAlignment.Left
themeLbl.ZIndex = 102
themeLbl.Parent = Content
currentY = currentY + 22

local themeFrame = Instance.new("Frame")
themeFrame.Size = UDim2.new(1, -20, 0, 28)
themeFrame.Position = UDim2.new(0, 10, 0, currentY)
themeFrame.BackgroundTransparency = 1
themeFrame.ZIndex = 102
themeFrame.Parent = Content

local function AddThemeBtn(text, tname, xpos)
    local b = Instance.new("TextButton")
    b.Size = UDim2.new(0.19, 0, 1, 0)
    b.Position = UDim2.new(xpos, 0, 0, 0)
    b.BackgroundColor3 = THEME.ButtonBG
    b.BorderColor3 = THEME.Accent
    b.BorderSizePixel = 1
    b.Text = text
    b.TextColor3 = THEME.Text
    b.Font = Enum.Font.Code
    b.TextSize = 9
    b.ZIndex = 103
    b.Parent = themeFrame
    Instance.new("UICorner", b).CornerRadius = UDim.new(0, 3)
    b.MouseButton1Click:Connect(function()
        local p = ThemePresets[tname]
        if p then
            for k, v in pairs(p) do THEME[k] = v end
            CurrentThemeName = tname
            themeLbl.Text = "> THEME: "..string.upper(tname)
            Notify("Theme", tname, 2)
        end
    end)
end
AddThemeBtn("BIRU", "Biru", 0)
AddThemeBtn("MERAH", "Merah", 0.205)
AddThemeBtn("HIJAU", "Hijau", 0.41)
AddThemeBtn("UNGU", "Ungu", 0.615)
AddThemeBtn("KUNING", "Kuning", 0.82)
currentY = currentY + 32

--===== USER INFO =====
AddSection("=== USER INFORMATION ===")
local UIF = Instance.new("Frame")
UIF.Size = UDim2.new(1, -20, 0, 80)
UIF.Position = UDim2.new(0, 10, 0, currentY)
UIF.BackgroundColor3 = THEME.PanelBG
UIF.BorderColor3 = THEME.Accent
UIF.BorderSizePixel = 1
UIF.ZIndex = 102
UIF.Parent = Content
Instance.new("UICorner", UIF).CornerRadius = UDim.new(0, 4)

local function InfoLbl(text, y, color)
    local l = Instance.new("TextLabel")
    l.Size = UDim2.new(1, -15, 0, 22)
    l.Position = UDim2.new(0, 10, 0, y)
    l.BackgroundTransparency = 1
    l.Text = text
    l.TextColor3 = color or THEME.Text
    l.Font = Enum.Font.Code
    l.TextSize = 11
    l.TextXAlignment = Enum.TextXAlignment.Left
    l.ZIndex = 103
    l.Parent = UIF
end
InfoLbl("> NAME: "..LocalPlayer.DisplayName, 5)
InfoLbl("> USER: "..LocalPlayer.Name, 28)
InfoLbl("> BUILD: V4.4 RESMI + NIGHT LOCK", 51, Color3.fromRGB(0, 255, 200))
currentY = currentY + 85

--===== MAIN FEATURES =====
AddSection("=== MAIN FEATURES ===")

AddToggle("> FPS BOOST: OFF", function(b)
    FPSBoostEnabled = not FPSBoostEnabled
    b.Text = FPSBoostEnabled and "> FPS BOOST: ON" or "> FPS BOOST: OFF"
    b.BackgroundColor3 = FPSBoostEnabled and THEME.ButtonActive or THEME.ButtonBG
    if FPSBoostEnabled then EnableFPSBoost() else DisableFPSBoost() end
end)

AddToggle("> FULLBRIGHT: OFF", function(b)
    FullbrightEnabled = not FullbrightEnabled
    b.Text = FullbrightEnabled and "> FULLBRIGHT: ON" or "> FULLBRIGHT: OFF"
    b.BackgroundColor3 = FullbrightEnabled and THEME.ButtonActive or THEME.ButtonBG
    if FullbrightEnabled then EnableFullbright() else DisableFullbright() end
end)

AddToggle("> SPEED HACK: OFF", function(b)
    SpeedHackEnabled = not SpeedHackEnabled
    b.Text = SpeedHackEnabled and "> SPEED HACK: ON" or "> SPEED HACK: OFF"
    b.BackgroundColor3 = SpeedHackEnabled and THEME.ButtonActive or THEME.ButtonBG
    if SpeedHackEnabled then EnableSpeedHack() else DisableSpeedHack() end
end)

local spdInput = AddInput("> Speed (16-500)", tostring(SpeedMultiplier))
spdInput.FocusLost:Connect(function(enter)
    if enter then
        local n = tonumber(spdInput.Text)
        if n then SpeedMultiplier = math.clamp(n, 16, MaxSpeed) end
        spdInput.Text = tostring(SpeedMultiplier)
    end
end)

AddToggle("> INFINITE JUMP: OFF", function(b)
    InfiniteJumpEnabled = not InfiniteJumpEnabled
    b.Text = InfiniteJumpEnabled and "> INF JUMP: ON" or "> INFINITE JUMP: OFF"
    b.BackgroundColor3 = InfiniteJumpEnabled and THEME.ButtonActive or THEME.ButtonBG
    if InfiniteJumpEnabled then EnableInfiniteJump() else DisableInfiniteJump() end
end)

AddToggle("> NOCLIP: OFF", function(b)
    NoclipEnabled = not NoclipEnabled
    b.Text = NoclipEnabled and "> NOCLIP: ON" or "> NOCLIP: OFF"
    b.BackgroundColor3 = NoclipEnabled and THEME.ButtonActive or THEME.ButtonBG
    if NoclipEnabled then EnableNoclip() else DisableNoclip() end
end)

AddToggle("> 👻 INVISIBLE: OFF", function(b)
    InvisibleEnabled = not InvisibleEnabled
    b.Text = InvisibleEnabled and "> 👻 INVISIBLE: ON" or "> 👻 INVISIBLE: OFF"
    b.BackgroundColor3 = InvisibleEnabled and THEME.ButtonActive or THEME.ButtonBG
    if InvisibleEnabled then EnableInvisible() else DisableInvisible() end
end)

AddToggle("> ⚡ DASH: OFF (SHIFT)", function(b)
    DashEnabled = not DashEnabled
    b.Text = DashEnabled and "> ⚡ DASH: ON" or "> ⚡ DASH: OFF (SHIFT)"
    b.BackgroundColor3 = DashEnabled and THEME.ButtonActive or THEME.ButtonBG
end)

--===== FLY NORMAL =====
AddSection("=== 🛫 FLY NORMAL ===")
AddToggle("> FLY NORMAL: OFF", function(b)
    FlyNormalEnabled = not FlyNormalEnabled
    b.Text = FlyNormalEnabled and "> FLY NORMAL: ON" or "> FLY NORMAL: OFF"
    b.BackgroundColor3 = FlyNormalEnabled and THEME.ButtonActive or THEME.ButtonBG
    if FlyNormalEnabled then EnableFlyNormal() else DisableFlyNormal() end
end)

AddHalfRow("> MODE: FREE", function(b)
    b.Text = "> MODE: "..(b.Text:find("FREE") and "HOVER" or "FREE")
end, "> KEY: WASD", function(b)
    Notify("Fly", "WASD + Space + Ctrl", 2)
end)

local flyInput = AddInput("> Fly Speed (10-500)", tostring(FlyNormalSpeed))
flyInput.FocusLost:Connect(function(enter)
    if enter then
        local n = tonumber(flyInput.Text)
        if n then FlyNormalSpeed = math.clamp(n, 10, 500) end
        flyInput.Text = tostring(FlyNormalSpeed)
    end
end)

--===== AIMBOT =====
AddSection("=== 🎯 AIMBOT + FOV ===")
local aimBtn = AddButton("> AIMBOT: OFF", function(b)
    AimbotEnabled = not AimbotEnabled
    if AimbotEnabled then
        b.Text = "> AIMBOT: ON"
        b.BackgroundColor3 = THEME.ButtonActive
        EnableAimbotLoop()
    else
        b.Text = "> AIMBOT: OFF"
        b.BackgroundColor3 = THEME.ButtonBG
        AimbotStickyTarget = nil
        DisconnectKey("Aimbot")
    end
end)

local tpLbl = Instance.new("TextLabel")
tpLbl.Size = UDim2.new(1, -20, 0, 18)
tpLbl.Position = UDim2.new(0, 10, 0, currentY)
tpLbl.BackgroundTransparency = 1
tpLbl.Text = "> TARGET PART: KEPALA"
tpLbl.TextColor3 = THEME.Text
tpLbl.Font = Enum.Font.Code
tpLbl.TextSize = 10
tpLbl.TextXAlignment = Enum.TextXAlignment.Left
tpLbl.ZIndex = 102
tpLbl.Parent = Content
currentY = currentY + 22

local tpFrame = Instance.new("Frame")
tpFrame.Size = UDim2.new(1, -20, 0, 28)
tpFrame.Position = UDim2.new(0, 10, 0, currentY)
tpFrame.BackgroundTransparency = 1
tpFrame.ZIndex = 102
tpFrame.Parent = Content

local function AddTPBtn(text, part, xpos)
    local b = Instance.new("TextButton")
    b.Size = UDim2.new(0.32, 0, 1, 0)
    b.Position = UDim2.new(xpos, 0, 0, 0)
    b.BackgroundColor3 = THEME.ButtonBG
    b.BorderColor3 = THEME.Accent
    b.BorderSizePixel = 1
    b.Text = text
    b.TextColor3 = THEME.Text
    b.Font = Enum.Font.Code
    b.TextSize = 10
    b.ZIndex = 103
    b.Parent = tpFrame
    Instance.new("UICorner", b).CornerRadius = UDim.new(0, 3)
    b.MouseButton1Click:Connect(function()
        AimbotTargetPart = part
        tpLbl.Text = "> TARGET PART: "..text
        Notify("Aimbot", "Target: "..text, 2)
    end)
end
AddTPBtn("KEPALA", "Head", 0)
AddTPBtn("BADAN", "UpperTorso", 0.345)
AddTPBtn("LEHER", "Neck", 0.69)
currentY = currentY + 32

AddToggle("> 🎯 SILENT AIM: OFF", function(b)
    SilentAimEnabled = not SilentAimEnabled
    b.Text = SilentAimEnabled and "> SILENT AIM: ON" or "> 🎯 SILENT AIM: OFF"
    b.BackgroundColor3 = SilentAimEnabled and THEME.ButtonActive or THEME.ButtonBG
end)

AddToggle("> FOV: OFF", function(b)
    FOVCircleEnabled = not FOVCircleEnabled
    b.Text = FOVCircleEnabled and "> FOV: ON" or "> FOV: OFF"
    b.BackgroundColor3 = FOVCircleEnabled and THEME.ButtonActive or THEME.ButtonBG
    if FOVCircleEnabled then EnableFOVLoop() else DisableFOVLoop() end
end)

local fovInput = AddInput("> FOV (50-5000)", tostring(FOVRadius))
fovInput.FocusLost:Connect(function(enter)
    if enter then
        local n = tonumber(fovInput.Text)
        if n then FOVRadius = math.clamp(n, 50, FOVMaxRadius); AimbotFOV = FOVRadius end
        fovInput.Text = tostring(FOVRadius)
    end
end)

AddToggle("> TEAM CHECK: OFF", function(b)
    AimbotTeamCheck = not AimbotTeamCheck
    b.Text = AimbotTeamCheck and "> TEAM: ON" or "> TEAM: OFF"
    b.BackgroundColor3 = AimbotTeamCheck and THEME.ButtonActive or THEME.ButtonBG
end)

AddToggle("> WALL CHECK: OFF", function(b)
    AimbotWallCheck = not AimbotWallCheck
    b.Text = AimbotWallCheck and "> WALL: ON" or "> WALL: OFF"
    b.BackgroundColor3 = AimbotWallCheck and THEME.ButtonActive or THEME.ButtonBG
end)

AddToggle("> KEYBIND AIMBOT (E): OFF", function(b)
    AimKeybindEnabled = not AimKeybindEnabled
    b.Text = AimKeybindEnabled and "> KEYBIND (E): ON" or "> KEYBIND (E): OFF"
    b.BackgroundColor3 = AimKeybindEnabled and THEME.ButtonActive or THEME.ButtonBG
end)

AddToggle("> 🔫 AUTO SHOOT: OFF", function(b)
    AutoShootEnabled = not AutoShootEnabled
    b.Text = AutoShootEnabled and "> AUTO SHOOT: ON" or "> 🔫 AUTO SHOOT: OFF"
    b.BackgroundColor3 = AutoShootEnabled and THEME.ButtonActive or THEME.ButtonBG
    if AutoShootEnabled then EnableAimbotLoop() end
end)

AddToggle("> 📡 OFF-SCREEN ARROW: OFF", function(b)
    OffScreenArrowEnabled = not OffScreenArrowEnabled
    b.Text = OffScreenArrowEnabled and "> OFF-ARROW: ON" or "> 📡 OFF-SCREEN ARROW: OFF"
    b.BackgroundColor3 = OffScreenArrowEnabled and THEME.ButtonActive or THEME.ButtonBG
    if OffScreenArrowEnabled then EnableOffScreenArrow() else DisableOffScreenArrow() end
end)

--===== ESP =====
AddSection("=== 👁️ FULL ESP ===")
AddToggle("> ESP MASTER: OFF", function(b)
    ESPEnabled = not ESPEnabled
    b.Text = ESPEnabled and "> ESP: ON" or "> ESP MASTER: OFF"
    b.BackgroundColor3 = ESPEnabled and THEME.ButtonActive or THEME.ButtonBG
    if ESPEnabled then EnableESPLoop() else DisableESPLoop() end
end)

AddToggle("> 🌈 RAINBOW ESP: OFF", function(b)
    RainbowESPEnabled = not RainbowESPEnabled
    b.Text = RainbowESPEnabled and "> 🌈 RAINBOW: ON" or "> 🌈 RAINBOW ESP: OFF"
    b.BackgroundColor3 = RainbowESPEnabled and THEME.ButtonActive or THEME.ButtonBG
    if RainbowESPEnabled then EnableRainbowESP() else DisableRainbowESP() end
end)

AddToggle("> NPC ESP: OFF", function(b)
    NPCEspEnabled = not NPCEspEnabled
    b.Text = NPCEspEnabled and "> NPC ESP: ON" or "> NPC ESP: OFF"
    b.BackgroundColor3 = NPCEspEnabled and THEME.ButtonActive or THEME.ButtonBG
    if not NPCEspEnabled then
        for model, _ in pairs(NPCESPObjects) do RemoveNPCEsp(model) end
    end
end)

AddToggle("> NPC DETECTION: OFF", function(b)
    NPCDetectionEnabled = not NPCDetectionEnabled
    b.Text = NPCDetectionEnabled and "> NPC DETECT: ON" or "> NPC DETECTION: OFF"
    b.BackgroundColor3 = NPCDetectionEnabled and THEME.ButtonActive or THEME.ButtonBG
end)

--===== HITBOX =====
AddSection("=== 🎯 HITBOX ===")
AddToggle("> HITBOX: OFF", function(b)
    HitboxEnabled = not HitboxEnabled
    b.Text = HitboxEnabled and "> HITBOX: ON" or "> HITBOX: OFF"
    b.BackgroundColor3 = HitboxEnabled and THEME.ButtonActive or THEME.ButtonBG
    if HitboxEnabled then EnableHitboxExpander() else DisableHitboxExpander() end
end)
local hbInput = AddInput("> Hitbox Size (1-100)", tostring(HitboxSize))
hbInput.FocusLost:Connect(function(enter)
    if enter then
        local n = tonumber(hbInput.Text)
        if n then HitboxSize = math.clamp(n, 1, 100) end
        hbInput.Text = tostring(HitboxSize)
    end
end)

--===== DRONE =====
AddSection("=== 🚁 DRONE MODE ===")
AddToggle("> DRONE CAMERA: OFF", function(b)
    DroneModeEnabled = not DroneModeEnabled
    b.Text = DroneModeEnabled and "> DRONE: ON" or "> DRONE CAMERA: OFF"
    b.BackgroundColor3 = DroneModeEnabled and THEME.ButtonActive or THEME.ButtonBG
    if DroneModeEnabled then EnableDroneMode() else DisableDroneMode() end
end)

--===== SURVIVAL =====
AddSection("=== SURVIVAL ===")
AddToggle("> AUTO RESPAWN: OFF", function(b)
    AutoRespawnEnabled = not AutoRespawnEnabled
    b.Text = AutoRespawnEnabled and "> RESPAWN: ON" or "> AUTO RESPAWN: OFF"
    b.BackgroundColor3 = AutoRespawnEnabled and THEME.ButtonActive or THEME.ButtonBG
    if AutoRespawnEnabled then EnableAutoRespawn() else DisableAutoRespawn() end
end)

AddToggle("> ANTI-FLING: OFF", function(b)
    AntiFlingEnabled = not AntiFlingEnabled
    b.Text = AntiFlingEnabled and "> ANTI-FLING: ON" or "> ANTI-FLING: OFF"
    b.BackgroundColor3 = AntiFlingEnabled and THEME.ButtonActive or THEME.ButtonBG
    if AntiFlingEnabled then EnableAntiFling() else DisableAntiFling() end
end)

AddToggle("> ANTI-AFK: OFF", function(b)
    AntiAFKEnabled = not AntiAFKEnabled
    b.Text = AntiAFKEnabled and "> ANTI-AFK: ON" or "> ANTI-AFK: OFF"
    b.BackgroundColor3 = AntiAFKEnabled and THEME.ButtonActive or THEME.ButtonBG
    if AntiAFKEnabled then EnableAntiAFK() else DisableAntiAFK() end
end)

--===== FLY-VOID =====
AddSection("=== 🕳️ FLY-VOID V2 ===")
AddToggle("> FLY-VOID: OFF", function(b)
    FlyVoidEnabled = not FlyVoidEnabled
    b.Text = FlyVoidEnabled and "> FLY-VOID: ON" or "> FLY-VOID: OFF"
    b.BackgroundColor3 = FlyVoidEnabled and THEME.ButtonActive or THEME.ButtonBG
    if FlyVoidEnabled then EnableFlyVoid() else DisableFlyVoid() end
end)

AddHalfRow("> HIDE: OFF", function(b)
    FlyVoidHideMode = not FlyVoidHideMode
    b.Text = FlyVoidHideMode and "> HIDE: ON" or "> HIDE: OFF"
    b.BackgroundColor3 = FlyVoidHideMode and THEME.ButtonActive or THEME.ButtonBG
end, "> KEY: V", function(b)
    Notify("Fly-Void", "Tekan V", 2)
end)

--===== SOUND =====
AddSection("=== SOUND ESP ===")
AddToggle("> SOUND ESP: OFF", function(b)
    SoundESPEnabled = not SoundESPEnabled
    b.Text = SoundESPEnabled and "> SOUND: ON" or "> SOUND ESP: OFF"
    b.BackgroundColor3 = SoundESPEnabled and THEME.ButtonActive or THEME.ButtonBG
    if SoundESPEnabled then EnableSoundESP() else DisableSoundESP() end
end)

--===== MUSIC =====
AddSection("=== 🎵 MUSIC PLAYLIST ===")
AddToggle("> MUSIC: OFF", function(b)
    MusicPlayerEnabled = not MusicPlayerEnabled
    b.Text = MusicPlayerEnabled and "> MUSIC: ON" or "> MUSIC: OFF"
    b.BackgroundColor3 = MusicPlayerEnabled and THEME.ButtonActive or THEME.ButtonBG
    if MusicPlayerEnabled then PlayMusic() else StopMusic() end
end)
AddHalfRow("> ⏮ PREV", function(b) PrevMusic() end, "> ⏭ NEXT", function(b) NextMusic() end)
AddHalfRow("> SHUFFLE: OFF", function(b)
    MusicShuffle = not MusicShuffle
    b.Text = MusicShuffle and "> SHUFFLE: ON" or "> SHUFFLE: OFF"
    b.BackgroundColor3 = MusicShuffle and THEME.ButtonActive or THEME.ButtonBG
end, "> PLAYLIST: 2", function(b)
    Notify("Music", "Kelingan Mantan + Teh Hijau", 2)
end)

--===== KILL NOTIF =====
AddSection("=== 🔔 KILL NOTIF ===")
AddToggle("> KILL NOTIF: OFF", function(b)
    KillNotifEnabled = not KillNotifEnabled
    b.Text = KillNotifEnabled and "> KILL: ON" or "> KILL NOTIF: OFF"
    b.BackgroundColor3 = KillNotifEnabled and THEME.ButtonActive or THEME.ButtonBG
    if KillNotifEnabled then EnableKillNotif() else DisableKillNotif() end
end)

--===== INFO PANEL =====
AddSection("=== 📊 INFO PANEL ===")
AddToggle("> INFO PANEL: OFF", function(b)
    InfoPanelEnabled = not InfoPanelEnabled
    b.Text = InfoPanelEnabled and "> INFO: ON" or "> INFO PANEL: OFF"
    b.BackgroundColor3 = InfoPanelEnabled and THEME.ButtonActive or THEME.ButtonBG
    if InfoPanelEnabled then
        CreateInfoPanel()
    else
        if InfoPanelFrame then pcall(function() InfoPanelFrame:Destroy() end); InfoPanelFrame = nil end
    end
end)

--===== WAYPOINT =====
AddSection("=== 🗺️ WAYPOINT ===")
local wpInput = AddInput("> Waypoint name", "Base")
AddButton("> ➕ ADD WAYPOINT", function(b)
    AddWaypoint(wpInput.Text)
end)

--===== CHAT SPAM =====
AddSection("=== CHAT SPAM ===")
AddToggle("> CHAT SPAM: OFF", function(b)
    ChatSpamEnabled = not ChatSpamEnabled
    b.Text = ChatSpamEnabled and "> SPAM: ON" or "> CHAT SPAM: OFF"
    b.BackgroundColor3 = ChatSpamEnabled and THEME.ButtonActive or THEME.ButtonBG
    if ChatSpamEnabled then EnableChatSpam() else DisableChatSpam() end
end)
local chatInput = AddInput("> Message", ChatSpamText)
chatInput.FocusLost:Connect(function(enter)
    if enter and chatInput.Text ~= "" then ChatSpamText = chatInput.Text end
end)

--===== SERVER HOP =====
AddSection("=== 🌐 SERVER HOP ===")
AddButton("> 🌐 SERVER HOP (RANDOM)", function(b) DoServerHop() end)
AddHalfRow("> 🎯 BEST SERVER", function(b) DoBestServerHop() end, "> 🔄 REJOIN", function(b) DoRejoin() end)

--===== TELEPORT KE ORANG =====
AddSection("=== 🆕 TELEPORT KE ORANG ===")
TeleportListFrame = Instance.new("ScrollingFrame")
TeleportListFrame.Size = UDim2.new(1, -20, 0, 130)
TeleportListFrame.Position = UDim2.new(0, 10, 0, currentY)
TeleportListFrame.BackgroundColor3 = THEME.PanelBG
TeleportListFrame.BorderColor3 = THEME.Accent
TeleportListFrame.BorderSizePixel = 1
TeleportListFrame.ScrollBarThickness = 5
TeleportListFrame.ScrollBarImageColor3 = THEME.Accent
TeleportListFrame.CanvasSize = UDim2.new(0, 0, 0, 0)
TeleportListFrame.ZIndex = 102
TeleportListFrame.Parent = Content
Instance.new("UICorner", TeleportListFrame).CornerRadius = UDim.new(0, 4)
TeleportListContainer = Instance.new("Frame")
TeleportListContainer.Size = UDim2.new(1, -10, 1, -10)
TeleportListContainer.Position = UDim2.new(0, 5, 0, 5)
TeleportListContainer.BackgroundTransparency = 1
TeleportListContainer.ZIndex = 103
TeleportListContainer.Parent = TeleportListFrame
currentY = currentY + 135

--===== TELEPORT =====
AddSection("=== TELEPORT ===")
AddButton("> 📍 TELEPORT TO MOUSE", function(b) TeleportToMouse() end)
AddHalfRow("> SAVE LOC", function(b) SaveLocation() end, "> LOAD LOC", function(b) LoadLocation() end)

--===== UPDATE CANVAS SIZE =====
ScrollFrame.CanvasSize = UDim2.new(0, 0, 0, currentY + 50)
Content.Size = UDim2.new(1, 0, 0, currentY + 50)
print("[ZET] Menu built. Final Y =", currentY)

--==============================================================
-- MENU BUTTON
--==============================================================
local MenuBtn = Instance.new("TextButton")
MenuBtn.Size = UDim2.new(0, 50, 0, 50)
MenuBtn.Position = UDim2.new(0, 10, 0.5, -25)
MenuBtn.BackgroundColor3 = THEME.ButtonActive
MenuBtn.BorderColor3 = THEME.Accent
MenuBtn.BorderSizePixel = 2
MenuBtn.Text = "≡"
MenuBtn.TextColor3 = THEME.Text
MenuBtn.Font = Enum.Font.Code
MenuBtn.TextSize = 24
MenuBtn.ZIndex = 200
MenuBtn.Visible = false
MenuBtn.Parent = ScreenGui
Instance.new("UICorner", MenuBtn).CornerRadius = UDim.new(0, 25)

local btnDrag, btnStart, btnStartPos, btnMoved = false, nil, nil, false
MenuBtn.InputBegan:Connect(function(input)
    if input.UserInputType == Enum.UserInputType.MouseButton1 or input.UserInputType == Enum.UserInputType.Touch then
        btnDrag = true; btnMoved = false; btnStart = input.Position; btnStartPos = MenuBtn.Position
    end
end)
MenuBtn.InputChanged:Connect(function(input)
    if (input.UserInputType == Enum.UserInputType.MouseMovement or input.UserInputType == Enum.UserInputType.Touch) and btnDrag then
        local d = input.Position - btnStart
        if math.abs(d.X) > 8 or math.abs(d.Y) > 8 then btnMoved = true end
        if btnMoved then
            MenuBtn.Position = UDim2.new(btnStartPos.X.Scale, btnStartPos.X.Offset + d.X, btnStartPos.Y.Scale, btnStartPos.Y.Offset + d.Y)
        end
    end
end)
UserInputService.InputEnded:Connect(function(input)
    if input.UserInputType == Enum.UserInputType.MouseButton1 or input.UserInputType == Enum.UserInputType.Touch then btnDrag = false end
end)
MenuBtn.MouseButton1Click:Connect(function()
    if btnMoved then return end
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

-- Make draggable
local function MakeDraggable(frame)
    local drag, dragInput, dragStart, startPos = false, nil, nil, nil
    frame.InputBegan:Connect(function(input)
        if input.UserInputType == Enum.UserInputType.MouseButton1 or input.UserInputType == Enum.UserInputType.Touch then
            drag = true; dragStart = input.Position; startPos = frame.Position
        end
    end)
    frame.InputChanged:Connect(function(input)
        if input.UserInputType == Enum.UserInputType.MouseMovement or input.UserInputType == Enum.UserInputType.Touch then dragInput = input end
    end)
    UserInputService.InputChanged:Connect(function(input)
        if input == dragInput and drag then
            local d = input.Position - dragStart
            frame.Position = UDim2.new(startPos.X.Scale, startPos.X.Offset + d.X, startPos.Y.Scale, startPos.Y.Offset + d.Y)
        end
    end)
    UserInputService.InputEnded:Connect(function(input)
        if input.UserInputType == Enum.UserInputType.MouseButton1 or input.UserInputType == Enum.UserInputType.Touch then drag = false end
    end)
end
MakeDraggable(LoginFrame)
MakeDraggable(MainHub)

--==============================================================
-- LOGIN LOGIC
--==============================================================
LoginBtn.MouseButton1Click:Connect(function()
    local key = KeyBox.Text
    local kd = ValidKeys[key]
    if kd and (kd.Expiry == 0 or os.time() < kd.Expiry) then
        IsLoggedIn = true
        LoginFrame.Visible = false
        MainHub.Visible = true
        MenuBtn.Visible = true
        MenuVisible = true
        LoginStatus.Text = "> ACCESS GRANTED..."
        Notify("✅ Success", "WELCOME V4.4 RESMI", 3)
        pcall(ActivateAntiKick)
        pcall(ActivateAutoReconnect)
        pcall(ActivateNightLock)
        Notify("🔒 NIGHT LOCK", "AUTO KICK ACTIVE", 3)
        task.wait(0.3)
        RefreshTeleportList()
    else
        LoginStatus.Text = "> ERROR: KEY INVALID"
        Notify("❌ Failed", "KEY INVALID", 2)
    end
end)

GetKeyBtn.MouseButton1Click:Connect(function()
    if setclipboard then
        setclipboard(KeyWebsite)
        Notify("Key", "LINK COPIED", 2)
    else
        Notify("Key", KeyWebsite, 3)
    end
end)

--==============================================================
-- FINAL DEBUG
--==============================================================
task.delay(0.5, function()
    print("========== ZET DEBUG ==========")
    print("ScreenGui.Parent:", ScreenGui.Parent and ScreenGui.Parent.Name or "NIL")
    print("LoginFrame.Visible:", LoginFrame.Visible)
    print("LoginFrame.AbsoluteSize:", LoginFrame.AbsoluteSize)
    print("MainHub.AbsoluteSize:", MainHub.AbsoluteSize)
    print("ScrollFrame.AbsoluteSize:", ScrollFrame.AbsoluteSize)
    print("Content.AbsoluteSize:", Content.AbsoluteSize)
    print("Final Canvas Y:", currentY)
    print("=================================")
end)

print("[ZET] ✅ ALL LOADED SUCCESSFULLY!")
