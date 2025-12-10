-- Edward Script - Batata Hub (com Controle de Altura)
local RS = game:GetService("RunService")
local Players = game:GetService("Players")
local TS = game:GetService("TweenService")

local plr = Players.LocalPlayer
repeat task.wait() until plr.Character

local vooOn, espOn = false, false
local posSalva = nil
local velocidadeVoo = 26
local velocidadeTeleporte = 28
local alturaGO = 5 -- NOVA VARIÁVEL PARA ALTURA

-- LOADING SIMPLES
local sgLoading = Instance.new("ScreenGui")
sgLoading.Name = "EdwardLoading"
sgLoading.IgnoreGuiInset = true
sgLoading.ResetOnSpawn = false
sgLoading.DisplayOrder = 10
sgLoading.Parent = plr:WaitForChild("PlayerGui")

local bg = Instance.new("Frame")
bg.Size = UDim2.new(1,0,1,0)
bg.BackgroundColor3 = Color3.new(0,0,0)
bg.BorderSizePixel = 0
bg.Parent = sgLoading

local titulo = Instance.new("TextLabel")
titulo.Size = UDim2.new(0,500,0,100)
titulo.Position = UDim2.new(0.5,-250,0.4,0)
titulo.BackgroundTransparency = 1
titulo.Text = "🥔 BATATA HUB 🥔"
titulo.TextColor3 = Color3.fromRGB(255,200,0)
titulo.TextSize = 60
titulo.Font = Enum.Font.GothamBold
titulo.TextStrokeTransparency = 0
titulo.TextStrokeColor3 = Color3.new(0,0,0)
titulo.Parent = bg

local subTitulo = Instance.new("TextLabel")
subTitulo.Size = UDim2.new(0,400,0,50)
subTitulo.Position = UDim2.new(0.5,-200,0.5,0)
subTitulo.BackgroundTransparency = 1
subTitulo.Text = "Edward Script"
subTitulo.TextColor3 = Color3.fromRGB(0,200,255)
subTitulo.TextSize = 30
subTitulo.Font = Enum.Font.GothamBold
subTitulo.Parent = bg

-- ANIMAÇÃO DE ENTRADA
titulo.TextTransparency = 1
subTitulo.TextTransparency = 1

TS:Create(titulo, TweenInfo.new(1), {TextTransparency = 0}):Play()
task.wait(0.5)
TS:Create(subTitulo, TweenInfo.new(1), {TextTransparency = 0}):Play()
task.wait(2)

-- FADE OUT
TS:Create(bg, TweenInfo.new(0.5), {BackgroundTransparency = 1}):Play()
TS:Create(titulo, TweenInfo.new(0.5), {TextTransparency = 1}):Play()
TS:Create(subTitulo, TweenInfo.new(0.5), {TextTransparency = 1}):Play()
task.wait(0.6)

sgLoading:Destroy()
print("✅ Loading completo!")

-- GUI PRINCIPAL
local sg = Instance.new("ScreenGui", plr.PlayerGui)
sg.Name = "batata_hub"
sg.ResetOnSpawn = false

local batataBtn = Instance.new("TextButton", sg)
batataBtn.Size = UDim2.new(0,60,0,60)
batataBtn.Position = UDim2.new(0.5,-30,0.1,0)
batataBtn.BackgroundColor3 = Color3.fromRGB(30,30,35)
batataBtn.Text = "🥔"
batataBtn.TextSize = 35
batataBtn.Active = true
batataBtn.Draggable = true
batataBtn.Visible = false
Instance.new("UICorner", batataBtn).CornerRadius = UDim.new(1,0)

local batataStroke = Instance.new("UIStroke", batataBtn)
batataStroke.Color = Color3.fromRGB(0,200,255)
batataStroke.Thickness = 3

local main = Instance.new("Frame", sg)
main.Size = UDim2.new(0,220,0,280)
main.Position = UDim2.new(0.5,-110,0.5,-140)
main.BackgroundColor3 = Color3.fromRGB(20,20,25)
main.Active = true
main.Draggable = true
main.BackgroundTransparency = 0.1
Instance.new("UICorner", main).CornerRadius = UDim.new(0,12)

local mainStroke = Instance.new("UIStroke", main)
mainStroke.Color = Color3.fromRGB(0,200,255)
mainStroke.Thickness = 2

