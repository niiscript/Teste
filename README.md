local Players = game:GetService("Players")
local player = Players.LocalPlayer
local function comprarSementesComuns()
	local gui = player:WaitForChild("PlayerGui")
	
	-- Procurar a interface da loja
	for _, interface in pairs(gui:GetChildren()) do
		if interface:IsA("ScreenGui") and interface:FindFirstChildWhichIsA("Frame", true) then
			-- Procurar pelos itens da loja
			for _, item in pairs(interface:GetDescendants()) do
				if item:IsA("TextLabel") and (item.Text == "Carrot Seed" or item.Text == "Strawberry Seed") then
					local container = item.Parent

					-- Verificar se tem estoque
					local stock = container:FindFirstChildWhichIsA("TextLabel", true)
					if stock and stock.Text:find("Stock") then
						
						-- Procurar botão com preço em ¢
						for _, botao in pairs(container:GetDescendants()) do
							if botao:IsA("TextButton") and botao.Text:match("¢") then
								print("Comprando:", item.Text)
								botao:Activate()
							end
						end
					end
				end
			end
		end
	end
end

-- Chamar a função
comprarSementesComuns()
