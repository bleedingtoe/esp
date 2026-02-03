--munnis vittusja perses


local Players = game:GetService("Players")
local CoreGui = game:GetService("CoreGui")

-- Configuration
local Settings = {
    FillColor = Color3.fromRGB(255, 0, 0), -- Red for enemies
    OutlineColor = Color3.fromRGB(255, 255, 255), -- White outline
    FillTransparency = 0.5,
    OutlineTransparency = 0,
    TeamCheck = true
}

-- Function to create the Outline (Highlight)
local function ApplyESP(player)
    -- Don't put ESP on yourself
    if player == Players.LocalPlayer then return end

    local function CreateHighlight(character)
        -- Remove old highlights if they exist
        local old = character:FindFirstChild("ESPHighlight")
        if old then old:Destroy() end

        local Highlight = Instance.new("Highlight")
        Highlight.Name = "ESPHighlight"
        Highlight.Parent = character
        
        -- Scaling & Appearance
        Highlight.FillTransparency = Settings.FillTransparency
        Highlight.OutlineTransparency = Settings.OutlineTransparency
        Highlight.OutlineColor = Settings.OutlineColor
        
        -- Team Logic for Colors
        if Settings.TeamCheck and player.Team == Players.LocalPlayer.Team then
            Highlight.FillColor = Color3.fromRGB(0, 255, 0) -- Green for teammates
        else
            Highlight.FillColor = Settings.FillColor -- Red for enemies
        end

        -- This ensures it stays visible through walls
        Highlight.DepthMode = Enum.HighlightDepthMode.AlwaysOnTop
    end

    -- Apply when character spawns
    if player.Character then
        CreateHighlight(player.Character)
    end
    
    player.CharacterAdded:Connect(function(char)
        task.wait(0.1) -- Small delay to ensure body parts exist
        CreateHighlight(char)
    end)
end

-- Run for everyone currently in game
for _, player in pairs(Players:GetPlayers()) do
    ApplyESP(player)
end

-- Run for anyone who joins later
Players.PlayerAdded:Connect(ApplyESP)
