--[[
    ZetGames-AimLock-Advanserver | TIMER BUILD v4.4 (FIX v2)
    Theme: Red & Black (TESTING)
    Target Release: 30 September 2025 | 19:30 WIB | Rabu
--]]

--==============================================================
-- SERVICES
--==============================================================
local Players = game:GetService("Players")
local TweenService = game:GetService("TweenService")
local UserInputService = game:GetService("UserInputService")

local LocalPlayer = Players.LocalPlayer

--==============================================================
-- THEME COLORS (RED & BLACK)
--==============================================================
local THEME = {
    MainBG = Color3.fromRGB(10, 10, 10),
    PanelBG = Color3.fromRGB(15, 15, 15),
    SectionBG = Color3.fromRGB(40, 0, 0),
    AccentColor = Color3.fromRGB(255, 0, 0),
    AccentLight = Color3.fromRGB(255, 80, 80),
    AccentDark = Color3.fromRGB(150, 0, 0),
    ButtonBG = Color3.fromRGB(25, 25, 25),
    ButtonActive = Color3.fromRGB(100, 0, 0),
    TextColor = Color3.fromRGB(255, 0, 0),
    TextLight = Color3.fromRGB(255, 100, 100),
    WarningColor = Color3.fromRGB(255, 200, 0),
    SuccessColor = Color3.fromRGB(0, 255, 100),
}

--==============================================================
-- CONFIG — TARGET RELEASE
--==============================================================
local TARGET_YEAR = 2025
local TARGET_MONTH = 9   -- 9 = September
local TARGET_DAY = 30
local TARGET_HOUR = 19   -- 19:30
local TARGET_MIN = 30

local EXECUTE_URL = "https://raw.githubusercontent.com/arkaraffaza387-dotcom/Testing-Update/refs/heads/main/README.md"

--==============================================================
-- SCREEN GUI
--==============================================================
local ScreenGui = Instance.new("ScreenGui")
ScreenGui.Name = "ZetGamesAimLockAdvanserver"
ScreenGui.ResetOnSpawn = false
ScreenGui.IgnoreGuiInset = true
ScreenGui.ZIndexBehavior = Enum.ZIndexBehavior.Sibling

local parentSuccess = false
pcall(function()
    ScreenGui.Parent = game:GetService("CoreGui")
    parentSuccess = true
end)
if not parentSuccess then
    pcall(function()
        ScreenGui.Parent = LocalPlayer:WaitForChild("PlayerGui")
        parentSuccess = true
    end)
end
if not parentSuccess then
    pcall(function()
        ScreenGui.Parent = game:GetService("Players").LocalPlayer:WaitForChild("PlayerGui")
    end)
end

--==============================================================
-- NOTIFICATION
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
    Notif.BorderColor3 = THEME.AccentColor
    Notif.BorderSizePixel = 2
    Notif.ZIndex = 501
    Notif.Parent = Notifications
    Instance.new("UICorner", Notif).CornerRadius = UDim.new(0, 8)

    local Title = Instance.new("TextLabel")
    Title.Size = UDim2.new(1, -16, 0, 22)
    Title.Position = UDim2.new(0, 8, 0, 4)
    Title.BackgroundTransparency = 1
    Title.Text = title
    Title.TextColor3 = THEME.TextColor
    Title.Font = Enum.Font.Code
    Title.TextSize = 12
    Title.TextXAlignment = Enum.TextXAlignment.Left
    Title.ZIndex = 502
    Title.Parent = Notif

    local Msg = Instance.new("TextLabel")
    Msg.Size = UDim2.new(1, -16, 0, 22)
    Msg.Position = UDim2.new(0, 8, 0, 28)
    Msg.BackgroundTransparency = 1
    Msg.Text = message
    Msg.TextColor3 = THEME.TextLight
    Msg.Font = Enum.Font.Code
    Msg.TextSize = 10
    Msg.TextXAlignment = Enum.TextXAlignment.Left
    Msg.ZIndex = 502
    Msg.Parent = Notif

    TweenService:Create(Notif, TweenInfo.new(0.3), {Position = UDim2.new(0, 0, 0, 0)}):Play()
    task.delay(duration, function()
        local tw = TweenService:Create(Notif, TweenInfo.new(0.3), {Position = UDim2.new(0, 0, 0, -55)})
        tw:Play()
        tw.Completed:Connect(function() Notif:Destroy() end)
    end)
