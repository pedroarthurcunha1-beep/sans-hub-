--[[
Sans Hub Script
Opções:
1. Walkspeed
2. ESP
3. Secret
4. Brainrot
5. Teleguiado (gancho até a base do jogador executor)
]]

-- Função utilitária para criar GUI simples
local function createSansHubGUI()
    local ScreenGui = Instance.new("ScreenGui")
    ScreenGui.Name = "SansHub"
    ScreenGui.Parent = game.Players.LocalPlayer:WaitForChild("PlayerGui")
    local Frame = Instance.new("Frame")
    Frame.Size = UDim2.new(0, 220, 0, 260)
    Frame.Position = UDim2.new(0.5, -110, 0.5, -130)
    Frame.BackgroundColor3 = Color3.fromRGB(35, 35, 35)
    Frame.Parent = ScreenGui

    local title = Instance.new("TextLabel")
    title.Text = "Sans Hub"
    title.Size = UDim2.new(1, 0, 0, 36)
    title.BackgroundTransparency = 1
    title.TextColor3 = Color3.new(1, 1, 1)
    title.Font = Enum.Font.SourceSansBold
    title.TextScaled = true
    title.Parent = Frame

    local buttons = {
        {Text = "Walkspeed", Callback = function()
            local ws = game.Players.LocalPlayer.Character:FindFirstChildOfClass("Humanoid")
            if ws then ws.WalkSpeed = 50 end
        end},
        {Text = "ESP", Callback = function()
            for _,v in pairs(game.Players:GetPlayers()) do
                if v ~= game.Players.LocalPlayer and v.Character then
                    local highlight = Instance.new("Highlight")
                    highlight.Adornee = v.Character
                    highlight.FillColor = Color3.new(1,0,0)
                    highlight.Parent = v.Character
                end
            end
        end},
        {Text = "Secret", Callback = function()
            game.StarterGui:SetCore("SendNotification",{Title="Secret",Text="Você encontrou o segredo!"})
        end},
        {Text = "Brainrot", Callback = function()
            local head = game.Players.LocalPlayer.Character:FindFirstChild("Head")
            if head then
                local rot = Instance.new("BodyAngularVelocity")
                rot.AngularVelocity = Vector3.new(0,200,0)
                rot.MaxTorque = Vector3.new(0,math.huge,0)
                rot.Parent = head
                wait(2)
                rot:Destroy()
            end
        end},
        {Text = "Teleguiado", Callback = function()
            local base = workspace:FindFirstChild(game.Players.LocalPlayer.Name.."_Base")
            if base then
                local char = game.Players.LocalPlayer.Character
                if char and char:FindFirstChild("HumanoidRootPart") then
                    char:MoveTo(base.Position)
                end
            else
                game.StarterGui:SetCore("SendNotification",{Title="Teleguiado",Text="Base não encontrada."})
            end
        end},
    }

    for i, btn in ipairs(buttons) do
        local b = Instance.new("TextButton")
        b.Text = btn.Text
        b.Size = UDim2.new(1, -20, 0, 36)
        b.Position = UDim2.new(0, 10, 0, 40 + (i-1)*44)
        b.BackgroundColor3 = Color3.fromRGB(65,65,65)
        b.TextColor3 = Color3.new(1,1,1)
        b.Font = Enum.Font.SourceSans
        b.TextScaled = true
        b.Parent = Frame
        b.MouseButton1Click:Connect(btn.Callback)
    end
end

-- Executa GUI
createSansHubGUI()
