-- 陈某脚本 - 多功能脚本中心
-- 作者：神秘（帮解忍者注入器）
-- 合作群聊：582333520 (可复制)
-- 版本：v2.3 FIN-WindUI版
-- 语言：中英双语（带记忆功能）

local Players = game:GetService("Players")
local RunService = game:GetService("RunService")
local Lighting = game:GetService("Lighting")
local Workspace = game:GetService("Workspace")
local ReplicatedStorage = game:GetService("ReplicatedStorage")
local TextChatService = game:GetService("TextChatService")
local TeleportService = game:GetService("TeleportService")
local ProximityPromptService = game:GetService("ProximityPromptService")
local UserInputService = game:GetService("UserInputService")
local TweenService = game:GetService("TweenService")

local LocalPlayer = Players.LocalPlayer

-- ========== ESP透视管理器 ==========
local ESPManager = {
    Enabled = false,
    Boxes = {},
    Names = {},
    HealthBars = {},
    Tracers = {},
    TeamCheck = false,
    ShowName = true,
    ShowBox = true,
    ShowHealth = true,
    ShowTracer = false,
    MaxDistance = 1000,
    Colors = {
        Team = Color3.fromRGB(0, 255, 0),    -- 队友颜色
        Enemy = Color3.fromRGB(255, 0, 0),   -- 敌人颜色
        Neutral = Color3.fromRGB(255, 255, 0) -- 中立颜色
    }
}

-- ========== 碰撞箱管理器 ==========
local HitboxManager = {
    Enabled = false,
    SizeMultiplier = 3.0,  -- 碰撞箱大小倍数
    Transparency = 0.8,    -- 透明度
    Color = Color3.fromRGB(255, 0, 0),  -- 碰撞箱颜色
    Hitboxes = {},         -- 存储碰撞箱
    ShowVisual = false,    -- 显示碰撞箱可视化
    VisualBoxes = {}       -- 可视化碰撞箱
}

-- ========== 创建启动动画 ==========
local function CreateStartupAnimation()
    local PlayerGui = LocalPlayer:WaitForChild("PlayerGui")
    
    -- 创建加载屏幕
    local LoadingScreen = Instance.new("ScreenGui")
    LoadingScreen.Name = "ChenScriptLoadingScreen"
    LoadingScreen.ResetOnSpawn = false
    LoadingScreen.IgnoreGuiInset = true
    LoadingScreen.DisplayOrder = 9999
    LoadingScreen.ZIndexBehavior = Enum.ZIndexBehavior.Sibling
    LoadingScreen.Parent = PlayerGui
    
    -- 创建背景框架
    local BackgroundFrame = Instance.new("Frame")
    BackgroundFrame.Name = "Background"
    BackgroundFrame.Size = UDim2.new(1, 0, 1, 0)
    BackgroundFrame.BackgroundColor3 = Color3.fromRGB(15, 15, 20)
    BackgroundFrame.BackgroundTransparency = 0
    BackgroundFrame.BorderSizePixel = 0
    BackgroundFrame.Parent = LoadingScreen
    
    -- 创建渐变背景
    local Gradient = Instance.new("UIGradient")
    Gradient.Color = ColorSequence.new({
        ColorSequenceKeypoint.new(0, Color3.fromRGB(10, 10, 15)),
        ColorSequenceKeypoint.new(1, Color3.fromRGB(25, 25, 35))
    })
    Gradient.Rotation = 45
    Gradient.Parent = BackgroundFrame
    
    -- 创建中心容器
    local MainContainer = Instance.new("Frame")
    MainContainer.Name = "MainContainer"
    MainContainer.AnchorPoint = Vector2.new(0.5, 0.5)
    MainContainer.Position = UDim2.new(0.5, 0, 0.5, 0)
    MainContainer.Size = UDim2.new(0, 500, 0, 350)
    MainContainer.BackgroundTransparency = 1
    MainContainer.Parent = LoadingScreen
    
    -- 创建Logo
    local Logo = Instance.new("ImageLabel")
    Logo.Name = "Logo"
    Logo.AnchorPoint = Vector2.new(0.5, 0.5)
    Logo.Position = UDim2.new(0.5, 0, 0.35, 0)
    Logo.Size = UDim2.new(0, 150, 0, 150)
    Logo.BackgroundTransparency = 1
    Logo.Image = "rbxassetid://76629081012708" -- 使用脚本Logo
    Logo.ImageTransparency = 1
    Logo.ZIndex = 2
    Logo.Parent = MainContainer
    
    local LogoCorner = Instance.new("UICorner")
    LogoCorner.CornerRadius = UDim.new(0.2, 0)
    LogoCorner.Parent = Logo
    
    local LogoStroke = Instance.new("UIStroke")
    LogoStroke.Color = Color3.fromRGB(100, 150, 255)
    LogoStroke.Thickness = 3
    LogoStroke.Transparency = 1
    LogoStroke.Parent = Logo
    
    -- 创建标题
    local Title = Instance.new("TextLabel")
    Title.Name = "Title"
    Title.AnchorPoint = Vector2.new(0.5, 0.5)
    Title.Position = UDim2.new(0.5, 0, 0.62, 0)
    Title.Size = UDim2.new(0.8, 0, 0, 50)
    Title.BackgroundTransparency = 1
    Title.Text = "陈某脚本"
    Title.TextColor3 = Color3.fromRGB(255, 255, 255)
    Title.TextSize = 42
    Title.Font = Enum.Font.GothamBold
    Title.TextTransparency = 1
    Title.TextStrokeTransparency = 0.7
    Title.TextStrokeColor3 = Color3.fromRGB(50, 50, 50)
    Title.ZIndex = 2
    Title.Parent = MainContainer
    
    -- 创建副标题
    local Subtitle = Instance.new("TextLabel")
    Subtitle.Name = "Subtitle"
    Subtitle.AnchorPoint = Vector2.new(0.5, 0.5)
    Subtitle.Position = UDim2.new(0.5, 0, 0.72, 0)
    Subtitle.Size = UDim2.new(0.8, 0, 0, 30)
    Subtitle.BackgroundTransparency = 1
    Subtitle.Text = "v2.3 FIN-WindUI版"
    Subtitle.TextColor3 = Color3.fromRGB(200, 200, 255)
    Subtitle.TextSize = 22
    Subtitle.Font = Enum.Font.GothamMedium
    Subtitle.TextTransparency = 1
    Subtitle.ZIndex = 2
    Subtitle.Parent = MainContainer
    
    -- 创建加载条背景
    local ProgressBarBackground = Instance.new("Frame")
    ProgressBarBackground.Name = "ProgressBarBackground"
    ProgressBarBackground.AnchorPoint = Vector2.new(0.5, 0.5)
    ProgressBarBackground.Position = UDim2.new(0.5, 0, 0.85, 0)
    ProgressBarBackground.Size = UDim2.new(0.7, 0, 0, 8)
    ProgressBarBackground.BackgroundColor3 = Color3.fromRGB(40, 40, 50)
    ProgressBarBackground.BackgroundTransparency = 1
    ProgressBarBackground.BorderSizePixel = 0
    ProgressBarBackground.ZIndex = 2
    ProgressBarBackground.Parent = MainContainer
    
    local ProgressBarCorner = Instance.new("UICorner")
    ProgressBarCorner.CornerRadius = UDim.new(1, 0)
    ProgressBarCorner.Parent = ProgressBarBackground
    
    -- 创建加载条
    local ProgressBar = Instance.new("Frame")
    ProgressBar.Name = "ProgressBar"
    ProgressBar.Size = UDim2.new(0, 0, 1, 0)
    ProgressBar.BackgroundColor3 = Color3.fromRGB(100, 150, 255)
    ProgressBar.BackgroundTransparency = 1
    ProgressBar.BorderSizePixel = 0
    ProgressBar.ZIndex = 3
    ProgressBar.Parent = ProgressBarBackground
    
    local ProgressBarCorner2 = Instance.new("UICorner")
    ProgressBarCorner2.CornerRadius = UDim.new(1, 0)
    ProgressBarCorner2.Parent = ProgressBar
    
    -- 创建加载文本
    local LoadingText = Instance.new("TextLabel")
    LoadingText.Name = "LoadingText"
    LoadingText.AnchorPoint = Vector2.new(0.5, 0.5)
    LoadingText.Position = UDim2.new(0.5, 0, 0.9, 0)
    LoadingText.Size = UDim2.new(0.7, 0, 0, 25)
    LoadingText.BackgroundTransparency = 1
    LoadingText.Text = "正在初始化..."
    LoadingText.TextColor3 = Color3.fromRGB(180, 180, 220)
    LoadingText.TextSize = 16
    LoadingText.Font = Enum.Font.Gotham
    LoadingText.TextTransparency = 1
    LoadingText.ZIndex = 2
    LoadingText.Parent = MainContainer
    
    -- 创建粒子效果容器
    local ParticleContainer = Instance.new("Frame")
    ParticleContainer.Name = "ParticleContainer"
    ParticleContainer.Size = UDim2.new(1, 0, 1, 0)
    ParticleContainer.BackgroundTransparency = 1
    ParticleContainer.Parent = LoadingScreen
    
    -- 动画函数
    local function animateIn()
        -- Logo淡入动画
        local logoFadeIn = TweenService:Create(Logo, TweenInfo.new(1.5, Enum.EasingStyle.Quint, Enum.EasingDirection.Out), {
            ImageTransparency = 0
        })
        
        local logoStrokeFadeIn = TweenService:Create(LogoStroke, TweenInfo.new(1.5, Enum.EasingStyle.Quint, Enum.EasingDirection.Out), {
            Transparency = 0
        })
        
        -- Logo缩放动画
        local logoScaleUp = TweenService:Create(Logo, TweenInfo.new(1, Enum.EasingStyle.Back, Enum.EasingDirection.Out, 0, false, 0.5), {
            Size = UDim2.new(0, 180, 0, 180)
        })
        
        -- 标题淡入动画
        local titleFadeIn = TweenService:Create(Title, TweenInfo.new(1.2, Enum.EasingStyle.Quad, Enum.EasingDirection.Out, 0, false, 0.8), {
            TextTransparency = 0
        })
        
        -- 副标题淡入动画
        local subtitleFadeIn = TweenService:Create(Subtitle, TweenInfo.new(1.2, Enum.EasingStyle.Quad, Enum.EasingDirection.Out, 0, false, 1), {
            TextTransparency = 0
        })
        
        -- 加载条背景淡入
        local progressBgFadeIn = TweenService:Create(ProgressBarBackground, TweenInfo.new(1, Enum.EasingStyle.Quad, Enum.EasingDirection.Out, 0, false, 1.2), {
            BackgroundTransparency = 0
        })
        
        -- 加载条淡入
        local progressBarFadeIn = TweenService:Create(ProgressBar, TweenInfo.new(1, Enum.EasingStyle.Quad, Enum.EasingDirection.Out, 0, false, 1.2), {
            BackgroundTransparency = 0
        })
        
        -- 加载文本淡入
        local loadingTextFadeIn = TweenService:Create(LoadingText, TweenInfo.new(1, Enum.EasingStyle.Quad, Enum.EasingDirection.Out, 0, false, 1.2), {
            TextTransparency = 0
        })
        
        -- 开始动画
        logoFadeIn:Play()
        logoStrokeFadeIn:Play()
        logoScaleUp:Play()
        
        task.wait(0.8)
        titleFadeIn:Play()
        
        task.wait(0.3)
        subtitleFadeIn:Play()
        
        task.wait(0.2)
        progressBgFadeIn:Play()
        progressBarFadeIn:Play()
        loadingTextFadeIn:Play()
        
        return true
    end
    
    -- 更新加载进度
    local function updateProgress(progress, text)
        local targetSize = UDim2.new(progress, 0, 1, 0)
        local tween = TweenService:Create(ProgressBar, TweenInfo.new(0.5, Enum.EasingStyle.Quad, Enum.EasingDirection.Out), {
            Size = targetSize
        })
        tween:Play()
        
        if text then
            LoadingText.Text = text
        end
    end
    
    -- 创建粒子效果
    local function createParticles()
        for i = 1, 15 do
            task.spawn(function()
                local particle = Instance.new("Frame")
                particle.Name = "Particle"
                particle.Size = UDim2.new(0, math.random(4, 10), 0, math.random(4, 10))
                particle.Position = UDim2.new(math.random(), 0, math.random(), 0)
                particle.BackgroundColor3 = Color3.fromRGB(100, 150, 255)
                particle.BackgroundTransparency = 0.6
                particle.BorderSizePixel = 0
                particle.ZIndex = 1
                
                local particleCorner = Instance.new("UICorner")
                particleCorner.CornerRadius = UDim.new(1, 0)
                particleCorner.Parent = particle
                
                particle.Parent = ParticleContainer
                
                -- 粒子漂浮动画
                while particle.Parent do
                    local targetPos = UDim2.new(
                        particle.Position.X.Scale + math.random(-0.1, 0.1),
                        0,
                        particle.Position.Y.Scale + math.random(-0.1, 0.1),
                        0
                    )
                    
                    local tween = TweenService:Create(particle, TweenInfo.new(2, Enum.EasingStyle.Sine, Enum.EasingDirection.InOut), {
                        Position = targetPos,
                        BackgroundTransparency = math.random(0.3, 0.8)
                    })
                    tween:Play()
                    
                    task.wait(math.random(1, 3))
                end
            end)
        end
    end
    
    -- 淡出动画
    local function animateOut()
        local fadeOutTime = 1.5
        
        -- 创建所有元素的淡出动画
        local fadeOutAnimations = {
            TweenService:Create(Logo, TweenInfo.new(fadeOutTime, Enum.EasingStyle.Quad, Enum.EasingDirection.In), {
                ImageTransparency = 1,
                Size = UDim2.new(0, 200, 0, 200)
            }),
            TweenService:Create(LogoStroke, TweenInfo.new(fadeOutTime, Enum.EasingStyle.Quad, Enum.EasingDirection.In), {
                Transparency = 1
            }),
            TweenService:Create(Title, TweenInfo.new(fadeOutTime, Enum.EasingStyle.Quad, Enum.EasingDirection.In), {
                TextTransparency = 1
            }),
            TweenService:Create(Subtitle, TweenInfo.new(fadeOutTime, Enum.EasingStyle.Quad, Enum.EasingDirection.In), {
                TextTransparency = 1
            }),
            TweenService:Create(ProgressBarBackground, TweenInfo.new(fadeOutTime, Enum.EasingStyle.Quad, Enum.EasingDirection.In), {
                BackgroundTransparency = 1
            }),
            TweenService:Create(ProgressBar, TweenInfo.new(fadeOutTime, Enum.EasingStyle.Quad, Enum.EasingDirection.In), {
                BackgroundTransparency = 1
            }),
            TweenService:Create(LoadingText, TweenInfo.new(fadeOutTime, Enum.EasingStyle.Quad, Enum.EasingDirection.In), {
                TextTransparency = 1
            }),
            TweenService:Create(BackgroundFrame, TweenInfo.new(fadeOutTime, Enum.EasingStyle.Quad, Enum.EasingDirection.In), {
                BackgroundTransparency = 1
            })
        }
        
        -- 播放所有淡出动画
        for _, anim in ipairs(fadeOutAnimations) do
            anim:Play()
        end
        
        -- 清除粒子
        for _, particle in ipairs(ParticleContainer:GetChildren()) do
            if particle:IsA("Frame") then
                particle:Destroy()
            end
        end
        
        -- 等待动画完成然后移除加载屏幕
        task.wait(fadeOutTime + 0.5)
        LoadingScreen:Destroy()
    end
    
    -- 开始动画
    task.spawn(function()
        createParticles()
        animateIn()
        
        -- 模拟加载过程
        updateProgress(0.1, "正在初始化界面...")
        task.wait(0.5)
        
        updateProgress(0.3, "正在加载脚本库...")
        task.wait(0.7)
        
        updateProgress(0.5, "正在准备功能模块...")
        task.wait(0.6)
        
        updateProgress(0.7, "正在初始化设置...")
        task.wait(0.5)
        
        updateProgress(0.9, "正在完成启动...")
        task.wait(0.8)
        
        updateProgress(1.0, "启动完成!")
        task.wait(1)
        
        animateOut()
    end)
    
    return {
        UpdateProgress = updateProgress,
        AnimateOut = animateOut
    }
