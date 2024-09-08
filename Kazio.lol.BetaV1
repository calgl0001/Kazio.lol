local Library = loadstring(game:HttpGet("https://raw.githubusercontent.com/bloodball/-back-ups-for-libs/main/cat"))()
local Window = Library:CreateWindow("Kazio.lua (Beta)", Vector2.new(340, 350), Enum.KeyCode.RightControl)

--Tabs
local MainTab = Window:CreateTab("Main")

local VisualsTab = Window:CreateTab("Visuals")

local MiscTab = Window:CreateTab("Misc")

--Sections
local CamlockSection = MainTab:CreateSector("Camlock", "left")

local AimlockSection MainTab:CreateSector("Aimlock", "right")

local VisualsSection =
VisualsTab:CreateSector("Visuals", "left")

local MiscSection = MiscTab:CreateSector("First Section", "left")

--Buttons
CamlockSection:AddButton("Camlock GUI", function(IhateGayPeople)
        local Players = game:GetService("Players")
        local RunService = game:GetService("RunService")
        local LocalPlayer = Players.LocalPlayer
        local Camera = workspace.CurrentCamera
        local UIS = game:GetService("UserInputService")
        local Mouse = LocalPlayer:GetMouse()

        local function createGUI()
            local ScreenGui = Instance.new("ScreenGui")
            local BarFrame = Instance.new("Frame")
            local Button = Instance.new("TextButton")

            ScreenGui.Name = "KazioGui"
            ScreenGui.Parent = LocalPlayer:WaitForChild("PlayerGui")

            BarFrame.Name = "MoveableBar"
            BarFrame.Size = UDim2.new(0, 220, 0, 70)
            BarFrame.Position = UDim2.new(1, -240, 0, 20)
            BarFrame.BackgroundColor3 = Color3.new(0.2, 0.2, 0.2)
            BarFrame.BorderSizePixel = 2
            BarFrame.Parent = ScreenGui
            BarFrame.Active = true

            Button.Name = "Kazio.lol"
            Button.Size = UDim2.new(0, 200, 0, 50)
            Button.Position = UDim2.new(0, 10, 0, 10)
            Button.Text = "Kazio Off"
            Button.Parent = BarFrame

            Button.Font = Enum.Font.LuckiestGuy
            Button.TextSize = 30
            Button.TextColor3 = Color3.new(1, 1, 1)
            Button.TextStrokeTransparency = 0.5
            Button.TextStrokeColor3 = Color3.new(0, 0, 0)

            local function rainbowBackground(button)
                while true do
                    for i = 0, 1, 0.01 do
                        button.BackgroundColor3 = Color3.fromHSV(i, 1, 1)
                        wait(0.01)
                    end
                end
            end

            spawn(function()
                rainbowBackground(Button)
            end)

            local dragging = false
            local dragInput, dragStart, startPos

            local function updateDrag(input)
                local delta = input.Position - dragStart
                BarFrame.Position = UDim2.new(startPos.X.Scale, startPos.X.Offset + delta.X, startPos.Y.Scale, startPos.Y.Offset + delta.Y)
            end

            BarFrame.InputBegan:Connect(function(input)
                if input.UserInputType == Enum.UserInputType.MouseButton1 then
                    dragging = true
                    dragStart = input.Position
                    startPos = BarFrame.Position

                    input.Changed:Connect(function()
                        if input.UserInputState == Enum.UserInputState.End then
                            dragging = false
                        end
                    end)
                end
            end)

            BarFrame.InputChanged:Connect(function(input)
                if input.UserInputType == Enum.UserInputType.MouseMovement then
                    dragInput = input
                end
            end)

            UIS.InputChanged:Connect(function(input)
                if input == dragInput and dragging then
                    updateDrag(input)
                end
            end)

            local predictionValue = 0.1488375834163075
            local jumpOffset = 0.1
            local camlockXOffset = 0.5
            local camlockYOffset = 0.2
            local isLocked = false
            local TargetPlayer = nil
            local RenderConnection = nil

            local function findClosestPlayerToCamera()
                local closestPlayer = nil
                local closestDist = math.huge

                for _, player in pairs(Players:GetPlayers()) do
                    if player ~= LocalPlayer and player.Character and player.Character:FindFirstChild("UpperTorso") then
                        local playerPos = player.Character.UpperTorso.Position
                        local screenPos, onScreen = Camera:WorldToScreenPoint(playerPos)

                        if onScreen then
                            local mousePos = UIS:GetMouseLocation()
                            local dist = (Vector2.new(mousePos.X, mousePos.Y) - Vector2.new(screenPos.X, screenPos.Y)).Magnitude

                            if dist < closestDist then
                                closestDist = dist
                                closestPlayer = player
                            end
                        end
                    end
                end
                return closestPlayer
            end

            local function lockOntoPlayer(player)
                if player and player.Character and player.Character:FindFirstChild("UpperTorso") then
                    local targetPart = player.Character.UpperTorso
                    if RenderConnection then
                        RenderConnection:Disconnect()
                    end
                    RenderConnection = RunService.RenderStepped:Connect(function()
                        if isLocked and player.Character then
                            local predictedPosition = targetPart.Position + targetPart.Velocity * predictionValue + Vector3.new(0, jumpOffset, 0)
                            local cameraOffset = Vector3.new(camlockXOffset, camlockYOffset, 0)
                            local goalCFrame = CFrame.new(Camera.CFrame.Position, predictedPosition + cameraOffset)
                            Camera.CFrame = goalCFrame
                        end
                    end)
                end
            end

            Button.MouseButton1Click:Connect(function()
                if isLocked then
                    if RenderConnection then
                        RenderConnection:Disconnect()
                        RenderConnection = nil
                    end
                    Camera.CameraType = Enum.CameraType.Custom
                    Button.Text = "Kazio Off"
                    isLocked = false
                else
                    isLocked = true
                    TargetPlayer = findClosestPlayerToCamera()

                    if TargetPlayer then
                        lockOntoPlayer(TargetPlayer)
                        Button.Text = "Kazio On"
                    else
                        Button.Text = "Kazio Off"
                        isLocked = false
                    end
                end
            end)
        end

        createGUI()

        LocalPlayer.CharacterAdded:Connect(function()
            repeat wait() until LocalPlayer:FindFirstChild("PlayerGui")

            local existingGui = LocalPlayer.PlayerGui:FindFirstChild("KazioGui")
            if not existingGui then
                createGUI()
            end
        end)
    print("button")
end)

