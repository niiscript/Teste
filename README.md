-- Variável de controle
local autoBuyEnabled = true

-- Criar botão na tela
local player = game.Players.LocalPlayer
local gui = Instance.new("ScreenGui", player:WaitForChild("PlayerGui"))
gui.Name = "AutoBuyTestGUI"

local button = Instance.new("TextButton")
button.Size = UDim2.new(0, 220, 0, 50)
button.Position = UDim2.new(0, 50, 0, 100)
button.Text = "Auto-Buy: ON (Common Test)"
button.BackgroundColor3 = Color3.fromRGB(0, 150, 255)
button.TextScaled = true
button.Parent = gui

-- Botão ON/OFF
button.MouseButton1Click:Connect(function()
    autoBuyEnabled = not autoBuyEnabled
    button.Text = autoBuyEnabled and "Auto-Buy: ON (Common Test)" or "Auto-Buy: OFF"
    button.BackgroundColor3 = autoBuyEnabled and Color3.fromRGB(0, 150, 255) or Color3.fromRGB(100, 100, 100)
end)

-- Função de compra automática
task.spawn(function()
    while true do
        if autoBuyEnabled then
            local shop = workspace:FindFirstChild("SEEDS")
            if shop then
                for _, seed in pairs(shop:GetChildren()) do
                    if seed:IsA("Model") then
                        local stockObj = seed:FindFirstChild("Stock")
                        local priceObj = seed:FindFirstChild("Price")
                        local buyPart = seed:FindFirstChild("Buy")

                        if stockObj and priceObj and buyPart then
                            local stock = tonumber(stockObj.Value:match("%d+")) or 0
                            local priceText = priceObj.Value
                            local price = tonumber(priceText:gsub(",", ""):match("%d+")) or math.huge
                            local money = player.leaderstats and player.leaderstats:FindFirstChild("Money") and player.leaderstats.Money.Value or 0

                            if stock > 0 and money >= price then
                                fireclickdetector(buyPart:FindFirstChildOfClass("ClickDetector"))
                                button.Text = "Bought: " .. seed.Name
                                task.wait(0.5)
                                button.Text = "Auto-Buy: ON (Common Test)"
                            end
                        end
                    end
                end
            end
        end
        task.wait(2)
    end
end)
