-- WL AFK Hub | by willgamesyt

-- Proteções básicas
if not game:IsLoaded() then game.Loaded:Wait() end
pcall(function() setfpscap(100) end)

-- Efeito de carregamento
local function showLoading()
    local loadingGui = Instance.new("ScreenGui")
    loadingGui.Name = "LoadingGui"
    loadingGui.ResetOnSpawn = false
    loadingGui.IgnoreGuiInset = true
    loadingGui.ZIndexBehavior = Enum.ZIndexBehavior.Sibling
    loadingGui.Parent = game:GetService("CoreGui")

    local frame = Instance.new("Frame")
    frame.Size = UDim2.new(0, 300, 0, 100)
    frame.Position = UDim2.new(0.5, -150, 0.5, -50)
    frame.BackgroundColor3 = Color3.fromRGB(25, 25, 25)
    frame.BorderSizePixel = 0
    frame.Parent = loadingGui

    local text = Instance.new("TextLabel")
    text.Size = UDim2.new(1, 0, 1, 0)
    text.BackgroundTransparency = 1
    text.Text = "Carregando WL AFK Hub..."
    text.TextColor3 = Color3.fromRGB(255, 255, 255)
    text.TextScaled = true
    text.Font = Enum.Font.SourceSansBold
    text.Parent = frame

    wait(2)
    loadingGui:Destroy()
end

showLoading()

-- UI Library
local OrionLib = loadstring(game:HttpGet("https://raw.githubusercontent.com/shlexware/Orion/main/source"))()

local Window = OrionLib:MakeWindow({
    Name = "🌑 WL AFK Hub 🌑",
    HidePremium = false,
    SaveConfig = true,
    ConfigFolder = "WLAfkHub",
    IntroText = "Solo Leveling Power",
    IntroIcon = "rbxassetid://14384894792"
})

-- Variáveis
local selectedIsland = "Ilha 1"
local clickMode = "Normal"
local ranks = {"E", "D", "C", "B", "A", "S"}
local selectedRank = "C"

-- Aba AFK
local TabAFK = Window:MakeTab({Name = "AFK / AutoClick", Icon = "rbxassetid://6034987532", PremiumOnly = false})
TabAFK:AddDropdown({
    Name = "Modo de AutoClick",
    Default = "Normal",
    Options = {"Normal", "Intermediário", "Potente"},
    Callback = function(v) clickMode = v end
})
TabAFK:AddButton({Name = "Ativar AutoClick", Callback = function()
    local delayTime = (clickMode == "Normal" and 1) or (clickMode == "Intermediário" and 0.2) or 0.05
    while true do
        task.wait(delayTime)
        mouse1click()
    end
end})
TabAFK:AddButton({Name = "Dar ARISE nas sombras", Callback = function()
    -- Código de ARISE
end})
TabAFK:AddButton({Name = "Destruir sombras", Callback = function()
    -- Código de destruir sombras
end})

-- Aba Farm de Money
local TabFarm = Window:MakeTab({Name = "Farm Money", Icon = "rbxassetid://6035067836", PremiumOnly = false})
TabFarm:AddDropdown({
    Name = "Selecionar Ilha",
    Default = "Ilha 1",
    Options = {"Ilha 1", "Ilha 2", "Ilha 3", "Ilha 4", "Ilha 5", "Ilha 6"},
    Callback = function(v) selectedIsland = v end
})
TabFarm:AddToggle({
    Name = "Farmar NPCs da ilha",
    Default = false,
    Callback = function(v)
        while v do
            -- Detecção da Ilha do Gelo (exemplo)
            if game:GetService("Workspace"):FindFirstChild("GeloRaid") then break end
            -- Código para atacar NPCs grandes e pequenos da selectedIsland
            task.wait(0.2)
        end
    end
})

-- Aba Raid do Gelo
local TabGelo = Window:MakeTab({Name = "Raid do Gelo", Icon = "rbxassetid://6031075938", PremiumOnly = false})
TabGelo:AddToggle({
    Name = "Ativar Raid do Gelo",
    Default = true,
    Callback = function(v)
        while v do
            -- Código para teleportar e matar os NPCs da Raid do Gelo
            task.wait(0.2)
        end
    end
})

-- Aba Raids
local TabRaids = Window:MakeTab({Name = "Raids", Icon = "rbxassetid://6035193183", PremiumOnly = false})
TabRaids:AddDropdown({
    Name = "Selecionar Rank da Raid",
    Default = "C",
    Options = ranks,
    Callback = function(v) selectedRank = v end
})
TabRaids:AddToggle({
    Name = "Fazer Raids automaticamente",
    Default = false,
    Callback = function(v)
        while v do
            -- Teleporta para os NPCs e ativa kill aura
            task.wait(0.2)
        end
    end
})

-- Aba Vender / Trocar
local TabTrocar = Window:MakeTab({Name = "Vender / Trocar", Icon = "rbxassetid://6031154879", PremiumOnly = false})
TabTrocar:AddDropdown({
    Name = "Selecionar Rank para vender",
    Default = "C",
    Options = ranks,
    Callback = function(v) selectedRank = v end
})
TabTrocar:AddButton({Name = "Vender Sombras", Callback = function()
    -- Código para vender sombras do rank selecionado
end})
TabTrocar:AddButton({Name = "Trocar Pós Comuns", Callback = function()
    -- Código para trocar pós comuns
end})
TabTrocar:AddButton({Name = "Trocar Pós Raros", Callback = function()
    -- Código para trocar pós raros
end})
TabTrocar:AddButton({Name = "Trocar Pós Lendários", Callback = function()
    -- Código para trocar pós lendários
end})

-- Inicializar a interface
OrionLib:Init()