-- ABA DE VELOCIDADE (AGORA COM ALTURA)
local velocidadeFrame = Instance.new("Frame", sg)
velocidadeFrame.Size = UDim2.new(0,220,0,380) -- AUMENTADO PARA CABER A ALTURA
velocidadeFrame.Position = UDim2.new(0.5,-110,0.5,-190)
velocidadeFrame.BackgroundColor3 = Color3.fromRGB(20,20,25)
velocidadeFrame.Active = true
velocidadeFrame.Draggable = true
velocidadeFrame.BackgroundTransparency = 0.1
velocidadeFrame.Visible = false
Instance.new("UICorner", velocidadeFrame).CornerRadius = UDim.new(0,12)

local velStroke = Instance.new("UIStroke", velocidadeFrame)
velStroke.Color = Color3.fromRGB(255,100,0)
velStroke.Thickness = 2

local header = Instance.new("Frame", main)
header.Size = UDim2.new(1,0,0,35)
header.BackgroundColor3 = Color3.fromRGB(15,15,20)
Instance.new("UICorner", header).CornerRadius = UDim.new(0,12)

local iconeBatata = Instance.new("TextLabel", header)
iconeBatata.Size = UDim2.new(0,30,0,30)
iconeBatata.Position = UDim2.new(0,8,0,2)
iconeBatata.BackgroundTransparency = 1
iconeBatata.Text = "🥔"
iconeBatata.TextSize = 20
iconeBatata.Font = Enum.Font.GothamBold

local top = Instance.new("TextLabel", header)
top.Size = UDim2.new(1,-80,1,0)
top.Position = UDim2.new(0,40,0,0)
top.BackgroundTransparency = 1
top.Text = "batata hub"
top.TextColor3 = Color3.fromRGB(0,200,255)
top.TextSize = 14
top.Font = Enum.Font.GothamBold
top.TextXAlignment = Enum.TextXAlignment.Left

local btnFechar = Instance.new("TextButton", header)
btnFechar.Size = UDim2.new(0,30,0,30)
btnFechar.Position = UDim2.new(1,-35,0,2)
btnFechar.BackgroundColor3 = Color3.fromRGB(220,50,50)
btnFechar.Text = "×"
btnFechar.TextColor3 = Color3.new(1,1,1)
btnFechar.TextSize = 22
btnFechar.Font = Enum.Font.GothamBold
Instance.new("UICorner", btnFechar).CornerRadius = UDim.new(0,6)

-- HEADER DA ABA DE VELOCIDADE
local headerVel = Instance.new("Frame", velocidadeFrame)
headerVel.Size = UDim2.new(1,0,0,35)
headerVel.BackgroundColor3 = Color3.fromRGB(15,15,20)
Instance.new("UICorner", headerVel).CornerRadius = UDim.new(0,12)

local iconeVel = Instance.new("TextLabel", headerVel)
iconeVel.Size = UDim2.new(0,30,0,30)
iconeVel.Position = UDim2.new(0,8,0,2)
iconeVel.BackgroundTransparency = 1
iconeVel.Text = "⚡"
iconeVel.TextSize = 20
iconeVel.Font = Enum.Font.GothamBold

local topVel = Instance.new("TextLabel", headerVel)
topVel.Size = UDim2.new(1,-80,1,0)
topVel.Position = UDim2.new(0,40,0,0)
topVel.BackgroundTransparency = 1
topVel.Text = "configurações"
topVel.TextColor3 = Color3.fromRGB(255,100,0)
topVel.TextSize = 14
topVel.Font = Enum.Font.GothamBold
topVel.TextXAlignment = Enum.TextXAlignment.Left

local btnFecharVel = Instance.new("TextButton", headerVel)
btnFecharVel.Size = UDim2.new(0,30,0,30)
btnFecharVel.Position = UDim2.new(1,-35,0,2)
btnFecharVel.BackgroundColor3 = Color3.fromRGB(220,50,50)
btnFecharVel.Text = "×"
btnFecharVel.TextColor3 = Color3.new(1,1,1)
btnFecharVel.TextSize = 22
btnFecharVel.Font = Enum.Font.GothamBold
Instance.new("UICorner", btnFecharVel).CornerRadius = UDim.new(0,6)

