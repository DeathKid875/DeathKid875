Local ID = game.PlaceId
local baseURL = "https://raw.githubusercontent.com/YOUR_USERNAME/YOUR_REPO_NAME/main/" -- DeathKid
local Players = game:GetService("Players")
local plr = Players.LocalPlayer

function GetGame()
    if ID == 1234567890 then -- blue lock
        return "MyGameScript.lua" -- DeathKid
    else
        print("Game is not supported.")
        return nil
    end
end

local gameScript = GetGame()

if gameScript then
    loadstring(game:HttpGet(baseURL .. gameScript))()
end

for _, v in next, getconnections(plr.Idled) do
    v:Disable()
end

local VirtualUser = game:GetService("VirtualUser")
local status = getgenv().afk_toggle
if status == nil then
    getgenv().afk_toggle = false
end

if not plr then
    error("Failed to get LocalPlayer reference")
end

plr.Idled:Connect(function()
    if not getgenv().afk_toggle then return end
    pcall(function()
        VirtualUser:CaptureController()
        VirtualUser:ClickButton2(Vector2.new())
    end)
end)
