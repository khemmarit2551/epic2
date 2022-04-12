--epic
if game.PlaceId == 537413528 then
	wait(1)
local blur = Instance.new("BlurEffect", game.Lighting)
blur.Size = 0
local ScreenGui = Instance.new("ScreenGui")
local ImageLabel = Instance.new("ImageLabel")
ScreenGui.Parent = game.CoreGui
ImageLabel.Parent = ScreenGui
ImageLabel.BackgroundColor3 = Color3.new(1, 1, 1)
ImageLabel.BackgroundTransparency = 1
ImageLabel.Position = UDim2.new(0.5, -(303 / 2), 0.5, -(263 / 2))
ImageLabel.Rotation = 0
ImageLabel.Size = UDim2.new(0, 303, 0, 263)
ImageLabel.Image = "rbxassetid://9166515678"
ImageLabel.ImageTransparency = 1

for i = 1, 50, 2 do
    blur.Size = i
    ImageLabel.ImageTransparency = ImageLabel.ImageTransparency - 0.1
    wait()
end
wait(0.1)

for i = 1, 50, 2 do
    blur.Size = 50 - i
    ImageLabel.ImageTransparency = ImageLabel.ImageTransparency + 0.1
    wait()
end
  
blur:Destroy()
ScreenGui:Destroy()

wait(1)

game.StarterGui:SetCore(
    "SendNotification",
    {
        Title = "Halo | No.1",
        Text = "Loading...",
		Icon = "rbxassetid://9166515678",
		Duration = 9
    }
)

wait(10)

	local library = loadstring(game:HttpGet("https://raw.githubusercontent.com/guitar555/Guitar-Hub/main/Main.lua"))()
	local venyx = library.new("Halo | No.1", 5013109572)
	
	local main = venyx:addPage("Main", 5012544693)
	local sectionmain1 = main:addSection("Main")
	local sectionmain2 = main:addSection("Player")
	local sectionmain3 = main:addSection("Music")
	local setting = venyx:addPage("Setting", 5012544693)
	local sectionsetting1 = setting:addSection("Setting")
	local theme = venyx:addPage("Theme", 5012544693)
	local colors = theme:addSection("Colors")
	
	Fly = false  
	
	sectionmain1:addToggle("Autofarm", false, function(vu)
		Autofarm = vu
	
		game:GetService("RunService").Stepped:connect(
			function()
				if Autofarm then
					game.Players.LocalPlayer.Character:WaitForChild("Humanoid"):ChangeState(11)
				end
			end
		)
		if Autofarm then
			ToxmodsisHOT()
		end
	
		if not Autofarm then
			game.Players.LocalPlayer.Character.Head:Destroy()
		end
		
		game.Players.LocalPlayer.CharacterAdded:Connect(
			function()
				repeat
					wait()
				until game.Players.LocalPlayer.Character
				wait(3)
				if Autofarm then
					ToxmodsisHOT()
				end
			end
		)
	end)
	
	sectionmain1:addDropdown("Chest", {"Common Chest", "Uncommon Chest", "Rare Chest", "Epic Chest", "Legendary Chest"}, function(abc)
		Chest = abc
	end)
	
	sectionmain1:addToggle("Open Chest",false,  function(vu)
		OpenChest = vu
		game:GetService('RunService').Stepped:connect(function()
			if OpenChest then
			workspace.ItemBoughtFromShop:InvokeServer(Chest,1)
			end 
			end)
	end)

	sectionmain1:addButton("Anti Afk",  function()
		loadstring(game:HttpGet("https://raw.githubusercontent.com/khemmarit2551/TELEPROT/main/anti%20afk"))()
    end)
	
	players = {}
	 
	for i,v in pairs(game:GetService("Players"):GetChildren()) do
	   table.insert(players,v.Name)
	end
	
	sectionmain2:addDropdown("Player", players, function(abc)
		Select = abc
	end)
	sectionmain2:addButton("Refresh",  function()
		table.clear(players)
	for i,v in pairs(game:GetService("Players"):GetChildren()) do
	   table.insert(players,v.Name)
	end
		end)
	
	sectionmain2:addButton("Teleport",  function()
		game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = game.Players[Select].Character.HumanoidRootPart.CFrame
	end)
	
	sectionmain2:addToggle("Fly", false, function(vu)
		Fly = vu
		activatefly()
	end)
	
	sectionmain2:addToggle("Infinity Jump", false, function(vu)
		Infinity = vu
		game:GetService("UserInputService").JumpRequest:connect(function()
			if Infinity then
				game:GetService"Players".LocalPlayer.Character:FindFirstChildOfClass'Humanoid':ChangeState("Jumping")
			end
		end) 
	end)
	
	sectionmain2:addToggle("Esp Player", false, function(Value)
		PlayerESP = Value
		while PlayerESP do wait()
			UpdatePlayer()
		end
	end)

	sectionmain3:addTextbox("Music Id", "Default", function(value)
	music = value
	end
	)

	local sm = Instance.new("Sound")
	sectionmain3:addButton("Play",  function()
		sm.Name = "Sound"
		sm.SoundId = "rbxassetid://"..music
		sm.Volume = 1000000000000000
		sm.archivable = false
		sm.Parent = game.Workspace
		sm:play()

	end)

	sectionmain3:addButton("Stop",  function()

		sm:Stop()

end)

	sectionmain3:addButton("Pause",  function()

	sm:Pause()

end)

