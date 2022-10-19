local Duolingo = Instance.new("ScreenGui")
local bar = Instance.new("Frame")
local icon = Instance.new("ImageLabel")
local title = Instance.new("TextLabel")
local Background = Instance.new("Frame")
local money = Instance.new("TextButton")
local UICorner = Instance.new("UICorner")
local bodysuit = Instance.new("TextButton")
local UICorner_2 = Instance.new("UICorner")
local cap = Instance.new("TextButton")
local UICorner_3 = Instance.new("UICorner")
local TextLabel = Instance.new("TextLabel")

Duolingo.Name = "ทำโดยกริชสุดหล่อ"
Duolingo.Parent = game.CoreGui
Duolingo.Enabled = true
Duolingo.ZIndexBehavior = Enum.ZIndexBehavior.Sibling

bar.Name = "bar"
bar.Parent = Duolingo
bar.BackgroundColor3 = Color3.fromRGB(255, 0, 0)
bar.BorderSizePixel = 0
bar.Position = UDim2.new(0.458333343, 0, 0.307550639, 0)
bar.Size = UDim2.new(0, 316, 0, 25)

icon.Name = "icon"
icon.Parent = bar
icon.BackgroundColor3 = Color3.fromRGB(255, 255, 255)
icon.BackgroundTransparency = 1.000
icon.Position = UDim2.new(0.0221518986, 0, 0.159999996, 0)
icon.Size = UDim2.new(0, 18, 0, 17)
icon.Image = "rbxassetid://10585839033"

title.Name = "title"
title.Parent = bar
title.BackgroundColor3 = Color3.fromRGB(255, 255, 255)
title.BackgroundTransparency = 1.000
title.Position = UDim2.new(0.183544308, 0, 0.159999996, 0)
title.Size = UDim2.new(0, 200, 0, 17)
title.Font = Enum.Font.GothamBold
title.Text = "สคริปแมพ   duolingo ทำโดยZeRex#"
title.TextColor3 = Color3.fromRGB(255, 255, 255)
title.TextScaled = true
title.TextSize = 14.000
title.TextWrapped = true

Background.Name = "Background"
Background.Parent = bar
Background.BackgroundColor3 = Color3.fromRGB(0, 0, 0)
Background.BorderSizePixel = 0
Background.Position = UDim2.new(-0.0030837059, 0, 0.978858173, 0)
Background.Size = UDim2.new(0, 316, 0, 203)

money.Name = "เงิน"
money.Parent = Background
money.BackgroundColor3 = Color3.fromRGB(255, 69, 0)
money.Position = UDim2.new(0.0221518986, 0, 0.0443349741, 0)
money.Size = UDim2.new(0, 106, 0, 21)
money.Font = Enum.Font.SourceSans
money.Text = "เสกเงิน"
money.TextColor3 = Color3.fromRGB(255, 255, 255)
money.TextSize = 14.000

UICorner.Parent = money

bodysuit.Name = "ชุด"
bodysuit.Parent = Background
bodysuit.BackgroundColor3 = Color3.fromRGB(255, 69, 0)
bodysuit.Position = UDim2.new(0.632911325, 0, 0.0443349741, 0)
bodysuit.Size = UDim2.new(0, 106, 0, 21)
bodysuit.Font = Enum.Font.SourceSans
bodysuit.Text = "ซื้อชุด"
bodysuit.TextColor3 = Color3.fromRGB(255, 255, 255)
bodysuit.TextSize = 14.000

UICorner_2.Parent = bodysuit

cap.Name = "หมวก"
cap.Parent = Background
cap.BackgroundColor3 = Color3.fromRGB(255, 69, 0)
cap.Position = UDim2.new(0.0221518986, 0, 0.197044343, 0)
cap.Size = UDim2.new(0, 106, 0, 21)
cap.Font = Enum.Font.SourceSans
cap.Text = "ซื้อหมวก"
cap.TextColor3 = Color3.fromRGB(255, 255, 255)
cap.TextSize = 14.000

UICorner_3.Parent = cap

TextLabel.Parent = Background
TextLabel.BackgroundColor3 = Color3.fromRGB(255, 255, 255)
TextLabel.BackgroundTransparency = 1.000
TextLabel.Position = UDim2.new(0.0221518986, 0, 0.881773412, 0)
TextLabel.Size = UDim2.new(0, 106, 0, 18)
TextLabel.Font = Enum.Font.SourceSans
TextLabel.Text = "f - เปิด/ปิด Menu"
TextLabel.TextColor3 = Color3.fromRGB(255, 255, 255)
TextLabel.TextSize = 14.000
TextLabel.TextXAlignment = Enum.TextXAlignment.Left
TextLabel.TextYAlignment = Enum.TextYAlignment.Bottom


-------

-- DRAG GUI --

local UserInputService = game:GetService("UserInputService")

local gui = bar

local dragging
local dragInput
local dragStart
local startPos

local function update(input)
	local delta = input.Position - dragStart
	gui.Position = UDim2.new(startPos.X.Scale, startPos.X.Offset + delta.X, startPos.Y.Scale, startPos.Y.Offset + delta.Y)
end

gui.InputBegan:Connect(function(input)
	if input.UserInputType == Enum.UserInputType.MouseButton1 or input.UserInputType == Enum.UserInputType.Touch then
		dragging = true
		dragStart = input.Position
		startPos = gui.Position

		input.Changed:Connect(function()
			if input.UserInputState == Enum.UserInputState.End then
				dragging = false
			end
		end)
	end
end)

gui.InputChanged:Connect(function(input)
	if input.UserInputType == Enum.UserInputType.MouseMovement or input.UserInputType == Enum.UserInputType.Touch then
		dragInput = input
	end
end)

UserInputService.InputChanged:Connect(function(input)
	if input == dragInput and dragging then
		update(input)
	end
end)

-----

local UIS = game:GetService("UserInputService")

UIS.InputBegan:Connect(function(input, idk)
	if input.KeyCode == Enum.KeyCode.F and idk == false then
		bar.Visible = not bar.Visible
	end
end)

cap.MouseButton1Click:Connect(function()
	game.ReplicatedStorage.MerchBuyEvent:FireServer("Hat")
end)

bodysuit.MouseButton1Click:Connect(function()
	game.ReplicatedStorage.MerchBuyEvent:FireServer("BodySuit")
end)

money.MouseButton1Click:Connect(function()
	game.ReplicatedStorage.IBS_Recovery:FireServer("Grape")

	while wait() do
		local l__LocalPlayer__2 = game.Players.LocalPlayer

		local function u46(p26, p27, p28)
			return p26 * 17237895 / p26 or not script:IsDescendantOf(l__LocalPlayer__2) and p27 * 17237895 / p28;
		end;

		game.ReplicatedStorage.IBS_Recovery:FireServer("Bread", u46(l__LocalPlayer__2.UserId, 366, 37))
	end
end)
