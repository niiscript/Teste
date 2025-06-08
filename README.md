local player = game.Players.LocalPlayer

-- Criar GUI
local gui = Instance.new("ScreenGui", player:WaitForChild("PlayerGui"))
gui.Name = "ExplorerGUI"

local button = Instance.new("TextButton")
button.Size = UDim2.new(0, 300, 0, 50)
button.Position = UDim2.new(0, 50, 0, 200)
button.Text = "Detectar Tudo"
button.BackgroundColor3 = Color3.fromRGB(255, 200, 0)
button.TextScaled = true
button.Parent = gui

-- Explora o jogo inteiro
button.MouseButton1Click:Connect(function()
    local sources = {
        workspace,
        game.ReplicatedStorage,
        game:GetService("StarterGui"),
        game:GetService("Players"),
        game:GetService("StarterPack"),
    }

    local found = {}

    for _, container in pairs(sources) do
        for _, obj in pairs(container:GetChildren()) do
            table.insert(found, container.Name .. "/" .. obj.Name)
        end
    end

    local list = table.concat(found, ", ")
    print("Detectados:", list)
    button.Text = found[1] and "Achou: " .. found[1] or "Nada encontrado"
end)
