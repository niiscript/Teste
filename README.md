local button = script.Parent
local player = game:GetService("Players").LocalPlayer

-- Cria uma função para exibir mensagem na tela
local function showMessage(text)
	local msg = Instance.new("TextLabel")
	msg.Text = text
	msg.Size = UDim2.new(0, 300, 0, 50)
	msg.Position = UDim2.new(0.5, -150, 0.85, 0)
	msg.BackgroundColor3 = Color3.new(0, 0, 0)
	msg.TextColor3 = Color3.new(1, 1, 1)
	msg.TextScaled = true
	msg.Parent = player:WaitForChild("PlayerGui")
	
	-- Some após 3 segundos
	game:GetService("Debris"):AddItem(msg, 3)
end

button.MouseButton1Click:Connect(function()
	for _, gui in pairs(player.PlayerGui:GetChildren()) do
		if gui:IsA("ScreenGui") then
			for _, item in pairs(gui:GetDescendants()) do
				if item:IsA("TextLabel") and (item.Text == "Carrot Seed" or item.Text == "Strawberry Seed") then
					showMessage("Encontrado: " .. item.Text)
				end
			end
		end
	end
end)