end

-- 创建启动动画
local startupAnimation = CreateStartupAnimation()

-- 等待动画开始
task.wait(2)

-- ========== 加载FIN-WindUI库 ==========
local success, WindUI = pcall(function()
    return loadstring(game:HttpGet("https://raw.githubusercontent.com/finendss/FIN-Ui/refs/heads/main/FIN-WindUi", true))()
end)

if not success or not WindUI then
    -- 如果加载失败，尝试备用链接
    success, WindUI = pcall(function()
        return loadstring(game:HttpGet("https://raw.githubusercontent.com/finendss/FIN-Ui/main/FIN-WindUi", true))()
    end)
end

if not success or not WindUI then
    warn("无法加载FIN-WindUI库，请检查网络连接")
    return
end

-- 更新加载进度
if startupAnimation and startupAnimation.UpdateProgress then
    startupAnimation.UpdateProgress(0.3, "正在加载UI库...")
end

-- ========== 语言设置 ==========
local DefaultLanguage = "中文"
local Language = DefaultLanguage
local shouldAskToClose = true

-- 加载保存的语言
local function LoadSavedLanguage()
    pcall(function()
        if isfolder and isfolder("陈某脚本配置") and isfile and isfile("陈某脚本配置/配置.json") then
            local json = readfile("陈某脚本配置/配置.json")
            if json then
                local settings = game:GetService("HttpService"):JSONDecode(json)
                if settings and settings.Language then
                    return settings.Language
                end
            end
        end
    end)
    return DefaultLanguage
end

-- 保存语言设置
local function SaveLanguage(lang)
    Language = lang
    pcall(function()
        if makefolder and not isfolder("陈某脚本配置") then
            makefolder("陈某脚本配置")
        end
        if writefile then
            local HttpService = game:GetService("HttpService")
            local settings = {
                Language = lang,
                LastUpdate = os.time(),
                UserId = LocalPlayer.UserId,
                UserName = LocalPlayer.Name
            }
            writefile("陈某脚本配置/配置.json", HttpService:JSONEncode(settings))
        end
    end)
end

Language = LoadSavedLanguage() or DefaultLanguage

if startupAnimation and startupAnimation.UpdateProgress then
    startupAnimation.UpdateProgress(0.5, "正在加载语言设置...")
end

-- ========== 安全通知函数 ==========
local function SafeNotify(title, content, duration)
    duration = duration or 2
    
    WindUI:Notify({
        Title = title,
        Content = content,
        Duration = duration,
    })
end