local abaAberta = true
btnFechar.MouseButton1Click:Connect(function()
    abaAberta = false
    main.Visible = false
    batataBtn.Visible = true
end)

btnFecharVel.MouseButton1Click:Connect(function()
    velocidadeFrame.Visible = false
    batataBtn.Visible = true
end)

batataBtn.MouseButton1Click:Connect(function()
    abaAberta = true
    main.Visible = true
    batataBtn.Visible = false
end)

local function btn(txt, y, col)
    local b = Instance.new("TextButton", main)
    b.Size = UDim2.new(0.9,0,0,40)
    b.Position = UDim2.new(0.05,0,0,y)
    b.BackgroundColor3 = col
    b.Text = txt
    b.TextColor3 = Color3.new(1,1,1)
    b.TextSize = 13
    b.Font = Enum.Font.GothamBold
    b.BackgroundTransparency = 0.15
    Instance.new("UICorner", b).CornerRadius = UDim.new(0,8)
    
    local stroke = Instance.new("UIStroke", b)
    stroke.Color = Color3.fromRGB(0,200,255)
    stroke.Thickness = 1
    stroke.Transparency = 0.7
    
    return b
end

local b1 = btn("🚀 VOO", 80, Color3.fromRGB(30,30,40))
local b2 = btn("👁 ESP", 130, Color3.fromRGB(30,30,40))
local b3 = btn("📍 SAVE", 180, Color3.fromRGB(30,30,40))
local b4 = btn("✈ GO", 230, Color3.fromRGB(30,30,40))

-- BOTÃO PARA ABRIR ABA DE VELOCIDADE
local btnVelocidade = Instance.new("TextButton", main)
btnVelocidade.Size = UDim2.new(0.42,0,0,28)
btnVelocidade.Position = UDim2.new(0.05,0,0,42)
btnVelocidade.BackgroundColor3 = Color3.fromRGB(40,40,50)
btnVelocidade.Text = "⚙ CONFIG"
btnVelocidade.TextColor3 = Color3.fromRGB(255,200,0)
btnVelocidade.TextSize = 12
btnVelocidade.Font = Enum.Font.GothamBold
Instance.new("UICorner", btnVelocidade).CornerRadius = UDim.new(0,6)

btnVelocidade.MouseButton1Click:Connect(function()
    main.Visible = false
    velocidadeFrame.Visible = true
end)

-- BOTÃO VOLTAR NA ABA DE VELOCIDADE
local btnVoltar = Instance.new("TextButton", velocidadeFrame)
btnVoltar.Size = UDim2.new(0.42,0,0,28)
btnVoltar.Position = UDim2.new(0.53,0,0,42)
btnVoltar.BackgroundColor3 = Color3.fromRGB(40,40,50)
btnVoltar.Text = "← MENU"
btnVoltar.TextColor3 = Color3.fromRGB(0,200,255)
btnVoltar.TextSize = 12
btnVoltar.Font = Enum.Font.GothamBold
Instance.new("UICorner", btnVoltar).CornerRadius = UDim.new(0,6)

btnVoltar.MouseButton1Click:Connect(function()
    velocidadeFrame.Visible = false
    main.Visible = true
end)

-- CONTROLES DE VELOCIDADE VOO
local labelVoo = Instance.new("TextLabel", velocidadeFrame)
labelVoo.Size = UDim2.new(0.9,0,0,25)
labelVoo.Position = UDim2.new(0.05,0,0,80)
labelVoo.BackgroundTransparency = 1
labelVoo.Text = "🚀 Velocidade do Voo: " .. velocidadeVoo
labelVoo.TextColor3 = Color3.new(1,1,1)
labelVoo.TextSize = 13
labelVoo.Font = Enum.Font.GothamBold
labelVoo.TextXAlignment = Enum.TextXAlignment.Left

local sliderVoo = Instance.new("Frame", velocidadeFrame)
sliderVoo.Size = UDim2.new(0.9,0,0,6)
sliderVoo.Position = UDim2.new(0.05,0,0,115)
sliderVoo.BackgroundColor3 = Color3.fromRGB(50,50,60)
Instance.new("UICorner", sliderVoo).CornerRadius = UDim.new(1,0)

