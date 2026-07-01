local Players = game:GetService("Players")
local RunService = game:GetService("RunService")
local UserInputService = game:GetService("UserInputService")
local LocalPlayer = Players.LocalPlayer
local Camera = workspace.CurrentCamera
-- CẤU HÌNH TÍNH NĂNG
local IsAimbotEnabled = false -- Trạng thái bật/tắt
local FOV_RADIUS = 150 -- Bán kính vòng FOV (pixel)
local FOV_COLOR = Color3.fromRGB(255, 0, 0) -- Màu đỏ
-- TẠO VÒNG FOV BẰNG DRAWING API (Chỉ hoạt động ở Client)
local FOVCircle = Drawing.new("Circle")
FOVCircle.Thickness = 2
FOVCircle.Color = FOV_COLOR
FOVCircle.Filled = false
FOVCircle.Transparent = true
FOVCircle.Visible = false
-- TẠO GIAO DIỆN NÚT BẤM (GUI)
local ScreenGui = Instance.new("ScreenGui")
ScreenGui.Name = "AimbotMenu"
ScreenGui.ResetOnSpawn = false
ScreenGui.Parent = LocalPlayer:WaitForChild("PlayerGui")
local ToggleButton = Instance.new("TextButton")
ToggleButton.Size = UDim2.new(0, 120, 0, 40)
ToggleButton.Position = UDim2.new(0, 20, 0, 20) -- Góc trên bên trái
ToggleButton.BackgroundColor3 = Color3.fromRGB(200, 50, 50) -- Màu đỏ (OFF)
ToggleButton.Text = "Aimbot: OFF"
ToggleButton.TextColor3 = Color3.fromRGB(255, 255, 255)
ToggleButton.Font = Enum.Font.SourceSansBold
ToggleButton.TextSize = 18
ToggleButton.Parent = ScreenGui
-- Hàm bo góc cho nút bấm
local UICorner = Instance.new("UICorner")
UICorner.CornerRadius = UDim.new(0, 8)
UICorner.Parent = ToggleButton
-- SỰ KIỆN BẤM NÚT BẬT/TẮT
ToggleButton.MouseButton1Click:Connect(function()
IsAimbotEnabled = not IsAimbotEnabled
if IsAimbotEnabled then
ToggleButton.Text = "Aimbot: ON"
ToggleButton.BackgroundColor3 = Color3.fromRGB(50, 200, 50) -- Màu xanh (ON)
FOVCircle.Visible = true
else
ToggleButton.Text = "Aimbot: OFF"
ToggleButton.BackgroundColor3 = Color3.fromRGB(200, 50, 50) -- Màu đỏ (OFF)
FOVCircle.Visible = false
end
end)
-- VÒNG LẶP CẬP NHẬT FOV THEO MÀN HÌNH
RunService.RenderStepped:Connect(function()
if IsAimbotEnabled then
-- Luôn giữ vòng FOV ở chính giữa màn hình của người chơi
local ViewportSize = Camera.ViewportSize
FOVCircle.Position = Vector2.new(ViewportSize.X / 2, ViewportSize.Y / 2)
FOVCircle.Radius = FOV_RADIUS# Aimbot.lua
