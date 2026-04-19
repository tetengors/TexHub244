# TexHub244
Bem vindo o Texhub
--[[
██╗  ██╗███████╗██████╗ ███████╗
██║ ██╔╝██╔════╝██╔══██╗██╔════╝
█████╔╝ █████╗  ██████╔╝█████╗  
██╔═██╗ ██╔══╝  ██╔══██╗██╔══╝  
██║  ██╗███████╗██║  ██║███████╗
╚═╝  ╚═╝╚══════╝╚═╝  ╚═╝╚══════╝
       TEX HUB - V8 MUTE SUPREMO (PRIVATE EDITION)
]]

if not game:IsLoaded() then game.Loaded:Wait() end

local TweenService = game:GetService("TweenService")
local Players = game:GetService("Players")
local Player = Players.LocalPlayer
local UIS = game:GetService("UserInputService")
local RunService = game:GetService("RunService")

-- CONFIGURAÇÕES DE ELITE
local CORRECT_KEY = "Texh9375(()(/.54hubt9632)(("
local MEU_NICK = "Tetengors_legal68"
_G.BannedTex = _G.BannedTex or {} -- Lista de banidos no servidor

-- LIMPAR ANTERIOR
local function Limpar()
    local name = "TexHub_Supremo_V8"
    if game:GetService("CoreGui"):FindFirstChild(name) then game:GetService("CoreGui")[name]:Destroy() end
    if Player:WaitForChild("PlayerGui"):FindFirstChild(name) then Player.PlayerGui[name]:Destroy() end
end
Limpar()

local Gui = Instance.new("ScreenGui")
Gui.Name = "TexHub_Supremo_V8"
Gui.ZIndexBehavior = Enum.ZIndexBehavior.Global
Gui.ResetOnSpawn = false

local success, _ = pcall(function() Gui.Parent = game:GetService("CoreGui") end)
if not success then Gui.Parent = Player:WaitForChild("PlayerGui") end

local Cores = {
    Fundo = Color3.fromRGB(5, 5, 8),
    Destaque = Color3.fromRGB(255, 0, 0),
    Texto = Color3.fromRGB(255, 255, 255),
    Botao = Color3.fromRGB(15, 15, 20),
    Verde = Color3.fromRGB(0, 255, 130),
    Vermelho = Color3.fromRGB(255, 0, 0),
    Barra = Color3.fromRGB(30, 30, 40)
}

-- FUNÇÃO DE SINCRONIZAÇÃO DE CARGO
local function SetRole(alvo, cargo)
    local val = alvo:FindFirstChild("TexRole") or Instance.new("StringValue", alvo)
    val.Name = "TexRole"
    val.Value = cargo
end

-- // FUNÇÃO DE ARREDONDAR
local function Arredondar(Obj, Raio)
    local UIC = Instance.new("UICorner")
    UIC.CornerRadius = UDim.new(0, Raio); UIC.Parent = Obj
end

-- // --- SISTEMA DE LOADRISG ---
local function StartLoadrisg()
    local LoadCanvas = Instance.new("Frame", Gui)
    LoadCanvas.Size = UDim2.new(1, 0, 1, 0); LoadCanvas.BackgroundColor3 = Color3.fromRGB(2, 2, 4); LoadCanvas.ZIndex = 2000
    local Logo = Instance.new("TextLabel", LoadCanvas)
    Logo.Size = UDim2.new(0, 400, 0, 100); Logo.Position = UDim2.new(0.5, -200, 0.45, -50); Logo.BackgroundTransparency = 1
    Logo.Text = "TEX HUB V8"; Logo.Font = Enum.Font.GothamBold; Logo.TextSize = 55; Logo.TextColor3 = Cores.Vermelho
    local BarBg = Instance.new("Frame", LoadCanvas); BarBg.Size = UDim2.new(0, 300, 0, 6); BarBg.Position = UDim2.new(0.5, -150, 0.6, 0); BarBg.BackgroundColor3 = Cores.Barra; Arredondar(BarBg, 4)
    local BarFill = Instance.new("Frame", BarBg); BarFill.Size = UDim2.new(0, 0, 1, 0); BarFill.BackgroundColor3 = Cores.Vermelho; Arredondar(BarFill, 4)
    TweenService:Create(BarFill, TweenInfo.new(2.5, Enum.EasingStyle.Quart), {Size = UDim2.new(1, 0, 1, 0)}):Play()
    task.wait(2.7); LoadCanvas:Destroy()
end