-- ========== 复制文本函数 ==========
local function CopyToClipboard(text)
    pcall(function()
        if setclipboard then
            setclipboard(text)
            SafeNotify("复制成功", "已复制到剪贴板: " .. text, 2)
        else
            SafeNotify("复制失败", "不支持剪贴板功能", 2)
        end
    end)
end

-- ========== 聊天消息函数 ==========
local function SendSafeChatMessage(messageType)
    local success = false
    
    local safeMessages = {
        greeting = {
            "Greetings everyone!",
            "Hello there! Good to see you all!",
            "Welcome to the game! Have fun!",
            "Nice to meet you all!",
            "Hello everyone! Enjoy the game!"
        },
        test = {
            "Testing chat function!",
            "This is a test message.",
            "Chat test successful!",
            "Testing 1 2 3...",
            "Chat system working!"
        },
        general = {
            "Have a great time playing!",
            "Good luck everyone!",
            "Enjoy the game!",
            "Let's have some fun!",
            "Wishing everyone a good game!"
        }
    }
    
    local msgType = messageType or "general"
    local messageList = safeMessages[msgType] or safeMessages["general"]
    
    local randomIndex = math.random(1, #messageList)
    local selectedMessage = messageList[randomIndex]
    
    pcall(function()
        local channel = TextChatService.TextChannels:FindFirstChild("RBXGeneral")
        if channel then
            channel:SendAsync(selectedMessage)
            success = true
        end
    end)
    
    if not success then
        pcall(function()
            local chatEvents = ReplicatedStorage:FindFirstChild("DefaultChatSystemChatEvents")
            if chatEvents then
                local sayMessage = chatEvents:FindFirstChild("SayMessageRequest")
                if sayMessage then
                    sayMessage:FireServer(selectedMessage, "All")
                    success = true
                end
            end
        end)
    end
    
    if success then
        SafeNotify("消息已发送", "发送了安全消息", 1)
    else
        SafeNotify("发送失败", "无法发送聊天消息", 2)
    end
    
    return success, selectedMessage
end

-- ========== 脚本加载函数 ==========
local function EnhancedLoadScript(url, scriptName, askToClose)
    task.spawn(function()
        local success, result = pcall(function()
            local scriptContent = game:HttpGet(url, true)
            if scriptContent then
                return loadstring(scriptContent)()
            end
            return false
        end)
        
        if success then
            local successMsg = scriptName .. (Language == "English" and " loaded successfully!" or " 加载成功！")
            SafeNotify("脚本加载", successMsg, 2)
            
            print("脚本加载成功: " .. scriptName)
            print("来源: " .. url)
            print("时间: " .. os.date("%H:%M:%S"))
            
            if askToClose ~= false then
                AskToCloseScript(scriptName)
            end
        else
            SafeNotify("脚本加载", scriptName .. (Language == "English" and " failed to load!" or " 加载失败！"), 2)
        end
        
        return success
    end)
end

-- ========== 询问关闭函数 ==========
local function AskToCloseScript(scriptName)
    if not shouldAskToClose then
        return
    end
    
    task.wait(1)
    
    WindUI:Notify({
        Title = Language == "English" and "Script Loaded" or "脚本加载",
        Content = Language == "English" and 
            string.format("%s loaded successfully!\nDo you want to close Chen's Script UI?", scriptName) or
            string.format("%s 加载成功！\n是否关闭陈某脚本UI？", scriptName),
        Duration = 8,
        Callback = function(response)
            if response then
                if Window then
                    WindUI:Destroy()
                    SafeNotify("UI关闭", "陈某脚本UI已关闭", 2)
                    print("陈某脚本UI已关闭 (用户选择)")
                end
            else
                SafeNotify("UI保持", "陈某脚本UI保持开启", 2)
            end
        end,
        Buttons = {
            {
                Title = Language == "English" and "Yes" or "确定",
                Callback = function() return true end
            },
            {
                Title = Language == "English" and "No" or "取消",
                Callback = function() return false end
            }
        }
    })
end

-- ========== ESP透视功能 ==========
local function CreateESPBox(player)
    local character = player.Character
    if not character then return end
    
    local humanoidRootPart = character:FindFirstChild("HumanoidRootPart")
    if not humanoidRootPart then return end
    
    -- 创建Box
    local box = Instance.new("BoxHandleAdornment")
    box.Name = player.Name .. "_ESPBox"
    box.Adornee = humanoidRootPart
    box.AlwaysOnTop = true
    box.ZIndex = 10
    box.Size = Vector3.new(4, 6, 1)
    box.Transparency = 0.3
    box.Color3 = ESPManager.Colors.Enemy
    box.Parent = humanoidRootPart
    
    -- 创建名称标签
    local nameTag = Instance.new("BillboardGui")
    nameTag.Name = player.Name .. "_ESPName"
    nameTag.Adornee = humanoidRootPart
    nameTag.Size = UDim2.new(0, 200, 0, 50)
    nameTag.StudsOffset = Vector3.new(0, 4, 0)
    nameTag.AlwaysOnTop = true
    nameTag.MaxDistance = ESPManager.MaxDistance
    nameTag.Parent = humanoidRootPart
    
    local nameLabel = Instance.new("TextLabel")
    nameLabel.Name = "NameLabel"
    nameLabel.Size = UDim2.new(1, 0, 1, 0)
    nameLabel.BackgroundTransparency = 1
    nameLabel.Text = player.Name
    nameLabel.TextColor3 = ESPManager.Colors.Enemy
    nameLabel.TextSize = 16
    nameLabel.Font = Enum.Font.GothamBold
    nameLabel.TextStrokeTransparency = 0.5
    nameLabel.Parent = nameTag
    
    -- 创建血量条
    local healthBar = Instance.new("BillboardGui")
    healthBar.Name = player.Name .. "_ESPHealth"
    healthBar.Adornee = humanoidRootPart
    healthBar.Size = UDim2.new(0, 100, 0, 10)
    healthBar.StudsOffset = Vector3.new(0, 3, 0)
    healthBar.AlwaysOnTop = true
    healthBar.MaxDistance = ESPManager.MaxDistance
    healthBar.Parent = humanoidRootPart
    
    local healthBackground = Instance.new("Frame")
    healthBackground.Name = "HealthBackground"
    healthBackground.Size = UDim2.new(1, 0, 1, 0)
    healthBackground.BackgroundColor3 = Color3.fromRGB(50, 50, 50)
    healthBackground.BorderSizePixel = 1
    healthBackground.BorderColor3 = Color3.fromRGB(20, 20, 20)
    healthBackground.Parent = healthBar
    
    local healthFill = Instance.new("Frame")
    healthFill.Name = "HealthFill"
    healthFill.Size = UDim2.new(1, 0, 1, 0)
    healthFill.BackgroundColor3 = Color3.fromRGB(0, 255, 0)
    healthFill.BorderSizePixel = 0
    healthFill.Parent = healthBackground
    
    -- 存储到管理器
    ESPManager.Boxes[player] = box
    ESPManager.Names[player] = nameTag
    ESPManager.HealthBars[player] = healthBar
    
    return box, nameTag, healthBar
end

local function UpdateESPColor(player)
    local box = ESPManager.Boxes[player]
    local nameTag = ESPManager.Names[player]
    
    if box and nameTag then
        local color = ESPManager.Colors.Enemy
        
        -- 检查是否是队友（如果有团队系统）
        if ESPManager.TeamCheck then
            local localTeam = LocalPlayer.Team
            local playerTeam = player.Team
            
            if localTeam and playerTeam and localTeam == playerTeam then
                color = ESPManager.Colors.Team
            end
        end
        
        box.Color3 = color
        if nameLabel then
            nameLabel.TextColor3 = color
        end
    end
end

local function UpdateHealthBar(player)
    local character = player.Character
    if not character then return end
    
    local humanoid = character:FindFirstChild("Humanoid")
    local healthBar = ESPManager.HealthBars[player]
    
    if humanoid and healthBar then
        local healthFill = healthBar:FindFirstChild("HealthBackground"):FindFirstChild("HealthFill")
        if healthFill then
            local healthPercent = humanoid.Health / humanoid.MaxHealth
            healthFill.Size = UDim2.new(healthPercent, 0, 1, 0)
            
            -- 根据血量改变颜色
            if healthPercent > 0.5 then
                healthFill.BackgroundColor3 = Color3.fromRGB(0, 255, 0)
            elseif healthPercent > 0.25 then
                healthFill.BackgroundColor3 = Color3.fromRGB(255, 255, 0)
            else
                healthFill.BackgroundColor3 = Color3.fromRGB(255, 0, 0)
            end
        end
    end
end

local function RemoveESP(player)
    if ESPManager.Boxes[player] then
        ESPManager.Boxes[player]:Destroy()
        ESPManager.Boxes[player] = nil
    end
    
    if ESPManager.Names[player] then
        ESPManager.Names[player]:Destroy()
        ESPManager.Names[player] = nil
    end
    
    if ESPManager.HealthBars[player] then
        ESPManager.HealthBars[player]:Destroy()
        ESPManager.HealthBars[player] = nil
    end
    
    if ESPManager.Tracers[player] then
        ESPManager.Tracers[player]:Destroy()
        ESPManager.Tracers[player] = nil
    end
end

local function ToggleESP(state)
    ESPManager.Enabled = state
    
    if state then
        -- 为所有玩家创建ESP
        for _, player in ipairs(Players:GetPlayers()) do
            if player ~= LocalPlayer then
                CreateESPBox(player)
            end
        end
        
        -- 监听新玩家加入
        Players.PlayerAdded:Connect(function(player)
            task.wait(2) -- 等待角色加载
            CreateESPBox(player)
        end)
        
        -- 监听玩家离开
        Players.PlayerRemoving:Connect(function(player)
            RemoveESP(player)
        end)
        
        -- 更新循环
        RunService.RenderStepped:Connect(function()
            for player, box in pairs(ESPManager.Boxes) do
                local character = player.Character
                if character then
                    local humanoidRootPart = character:FindFirstChild("HumanoidRootPart")
                    if humanoidRootPart then
                        -- 更新颜色
                        UpdateESPColor(player)
                        
                        -- 更新血量
                        UpdateHealthBar(player)
                        
                        -- 更新可见性
                        local camera = Workspace.CurrentCamera
                        local distance = (humanoidRootPart.Position - camera.CFrame.Position).Magnitude
                        
                        local nameTag = ESPManager.Names[player]
                        local healthBar = ESPManager.HealthBars[player]
                        
                        if nameTag then
                            nameTag.Enabled = ESPManager.ShowName and distance <= ESPManager.MaxDistance
                        end
                        
                        if healthBar then
                            healthBar.Enabled = ESPManager.ShowHealth and distance <= ESPManager.MaxDistance
                        end
                        
                        if box then
                            box.Visible = ESPManager.ShowBox and distance <= ESPManager.MaxDistance
                        end
                    end
                end
            end
        end)
        
        SafeNotify("透视功能", "ESP透视已开启", 2)
    else
        -- 清除所有ESP
        for player, _ in pairs(ESPManager.Boxes) do
            RemoveESP(player)
        end
        
        -- 清空表格
        ESPManager.Boxes = {}
        ESPManager.Names = {}
        ESPManager.HealthBars = {}
        ESPManager.Tracers = {}
        
        SafeNotify("透视功能", "ESP透视已关闭", 2)
    end
end

-- ========== 碰撞箱修改功能 ==========
local function CreateHitbox(player)
    local character = player.Character
    if not character then return end
    
    local humanoidRootPart = character:FindFirstChild("HumanoidRootPart")
    if not humanoidRootPart then return nil end
    
    -- 创建碰撞箱
    local hitbox = Instance.new("Part")
    hitbox.Name = player.Name .. "_Hitbox"
    hitbox.Anchored = false
    hitbox.CanCollide = false
    hitbox.Transparency = 1.0
    hitbox.Size = Vector3.new(4, 6, 1) * HitboxManager.SizeMultiplier
    hitbox.Position = humanoidRootPart.Position
    hitbox.Parent = Workspace
    
    -- 创建约束
    local weld = Instance.new("Weld")
    weld.Name = "HitboxWeld"
    weld.Part0 = humanoidRootPart
    weld.Part1 = hitbox
    weld.C0 = CFrame.new()
    weld.C1 = CFrame.new()
    weld.Parent = hitbox
    
    -- 创建可视化碰撞箱（如果启用）
    if HitboxManager.ShowVisual then
        local visualBox = Instance.new("BoxHandleAdornment")
        visualBox.Name = player.Name .. "_HitboxVisual"
        visualBox.Adornee = hitbox
        visualBox.AlwaysOnTop = true
        visualBox.ZIndex = 5
        visualBox.Size = hitbox.Size
        visualBox.Transparency = HitboxManager.Transparency
        visualBox.Color3 = HitboxManager.Color
        visualBox.Parent = hitbox
        
        HitboxManager.VisualBoxes[player] = visualBox
    end
    
    HitboxManager.Hitboxes[player] = hitbox
    
    return hitbox
end

local function UpdateHitboxSize(player)
    local hitbox = HitboxManager.Hitboxes[player]
    if not hitbox then return end
    
    local originalSize = Vector3.new(4, 6, 1)
    hitbox.Size = originalSize * HitboxManager.SizeMultiplier
    
    -- 更新可视化碰撞箱
    local visualBox = HitboxManager.VisualBoxes[player]
    if visualBox then
        visualBox.Size = hitbox.Size
        visualBox.Transparency = HitboxManager.Transparency
        visualBox.Color3 = HitboxManager.Color
    end
end

local function UpdateHitboxVisibility(player)
    local visualBox = HitboxManager.VisualBoxes[player]
    if visualBox then
        visualBox.Visible = HitboxManager.ShowVisual
    end
end

local function RemoveHitbox(player)
    local hitbox = HitboxManager.Hitboxes[player]
    if hitbox then
        hitbox:Destroy()
        HitboxManager.Hitboxes[player] = nil
    end
    
    local visualBox = HitboxManager.VisualBoxes[player]
    if visualBox then
        visualBox:Destroy()
        HitboxManager.VisualBoxes[player] = nil
    end
end

local function ToggleHitboxes(state)
    HitboxManager.Enabled = state
    
    if state then
        -- 为所有玩家创建碰撞箱
        for _, player in ipairs(Players:GetPlayers()) do
            if player ~= LocalPlayer then
                CreateHitbox(player)
            end
        end
        
        -- 监听新玩家加入
        Players.PlayerAdded:Connect(function(player)
            task.wait(2) -- 等待角色加载
            CreateHitbox(player)
        end)
        
        -- 监听玩家离开
        Players.PlayerRemoving:Connect(function(player)
            RemoveHitbox(player)
        end)
        
        -- 监听玩家重生
        Players.PlayerAdded:Connect(function(player)
            player.CharacterAdded:Connect(function()
                task.wait(1) -- 等待角色完全加载
                if HitboxManager.Enabled then
                    RemoveHitbox(player)
                    CreateHitbox(player)
                end
            end)
        end)
        
        -- 为现有玩家添加角色监听
        for _, player in ipairs(Players:GetPlayers()) do
            if player.Character then
                player.CharacterAdded:Connect(function()
                    task.wait(1) -- 等待角色完全加载
                    if HitboxManager.Enabled then
                        RemoveHitbox(player)
                        CreateHitbox(player)
                    end
                end)
            end
        end
        
        -- 更新循环
        local updateConnection = RunService.Heartbeat:Connect(function()
            for player, hitbox in pairs(HitboxManager.Hitboxes) do
                local character = player.Character
                if character then
                    local humanoidRootPart = character:FindFirstChild("HumanoidRootPart")
                    if humanoidRootPart then
                        -- 确保碰撞箱跟随玩家
                        if hitbox.Parent ~= Workspace then
                            hitbox.Parent = Workspace
                        end
                    end
                end
            end
        end)
        
        HitboxManager.UpdateConnection = updateConnection
        
        SafeNotify("碰撞箱", "碰撞箱修改已开启", 2)
    else
        -- 清除所有碰撞箱
        for player, _ in pairs(HitboxManager.Hitboxes) do
            RemoveHitbox(player)
        end
        
        -- 清空表格
        HitboxManager.Hitboxes = {}
        HitboxManager.VisualBoxes = {}
        
        -- 断开更新连接
        if HitboxManager.UpdateConnection then
            HitboxManager.UpdateConnection:Disconnect()
            HitboxManager.UpdateConnection = nil
        end
        
        SafeNotify("碰撞箱", "碰撞箱修改已关闭", 2)
    end
end

-- 更新碰撞箱设置
local function UpdateHitboxSettings()
    for player, _ in pairs(HitboxManager.Hitboxes) do
        UpdateHitboxSize(player)
        UpdateHitboxVisibility(player)
    end
end

if startupAnimation and startupAnimation.UpdateProgress then
    startupAnimation.UpdateProgress(0.7, "正在准备功能模块...")
end

-- 显示启动弹窗
WindUI:Popup({
    Title = "陈某脚本",
    Icon = "sparkles",
    Content = "尊敬的：" .. game.Players.LocalPlayer.Name .. "\n欢迎使用陈某脚本 v2.3 FIN-WindUI版",
    Buttons = {
        {
            Title = "启动UI",
            Icon = "arrow-right",
            Variant = "Primary",
            Callback = function()
                print("启动陈某脚本UI")
                createMainWindow()
            end
        }
    }
})

if startupAnimation and startupAnimation.UpdateProgress then
    startupAnimation.UpdateProgress(0.85, "正在启动主界面...")
end

-- ========== 创建主窗口 ==========
function createMainWindow()
    if startupAnimation and startupAnimation.UpdateProgress then
        startupAnimation.UpdateProgress(0.9, "正在创建主窗口...")
    end
    
    local windowTitle = Language == "English" and "Chen's Script - Multi-function Center" or "陈某脚本 - 多功能脚本中心"
    
    Window = WindUI:CreateWindow({
        Title = windowTitle,
        Icon = "rbxassetid://4483362748",
        IconTransparency = 0.5,
        IconThemed = true,
        Author = "神秘（帮解忍者注入器）",
        Folder = "ChenScript",
        Size = UDim2.fromOffset(700, 500),
        Transparent = true,
        Theme = Language == "English" and "Light" or "Dark",
        User = {
            Enabled = true,
            Callback = function() 
                SafeNotify("用户信息", "点击了用户头像", 1)
            end,
            Anonymous = false
        },
        SideBarWidth = 200,
        ScrollBarEnabled = true,
        Background = "rbxassetid://76629081012708"
    })
    
    -- 时间标签
    local TimeTag = Window:Tag({
        Title = "00:00",
        Color = Color3.fromHex("#30ff6a")
    })
    
    -- 彩虹效果和时间更新
    local hue = 0
    task.spawn(function()
        while true do
            local now = os.date("*t")
            local hours = string.format("%02d", now.hour)
            local minutes = string.format("%02d", now.min)
            
            hue = (hue + 0.01) % 1
            local color = Color3.fromHSV(hue, 1, 1)
            
            TimeTag:SetTitle(hours .. ":" .. minutes)
            task.wait(0.06)
        end
    end)
    
    Window:Tag({
        Title = Language == "English" and "Chen Script v2.3" or "陈某脚本 v2.3",
        Color = Color3.fromHex("#315dff")
    })
    
    local UpdateTag = Window:Tag({
        Title = Language == "English" and "Cooperation: 582333520" or "合作群: 582333520",
        Color = Color3.fromHex("#000000")
    })
    
    task.wait(0.3)
    
    -- 编辑打开按钮
    Window:EditOpenButton({
        Title = Language == "English" and "Chen Script" or "陈某脚本",
        Icon = "monitor",
        CornerRadius = UDim.new(0,16),
        StrokeThickness = 2,
        Color = ColorSequence.new({
            ColorSequenceKeypoint.new(0, Color3.fromHex("FF0000")),
            ColorSequenceKeypoint.new(0.66, Color3.fromHex("0000FF")),
            ColorSequenceKeypoint.new(0.83, Color3.fromHex("4B0082")),
            ColorSequenceKeypoint.new(1, Color3.fromHex("9400D3"))
        }),
        Draggable = true,
    })
    
    task.wait(0.2)
    
    -- ========== 公告标签页 ==========
    local AnnouncementTab = Window:Tab({
        Title = Language == "English" and "Announcements" or "公告",
        Icon = "zap",
        Locked = false,
    })
    
    AnnouncementTab:Paragraph({
        Title = Language == "English" and "Copy Group Number" or "复制群号",
        Desc = Language == "English" and "Click to copy cooperation group number" or "点击复制合作群号码",
        ImageSize = 20,
        Color = "Grey",
        Buttons = {
            {
                Title = Language == "English" and "Copy" or "复制",
                Icon = "copy",
                Variant = "Tertiary",
                Callback = function()
                    setclipboard("582333520")
                    WindUI:Notify({
                        Title = Language == "English" and "Copied!" or "已复制！",
                        Content = Language == "English" and "Group number copied to clipboard" or "群号已复制到剪贴板",
                        Duration = 2
                    })
                end
            }
        }
    })
    
    -- 公告内容
    local announcementList = {
        {
            title = Language == "English" and "Script Update" or "脚本更新",
            content = Language == "English" and "Welcome to use Chen's Script v2.3 FIN-WindUI version!" or "欢迎使用陈某脚本 v2.3 FIN-WindUI版！",
            time = "2025-12-22"
        },
        {
            title = Language == "English" and "Cooperation Information" or "合作信息",
            content = Language == "English" and "Cooperation group: 582333520, welcome to join!" or "合作群聊: 582333520，欢迎加入！",
            time = "2025-12-22"
        },
        {
            title = Language == "English" and "Important Warning" or "重要警告",
            content = Language == "English" and "Please use scripts reasonably and follow game rules.\nThis script does NOT have anti-ban protection." or "请合理使用脚本，遵守游戏规则。\n本脚本不具有防封功能。",
            time = "2025-12-22"
        }
    }
    
    -- 添加公告信息
    AnnouncementTab:Paragraph({
        Title = announcementList[1].title,
        Desc = announcementList[1].content .. "\n" .. (Language == "English" and "Time: " or "时间: ") .. announcementList[1].time,
        ImageSize = 20,
        Color = "Blue"
    })
    
    AnnouncementTab:Paragraph({
        Title = announcementList[2].title,
        Desc = announcementList[2].content .. "\n" .. (Language == "English" and "Time: " or "时间: ") .. announcementList[2].time,
        ImageSize = 20,
        Color = "Orange"
    })
    
    AnnouncementTab:Paragraph({
        Title = announcementList[3].title,
        Desc = announcementList[3].content .. "\n" .. (Language == "English" and "Time: " or "时间: ") .. announcementList[3].time,
        ImageSize = 20,
        Color = "Red"
    })
    
    -- ========== 合作分支标签页 ==========
    local CooperationTab = Window:Tab({
        Title = Language == "English" and "Cooperation" or "合作分支",
        Icon = "drama",
        Locked = false,
    })
    
    CooperationTab:Paragraph({
        Title = Language == "English" and "Author Information" or "作者信息",
        Desc = "作者：神秘（帮解忍者注入器）\n合作脚本 Script (中文版)]脚本",
        ImageSize = 20,
        Color = "Grey"
    })
    
    CooperationTab:Button({
        Title = Language == "English" and "Copy Group Number" or "复制群聊号码",
        Default = true,
        Callback = function()
            CopyToClipboard("582333520")
        end
    })
    
    CooperationTab:Button({
        Title = Language == "English" and "Ninja Injector" or "忍者注入器",
        Default = false,
        Callback = function()
            EnhancedLoadScript("https://raw.githubusercontent.com/mystery-cooperation/ninja-injector/main/injector.lua", "忍者注入器")
        end
    })
    
    CooperationTab:Button({
        Title = Language == "English" and "Cooperation Hub" or "合作中心",
        Default = false,
        Callback = function()
            EnhancedLoadScript("https://raw.githubusercontent.com/mystery-cooperation/cooperation-hub/main/hub.lua", "合作中心")
        end
    })
    
    -- ========== LC脚本分支标签页 ==========
    local LCTab = Window:Tab({
        Title = "LC脚本分支",
        Icon = "book-open",
        Locked = false,
    })
    
    LCTab:Paragraph({
        Title = "Lexington and Concord 脚本",
        Desc = "加载Lexington and Concord游戏脚本\n点击下方按钮加载LC脚本",
        ImageSize = 20,
        Color = "Blue"
    })
    
    LCTab:Button({
        Title = "加载LC脚本",
        Default = true,
        Callback = function()
            EnhancedLoadScript("https://rawscripts.net/raw/Lexington-and-Concord-LC-75016", "LC脚本")
        end
    })
    
    -- ========== 工具脚本标签页 ==========
    local ToolsTab = Window:Tab({
        Title = Language == "English" and "Tool Scripts" or "工具脚本",
        Icon = "tool",
        Locked = false,
    })
    
    ToolsTab:Button({
        Title = Language == "English" and "Load Script" or "加载脚本",
        Default = false,
        Callback = function()
            EnhancedLoadScript("https://pastefy.app/s9PijnvT/raw", "外部脚本")
        end
    })
    
    ToolsTab:Button({
        Title = Language == "English" and "Dex Tool" or "Dex 工具",
        Default = false,
        Callback = function()
            EnhancedLoadScript("https://gitee.com/cmbhbh/cmbh/raw/master/Bex.lua", "Dex工具")
        end
    })
    
    ToolsTab:Button({
        Title = Language == "English" and "Pastebin Script" or "Pastebin 脚本",
        Default = false,
        Callback = function()
            EnhancedLoadScript("https://pastebin.com/raw/Up3P2KBp", "Pastebin脚本")
        end
    })
    
    -- ========== 游戏脚本标签页 ==========
    local GamesTab = Window:Tab({
        Title = Language == "English" and "Game Scripts" or "游戏脚本",
        Icon = "gamepad-2",
        Locked = false,
    })
    
    GamesTab:Button({
        Title = "Ink Game",
        Default = false,
        Callback = function()
            EnhancedLoadScript("https://raw.githubusercontent.com/VapeVoidware/VW-Add/main/inkgame.lua", "Ink Game脚本")
        end
    })
    
    GamesTab:Button({
        Title = "99 Nights",
        Default = false,
        Callback = function()
            EnhancedLoadScript("https://raw.githubusercontent.com/VapeVoidware/VW-Add/main/nightsintheforest.lua", "99 Nights脚本")
        end
    })
    
    GamesTab:Button({
        Title = "Ohio",
        Default = false,
        Callback = function()
            EnhancedLoadScript("https://github.com/DevSloPo/Main/raw/main/Ohio", "Ohio")
        end
    })
    
    GamesTab:Button({
        Title = "99 Nights 2",
        Default = false,
        Callback = function()
            EnhancedLoadScript("https://github.com/DevSloPo/Main/raw/main/99day", "99 Nights 2")
        end
    })
    
    GamesTab:Button({
        Title = Language == "English" and "Forsaken" or "被遗弃",
        Default = false,
        Callback = function()
            EnhancedLoadScript("https://raw.githubusercontent.com/qazwsx422/Je/26ab7022f3767d471f2fbb3d67e0683f0c13a55a/%E8%A2%AB%E9%81%97%E5%BC%83", "被遗弃脚本", true)
        end
    })
    
    -- ========== 强力脚本标签页 ==========
    local PowerTab = Window:Tab({
        Title = Language == "English" and "Powerful Scripts" or "强力脚本",
        Icon = "zap",
        Locked = false,
    })
    
    PowerTab:Button({
        Title = Language == "English" and "Kill Script (FengYu_HUB)" or "殺脚本 (FengYu_HUB)",
        Default = false,
        Callback = function()
            task.spawn(function()
                SafeNotify("脚本加载", "正在加载殺脚本...", 2)
                
                local function LoadFengYuScript()
                    local urls = {
                        "https://raw.githubusercontent.com/FengYu-3/FengYu/refs/heads/Feng/QQ1926190957",
                        "https://raw.githubusercontent.com/FengYu-3/FengYu/main/QQ1926190957",
                        "https://raw.githubusercontent.com/FengYu-3/FengYu/refs/heads/main/QQ1926190957"
                    }
                    
                    for _, url in ipairs(urls) do
                        local success, result = pcall(function()
                            FengYu_HUB = "殺脚本"
                            local scriptContent = game:HttpGet(url, true)
                            if scriptContent then
                                loadstring(scriptContent)()
                                return true
                            end
                            return false
                        end)
                        
                        if success and result == true then
                            return true
                        end
                    end
                    return false
                end
                
                local loaded = LoadFengYuScript()
                
                if loaded then
                    SafeNotify("脚本加载", "🎯 殺脚本 加载成功！", 3)
                    task.wait(1)
                    AskToCloseScript("殺脚本")
                else
                    SafeNotify("脚本加载", "❌ 殺脚本 加载失败", 3)
                end
            end)
        end
    })
    
    PowerTab:Button({
        Title = Language == "English" and "Sword Master Cracked" or "剑客破解版",
        Default = false,
        Callback = function()
            EnhancedLoadScript("https://raw.githubusercontent.com/eksan966/Sword_Guest/refs/heads/main/VIP", "剑客破解版")
        end
    })
    
    PowerTab:Button({
        Title = "Ez Hub",
        Default = false,
        Callback = function()
            EnhancedLoadScript("https://raw.githubusercontent.com/debug420/Ez-Hub/master/EzHub.lua", "Ez Hub")
        end
    })
    
    PowerTab:Button({
        Title = Language == "English" and "Death Script" or "死亡脚本",
        Default = false,
        Callback = function()
            EnhancedLoadScript("https://raw.githubusercontent.com/liuliuqiang404-code/sw/refs/heads/main/死亡.lua", "死亡脚本")
        end
    })
    
    PowerTab:Button({
        Title = "XK Hub",
        Default = false,
        Callback = function()
            EnhancedLoadScript("https://raw.githubusercontent.com/devslopo/DVES/main/XK Hub.lua", "XK Hub")
        end
    })
    
    -- ========== 枪战脚本标签页 ==========
    local GunfightTab = Window:Tab({
        Title = Language == "English" and "Gunfight Script" or "枪战脚本",
        Icon = "target",
        Locked = false,
    })
    
    -- ESP透视功能部分
    GunfightTab:Paragraph({
        Title = Language == "English" and "ESP Wallhack" or "ESP透视",
        Desc = Language == "English" and 
            "Enable player ESP with boxes, names and health bars.\nFeatures:\n• Player boxes\n• Name tags\n• Health bars\n• Team colors\n• Distance limit" or
            "启用玩家ESP透视，显示方框、名称和血量条。\n功能：\n• 玩家方框\n• 名称标签\n• 血量显示\n• 队伍颜色\n• 距离限制",
        ImageSize = 20,
        Color = "Red"
    })
    
    -- ESP开关
    GunfightTab:Toggle({
        Title = Language == "English" and "Enable ESP" or "启用ESP",
        Desc = Language == "English" and "Toggle ESP wallhack on/off" or "切换ESP透视开关",
        Value = false,
        Callback = function(state)
            ToggleESP(state)
        end
    })
    
    -- ESP设置
    GunfightTab:Toggle({
        Title = Language == "English" and "Show Name" or "显示名称",
        Desc = Language == "English" and "Show player names" or "显示玩家名称",
        Value = true,
        Callback = function(state)
            ESPManager.ShowName = state
            for _, nameTag in pairs(ESPManager.Names) do
                nameTag.Enabled = state and ESPManager.Enabled
            end
        end
    })
    
    GunfightTab:Toggle({
        Title = Language == "English" and "Show Box" or "显示方框",
        Desc = Language == "English" and "Show player boxes" or "显示玩家方框",
        Value = true,
        Callback = function(state)
            ESPManager.ShowBox = state
            for _, box in pairs(ESPManager.Boxes) do
                box.Visible = state and ESPManager.Enabled
            end
        end
    })
    
    GunfightTab:Toggle({
        Title = Language == "English" and "Show Health" or "显示血量",
        Desc = Language == "English" and "Show player health bars" or "显示玩家血量条",
        Value = true,
        Callback = function(state)
            ESPManager.ShowHealth = state
            for _, healthBar in pairs(ESPManager.HealthBars) do
                healthBar.Enabled = state and ESPManager.Enabled
            end
        end
    })
    
    GunfightTab:Toggle({
        Title = Language == "English" and "Team Check" or "队伍检测",
        Desc = Language == "English" and "Color teammates differently" or "队友显示不同颜色",
        Value = false,
        Callback = function(state)
            ESPManager.TeamCheck = state
            for player, _ in pairs(ESPManager.Boxes) do
                UpdateESPColor(player)
            end
        end
    })
    
    GunfightTab:Slider({
        Title = Language == "English" and "Max Distance" or "最大距离",
        Desc = Language == "English" and "Maximum ESP rendering distance" or "ESP渲染最大距离",
        Value = {
            Min = 100,
            Max = 5000,
            Default = 1000,
        },
        Step = 100,
        Callback = function(value)
            ESPManager.MaxDistance = value
            for _, nameTag in pairs(ESPManager.Names) do
                nameTag.MaxDistance = value
            end
            for _, healthBar in pairs(ESPManager.HealthBars) do
                healthBar.MaxDistance = value
            end
        end
    })
    
    -- 碰撞箱修改功能部分
    GunfightTab:Paragraph({
        Title = Language == "English" and "Hitbox Modifier" or "碰撞箱修改",
        Desc = Language == "English" and 
            "Modify player hitboxes to make them easier to hit.\nFeatures:\n• Adjust hitbox size\n• Visual hitbox display\n• Real-time updates\n• Auto-adjust for new players" or
            "修改玩家碰撞箱使其更容易被击中。\n功能：\n• 调整碰撞箱大小\n• 可视化碰撞箱显示\n• 实时更新\n• 自动适应新玩家",
        ImageSize = 20,
        Color = "Orange"
    })
    
    -- 碰撞箱开关
    GunfightTab:Toggle({
        Title = Language == "English" and "Enable Hitboxes" or "启用碰撞箱",
        Desc = Language == "English" and "Toggle hitbox modifier on/off" or "切换碰撞箱修改开关",
        Value = false,
        Callback = function(state)
            ToggleHitboxes(state)
        end
    })
    
    -- 碰撞箱大小
    GunfightTab:Slider({
        Title = Language == "English" and "Hitbox Size" or "碰撞箱大小",
        Desc = Language == "English" and "Adjust hitbox size multiplier" or "调整碰撞箱大小倍数",
        Value = {
            Min = 1.0,
            Max = 10.0,
            Default = 3.0,
        },
        Step = 0.1,
        Callback = function(value)
            HitboxManager.SizeMultiplier = value
            UpdateHitboxSettings()
        end
    })
    
    -- 显示可视化碰撞箱
    GunfightTab:Toggle({
        Title = Language == "English" and "Show Visual Hitboxes" or "显示可视化碰撞箱",
        Desc = Language == "English" and "Display visual hitbox outlines" or "显示碰撞箱轮廓",
        Value = false,
        Callback = function(state)
            HitboxManager.ShowVisual = state
            UpdateHitboxSettings()
        end
    })
    
    -- 碰撞箱透明度
    GunfightTab:Slider({
        Title = Language == "English" and "Hitbox Transparency" or "碰撞箱透明度",
        Desc = Language == "English" and "Adjust hitbox transparency" or "调整碰撞箱透明度",
        Value = {
            Min = 0.0,
            Max = 1.0,
            Default = 0.8,
        },
        Step = 0.05,
        Callback = function(value)
            HitboxManager.Transparency = value
            UpdateHitboxSettings()
        end
    })
    
    -- 碰撞箱颜色选择器
    GunfightTab:Paragraph({
        Title = Language == "English" and "Hitbox Color" or "碰撞箱颜色",
        Desc = Language == "English" and "Select hitbox color" or "选择碰撞箱颜色",
        ImageSize = 20,
        Color = "Blue"
    })
    
    GunfightTab:Button({
        Title = Language == "English" and "Red" or "红色",
        Desc = Language == "English" and "Set hitbox color to red" or "设置碰撞箱颜色为红色",
        Default = false,
        Callback = function()
            HitboxManager.Color = Color3.fromRGB(255, 0, 0)
            UpdateHitboxSettings()
            SafeNotify("碰撞箱", Language == "English" and "Hitbox color changed to red" or "碰撞箱颜色已更改为红色", 1)
        end
    })
    
    GunfightTab:Button({
        Title = Language == "English" and "Green" or "绿色",
        Desc = Language == "English" and "Set hitbox color to green" or "设置碰撞箱颜色为绿色",
        Default = false,
        Callback = function()
            HitboxManager.Color = Color3.fromRGB(0, 255, 0)
            UpdateHitboxSettings()
            SafeNotify("碰撞箱", Language == "English" and "Hitbox color changed to green" or "碰撞箱颜色已更改为绿色", 1)
        end
    })
    
    GunfightTab:Button({
        Title = Language == "English" and "Blue" or "蓝色",
        Desc = Language == "English" and "Set hitbox color to blue" or "设置碰撞箱颜色为蓝色",
        Default = false,
        Callback = function()
            HitboxManager.Color = Color3.fromRGB(0, 0, 255)
            UpdateHitboxSettings()
            SafeNotify("碰撞箱", Language == "English" and "Hitbox color changed to blue" or "碰撞箱颜色已更改为蓝色", 1)
        end
    })
    
    GunfightTab:Button({
        Title = Language == "English" and "Yellow" or "黄色",
        Desc = Language == "English" and "Set hitbox color to yellow" or "设置碰撞箱颜色为黄色",
        Default = false,
        Callback = function()
            HitboxManager.Color = Color3.fromRGB(255, 255, 0)
            UpdateHitboxSettings()
            SafeNotify("碰撞箱", Language == "English" and "Hitbox color changed to yellow" or "碰撞箱颜色已更改为黄色", 1)
        end
    })
    
    -- 高级枪战脚本部分
    GunfightTab:Paragraph({
        Title = Language == "English" and "Advanced Gunfight Script" or "高级枪战脚本",
        Desc = Language == "English" and "Load advanced gunfight script with Aimbot and other features" or "加载高级枪战脚本，包含自瞄等功能",
        ImageSize = 20,
        Color = "Blue"
    })
    
    GunfightTab:Button({
        Title = Language == "English" and "Load Gunfight Script" or "加载枪战脚本",
        Default = true,
        Callback = function()
            task.spawn(function()
                SafeNotify("枪战脚本", "正在加载枪战脚本...", 2)
                
                local success, result = pcall(function()
                    local scriptContent = game:HttpGet("https://raw.githubusercontent.com/qazwsx422/Je/41d501970d87fe25a52560b451764bbf4f430ac2/%E6%9E%AA%E6%88%98", true)
                    if scriptContent then
                        loadstring(scriptContent)()
                        return true
                    end
                    return false
                end)
                
                if success then
                    SafeNotify("枪战脚本", "🎯 枪战脚本 加载成功！", 3)
                    task.wait(1)
                    AskToCloseScript("枪战脚本")
                else
                    SafeNotify("枪战脚本", "❌ 枪战脚本 加载失败", 3)
                end
            end)
        end
    })
    
    -- ========== 通用功能标签页 ==========
    local FunctionsTab = Window:Tab({
        Title = Language == "English" and "General Functions" or "通用功能",
        Icon = "settings",
        Locked = false,
    })
    
    FunctionsTab:Button({
        Title = Language == "English" and "Send Welcome Message" or "发送欢迎消息",
        Default = false,
        Callback = function()
            SendSafeChatMessage("greeting")
        end
    })
    
    -- 无限跳跃功能
    local JumpEnabled = false
    local jumpConnection
    
    local function getHumanoid()
        local char = game.Players.LocalPlayer.Character
        return char and char:FindFirstChildOfClass("Humanoid") or nil
    end
    
    FunctionsTab:Toggle({
        Title = Language == "English" and "Infinite Jump" or "无限跳跃",
        Desc = Language == "English" and "Enable infinite jumping" or "启用无限跳跃功能",
        Value = false,
        Callback = function(state)
            JumpEnabled = state
            if state then
                WindUI:Notify({
                    Title = Language == "English" and "Function Enabled" or "功能已启用",
                    Content = Language == "English" and "Infinite jump enabled" or "无限跳跃已开启",
                    Icon = "check-circle",
                    Color = Color3.fromHex("#30ff6a"),
                    Duration = 2
                })
            else
                WindUI:Notify({
                    Title = Language == "English" and "Function Disabled" or "功能已关闭",
                    Content = Language == "English" and "Infinite jump disabled" or "无限跳跃已禁用",
                    Icon = "x-circle",
                    Color = Color3.fromHex("#ff3030"),
                    Duration = 2
                })
            end
            if jumpConnection then jumpConnection:Disconnect() end
            if state then
                jumpConnection = UserInputService.JumpRequest:Connect(function()
                    local success, humanoid = pcall(getHumanoid)
                    if success and humanoid and humanoid.Health > 0 then
                        humanoid:ChangeState(Enum.HumanoidStateType.Jumping)
                    end
                end)
            end
        end
    })
    
    FunctionsTab:Slider({
        Title = Language == "English" and "Field of View" or "视野广角",
        Desc = Language == "English" and "Adjust camera field of view" or "调整摄像机视野角度",
        Value = {
            Min = 70,
            Max = 120,
            Default = 70,
        },
        Increment = 1,
        Callback = function(v)
            game.Workspace.CurrentCamera.FieldOfView = v
        end
    })
    
    FunctionsTab:Slider({
        Title = Language == "English" and "Movement Speed" or "移动速度",
        Desc = Language == "English" and "Adjust character movement speed" or "调整角色移动速度",
        Value = {
            Min = 16.0,
            Max = 400.0,
            Default = 16.0,
        },
        Step = 1.0,
        Callback = function(value)
            local char = game.Players.LocalPlayer.Character
            if char and char:FindFirstChild("Humanoid") then
                char.Humanoid.WalkSpeed = value
            end
        end
    })
    
    FunctionsTab:Slider({
        Title = Language == "English" and "Gravity Settings" or "重力设置",
        Desc = Language == "English" and "Adjust world gravity" or "调整世界重力大小",
        Value = {
            Min = 1,
            Max = 500,
            Default = Workspace.Gravity
        },
        Step = 1,
        Callback = function(value)
            Workspace.Gravity = tonumber(value)
        end
    })
    
    -- 防甩飞功能
    local antiWalkFlingConn
    FunctionsTab:Toggle({
        Title = Language == "English" and "Anti-Fling" or "防甩飞",
        Desc = Language == "English" and "Prevent being flung by others" or "防止被其他玩家甩飞",
        Value = false,
        Callback = function(state)
            if state then
                if antiWalkFlingConn then antiWalkFlingConn:Disconnect() end
                local lastVelocity = Vector3.new()
                antiWalkFlingConn = RunService.Stepped:Connect(function()
                    local character = LocalPlayer.Character
                    local hrp = character and character:FindFirstChild("HumanoidRootPart")
                    if not hrp then return end
                    local currentVelocity = hrp.Velocity
                    if (currentVelocity - lastVelocity).Magnitude > 100 then
                        hrp.Velocity = lastVelocity
                    end
                    lastVelocity = currentVelocity
                end)
            else
                if antiWalkFlingConn then antiWalkFlingConn:Disconnect() end
            end
        end
    })
    
    -- 反挂机功能
    FunctionsTab:Button({
        Title = Language == "English" and "Anti-AFK v2" or "反挂机v2",
        Desc = Language == "English" and "Enable anti-AFK function" or "启用反挂机功能",
        Default = false,
        Callback = function()
            loadstring(game:HttpGet("https://pastebin.com/raw/9fFu43FF", true))()
            WindUI:Notify({
                Title = Language == "English" and "Notification" or "通知",
                Content = Language == "English" and "Anti-AFK v2 loaded successfully" or "反挂机v2功能加载成功",
                Duration = 3,
                Icon = "layout-grid",
            })        
        end
    })
    
    -- 甩飞功能
    FunctionsTab:Button({
        Title = Language == "English" and "Yeet Script" or "甩飞脚本",
        Desc = Language == "English" and "Load yeet/fling script" or "加载甩飞脚本功能",
        Default = false,
        Callback = function()
            task.spawn(function()
                SafeNotify("甩飞脚本", Language == "English" and "Loading yeet script..." or "正在加载甩飞脚本...", 2)
                
                local success, result = pcall(function()
                    loadstring(game:HttpGet('https://raw.githubusercontent.com/0Ben1/fe/main/obf_5wpM7bBcOPspmX7lQ3m75SrYNWqxZ858ai3tJdEAId6jSI05IOUB224FQ0VSAswH.lua.txt', true))()
                    return true
                end)
                
                if success then
                    SafeNotify("甩飞脚本", Language == "English" and "🎯 Yeet script loaded successfully!" or "🎯 甩飞脚本加载成功！", 3)
                    task.wait(1)
                    AskToCloseScript(Language == "English" and "Yeet Script" or "甩飞脚本")
                else
                    SafeNotify("甩飞脚本", Language == "English" and "❌ Yeet script failed to load" or "❌ 甩飞脚本加载失败", 3)
                end
            end)
        end
    })
    
    -- 夜视功能
    local nightVisionEnabled = false
    local function EnableNightVision()
        Lighting.Ambient = Color3.new(1, 1, 1)
        Lighting.Brightness = 2
        nightVisionEnabled = true
        WindUI:Notify({
            Title = Language == "English" and "Night Vision" or "夜视功能",
            Content = Language == "English" and "Night vision enabled" or "夜视功能已开启",
            Duration = 2
        })
    end
    
    local function DisableNightVision()
        Lighting.Ambient = Color3.new(0, 0, 0)
        Lighting.Brightness = 1
        nightVisionEnabled = false
        WindUI:Notify({
            Title = Language == "English" and "Night Vision" or "夜视功能",
            Content = Language == "English" and "Night vision disabled" or "夜视功能已关闭",
            Duration = 2
        })
    end
    
    FunctionsTab:Toggle({
        Title = Language == "English" and "Night Vision" or "夜视功能", 
        Desc = Language == "English" and "Enable night vision mode" or "启用夜视模式",
        Value = false, 
        Callback = function(Value)
            if Value then
                EnableNightVision()
            else
                DisableNightVision()
            end
        end
    })
    
    -- SY飞行功能
    FunctionsTab:Button({
        Title = Language == "English" and "SY Flight" or "SY飞行",
        Desc = Language == "English" and "Enable SY flight function" or "启用SY飞行功能",
        Default = false,
        Callback = function()
            loadstring(game:HttpGet("https://raw.githubusercontent.com/21sd/HanHud/2d7fd987b5a2f0bdfe10eaf8c8d19f57e520be7a/SY.lua", true))()
            WindUI:Notify({
                Title = Language == "English" and "Notification" or "通知",
                Content = Language == "English" and "Flight function loaded successfully" or "飞行功能加载成功",
                Duration = 3,
                Icon = "layout-grid",
            })        
        end
    })
    
    FunctionsTab:Button({
        Title = Language == "English" and "Reset Character" or "重置人物",
        Default = false,
        Callback = function()
            local character = LocalPlayer.Character
            if character then
                local humanoid = character:FindFirstChild("Humanoid")
                if humanoid then
                    humanoid.Health = 0
                    SafeNotify("重置", "角色正在重置", 2)
                end
            end
        end
    })
    
    FunctionsTab:Button({
        Title = Language == "English" and "Rejoin Server" or "重进服务器",
        Default = false,
        Callback = function()
            TeleportService:TeleportToPlaceInstance(
                game.PlaceId,
                game.JobId,
                LocalPlayer
            )
            SafeNotify("重进", "正在重新进入服务器", 2)
        end
    })
    
    -- ========== 设置中心标签页 ==========
    local SettingsTab = Window:Tab({
        Title = Language == "English" and "Settings Center" or "设置中心",
        Icon = "user-cog",
        Locked = false,
    })
    
    SettingsTab:Dropdown({
        Title = Language == "English" and "Select Language" or "选择语言",
        Values = { "中文", "English" },
        Value = Language,
        Callback = function(option) 
            local oldLanguage = Language
            Language = option
            SaveLanguage(option)
            
            WindUI:Notify({
                Title = Language == "English" and "Language Settings" or "语言设置",
                Content = (Language == "English" and "Language changed to: " or "语言已切换为: ") .. option,
                Duration = 4,
            })
        end
    })
    
    SettingsTab:Button({
        Title = Language == "English" and "Save Current Language" or "保存当前语言",
        Default = false,
        Callback = function()
            SaveLanguage(Language)
            SafeNotify("设置保存", "语言设置已保存", 2)
        end
    })
    
    SettingsTab:Toggle({
        Title = Language == "English" and "Ask to close after loading script" or "加载脚本后询问关闭",
        Desc = Language == "English" and "Show prompt to close UI after loading scripts" or "加载脚本后显示关闭UI提示",
        Value = true,
        Callback = function(state)
            shouldAskToClose = state
            WindUI:Notify({
                Title = Language == "English" and "Settings" or "设置",
                Content = state and (Language == "English" and "Ask to close enabled" or "已启用询问关闭功能") or (Language == "English" and "Ask to close disabled" or "已关闭询问关闭功能"),
                Icon = state and "check" or "x",
                Duration = 2
            })
        end
    })
    
    SettingsTab:Button({
        Title = Language == "English" and "Manual Close UI" or "手动关闭UI",
        Default = false,
        Callback = function()
            WindUI:Destroy()
            SafeNotify("UI关闭", "陈某脚本UI已手动关闭", 2)
        end
    })
    
    SettingsTab:Button({
        Title = Language == "English" and "Show Script Info" or "显示脚本信息",
        Default = false,
        Callback = function()
            local scriptCount = 48
            local info
            if Language == "English" then
                info = string.format("Chen's Script v2.3 FIN-WindUI Version\nTotal Functions: %d\nCurrent User: %s\nGame: %s\nCurrent Language: %s\nAuthor: Mysterious (Ninja Injector Cooperation)\nCooperation Group: 582333520\n\n⚠️ WARNING: This script does NOT have anti-ban protection!",
                    scriptCount, LocalPlayer.Name, game.Name, Language)
            else
                info = string.format("陈某脚本 v2.3 FIN-WindUI版\n功能总数: %d\n当前用户: %s\n游戏: %s\n当前语言: %s\n作者: 神秘（帮解忍者注入器）\n合作群聊: 582333520\n\n⚠️ 警告：本脚本不具有防封功能！",
                    scriptCount, LocalPlayer.Name, game.Name, Language)
            end
            
            WindUI:Notify({
                Title = Language == "English" and "Script Information" or "脚本信息",
                Content = info,
                Duration = 8,
                Icon = "alert-triangle"
            })
        end
    })
    
    SettingsTab:Button({
        Title = Language == "English" and "Reset All Settings" or "重置所有设置",
        Default = false,
        Callback = function()
            Language = DefaultLanguage
            SaveLanguage(DefaultLanguage)
            shouldAskToClose = true
            
            WindUI:Notify({
                Title = Language == "English" and "Reset Settings" or "重置设置",
                Content = Language == "English" and "All settings restored to default" or "所有设置已恢复默认值",
                Duration = 3,
            })
        end
    })
    
    -- 启动完成，关闭加载动画
    if startupAnimation and startupAnimation.UpdateProgress then
        startupAnimation.UpdateProgress(1.0, "启动完成!")
        task.wait(1)
        startupAnimation.AnimateOut()
    end
    
    -- ========== 特殊用户检测 ==========
    task.spawn(function()
        task.wait(5)
        
        local specialUsers = {
            ["qazwsx14736991"] = Language == "English" and "Script Developer" or "脚本制作者",
            ["zcbn826"] = Language == "English" and "Special User" or "特殊用户",
            ["jrhrvyvgjfj556"] = Language == "English" and "Special User" or "特殊用户",
            ["qwertyuiojj48"] = Language == "English" and "Special User" or "特殊用户"
        }
        
        local currentUser = LocalPlayer.Name
        
        if specialUsers[currentUser] then
            WindUI:Notify({
                Title = "🎉 " .. (Language == "English" and "Welcome" or "欢迎使用") .. " 🎉",
                Content = Language == "English" and "Thank you for using this script!\nAll functions are ready." or "感谢您使用本脚本！\n所有功能已准备就绪。",
                Duration = 5,
            })
            
            if currentUser == "qazwsx14736991" then
                task.wait(3)
                SendSafeChatMessage("greeting")
            end
        else
            print("普通用户登录: " .. currentUser)
        end
        
        -- 脚本启动日志
        print("=========================================")
        print(Language == "English" and "Chen's Script started successfully!" or "陈某脚本启动成功！")
        print(Language == "English" and "Version: v2.3 FIN-WindUI Version" or "版本: v2.3 FIN-WindUI版")
        print("作者: 神秘（帮解忍者注入器）")
        print("合作脚本 Script (中文版)]脚本")
        print("合作群聊: 582333520")
        print("当前用户: " .. LocalPlayer.Name)
        print("当前语言: " .. Language)
        print("通用功能数量: 48+")
        print("ESP透视功能: 已添加")
        print("碰撞箱修改功能: 已添加")
        print("询问关闭功能: " .. (shouldAskToClose and "已启用" or "已禁用"))
        print("聊天安全模式: 已启用")
        print("飞行功能: 已集成")
        print("枪战脚本功能: 已添加")
        print("甩飞脚本功能: 已添加")
        print("⚠️ 警告: 本脚本不具有防封功能")
        print("启动时间: " .. os.date("%Y-%m-%d %H:%M:%S"))
        print("=========================================")
        
        task.spawn(function()
            task.wait(3)
            WindUI:Notify({
                Title = Language == "English" and "Cooperation Information" or "合作信息",
                Content = Language == "English" and "Cooperation group available!\nJoin group: 582333520" or "合作分支已启用！\n加入群聊: 582333520",
                Duration = 4,
            })
        end)
    end)
    
    -- ========== 添加关注作者弹窗 ==========
    task.spawn(function()
        task.wait(8) -- 等待8秒后显示弹窗
        
        WindUI:Popup({
            Title = Language == "English" and "Follow the Author?" or "关注作者了吗",
            Icon = "info",
            Content = Language == "English" and 
                "If you find this script helpful, please consider following the author for more updates and support!\n\nThank you for using!" or
                "如果您觉得这个脚本对您有帮助，请考虑关注作者以获取更多更新和支持！\n\n感谢您的使用！",
            Buttons = {
                {
                    Title = Language == "English" and "Not Useful" or "没用",
                    Callback = function() 
                        print(Language == "English" and "User selected 'Not Useful'" or "用户选择了'没用'")
                        WindUI:Notify({
                            Title = Language == "English" and "Feedback" or "反馈",
                            Content = Language == "English" and "Thanks for your feedback!" or "感谢您的反馈！",
                            Duration = 2
                        })
                    end,
                    Variant = "Tertiary",
                },
                {
                    Title = Language == "English" and "Followed" or "关注了",
                    Icon = "arrow-right",
                    Callback = function() 
                        print(Language == "English" and "User selected 'Followed'" or "用户选择了'关注了'")
                        WindUI:Notify({
                            Title = Language == "English" and "Thank You!" or "谢谢！",
                            Content = Language == "English" and "Thank you for your support!" or "感谢您的支持！",
                            Duration = 2
                        })
                    end,
                    Variant = "Primary",
                }
            }
        })
    end)
    
    -- ========== 初始化完成 ==========
    print(Language == "English" and "Chen's Script v2.3 FIN-WindUI Version loaded successfully" or "陈某脚本 v2.3 FIN-WindUI版 已加载完成")
    print("作者: 神秘（帮解忍者注入器）")
    print("合作脚本 Script (中文版)]脚本")
    print("合作群聊: 582333520")
    print("询问关闭功能: " .. (shouldAskToClose and "已启用" or "已禁用"))
    print("聊天安全模式已启用")
    print("飞行功能已集成")
    print("枪战脚本功能已添加")
    print("ESP透视功能已添加")
    print("碰撞箱修改功能已添加")
    print("甩飞脚本功能已添加")
    print("⚠️ 警告: 本脚本不具有防封功能")
    print(Language == "English" and "48+ general functions ready" or "48+个通用功能已就绪")
    print("当前语言: " .. Language)
end

-- 直接创建主窗口（绕过弹窗）
task.wait(3)
createMainWindow()
