-- Shift Lock Mobile Script
-- Coloque este script em **StarterPlayerScripts**

local UserInputService = game:GetService("UserInputService")
local RunService = game:GetService("RunService")
local Players = game:GetService("Players")
local StarterGui = game:GetService("StarterGui")

local player = Players.LocalPlayer
local camera = game.Workspace.CurrentCamera

-- Criar botão
local button = Instance.new("TextButton")
button.Size = UDim2.new(0, 100, 0, 40)
button.Position = UDim2.new(1, -110, 1, -50)
button.Text = "Shift Lock"
button.BackgroundColor3 = Color3.fromRGB(0, 170, 255)
button.TextColor3 = Color3.new(1, 1, 1)
button.Font = Enum.Font.SourceSansBold
button.TextSize = 18
button.Parent = StarterGui:WaitForChild("ScreenGui", 5) or Instance.new("ScreenGui", player:WaitForChild("PlayerGui"))

-- Criar estado de ativação
local shiftLockEnabled = false

-- Loop de travamento de câmera
RunService.RenderStepped:Connect(function()
	if shiftLockEnabled and player.Character and player.Character:FindFirstChild("HumanoidRootPart") then
		camera.CameraType = Enum.CameraType.Scriptable
		camera.CFrame = CFrame.new(camera.CFrame.Position, player.Character.HumanoidRootPart.Position)
	else
		camera.CameraType = Enum.CameraType.Custom
	end
end)

-- Clique do botão
button.MouseButton1Click:Connect(function()
	shiftLockEnabled = not shiftLockEnabled
	button.Text = shiftLockEnabled and "Unlock" or "Shift Lock"
	button.BackgroundColor3 = shiftLockEnabled and Color3.fromRGB(255, 85, 0) or Color3.fromRGB(0, 170, 255)
end)
