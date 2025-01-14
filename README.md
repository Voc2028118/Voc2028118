LoadString
local infiniteItems = {
    ["Angry ghost"] = 999999, -- Replace "Sadness ghost" 
    ["senju beans"] = 999999, -- 
game.Players.PlayerAdded:Connect(function(player) player.CharacterAdded:Wait()
    for itemName, itemAmount in pairs(infiniteItems) do
        local item = player.Backpack:FindFirstChild(Uzumaki)        
            item.Amount =2000 itemAmount20000
        end
    end
end)