sectionmain3:addButton("Resume",  function()

	sm:Resume()

end)

	sectionsetting1:addKeybind("Toggle Keybind", Enum.KeyCode.RightControl, function()
		venyx:toggle()
		end, function()
		end)
	
	local themes = {
	Background = Color3.fromRGB(24, 24, 24),
	Glow = Color3.fromRGB(0, 0, 0),
	Accent = Color3.fromRGB(10, 10, 10),
	LightContrast = Color3.fromRGB(20, 20, 20),
	DarkContrast = Color3.fromRGB(14, 14, 14),  
	TextColor = Color3.fromRGB(0, 255, 255)
	}
	
	
	for theme, color in pairs(themes) do -- all in one theme changer, i know, im cool
	colors:addColorPicker(theme, color, function(color3)
	venyx:setTheme(theme, color3)
	end)
	end
	
	-- load
	venyx:SelectPage(venyx.pages[1], true)
	
	Number = math.random(1,1000000)
	
	function UpdatePlayer()
		for i,v in pairs(game:GetService("Players"):GetChildren()) do
			pcall(function()
				if v.Character then
					if PlayerESP then
						if v.Character.Head and not v.Character.Head:FindFirstChild("PlayerESP"..Number) then
							local Bb = Instance.new("BillboardGui", v.Character.Head)
							Bb.Name = "PlayerESP"..Number
							Bb.ExtentsOffset = Vector3.new(0, 1, 0)
							Bb.Size = UDim2.new(1, 200, 1, 30)
							Bb.Adornee = v.Character.Head
							Bb.AlwaysOnTop = true
							local Textlb = Instance.new("TextLabel", Bb)
							Textlb.Font = "GothamBold"
							Textlb.FontSize = "Size14"
							Textlb.Text = v.Name.."\n"..math.round((v.Character.Head.Position - game:GetService("Players").LocalPlayer.Character.HumanoidRootPart.Position).Magnitude/3).." m."
							Textlb.Size = UDim2.new(1,0,1,0)
							Textlb.BackgroundTransparency = 1
							Textlb.TextStrokeTransparency = 0.5
							if v.Team == game:GetService("Players").LocalPlayer.Team then
								Textlb.TextColor3 = Color3.new(0, 255, 0)
							else
								Textlb.TextColor3 = Color3.new(0, 0, 204)
							end
						else
							v.Character.Head["PlayerESP"..Number].TextLabel.Text = v.Name.."\n"..math.round((v.Character.Head.Position - game:GetService('Players').LocalPlayer.Character.HumanoidRootPart.Position).Magnitude/3).." m."
						end
					else
						if v.Character.Head:FindFirstChild("PlayerESP"..Number) then
							v.Character.Head:FindFirstChild("PlayerESP"..Number):Destroy()
						end
					end
				end
			end)
		end
	end
	
	function activatefly()
		local mouse = game.Players.LocalPlayer:GetMouse''
		localplayer = game.Players.LocalPlayer
		game.Players.LocalPlayer.Character:WaitForChild("HumanoidRootPart")
		local torso = game.Players.LocalPlayer.Character.HumanoidRootPart
		local speedSET = 10
		local keys = {a = false, d = false, w = false, s = false}
		local e1
		local e2
		local function start()
			local pos = Instance.new("BodyPosition",torso)
			local gyro = Instance.new("BodyGyro",torso)
			pos.Name="EPIXPOS"
			pos.maxForce = Vector3.new(math.huge, math.huge, math.huge)
			pos.position = torso.Position
			gyro.maxTorque = Vector3.new(9e9, 9e9, 9e9)
			gyro.cframe = torso.CFrame
			repeat wait()
				localplayer.Character.Humanoid.PlatformStand = true
				local new = gyro.cframe - gyro.cframe.p + pos.position
				if not keys.w and not keys.s and not keys.a and not keys.d then
				   speed = 0
				end
				if keys.w then
				   new = new + workspace.CurrentCamera.CoordinateFrame.lookVector * speed
				   speed = speed+speedSET
				end
				if keys.s then
				   new = new - workspace.CurrentCamera.CoordinateFrame.lookVector * speed
				   speed = speed+speedSET
				end
				if keys.d then
				   new = new * CFrame.new(speed,0,0)
				   speed = speed+speedSET
				end
				if keys.a then
				   new = new * CFrame.new(-speed,0,0)
				   speed = speed+speedSET
				end
				if speed > speedSET then
				   speed = speedSET
				end
				   pos.position = new.p
				   if keys.w then
					   gyro.cframe = workspace.CurrentCamera.CoordinateFrame * CFrame.Angles(-math.rad(speed*15),0,0)
					elseif keys.s then
					   gyro.cframe = workspace.CurrentCamera.CoordinateFrame * CFrame.Angles(math.rad(speed*15),0,0)
					else
					gyro.cframe = workspace.CurrentCamera.CoordinateFrame
				end
			   until not Fly
			if gyro then 
				gyro:Destroy() 
			end
			if pos then 
				pos:Destroy() 
			end
			flying = false
			localplayer.Character.Humanoid.PlatformStand = false
			speed = 0
		end
		e1 = mouse.KeyDown:connect(function(key)
			if not torso or not torso.Parent then 
				flying = false
				e1:disconnect()
				e2:disconnect()
				return 
			end
			if key == "w" then
				keys.w = true
			elseif key == "s" then
				keys.s = true
			elseif key == "a" then
				keys.a = true
			elseif key == "d" then
				keys.d = true
			end
		end)
		e2 = mouse.KeyUp:connect(function(key)
			if key == "w" then
				keys.w = false
			elseif key == "s" then
				keys.s = false
			elseif key == "a" then
				keys.a = false
			elseif key == "d" then
				keys.d = false
			end
		end)
		start()
	end
	
	function ToxmodsisHOT()
		game.Players.LocalPlayer.Character:WaitForChild("HumanoidRootPart").CFrame = CFrame.new(-51.1823959, 80.6168747, -536.437805)
		tweenService, tweenInfo = game:GetService("TweenService"), TweenInfo.new(30, Enum.EasingStyle.Linear)
		tween =
			tweenService:Create(
			game:GetService("Players")["LocalPlayer"].Character:WaitForChild("HumanoidRootPart"),
			tweenInfo,
			{CFrame = CFrame.new(-60.5737877, 53.9498825, 8666.35059)}
		)
		tween:Play()
		wait(30)
		tweenService, tweenInfo = game:GetService("TweenService"), TweenInfo.new(0, Enum.EasingStyle.Linear)
		tween =
			tweenService:Create(
			game:GetService("Players")["LocalPlayer"].Character:WaitForChild("HumanoidRootPart"),
			tweenInfo,
			{CFrame = CFrame.new(-55.5486526, -360.063782, 9489.0498)}
		)
		tween:Play()
		
	end
	
	spawn(function()
		while wait(0.3) do 
			pcall(function()
				if Autofarm then
					local Xd = Instance.new("Part")
					Xd.Name = "xd"
					Xd.Parent = game.Workspace
					Xd.Anchored = true
					Xd.Color = Color3.fromRGB(255, 255, 0)
					Xd.Size = Vector3.new(15,0.5,15)
					Xd.Material = "Neon"
					Xd.Transparency = 1
					if (game.Players.LocalPlayer.Character.HumanoidRootPart.Position-game.Workspace["xd"].Position).Magnitude > 5  then
						game.Workspace["xd"].CFrame = CFrame.new(game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame.X,game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame.Y - 3.3,game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame.Z)
					end
					
				else
					if game:GetService("Workspace").xd then
						game:GetService("Workspace").xd:Destroy()
					end
				end
			end)
		end
	end)

	else
		game.Players.LocalPlayer:Kick("Halo | No.1 สคริปไม่มีแมพนี้")
	end