end

--==============================================================
-- FIX TOTAL: BANDINGKAN LANGSUNG PAKAI ANGKA
--==============================================================
-- Kita bandingkan angka tahun/bulan/tanggal/jam/menit
-- dari os.date("*t") yang mengembalikan waktu LOKAL DEVICE.

local function GetNowTable()
    return os.date("*t")
end

-- Konversi target ke "nomor urut" (format YYYYMMDDHHMM)
-- Contoh: 2025-09-30 19:30 → 202509301930
local function ToNumber(tbl)
    return tbl.year * 100000000
         + tbl.month * 1000000
         + tbl.day * 10000
         + tbl.hour * 100
         + tbl.min
end

local TARGET_NUM = TARGET_YEAR * 100000000
                 + TARGET_MONTH * 1000000
                 + TARGET_DAY * 10000
                 + TARGET_HOUR * 100
                 + TARGET_MIN

--==============================================================
-- HITUNG SISA WAKTU (PAKAI DETIK)
--==============================================================
local function GetNowNum()
    return ToNumber(GetNowTable())
end

-- Hitung selisih dalam detik dengan cara akurat:
-- Kita ubah target ke epoch time lokal
local function GetTargetEpoch()
    -- os.time() menerima table dengan format lokal
    -- jadi langsung aja, tidak perlu konversi WIB/UTC
    return os.time({
        year = TARGET_YEAR,
        month = TARGET_MONTH,
        day = TARGET_DAY,
        hour = TARGET_HOUR,
        min = TARGET_MIN,
        sec = 0
    })
end

local function GetNowEpoch()
    return os.time()
end

local function FormatCountdown(seconds)
    if seconds < 0 then seconds = 0 end
    local days = math.floor(seconds / 86400)
    local hours = math.floor((seconds % 86400) / 3600)
    local mins = math.floor((seconds % 3600) / 60)
    local secs = math.floor(seconds % 60)
    return days, hours, mins, secs
end

local function IsTimeReached()
    -- Bandingkan langsung pakai angka YYYYMMDDHHMM
    local nowNum = GetNowNum()
    return nowNum >= TARGET_NUM
end

--==============================================================
-- DEBUG INFO
--==============================================================
local function PrintDebug()
    local nowTbl = GetNowTable()
    local nowNum = GetNowNum()
    local target = GetTargetEpoch()
    local now = GetNowEpoch()
    local remaining = target - now
    
    print("╔══════════════════════════════════════════╗")
    print("║      ZETGAMES TIMER - DEBUG INFO v2      ║")
    print("╠══════════════════════════════════════════╣")
    print(string.format("║ Now (local):  %04d-%02d-%02d %02d:%02d:%02d",
        nowTbl.year, nowTbl.month, nowTbl.day, nowTbl.hour, nowTbl.min, nowTbl.sec))
    print(string.format("║ Target:       %04d-%02d-%02d %02d:%02d:00",
        TARGET_YEAR, TARGET_MONTH, TARGET_DAY, TARGET_HOUR, TARGET_MIN))
    print(string.format("║ Now (number): %d", nowNum))
    print(string.format("║ Target (num): %d", TARGET_NUM))
    print(string.format("║ Remaining:    %d seconds", remaining))
    print(string.format("║ Status:       %s", IsTimeReached() and "REACHED!" or "WAITING"))
    print("╚══════════════════════════════════════════╝")
end