CamlockSection:AddButton("Camlock TOOL", function(IhateGayPeople)
        local Players = game:GetService("Players")
        local RunService = game:GetService("RunService")
        local StarterPack = game:GetService("StarterPack")
        local Camera = workspace.CurrentCamera
        local UIS = game:GetService("UserInputService")
        local LocalPlayer = Players.LocalPlayer

        local ToolName = "KazioTool"
        local predictionValue = 0.1488375834163075
        local jumpOffset = 0.1
        local camlockXOffset = 0.5
        local camlockYOffset = 0.2
        local isLocked = false
        local TargetPlayer = nil
        local RenderConnection = nil

        local Tool = Instance.new("Tool")
        local Handle = Instance.new("Part")

        Tool.Name = ToolName
        Tool.RequiresHandle = true
        Tool.CanBeDropped = true

        Handle.Name = "Handle"
        Handle.Size = Vector3.new(1, 1, 1)
        Handle.Anchored = false
        Handle.CanCollide = false
        Handle.Transparency = 1
        Handle.Parent = Tool

        Tool.Parent = LocalPlayer.Backpack

        local function findClosestPlayerToCamera()
            local closestPlayer = nil
            local closestDist = math.huge

            for _, player in pairs(Players:GetPlayers()) do
                if player ~= LocalPlayer and player.Character and player.Character:FindFirstChild("UpperTorso") then
                    local playerPos = player.Character.UpperTorso.Position
                    local screenPos, onScreen = Camera:WorldToScreenPoint(playerPos)

                    if onScreen then
                        local mousePos = UIS:GetMouseLocation()
                        local dist = (Vector2.new(mousePos.X, mousePos.Y) - Vector2.new(screenPos.X, screenPos.Y)).Magnitude

                        if dist < closestDist then
                            closestDist = dist
                            closestPlayer = player
                        end
                    end
                end
            end
            return closestPlayer
        end

        local function lockOntoPlayer(player)
            if player and player.Character and player.Character:FindFirstChild("UpperTorso") then
                local targetPart = player.Character.UpperTorso
                if RenderConnection then
                    RenderConnection:Disconnect()
                end
                RenderConnection = RunService.RenderStepped:Connect(function()
                    if isLocked and player.Character then
                        local predictedPosition = targetPart.Position + targetPart.Velocity * predictionValue + Vector3.new(0, jumpOffset, 0)
                        local cameraOffset = Vector3.new(camlockXOffset, camlockYOffset, 0)
                        local goalCFrame = CFrame.new(Camera.CFrame.Position, predictedPosition + cameraOffset)
                        Camera.CFrame = goalCFrame
                    end
                end)
            end
        end

        Tool.Activated:Connect(function()
            if isLocked then
                if RenderConnection then
                    RenderConnection:Disconnect()
                    RenderConnection = nil
                end
                Camera.CameraType = Enum.CameraType.Custom
                isLocked = false
                Tool.ToolTip = "Kazio Tool - Off"
            else
                isLocked = true
                TargetPlayer = findClosestPlayerToCamera()

                if TargetPlayer then
                    lockOntoPlayer(TargetPlayer)
                    Tool.ToolTip = "Kazio Tool - On"
                else
                    isLocked = false
                    Tool.ToolTip = "Kazio Tool - Off"
                end
            end
        end)

        local function onCharacterAdded(character)
            local tool = StarterPack:FindFirstChild(ToolName)
            if tool then
                local clonedTool = tool:Clone()
                clonedTool.Parent = character:FindFirstChildOfClass("Backpack")
            end
        end

        Players.PlayerAdded:Connect(function(player)
            player.CharacterAdded:Connect(onCharacterAdded)
        end)

        for _, player in pairs(Players:GetPlayers()) do
            if player.Character then
                onCharacterAdded(player.Character)
            end
        end
    print("button")
end)

