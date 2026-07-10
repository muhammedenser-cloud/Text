local player = game.Players.LocalPlayer
local gui = Instance.new("ScreenGui")
gui.Name = "DeltaAdminGui"
gui.Parent = player.PlayerGui

local frame = Instance.new("Frame")
frame.Size = UDim2.new(0, 600, 0, 80)
frame.Position = UDim2.new(0.5, -300, 0.8, 0)
frame.BackgroundColor3 = Color3.new(0, 0, 0)
frame.BackgroundTransparency = 0.6
frame.BorderSizePixel = 0
frame.Parent = gui

local textBox = Instance.new("TextBox")
textBox.Size = UDim2.new(0, 580, 0, 40)
textBox.Position = UDim2.new(0, 10, 0, 10)
textBox.BackgroundColor3 = Color3.new(0.2, 0.2, 0.2)
textBox.TextColor3 = Color3.new(1, 1, 1)
textBox.BorderSizePixel = 2
textBox.BorderColor3 = Color3.new(0.3, 0.6, 1)
textBox.Font = Enum.Font.SourceSansBold
textBox.TextSize = 22
textBox.PlaceholderText = "Type message and press ENTER"
textBox.ClearTextOnFocus = false
textBox.Parent = frame

local displayLabel = Instance.new("TextLabel")
displayLabel.Size = UDim2.new(0, 800, 0, 120)
displayLabel.Position = UDim2.new(0.5, -400, 0.3, -60)
displayLabel.BackgroundTransparency = 1
displayLabel.TextColor3 = Color3.new(1, 1, 1)
displayLabel.TextScaled = true
displayLabel.Font = Enum.Font.SourceSansBold
displayLabel.Text = ""
displayLabel.Visible = false
displayLabel.Parent = gui

local blueTick = Instance.new("ImageLabel")
blueTick.Size = UDim2.new(0, 40, 0, 40)
blueTick.Position = UDim2.new(0.5, -480, 0.3, -70)
blueTick.BackgroundTransparency = 1
blueTick.Image = "rbxassetid://1234567890"
blueTick.Visible = false
blueTick.Parent = gui

local sound = Instance.new("Sound")
sound.SoundId = "rbxassetid://9120408690"
sound.Volume = 0.8
sound.Parent = gui

local glowEffect = Instance.new("BloomEffect")
glowEffect.Enabled = false
glowEffect.Intensity = 1
glowEffect.Size = 50
glowEffect.Threshold = 0.5
glowEffect.Parent = gui

local colorCorrection = Instance.new("ColorCorrectionEffect")
colorCorrection.Enabled = false
colorCorrection.Brightness = 0.2
colorCorrection.Contrast = 0.3
colorCorrection.Saturation = 0.5
colorCorrection.TintColor = Color3.new(1, 1, 0.5)
colorCorrection.Parent = gui

local shadow = Instance.new("ShadowEffect")
shadow.Enabled = false
shadow.Intensity = 1
shadow.Size = 10
shadow.Parent = gui

local particleEmitter = Instance.new("ParticleEmitter")
particleEmitter.Enabled = false
particleEmitter.Texture = "rbxassetid://1234567891"
particleEmitter.Rate = 200
particleEmitter.Lifetime = NumberRange.new(1, 2)
particleEmitter.SpreadAngle = Vector2.new(360, 360)
particleEmitter.VelocityInheritance = 0.5
particleEmitter.Acceleration = Vector3.new(0, -10, 0)
particleEmitter.Drag = 1
particleEmitter.LockedToPart = false
particleEmitter.Parent = gui

local messageHistory = {}
local historyFrame = Instance.new("Frame")
historyFrame.Size = UDim2.new(0, 300, 0, 400)
historyFrame.Position = UDim2.new(0.01, 0, 0.01, 0)
historyFrame.BackgroundColor3 = Color3.new(0, 0, 0)
historyFrame.BackgroundTransparency = 0.7
historyFrame.BorderSizePixel = 1
historyFrame.BorderColor3 = Color3.new(0.3, 0.6, 1)
historyFrame.Visible = false
historyFrame.Parent = gui