local fillVoo = Instance.new("Frame", sliderVoo)
fillVoo.Size = UDim2.new((velocidadeVoo-10)/90,0,1,0)
fillVoo.BackgroundColor3 = Color3.fromRGB(0,200,255)
fillVoo.BorderSizePixel = 0
Instance.new("UICorner", fillVoo).CornerRadius = UDim.new(1,0)

local btnMenosVoo = Instance.new("TextButton", velocidadeFrame)
btnMenosVoo.Size = UDim2.new(0,40,0,35)
btnMenosVoo.Position = UDim2.new(0.05,0,0,130)
btnMenosVoo.BackgroundColor3 = Color3.fromRGB(200,50,50)
btnMenosVoo.Text = "-"
btnMenosVoo.TextSize = 25
btnMenosVoo.TextColor3 = Color3.new(1,1,1)
btnMenosVoo.Font = Enum.Font.GothamBold
Instance.new("UICorner", btnMenosVoo).CornerRadius = UDim.new(0,8)

local btnMaisVoo = Instance.new("TextButton", velocidadeFrame)
btnMaisVoo.Size = UDim2.new(0,40,0,35)
btnMaisVoo.Position = UDim2.new(0.95,-40,0,130)
btnMaisVoo.BackgroundColor3 = Color3.fromRGB(50,200,50)
btnMaisVoo.Text = "+"
btnMaisVoo.TextSize = 25
btnMaisVoo.TextColor3 = Color3.new(1,1,1)
btnMaisVoo.Font = Enum.Font.GothamBold
Instance.new("UICorner", btnMaisVoo).CornerRadius = UDim.new(0,8)

btnMenosVoo.MouseButton1Click:Connect(function()
    velocidadeVoo = math.max(10, velocidadeVoo - 5)
    labelVoo.Text = "🚀 Velocidade do Voo: " .. velocidadeVoo
    fillVoo.Size = UDim2.new((velocidadeVoo-10)/90,0,1,0)
end)

btnMaisVoo.MouseButton1Click:Connect(function()
    velocidadeVoo = math.min(100, velocidadeVoo + 5)
    labelVoo.Text = "🚀 Velocidade do Voo: " .. velocidadeVoo
    fillVoo.Size = UDim2.new((velocidadeVoo-10)/90,0,1,0)
end)

-- CONTROLES DE VELOCIDADE TELEPORTE
local labelTele = Instance.new("TextLabel", velocidadeFrame)
labelTele.Size = UDim2.new(0.9,0,0,25)
labelTele.Position = UDim2.new(0.05,0,0,180)
labelTele.BackgroundTransparency = 1
labelTele.Text = "✈ Velocidade do GO: " .. velocidadeTeleporte
labelTele.TextColor3 = Color3.new(1,1,1)
labelTele.TextSize = 13
labelTele.Font = Enum.Font.GothamBold
labelTele.TextXAlignment = Enum.TextXAlignment.Left

local sliderTele = Instance.new("Frame", velocidadeFrame)
sliderTele.Size = UDim2.new(0.9,0,0,6)
sliderTele.Position = UDim2.new(0.05,0,0,215)
sliderTele.BackgroundColor3 = Color3.fromRGB(50,50,60)
Instance.new("UICorner", sliderTele).CornerRadius = UDim.new(1,0)

local fillTele = Instance.new("Frame", sliderTele)
fillTele.Size = UDim2.new((velocidadeTeleporte-10)/90,0,1,0)
fillTele.BackgroundColor3 = Color3.fromRGB(255,100,0)
fillTele.BorderSizePixel = 0
Instance.new("UICorner", fillTele).CornerRadius = UDim.new(1,0)

local btnMenosTele = Instance.new("TextButton", velocidadeFrame)
btnMenosTele.Size = UDim2.new(0,40,0,35)
btnMenosTele.Position = UDim2.new(0.05,0,0,230)
btnMenosTele.BackgroundColor3 = Color3.fromRGB(200,50,50)
btnMenosTele.Text = "-"
btnMenosTele.TextSize = 25
btnMenosTele.TextColor3 = Color3.new(1,1,1)
btnMenosTele.Font = Enum.Font.GothamBold
Instance.new("UICorner", btnMenosTele).CornerRadius = UDim.new(0,8)