--==============================================================
-- EXECUTE
--==============================================================
local hasExecuted = false

local function ExecuteNewScript()
    if hasExecuted then return end
    hasExecuted = true
    
    Notify("System", "> TIME REACHED! LOADING v4.4...", 3)
    task.wait(1)
    
    local success, err = pcall(function()
        loadstring(game:HttpGet(EXECUTE_URL))()
    end)
    
    if success then
        Notify("Success", "> v4.4 LOADED", 3)
    else
        Notify("Error", "> FAILED TO LOAD", 3)
        warn("[ZetGames] Execute Error: " .. tostring(err))
    end
end

--==============================================================
-- TIMER FRAME UI
--==============================================================
local TimerFrame = Instance.new("Frame")
TimerFrame.Size = UDim2.new(0, 400, 0, 480)
TimerFrame.Position = UDim2.new(0.5, -200, 0.5, -240)
TimerFrame.BackgroundColor3 = THEME.MainBG
TimerFrame.BorderColor3 = THEME.AccentColor
TimerFrame.BorderSizePixel = 3
TimerFrame.ZIndex = 10
TimerFrame.Visible = false
TimerFrame.Parent = ScreenGui
Instance.new("UICorner", TimerFrame).CornerRadius = UDim.new(0, 12)

local TopBar = Instance.new("Frame")
TopBar.Size = UDim2.new(1, 0, 0, 40)
TopBar.BackgroundColor3 = THEME.SectionBG
TopBar.BorderSizePixel = 0
TopBar.ZIndex = 11
TopBar.Parent = TimerFrame
Instance.new("UICorner", TopBar).CornerRadius = UDim.new(0, 12)

local TopTxt = Instance.new("TextLabel")
TopTxt.Size = UDim2.new(1, -16, 1, 0)
TopTxt.Position = UDim2.new(0, 8, 0, 0)
TopTxt.BackgroundTransparency = 1
TopTxt.Text = "● ZETGAMES-AIMLOCK v4.4 TIMER"
TopTxt.TextColor3 = THEME.TextColor
TopTxt.Font = Enum.Font.Code
TopTxt.TextSize = 13
TopTxt.TextXAlignment = Enum.TextXAlignment.Left
TopTxt.ZIndex = 12
TopTxt.Parent = TopBar

local MTitle = Instance.new("TextLabel")
MTitle.Size = UDim2.new(1, -30, 0, 35)
MTitle.Position = UDim2.new(0, 15, 0, 55)
MTitle.BackgroundTransparency = 1
MTitle.Text = "⏳ WAITING FOR RELEASE ⏳"
MTitle.TextColor3 = THEME.WarningColor
MTitle.Font = Enum.Font.Code
MTitle.TextSize = 18
MTitle.ZIndex = 12
MTitle.Parent = TimerFrame

local MTag = Instance.new("TextLabel")
MTag.Size = UDim2.new(1, -30, 0, 20)
MTag.Position = UDim2.new(0, 15, 0, 90)
MTag.BackgroundTransparency = 1
MTag.Text = "[ TESTING BUILD - v4.4 ]"
MTag.TextColor3 = THEME.WarningColor
MTag.Font = Enum.Font.Code
MTag.TextSize = 11
MTag.ZIndex = 12
MTag.Parent = TimerFrame

local ReleaseInfo = Instance.new("TextLabel")
ReleaseInfo.Size = UDim2.new(1, -30, 0, 25)
ReleaseInfo.Position = UDim2.new(0, 15, 0, 120)
ReleaseInfo.BackgroundTransparency = 1
ReleaseInfo.Text = "> RELEASE: 30 SEPTEMBER 2025 | 19:30 WIB"
ReleaseInfo.TextColor3 = THEME.TextLight
ReleaseInfo.Font = Enum.Font.Code
ReleaseInfo.TextSize = 11
ReleaseInfo.TextXAlignment = Enum.TextXAlignment.Center
ReleaseInfo.ZIndex = 12
ReleaseInfo.Parent = TimerFrame

