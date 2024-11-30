=-- Inicialização
local Players = game:GetService("Players")
local admins = {
    ["NomeDoJogador1"] = true,
    ["NomeDoJogador2"] = true
}

-- Função para checar se o jogador é um administrador
local function isAdmin(player)
    return admins[player.Name] == true
end

-- Comando de teletransporte
local function teleportTo(player, targetPlayer)
    if targetPlayer and targetPlayer.Character and targetPlayer.Character:FindFirstChild("HumanoidRootPart") then
        player.Character.HumanoidRootPart.CFrame = targetPlayer.Character.HumanoidRootPart.CFrame
    end
end

-- Comando para alterar a velocidade de movimento
local function changeWalkSpeed(player, speed)
    if player.Character and player.Character:FindFirstChild("Humanoid") then
        player.Character.Humanoid.WalkSpeed = speed
    end
end

-- Evento quando o jogador entra no jogo
Players.PlayerAdded:Connect(function(player)
    if isAdmin(player) then
        player.Chatted:Connect(function(message)
            local args = message:split(" ")
            local command = args[1]:lower()
            if command == "!tp" then
                local targetPlayerName = args[2]
                local targetPlayer = Players:FindFirstChild(targetPlayerName)
                if targetPlayer then
                    teleportTo(player, targetPlayer)
                end
            elseif command == "!speed" then
                local speed = tonumber(args[2])
                if speed then
                    changeWalkSpeed(player, speed)
                end
            end
        end)
    end
end)
