-- Script para ambiente espacial (esp) em Roblox

-- Defina as variáveis de configuração
local espName = "Meu Esp"
local espDescription = "Um espaço para explorar"

-- Crie o objeto do esp
local esp = Instance.new("Model")
esp.Name = espName
esp.Description = espDescription

-- Adicione a descrição do esp
local descriptionLabel = Instance.new("TextLabel")
descriptionLabel.Parent = esp
descriptionLabel.Text = espDescription
descriptionLabel.Size = UDim2.new(1, 0, 0, 100)

-- Adicione um objeto para o jogador se posicionar
local playerPosition = Instance.new("Part")
playerPosition.Parent = esp
playerPosition.Size = Vector3.new(1, 1, 1)
playerPosition.Position = Vector3.new(0, 5, 0)

-- Adicione um objeto para o jogador se mover
local playerMovement = Instance.new("Part")
playerMovement.Parent = esp
playerMovement.Size = Vector3.new(1, 1, 1)
playerMovement.Position = Vector3.new(0, 5, 0)
playerMovement.Anchored = false

-- Adicione um objeto para o jogador olhar
local playerView = Instance.new("Part")
playerView.Parent = esp
playerView.Size = Vector3.new(1, 1, 1)
playerView.Position = Vector3.new(0, 5, 0)
playerView.Anchored = false

-- Adicione um script para a movimentação do jogador
local playerMovementScript = Instance.new("Script")
playerMovementScript.Parent = playerMovement
playerMovementScript.Source = [[
    local player = game.Players.LocalPlayer
    local character = player.Character
    local humanoidRootPart = character:WaitForChild("HumanoidRootPart")

    while true do
        local userInputService = game:GetService("UserInputService")
        local movementInput = userInputService:GetMouseDelta()

        local movementX = movementInput.X
        local movementZ = movementInput.Y

        local movementVector = Vector3.new(movementX, 0, movementZ)
        humanoidRootPart.CFrame = humanoidRootPart.CFrame * CFrame.new(movementVector)
    end
]]

-- Adicione um script para a visão do jogador
local playerViewScript = Instance.new("Script")
playerViewScript.Parent = playerView
playerViewScript.Source = [[
    local player = game.Players.LocalPlayer
    local character = player.Character
    local humanoidRootPart = character:WaitForChild("HumanoidRootPart")

    while true do
        local userInputService = game:GetService("UserInputService")
        local viewInput = userInputService:GetMouseDelta()

        local viewX = viewInput.X
        local viewZ = viewInput.Y

        local viewVector = Vector3.new(viewX, 0, viewZ)
        humanoidRootPart.CFrame = humanoidRootPart.CFrame * CFrame.new(viewVector)
    end
]]

-- Adicione um script para a interação do jogador com o ambiente
local playerInteractionScript = Instance.new("Script")
playerInteractionScript.Parent = esp
playerInteractionScript.Source = [[
    local player = game.Players.LocalPlayer
    local character = player.Character
    local humanoidRootPart = character:WaitForChild("HumanoidRootPart")

    while true do
        local userInputService = game:GetService("UserInputService")
        local interactionInput = userInputService:GetMouseDelta()

        local interactionVector = Vector3.new(interactionInput.X, 0, interactionInput.Y)
        if interactionVector.magnitude > 1 then
            local target = game.Workspace:FindFirstChild("Target")
            if target then
                target.CFrame = humanoidRootPart.CFrame * CFrame.new(interactionVector)
            end
        end
    end
]]

-- Adicione um script para a lógica do ambiente
local ambienteLogicScript = Instance.new("Script")
ambienteLogicScript.Parent = esp
ambienteLogicScript.Source = [[
    local esp = game.Workspace:WaitForChild("Meu Esp")

    while true do
        local targets = esp:FindDescendantsByTag("Target")
        for _, target in pairs(targets) do
            local humanoidRootPart = target.Parent:WaitForChild("HumanoidRootPart")
            local movementVector = humanoidRootPart.CFrame.lookVector * 5
            target.CFrame = target.CFrame + CFrame.new(movementVector)
        end
    end
]]