local btnMaisTele = Instance.new("TextButton", velocidadeFrame)
btnMaisTele.Size = UDim2.new(0,40,0,35)
btnMaisTele.Position = UDim2.new(0.95,-40,0,230)
btnMaisTele.BackgroundColor3 = Color3.fromRGB(50,200,50)
btnMaisTele.Text = "+"
btnMaisTele.TextSize = 25
btnMaisTele.TextColor3 = Color3.new(1,1,1)
btnMaisTele.Font = Enum.Font.GothamBold
Instance.new("UICorner", btnMaisTele).CornerRadius = UDim.new(0,8)

btnMenosTele.MouseButton1Click:Connect(function()
    velocidadeTeleporte = math.max(10, velocidadeTeleporte - 5)
    labelTele.Text = "✈ Velocidade do GO: " .. velocidadeTeleporte
    fillTele.Size = UDim2.new((velocidadeTeleporte-10)/90,0,1,0)
end)

btnMaisTele.MouseButton1Click:Connect(function()
    velocidadeTeleporte = math.min(100, velocidadeTeleporte + 5)
    labelTele.Text = "✈ Velocidade do GO: " .. velocidadeTeleporte
    fillTele.Size = UDim2.new((velocidadeTeleporte-10)/90,0,1,0)
end)

-- ============== CONTROLES DE ALTURA DO GO ==============
local labelAltura = Instance.new("TextLabel", velocidadeFrame)
labelAltura.Size = UDim2.new(0.9,0,0,25)
labelAltura.Position = UDim2.new(0.05,0,0,280)
labelAltura.BackgroundTransparency = 1
labelAltura.Text = "📏 Altura do GO: " .. alturaGO .. " studs"
labelAltura.TextColor3 = Color3.new(1,1,1)
labelAltura.TextSize = 13
labelAltura.Font = Enum.Font.GothamBold
labelAltura.TextXAlignment = Enum.TextXAlignment.Left

local sliderAltura = Instance.new("Frame", velocidadeFrame)
sliderAltura.Size = UDim2.new(0.9,0,0,6)
sliderAltura.Position = UDim2.new(0.05,0,0,315)
sliderAltura.BackgroundColor3 = Color3.fromRGB(50,50,60)
Instance.new("UICorner", sliderAltura).CornerRadius = UDim.new(1,0)

local fillAltura = Instance.new("Frame", sliderAltura)
fillAltura.Size = UDim2.new((alturaGO)/50,0,1,0)
fillAltura.BackgroundColor3 = Color3.fromRGB(100,255,100)
fillAltura.BorderSizePixel = 0
Instance.new("UICorner", fillAltura).CornerRadius = UDim.new(1,0)

local btnMenosAltura = Instance.new("TextButton", velocidadeFrame)
btnMenosAltura.Size = UDim2.new(0,40,0,35)
btnMenosAltura.Position = UDim2.new(0.05,0,0,330)
btnMenosAltura.BackgroundColor3 = Color3.fromRGB(200,50,50)
btnMenosAltura.Text = "-"
btnMenosAltura.TextSize = 25
btnMenosAltura.TextColor3 = Color3.new(1,1,1)
btnMenosAltura.Font = Enum.Font.GothamBold
Instance.new("UICorner", btnMenosAltura).CornerRadius = UDim.new(0,8)

local btnMaisAltura = Instance.new("TextButton", velocidadeFrame)
btnMaisAltura.Size = UDim2.new(0,40,0,35)
btnMaisAltura.Position = UDim2.new(0.95,-40,0,330)
btnMaisAltura.BackgroundColor3 = Color3.fromRGB(50,200,50)
btnMaisAltura.Text = "+"
btnMaisAltura.TextSize = 25
btnMaisAltura.TextColor3 = Color3.new(1,1,1)
btnMaisAltura.Font = Enum.Font.GothamBold
Instance.new("UICorner", btnMaisAltura).CornerRadius = UDim.new(0,8)

btnMenosAltura.MouseButton1Click:Connect(function()
    alturaGO = math.max(0, alturaGO - 5)
    labelAltura.Text = "📏 Altura do GO: " .. alturaGO .. " studs"
    fillAltura.Size = UDim2.new(alturaGO/50,0,1,0)
end)