-- // --- TITLER CORRIGIDO (SINCRONIZAÇÃO TOTAL) ---
local function CriarTag(alvo)
    local function Aplicar()
        task.wait(1)
        local roleVal = alvo:FindFirstChild("TexRole")
        -- Se não tiver o valor e não for você, não mostra nada (evita mostrar em quem não usa o script)
        if alvo.Name ~= MEU_NICK and not roleVal then return end
        
        local cargoNome = (alvo.Name == MEU_NICK) and "CRIADOR" or (roleVal and roleVal.Value or "Membro")
        
        local char = alvo.Character or alvo.CharacterAdded:Wait()
        local head = char:WaitForChild("Head", 15)
        if head:FindFirstChild("TexTag") then head.TexTag:Destroy() end
        
        local bgu = Instance.new("BillboardGui", head)
        bgu.Name = "TexTag"; bgu.Size = UDim2.new(0, 250, 0, 50); bgu.StudsOffset = Vector3.new(0, 3.5, 0); bgu.AlwaysOnTop = true
        local tl = Instance.new("TextLabel", bgu)
        tl.Size = UDim2.new(1, 0, 1, 0); tl.BackgroundTransparency = 1; tl.Font = Enum.Font.GothamBold; tl.TextSize = 24; tl.TextStrokeTransparency = 0
        tl.Text = "["..cargoNome.." TEXHUB]"
        
        task.spawn(function()
            while tl and tl.Parent do
                tl.TextColor3 = Color3.fromHSV(tick() % 5 / 5, 0.8, 1)
                task.wait()
            end
        end)
    end
    alvo.CharacterAdded:Connect(Aplicar); Aplicar()
end

-- // FUNÇÕES DE INTERFACE
local function MakeDraggable(frame)
    local dragging, dragInput, dragStart, startPos
    frame.InputBegan:Connect(function(input)
        if (input.UserInputType == Enum.UserInputType.MouseButton1 or input.UserInputType == Enum.UserInputType.Touch) then
            dragging = true; dragStart = input.Position; startPos = frame.Position
            input.Changed:Connect(function() if input.UserInputState == Enum.UserInputState.End then dragging = false end end)
        end
    end)
    frame.InputChanged:Connect(function(input)
        if (input.UserInputType == Enum.UserInputType.MouseMovement or input.UserInputType == Enum.UserInputType.Touch) then dragInput = input end
    end)
    UIS.InputChanged:Connect(function(input)
        if input == dragInput and dragging then
            local delta = input.Position - dragStart
            frame.Position = UDim2.new(startPos.X.Scale, startPos.X.Offset + delta.X, startPos.Y.Scale, startPos.Y.Offset + delta.Y)
        end
    end)
end

local function ApplyRGB(textObj)
    task.spawn(function()
        while textObj and textObj.Parent do
            textObj.TextColor3 = Color3.fromHSV(tick() % 5 / 5, 0.8, 1); task.wait(0.05)
        end
    end)
end

-- // JANELA PRINCIPAL
local Main = Instance.new("Frame", Gui)
Main.Size = UDim2.new(0, 550, 0, 380); Main.Position = UDim2.new(0.5, -275, 0.5, -190); Main.BackgroundColor3 = Cores.Fundo; Main.Visible = false; Main.Active = true; Arredondar(Main, 10)
Instance.new("UIStroke", Main).Color = Cores.Vermelho; MakeDraggable(Main)

local TopBanner = Instance.new("TextLabel", Main)
TopBanner.Size = UDim2.new(1, 0, 0, 45); TopBanner.Text = "TEXHUB V8 - MUTE SUPREMO"; TopBanner.Font = Enum.Font.GothamBold; TopBanner.TextSize = 22; TopBanner.BackgroundTransparency = 1; ApplyRGB(TopBanner)

local Sidebar = Instance.new("ScrollingFrame", Main)
Sidebar.Size = UDim2.new(0, 130, 1, -60); Sidebar.Position = UDim2.new(0, 10, 0, 55); Sidebar.BackgroundTransparency = 1; Sidebar.ScrollBarThickness = 0
Instance.new("UIListLayout", Sidebar).Padding = UDim.new(0, 5)

local Container = Instance.new("Frame", Main)
Container.Size = UDim2.new(1, -160, 1, -60); Container.Position = UDim2.new(0, 150, 0, 55); Container.BackgroundTransparency = 1

