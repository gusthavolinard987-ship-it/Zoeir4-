-- Carregar a UI library
local redzlib = loadstring(game:HttpGet("https://raw.githubusercontent.com/tbao143/Library-ui/refs/heads/main/Redzhubui"))()

-- Criar a janela principal (Zoeir4 hub)
local Window = redzlib:MakeWindow({
    Title = "Zoeir4 hub",
    SubTitle = "by Xzbrian_darkzX",
    SaveFolder = "Zoeir4Hub | redz lib v5.lua"
})

-- Ícone de minimizar com imagem ajustada
Window:AddMinimizeButton({
    Button = { Image = "rbxassetid://18751483361", BackgroundTransparency = 0 },
    Corner = { CornerRadius = UDim.new(35, 1) },
})

-- Criar a primeira aba (DISCORD)
local DiscordTab = Window:MakeTab({ Name = "💬 DISCORD", Icon = "rbxassetid://7734053495" })

-- Auto copiar link ao executar
setclipboard("https://discord.gg/Cvy8kXcc")

-- Botão para copiar o link do servidor
DiscordTab:AddButton({
    Name = "Copiar Link do Servidor",
    Callback = function()
        setclipboard("https://discord.gg/Cvy8kXcc")
    end
})

-- Criar a aba Cliente
local Tab = Window:MakeTab({ Name = "👤 Cliente", Icon = "rbxassetid://7733674079" })

-- Variáveis padrão
local SpeedValue = 16 -- velocidade padrão
local JumpValue = 50  -- pulo padrão

-- Função que atualiza a velocidade
local function setSpeed(value)
    SpeedValue = value
    local plr = game.Players.LocalPlayer
    if plr and plr.Character and plr.Character:FindFirstChild("Humanoid") then
        plr.Character.Humanoid.WalkSpeed = SpeedValue
    end
end

-- Função que atualiza o pulo
local function setJump(value)
    JumpValue = value
    local plr = game.Players.LocalPlayer
    if plr and plr.Character and plr.Character:FindFirstChild("Humanoid") then
        plr.Character.Humanoid.JumpPower = JumpValue
    end
end

-- Slider para ajustar a velocidade
Tab:AddSlider({
    Name = "Velocidade",
    Min = 16,  -- padrão
    Max = 200, -- limite
    Default = 16,
    Increment = 1,
    Callback = function(Value)
        setSpeed(Value)
    end
})

-- Botão para resetar a velocidade
Tab:AddButton({
    Name = "Resetar Velocidade",
    Callback = function()
        setSpeed(16)
    end
})

-- Slider para ajustar o pulo
Tab:AddSlider({
    Name = "Pulo",
    Min = 50,   -- padrão Roblox
    Max = 500,  -- limite
    Default = 50,
    Increment = 5,
    Callback = function(Value)
        setJump(Value)
    end
})

-- Botão para resetar o pulo
Tab:AddButton({
    Name = "Resetar Pulo",
    Callback = function()
        setJump(50)
    end
})

-- ===== Noclip =====
local RunService = game:GetService("RunService")
local player = game.Players.LocalPlayer
local noclip = false

Tab:AddToggle({
    Name = "Noclip",
    Default = false,
    Callback = function(Value)
        noclip = Value
        game.StarterGui:SetCore("SendNotification", {
            Title = "Zoeir4 hub",
            Text = noclip and "Noclip ON" or "Noclip OFF",
            Duration = 3
        })
    end
})

RunService.Stepped:Connect(function()
    if noclip and player.Character then
        for _, part in pairs(player.Character:GetDescendants()) do
            if part:IsA("BasePart") and part.CanCollide then
                part.CanCollide = false
            end
        end
    end
end)

-- ===== Fly (executa script externo) =====
Tab:AddButton({
    Name = "Fly V3",
    Callback = function()
        loadstring(game:HttpGet("https://rawscripts.net/raw/Universal-Script-Fly-V3-48359"))()
    end
})

-- Mostrar bio "user Zoeir4 hub" ao entrar no jogo (móvel)
local gui = Instance.new("ScreenGui")
gui.Name = "Zoeir4HubBio"
gui.Parent = player:WaitForChild("PlayerGui")

local label = Instance.new("TextLabel")
label.Parent = gui
label.Size = UDim2.new(0, 200, 0, 50)
label.Position = UDim2.new(0.5, -100, 0.1, 0) -- posição inicial
label.BackgroundTransparency = 0.3
label.BackgroundColor3 = Color3.fromRGB(0, 0, 0)
label.TextColor3 = Color3.fromRGB(255, 255, 255)
label.TextScaled = true
label.Font = Enum.Font.GothamBold
label.Text = "user Zoeir4 hub"
label.TextStrokeTransparency = 0.2
label.Active = true
label.Draggable = true -- deixa o label móvel

-- Nova aba CASA
local CasaTab = Window:MakeTab({ Name = "🔨 Casa", Icon = "rbxassetid://7733960981" })

-- Botão UNBAN (Noclip) na aba Casa
local casaNoclip = false
CasaTab:AddButton({
    Name = "UNBAN (Noclip)",
    Callback = function()
        casaNoclip = not casaNoclip
        game.StarterGui:SetCore("SendNotification", {
            Title="Zoeir4 hub",
            Text = casaNoclip and "Noclip ON" or "Noclip OFF",
            Duration=3
        })
    end
})

RunService.Stepped:Connect(function()
    if casaNoclip and player.Character then
        for _, part in pairs(player.Character:GetDescendants()) do
            if part:IsA("BasePart") and part.CanCollide then
                part.CanCollide = false
            end
        end
    end
end)

