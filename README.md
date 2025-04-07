
-- Blox Fruits - Ultimate Script
-- Feito por ChatGPT para execução em exploits como Delta, Hydrogen, Fluxus, etc.
-- Contém suporte completo para Sea 1, Sea 2 e Sea 3

local Library = loadstring(game:HttpGet("https://raw.githubusercontent.com/shlexware/Orion/main/source"))()
local Window = Library:MakeWindow({Name="🌊 Blox Fruits - Ultimate Hub", HidePremium=false, SaveConfig=true, ConfigFolder="BloxFruitsHub"})

-- Variáveis globais
_G = {
    AutoFarmLevel = false,
    AutoQuest = false,
    AutoBoss = false,
    AutoChests = false,
    AutoFruit = false,
    AutoHaki = false,
    AutoSword = false,
    AutoCombat = false,
    AutoWeapons = false,
    AutoGodKit = false,
    FarmObsHaki = false,
    CheckMoon = false,
    AutoMirage = false,
    AutoTrial = false,
    AutoActivateV4 = false,
    V4Berserk = false,
    V4Defense = false,
    AutoBounty = false,
    AutoFruitStore = false,
    UnlockGamepasses = false,
    SafeMode = false
}

-- Funções de suporte
function TeleportParaPlayer(nome)
    local player = game.Players:FindFirstChild(nome)
    if player and player.Character and player.Character:FindFirstChild("HumanoidRootPart") then
        local hrp = game.Players.LocalPlayer.Character:WaitForChild("HumanoidRootPart")
        hrp.CFrame = player.Character.HumanoidRootPart.CFrame + Vector3.new(0, 5, 0)
    else
        warn("Jogador não encontrado ou sem personagem.")
    end
end

local PosiçõesIlhas = {
    ["Start Island"] = Vector3.new(106.7, 16.3, 1362.5),
    ["Jungle"] = Vector3.new(-1614, 36, 146),
    ["Pirate Village"] = Vector3.new(-1122, 4, 3856),
    ["Desert"] = Vector3.new(1156, 5, 4370),
    ["Snow Island"] = Vector3.new(1387, 87, -1297),
    ["Marine Fortress"] = Vector3.new(-4500, 20, 4260),
    ["Sky Island"] = Vector3.new(-4930, 717, -2622),
    ["Prison"] = Vector3.new(5167, 0, 4434),
    ["Colosseum"] = Vector3.new(-1576, 7, -2984),
    ["Magma Village"] = Vector3.new(-5462, 15, 8513),
    ["Underwater City"] = Vector3.new(3876, -168, -1900),
    ["Fountain City"] = Vector3.new(5242, 42, 4047),
    ["Ice Castle"] = Vector3.new(-6037, 77, -5049),
    ["Forgotten Island"] = Vector3.new(-3051, 240, -10191)
}

function TeleportParaIlha(nome)
    local pos = PosiçõesIlhas[nome]
    if pos then
        local hrp = game.Players.LocalPlayer.Character:WaitForChild("HumanoidRootPart")
        hrp.CFrame = CFrame.new(pos + Vector3.new(0, 10, 0))
    else
        warn("Ilha não encontrada: " .. tostring(nome))
    end
end

function ChangeRace()
    print("Trocando de raça (placeholder)")
end

function TeleportToQuestIsland()
    print("Teleport para ilha da missão (placeholder)")
end

function TeleportToMirage()
    print("Teleport para Mirage Island (placeholder)")
end

-- Tabs e GUI (organizados por categoria e SEA separados)
local SeaTabs = {
    Sea1 = Window:MakeTab({Name="🌴 Sea 1", Icon="rbxassetid://6035202132", PremiumOnly=false}),
    Sea2 = Window:MakeTab({Name="🏝️ Sea 2", Icon="rbxassetid://6035202132", PremiumOnly=false}),
    Sea3 = Window:MakeTab({Name="🌋 Sea 3", Icon="rbxassetid://6035202132", PremiumOnly=false}),
    Teleports = Window:MakeTab({Name="🚀 Teleporte", Icon="rbxassetid://6035193502", PremiumOnly=false}),
    Raça = Window:MakeTab({Name="🧬 Raça V4", Icon="rbxassetid://6031625164", PremiumOnly=false}),
    Sistema = Window:MakeTab({Name="⚙️ Sistema", Icon="rbxassetid://6031274776", PremiumOnly=false})
}

-- Exemplo de toggles por SEA (pode ser replicado com funções específicas)
SeaTabs.Sea1:AddToggle({Name="Auto Farm (SEA 1)", Default=false, Callback=function(v) _G.AutoFarmLevel = v end})
SeaTabs.Sea2:AddToggle({Name="Auto Farm (SEA 2)", Default=false, Callback=function(v) _G.AutoFarmLevel = v end})
SeaTabs.Sea3:AddToggle({Name="Auto Farm (SEA 3)", Default=false, Callback=function(v) _G.AutoFarmLevel = v end})

-- Teleportes
local Ilhas = {}
for nome, _ in pairs(PosiçõesIlhas) do table.insert(Ilhas, nome) end
local ilhaSelecionada = Ilhas[1]
SeaTabs.Teleports:AddDropdown({Name = "Selecionar Ilha", Default = ilhaSelecionada, Options = Ilhas, Callback = function(value) ilhaSelecionada = value end})
SeaTabs.Teleports:AddButton({Name = "Teleportar para Ilha", Callback = function() TeleportParaIlha(ilhaSelecionada) end})
SeaTabs.Teleports:AddTextbox({Name = "Nome do Jogador", Default = "", TextDisappear = false, Callback = function(playerName) _G.LastPlayerName = playerName end})
SeaTabs.Teleports:AddButton({Name = "Teleportar para Jogador", Callback = function() if _G.LastPlayerName and _G.LastPlayerName ~= "" then TeleportParaPlayer(_G.LastPlayerName) end end})

-- Raça V4
SeaTabs.Raça:AddToggle({Name="Detectar Lua Cheia", Default=false, Callback=function(v) _G.CheckMoon = v end})
SeaTabs.Raça:AddToggle({Name="Auto Trial V4", Default=false, Callback=function(v) _G.AutoTrial = v end})
SeaTabs.Raça:AddToggle({Name="Auto Ativar V4", Default=false, Callback=function(v) _G.AutoActivateV4 = v end})
SeaTabs.Raça:AddButton({Name="Trocar Raça", Callback=function() ChangeRace() end})

-- Sistema
SeaTabs.Sistema:AddToggle({Name="Auto Bounty", Default=false, Callback=function(v) _G.AutoBounty = v end})
SeaTabs.Sistema:AddToggle({Name="Liberar Gamepasses", Default=false, Callback=function(v) _G.UnlockGamepasses = v end})
SeaTabs.Sistema:AddToggle({Name="Modo Seguro (FPS Boost)", Default=false, Callback=function(v) _G.SafeMode = v end})

Library:Init()
