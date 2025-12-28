-- TỰ TẠO SCRIPT TÀNG HÌNH + ĐÁNH NGƯỜI (GỌN NHẤT)
local p = game.Players.LocalPlayer
local c = p.Character
local inv = false

-- Tạo nút bấm siêu nhỏ
local b = Instance.new("TextButton", Instance.new("ScreenGui", game.CoreGui))
b.Size, b.Text = UDim2.new(0,60,0,30), "OFF"

b.MouseButton1Click:Connect(function()
    inv = not inv
    b.Text = inv and "ON" or "OFF"
    
    -- Vòng lặp làm tàng hình liên tục (để không bị hiện lại)
    task.spawn(function()
        while inv and task.wait() do
            for _, v in pairs(c:GetDescendants()) do
                if v:IsA("BasePart") or v:IsA("Decal") then v.Transparency = 1 end
            end
            -- Tăng tầm đánh khi đang tàng hình
            local t = c:FindFirstChildOfClass("Tool")
            if t and t:FindFirstChild("Handle") then
                t.Handle.Size = Vector3.new(20, 20, 20)
                t.Handle.CanCollide = false
            end
        end
    end)
end)