MiscSection:AddButton("CFrame Speed", function(IhateGayPeopl)
        local speed = 40  -- Speed value
        local isMoving = true
        local player = game.Players.LocalPlayer
        local character = player.Character or player.CharacterAdded:Wait()
        local hrp = character:WaitForChild("HumanoidRootPart")

        -- Create the GUI
        local screenGui = Instance.new("ScreenGui", player:WaitForChild("PlayerGui"))
        local toggleButton = Instance.new("TextButton", screenGui)

        toggleButton.Size = UDim2.new(0, 100, 0, 50)
        toggleButton.Position = UDim2.new(0, 10, 0, 10)  -- Top left of the screen
        toggleButton.Text = "Stop"
        toggleButton.BackgroundColor3 = Color3.fromRGB(255, 0, 0)  -- Red color for stop
        toggleButton.TextScaled = true

        -- Function to toggle movement
        local function toggleMovement()
            isMoving = not isMoving
            if isMoving then
                toggleButton.Text = "Stop"
                toggleButton.BackgroundColor3 = Color3.fromRGB(255, 0, 0)  -- Red for stop
            else
                toggleButton.Text = "Go"
                toggleButton.BackgroundColor3 = Color3.fromRGB(0, 255, 0)  -- Green for go
            end
        end

        -- Connect the button click to toggle the movement
        toggleButton.MouseButton1Click:Connect(toggleMovement)

        -- Run the movement loop
        game:GetService("RunService").RenderStepped:Connect(function(deltaTime)
            if isMoving then
                local moveDirection = hrp.CFrame.LookVector
                hrp.CFrame = hrp.CFrame + moveDirection * speed * deltaTime
            end
        end)
    print("button")
end)

MiscSection:AddButton("Right Click", function(IhateGayPeople)       loadstring(game:HttpGet("https://raw.githubusercontent.com/DHBCommunity/DHBOfficialScript/main/RightClick"))()
    print("button")
end)

--Toggles
local ToggleBind = CamlockSection:AddToggle("Camlock", false, function(e)

end)

local RunService = game:GetService("RunService")
local Players = game:GetService("Players")
local LocalPlayer = Players.LocalPlayer

local toggleEnabled = false

local function zeroOutYVelocity(hrp)
    if hrp then
        hrp.Velocity = Vector3.new(hrp.Velocity.X, 0, hrp.Velocity.Z)
        hrp.AssemblyLinearVelocity = Vector3.new(hrp.Velocity.X, 0, hrp.Velocity.Z)
    end
end

local function onPlayerAdded(player)
    player.CharacterAdded:Connect(function(character)
        local hrp = character:WaitForChild("HumanoidRootPart", 5)
        zeroOutYVelocity(hrp)
    end)
end

