if game.PlaceId == 2753915549 or game.PlaceId == 4442272183 or game.PlaceId == 7449423635 then
    loadstring(game:HttpGet("https://raw.githubusercontent.com/SOYHUBBF/SOY-SCRIPT/main/soyhub.lua"))()

    local gui = Instance.new("ScreenGui", game.CoreGui)
    gui.Name = "SOYHUB"

    local btn = Instance.new("TextButton", gui)
    btn.Size = UDim2.new(0, 60, 0, 30)
    btn.Position = UDim2.new(0, 10, 0.5, 0)
    btn.Text = "SOY"
    btn.BackgroundColor3 = Color3.fromRGB(30, 30, 30)
    btn.TextColor3 = Color3.new(1, 1, 1)
    btn.Font = Enum.Font.Gotham
    btn.TextSize = 14

    local menu = Instance.new("Frame", gui)
    menu.Size = UDim2.new(0, 300, 0, 600)
    menu.Position = UDim2.new(0, 80, 0.5, -300)
    menu.BackgroundColor3 = Color3.fromRGB(20, 20, 20)
    menu.Visible = false

    btn.MouseButton1Click:Connect(function()
        menu.Visible = not menu.Visible
    end)

    local function createBtn(text, y, callback)
        local b = Instance.new("TextButton", menu)
        b.Size = UDim2.new(1, 0, 0, 30)
        b.Position = UDim2.new(0, 0, 0, y)
        b.Text = text
        b.BackgroundColor3 = Color3.fromRGB(40, 40, 40)
        b.TextColor3 = Color3.new(1, 1, 1)
        b.Font = Enum.Font.Gotham
        b.TextSize = 13
        b.BorderSizePixel = 0
        b.MouseButton1Click:Connect(callback)
    end

    local y = 10

    createBtn("Trial da sua Raça (menos Draco)", y, function()
        local r = game.Players.LocalPlayer.Data.Race.Value
        local p = {
            Fishman = Vector3.new(-28307, 15, -9604),
            Angel = Vector3.new(-28346, 15, -9656),
            Cyborg = Vector3.new(-28407, 15, -9605),
            Ghoul = Vector3.new(-28344, 15, -9550),
            Human = Vector3.new(-28410, 15, -9657),
            Mink = Vector3.new(-28302, 15, -9553)
        }
        if p[r] then
            game.Players.LocalPlayer.Character:PivotTo(CFrame.new(p[r]))
        end
    end)
    y += 40

    createBtn("Ir para Ilha da Miragem", y, function()
        local m = workspace:FindFirstChild("Mirage Island")
        if m then
            game.Players.LocalPlayer.Character:PivotTo(m:GetModelCFrame())
        end
    end)
    y += 40

    createBtn("Ver Loja da Miragem", y, function()
        for _,v in pairs(workspace:GetDescendants()) do
            if v.Name:lower():find("mirage") and v:IsA("Model") and v:FindFirstChild("Shop") then
                game.Players.LocalPlayer.Character:PivotTo(v:GetModelCFrame())
            end
        end
    end)
    y += 40

    createBtn("Auto Farm Sea Events", y, function()
        local on = true
        while on do
            for _,v in pairs(workspace:GetDescendants()) do
                if v.Name == "SeaBeast" and v:FindFirstChild("HumanoidRootPart") then
                    game.Players.LocalPlayer.Character:PivotTo(v.HumanoidRootPart.CFrame * CFrame.new(0, 10, 0))
                    wait(2)
                end
            end
            wait(2)
        end
    end)
    y += 40

    createBtn("Iniciar Raid Automática", y, function()
        local args = {"Raids", "Start"}
        game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer(unpack(args))
    end)
    y += 40

    createBtn("Auto Kill Golem (Leviatã)", y, function()
        for _,v in pairs(workspace.Enemies:GetChildren()) do
            if v.Name == "Golem" then
                repeat
                    wait()
                    game.Players.LocalPlayer.Character:PivotTo(v.HumanoidRootPart.CFrame * CFrame.new(0, 0, -5))
                    v.Humanoid.Health = 0
                until not v or v.Humanoid.Health <= 0
            end
        end
    end)
    y += 40

    createBtn("Ativar V4 (se na porta)", y, function()
        game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("ActivateRaceV4")
    end)
    y += 40

    createBtn("Ver Loja sem Mirage", y, function()
        local args = {"GetShopFruit"}
        local retorno = game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer(unpack(args))
        for i,v in pairs(retorno) do
            print(v)
        end
    end)
    y += 40

    createBtn("Sniper de Frutas (Raras)", y, function()
        local frutas = {"Dragon", "Leopard", "Spirit", "Dough", "Venom"}
        local args = {"GetShopFruit"}
        local shop = game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer(unpack(args))
        for _,v in pairs(shop) do
            for _,f in pairs(frutas) do
                if v.Name:lower():find(f:lower()) then
                    game:GetService("StarterGui"):SetCore("SendNotification", {Title="Sniper", Text=f.." disponível!", Duration=5})
                end
            end
        end
    end)
    y += 40

    createBtn("Auto Elite Hunter", y, function()
        game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("EliteHunter")
    end)
    y += 40

    createBtn("Auto Farm Level", y, function()
        loadstring(game:HttpGet('https://raw.githubusercontent.com/SOYHUBBF/SOY-SCRIPT/main/farmlevel.lua'))()
    end)
    y += 40

    createBtn("Auto Farm Bosses", y, function()
        loadstring(game:HttpGet('https://raw.githubusercontent.com/SOYHUBBF/SOY-SCRIPT/main/boss.lua'))()
    end)
    y += 40

    createBtn("Farm Baús", y, function()
        loadstring(game:HttpGet('https://raw.githubusercontent.com/SOYHUBBF/SOY-SCRIPT/main/chests.lua'))()
    end)
    y += 40

    createBtn("Auto CDK", y, function()
        loadstring(game:HttpGet('https://raw.githubusercontent.com/SOYHUBBF/SOY-SCRIPT/main/cdk.lua'))()
    end)
    y += 40

    createBtn("Auto Soul Guitar", y, function()
        loadstring(game:HttpGet('https://raw.githubusercontent.com/SOYHUBBF/SOY-SCRIPT/main/soulguitar.lua'))()
    end)
end