btnMaisAltura.MouseButton1Click:Connect(function()
    alturaGO = math.min(50, alturaGO + 5)
    labelAltura.Text = "📏 Altura do GO: " .. alturaGO .. " studs"
    fillAltura.Size = UDim2.new(alturaGO/50,0,1,0)
end)
-- =======================================================

-- VOO
local vooConn = nil
b1.MouseButton1Click:Connect(function()
    vooOn = not vooOn
    if vooOn then
        b1.Text = "✅ VOO ATIVO"
        b1.BackgroundColor3 = Color3.fromRGB(50,200,50)
        
        vooConn = RS.Heartbeat:Connect(function()
            local char = plr.Character
            if not char or not vooOn then return end
            local r = char:FindFirstChild("HumanoidRootPart")
            if r then
                local cam = workspace.CurrentCamera
                local vel = cam.CFrame.LookVector * velocidadeVoo
                pcall(function()
                    r.Velocity = vel
                end)
            end
        end)
    else
        b1.Text = "🚀 VOO"
        b1.BackgroundColor3 = Color3.fromRGB(30,30,40)
        if vooConn then vooConn:Disconnect() end
    end
end)

-- ESP
b2.MouseButton1Click:Connect(function()
    espOn = not espOn
    if espOn then
        b2.Text = "✅ ESP ATIVO"
        b2.BackgroundColor3 = Color3.fromRGB(50,200,50)
    else
        b2.Text = "👁 ESP"
        b2.BackgroundColor3 = Color3.fromRGB(30,30,40)
        for _,p in pairs(Players:GetPlayers()) do
            if p~=plr and p.Character then
                for _,v in pairs(p.Character:GetDescendants()) do
                    if v:IsA("Highlight") then v:Destroy() end
                end
            end
        end
    end
end)

-- SALVAR
b3.MouseButton1Click:Connect(function()
    local char = plr.Character
    if not char then return end
    local r = char:FindFirstChild("HumanoidRootPart")
    if r then
        posSalva = r.Position
        b3.Text = "✅ SALVO"
        b3.BackgroundColor3 = Color3.fromRGB(50,200,50)
        task.wait(1.5)
        b3.Text = "📍 SAVE"
        b3.BackgroundColor3 = Color3.fromRGB(30,30,40)
    end
end)

-- TELEPORTE (AGORA USA A ALTURA CONTROLADA)
local flutuando = false
local flutuarConn = nil
b4.MouseButton1Click:Connect(function()
    if not posSalva then return end
    
    flutuando = not flutuando
    if flutuando then
        b4.Text = "⏳ INDO..."
        b4.BackgroundColor3 = Color3.fromRGB(255,165,0)
        
        local posAlvo = posSalva + Vector3.new(0, alturaGO, 0) -- USANDO alturaGO
        
        flutuarConn = RS.Heartbeat:Connect(function()
            if not flutuando then return end
            local char = plr.Character
            if not char then return end
            local r = char:FindFirstChild("HumanoidRootPart")
            if not r then return end
            
            local dist = (posAlvo - r.Position).Magnitude
            if dist < 3 then
                flutuando = false
                if flutuarConn then flutuarConn:Disconnect() end
                b4.Text = "✅ CHEGOU"
                b4.BackgroundColor3 = Color3.fromRGB(50,200,50)
                task.wait(1.5)
                b4.Text = "✈ GO"
                b4.BackgroundColor3 = Color3.fromRGB(30,30,40)
            else
                local dir = (posAlvo - r.Position).Unit
                pcall(function()
                    r.Velocity = dir * velocidadeTeleporte
                end)
            end
        end)
    else
        b4.Text = "✈ GO"
        b4.BackgroundColor3 = Color3.fromRGB(30,30,40)
        if flutuarConn then flutuarConn:Disconnect() end
    end
end)

-- ESP LOOP
task.spawn(function()
    while task.wait(0.5) do
        if espOn then
            for _,p in pairs(Players:GetPlayers()) do
                if p~=plr and p.Character and not p.Character:FindFirstChild("Highlight") then
                    pcall(function()
                        local h = Instance.new("Highlight", p.Character)
                        h.FillColor = Color3.fromRGB(255,0,0)
                        h.FillTransparency = 0.6
                        h.OutlineTransparency = 0.3
                    end)
                end
            end
        end
    end
end)

print("✅ Edward Script carregado com controle de altura!")
