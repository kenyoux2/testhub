

--// Fluent
local Fluent = loadstring(game:HttpGet("https://github.com/dawid-scripts/Fluent/releases/latest/download/main.lua"))()
local SaveManager = loadstring(game:HttpGet("https://raw.githubusercontent.com/dawid-scripts/Fluent/master/Addons/SaveManager.lua"))()
local InterfaceManager = loadstring(game:HttpGet("https://raw.githubusercontent.com/dawid-scripts/Fluent/master/Addons/InterfaceManager.lua"))()

local Window = Fluent:CreateWindow({
    Title = "Zephyr Hub New Projects",
    SubTitle = "Version 2.0",
    TabWidth = 160,
    Size = UDim2.fromOffset(500, 350),
    Acrylic = false,
    Theme = "Dark",
    MinimizeKey = Enum.KeyCode.End
})
local Options = Fluent.Options
local Tabs = {
    Main = Window:AddTab({ Title = "Main", Icon = "home" }),
    Setting = Window:AddTab({ Title = "Setting", Icon = "settings" }),
}

_G.Settings = {
    Auto_Farm_Level = false,
}

--------------------------------------------------------------------------------------------------------------------------------------------

if game.PlaceId == 2753915549 then
    World1 = true
elseif game.PlaceId == 4442272183 then
    World2 = true
elseif game.PlaceId == 7449423635 then
    World3 = true
else
    game:Shutdown()
end

function LoadSettings()
	if readfile and writefile and isfile and isfolder then
		if not isfolder("Zephyr Hub Free Script") then
			makefolder("Zephyr Hub Free Script")
		end
		if not isfolder("Zephyr Hub Free Script/Blox Fruits/") then
			makefolder("Zephyr Hub Free Script/Blox Fruits/")
		end
		if not isfile("Zephyr Hub Free Script/Blox Fruits/" .. game.Players.LocalPlayer.Name .. ".json") then
			writefile("Zephyr Hub Free Script/Blox Fruits/" .. game.Players.LocalPlayer.Name .. ".json", game:GetService("HttpService"):JSONEncode(_G.Settings))
		else
			local Decode = game:GetService("HttpService"):JSONDecode(readfile("Zephyr Hub Free Script/Blox Fruits/" .. game.Players.LocalPlayer.Name .. ".json"))
			for i,v in pairs(Decode) do
				_G.Settings[i] = v
			end
		end
	else
		return warn("Status : Undetected Executor")
	end
end

function SaveSettings()
	if readfile and writefile and isfile and isfolder then
		if not isfile("Zephyr Hub Free Script/Blox Fruits/" .. game.Players.LocalPlayer.Name .. ".json") then
			LoadSettings()
		else
			local Decode = game:GetService("HttpService"):JSONDecode(readfile("Zephyr Hub Free Script/Blox Fruits/" .. game.Players.LocalPlayer.Name .. ".json"))
			local Array = {}
			for i,v in pairs(_G.Settings) do
				Array[i] = v
			end
			writefile("Zephyr Hub Free Script/Blox Fruits/" .. game.Players.LocalPlayer.Name .. ".json", game:GetService("HttpService"):JSONEncode(Array))
		end
	else
		return warn("Status : Undetected Executor")
	end
end

LoadSettings()

game:GetService("Players").LocalPlayer.Idled:connect(function()
	game:GetService("VirtualUser"):Button2Down(Vector2.new(0,0),workspace.CurrentCamera.CFrame)
	wait(1)
	game:GetService("VirtualUser"):Button2Up(Vector2.new(0,0),workspace.CurrentCamera.CFrame)
end)

if game:GetService("ReplicatedStorage").Effect.Container:FindFirstChild("Death") then
	game:GetService("ReplicatedStorage").Effect.Container.Death:Destroy()
end
if game:GetService("ReplicatedStorage").Effect.Container:FindFirstChild("Respawn") then
	game:GetService("ReplicatedStorage").Effect.Container.Respawn:Destroy()
end

__Function__ = {}