local function onPlayerRemoving(player)
    -- Clean-up code if necessary
end

Players.PlayerAdded:Connect(onPlayerAdded)
Players.PlayerRemoving:Connect(onPlayerRemoving)

-- Toggle function
CamlockSection:AddToggle("Resolver", false, function(state)
    toggleEnabled = state
end)

RunService.Heartbeat:Connect(function()
    if not toggleEnabled then
        return
    end

    pcall(function()
        for _, player in ipairs(Players:GetPlayers()) do
            if player ~= LocalPlayer and player.Character then
                local hrp = player.Character:FindFirstChild("HumanoidRootPart")
                zeroOutYVelocity(hrp)
            end
        end
    end)
end)

local localPlayer = game.Players.LocalPlayer
local highlightFolder = Instance.new("Folder", game.CoreGui)
highlightFolder.Name = "ESPHighlights"

local ESPEnabled = false

local function createHighlight(player)
    if player.Character and player.Character:FindFirstChild("HumanoidRootPart") then
        local highlight = Instance.new("Highlight")
        highlight.Adornee = player.Character
        highlight.FillColor = Color3.fromRGB(128, 0, 128)
        highlight.OutlineColor = Color3.fromRGB(128, 0, 128)
        highlight.OutlineTransparency = 0
        highlight.FillTransparency = 0.5
        highlight.Parent = highlightFolder
        highlight.Name = player.Name
    end
end

local function removeHighlight(player)
    if highlightFolder:FindFirstChild(player.Name) then
        highlightFolder:FindFirstChild(player.Name):Destroy()
    end
end

game.Players.PlayerAdded:Connect(function(player)
    player.CharacterAdded:Connect(function()
        if ESPEnabled then
            wait(1)
            createHighlight(player)
        end
    end)
end)

game.Players.PlayerRemoving:Connect(function(player)
    removeHighlight(player)
end)

for _, player in ipairs(game.Players:GetPlayers()) do
    if player ~= localPlayer then
        if player.Character then
            if ESPEnabled then
                createHighlight(player)
            end
        end
        player.CharacterAdded:Connect(function()
            if ESPEnabled then
                wait(1)
                createHighlight(player)
            end
        end)
    end
end

VisualsSection:AddToggle("Player Visuals", false, function(state)
    ESPEnabled = state

    if ESPEnabled then
        for _, player in ipairs(game.Players:GetPlayers()) do
            if player ~= localPlayer and player.Character then
                createHighlight(player)
            end
        end
    else
        for _, player in ipairs(game.Players:GetPlayers()) do
            removeHighlight(player)
        end
    end
end)

local Players = game:GetService("Players")
local RunService = game:GetService("RunService")
local Camera = workspace.CurrentCamera
local LocalPlayer = Players.LocalPlayer

local tracers = {}
local toggleState = false

local function createTracer(player)
    local tracer = Drawing.new("Line")
    tracer.Visible = false
    tracer.Color = Color3.new(0.678, 0.847, 0.902)
    tracer.Thickness = 2
    tracer.Transparency = 1
    tracer.From = Vector2.new(Camera.ViewportSize.X / 2, Camera.ViewportSize.Y)

    local function updateTracer()
        local character = player.Character
        if character and character:FindFirstChild("HumanoidRootPart") then
            local position, onScreen = Camera:WorldToViewportPoint(character.HumanoidRootPart.Position)
            if onScreen and toggleState then
                tracer.To = Vector2.new(position.X, position.Y)
                tracer.Visible = true
            else
                tracer.Visible = false
            end
        else
            tracer.Visible = false
        end
    end

    tracers[player] = tracer
    RunService.RenderStepped:Connect(updateTracer)
end

local function removeTracer(player)
    if tracers[player] then
        tracers[player]:Remove()
        tracers[player] = nil
    end
end

for _, player in pairs(Players:GetPlayers()) do
    if player ~= LocalPlayer then
        createTracer(player)
    end
end

Players.PlayerAdded:Connect(function(player)
    if player ~= LocalPlayer then
        createTracer(player)
    end
end)

Players.PlayerRemoving:Connect(function(player)
    removeTracer(player)
end)

VisualsSection:AddToggle("Player Tracers", false, function(state)
    toggleState = state
    for player, tracer in pairs(tracers) do
        if toggleState then
            tracer.Visible = true
        else
            tracer.Visible = false
        end
    end
end)