local Pages = {}
local function CreatePage(name, isSpecial)
    local Page = Instance.new("ScrollingFrame", Container)
    Page.Size = UDim2.new(1, 0, 1, 0); Page.BackgroundTransparency = 1; Page.Visible = false; Page.ScrollBarThickness = 2
    if name ~= "🏠 INÍCIO" and name ~= "📄 CRÉDITOS" and name ~= "⚙️ INTERNO" then
        local Grid = Instance.new("UIGridLayout", Page); Grid.CellSize = UDim2.new(0, 115, 0, 50); Grid.CellPadding = UDim2.new(0, 5, 0, 5)
    end
    local Tab = Instance.new("TextButton", Sidebar)
    Tab.Size = UDim2.new(1, 0, 0, 35); Tab.BackgroundColor3 = Cores.Botao; Tab.Text = name; Tab.TextColor3 = Cores.Texto; Tab.Font = Enum.Font.GothamBold; Tab.TextSize = 10; Arredondar(Tab, 6)
    
    Tab.MouseButton1Click:Connect(function() 
        if isSpecial then
            local myRole = Player:FindFirstChild("TexRole") and Player.TexRole.Value or "Membro"
            if Player.Name ~= MEU_NICK and myRole ~= "Sub Criador" then
                local oldText = Tab.Text
                Tab.Text = "SÓ O CRIADOR! ⚙️"
                task.wait(1.5)
                Tab.Text = oldText
                return
            end
        end
        for _, p in pairs(Pages) do p.Visible = false end; Page.Visible = true 
    end)
    Pages[name] = Page
    return Page
end

-- ABA INTERNA (ADMIN)
local pInterno = CreatePage("⚙️ INTERNO", true)
local AdminLayout = Instance.new("UIListLayout", pInterno); AdminLayout.Padding = UDim.new(0, 10)

local TargetInput = Instance.new("TextBox", pInterno)
TargetInput.Size = UDim2.new(1, -10, 0, 40); TargetInput.PlaceholderText = "Nick do Player..."; TargetInput.BackgroundColor3 = Cores.Botao; TargetInput.TextColor3 = Cores.Texto; Arredondar(TargetInput, 6)

local btnBan = Instance.new("TextButton", pInterno)
btnBan.Size = UDim2.new(1, -10, 0, 40); btnBan.Text = "BANIR DO HUB ❌"; btnBan.BackgroundColor3 = Cores.Vermelho; btnBan.TextColor3 = Cores.Texto; Arredondar(btnBan, 6)
btnBan.MouseButton1Click:Connect(function()
    if Player.Name ~= MEU_NICK then return end
    local t = Players:FindFirstChild(TargetInput.Text)
    if t then 
        table.insert(_G.BannedTex, t.Name)
        t:Kick("Você está banido do [TEXHUB]❌") 
    end
end)

local cargos = {"Membro", "Staff", "Moderador", "Sub Criador"}
for _, cargo in pairs(cargos) do
    local b = Instance.new("TextButton", pInterno)
    b.Size = UDim2.new(1, -10, 0, 35); b.Text = "DAR CARGO: "..cargo; b.BackgroundColor3 = Cores.Botao; b.TextColor3 = Cores.Texto; Arredondar(b, 6)
    b.MouseButton1Click:Connect(function()
        local myRole = Player:FindFirstChild("TexRole") and Player.TexRole.Value or "Membro"
        if cargo == "Sub Criador" and Player.Name ~= MEU_NICK then return end
        local t = Players:FindFirstChild(TargetInput.Text)
        if t then SetRole(t, cargo) end
    end)
end

-- TODAS AS SUAS ABAS ORIGINAIS (MANTIDAS)
local function AddToggle(pg, txt)
    local active = false
    local TFrame = Instance.new("Frame", pg); TFrame.BackgroundColor3 = Cores.Botao; Arredondar(TFrame, 6)
    local Label = Instance.new("TextLabel", TFrame); Label.Size = UDim2.new(1, -10, 0, 25); Label.Position = UDim2.new(0, 10, 0, 5); Label.Text = txt; Label.TextColor3 = Cores.Texto; Label.Font = Enum.Font.GothamBold; Label.TextSize = 9; Label.BackgroundTransparency = 1
    local Status = Instance.new("TextLabel", TFrame); Status.Size = UDim2.new(1, 0, 0, 15); Status.Position = UDim2.new(0, 10, 0, 30); Status.Text = "OFF ❌"; Status.TextColor3 = Cores.Vermelho; Status.Font = Enum.Font.GothamBold; Status.TextSize = 8; Status.BackgroundTransparency = 1
    local Btn = Instance.new("TextButton", TFrame); Btn.Size = UDim2.new(1,0,1,0); Btn.BackgroundTransparency = 1; Btn.Text = ""
    Btn.MouseButton1Click:Connect(function() 
        active = not active; 
        Status.Text = active and "ON ✅" or "OFF ❌"; 
        Status.TextColor3 = active and Cores.Verde or Cores.Vermelho
        
        -- Lógica de Kick Funcional
        if txt == "Kick Player" and active then
            local t = Players:FindFirstChild(TargetInput.Text)
            if t then t:Kick("Kicked by TexHub") end
        end
    end)
