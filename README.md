local button = script.Parent
local player = game:GetService("Players").LocalPlayer

button.MouseButton1Click:Connect(function()
	local count = 0

	for _, obj in pairs(workspace:GetDescendants()) do
		if obj:IsA("Model") and obj:FindFirstChildWhichIsA("Humanoid") then
			count += 1

			local label = Instance.new("TextLabel")
			label.Size = UDim2.new(0, 350, 0, 30)
			label.Position = UDim2.new(0, 10, 0, 10 + (count * 35))
			label.Text = "NPC: " .. obj.Name .. " (" .. obj:GetFullName() .. ")"
			label.TextColor3 = Color3.new(1, 1, 1)
			label.BackgroundColor3 = Color3.new(0, 0, 0)
			label.TextScaled = true
			label.Parent = player:WaitForChild("PlayerGui")
			
			game:GetService("Debris"):AddItem(label, 6)
		end
	end

	if count == 0 then
		local noNPC = Instance.new("TextLabel")
		noNPC.Size = UDim2.new(0, 300, 0, 50)
		noNPC.Position = UDim2.new(0.5, -150, 0.5, -25)
		noNPC.Text = "Nenhum NPC encontrado!"
		noNPC.TextColor3 = Color3.new(1, 0, 0)
		noNPC.BackgroundColor3 = Color3.new(0, 0, 0)
		noNPC.TextScaled = true
		noNPC.Parent = player:WaitForChild("PlayerGui")
		
		game:GetService("Debris"):AddItem(noNPC, 3)
	end
end)
