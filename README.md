local player = game.Players.LocalPlayer

-- Criar GUI
local gui = Instance.new("ScreenGui", player:WaitForChild("PlayerGui"))
gui.Name = "ExplorerGUI"

local button = Instance.new("TextButton")
button.Size = UDim2.new(0, 300, 0, 50)
button.Position = UDim2.new(0, 50, 0, 200)
button.Text = "Detectar Objetos"
button.BackgroundColor3 = Color3.fromRGB(0, 255, 100)
button.TextScaled = true
button.Parent = gui

-- Quando clicar, lista os objetos
button.MouseButton1Click:Connect(function()
    local result = {}
    for _, obj in pairs(workspace:GetChildren()) do
        table.insert(result, obj.Name)
    end

    -- Mostrar primeiros nomes no botão
    local list = table.concat(result, ", ")
    print("Objetos no workspace:", list)
    button.Text = result[1] and "Achou: " .. result[1] or "Nada encontrado"
end)
