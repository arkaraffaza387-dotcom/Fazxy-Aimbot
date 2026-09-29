--[[
    ZetGames-AimLock-Advanserver | INFO BUILD v4.4
    Theme: Red & Black (TESTING)
    Info: Update selesai 30 September 2025 | 19:30 WIB | Rabu
    No Timer - No Auto Execute - Just Info Display
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
    TextColor = Color3.fromRGB(255, 0, 0),
    TextLight = Color3.fromRGB(255, 100, 100),
    WarningColor = Color3.fromRGB(255, 200, 0),
    SuccessColor = Color3.fromRGB(0, 255, 100),
}

--==============================================================
-- SCREEN GUI (FIXED - MULTIPLE FALLBACK)
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
-- INFO FRAME (MAIN UI)
--==============================================================
local InfoFrame = Instance.new("Frame")
InfoFrame.Size = UDim2.new(0, 400, 0, 420)
InfoFrame.Position = UDim2.new(0.5, -200, 0.5, -210)
InfoFrame.BackgroundColor3 = THEME.MainBG
InfoFrame.BorderColor3 = THEME.AccentColor
InfoFrame.BorderSizePixel = 3
InfoFrame.ZIndex = 10
InfoFrame.Visible = false
InfoFrame.Parent = ScreenGui
Instance.new("UICorner", InfoFrame).CornerRadius = UDim.new(0, 12)

-- TOP BAR
local TopBar = Instance.new("Frame")
TopBar.Size = UDim2.new(1, 0, 0, 40)
TopBar.BackgroundColor3 = THEME.SectionBG
TopBar.BorderSizePixel = 0
TopBar.ZIndex = 11
TopBar.Parent = InfoFrame
Instance.new("UICorner", TopBar).CornerRadius = UDim.new(0, 12)

local TopTxt = Instance.new("TextLabel")
TopTxt.Size = UDim2.new(1, -16, 1, 0)
TopTxt.Position = UDim2.new(0, 8, 0, 0)
TopTxt.BackgroundTransparency = 1
TopTxt.Text = "● ZETGAMES-AIMLOCK v4.4 INFO"
TopTxt.TextColor3 = THEME.TextColor
TopTxt.Font = Enum.Font.Code
TopTxt.TextSize = 13
TopTxt.TextXAlignment = Enum.TextXAlignment.Left
TopTxt.ZIndex = 12
TopTxt.Parent = TopBar

-- TITLE
local MTitle = Instance.new("TextLabel")
MTitle.Size = UDim2.new(1, -30, 0, 35)
MTitle.Position = UDim2.new(0, 15, 0, 55)
MTitle.BackgroundTransparency = 1
MTitle.Text = "📢 UPDATE INFORMATION 📢"
MTitle.TextColor3 = THEME.WarningColor
MTitle.Font = Enum.Font.Code
MTitle.TextSize = 18
MTitle.ZIndex = 12
MTitle.Parent = InfoFrame

-- TAG
local MTag = Instance.new("TextLabel")
MTag.Size = UDim2.new(1, -30, 0, 20)
MTag.Position = UDim2.new(0, 15, 0, 90)
MTag.BackgroundTransparency = 1
MTag.Text = "[ TESTING BUILD - v4.4 ]"
MTag.TextColor3 = THEME.WarningColor
MTag.Font = Enum.Font.Code
MTag.TextSize = 11
MTag.ZIndex = 12
MTag.Parent = InfoFrame

-- MAIN INFO BOX
local InfoBox = Instance.new("Frame")
InfoBox.Size = UDim2.new(1, -30, 0, 200)
InfoBox.Position = UDim2.new(0, 15, 0, 125)
InfoBox.BackgroundColor3 = THEME.PanelBG
InfoBox.BorderColor3 = THEME.AccentColor
InfoBox.BorderSizePixel = 2
InfoBox.ZIndex = 12
InfoBox.Parent = InfoFrame
Instance.new("UICorner", InfoBox).CornerRadius = UDim.new(0, 8)

-- LABEL "UPDATE SELESAI PADA:"
local InfoTitle = Instance.new("TextLabel")
InfoTitle.Size = UDim2.new(1, -20, 0, 25)
InfoTitle.Position = UDim2.new(0, 10, 0, 15)
InfoTitle.BackgroundTransparency = 1
InfoTitle.Text = "> UPDATE SELESAI PADA:"
InfoTitle.TextColor3 = THEME.TextColor
InfoTitle.Font = Enum.Font.Code
InfoTitle.TextSize = 12
InfoTitle.TextXAlignment = Enum.TextXAlignment.Left
InfoTitle.ZIndex = 13
InfoTitle.Parent = InfoBox

-- TANGGAL
local DateLbl = Instance.new("TextLabel")
DateLbl.Size = UDim2.new(1, -20, 0, 35)
DateLbl.Position = UDim2.new(0, 10, 0, 45)
DateLbl.BackgroundTransparency = 1
DateLbl.Text = "30 SEPTEMBER 2025"
DateLbl.TextColor3 = THEME.WarningColor
DateLbl.Font = Enum.Font.Code
DateLbl.TextSize = 20
DateLbl.TextXAlignment = Enum.TextXAlignment.Left
DateLbl.ZIndex = 13
DateLbl.Parent = InfoBox

-- JAM
local TimeLbl = Instance.new("TextLabel")
TimeLbl.Size = UDim2.new(1, -20, 0, 30)
TimeLbl.Position = UDim2.new(0, 10, 0, 85)
TimeLbl.BackgroundTransparency = 1
TimeLbl.Text = "⏰ JAM: 19:30 WIB"
TimeLbl.TextColor3 = THEME.AccentLight
TimeLbl.Font = Enum.Font.Code
TimeLbl.TextSize = 16
TimeLbl.TextXAlignment = Enum.TextXAlignment.Left
TimeLbl.ZIndex = 13
TimeLbl.Parent = InfoBox

-- HARI
local DayLbl = Instance.new("TextLabel")
DayLbl.Size = UDim2.new(1, -20, 0, 25)
DayLbl.Position = UDim2.new(0, 10, 0, 120)
DayLbl.BackgroundTransparency = 1
DayLbl.Text = "📅 HARI: RABU"
DayLbl.TextColor3 = THEME.AccentLight
DayLbl.Font = Enum.Font.Code
DayLbl.TextSize = 14
DayLbl.TextXAlignment = Enum.TextXAlignment.Left
DayLbl.ZIndex = 13
DayLbl.Parent = InfoBox

-- SEPARATOR
local Sep2 = Instance.new("Frame")
Sep2.Size = UDim2.new(1, -20, 0, 2)
Sep2.Position = UDim2.new(0, 10, 0, 155)
Sep2.BackgroundColor3 = THEME.AccentColor
Sep2.BorderSizePixel = 0
Sep2.ZIndex = 13
Sep2.Parent = InfoBox

-- STATUS
local StatusLbl = Instance.new("TextLabel")
StatusLbl.Size = UDim2.new(1, -20, 0, 25)
StatusLbl.Position = UDim2.new(0, 10, 0, 165)
StatusLbl.BackgroundTransparency = 1
StatusLbl.Text = "> STATUS: DALAM PROSES PATCH..."
StatusLbl.TextColor3 = THEME.TextLight
StatusLbl.Font = Enum.Font.Code
StatusLbl.TextSize = 11
StatusLbl.TextXAlignment = Enum.TextXAlignment.Left
StatusLbl.ZIndex = 13
StatusLbl.Parent = InfoBox

-- SEPARATOR
local Sep = Instance.new("Frame")
Sep.Size = UDim2.new(1, -30, 0, 2)
Sep.Position = UDim2.new(0, 15, 0, 340)
Sep.BackgroundColor3 = THEME.AccentColor
Sep.BorderSizePixel = 0
Sep.ZIndex = 12
Sep.Parent = InfoFrame

-- INFO TAMBAHAN
local InfoMsg = Instance.new("TextLabel")
InfoMsg.Size = UDim2.new(1, -30, 0, 60)
InfoMsg.Position = UDim2.new(0, 15, 0, 350)
InfoMsg.BackgroundTransparency = 1
InfoMsg.Text = "> Script akan otomatis tersedia\n> setelah waktu update selesai\n> Mohon tunggu dengan sabar"
InfoMsg.TextColor3 = THEME.TextLight
InfoMsg.Font = Enum.Font.Code
InfoMsg.TextSize = 10
InfoMsg.TextXAlignment = Enum.TextXAlignment.Left
InfoMsg.ZIndex = 12
InfoMsg.Parent = InfoFrame

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

MakeDraggable(InfoFrame)

--==============================================================
-- LOADING SCREEN (MINI)
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
LTag.Text = "[ INFO BUILD - v4.4 ]"
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
LStatus.Text = "> LOADING INFO..."
LStatus.TextColor3 = THEME.TextLight
LStatus.Font = Enum.Font.Code
LStatus.TextSize = 10
LStatus.TextXAlignment = Enum.TextXAlignment.Left
LStatus.ZIndex = 302
LStatus.Parent = LoadingBg

--==============================================================
-- LOADING ANIMATION
--==============================================================
task.spawn(function()
    task.wait(0.3)
    local totalTime = 3
    local steps = 100
    local interval = totalTime / steps
    local loadingMsgs = {
        "> LOADING INFO SYSTEM...",
        "> FETCHING UPDATE DATA...",
        "> PREPARING DISPLAY...",
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
        InfoFrame.Visible = true
    end)
    
    Notify("ZetGames v4.4", "> INFO BUILD LOADED", 3)
    Notify("Update Info", "> SELESAI 30 SEPT 2025", 3)
end)

print("[ZetGames-AimLock] INFO BUILD v4.4 - Loaded Successfully")
print("[ZetGames] Update Release: 30 September 2025 | 19:30 WIB | Rabu")
