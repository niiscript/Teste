local Players = game:GetService("Players")
local player = Players.LocalPlayer
local character = player.Character or player.CharacterAdded:Wait()

local function encontrarSamCerto()
    local menorDistancia = math.huge
    local samCorreto = nil

    -- Tenta encontrar o botão SELL
    local sellButton = nil
    for _, gui in pairs(game:GetDescendants()) do
        if gui:IsA("TextButton") and gui.Text == "SELL" then
            sellButton = gui
            break
        end
    end

    if not sellButton then
        warn("Botão SELL não encontrado.")
        return
    end

    local sellPos = sellButton.AbsolutePosition

    -- Procura por todos NPCs Sam
    for _, model in pairs(game.Workspace:GetDescendants()) do
        if model:IsA("Model") and model:FindFirstChild("HumanoidRootPart") and model.Name == "Sam" then
            local npcPos = model.HumanoidRootPart.Position
            local dist = (npcPos - character:FindFirstChild("HumanoidRootPart").Position).Magnitude
            if dist < menorDistancia then
                menorDistancia = dist
                samCorreto = model
            end
        end
    end

    if samCorreto then
        print("Sam certo encontrado:", samCorreto.Name)
        -- Aqui você pode fazer ele ir até o NPC ou ativar o botão de Talk
    else
        warn("Nenhum Sam encontrado.")
    end
end

-- Cria um botão na tela
local btn = Instance.new("TextButton")
btn.Size = UDim2.new(0, 150, 0, 40)
btn.Position = UDim2.new(0.5, -75, 0.9, 0)
btn.BackgroundColor3 = Color3.fromRGB(100, 200, 100)
btn.Text = "Encontrar NPC Sam"
btn.Parent = game.Players.LocalPlayer:WaitForChild("PlayerGui")

btn.MouseButton1Click:Connect(encontrarSamCerto)