local DayInfo = Instance.new("TextLabel")
DayInfo.Size = UDim2.new(1, -30, 0, 20)
DayInfo.Position = UDim2.new(0, 15, 0, 145)
DayInfo.BackgroundTransparency = 1
DayInfo.Text = "> HARI: RABU"
DayInfo.TextColor3 = THEME.AccentLight
DayInfo.Font = Enum.Font.Code
DayInfo.TextSize = 11
DayInfo.TextXAlignment = Enum.TextXAlignment.Center
DayInfo.ZIndex = 12
DayInfo.Parent = TimerFrame

local TimerBox = Instance.new("Frame")
TimerBox.Size = UDim2.new(1, -30, 0, 130)
TimerBox.Position = UDim2.new(0, 15, 0, 175)
TimerBox.BackgroundColor3 = THEME.PanelBG
TimerBox.BorderColor3 = THEME.AccentColor
TimerBox.BorderSizePixel = 2
TimerBox.ZIndex = 12
TimerBox.Parent = TimerFrame
Instance.new("UICorner", TimerBox).CornerRadius = UDim.new(0, 8)

local CountdownLbl = Instance.new("TextLabel")
CountdownLbl.Size = UDim2.new(1, -10, 0, 20)
CountdownLbl.Position = UDim2.new(0, 5, 0, 5)
CountdownLbl.BackgroundTransparency = 1
CountdownLbl.Text = "> COUNTDOWN:"
CountdownLbl.TextColor3 = THEME.TextColor
CountdownLbl.Font = Enum.Font.Code
CountdownLbl.TextSize = 11
CountdownLbl.TextXAlignment = Enum.TextXAlignment.Left
CountdownLbl.ZIndex = 13
CountdownLbl.Parent = TimerBox

local TimerDisplay = Instance.new("TextLabel")
TimerDisplay.Size = UDim2.new(1, -20, 0, 50)
TimerDisplay.Position = UDim2.new(0, 10, 0, 30)
TimerDisplay.BackgroundTransparency = 1
TimerDisplay.Text = "00 : 00 : 00 : 00"
TimerDisplay.TextColor3 = THEME.AccentColor
TimerDisplay.Font = Enum.Font.Code
TimerDisplay.TextSize = 28
TimerDisplay.TextXAlignment = Enum.TextXAlignment.Center
TimerDisplay.ZIndex = 13
TimerDisplay.Parent = TimerBox

local LabelsFrame = Instance.new("Frame")
LabelsFrame.Size = UDim2.new(1, -20, 0, 20)
LabelsFrame.Position = UDim2.new(0, 10, 0, 85)
LabelsFrame.BackgroundTransparency = 1
LabelsFrame.ZIndex = 13
LabelsFrame.Parent = TimerBox

local function CreateTimerLabel(text, xPos)
    local lbl = Instance.new("TextLabel")
    lbl.Size = UDim2.new(0.25, 0, 1, 0)
    lbl.Position = UDim2.new(xPos, 0, 0, 0)
    lbl.BackgroundTransparency = 1
    lbl.Text = text
    lbl.TextColor3 = THEME.TextLight
    lbl.Font = Enum.Font.Code
    lbl.TextSize = 10
    lbl.TextXAlignment = Enum.TextXAlignment.Center
    lbl.ZIndex = 14
    lbl.Parent = LabelsFrame
end

CreateTimerLabel("DAYS", 0)
CreateTimerLabel("HOURS", 0.25)
CreateTimerLabel("MINS", 0.5)
CreateTimerLabel("SECS", 0.75)

local Sep = Instance.new("Frame")
Sep.Size = UDim2.new(1, -30, 0, 2)
Sep.Position = UDim2.new(0, 15, 0, 320)
Sep.BackgroundColor3 = THEME.AccentColor
Sep.BorderSizePixel = 0
Sep.ZIndex = 12
Sep.Parent = TimerFrame