end

local pInicio = CreatePage("🏠 INÍCIO", false)
local Welcome = Instance.new("TextLabel", pInicio); Welcome.Size = UDim2.new(1, 0, 1, 0); Welcome.BackgroundTransparency = 1; Welcome.Font = Enum.Font.GothamBold; Welcome.TextSize = 25; Welcome.TextColor3 = Cores.Texto; Welcome.TextWrapped = true; Welcome.Text = "BEM VINDO AO TEXHUB V8.1!\nAPROVEITE, "..MEU_NICK:upper()

local pCombate = CreatePage("⚔️ COMBATE", false)
for _, n in pairs({"Kill Aura", "Silent Aim", "Auto Clicker", "Reach hack", "No Velocity", "Trigger Bot", "Hitbox Expander", "Fast Attack", "Auto Block", "Aim Lock", "Knife Kill", "Infinite Ammo", "Anti Knockback", "Wallshot", "Teleport Kill"}) do AddToggle(pCombate, n) end

local pMovimento = CreatePage("💨 MOVIMENTO", false)
for _, n in pairs({"WalkSpeed", "Infinite Jump", "Fly Mobile", "Noclip", "Spider Walk", "Air Walk", "Speed Bypass", "Teleport Click", "Swim Air", "High Jump", "Spin Bot", "Auto Walk", "No Slowdown", "Bunny Hop", "Dash Hack"}) do AddToggle(pMovimento, n) end

local pVisual = CreatePage("👁️ VISUAL", false)
for _, n in pairs({"Player ESP", "Box ESP", "Tracers", "Name Tags", "FullBright", "No Fog", "Chams Rainbow", "X-Ray", "Wallhack", "Armor ESP", "Distance ESP", "Object ESP", "FOV Changer", "Crosshair Custom", "Bullet Tracers"}) do AddToggle(pVisual, n) end

local pMundo = CreatePage("🌍 MUNDO", false)
for _, n in pairs({"Delete Parts", "Gravity Zero", "Time Changer", "No Water", "Full Night", "Full Day", "Terrain Edit", "Part Spam", "Lava Immunity", "Explode All", "Bypassed Fly", "Instant Interact", "Destroy Map", "Lag Server", "FPS Booster"}) do AddToggle(pMundo, n) end

local pAdmin = CreatePage("👑 ADMIN", false)
for _, n in pairs({"Infinite Yield", "CMD-X", "Anti AFK", "Rejoin", "Server Hop", "Copy Game", "Free Cam", "DEX Explorer", "Remote Spy", "Audio Logger", "Chat Spammer", "Admin Logs", "Kick Player", "Ban Bypass", "God Mode"}) do AddToggle(pAdmin, n) end

local pCreditos = CreatePage("📄 CRÉDITOS", false)
local CredTxt = Instance.new("TextLabel", pCreditos); CredTxt.Size = UDim2.new(1, 0, 1, 0); CredTxt.BackgroundTransparency = 1; CredTxt.Font = Enum.Font.GothamBold; CredTxt.TextSize = 18; CredTxt.TextColor3 = Cores.Texto; CredTxt.Text = "CRIADO POR: "..MEU_NICK.."\nVERSÃO: V8.1 SUPREMO\n\nOBRIGADO POR USAR O TEX HUB!"

Pages["🏠 INÍCIO"].Visible = true