local historyList = Instance.new("ScrollingFrame")
historyList.Size = UDim2.new(0, 280, 0, 380)
historyList.Position = UDim2.new(0, 10, 0, 10)
historyList.BackgroundTransparency = 1
historyList.BorderSizePixel = 0
historyList.CanvasSize = UDim2.new(0, 0, 0, 0)
historyList.ScrollBarThickness = 8
historyList.Parent = historyFrame

local toggleHistory = Instance.new("TextButton")
toggleHistory.Size = UDim2.new(0, 150, 0, 30)
toggleHistory.Position = UDim2.new(0.01, 0, 0.01, 0)
toggleHistory.BackgroundColor3 = Color3.new(0.2, 0.2, 0.2)
toggleHistory.TextColor3 = Color3.new(1, 1, 1)
toggleHistory.Text = "Show History"
toggleHistory.Font = Enum.Font.SourceSansBold
toggleHistory.TextSize = 16
toggleHistory.BorderSizePixel = 1
toggleHistory.BorderColor3 = Color3.new(0.3, 0.6, 1)
toggleHistory.Parent = gui

local clearHistory = Instance.new("TextButton")
clearHistory.Size = UDim2.new(0, 100, 0, 30)
clearHistory.Position = UDim2.new(0.15, 0, 0.01, 0)
clearHistory.BackgroundColor3 = Color3.new(0.2, 0.2, 0.2)
clearHistory.TextColor3 = Color3.new(1, 0.2, 0.2)
clearHistory.Text = "Clear"
clearHistory.Font = Enum.Font.SourceSansBold
clearHistory.TextSize = 16
clearHistory.BorderSizePixel = 1
clearHistory.BorderColor3 = Color3.new(1, 0.2, 0.2)
clearHistory.Parent = gui

local charCounter = Instance.new("TextLabel")
charCounter.Size = UDim2.new(0, 100, 0, 20)
charCounter.Position = UDim2.new(0, 490, 0, 55)
charCounter.BackgroundTransparency = 1
charCounter.TextColor3 = Color3.new(0.5, 0.5, 0.5)
charCounter.Text = "0/200"
charCounter.Font = Enum.Font.SourceSans
charCounter.TextSize = 14
charCounter.TextXAlignment = Enum.TextXAlignment.Right
charCounter.Parent = frame

local typingIndicator = Instance.new("TextLabel")
typingIndicator.Size = UDim2.new(0, 200, 0, 30)
typingIndicator.Position = UDim2.new(0.5, -100, 0.75, 0)
typingIndicator.BackgroundTransparency = 1
typingIndicator.TextColor3 = Color3.new(0.5, 0.8, 1)
typingIndicator.Text = "You are typing..."
typingIndicator.Font = Enum.Font.SourceSans
typingIndicator.TextSize = 16
typingIndicator.Visible = false
typingIndicator.Parent = gui