local StatusLbl = Instance.new("TextLabel")
StatusLbl.Size = UDim2.new(1, -30, 0, 25)
StatusLbl.Position = UDim2.new(0, 15, 0, 330)
StatusLbl.BackgroundTransparency = 1
StatusLbl.Text = "> STATUS: WAITING FOR RELEASE..."
StatusLbl.TextColor3 = THEME.TextColor
StatusLbl.Font = Enum.Font.Code
StatusLbl.TextSize = 11
StatusLbl.TextXAlignment = Enum.TextXAlignment.Left
StatusLbl.ZIndex = 12
StatusLbl.Parent = TimerFrame

local TimeInfoLbl = Instance.new("TextLabel")
TimeInfoLbl.Size = UDim2.new(1, -30, 0, 20)
TimeInfoLbl.Position = UDim2.new(0, 15, 0, 360)
TimeInfoLbl.BackgroundTransparency = 1
TimeInfoLbl.Text = "> DEVICE TIME: --"
TimeInfoLbl.TextColor3 = THEME.TextLight
TimeInfoLbl.Font = Enum.Font.Code
TimeInfoLbl.TextSize = 10
TimeInfoLbl.TextXAlignment = Enum.TextXAlignment.Left
TimeInfoLbl.ZIndex = 12
TimeInfoLbl.Parent = TimerFrame

local TargetInfoLbl = Instance.new("TextLabel")
TargetInfoLbl.Size = UDim2.new(1, -30, 0, 20)
TargetInfoLbl.Position = UDim2.new(0, 15, 0, 380)
TargetInfoLbl.BackgroundTransparency = 1
TargetInfoLbl.Text = "> TARGET TIME: --"
TargetInfoLbl.TextColor3 = THEME.TextLight
TargetInfoLbl.Font = Enum.Font.Code
TargetInfoLbl.TextSize = 10
TargetInfoLbl.TextXAlignment = Enum.TextXAlignment.Left
TargetInfoLbl.ZIndex = 12
TargetInfoLbl.Parent = TimerFrame

local InfoLbl = Instance.new("TextLabel")
InfoLbl.Size = UDim2.new(1, -30, 0, 50)
InfoLbl.Position = UDim2.new(0, 15, 0, 405)
InfoLbl.BackgroundTransparency = 1
InfoLbl.Text = "> Script akan otomatis dijalankan\n> saat waktu release tercapai"
InfoLbl.TextColor3 = THEME.TextLight
InfoLbl.Font = Enum.Font.Code
InfoLbl.TextSize = 10
InfoLbl.TextXAlignment = Enum.TextXAlignment.Left
InfoLbl.ZIndex = 12
InfoLbl.Parent = TimerFrame

--==============================================================
-- DRAGGABLE
--==============================================================
local function MakeDraggable(frame)
    local dragging = false
    local dragInput, dragStart, startPos

    frame.InputBegan:Connect(function(input)
        if input.UserInputType == Enum.UserInputType.MouseButton1 or input.UserInputType == Enum.UserInputType.Touch then
            dragging = true
            dragStart = input.Position
            startPos = frame.Position
        end
    end)

    frame.InputChanged:Connect(function(input)
        if input.UserInputType == Enum.UserInputType.MouseMovement or input.UserInputType == Enum.UserInputType.Touch then
            dragInput = input
        end
    end)

    UserInputService.InputChanged:Connect(function(input)
        if input == dragInput and dragging then
            local delta = input.Position - dragStart
            frame.Position = UDim2.new(startPos.X.Scale, startPos.X.Offset + delta.X, startPos.Y.Scale, startPos.Y.Offset + delta.Y)
        end
    end)

    UserInputService.InputEnded:Connect(function(input)
        if input.UserInputType == Enum.UserInputType.MouseButton1 or input.UserInputType == Enum.UserInputType.Touch then
            dragging = false
        end
    end)