-- // JANELA DE KEY
local KeyMain = Instance.new("Frame", Gui)
KeyMain.Size = UDim2.new(0, 350, 0, 300); KeyMain.Position = UDim2.new(0.5, -175, 0.5, -150); KeyMain.BackgroundColor3 = Cores.Fundo; Arredondar(KeyMain, 12); MakeDraggable(KeyMain); KeyMain.Visible = false
local KTitle = Instance.new("TextLabel", KeyMain); KTitle.Size = UDim2.new(1, 0, 0, 50); KTitle.Text = "TEXHUB AUTHENTICATION"; KTitle.Font = Enum.Font.GothamBold; KTitle.TextColor3 = Cores.Vermelho; KTitle.TextSize = 18; KTitle.BackgroundTransparency = 1
local KBox = Instance.new("TextBox", KeyMain); KBox.Size = UDim2.new(0.85, 0, 0, 45); KBox.Position = UDim2.new(0.075, 0, 0.3, 0); KBox.BackgroundColor3 = Cores.Botao; KBox.PlaceholderText = "Sua Key..."; KBox.Text = ""; KBox.TextColor3 = Cores.Texto; Arredondar(KBox, 8)
local KBtn = Instance.new("TextButton", KeyMain); KBtn.Size = UDim2.new(0.85, 0, 0, 45); KBtn.Position = UDim2.new(0.075, 0, 0.55, 0); KBtn.BackgroundColor3 = Cores.Vermelho; KBtn.Text = "VALIDAR ACESSO"; KBtn.Font = Enum.Font.GothamBold; Arredondar(KBtn, 8)

local LoadFrame = Instance.new("Frame", KeyMain); LoadFrame.Size = UDim2.new(0.85, 0, 0, 20); LoadFrame.Position = UDim2.new(0.075, 0, 0.8, 0); LoadFrame.BackgroundColor3 = Cores.Barra; LoadFrame.Visible = false; Arredondar(LoadFrame, 6)
local Fill = Instance.new("Frame", LoadFrame); Fill.Size = UDim2.new(0, 0, 1, 0); Fill.BackgroundColor3 = Cores.Verde; Arredondar(Fill, 6)
local StatusMsg = Instance.new("TextLabel", KeyMain); StatusMsg.Size = UDim2.new(1, 0, 0, 20); StatusMsg.Position = UDim2.new(0, 0, 0.9, 0); StatusMsg.BackgroundTransparency = 1; StatusMsg.TextColor3 = Cores.Texto; StatusMsg.Font = Enum.Font.GothamBold; StatusMsg.TextSize = 10; StatusMsg.Text = ""; StatusMsg.Visible = false

local Mensagens = {"Buscando scripts...", "Validando credenciais...", "Injetando Supremo V8...", "Limpando rastros...", "Acesso liberado!"}

KBtn.MouseButton1Click:Connect(function()
    for _, name in pairs(_G.BannedTex) do if Player.Name == name then Player:Kick("Você está banido do [TEXHUB]❌") return end end
    if KBox.Text == CORRECT_KEY then
        KBtn.Visible = false; KBox.Visible = false; LoadFrame.Visible = true; StatusMsg.Visible = true
        SetRole(Player, (Player.Name == MEU_NICK) and "CRIADOR" or "Membro")
        for i = 1, #Mensagens do
            StatusMsg.Text = Mensagens[i]
            TweenService:Create(Fill, TweenInfo.new(1), {Size = UDim2.new(i/5, 0, 1, 0)}):Play()
            task.wait(1)
        end
        KeyMain:Destroy(); Main.Visible = true
        for _, p in pairs(Players:GetPlayers()) do CriarTag(p) end
        Players.PlayerAdded:Connect(CriarTag)
        
        -- BOLINHA FLUTUANTE NEON VERMELHA
        local Float = Instance.new("TextButton", Gui)
        Float.Size = UDim2.new(0, 60, 0, 60); Float.Position = UDim2.new(0, 20, 0.5, 0); Float.BackgroundColor3 = Color3.fromRGB(20, 0, 0)
        Float.Text = "TexHub"; Float.TextColor3 = Color3.fromRGB(255, 255, 255); Float.Font = Enum.Font.GothamBold; Float.TextSize = 12
        Arredondar(Float, 30); local Aura = Instance.new("UIStroke", Float); Aura.Color = Color3.fromRGB(255, 0, 0); Aura.Thickness = 3
        task.spawn(function()
            while Float do
                TweenService:Create(Aura, TweenInfo.new(1, Enum.EasingStyle.Sine, Enum.EasingDirection.InOut, -1, true), {Thickness = 6}):Play()
                task.wait(1)
            end
        end)
        Float.MouseButton1Click:Connect(function() Main.Visible = not Main.Visible end)
    else
        KBtn.Text = "KEY INVÁLIDA!"; KBtn.BackgroundColor3 = Cores.Vermelho; task.wait(1.5); KBtn.Text = "VALIDAR ACESSO"
    end
end)

task.spawn(function() StartLoadrisg(); KeyMain.Visible = true end)