function __Function__:QuestCheck()
	local Lvl = game:GetService("Players").LocalPlayer.Data.Level.Value
	if Lvl >= 1 and Lvl <= 9 then
		if tostring(game.Players.LocalPlayer.Team) == "Marines" then
			MobName = "Trainee"
			QuestName = "MarineQuest"
			QuestLevel = 1
			Mon = "Trainee"
			NPCPosition = CFrame.new(-2709.67944, 24.5206585, 2104.24585, -0.744724929, -3.97967455e-08, -0.667371571, 4.32403588e-08, 1, -1.07884304e-07, 0.667371571, -1.09201515e-07, -0.744724929)
		elseif tostring(game.Players.LocalPlayer.Team) == "Pirates" then
			MobName = "Bandit"
			Mon = "Bandit"
			QuestName = "BanditQuest1"
			QuestLevel = 1
			NPCPosition = CFrame.new(1059.99731, 16.9222069, 1549.28162, -0.95466274, 7.29721794e-09, 0.297689587, 1.05190106e-08, 1, 9.22064114e-09, -0.297689587, 1.19340022e-08, -0.95466274)
		end
		return {
			[1] = QuestLevel,
			[2] = NPCPosition,
			[3] = MobName,
			[4] = QuestName,
			[5] = LevelRequire,
			[6] = Mon,
			[7] = MobCFrame
		}
	end
	if Lvl >= 375 and Lvl <= 399 then -- Fishman Warrior
		MobName = "Fishman Warrior"
		QuestName = "FishmanQuest"
		QuestLevel = 1
		Mon = "Fishman Warrior"
		NPCPosition = CFrame.new(61122.5625, 18.4716396, 1568.16504, 0.893533468, 3.95251609e-09, 0.448996574, -2.34327455e-08, 1, 3.78297464e-08, -0.448996574, -4.43233645e-08, 0.893533468)
		MobCFrame = CFrame.new(60955.0625, 48.7988472, 1543.7168, -0.831178129, 6.20639318e-09, -0.556006253, 7.20035302e-08, 1, -9.64761853e-08, 0.556006253, -1.20223305e-07, -0.831178129)
		if _G.Auto_Farm_Level and (NPCPosition.Position - game.Players.LocalPlayer.Character.HumanoidRootPart.Position).Magnitude > 3000 then
			game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("requestEntrance",Vector3.new(61163.8515625, 11.6796875, 1819.7841796875))
		end
		return {
			[1] = QuestLevel,
			[2] = NPCPosition,
			[3] = MobName,
			[4] = QuestName,
			[5] = LevelRequire,
			[6] = Mon,
			[7] = MobCFrame
		}
	elseif Lvl >= 15 and Lvl <= 29 then
		MobName = "Gorilla"
		QuestName = "JungleQuest"
		QuestLevel = 2
		Mon = "Gorilla"
		NPCPosition = CFrame.new(-1604.12012, 36.8521118, 154.23732, 0.0648873374, -4.70858913e-06, -0.997892559, 1.41431883e-07, 1, -4.70933674e-06, 0.997892559, 1.64442184e-07, 0.0648873374)
		MobCFrame = CFrame.new(-1142.0293, 40.5877495, -516.118103, 0.55559355, 7.58965513e-08, 0.831454039, 1.24594361e-08, 1, -9.96073553e-08, -0.831454039, 6.57006538e-08, 0.55559355)
		return {
			[1] = QuestLevel,
			[2] = NPCPosition,
			[3] = MobName,
			[4] = QuestName,
			[5] = LevelRequire,
			[6] = Mon,
			[7] = MobCFrame
		}
	elseif Lvl >= 400 and Lvl <= 449 then -- Fishman Commando
		MobName = "Fishman Commando"
		QuestName = "FishmanQuest"
		QuestLevel = 2
		Mon = "Fishman Commando"
		NPCPosition = CFrame.new(61122.5625, 18.4716396, 1568.16504, 0.893533468, 3.95251609e-09, 0.448996574, -2.34327455e-08, 1, 3.78297464e-08, -0.448996574, -4.43233645e-08, 0.893533468)
		MobCFrame = CFrame.new(61872.3008, 75.5976562, 1394.83484, -0.922134459, 4.36911973e-09, -0.38686946, -2.54707899e-08, 1, 7.20052e-08, 0.38686946, 7.62523484e-08, -0.922134459)
		if _G.Auto_Farm_Level and (NPCPosition.Position - game.Players.LocalPlayer.Character.HumanoidRootPart.Position).Magnitude > 3000 then
			game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("requestEntrance",Vector3.new(61163.8515625, 11.6796875, 1819.7841796875))
		end
		return {
			[1] = QuestLevel,
			[2] = NPCPosition,
			[3] = MobName,
			[4] = QuestName,
			[5] = LevelRequire,
			[6] = Mon,
			[7] = MobCFrame
		}
	end

	--game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("requestEntrance",Vector3.new(61163.8515625, 11.6796875, 1819.7841796875))
	local GuideModule = require(game:GetService("ReplicatedStorage").GuideModule)
	local Quests = require(game:GetService("ReplicatedStorage").Quests)
	for i,v in pairs(GuideModule["Data"]["NPCList"]) do
		for i1,v1 in pairs(v["Levels"]) do
			if Lvl >= v1 then
				if not LevelRequire then
					LevelRequire = 0
				end
				if v1 > LevelRequire then
					NPCPosition = i["CFrame"]
					QuestLevel = i1
					LevelRequire = v1
				end
				if #v["Levels"] == 3 and QuestLevel == 3 then
					NPCPosition = i["CFrame"]
					QuestLevel = 2
					LevelRequire = v["Levels"][2]
				end
			end
		end
	end
	for i,v in pairs(Quests) do
		for i1,v1 in pairs(v) do
			if v1["LevelReq"] == LevelRequire and i ~= "CitizenQuest" then
				QuestName = i
				for i2,v2 in pairs(v1["Task"]) do
					MobName = i2
					Mon = string.split(i2," [Lv. ".. v1["LevelReq"] .. "]")[1]
				end
			end
		end
	end
	if QuestName == "MarineQuest2" then
		QuestName = "MarineQuest2"
		QuestLevel = 1
		MobName = "Chief Petty Officer"
		Mon = "Chief Petty Officer"
		LevelRequire = 120
	elseif QuestName == "ImpelQuest" then
		QuestName = "PrisonerQuest"
		QuestLevel = 2
		MobName = "Dangerous Prisoner"
		Mon = "Dangerous Prisoner"
		LevelRequire = 210
		NPCPosition = CFrame.new(5310.60547, 0.350014925, 474.946594, 0.0175017118, 0, 0.999846935, 0, 1, 0, -0.999846935, 0, 0.0175017118)
	elseif QuestName == "SkyExp1Quest" then
		if QuestLevel == 1 then
			NPCPosition = CFrame.new(-4721.88867, 843.874695, -1949.96643, 0.996191859, -0, -0.0871884301, 0, 1, -0, 0.0871884301, 0, 0.996191859)
		elseif QuestLevel == 2 then
			NPCPosition = CFrame.new(-7859.09814, 5544.19043, -381.476196, -0.422592998, 0, 0.906319618, 0, 1, 0, -0.906319618, 0, -0.422592998)
		end
	elseif QuestName == "Area2Quest" and QuestLevel == 2 then
		QuestName = "Area2Quest"
		QuestLevel = 1
		MobName = "Swan Pirate"
		Mon = "Swan Pirate"
		LevelRequire = 775
	end
	MobName = MobName:sub(1,#MobName)
	return {
		[1] = QuestLevel,
		[2] = NPCPosition,
		[3] = MobName,
		[4] = QuestName,
		[5] = LevelRequire,
		[6] = Mon,
		[7] = MobCFrame
	}
end

function __Function__:Module()
    local Players = game.Players
    local Client = Players.localPlayer
    local Character = Client.Character
    local RootPart = Client.HumanoidRootPart
    local PlayerGui = Client.PlayerGui
    return { 
        [1] = Client, [2] = Character, [3] = RootPart, [4] = PlayerGui,
	}
end

function __Function__:EquipTools(tool)
	if not _G.NotAutoEquip then
		if game.Players.LocalPlayer.Backpack:FindFirstChild(tool) then
			local Tool_v = game.Players.LocalPlayer.Backpack:FindFirstChild(tool)
			wait(.1)
			game.Players.LocalPlayer.Character.Humanoid:EquipTool(Tool_v)
		end
	end
end

function __Function__:IsSameName(full, sub)
    return full:lower():sub(1, #sub) == sub:lower()
end

function __Function__:GetMobName(name, custom)
    local targetList = custom
    local nearest, minDist, minHealth = nil, math.huge, math.huge
    for _, target in ipairs(targetList) do
        local humanoid = target:FindFirstChildOfClass("Humanoid")
        if (not name or __Function__:IsSameName(target.Name, name) or name == "") and (not excludePlayer or target.Parent ~= game.workspac.Characters) then
            if humanoid and humanoid.Health > 0 then
                local targetPosition = humanoid.RootPart.Position
                local distanceToTarget = (targetPosition - game.Players.LocalPlayer.Character.HumanoidRootPart.Position).magnitude
                if distanceToTarget < minDist or (distanceToTarget - minDist < 50 and humanoid.Health < minHealth) then
                    minDist, minHealth, nearest = distanceToTarget, humanoid.Health, target
                end
            end
        end
    end
    return nearest
end

function __Function__:BTP(Position)
	game.Players.LocalPlayer.Character.Head:Destroy()
	game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = Position
	wait(0.5)
	game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = Position
	game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("SetSpawnPoint")
end

function __Function__:ToTarget(targetCFrame)
	Distance = (targetCFrame.Position - game.Players.LocalPlayer.Character.HumanoidRootPart.Position).Magnitude
	if game.Players.LocalPlayer.Character.Humanoid.Sit == true then game.Players.LocalPlayer.Character.Humanoid.Sit = false end
	pcall(function() tween = game:GetService("TweenService"):Create(game.Players.LocalPlayer.Character.HumanoidRootPart,TweenInfo.new(Distance/290, Enum.EasingStyle.Linear),{CFrame = targetCFrame}) end)
	tween:Play()
	if Distance <= 1 then
		tween:Cancel()
		game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = targetCFrame
	elseif Distance <= 100 then
		game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = targetCFrame
	end
	if _G.StopTween == true then
		tween:Cancel()
		_G.Clip = false
	end
end

function __Function__:AutoHaki()
    if not game:GetService("Players").LocalPlayer.Character:FindFirstChild("HasBuso") then
        game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("Buso")
    end
end

function __Function__:StopTween(target)
	if not target then
		__Function__:ToTarget(game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame)
		if game.Players.LocalPlayer.Character:FindFirstChild("Root") then
			game.Players.LocalPlayer.Character:FindFirstChild("Root"):Destroy()
		end
	end
end


canHits = {}
_G.FastAttack = true

_Module_ = function()
	local Success,Error = pcall(function()
		local PC = require(game.Players.LocalPlayer.PlayerScripts.CombatFramework.Particle)
		local RL = require(game:GetService("ReplicatedStorage").CombatFramework.RigLib)
		local DMG = require(game.Players.LocalPlayer.PlayerScripts.CombatFramework.Particle.Damage)
		local RigC = getupvalue(require(game.Players.LocalPlayer.PlayerScripts.CombatFramework.RigController), 2)
		local Combat = getupvalue(require(game.Players.LocalPlayer.PlayerScripts.CombatFramework), 2)
		local CameraShaker = require(game.ReplicatedStorage.Util.CameraShaker)
		local RigEvent = game:GetService("ReplicatedStorage").RigControllerEvent
		return {
			[1] = PC,
			[2] = RL,
			[3] = DMG,
			[4] = RigC,
			[5] = Combat,
			[6] = CameraShaker,
			[7] = RigEvent
		}
	end
	if not Success then
		warn("Module Error Send this message to mexuaita\n",Error)
	end
end

function GetPositionMob()
	local Hits = {}
	local nearbymon = false
	local Success,Error = pcall(function()
		if nearbymon then
			local Enemies = game.workspace.Enemies:GetChildren()
			local Characters = game.workspace.Characters:GetChildren()
			for i = 1, #Enemies do
				local v = Enemies[i]
				local Human = v:FindFirstChildOfClass("Humanoid")
				if Human and Human.RootPart and Human.Health > 0 and (v.HumanoidRootPart.Position - game.Players.LocalPlayer.Character.HumanoidRootPart.Position).Magnitude <= 50 then
					canHits[#canHits + 1] = Human.RootPart
				end
			end
			for i = 1, #Characters do
				local v = Characters[i]
				if v ~= game.Players.LocalPlayer.Character then
					local Human = v:FindFirstChildOfClass("Humanoid")
					if Human and Human.RootPart and Human.Health > 0 and (v.HumanoidRootPart.Position - game.Players.LocalPlayer.Character.HumanoidRootPart.Position).Magnitude <= 50 then
						canHits[#canHits + 1] = Human.RootPart
					end
				end
			end
		end
	end)
	if not Success then
		warn("Position Error Send this message to mexuaita\n",Error)
	end
	return Hits
end

task.spawn(function()
	local Success,Error = pcall(function()
		local Data = _Module_()[5]
		local Blank = function() end
		local Animation = Instance.new("Animation")
		local AttackCD = 0
		local Controller
		local lastFireValid = 0
		local MaxLag = 350
		local fucker = 0.07
		local TryLag = 0

		local resetCD = function()
			local WeaponName = Controller.currentWeaponModel.Name
			local Cooldown = {
				combat = 0.07
			}
			AttackCD = tick() + (fucker and Cooldown[WeaponName:lower()] or fucker or 0.285) + ((TryLag / MaxLag) * 0.3)
			_Module_()[7]:FireServer("weaponChange", WeaponName)
			TryLag = TryLag + 0.8
			task.delay((fucker or 0.285) + (TryLag + 0.5 / MaxLag) * 0.3, function()
				TryLag = TryLag - 0.8
			end)
		end

		if not shared.orl then
			shared.orl = _Module_()[2].wrapAttackAnimationAsync
		end

		if not shared.cpc then
			shared.cpc = _Module_()[1].play
		end

		if not shared.dnew then
			shared.dnew = _Module_()[3].new
		end

		if not shared.attack then
			shared.attack = _Module_()[4].attack
		end

		_Module_()[2].wrapAttackAnimationAsync = function(a, b, c, d, func)
			if not _G.FastAttack then
				_Module_()[1].play = shared.cpc
				return shared.orl(a, b, c, 50, func)
			end

			local Radius = _G.FastAttack or 50

			if canHits and #canHits > 0 then
				_Module_()[1].play = function() end
				a:Play(0.00075, 0.01, 0.01)
				func(canHits)
				wait(a.length * 0.5)
				a:Stop()
			end
		end

		while game:GetService("RunService").Stepped:Wait() do
			if #canHits > 0 then
				Controller = Data.activeController

				if Controller and Controller.equipped and Controller.currentWeaponModel then
					if _G.FastAttack then
						if _G.FastAttack and tick() > AttackCD then
							resetCD()
						end

						if tick() - lastFireValid > 0.5 or not _G.FastAttack then
							Controller.timeToNextAttack = 0
							Controller.hitboxMagnitude = 65
							pcall(task.spawn, Controller.attack, Controller)
							lastFireValid = tick()
							_Module_()[6]:Stop()
						end

						local AID3 = Controller.anims.basic[3]
						local AID2 = Controller.anims.basic[2]
						local ID = AID3 or AID2
						Animation.AnimationId = ID
						local Playing = Controller.humanoid:LoadAnimation(Animation)
						Playing:Play(0.00075, 0.01, 0.01)
						_Module_()[7]:FireServer("hit", canHits, AID3 and 3 or 2, "")
						delay(0.5, function()
							Playing:Stop()
						end)
					end
				end
			end
		end
	end)
	if not Success then
		warn("Fast Attack Error Send this message to mexuaita\n",Error)
	end
end)

function _C(Data)
    game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer(Data)
end

-- Example usage
local __FunctionMain__ = setmetatable({}, {__index = __Function__ })

-----------------------------------------------------------------------------------------------------------------------------

local Select_Weapon = Tabs.Main:AddDropdown("DropdownSelectWeapon", {
    Title = "Weapon",
    Values = {'Melee','Sword','Blox Fruit'},
    Multi = false,
    Default = 1,
})
Select_Weapon:SetValue('Melee')
Select_Weapon:OnChanged(function(Value)
    _G.Select_Weapon = Value
end)

spawn(function()
    while wait() do
        pcall(function()
            if _G.Select_Weapon == "Melee" then
                for i ,v in pairs(__FunctionMain__:Module()[1].Backpack:GetChildren()) do
                    if v.ToolTip == "Melee" then
                        if __FunctionMain__:Module()[1].Backpack:FindFirstChild(tostring(v.Name)) then
                            SelectWeapon = v.Name
                        end
                    end
                end
            elseif _G.Select_Weapon == "Sword" then
                for i ,v in pairs(__FunctionMain__:Module()[1].Backpack:GetChildren()) do
                    if v.ToolTip == "Sword" then
                        if __FunctionMain__:Module()[1].Backpack:FindFirstChild(tostring(v.Name)) then
                            SelectWeapon = v.Name
                        end
                    end
                end
            elseif _G.Select_Weapon == " Blox Fruit" then
                for i ,v in pairs(__FunctionMain__:Module()[1].Backpack:GetChildren()) do
                    if v.ToolTip == "Blox Fruit" then
                        if __FunctionMain__:Module()[1].Backpack:FindFirstChild(tostring(v.Name)) then
                            SelectWeapon = v.Name
                        end
                    end
                end
            else
                for i ,v in pairs(__FunctionMain__:Module()[1].Backpack:GetChildren()) do
                    if v.ToolTip == "Melee" then
                        if __FunctionMain__:Module()[1].Backpack:FindFirstChild(tostring(v.Name)) then
                            SelectWeapon = v.Name
                        end
                    end
                end
            end
        end)
    end
end)


local ToggleLevel = Tabs.Main:AddToggle("ToggleLevel", {
    Title = "Auto Level", 
    Default = _G.Settings.Auto_Farm_Level 
})
Options.ToggleLevel:SetValue(false)
QuestCheck()
spawn(function()
    while wait() do
        pcall(function()
            if _G.Auto_Farm_Level and game.Players.LocalPlayer.Data.Level < 300 then
                local __FunctionMain__ = __FunctionMain__ -- เพิ่มตรงนี้
                if __FunctionMain__ then
                    local module = __FunctionMain__:Module()
                    local questCheck = __FunctionMain__:QuestCheck()
                    if module[4].Main.Quest.Visible then
                        local questName = questCheck[3]
                        local enemy = game:GetService("Workspace").Enemies:FindFirstChild(questName)
                        if enemy then
                            local _x = __FunctionMain__:GetMobName(questName)
                            if _x and _x:FindFirstChild("Humanoid") and _x:FindFirstChild("HumanoidRootPart") and _x.Humanoid.Health > 0 then
                                repeat wait()
                                    if not string.find(module[4].Main.Quest.Container.QuestTitle.Title.Text, questCheck[6]) then
                                        _C("AbandonQuest")
                                    else
                                        local howFar = Step[1] or Vector3.new(0, 50, 0)
                                        if math.abs(_x.HumanoidRootPart.RootPart.Position.X - 1000) < 25 then
                                            local newPosition = _x.HumanoidRootPart.RootPart.Position + howFar + Vector3.new(math.random(-1, 1) / 4, 0, math.random(-1, 1) / 4)
                                            print(math.floor(newPosition.X), math.floor(newPosition.Y), math.floor(newPosition.Z))
                                        end
										PosMon = _x.HumanoidRootPart.CFrame
                                        __FunctionMain__:EquipTools(_G.Select_Weapon)
                                        __FunctionMain__:ToTarget(_x.HumanoidRootPart.RootPart.Position + howFar)
                                        if (_x.HumanoidRootPart.CFrame.Position - module[3].Position).Magnitude <= 50 then
                                            game:GetService("VirtualUser"):CaptureController()
                                            game:GetService("VirtualUser"):Button1Down(Vector2.new(1280, 672))
                                        end
                                    end
                                until not _G.Auto_Farm_Level or not _x.Parent or _x.Humanoid.Health <= 0 or game.Players.LocalPlayer.PlayerGui.Main.Quest.Visible == false
                            end
                        else
                            repeat
                                wait()
                                __FunctionMain__:ToTarget(questCheck[2])
                            until (questCheck[2].Position - module[3].Position).Magnitude <= 1 or not _G.Auto_Farm_Level
                        end
                    else
                        repeat
                            wait()
                            __FunctionMain__:ToTarget(questCheck[2])
                        until (questCheck[2].Position - module[3].Position).Magnitude <= 1 or not _G.Auto_Farm_Level
                        if (questCheck[2].Position - module[3].Position).Magnitude <= 10 then
                            wait(0.2)
                            _C("StartQuest", questCheck[4], questCheck[1])
                            wait(0.5)
                        else
                            repeat
                                wait()
                                __FunctionMain__:ToTarget(questCheck[2])
                            until (questCheck[2].Position - module[3].Position).Magnitude <= 1 or not _G.Auto_Farm_Level
                        end
                    end
                end
            else
                game.Players.localPlayer.kick(" Your level is over 300. \n Developer : Maruko ")
                task.wait(10.0)
                local ts = game:GetService("TeleportService")
                local p = game:GetService("Players").LocalPlayer
                ts:Teleport(game.PlaceId, p)
            end
        end)
    end
end)



spawn(function()
	while task.wait() do
		pcall(function()
			if _G.Bring_Mob then
				for i,v in pairs(game.Workspace.Enemies:GetChildren()) do
					if _G.Auto_Farm_Level and BringMobFarm and string.find(v.Name,__FunctionMain__:QuestCheck()()[3]) and (v.HumanoidRootPart.Position - PosMon.Position).Magnitude <= 250 and v:FindFirstChild("Humanoid") and v:FindFirstChild("HumanoidRootPart") and v.Humanoid.Health > 0 then	
						v.HumanoidRootPart.CFrame = PosMon
						v.HumanoidRootPart.CanCollide = false
						v.HumanoidRootPart.Size = Vector3.new(50, 50, 50)
						if v.Humanoid:FindFirstChild("Animator") then
							v.Humanoid.Animator:Destroy()
						end
						sethiddenproperty(game:GetService("Players").LocalPlayer,"SimulationRadius",math.huge)
					end
				end
			end
		end)
	end
end)

Options.ToggleLevel:SetValue(false)

SaveManager:SetLibrary(Fluent)
InterfaceManager:SetLibrary(Fluent)
SaveManager:IgnoreThemeSettings()
SaveManager:SetIgnoreIndexes({})
InterfaceManager:SetFolder("FluentScriptHub")
SaveManager:SetFolder("FluentScriptHub/specific-game")
InterfaceManager:BuildInterfaceSection(Tabs.Settings)
SaveManager:BuildConfigSection(Tabs.Settings)
Window:SelectTab(1)
Fluent:Notify({
	Title = "Zephyr Hub",
	Content = "Script Success ...",
	Duration = 8
})
SaveManager:LoadAutoloadConfig()