local function addHistoryEntry(name, msg)
    local entry = Instance.new("TextLabel")
    entry.Size = UDim2.new(0, 280, 0, 30)
    entry.BackgroundTransparency = 1
    entry.TextColor3 = Color3.new(1, 1, 1)
    entry.Text = name .. ": " .. msg
    entry.Font = Enum.Font.SourceSans
    entry.TextSize = 14
    entry.TextXAlignment = Enum.TextXAlignment.Left
    entry.Parent = historyList
    
    table.insert(messageHistory, {name = name, msg = msg})
    historyList.CanvasSize = UDim2.new(0, 0, 0, #messageHistory * 30)
end

local function clearHistoryEntries()
    for _, child in pairs(historyList:GetChildren()) do
        child:Destroy()
    end
    messageHistory = {}
    historyList.CanvasSize = UDim2.new(0, 0, 0, 0)
end

local function showMessageWithEffects(msg)
    displayLabel.Text = player.Name .. " 🔹 " .. msg
    displayLabel.Visible = true
    blueTick.Visible = true
    sound:Play()
    glowEffect.Enabled = true
    colorCorrection.Enabled = true
    shadow.Enabled = true
    particleEmitter.Enabled = true
    
    local flashCount = 0
    while flashCount < 5 do
        displayLabel.TextColor3 = Color3.new(1, 1, 0.5)
        colorCorrection.TintColor = Color3.new(1, 1, 0.3)
        wait(0.05)
        displayLabel.TextColor3 = Color3.new(1, 1, 1)
        colorCorrection.TintColor = Color3.new(1, 1, 0.5)
        wait(0.05)
        flashCount = flashCount + 1
    end
    
    local startPos = displayLabel.Position
    local endPos = UDim2.new(0.5, -400, -0.1, -60)
    local duration = 2.5
    local elapsed = 0
    
    wait(5)
    
    while elapsed < duration do
        elapsed = elapsed + 0.05
        local ratio = elapsed / duration
        local newY = startPos.Y.Scale + (endPos.Y.Scale - startPos.Y.Scale) * ratio
        local newX = startPos.X.Scale + (endPos.X.Scale - startPos.X.Scale) * ratio * 0.2
        
        displayLabel.Position = UDim2.new(newX, -400 + (ratio * 100), newY, -60)
        blueTick.Position = UDim2.new(0.5 - (ratio * 0.05), -480 + (ratio * 50), newY - 0.1, -70)
        
        displayLabel.TextTransparency = ratio * 0.8
        blueTick.ImageTransparency = ratio * 0.8
        displayLabel.TextStrokeTransparency = ratio * 0.5
        displayLabel.TextStrokeColor3 = Color3.new(1, 0.8, 0.3)
        
        displayLabel.Rotation = math.sin(elapsed * 2) * 3 * (1 - ratio)
        displayLabel.Size = UDim2.new(0, 800 + (ratio * 200), 0, 120 + (ratio * 30))
        
        local scale = 1 + (ratio * 0.1)
        displayLabel.TextScaled = true
        
        wait(0.05)
    end
    
    displayLabel.Visible = false
    blueTick.Visible = false
    displayLabel.TextTransparency = 0
    blueTick.ImageTransparency = 0
    displayLabel.TextStrokeTransparency = 0
    displayLabel.Rotation = 0
    displayLabel.Size = UDim2.new(0, 800, 0, 120)
    displayLabel.Position = UDim2.new(0.5, -400, 0.3, -60)
    blueTick.Position = UDim2.new(0.5, -480, 0.3, -70)
    
    glowEffect.Enabled = false
    colorCorrection.Enabled = false
    shadow.Enabled = false
    particleEmitter.Enabled = false
    
    addHistoryEntry(player.Name, msg)
end

textBox.Changed:Connect(function(prop)
    if prop == "Text" then
        local len = string.len(textBox.Text)
        charCounter.Text = len .. "/200"
        
        if len > 0 then
            typingIndicator.Visible = true
        else
            typingIndicator.Visible = false
        end
        
        if len > 200 then
            textBox.Text = string.sub(textBox.Text, 1, 200)
        end
    end
end)

textBox.FocusLost:Connect(function(enterPressed)
    if enterPressed then
        local msg = textBox.Text
        if msg ~= "" then
            showMessageWithEffects(msg)
            textBox.Text = ""
            charCounter.Text = "0/200"
            typingIndicator.Visible = false
        end
    end
end)

toggleHistory.MouseButton1Click:Connect(function()
    historyFrame.Visible = not historyFrame.Visible
    if historyFrame.Visible then
        toggleHistory.Text = "Hide History"
    else
        toggleHistory.Text = "Show History"
    end
end)

clearHistory.MouseButton1Click:Connect(function()
    clearHistoryEntries()
end)

local function updateScrollbar()
    historyList.CanvasPosition = UDim2.new(0, 0, 0, historyList.CanvasSize.Y.Offset)
end

historyList.ChildAdded:Connect(function()
    wait(0.1)
    updateScrollbar()
end)

local function animateParticles()
    while true do
        if particleEmitter.Enabled then
            particleEmitter.Rate = 150 + math.random(0, 100)
            particleEmitter.Lifetime = NumberRange.new(0.5 + math.random(), 1.5 + math.random())
        end
        wait(0.5)
    end
end

coroutine.wrap(animateParticles)()

local function flashButton()
    while true do
        toggleHistory.BackgroundColor3 = Color3.new(0.2 + math.sin(tick() * 2) * 0.1, 0.2, 0.2)
        clearHistory.BackgroundColor3 = Color3.new(0.2, 0.2 - math.sin(tick() * 2) * 0.1, 0.2 - math.sin(tick() * 2) * 0.1)
        wait(0.1)
    end
end

coroutine.wrap(flashButton)()

local function preventSpam()
    local lastMessage = ""
    local cooldown = false
    
    textBox.FocusLost:Connect(function(enterPressed)
        if enterPressed then
            local msg = textBox.Text
            if msg ~= "" and msg == lastMessage then
                textBox.Text = ""
                textBox.PlaceholderText = "No spam allowed!"
                wait(2)
                textBox.PlaceholderText = "Type message and press ENTER"
            else
                lastMessage = msg
            end
        end
    end)
end

preventSpam()

local function autoSaveHistory()
    while true do
        if #messageHistory > 0 then
            local saveData = {}
            for i, entry in ipairs(messageHistory) do
                saveData[i] = entry.name .. "|" .. entry.msg
            end
            -- save to datastore would go here
        end
        wait(60)
    end
end

coroutine.wrap(autoSaveHistory)()

local function displayWelcome()
    local welcome = Instance.new("TextLabel")
    welcome.Size = UDim2.new(0, 600, 0, 50)
    welcome.Position = UDim2.new(0.5, -300, 0.1, 0)
    welcome.BackgroundTransparency = 1
    welcome.TextColor3 = Color3.new(0.3, 0.6, 1)
    welcome.Text = "Delta Admin System v2.0 - Type message and press ENTER"
    welcome.Font = Enum.Font.SourceSansBold
    welcome.TextSize = 18
    welcome.TextTransparency = 0.8
    welcome.Parent = gui
    
    local alpha = 0.8
    while alpha > 0 do
        alpha = alpha - 0.05
        welcome.TextTransparency = alpha
        wait(0.1)
    end
    welcome:Destroy()
end

coroutine.wrap(displayWelcome)()

local function handleResize()
    local screenSize = game:GetService("GuiService"):GetScreenResolution()
    if screenSize.X < 800 or screenSize.Y < 600 then
        frame.Size = UDim2.new(0, 400, 0, 70)
        frame.Position = UDim2.new(0.5, -200, 0.8, 0)
        textBox.Size = UDim2.new(0, 380, 0, 35)
        textBox.Position = UDim2.new(0, 10, 0, 10)
        textBox.TextSize = 18
        displayLabel.Size = UDim2.new(0, 600, 0, 90)
        displayLabel.Position = UDim2.new(0.5, -300, 0.3, -45)
        blueTick.Size = UDim2.new(0, 30, 0, 30)
        blueTick.Position = UDim2.new(0.5, -380, 0.3, -55)
        charCounter.Position = UDim2.new(0, 300, 0, 50)
    else
        frame.Size = UDim2.new(0, 600, 0, 80)
        frame.Position = UDim2.new(0.5, -300, 0.8, 0)
        textBox.Size = UDim2.new(0, 580, 0, 40)
        textBox.Position = UDim2.new(0, 10, 0, 10)
        textBox.TextSize = 22
        displayLabel.Size = UDim2.new(0, 800, 0, 120)
        displayLabel.Position = UDim2.new(0.5, -400, 0.3, -60)
        blueTick.Size = UDim2.new(0, 40, 0, 40)
        blueTick.Position = UDim2.new(0.5, -480, 0.3, -70)
        charCounter.Position = UDim2.new(0, 490, 0, 55)
    end
end

game:GetService("GuiService").ScreenResolutionChanged:Connect(handleResize)
handleResize()

local function setCustomColors()
    local colors = {
        Color3.new(1, 0.5, 0.5),
        Color3.new(0.5, 1, 0.5),
        Color3.new(0.5, 0.5, 1),
        Color3.new(1, 1, 0.5),
        Color3.new(1, 0.5, 1),
        Color3.new(0.5, 1, 1)
    }
    
    local index = 1
    while true do
        if displayLabel.Visible then
            local color = colors[index % #colors + 1]
            displayLabel.TextColor3 = color
            index = index + 1
        end
        wait(0.5)
    end
end

coroutine.wrap(setCustomColors)()

local function createLoadingScreen()
    local loading = Instance.new("Frame")
    loading.Size = UDim2.new(0, 300, 0, 50)
    loading.Position = UDim2.new(0.5, -150, 0.5, -25)
    loading.BackgroundColor3 = Color3.new(0, 0, 0)
    loading.BackgroundTransparency = 0.8
    loading.BorderSizePixel = 0
    loading.Parent = gui
    
    local loadingText = Instance.new("TextLabel")
    loadingText.Size = UDim2.new(0, 300, 0, 50)
    loadingText.Position = UDim2.new(0, 0, 0, 0)
    loadingText.BackgroundTransparency = 1
    loadingText.TextColor3 = Color3.new(1, 1, 1)
    loadingText.Text = "Loading Delta System..."
    loadingText.Font = Enum.Font.SourceSansBold
    loadingText.TextSize = 20
    loadingText.Parent = loading
    
    local progress = 0
    while progress < 1 do
        progress = progress + 0.01
        loadingText.Text = "Loading Delta System... " .. math.floor(progress * 100) .. "%"
        loadingText.TextColor3 = Color3.new(progress, 1 - progress * 0.5, 0.5)
        wait(0.05)
    end
    
    loading:Destroy()
end

coroutine.wrap(createLoadingScreen)()

local function keybindHandler()
    local UserInputService = game:GetService("UserInputService")
    
    UserInputService.InputBegan:Connect(function(input, gameProcessed)
        if gameProcessed then return end
        
        if input.KeyCode == Enum.KeyCode.F1 then
            toggleHistory.MouseButton1Click:Fire()
        elseif input.KeyCode == Enum.KeyCode.F2 then
            clearHistory.MouseButton1Click:Fire()
        elseif input.KeyCode == Enum.KeyCode.F3 then
            textBox:CaptureFocus()
        elseif input.KeyCode == Enum.KeyCode.F4 then
            frame.Visible = not frame.Visible
        end
    end)
end

keybindHandler()

local function versionCheck()
    local version = "2.0"
    local latestVersion = "2.0"
    
    if version ~= latestVersion then
        local updateNotice = Instance.new("TextLabel")
        updateNotice.Size = UDim2.new(0, 400, 0, 30)
        updateNotice.Position = UDim2.new(0.5, -200, 0.95, 0)
        updateNotice.BackgroundTransparency = 1
        updateNotice.TextColor3 = Color3.new(1, 0.5, 0)
        updateNotice.Text = "Update available! Version " .. latestVersion
        updateNotice.Font = Enum.Font.SourceSansBold
        updateNotice.TextSize = 14
        updateNotice.Parent = gui
        
        wait(5)
        updateNotice:Destroy()
    end
end

coroutine.wrap(versionCheck)()