end

MakeDraggable(TimerFrame)

--==============================================================
-- LOADING SCREEN
--==============================================================
local LoadingScreen = Instance.new("Frame")
LoadingScreen.Size = UDim2.new(1, 0, 1, 0)
LoadingScreen.BackgroundColor3 = Color3.fromRGB(5, 0, 0)
LoadingScreen.BorderSizePixel = 0
LoadingScreen.ZIndex = 300
LoadingScreen.Visible = true
LoadingScreen.Parent = ScreenGui

local LoadingBg = Instance.new("Frame")
LoadingBg.Size = UDim2.new(0, 340, 0, 180)
LoadingBg.Position = UDim2.new(0.5, -170, 0.5, -90)
LoadingBg.BackgroundColor3 = THEME.MainBG
LoadingBg.BorderColor3 = THEME.AccentColor
LoadingBg.BorderSizePixel = 2
LoadingBg.ZIndex = 301
LoadingBg.Parent = LoadingScreen
Instance.new("UICorner", LoadingBg).CornerRadius = UDim.new(0, 15)

local LTitle = Instance.new("TextLabel")
LTitle.Size = UDim2.new(1, -30, 0, 35)
LTitle.Position = UDim2.new(0, 15, 0, 15)
LTitle.BackgroundTransparency = 1
LTitle.Text = "ZETGAMES-AIMLOCK"
LTitle.TextColor3 = THEME.TextColor
LTitle.Font = Enum.Font.Code
LTitle.TextSize = 20
LTitle.ZIndex = 302
LTitle.Parent = LoadingBg

local LTag = Instance.new("TextLabel")
LTag.Size = UDim2.new(1, -30, 0, 20)
LTag.Position = UDim2.new(0, 15, 0, 50)
LTag.BackgroundTransparency = 1
LTag.Text = "[ TIMER BUILD - v4.4 ]"
LTag.TextColor3 = THEME.WarningColor
LTag.Font = Enum.Font.Code
LTag.TextSize = 11
LTag.ZIndex = 302
LTag.Parent = LoadingBg

local LBarBg = Instance.new("Frame")
LBarBg.Size = UDim2.new(1, -30, 0, 15)
LBarBg.Position = UDim2.new(0, 15, 0, 90)
LBarBg.BackgroundColor3 = Color3.fromRGB(30, 10, 10)
LBarBg.BorderColor3 = THEME.AccentColor
LBarBg.BorderSizePixel = 1
LBarBg.ZIndex = 302
LBarBg.Parent = LoadingBg
Instance.new("UICorner", LBarBg).CornerRadius = UDim.new(0, 7)

local LBarFill = Instance.new("Frame")
LBarFill.Size = UDim2.new(0, 0, 1, 0)
LBarFill.BackgroundColor3 = THEME.AccentColor
LBarFill.BorderSizePixel = 0
LBarFill.ZIndex = 303
LBarFill.Parent = LBarBg
Instance.new("UICorner", LBarFill).CornerRadius = UDim.new(0, 7)

local LPercent = Instance.new("TextLabel")
LPercent.Size = UDim2.new(1, -30, 0, 20)
LPercent.Position = UDim2.new(0, 15, 0, 115)
LPercent.BackgroundTransparency = 1
LPercent.Text = "0%"
LPercent.TextColor3 = THEME.TextColor
LPercent.Font = Enum.Font.Code
LPercent.TextSize = 14
LPercent.ZIndex = 302
LPercent.Parent = LoadingBg

local LStatus = Instance.new("TextLabel")
LStatus.Size = UDim2.new(1, -30, 0, 20)
LStatus.Position = UDim2.new(0, 15, 0, 145)
LStatus.BackgroundTransparency = 1
LStatus.Text = "> LOADING TIMER..."
LStatus.TextColor3 = THEME.TextLight
LStatus.Font = Enum.Font.Code
LStatus.TextSize = 10
LStatus.TextXAlignment = Enum.TextXAlignment.Left
LStatus.ZIndex = 302
LStatus.Parent = LoadingBg

