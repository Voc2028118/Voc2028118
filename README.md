
local var1 = game.Players.LocalPlayer.PlayerGui
local var2 = var1:WaitForChild("Abyss Dungeon"):WaitForChild("Frame")
local r_GetUnitStats_0 = require(game.ReplicatedStorage.Assets.CheckUnitModule.GetUnitStats)
local r_Dungeon_0 = require(game.ReplicatedStorage.Assets.CheckUnitModule.Stage_System.StageInfo.Dungeon)
local r_LoadBanList_0 = require(game.ReplicatedStorage.Modules.System.LoadBanList)
local var6 = nil
local var7 = false
function _G.LoadAbyss()
	
	if not var7 then
		local var8 = var2.Drop_List
		local function var22(arg9)
			
			var8:ClearAllChildren()
			var2.Yo.Info_Grid:Clone().Parent = var8
			local function var18(arg10, _)
				
				local var11 = r_GetUnitStats_0((tostring(arg10)))
				local var12 = var11.Status[1]
				local var13 = var11.Rank
				local var14 = game.ReplicatedStorage.Templete.UnitPreview:Clone()
				var14.Parent = var8
				var14.Name = tostring(arg10)
				var14.UnitName.Text = tostring(arg10)
				var14.Rarity.Text = var13
				local var15 = game.ReplicatedStorage.Assets.CheckUnitModule.Unit:FindFirstChild((tostring(arg10))):FindFirstChild("1"):FindFirstChild((tostring(arg10)))
				var15.Archivable = true
				local var16 = var15:Clone()
				local var17 = game.ReplicatedStorage.Templete:FindFirstChild(var12.Color)
				var14.Color.Image = var17.Image
				var14.Color:ClearAllChildren()
				var17.UIGradient:Clone().Parent = var14.Color
				if var13 == "C" then
					var14.Cash_Frame.ImageColor3 = Color3.new(1, 1, 1)
				elseif var13 == "R" then
					var14.Cash_Frame.ImageColor3 = Color3.new(0.290196, 0.941176, 1)
				elseif var13 == "SR" then
					var14.Cash_Frame.ImageColor3 = Color3.new(1, 0.898039, 0.101961)
				elseif var13 == "UR" then
					var14.Cash_Frame.ImageColor3 = Color3.new(1, 0.0313725, 0.0313725)
				elseif var13 == "SCR" then
					var14.Cash_Frame.ImageColor3 = Color3.new(1, 0.309804, 0.607843)
				elseif var13 == "LR" or var13 == "MR" then
					var14.Cash_Frame.ImageColor3 = Color3.new(1, 1, 1)
					if var14.Cash_Frame:FindFirstChild("Legendary") then
						if var13 == "MR" then
							var14.Cash_Frame:FindFirstChild("Legendary").Color = game.ReplicatedStorage.Templete.Miracle_Color.Color
						end
						var14.Cash_Frame:FindFirstChild("Legendary").Enabled = true
					end
				end
				var16.Parent = var14.ViewportFrame.WorldModel
				var16:SetPrimaryPartCFrame(CFrame.new(0.95, 3.5, -1.3))
			end
			for var19, var20 in pairs(arg9) do
				if var19 then
					if game.ReplicatedStorage.Assets.CheckUnitModule.Item_System.ItemPic:FindFirstChild(var19) then
						local var21 = game.ReplicatedStorage.Assets.CheckUnitModule.Item_System.ItemPic[var19]:Clone()
						var21.LayoutOrder = 1
						var21.Parent = var8
						var21.Count.Text = "x" .. var20
					elseif game.ReplicatedStorage.Assets.CheckUnitModule.Unit:FindFirstChild(var19) then
						var18(var19, var20)
					end
				end
			end
		end
		local function var27(arg23)
			
			local var24 = r_Dungeon_0.GetData(arg23)
			var2.Boss_Preview.Title.Text = var24.Boss
			var2.Layer_Text.Text = "Layer " .. arg23
			var2.Title_Text.Text = var24.Mode
			var2.Stage_Frame.StagePic.Image = var24.StageImage
			var2.Category_Text.Text = "[" .. var24.CategoryBuff .. "] Category"
			local var25 = game.ReplicatedStorage.Templete:FindFirstChild(var24.Color)
			var2.Color.Image = var25.Image
			var2.Color.ImageColor3 = var25.ImageColor3
			var2.Color:ClearAllChildren()
			var25.UIGradient:Clone().Parent = var2.Color
			var2.Boss_Preview.ViewportFrame.WorldModel:ClearAllChildren()
			local var26 = game.ReplicatedStorage.Assets.CheckUnitModule.Mob[var24.Boss]:Clone()
			var26.Parent = var2.Boss_Preview.ViewportFrame.WorldModel
			var26:SetPrimaryPartCFrame(CFrame.new(0.9, 3.5, -1.3))
			if var24.Boss == "Cow SeaBeast" then
				var26:SetPrimaryPartCFrame(CFrame.new(1.5, -5, 19))
			end
			var22(var24.Reward)
			var6 = arg23
		end
		(function()
			
			game:GetService("RunService"):IsStudio()
			local var28 = _G.Data.Cleared_Abyss + 1
			local var29 = math.clamp(var28, 1, 1000)
			for var30 = 1, var29 do
				local var31 = game.ReplicatedStorage.Templete.AbyssStageSelect:Clone()
				var31.LayoutOrder = 9999 - var30
				var31.Topic.Text = "Layer " .. var30
				var31.Parent = var2.StageList
				var31.Button.MouseButton1Click:Connect(function()
					
					local var32 = game.ReplicatedStorage.Assets.SoundEffects.Click:Clone()
					var32.Parent = workspace.CurrentCamera
					var32:Play()
					game.Debris:AddItem(var32, 10)
					var27(var30)
				end)
			end
			var27(var29)
			var7 = true
		end)()
		local var33 = nil
		var33 = var2.Play.MouseButton1Click:Connect(function()
			
			var33:Disconnect()
			local var34 = game.ReplicatedStorage.Assets.SoundEffects.Click:Clone()
			var34.Parent = workspace.CurrentCamera
			var34:Play()
			game.Debris:AddItem(var34, 10)
			game:GetService("RunService"):IsStudio()
			game.ReplicatedStorage.Remote.TeleportToStage:FireServer("Abyss_" .. var6)
		end)
	end
end
var2.Banlist.Activated:Connect(function()
	
	r_LoadBanList_0.LoadAbyssBanlsit()
	game.ReplicatedStorage.Assets.SoundEffects.Click:Play()
end)
var1.Banlist.BanlistList.Close.Click.Activated:Connect(function()
	
	r_LoadBanList_0.close()
	game.ReplicatedStorage.Assets.SoundEffects.Close:Play()
end)