--==============================================================
-- UPDATE TIMER DISPLAY
--==============================================================
local function UpdateTimerDisplay()
    local nowTbl = GetNowTable()
    local targetEpoch = GetTargetEpoch()
    local nowEpoch = GetNowEpoch()
    local remaining = targetEpoch - nowEpoch
    
    TimeInfoLbl.Text = string.format("> DEVICE TIME: %04d-%02d-%02d %02d:%02d:%02d",
        nowTbl.year, nowTbl.month, nowTbl.day, nowTbl.hour, nowTbl.min, nowTbl.sec)
    
    TargetInfoLbl.Text = string.format("> TARGET TIME: %04d-%02d-%02d %02d:%02d:00",
        TARGET_YEAR, TARGET_MONTH, TARGET_DAY, TARGET_HOUR, TARGET_MIN)
    
    if IsTimeReached() then
        TimerDisplay.Text = "00 : 00 : 00 : 00"
        TimerDisplay.TextColor3 = THEME.SuccessColor
        StatusLbl.Text = "> STATUS: RELEASE TIME REACHED!"
        StatusLbl.TextColor3 = THEME.SuccessColor
        return false
    end
    
    local days, hours, mins, secs = FormatCountdown(remaining)
    TimerDisplay.Text = string.format("%02d : %02d : %02d : %02d", days, hours, mins, secs)
    StatusLbl.Text = string.format("> STATUS: WAITING... (%dd %dh %dm %ds)", days, hours, mins, secs)
    return true
end

--==============================================================
-- MAIN LOOP
--==============================================================
task.spawn(function()
    PrintDebug()
    
    task.wait(0.3)
    local totalTime = 3
    local steps = 100
    local interval = totalTime / steps
    local loadingMsgs = {
        "> LOADING TIMER SYSTEM...",
        "> CHECKING RELEASE DATE...",
        "> INITIALIZING COUNTDOWN...",
        "> SYSTEM READY!"
    }
    
    for i = 1, steps do
        task.wait(interval)
        pcall(function()
            LBarFill.Size = UDim2.new(i / 100, 0, 1, 0)
            LPercent.Text = i .. "%"
            local mi = math.floor(i / 25) + 1
            if mi > #loadingMsgs then mi = #loadingMsgs end
            LStatus.Text = loadingMsgs[mi]
        end)
    end
    
    pcall(function()
        LPercent.Text = "100%"
        LStatus.Text = "> SYSTEM READY!"
        LBarFill.Size = UDim2.new(1, 0, 1, 0)
    end)
    
    task.wait(0.5)
    pcall(function()
        LoadingScreen.Visible = false
        TimerFrame.Visible = true
    end)
    
    if IsTimeReached() then
        Notify("System", "> RELEASE TIME REACHED!", 3)
        Notify("Info", "> Auto-loading v4.4...", 3)
        task.wait(2)
        ExecuteNewScript()
        return
    end
    
    Notify("Timer v4.4", "> COUNTDOWN STARTED", 3)
    Notify("Release", "> 30 SEPT 2025 | 19:30 WIB", 3)
    
    while true do
        task.wait(1)
        local shouldContinue = UpdateTimerDisplay()
        if not shouldContinue then
            Notify("System", "> RELEASE TIME REACHED!", 3)
            task.wait(2)
            ExecuteNewScript()
            break
        end
    end
end)

print("[ZetGames-AimLock] TIMER BUILD v4.4 (FIX v2) - Loaded")
print(string.format("[ZetGames] Target: %04d-%02d-%02d %02d:%02d", TARGET_YEAR, TARGET_MONTH, TARGET_DAY, TARGET_HOUR, TARGET_MIN))
