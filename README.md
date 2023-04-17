


if not game:IsLoaded() then
    game.Loaded:Wait()
end
repeat
    wait()
until game.Players
repeat
    wait()
until game.Players.LocalPlayer
repeat
    wait()
until game.ReplicatedStorage
repeat
    wait()
until game.ReplicatedStorage:FindFirstChild("Remotes");
repeat
    wait()
until game.Players.LocalPlayer:FindFirstChild("PlayerGui");
repeat
    wait()
until game.Players.LocalPlayer.PlayerGui:FindFirstChild("Main");

wait(1)

if not game:IsLoaded() then
    repeat
        game.Loaded:Wait()
    until game:IsLoaded()
end

if game:GetService("Players").LocalPlayer.PlayerGui.Main:FindFirstChild("ChooseTeam") then
    repeat
        wait()
        if game:GetService("Players").LocalPlayer.PlayerGui:WaitForChild("Main").ChooseTeam.Visible == true then
            if _G.SelectTeam == "Pirate" then
                for i, v in pairs(getconnections(game:GetService("Players").LocalPlayer.PlayerGui.Main.ChooseTeam
                                                    .Container.Pirates.Frame.ViewportFrame.TextButton.Activated)) do
                    v.Function()
                end
            elseif _G.SelectTeam == "Marine" then
                for i, v in pairs(getconnections(game:GetService("Players").LocalPlayer.PlayerGui.Main.ChooseTeam
                                                    .Container.Marines.Frame.ViewportFrame.TextButton.Activated)) do
                    v.Function()
                end
            else
                for i, v in pairs(getconnections(game:GetService("Players").LocalPlayer.PlayerGui.Main.ChooseTeam.Container.Pirates.Frame.ViewportFrame.TextButton.Activated)) do
                    v.Function()
                end
            end
        end
    until game.Players.LocalPlayer.Team ~= nil and game:IsLoaded()
end



game:GetService("ReplicatedStorage").Assets.GUI.DamageCounter.Enabled = false 
AttackRandomType = 1

----------
local id = game.PlaceId
if id == 2753915549 then
    OldWolrd = true;
elseif id == 4442272183 then
    SecondSea = true;
elseif id == 7449423635 then
    ThirdSea = true;
end
-------------
if game.CoreGui:FindFirstChild("PepsiUi") then
    game.CoreGui:FindFirstChild("PepsiUi"):Destroy()
end

-- [ Gui ] --

local library = {
	WorkspaceName = "Name",
	flags = {},
	signals = {},
	objects = {},
	elements = {},
	globals = {},
	subs = {},
	colored = {},
	configuration = {
		hideKeybind = Enum.KeyCode.RightControl,
		smoothDragging = false,
		easingStyle = Enum.EasingStyle.Quart,
		easingDirection = Enum.EasingDirection.Out
	},
	colors = {
		main = Color3.fromRGB(120, 16, 206),
		background = Color3.fromRGB(0,20,11),
		outerBorder = Color3.fromRGB(15, 15, 15),
		innerBorder = Color3.fromRGB(120, 16, 206),
		topGradient = Color3.fromRGB(35, 35, 35),
		bottomGradient = Color3.fromRGB(29, 29, 29),
		sectionBackground = Color3.fromRGB(0,30,5),
		section = Color3.fromRGB(255, 255, 255),
		otherElementText = Color3.fromRGB(255, 255, 255),
		elementText = Color3.fromRGB(255, 255, 255),
		elementBorder = Color3.fromRGB(20, 20, 20),
		selectedOption = Color3.fromRGB(55, 55, 55),
		unselectedOption = Color3.fromRGB(40, 40, 40),
		hoveredOptionTop = Color3.fromRGB(65, 65, 65),
		unhoveredOptionTop = Color3.fromRGB(50, 50, 50),
		hoveredOptionBottom = Color3.fromRGB(45, 45, 45),
		unhoveredOptionBottom = Color3.fromRGB(35, 35, 35),
		tabText = Color3.fromRGB(255, 255, 255)
	},
	gui_parent = (function()
		local x, c = pcall(function()
			return game:GetService("CoreGui")
		end)
		if x and c then
			return c
		end
		x, c = pcall(function()
			return (game:IsLoaded() or (game.Loaded:Wait() or 1)) and game:GetService("Players").LocalPlayer:WaitForChild("PlayerGui")
		end)
		if x and c then
			return c
		end
		x, c = pcall(function()
			return game:GetService("StarterGui")
		end)
		if x and c then
			return c
		end
		return error("Seriously bad exploit. Can't find a place to store the GUI. Robust code can't help here.")
	end)(),
	colorpicker = false,
	colorpickerconflicts = {},
	rainbowflags = {},
	rainbows = 0,
	rainbowsg = 0
}
library.Subs = library.subs
local library_flags = library.flags
local destroyrainbows, destroyrainbowsg = nil
function darkenColor(clr, intensity)
	if not intensity or intensity == 1 then
		return clr
	end
	if clr and (typeof(clr) == "Color3" or type(clr) == "table") then
		return Color3.new(clr.R / intensity, clr.G / intensity, clr.B / intensity)
	end
end
library.subs.darkenColor = darkenColor
local __runscript = true
local function wait_check(...)
	if __runscript then
		return wait(...)
	else
		wait()
		return false
	end
end
library.subs.Wait, library.subs.wait = wait_check, wait_check
local lasthidebing = 0
local temp = game:FindService("MarketplaceService") or game:GetService("MarketplaceService")
local Marketplace = (temp and (cloneref and cloneref(temp))) or temp
local resolvevararg, temp = nil
do
	local lwr = string.lower
	function library.defaultSort(a, b)
		return lwr(tostring(b)) > lwr(tostring(a))
	end
end
do
	local varargresolve = {
		Window = {"Name", "Theme"},
		Tab = {"Name", "Image"},
		Section = {"Name", "Side"},
		Label = {"Text", "Flag", "UnloadValue", "UnloadFunc"},
		Toggle = {"Name", "Value", "Callback", "Flag", "Location", "LocationFlag", "UnloadValue", "UnloadFunc", "Locked", "Keybind", "Condition", "AllowDuplicateCalls"},
		Textbox = {"Name", "Value", "Callback", "Flag", "Location", "LocationFlag", "UnloadValue", "UnloadFunc", "Placeholder", "Type", "Min", "Max", "Decimals", "Hex", "Binary", "Base", "RichTextBox", "MultiLine", "TextScaled", "TextFont", "PreFormat", "PostFormat", "CustomProperties", "AllowDuplicateCalls"},
		Slider = {"Name", "Value", "Callback", "Flag", "Location", "LocationFlag", "UnloadValue", "UnloadFunc", "Min", "Max", "Decimals", "Format", "IllegalInput", "Textbox", "AllowDuplicateCalls"},
		Button = {"Name", "Callback", "Locked", "Condition"},
		Keybind = {"Name", "Value", "Callback", "Flag", "Location", "LocationFlag", "UnloadValue", "UnloadFunc", "Pressed", "KeyNames", "AllowDuplicateCalls"},
		Dropdown = {"Name", "Value", "Callback", "Flag", "Location", "LocationFlag", "UnloadValue", "UnloadFunc", "List", "Filter", "Method", "Nothing", "Sort", "MultiSelect", "ItemAdded", "ItemRemoved", "ItemChanged", "ItemsCleared", "ScrollUpButton", "ScrollDownButton", "ScrollButtonRate", "DisablePrecisionScrolling", "AllowDuplicateCalls"},
		SearchBox = {"Name", "Value", "Callback", "Flag", "Location", "LocationFlag", "UnloadValue", "UnloadFunc", "List", "Filter", "Method", "Nothing", "Sort", "MultiSelect", "ItemAdded", "ItemRemoved", "ItemChanged", "ItemsCleared", "ScrollUpButton", "ScrollDownButton", "ScrollButtonRate", "DisablePrecisionScrolling", "RegEx", "AllowDuplicateCalls"},
		Colorpicker = {"Name", "Value", "Callback", "Flag", "Location", "LocationFlag", "UnloadValue", "UnloadFunc", "Rainbow", "Random", "AllowDuplicateCalls"},
		Persistence = {"Name", "Value", "Callback", "Flag", "Location", "LocationFlag", "UnloadValue", "UnloadFunc", "Workspace", "Persistive", "Suffix", "LoadCallback", "SaveCallback", "PostLoadCallback", "PostSaveCallback", "ScrollUpButton", "ScrollDownButton", "ScrollButtonRate", "DisablePrecisionScrolling", "AllowDuplicateCalls"},
		Designer = {"Backdrop", "Image", "Info", "Credit"}
	}
	function resolvevararg(objtype, ...)
		local data = varargresolve[objtype]
		local t = {}
		if data then
			for index, value in next, {...} do
				t[data[index]] = value
			end
		end
		return t
	end
end
local resolvercache = {}
library.resolvercache = resolvercache
local function resolveid(image, flag)
	if image then
		if type(image) == "string" then
			if (#image > 14 and string.sub(image, 1, 13) == "rbxassetid://") or (#image > 12 and string.sub(image, 1, 11) == "rbxasset://") or (#image > 12 and string.sub(image, 1, 11) ~= "rbxthumb://") then
				if flag then
					local thing = library.elements[flag] or library.designerelements[flag]
					if thing and thing.Set then
						task.spawn(thing.Set, thing, image)
					end
				end
				return image
			end
		end
		local orig = image
		if resolvercache[orig] then
			if flag then
				local thing = library.elements[flag] or library.designerelements[flag]
				if thing and thing.Set then
					task.spawn(thing.Set, thing, resolvercache[orig])
				end
			end
			return resolvercache[orig]
		end
		image = tonumber(image) or image
		local succezz = pcall(function()
			local typ = type(image)
			if typ == "string" then
				if getsynasset then
					if #image > 11 and string.sub(image, 1, 11) == "synasset://" then
						return getsynasset(string.sub(image, 12))
					elseif #image > 14 and string.sub(image, 1, 14) == "synasseturl://" then
						local x, e = pcall(function()
							local codename, fixes = string.gsub(image, ".", function(c)
								if c:lower() == c:upper() and not tonumber(c) then
									return ""
								end
							end)
							codename = string.sub(codename, 1, 24) .. tostring(fixes)
							local fold = isfolder("./Function Lib")
							if not fold then
								makefolder("./Function Lib")
							end
							fold = isfolder("./Function Lib/Themes")
							if not fold then
								makefolder("./Function Lib/Themes")
							end
							fold = isfolder("./Function Lib/Themes/SynapseAssetsCache")
							if not fold then
								makefolder("./Function Lib Themes/SynapseAssetsCache")
							end
							if not fold or not isfile("./Function Lib/Themes/SynapseAssetsCache/" .. codename .. ".dat") then
								local res = game:HttpGet(string.sub(image, 15))
								if res ~= nil then
									writefile("./Function Lib/Themes/SynapseAssetsCache/" .. codename .. ".dat", res)
								end
							end
							return getsynasset(readfile("./Function Lib/Themes/SynapseAssetsCache/" .. codename .. ".dat"))
						end)
						if x and e ~= nil then
							return e
						end
					end
				end
				if #image < 11 or (string.sub(image, 1, 13) ~= "rbxassetid://" and string.sub(image, 1, 11) ~= "rbxasset://" and string.sub(image, 1, 11) ~= "rbxthumb://") then
					image = tonumber(image:gsub("%D", ""), 10) or image
					typ = type(image)
				end
			end
			if typ == "number" and image > 0 then
				pcall(function()
					local nfo = Marketplace and Marketplace:GetProductInfo(image)
					image = tostring(image)
					if nfo and nfo.AssetTypeId == 1 then
						image = "rbxassetid://" .. image
					elseif nfo.AssetTypeId == 13 then
						local decal = game:GetObjects("rbxassetid://" .. image)[1]
						image = "rbxassetid://" .. decal.Texture:match("%d+$")
						decal = (decal and decal:Destroy() and nil) or nil
					end
				end)
			else
				image = nil
			end
		end)
		if succezz and image then
			if orig then
				resolvercache[orig] = image
			end
			resolvercache[image] = image
			if flag then
				local thing = library.elements[flag] or library.designerelements[flag]
				if thing and thing.Set then
					task.spawn(thing.Set, thing, image)
				end
			end
		end
	end
	return image
end
library.subs.ResolveID = resolveid
library.resolvercache = resolvercache
local colored = library.colored
local colors = library.colors
local tweenService = game:GetService("TweenService")
local updatecolors = nil
do
	function updatecolors(tweenit)
		if library.objects and (#library.objects > 0 or next(library.objects)) then
			for _, data in next, colored do
				local x, e
				if tweenit then
					x, e = pcall(function()
						local cclr = colors[data[3]]
						local darkness = data[4]
						tweenService:Create(data[1], TweenInfo.new(tweenit, library.configuration.easingStyle, library.configuration.easingDirection), {
							[data[2]] = (darkness and darkness ~= 1 and darkenColor(cclr, darkness)) or cclr
						}):Play()
					end)
				end
				if not x then
					local x, e = pcall(function()
						local cclr = colors[data[3]]
						local darkness = data[4]
						data[1][data[2]] = (darkness and darkness ~= 1 and darkenColor(cclr, darkness)) or cclr
					end)
					if not x and e then
						warn(debug.traceback(e))
					end
				end
			end
			pcall(function()
				if library.Backdrop then
					library.Backdrop.Visible = not not library_flags["__Designer.Background.UseBackgroundImage"]
					library.Backdrop.Image = resolveid(library_flags["__Designer.Background.ImageAssetID"], "__Designer.Background.ImageAssetID") or ""
					library.Backdrop.ImageColor3 = library_flags["__Designer.Background.ImageColor"] or Color3.new(1, 1, 1)
					library.Backdrop.ImageTransparency = (library_flags["__Designer.Background.ImageTransparency"] or 95) / 100
				end
			end)
		end
	end
	library.subs.UpdateColors = updatecolors
end
local function updatecolorsnotween()
	updatecolors()
end
library.subs.updatecolors = updatecolors
library.colors = setmetatable({}, {
	__index = colors,
	__newindex = function(_, k, v)
		if colors[k] ~= v then
			colors[k] = v
			spawn(updatecolorsnotween)
		end
	end
})
local elements = library.elements
shared.libraries = shared.libraries or {}
local colorpickerconflicts = library.colorpickerconflicts
local keyHandler = {
	notAllowedKeys = {
		[Enum.KeyCode.Return] = true,
		[Enum.KeyCode.Space] = true,
		[Enum.KeyCode.Tab] = true,
		[Enum.KeyCode.Unknown] = true,
		[Enum.KeyCode.Backspace] = true
	},
	notAllowedMouseInputs = {
		[Enum.UserInputType.MouseMovement] = true,
		[Enum.UserInputType.MouseWheel] = true,
		[Enum.UserInputType.MouseButton1] = true,
		[Enum.UserInputType.MouseButton2] = true,
		[Enum.UserInputType.MouseButton3] = true
	},
	allowedKeys = {
		[Enum.KeyCode.LeftShift] = "LShift",
		[Enum.KeyCode.RightShift] = "RShift",
		[Enum.KeyCode.LeftControl] = "LCtrl",
		[Enum.KeyCode.RightControl] = "RCtrl",
		[Enum.KeyCode.LeftAlt] = "LAlt",
		[Enum.KeyCode.RightAlt] = "RAlt",
		[Enum.KeyCode.CapsLock] = "CAPS",
		[Enum.KeyCode.One] = "1",
		[Enum.KeyCode.Two] = "2",
		[Enum.KeyCode.Three] = "3",
		[Enum.KeyCode.Four] = "4",
		[Enum.KeyCode.Five] = "5",
		[Enum.KeyCode.Six] = "6",
		[Enum.KeyCode.Seven] = "7",
		[Enum.KeyCode.Eight] = "8",
		[Enum.KeyCode.Nine] = "9",
		[Enum.KeyCode.Zero] = "0",
		[Enum.KeyCode.KeypadOne] = "Num-1",
		[Enum.KeyCode.KeypadTwo] = "Num-2",
		[Enum.KeyCode.KeypadThree] = "Num-3",
		[Enum.KeyCode.KeypadFour] = "Num-4",
		[Enum.KeyCode.KeypadFive] = "Num-5",
		[Enum.KeyCode.KeypadSix] = "Num-6",
		[Enum.KeyCode.KeypadSeven] = "Num-7",
		[Enum.KeyCode.KeypadEight] = "Num-8",
		[Enum.KeyCode.KeypadNine] = "Num-9",
		[Enum.KeyCode.KeypadZero] = "Num-0",
		[Enum.KeyCode.Minus] = "-",
		[Enum.KeyCode.Equals] = "=",
		[Enum.KeyCode.Tilde] = "~",
		[Enum.KeyCode.LeftBracket] = "[",
		[Enum.KeyCode.RightBracket] = "]",
		[Enum.KeyCode.RightParenthesis] = ")",
		[Enum.KeyCode.LeftParenthesis] = "(",
		[Enum.KeyCode.Semicolon] = ";",
		[Enum.KeyCode.Quote] = "'",
		[Enum.KeyCode.BackSlash] = "\\",
		[Enum.KeyCode.Comma] = ",",
		[Enum.KeyCode.Period] = ".",
		[Enum.KeyCode.Slash] = "/",
		[Enum.KeyCode.Asterisk] = "*",
		[Enum.KeyCode.Plus] = "+",
		[Enum.KeyCode.Period] = ".",
		[Enum.KeyCode.Backquote] = "`"
	}
}
local function hardunload(library)
	if library.UnloadCallback and type(library.UnloadCallback) == "function" then
		local x, e = pcall(library.UnloadCallback)
		if not x and e then
			task.spawn(error, e, 2)
		end
	end
	for cflag, data in next, elements do
		if data.Type ~= "Persistence" then
			if data.Set and data.Options.UnloadValue ~= nil then
				data.Set(data.Options.UnloadValue)
			end
			if data.Options.UnloadFunc then
				local y, u = pcall(data.Options.UnloadFunc)
				if not y and u then
					warn(debug.traceback("Error unloading '" .. tostring(cflag) .. "'\n" .. u))
				end
			end
		end
	end
	for _, v in next, {library.signals, library.objects} do
		for k, o in next, v do
			if o then
				local te = typeof(o)
				if te == "RBXScriptConnection" then
					o:Disconnect()
				elseif te == "Instance" then
					o:Destroy()
				end
			end
			v[k] = nil
		end
	end
	library.signals = nil
	library.objects = nil
end
library.Subs.UnloadArg = hardunload
local function unloadall()
	if shared.libraries then
		local b = 50
		while #shared.libraries > 0 do
			b = b - 1
			if b < 0 then
				b = 50
				wait(warn("Looped 50 times while unloading....?"))
			end
			local v = shared.libraries[1]
			if v and v.unload and type(v.unload) == "function" then
				if not pcall(v.unload) then
					pcall(hardunload, v)
					for k in next, v do
						v[k] = nil
					end
				end
				table.remove(shared.libraries, 1)
			end
		end
	end
	shared.libraries = nil
end
shared.unloadall = unloadall
library.unloadall = unloadall
shared.libraries[1 + #shared.libraries] = library
function library.unload()
	__runscript = nil
	hardunload(library)
	if shared.libraries then
		for k, v in next, shared.libraries or {} do
			if v == library then
				for k in next, table.remove(shared.libraries, k) do
					v[k] = nil
				end
				break
			end
		end
		if #shared.libraries == 0 then
			shared.libraries = nil
		end
	end
	warn("Unloaded")
end
library.Unload = library.unload
local Instance_new = (syn and syn.protect_gui and function(...)
	local x = {Instance.new(...)}
	if x[1] then
		library.objects[1 + #library.objects] = x[1]
		pcall(syn.protect_gui, x[1])
	end
	return unpack(x)
end) or function(...)
	local x = {Instance.new(...)}
	if x[1] then
		library.objects[1 + #library.objects] = x[1]
	end
	return unpack(x)
end
library.subs.Instance_new = Instance_new
local playersservice = game:GetService("Players")
local function getresolver(listt, filter, method, _)
	local huo, args = type(filter), {}
	local hou = typeof(listt)
	return (hou == "table" and function()
		return listt
	end) or function()
		local hardtype = nil
		local g = listt
		for _ = 1, 5 do
			hardtype = typeof(g)
			if hardtype == "function" then
				local x, e = pcall(listt)
				if x and e then
					g = e
				end
				hardtype = typeof(g)
			end
			if hardtype == "Instance" then
				local lastg = g
				if method == nil and listt == playersservice then
					g = listt:GetPlayers()
				end
				if method then
					local metype = type(method)
					if metype == "table" then
						method = method.Method or method[1]
						args = method.Args or method.Arguments or unpack(method, (method.Method ~= nil and 1) or 2)
						metype = type(method)
					end
					local y, u = nil, nil
					if metype == "function" then
						y, u = pcall(method, listt, unpack(args))
					elseif metype == "string" then
						local y, u = pcall(function()
							return listt[method](listt, unpack(args))
						end)
					else
						warn("Idk how to handle method type of", metype, debug.traceback(""))
					end
					if u then
						if y then
							g = u
						else
							warn("Error trying method", method, "on", listt, debug.traceback(u))
						end
					end
				end
				if g == lastg then
					g = listt:GetChildren()
				end
			end
			if hardtype == "Enum" then
				g = listt:GetEnumItems()
			end
			hardtype = typeof(g)
			if hardtype == "table" then
				break
			end
		end
		hardtype = typeof(g)
		if hardtype ~= "table" then
			warn("Could not resolve " .. hou .. " type to a list.")
			return {}
		end
		if filter then
			if huo == "function" then
				local accept = {}
				for _, v in next, g do
					local x, e = pcall(filter, v)
					if x and e then
						accept[1 + #accept] = (e == true and v) or e
					end
				end
				g = accept
			elseif huo == "string" then
				local accept = {}
				for _, v in next, g do
					if tostring(v):lower():find(huo) then
						accept[1 + #accept] = v
					end
				end
				g = accept
			elseif huo == "table" then
				local accept = {}
				if type(filter[1]) == "string" then
					for _, v in next, g do
						if tostring(v):lower():find(huo) then
							accept[1 + #accept] = v
						elseif filter[0] then
							accept[1 + #accept] = v
						end
					end
				else
					for _, v in next, g do
						if not table.find(filter, v) and not table.find(filter, tostring(v)) then
							accept[1 + #accept] = v
						elseif not filter[0] then
							accept[1 + #accept] = v
						end
					end
				end
				g = accept
			end
		end
		return g
	end
end
library.subs.GetResolver = getresolver
local function resetall()
	destroyrainbowsg = true
	pcall(function()
		for k, v in next, elements do
			if v and k and v.Set and v.Default ~= nil and library_flags[k] ~= v.Default and string.sub(k, 1, 11) ~= "__Designer." then
				v:Set(v.Default)
			end
		end
	end)
end
library.ResetAll = resetall
local textService = game:GetService("TextService")
local userInputService = game:GetService("UserInputService")
local runService = game:GetService("RunService")
local LP = playersservice.LocalPlayer
library.LP = LP
library.Players = playersservice
library.UserInputService = userInputService
library.RunService = runService
local mouse = LP and LP:GetMouse()
if not mouse and PluginManager and runService:IsStudio() then
	shared.library_plugin = shared.library_plugin or print("Creating Studio Test-Plugin...") or PluginManager():CreatePlugin()
	mouse = shared.library_plugin:GetMouse()
	library.plugin = shared.library_plugin
end
library.Mouse = mouse
local function textToSize(object)
	if object ~= nil then
		local output = textService:GetTextSize(object.Text, object.TextSize, object.Font, Vector2.new(math.huge, math.huge))
		return {
			X = output.X,
			Y = output.Y
		}
	end
end
library.subs.textToSize = textToSize
local function removeSpaces(str)
	if str then
		local newStr = str:gsub(" ", "")
		return newStr
	end
end
library.subs.removeSpaces = removeSpaces
local function Color3FromHex(hex)
	hex = hex:gsub("#", ""):upper():gsub("0X", "")
	return Color3.fromRGB(tonumber(hex:sub(1, 2), 16), tonumber(hex:sub(3, 4), 16), tonumber(hex:sub(5, 6), 16))
end
library.subs.Color3FromHex = Color3FromHex
local floor = math.floor
local function Color3ToHex(color)
	local r, g, b = string.format("%X", floor(color.R * 255)), string.format("%X", floor(color.G * 255)), string.format("%X", floor(color.B * 255))
	if #r < 2 then
		r = "0" .. r
	end
	if #g < 2 then
		g = "0" .. g
	end
	if #b < 2 then
		b = "0" .. b
	end
	return string.format("%s%s%s", r, g, b)
end
if Color3.ToHex and not shared.overridecolortohex then
	local x, e = pcall(Color3.ToHex, Color3.new())
	if x and type(e) == "string" and #e == 6 then
		Color3ToHex = Color3.ToHex
	end
end
library.subs.Color3ToHex = Color3ToHex
local isDraggingSomething = false
local function makeDraggable(topBarObject, object)
	local dragging = nil
	local dragInput = nil
	local dragStart = nil
	local startPosition = nil
	library.signals[1 + #library.signals] = topBarObject.InputBegan:Connect(function(input)
		if input.UserInputType == Enum.UserInputType.MouseButton1 or input.UserInputType == Enum.UserInputType.Touch then
			dragging = true
			dragStart = input.Position
			startPosition = object.Position
			input.Changed:Connect(function()
				if input.UserInputState == Enum.UserInputState.End then
					dragging = false
				end
			end)
		end
	end)
	library.signals[1 + #library.signals] = topBarObject.InputChanged:Connect(function(input)
		if input.UserInputType == Enum.UserInputType.MouseMovement or input.UserInputType == Enum.UserInputType.Touch then
			dragInput = input
		end
	end)
	library.signals[1 + #library.signals] = userInputService.InputChanged:Connect(function(input)
		if input == dragInput and dragging then
			local delta = input.Position - dragStart
			if not isDraggingSomething and library.configuration.smoothDragging then
				tweenService:Create(object, TweenInfo.new(0.35, library.configuration.easingStyle, library.configuration.easingDirection), {
					Position = UDim2.new(startPosition.X.Scale, startPosition.X.Offset + delta.X, startPosition.Y.Scale, startPosition.Y.Offset + delta.Y)
				}):Play()
			elseif not isDraggingSomething and not library.configuration.smoothDragging then
				object.Position = UDim2.new(startPosition.X.Scale, startPosition.X.Offset + delta.X, startPosition.Y.Scale, startPosition.Y.Offset + delta.Y)
			end
		end
	end)
end
library.subs.makeDraggable = makeDraggable
local JSONEncode, JSONDecode = nil, nil
do
	local temp_http = game:FindService("HttpService") or game:GetService("HttpService")
	local httpservice = temp_http
	if cloneref and type(cloneref) == "function" then
		httpservice, temp_http = cloneref(httpservice), nil
	end
	library.Http = httpservice
	local JSONEncodeFunc = httpservice.JSONEncode
	function JSONEncode(...)
		return pcall(JSONEncodeFunc, httpservice, ...)
	end
	library.JSONEncode = JSONEncode
	local JSONDecodeFunc = httpservice.JSONDecode
	function JSONDecode(...)
		return pcall(JSONDecodeFunc, httpservice, ...)
	end
	library.JSONDecode = JSONDecode
end
local convertfilename
do
	local string_gsub = string.gsub
	function convertfilename(str, default, replace)
		replace = replace or "_"
		local corrections = 0
		local predname = string_gsub(str, "%W", function(c)
			local byt = c:byte()
			if not (byt == 0 or byt == 32 or byt == 33 or byt == 59 or byt == 61 or (byt >= 35 and byt <= 41) or (byt >= 43 and byt <= 57) or (byt >= 64 and byt <= 123) or (byt >= 125 and byt <= 127)) then
				corrections = 1 + corrections
				return replace
			end
		end)
		return (default and corrections == #predname and tostring(default)) or predname
	end
	library.subs.ConvertFilename = convertfilename
end
function library:CreateWindow(options, ...)
	options = (options and type(options) == "string" and resolvevararg("Window", options, ...)) or options
	local homepage = nil
	local windowoptions = options
	local windowName = options.Name or "Unnamed Window"
	options.Name = windowName
	if windowName and #windowName > 0 and library.WorkspaceName == "Function Lib" then
		library.WorkspaceName = convertfilename(windowName, "Function Lib")
	end
	local FunctionLibrary = Instance_new("ScreenGui")
	local main = Instance_new("Frame")
	local mainBorder = Instance_new("Frame")
	local tabSlider = Instance_new("Frame")
	local innerMain = Instance_new("Frame")
	local innerMainBorder = Instance_new("Frame")
	local innerBackdrop = Instance_new("ImageLabel")
	local innerMainHolder = Instance_new("Frame")
	local tabsHolder = Instance_new("ImageLabel")
	local tabHolderList = Instance_new("UIListLayout")
	local tabHolderPadding = Instance_new("UIPadding")
	local headline = Instance_new("TextLabel")
	local splitter = Instance_new("TextLabel")
	local submenuOpen = nil
	library.globals["__Window" .. options.Name] = {
		submenuOpen = submenuOpen
	}
	FunctionLibrary.Name = "PepsiUi"
	FunctionLibrary.Parent = library.gui_parent
	FunctionLibrary.ZIndexBehavior = Enum.ZIndexBehavior.Sibling
	FunctionLibrary.DisplayOrder = 10
	FunctionLibrary.ResetOnSpawn = false
	main.Name = "main"
	main.Parent = FunctionLibrary
	main.AnchorPoint = Vector2.new(0.5, 0.5)
	main.BackgroundColor3 = library.colors.background
	colored[1 + #colored] = {main, "BackgroundColor3", "background"}
	main.BorderColor3 = library.colors.outerBorder
	colored[1 + #colored] = {main, "BorderColor3", "outerBorder"}
	main.Position = UDim2.fromScale(0.5, 0.5)
	main.Size = UDim2.fromOffset(500, 545)
	makeDraggable(main, main)
	mainBorder.Name = "mainBorder"
	mainBorder.Parent = main
	mainBorder.AnchorPoint = Vector2.new(0.5, 0.5)
	mainBorder.BackgroundColor3 = library.colors.background
	colored[1 + #colored] = {mainBorder, "BackgroundColor3", "background"}
	mainBorder.BorderColor3 = library.colors.innerBorder
	colored[1 + #colored] = {mainBorder, "BorderColor3", "innerBorder"}
	mainBorder.BorderMode = Enum.BorderMode.Inset
	mainBorder.Position = UDim2.fromScale(0.5, 0.5)
	mainBorder.Size = UDim2.fromScale(1, 1)
	innerMain.Name = "innerMain"
	innerMain.Parent = main
	innerMain.AnchorPoint = Vector2.new(0.5, 0.5)
	innerMain.BackgroundColor3 = library.colors.background
	colored[1 + #colored] = {innerMain, "BackgroundColor3", "background"}
	innerMain.BorderColor3 = library.colors.outerBorder
	colored[1 + #colored] = {innerMain, "BorderColor3", "outerBorder"}
	innerMain.Position = UDim2.fromScale(0.5, 0.5)
	innerMain.Size = UDim2.new(1, -14, 1, -14)
	innerMainBorder.Name = "innerMainBorder"
	innerMainBorder.Parent = innerMain
	innerMainBorder.AnchorPoint = Vector2.new(0.5, 0.5)
	innerMainBorder.BackgroundColor3 = library.colors.background
	colored[1 + #colored] = {innerMainBorder, "BackgroundColor3", "background"}
	innerMainBorder.BorderColor3 = library.colors.innerBorder
	colored[1 + #colored] = {innerMainBorder, "BorderColor3", "innerBorder"}
	innerMainBorder.BorderMode = Enum.BorderMode.Inset
	innerMainBorder.Position = UDim2.fromScale(0.5, 0.5)
	innerMainBorder.Size = UDim2.fromScale(1, 1)
	innerMainHolder.Name = "innerMainHolder"
	innerMainHolder.Parent = innerMain
	innerMainHolder.BackgroundColor3 = Color3.new(1, 1, 1)
	innerMainHolder.BackgroundTransparency = 1
	innerMainHolder.Position = UDim2:fromOffset(25)
	innerMainHolder.Size = UDim2.new(1, 0, 1, -25)
	innerBackdrop.Name = "innerBackdrop"
	innerBackdrop.Parent = innerMainHolder
	innerBackdrop.BackgroundColor3 = Color3.new(1, 1, 1)
	innerBackdrop.BackgroundTransparency = 1
	innerBackdrop.Size = UDim2.fromScale(1, 1)
	innerBackdrop.ZIndex = -1
	innerBackdrop.Visible = not not library_flags["__Designer.Background.UseBackgroundImage"]
	innerBackdrop.ImageColor3 = library_flags["__Designer.Background.ImageColor"] or Color3.new(1, 1, 1)
	innerBackdrop.ImageTransparency = (library_flags["__Designer.Background.ImageTransparency"] or 95) / 100
	innerBackdrop.Image = resolveid(library_flags["__Designer.Background.ImageAssetID"], "__Designer.Background.ImageAssetID") or ""
	library.Backdrop = innerBackdrop
	tabsHolder.Name = "tabsHolder"
	tabsHolder.Parent = innerMain
	tabsHolder.BackgroundColor3 = library.colors.topGradient
	colored[1 + #colored] = {tabsHolder, "BackgroundColor3", "topGradient"}
	tabsHolder.BorderSizePixel = 0
	tabsHolder.Position = UDim2.fromOffset(1, 1)
	tabsHolder.Size = UDim2.new(1, -2, 0, 23)
	tabsHolder.Image = "rbxassetid://2454009026"
	tabsHolder.ImageColor3 = library.colors.bottomGradient
	colored[1 + #colored] = {tabsHolder, "ImageColor3", "bottomGradient"}
	tabHolderList.Name = "tabHolderList"
	tabHolderList.Parent = tabsHolder
	tabHolderList.FillDirection = Enum.FillDirection.Horizontal
	tabHolderList.SortOrder = Enum.SortOrder.LayoutOrder
	tabHolderList.VerticalAlignment = Enum.VerticalAlignment.Center
	tabHolderList.Padding = UDim:new(3)
	tabHolderPadding.Name = "tabHolderPadding"
	tabHolderPadding.Parent = tabsHolder
	tabHolderPadding.PaddingLeft = UDim:new(7)
	headline.Name = "headline"
	headline.Parent = tabsHolder
	headline.BackgroundColor3 = Color3.new(1, 1, 1)
	headline.BackgroundTransparency = 1
	headline.LayoutOrder = 1
	headline.Font = Enum.Font.Code
	headline.Text = (windowName and tostring(windowName)) or "???"
	headline.TextColor3 = library.colors.main
	colored[1 + #colored] = {headline, "TextColor3", "main"}
	headline.TextSize = 14
	headline.TextStrokeColor3 = library.colors.outerBorder
	colored[1 + #colored] = {headline, "TextStrokeColor3", "outerBorder"}
	headline.TextStrokeTransparency = 0.75
	headline.Size = UDim2:new(textToSize(headline).X + 4, 1)
	splitter.Name = "splitter"
	splitter.Parent = tabsHolder
	splitter.BackgroundColor3 = Color3.new(1, 1, 1)
	splitter.BackgroundTransparency = 1
	splitter.LayoutOrder = 2
	splitter.Size = UDim2:new(6, 1)
	splitter.Font = Enum.Font.Code
	splitter.Text = "|"
	splitter.TextColor3 = library.colors.tabText
	colored[1 + #colored] = {splitter, "TextColor3", "tabText"}
	splitter.TextSize = 14
	splitter.TextStrokeColor3 = library.colors.tabText
	colored[1 + #colored] = {splitter, "TextStrokeColor3", "tabText"}
	splitter.TextStrokeTransparency = 0.75
	tabSlider.Name = "tabSlider"
	tabSlider.Parent = main
	tabSlider.BackgroundColor3 = library.colors.main
	colored[1 + #colored] = {tabSlider, "BackgroundColor3", "main"}
	tabSlider.BorderSizePixel = 0
	tabSlider.Position = UDim2.fromOffset(100, 30)
	tabSlider.Size = UDim2:fromOffset(1)
	tabSlider.Visible = false
	do
		local os_clock = os.clock
		library.signals[1 + #library.signals] = userInputService.InputBegan:Connect(function(keyCode, gameProcessedEvent)
			gameProcessedEvent = gameProcessedEvent or userInputService:GetFocusedTextBox()
			if not gameProcessedEvent and keyCode.KeyCode == library.configuration.hideKeybind then
				if not lasthidebing or os_clock() - lasthidebing > 12 then
					main.Visible = not main.Visible
				end
				lasthidebing = nil
			end
		end)
	end
	local windowFunctions = {
		tabCount = 0,
		selected = {},
		Flags = elements
	}
	library.globals["__Window" .. windowName].windowFunctions = windowFunctions
	function windowFunctions:Show(x)
		main.Visible = x == nil or x == true or x == 1
	end
	function windowFunctions:Hide(x)
		main.Visible = x == false or x == 0
	end
	function windowFunctions:Visibility(x)
		if x == nil then
			main.Visible = not main.Visible
		else
			main.Visible = not not x
		end
	end
	function windowFunctions:MoveTabSlider(tabObject)
		spawn(function()
			tabSlider.Visible = true
			tweenService:Create(tabSlider, TweenInfo.new(0.35, library.configuration.easingStyle, library.configuration.easingDirection), {
				Size = UDim2.fromOffset(tabObject.AbsoluteSize.X, 1),
				Position = UDim2.fromOffset(tabObject.AbsolutePosition.X, tabObject.AbsolutePosition.Y + tabObject.AbsoluteSize.Y) - UDim2.fromOffset(main.AbsolutePosition.X, main.AbsolutePosition.Y)
			}):Play()
		end)
	end
	windowFunctions.LastTab = nil
	function windowFunctions:CreateTab(options, ...)
		options = (options and type(options) == "string" and resolvevararg("Tab", options, ...)) or options or {
			Name = "Function Style: Elite Hax"
		}
		local image = options.Image
		if image then
			image = resolveid(image)
		end
		local tabName = options.Name or "Unnamed Tab"
		options.Name = tabName
		windowFunctions.tabCount = windowFunctions.tabCount + 1
		local newTab = Instance_new((image and "ImageButton") or "TextButton")
		local newTabHolder = Instance_new("Frame")
		library.globals["__Window" .. windowName].newTabHolder = newTabHolder
		local left = Instance_new("ScrollingFrame")
		local leftList = Instance_new("UIListLayout")
		local leftPadding = Instance_new("UIPadding")
		local right = Instance_new("ScrollingFrame")
		local rightList = Instance_new("UIListLayout")
		local rightPadding = Instance_new("UIPadding")
		newTab.Name = removeSpaces((tabName and tostring(tabName):lower() or "???") .. "Tab")
		newTab.Parent = tabsHolder
		newTab.BackgroundTransparency = 1
		newTab.LayoutOrder = (options.LastTab and 99999) or tonumber(options.TabOrder or options.LayoutOrder) or (2 + windowFunctions.tabCount)
		local colored_newTab_TextColor3 = nil
		if image then
			newTab.Image = image
			newTab.ImageColor3 = options.ImageColor or options.Color or Color3.new(1, 1, 1)
			newTab.Size = UDim2:new(tabsHolder.AbsoluteSize.Y, 1)
		else
			colored_newTab_TextColor3 = {newTab, "TextColor3", "tabText"}
			colored[1 + #colored] = colored_newTab_TextColor3
			newTab.Font = Enum.Font.Code
			newTab.Text = (tabName and tostring(tabName)) or "???"
			if windowFunctions.tabCount ~= 1 then
				colored_newTab_TextColor3[4] = 1.35
				newTab.TextColor3 = darkenColor(library.colors.tabText, 1.35)
			else
				newTab.TextColor3 = library.colors.tabText
			end
			newTab.TextSize = 14
			newTab.TextStrokeColor3 = Color3.fromRGB(42, 42, 42)
			newTab.TextStrokeTransparency = 0.75
			newTab.Size = UDim2:new(textToSize(newTab).X + 4, 1)
		end
		local function goto()
			if not library.colorpicker and not submenuOpen and windowFunctions.selected.button ~= newTab then
				pcall(function()
					for _, e in next, library.elements do
						if e and type(e) == "table" and e.Update then
							pcall(e.Update)
						end
					end
				end)
				if windowFunctions.LastTab then
					windowFunctions.LastTab[4] = 1.35
				end
				windowFunctions:MoveTabSlider(newTab)
				if windowFunctions.selected.button.ClassName == "TextButton" then
					tweenService:Create(windowFunctions.selected.button, TweenInfo.new(0.35, library.configuration.easingStyle, library.configuration.easingDirection), {
						TextColor3 = darkenColor(library.colors.tabText, 1.35)
					}):Play()
				end
				if colored_newTab_TextColor3 then
					colored_newTab_TextColor3[4] = nil
				end
				windowFunctions.selected.holder.Visible = false
				windowFunctions.selected.button = newTab
				windowFunctions.selected.holder = newTabHolder
				if windowFunctions.selected.button.ClassName == "TextButton" then
					tweenService:Create(windowFunctions.selected.button, TweenInfo.new(0.35, library.configuration.easingStyle, library.configuration.easingDirection), {
						TextColor3 = library.colors.tabText
					}):Play()
				end
				windowFunctions.selected.holder.Visible = true
				windowFunctions.LastTab = colored_newTab_TextColor3
			end
		end
		if not homepage and newTab.LayoutOrder <= 4 then
			homepage = goto
		end
		library.signals[1 + #library.signals] = newTab.MouseButton1Click:Connect(goto)
		if windowFunctions.tabCount == 1 then
			tabSlider.Size = UDim2.fromOffset(newTab.AbsoluteSize.X, 1)
			tabSlider.Position = UDim2.fromOffset(newTab.AbsolutePosition.X, newTab.AbsolutePosition.Y + newTab.AbsoluteSize.Y) - UDim2.fromOffset(main.AbsolutePosition.X, main.AbsolutePosition.Y)
			tabSlider.Visible = true
			windowFunctions.selected.holder = newTabHolder
			windowFunctions.selected.button = newTab
		end
		newTabHolder.Name = removeSpaces((tabName and tabName:lower()) or "???") .. "TabHolder"
		newTabHolder.Parent = innerMainHolder
		newTabHolder.BackgroundColor3 = Color3.new(1, 1, 1)
		newTabHolder.BackgroundTransparency = 1
		newTabHolder.Size = UDim2.fromScale(1, 1)
		newTabHolder.Visible = windowFunctions.tabCount == 1
		left.Name = "left"
		left.Parent = newTabHolder
		left.BackgroundColor3 = Color3.new(1, 1, 1)
		left.BackgroundTransparency = 1
		left.Size = UDim2.fromScale(0.5, 1)
		left.CanvasSize = UDim2.new()
		left.ScrollBarThickness = 0
		leftList.Name = "leftList"
		leftList.Parent = left
		leftList.HorizontalAlignment = Enum.HorizontalAlignment.Center
		leftList.SortOrder = Enum.SortOrder.LayoutOrder
		leftList.Padding = UDim:new(14)
		leftPadding.Name = "leftPadding"
		leftPadding.Parent = left
		leftPadding.PaddingTop = UDim:new(12)
		right.Name = "right"
		right.Parent = newTabHolder
		right.BackgroundColor3 = Color3.new(1, 1, 1)
		right.BackgroundTransparency = 1
		right.Size = UDim2.fromScale(0.5, 1)
		right.CanvasSize = UDim2.new()
		right.ScrollBarThickness = 0
		right.Position = UDim2.new(0.5)
		rightList.Name = "rightList"
		rightList.Parent = right
		rightList.HorizontalAlignment = Enum.HorizontalAlignment.Center
		rightList.SortOrder = Enum.SortOrder.LayoutOrder
		rightList.Padding = UDim:new(14)
		rightPadding.Name = "rightPadding"
		rightPadding.Parent = right
		rightPadding.PaddingTop = UDim:new(12)
		local tabFunctions = {
			Flags = {}
		}
		function tabFunctions:CreateSection(options, ...)
			options = (options and type(options) == "string" and resolvevararg("Tab", options, ...)) or options
			local sectionName, holderSide = options.Name or "Unnamed Section", options.Side
			options.Name = sectionName
			local newSection = Instance_new("Frame")
			local newSectionBorder = Instance_new("Frame")
			local insideBorderHider = Instance_new("Frame")
			local outsideBorderHider = Instance_new("Frame")
			local sectionHolder = Instance_new("Frame")
			local sectionList = Instance_new("UIListLayout")
			local sectionPadding = Instance_new("UIPadding")
			local sectionHeadline = Instance_new("TextLabel")
			colorpickerconflicts[1 + #colorpickerconflicts] = insideBorderHider
			colorpickerconflicts[1 + #colorpickerconflicts] = outsideBorderHider
			colorpickerconflicts[1 + #colorpickerconflicts] = sectionHeadline
			newSection.Name = removeSpaces((sectionName and sectionName:lower() or "???") .. "Section")
			newSection.Parent = (holderSide and ((holderSide:lower() == "left" and left) or right)) or left
			newSection.BackgroundColor3 = library.colors.sectionBackground
			colored[1 + #colored] = {newSection, "BackgroundColor3", "sectionBackground"}
			newSection.BorderColor3 = library.colors.outerBorder
			colored[1 + #colored] = {newSection, "BorderColor3", "outerBorder"}
			newSection.Size = UDim2.new(1, -20)
			newSection.Visible = false
			newSectionBorder.Name = "newSectionBorder"
			newSectionBorder.Parent = newSection
			newSectionBorder.BackgroundColor3 = library.colors.sectionBackground
			colored[1 + #colored] = {newSectionBorder, "BackgroundColor3", "sectionBackground"}
			newSectionBorder.BorderColor3 = library.colors.innerBorder
			colored[1 + #colored] = {newSectionBorder, "BorderColor3", "innerBorder"}
			newSectionBorder.BorderMode = Enum.BorderMode.Inset
			newSectionBorder.Size = UDim2.fromScale(1, 1)
			sectionHolder.Name = "sectionHolder"
			sectionHolder.Parent = newSection
			sectionHolder.BackgroundColor3 = Color3.new(1, 1, 1)
			sectionHolder.BackgroundTransparency = 1
			sectionHolder.Size = UDim2.fromScale(1, 1)
			sectionList.Name = "sectionList"
			sectionList.Parent = sectionHolder
			sectionList.HorizontalAlignment = Enum.HorizontalAlignment.Center
			sectionList.SortOrder = Enum.SortOrder.LayoutOrder
			sectionList.Padding = UDim:new(1)
			sectionPadding.Name = "sectionPadding"
			sectionPadding.Parent = sectionHolder
			sectionPadding.PaddingTop = UDim:new(9)
			sectionHeadline.Name = "sectionHeadline"
			sectionHeadline.Parent = newSection
			sectionHeadline.BackgroundColor3 = Color3.new(1, 1, 1)
			sectionHeadline.BackgroundTransparency = 1
			sectionHeadline.Position = UDim2.fromOffset(18, -8)
			sectionHeadline.ZIndex = 2
			sectionHeadline.Font = Enum.Font.Code
			sectionHeadline.LineHeight = 1.15
			sectionHeadline.Text = (sectionName and sectionName or "???")
			sectionHeadline.TextColor3 = library.colors.section
			colored[1 + #colored] = {sectionHeadline, "TextColor3", "section"}
			sectionHeadline.TextSize = 14
			sectionHeadline.Size = UDim2.fromOffset(textToSize(sectionHeadline).X + 4, 12)
			insideBorderHider.Name = "insideBorderHider"
			insideBorderHider.Parent = newSection
			insideBorderHider.BackgroundColor3 = library.colors.sectionBackground
			colored[1 + #colored] = {insideBorderHider, "BackgroundColor3", "sectionBackground"}
			insideBorderHider.BorderSizePixel = 0
			insideBorderHider.Position = UDim2.fromOffset(15)
			insideBorderHider.Size = UDim2.fromOffset(sectionHeadline.AbsoluteSize.X + 3, 1)
			outsideBorderHider.Name = "outsideBorderHider"
			outsideBorderHider.Parent = newSection
			outsideBorderHider.BackgroundColor3 = library.colors.background
			colored[1 + #colored] = {outsideBorderHider, "BackgroundColor3", "background"}
			outsideBorderHider.BorderSizePixel = 0
			outsideBorderHider.Position = UDim2.fromOffset(15, -1)
			outsideBorderHider.Size = UDim2.fromOffset(sectionHeadline.AbsoluteSize.X + 3, 1)
			local sectionFunctions = {
				Flags = {}
			}
			function sectionFunctions:Update(extra)
				local currentHolder = newSection.Parent
				if not newSection.Visible then
					newSection.Visible = true
				end
				newSection.Size = UDim2.new(1, -20, 0, (sectionList.AbsoluteContentSize.Y + 15))
				currentHolder.CanvasSize = UDim2:fromOffset(currentHolder:FindFirstChildOfClass("UIListLayout").AbsoluteContentSize.Y + 22 + (extra and extra or 0))
			end
			function sectionFunctions:AddToggle(options, ...)
				options = (options and type(options) == "string" and resolvevararg("Tab", options, ...)) or options
				local toggleName, alreadyEnabled, callback, flagName = assert(options.Name, "Missing Name for new toggle."), options.Value or options.Enabled, options.Callback, options.Flag or (function()
					library.unnamedtoggles = 1 + (library.unnamedtoggles or 0)
					return "Toggle" .. tostring(library.unnamedtoggles)
				end)()
				if elements[flagName] ~= nil then
					warn(debug.traceback("Warning! Re-used flag '" .. flagName .. "'", 3))
				end
				local newToggle = Instance_new("Frame")
				local toggle = Instance_new("ImageLabel")
				local toggleInner = Instance_new("ImageLabel")
				local toggleButton = Instance_new("TextButton")
				local toggleHeadline = Instance_new("TextLabel")
				local keybindPositioner = Instance_new("Frame")
				local keybindList = Instance_new("UIListLayout")
				local keybindButton = Instance_new("TextButton")
				local lockedup = options.Locked
				newToggle.Name = removeSpaces((toggleName and toggleName:lower() or "???") .. "Toggle")
				newToggle.Parent = sectionHolder
				newToggle.BackgroundColor3 = Color3.new(1, 1, 1)
				newToggle.BackgroundTransparency = 1
				newToggle.Size = UDim2.new(1, 0, 0, 19)
				toggle.Name = "toggle"
				toggle.Parent = newToggle
				toggle.Active = true
				toggle.BackgroundColor3 = library.colors.topGradient
				local colored_toggle_BackgroundColor3 = {toggle, "BackgroundColor3", "topGradient"}
				colored[1 + #colored] = colored_toggle_BackgroundColor3
				toggle.BorderColor3 = library.colors.elementBorder
				colored[1 + #colored] = {toggle, "BorderColor3", "elementBorder"}
				toggle.Position = UDim2.fromScale(0.0308237672, 0.165842205)
				toggle.Selectable = true
				toggle.Size = UDim2.fromOffset(12, 12)
				toggle.Image = "rbxassetid://2454009026"
				toggle.ImageColor3 = library.colors.bottomGradient
				local colored_toggle_ImageColor3 = {toggle, "ImageColor3", "bottomGradient"}
				colored[1 + #colored] = colored_toggle_ImageColor3
				toggleInner.Name = "toggleInner"
				toggleInner.Parent = toggle
				toggleInner.Active = true
				toggleInner.AnchorPoint = Vector2.new(0.5, 0.5)
				toggleInner.BackgroundColor3 = library.colors.topGradient
				local colored_toggleInner_BackgroundColor3 = {toggleInner, "BackgroundColor3", "topGradient"}
				colored[1 + #colored] = colored_toggleInner_BackgroundColor3
				toggleInner.BorderColor3 = library.colors.elementBorder
				colored[1 + #colored] = {toggleInner, "BorderColor3", "elementBorder"}
				toggleInner.Position = UDim2.fromScale(0.5, 0.5)
				toggleInner.Selectable = true
				toggleInner.Size = UDim2.new(1, -4, 1, -4)
				toggleInner.Image = "rbxassetid://2454009026"
				toggleInner.ImageColor3 = library.colors.bottomGradient
				local colored_toggleInner_ImageColor3 = {toggleInner, "ImageColor3", "bottomGradient"}
				colored[1 + #colored] = colored_toggleInner_ImageColor3
				toggleButton.Name = "toggleButton"
				toggleButton.Parent = newToggle
				toggleButton.BackgroundColor3 = Color3.new(1, 1, 1)
				toggleButton.BackgroundTransparency = 1
				toggleButton.Size = UDim2.fromScale(1, 1)
				toggleButton.ZIndex = 5
				toggleButton.Font = Enum.Font.SourceSans
				toggleButton.Text = ""
				toggleButton.TextColor3 = Color3.new()
				toggleButton.TextSize = 14
				toggleButton.TextTransparency = 1
				toggleHeadline.Name = "toggleHeadline"
				toggleHeadline.Parent = newToggle
				toggleHeadline.BackgroundColor3 = Color3.new(1, 1, 1)
				toggleHeadline.BackgroundTransparency = 1
				toggleHeadline.Position = UDim2.fromScale(0.123, 0.165842161)
				toggleHeadline.Size = UDim2.fromOffset(170, 11)
				toggleHeadline.Font = Enum.Font.Code
				toggleHeadline.Text = toggleName or "???"
				toggleHeadline.TextColor3 = library.colors.elementText
				local colored_toggleHeadline_TextColor3 = {toggleHeadline, "TextColor3", "elementText", (lockedup and 0.5) or nil}
				colored[1 + #colored] = colored_toggleHeadline_TextColor3
				toggleHeadline.TextSize = 14
				toggleHeadline.TextXAlignment = Enum.TextXAlignment.Left
				local last_v = nil
				local function Set(t, newStatus)
					if nil == newStatus and t ~= nil then
						newStatus = t
					end
					last_v = library_flags[flagName]
					if options.Condition ~= nil then
						if type(options.Condition) == "function" then
							local v, e = pcall(options.Condition, newStatus, last_v)
							if e then
								if not v then
									warn(debug.traceback(string.format("Error in toggle %s's Condition function: %s", flagName, e), 2))
								end
							else
								return last_v
							end
						end
					end
					if newStatus ~= nil and type(newStatus) == "boolean" then
						library_flags[flagName] = newStatus
						if options.Location then
							options.Location[options.LocationFlag or flagName] = newStatus
						end
						if callback and (last_v ~= newStatus or options.AllowDuplicateCalls) then
							colored_toggleInner_BackgroundColor3[3] = (newStatus and "main") or "topGradient"
							colored_toggleInner_BackgroundColor3[4] = (newStatus and 1.5) or nil
							colored_toggleInner_ImageColor3[3] = (newStatus and "main") or "bottomGradient"
							colored_toggleInner_ImageColor3[4] = (newStatus and 2.5) or nil
							tweenService:Create(toggleInner, TweenInfo.new(0.35, library.configuration.easingStyle, library.configuration.easingDirection), {
								BackgroundColor3 = (newStatus and darkenColor(library.colors.main, 1.5)) or library.colors.topGradient,
								ImageColor3 = (newStatus and darkenColor(library.colors.main, 2.5)) or library.colors.bottomGradient
							}):Play()
							task.spawn(callback, newStatus, last_v)
						end
					end
					return newStatus
				end
				options.Keybind = options.Keybind or options.Key or options.KeyBind
				local haskbflag, kbUpdate, kbData = nil, nil, nil
				if options.Keybind then
					local options = options.Keybind
					local htyp = typeof(options)
					if htyp == "EnumItem" then
						options = {
							Value = options
						}
					elseif htyp ~= "table" then
						options = {}
					end
					local presetKeybind, callback, kbpresscallback, kbflag = options.Value or options.Key, options.Callback, options.Pressed, options.Flag or (function()
						if flagName then
							return flagName .. "_ToggleKeybind"
						end
						library.unnamedkeybinds = 1 + (library.unnamedkeybinds or 0)
						return "Keybind" .. tostring(library.unnamedkeybinds)
					end)()
					if elements[kbflag] ~= nil or kbflag == flagName then
						warn(debug.traceback("Warning! Re-used flag '" .. kbflag .. "'", 3))
					end
					haskbflag = kbflag
					library.keyHandler = keyHandler
					local keyHandler = options.KeyNames or keyHandler
					local bindedKey = presetKeybind
					local justBinded = false
					local keyName = keyHandler.allowedKeys[bindedKey] or (bindedKey and (bindedKey.Name or tostring(bindedKey):gsub("Enum.KeyCode.", ""))) or "NONE"
					local newKeybind = newToggle
					keybindPositioner.Name = "keybindPositioner"
					keybindPositioner.Parent = newKeybind
					keybindPositioner.BackgroundColor3 = Color3.new(1, 1, 1)
					keybindPositioner.BackgroundTransparency = 1
					keybindPositioner.Position = UDim2.new(0.00448430516)
					keybindPositioner.Size = UDim2.fromOffset(214, 19)
					keybindPositioner.ZIndex = 1 + toggleButton.ZIndex
					keybindList.Name = "keybindList"
					keybindList.Parent = keybindPositioner
					keybindList.FillDirection = Enum.FillDirection.Horizontal
					keybindList.HorizontalAlignment = Enum.HorizontalAlignment.Right
					keybindList.SortOrder = Enum.SortOrder.LayoutOrder
					keybindList.VerticalAlignment = Enum.VerticalAlignment.Center
					keybindButton.Name = "keybindButton"
					keybindButton.Parent = keybindPositioner
					keybindButton.Active = false
					keybindButton.BackgroundColor3 = Color3.new(1, 1, 1)
					keybindButton.BackgroundTransparency = 1
					keybindButton.Position = UDim2.fromScale(0.598130822, 0.184210524)
					keybindButton.Selectable = false
					keybindButton.Size = UDim2.fromOffset(46, 12)
					keybindButton.Font = Enum.Font.Code
					keybindButton.Text = keyName or (presetKeybind and tostring(presetKeybind):gsub("Enum.KeyCode.", "")) or "[NONE]"
					keybindButton.TextColor3 = library.colors.otherElementText
					local colored_keybindButton_TextColor3 = {keybindButton, "TextColor3", "otherElementText"}
					colored[1 + #colored] = colored_keybindButton_TextColor3
					keybindButton.TextSize = 14
					keybindButton.TextXAlignment = Enum.TextXAlignment.Right
					keybindButton.Size = UDim2.fromOffset(textToSize(keybindButton).X + 4, 12)
					local klast_v = bindedKey or presetKeybind
					local function newkey()
						if lockedup then
							return
						end
						local old_texts = keybindButton.Text
						colored_keybindButton_TextColor3[3] = "main"
						colored_keybindButton_TextColor3[4] = nil
						tweenService:Create(keybindButton, TweenInfo.new(0.35, library.configuration.easingStyle, library.configuration.easingDirection), {
							TextColor3 = library.colors.main
						}):Play()
						if klast_v then
							keybindButton.Text = "(Was " .. (klast_v and tostring(klast_v):gsub("Enum.KeyCode.", "") or "[NONE]") .. ") [...]"
						else
							keybindButton.Text = "[...]"
						end
						local receivingKey = nil
						receivingKey = userInputService.InputBegan:Connect(function(key)
							if lockedup then
								return receivingKey:Disconnect()
							end
							klast_v = library_flags[kbflag]
							if not keyHandler.notAllowedKeys[key.KeyCode] then
								if key.KeyCode ~= Enum.KeyCode.Unknown then
									bindedKey = (key.KeyCode ~= Enum.KeyCode.Escape and key.KeyCode) or library_flags[kbflag]
									library_flags[kbflag] = bindedKey
									if options.Location then
										options.Location[options.LocationFlag or kbflag] = bindedKey
									end
									if bindedKey then
										keyName = keyHandler.allowedKeys[bindedKey] or (bindedKey and (bindedKey.Name or tostring(bindedKey):gsub("Enum.KeyCode.", ""))) or "NONE"
										keybindButton.Text = "[" .. (keyName or (bindedKey and bindedKey.Name) or "NONE") .. "]"
										keybindButton.Size = UDim2.fromOffset(textToSize(keybindButton).X + 4, 12)
										justBinded = true
										colored_keybindButton_TextColor3[3] = "otherElementText"
										colored_keybindButton_TextColor3[4] = nil
										tweenService:Create(keybindButton, TweenInfo.new(0.35, library.configuration.easingStyle, library.configuration.easingDirection), {
											TextColor3 = library.colors.otherElementText
										}):Play()
										receivingKey:Disconnect()
									end
									if callback and klast_v ~= bindedKey then
										task.spawn(callback, bindedKey, klast_v)
									end
									return
								elseif key.KeyCode == Enum.KeyCode.Unknown and not keyHandler.notAllowedMouseInputs[key.UserInputType] then
									bindedKey = key.UserInputType
									library_flags[kbflag] = bindedKey
									if options.Location then
										options.Location[options.LocationFlag or kbflag] = bindedKey
									end
									keyName = keyHandler.allowedKeys[bindedKey]
									keybindButton.Text = "[" .. (keyName or (bindedKey and bindedKey.Name) or tostring(bindedKey.KeyCode):gsub("Enum.KeyCode.", "")) .. "]"
									keybindButton.Size = UDim2.fromOffset(textToSize(keybindButton).X + 4, 12)
									justBinded = true
									colored_keybindButton_TextColor3[3] = "otherElementText"
									colored_keybindButton_TextColor3[4] = nil
									tweenService:Create(keybindButton, TweenInfo.new(0.35, library.configuration.easingStyle, library.configuration.easingDirection), {
										TextColor3 = library.colors.otherElementText
									}):Play()
									receivingKey:Disconnect()
									if callback and klast_v ~= bindedKey then
										task.spawn(callback, bindedKey, klast_v)
									end
									return
								end
							end
							if key.KeyCode == Enum.KeyCode.Backspace or Enum.KeyCode.Escape == key.KeyCode then
								old_texts, bindedKey = "[NONE]", nil
							end
							keybindButton.Text = old_texts
							colored_keybindButton_TextColor3[3] = "otherElementText"
							colored_keybindButton_TextColor3[4] = nil
							tweenService:Create(keybindButton, TweenInfo.new(0.35, library.configuration.easingStyle, library.configuration.easingDirection), {
								TextColor3 = library.colors.otherElementText
							}):Play()
							receivingKey:Disconnect()
							if callback and klast_v ~= bindedKey then
								task.spawn(callback, bindedKey, klast_v)
							end
						end)
						library.signals[1 + #library.signals] = receivingKey
					end
					library.signals[1 + #library.signals] = keybindButton.MouseButton1Click:Connect(newkey)
					if kbpresscallback and not justBinded then
						library.signals[1 + #library.signals] = userInputService.InputBegan:Connect(function(key, chatting)
							chatting = chatting or not not userInputService:GetFocusedTextBox()
							if not chatting and not justBinded then
								if not keyHandler.notAllowedKeys[key.KeyCode] and not keyHandler.notAllowedMouseInputs[key.UserInputType] then
									if bindedKey == key.UserInputType or not justBinded and bindedKey == key.KeyCode then
										if kbpresscallback then
											task.spawn(kbpresscallback, key, chatting)
										end
									end
									justBinded = false
								end
							end
						end)
					end
					options.Mode = (options.Mode and string.lower(tostring(options.Mode))) or "dynamic"
					local modes = {
						dynamic = 1,
						hold = 1,
						toggle = 1
					}
					library.signals[1 + #library.signals] = userInputService.InputBegan:Connect(function(input, chatting)
						if justBinded then
							wait(0.1)
							justBinded = false
							return
						elseif lockedup then
							return
						end
						chatting = chatting or userInputService:GetFocusedTextBox()
						if not chatting then
							local key = library_flags[kbflag]
							local mode = options.Mode
							if not modes[mode] then
								mode = "dynamic"
								options.Mode = mode
							end
							if key == input.KeyCode or key == input.UserInputType then
								if mode == "dynamic" or mode == "both" or mode == "hold" then
									if mode == "dynamic" and library_flags[flagName] then
										return Set(false)
									end
									Set(true)
									local now = os.clock()
									local waittil = nil
									if mode == "dynamic" then
										waittil = Instance.new("BindableEvent")
									end
									local xconnection = nil
									xconnection = userInputService.InputEnded:Connect(function(input, chatting)
										chatting = chatting or userInputService:GetFocusedTextBox()
										if not chatting and (key == input.KeyCode or key == input.UserInputType) then
											xconnection = (xconnection and xconnection:Disconnect() and nil) or nil
											if mode == "hold" or os.clock() - now > math.clamp(tonumber(options.DynamicTime) or 0.65, 0.05, 20) then
												Set(false)
											end
										end
									end)
									library.signals[1 + #library.signals] = xconnection
								else
									Set(not library_flags[flagName])
								end
							end
						end
					end)
					local function kbset(t, key)
						if nil == key and t ~= nil then
							key = t
						end
						if key == "nil" or key == "NONE" or key == "none" then
							key = nil
						end
						last_v = library_flags[kbflag]
						bindedKey = key
						library_flags[kbflag] = key
						if options.Location then
							options.Location[options.LocationFlag or kbflag] = key
						end
						keyName = (key == nil and "NONE") or keyHandler.allowedKeys[key]
						keybindButton.Text = "[" .. (keyName or key.Name or tostring(key):gsub("Enum.KeyCode.", "")) .. "]"
						keybindButton.Size = UDim2.fromOffset(textToSize(keybindButton).X + 4, 12)
						justBinded = true
						colored_keybindButton_TextColor3[3] = "otherElementText"
						colored_keybindButton_TextColor3[4] = nil
						tweenService:Create(keybindButton, TweenInfo.new(0.35, library.configuration.easingStyle, library.configuration.easingDirection), {
							TextColor3 = library.colors.otherElementText
						}):Play()
						if callback and (last_v ~= key or options.AllowDuplicateCalls) then
							task.spawn(callback, key, last_v)
						end
						return key
					end
					if presetKeybind ~= nil then
						kbset(presetKeybind)
					else
						library_flags[kbflag] = bindedKey
						if options.Location then
							options.Location[options.LocationFlag or kbflag] = bindedKey
						end
					end
					local default = library_flags[kbflag]
					local function UpdateKb()
						callback, kbpresscallback = options.Callback, options.Pressed
						local key = library_flags[kbflag]
						bindedKey = key
						keyName = keyHandler.allowedKeys[bindedKey] or (bindedKey and (bindedKey.Name or tostring(bindedKey):gsub("Enum.KeyCode.", ""))) or "NONE"
						keybindButton.Text = "[" .. (keyName or (key and key.Name) or tostring(key):gsub("Enum.KeyCode.", "")) .. "]"
						keybindButton.Size = UDim2.fromOffset(textToSize(keybindButton).X + 4, 12)
						colored_keybindButton_TextColor3[3] = "otherElementText"
						colored_keybindButton_TextColor3[4] = (lockedup and 2.5) or nil
						tweenService:Create(keybindButton, TweenInfo.new(0.35, library.configuration.easingStyle, library.configuration.easingDirection), {
							TextColor3 = (lockedup and darkenColor(library.colors.otherElementText, colored_keybindButton_TextColor3[4])) or library.colors.otherElementText
						}):Play()
						return key
					end
					kbUpdate = UpdateKb
					local objectdata = {
						Options = options,
						Name = kbflag,
						Flag = kbflag,
						Type = "Keybind",
						Default = default,
						Parent = sectionFunctions,
						Instance = keybindButton,
						Get = function()
							return library_flags[kbflag]
						end,
						Set = kbset,
						RawSet = function(t, key)
							if t ~= nil and key == nil then
								key = t
							end
							library_flags[kbflag] = key
							UpdateKb()
							return key
						end,
						Update = UpdateKb,
						Reset = function()
							return kbset(nil, default)
						end
					}
					kbData = objectdata
					tabFunctions.Flags[kbflag], sectionFunctions.Flags[kbflag], elements[kbflag] = objectdata, objectdata, objectdata
				end
				sectionFunctions:Update()
				library.signals[1 + #library.signals] = toggleButton.MouseButton1Click:Connect(function()
					if not library.colorpicker and not submenuOpen and not lockedup then
						local newval = not library_flags[flagName]
						if options.Condition ~= nil then
							if type(options.Condition) == "function" then
								local v, e = pcall(options.Condition, newval, not newval)
								if e then
									if not v then
										warn(debug.traceback(string.format("Error in toggle %s's Condition function: %s", flagName, e), 2))
									end
								else
									return last_v
								end
							end
						end
						library_flags[flagName] = newval
						if options.Location then
							options.Location[options.LocationFlag or flagName] = newval
						end
						colored_toggleInner_BackgroundColor3[3] = (newval and "main") or "topGradient"
						colored_toggleInner_BackgroundColor3[4] = (newval and 1.5) or nil
						colored_toggleInner_ImageColor3[3] = (newval and "main") or "bottomGradient"
						colored_toggleInner_ImageColor3[4] = (newval and 2.5) or nil
						tweenService:Create(toggleInner, TweenInfo.new(0.35, library.configuration.easingStyle, library.configuration.easingDirection), {
							BackgroundColor3 = (newval and darkenColor(library.colors.main, 1.5)) or library.colors.topGradient,
							ImageColor3 = (newval and darkenColor(library.colors.main, 2.5)) or library.colors.bottomGradient
						}):Play()
						if callback then
							task.spawn(callback, newval)
						end
					end
				end)
				library.signals[1 + #library.signals] = newToggle.MouseEnter:Connect(function()
					colored_toggle_BackgroundColor3[3] = "main"
					colored_toggle_BackgroundColor3[4] = 1.5
					colored_toggle_ImageColor3[3] = "main"
					colored_toggle_ImageColor3[4] = 2.5
					tweenService:Create(toggle, TweenInfo.new(0.35, library.configuration.easingStyle, library.configuration.easingDirection), {
						BackgroundColor3 = darkenColor(library.colors.main, 1.5),
						ImageColor3 = darkenColor(library.colors.main, 2.5)
					}):Play()
				end)
				library.signals[1 + #library.signals] = newToggle.MouseLeave:Connect(function()
					colored_toggle_BackgroundColor3[3] = "topGradient"
					colored_toggle_BackgroundColor3[4] = nil
					colored_toggle_ImageColor3[3] = "bottomGradient"
					colored_toggle_ImageColor3[4] = nil
					tweenService:Create(toggle, TweenInfo.new(0.35, library.configuration.easingStyle, library.configuration.easingDirection), {
						BackgroundColor3 = library.colors.topGradient,
						ImageColor3 = library.colors.bottomGradient
					}):Play()
				end)
				if library_flags[flagName] then
					colored_toggleInner_BackgroundColor3[3] = "main"
					colored_toggleInner_BackgroundColor3[4] = 1.5
					colored_toggleInner_ImageColor3[3] = "main"
					colored_toggleInner_ImageColor3[4] = 2.5
					tweenService:Create(toggleInner, TweenInfo.new(0.35, library.configuration.easingStyle, library.configuration.easingDirection), {
						BackgroundColor3 = darkenColor(library.colors.main, 1.5),
						ImageColor3 = darkenColor(library.colors.main, 2.5)
					}):Play()
				end
				local function Update()
					toggleName, callback = options.Name or toggleName, options.Callback
					local boolstatus = library_flags[flagName]
					colored_toggleInner_BackgroundColor3[3] = (boolstatus and "main") or "topGradient"
					colored_toggleInner_BackgroundColor3[4] = (boolstatus and 1.5) or nil
					colored_toggleInner_ImageColor3[3] = (boolstatus and "main") or "bottomGradient"
					colored_toggleInner_ImageColor3[4] = (boolstatus and 2.5) or nil
					if lockedup then
						colored_toggleInner_BackgroundColor3[4] = 1 + (colored_toggleInner_BackgroundColor3[4] or 1)
						colored_toggleInner_ImageColor3[4] = 1 + (colored_toggleInner_ImageColor3[4] or 1)
					end
					tweenService:Create(toggleInner, TweenInfo.new(0.35, library.configuration.easingStyle, library.configuration.easingDirection), {
						BackgroundColor3 = (boolstatus and darkenColor(library.colors.main, colored_toggleInner_BackgroundColor3[4])) or library.colors.topGradient,
						ImageColor3 = (boolstatus and darkenColor(library.colors.main, colored_toggleInner_ImageColor3[4])) or library.colors.bottomGradient
					}):Play()
					colored_toggleHeadline_TextColor3[4] = (lockedup and 2.5) or nil
					tweenService:Create(toggleHeadline, TweenInfo.new(0.35, library.configuration.easingStyle, library.configuration.easingDirection), {
						TextColor3 = (lockedup and darkenColor(library.colors.elementText, colored_toggleHeadline_TextColor3[4])) or library.colors.elementText
					}):Play()
					toggleHeadline.Text = toggleName or "???"
					return boolstatus
				end
				if alreadyEnabled ~= nil then
					Set(alreadyEnabled)
				else
					library_flags[flagName] = not not alreadyEnabled
					if options.Location then
						options.Location[options.LocationFlag or flagName] = not not alreadyEnabled
					end
				end
				local default = not not library_flags[flagName]
				Update()
				if kbUpdate then
					kbUpdate()
				end
				local objectdata = {
					Options = options,
					Type = "Toggle",
					Name = flagName,
					Flag = flagName,
					Default = default,
					Parent = sectionFunctions,
					Instance = toggleButton,
					Set = Set,
					RawSet = function(t, newStatus, condition)
						if t ~= nil and type(t) ~= "table" then
							newStatus, condition = t, newStatus
						end
						last_v = library_flags[flagName]
						if condition ~= false and condition ~= 0 then
							local overridecondition = condition and type(condition) == "function" and condition
							if overridecondition or options.Condition ~= nil then
								if type(overridecondition or options.Condition) == "function" then
									local v, e = pcall(overridecondition or options.Condition, newStatus, last_v)
									if e then
										if not v then
											warn(debug.traceback(string.format("Error in toggle (RawSet) %s's Condition function: %s", flagName, e), 2))
										end
									else
										return last_v
									end
								end
							end
						end
						library_flags[flagName] = newStatus
						if options.Location then
							options.Location[options.LocationFlag or flagName] = newStatus
						end
						Update()
						return newStatus
					end,
					KeybindData = kbData,
					Get = function()
						return library_flags[flagName]
					end,
					Update = Update,
					Reset = function()
						return Set(nil, default)
					end,
					SetLocked = function(t, state)
						if type(t) ~= "table" then
							state = t
						end
						local last_v = lockedup
						if state == nil then
							lockedup = not lockedup
						else
							lockedup = state
						end
						if lockedup ~= last_v then
							colored_toggleHeadline_TextColor3[4] = (lockedup and 2.5) or nil
							Update()
							if kbUpdate then
								kbUpdate()
							end
						end
						return lockedup
					end,
					Lock = function()
						if not lockedup then
							lockedup = true
							colored_toggleHeadline_TextColor3[4] = 2.5
							Update()
							if kbUpdate then
								kbUpdate()
							end
						end
						return lockedup
					end,
					Unlock = function()
						if lockedup then
							lockedup = false
							colored_toggleHeadline_TextColor3[4] = nil
							Update()
							if kbUpdate then
								kbUpdate()
							end
						end
						return lockedup
					end,
					SetCondition = function(t, condition)
						if type(t) ~= "table" and condition == nil then
							condition = t
						end
						options.Condition = condition
						return condition
					end
				}
				if kbData then
					kbData.ToggleData = objectdata
				end
				tabFunctions.Flags[flagName], sectionFunctions.Flags[flagName], elements[flagName] = objectdata, objectdata, objectdata
				return objectdata
			end
			sectionFunctions.CreateToggle = sectionFunctions.AddToggle
			sectionFunctions.NewToggle = sectionFunctions.AddToggle
			sectionFunctions.Toggle = sectionFunctions.AddToggle
			sectionFunctions.Tog = sectionFunctions.AddToggle
			function sectionFunctions:AddButton(...)
				local args = nil
				if ... and not select(2, ...) and type(...) == "table" and #... > 0 and type((...)[1]) == "table" and (...)[1].Name then
					args = ...
				else
					args = {...}
				end
				local buttons, offset = {}, 0
				local fram = nil
				for _, options in next, args do
					options = (options and options[1] and type(options[1]) == "string" and resolvevararg("Button", unpack(options))) or options
					local buttonName, callback = assert(options.Name, "Missing Name for new button."), options.Callback or (warn("AddButton missing callback. Name:", options.Name or "No Name", debug.traceback("")) and nil) or function()
					end
					local lockedup = options.Locked
					local realButton = Instance_new("TextButton")
					realButton.Name = "realButton"
					realButton.BackgroundColor3 = Color3.new(1, 1, 1)
					realButton.BackgroundTransparency = 1
					realButton.Size = UDim2.fromScale(1, 1)
					realButton.ZIndex = 5
					realButton.Font = Enum.Font.Code
					realButton.Text = (buttonName and tostring(buttonName)) or "???"
					realButton.TextColor3 = library.colors.elementText
					local colored_realButton_TextColor3 = {realButton, "TextColor3", "elementText"}
					colored[1 + #colored] = colored_realButton_TextColor3
					realButton.TextSize = 14
					local textsize = textToSize(realButton).X + 14
					if newSection.Parent.AbsoluteSize.X < offset + textsize + 8 then
						offset, fram = 0, nil
					end
					local newButton = fram or Instance_new("Frame")
					fram = newButton
					local button = Instance_new("ImageLabel")
					newButton.Name = removeSpaces((buttonName and buttonName:lower() or "???") .. "Holder")
					newButton.Parent = sectionHolder
					newButton.BackgroundColor3 = Color3.new(1, 1, 1)
					newButton.BackgroundTransparency = 1
					newButton.Size = UDim2.new(1, 0, 0, 24)
					button.Name = "button"
					button.Parent = newButton
					button.Active = true
					button.BackgroundColor3 = library.colors.topGradient
					local colored_button_BackgroundColor3 = {button, "BackgroundColor3", "topGradient"}
					colored[1 + #colored] = colored_button_BackgroundColor3
					button.BorderColor3 = library.colors.elementBorder
					colored[1 + #colored] = {button, "BorderColor3", "elementBorder"}
					button.Position = UDim2.new(0.031, offset, 0.166)
					button.Selectable = true
					button.Size = UDim2.fromOffset(28, 18)
					button.Image = "rbxassetid://2454009026"
					button.ImageColor3 = library.colors.bottomGradient
					local colored_button_ImageColor3 = {button, "ImageColor3", "bottomGradient"}
					colored[1 + #colored] = colored_button_ImageColor3
					local buttonInner = Instance_new("ImageLabel")
					buttonInner.Name = "buttonInner"
					buttonInner.Parent = button
					buttonInner.Active = true
					buttonInner.AnchorPoint = Vector2.new(0.5, 0.5)
					buttonInner.BackgroundColor3 = library.colors.topGradient
					local colored_buttonInner_BackgroundColor3 = {buttonInner, "BackgroundColor3", "topGradient"}
					colored[1 + #colored] = colored_buttonInner_BackgroundColor3
					buttonInner.BorderColor3 = library.colors.elementBorder
					colored[1 + #colored] = {buttonInner, "BorderColor3", "elementBorder"}
					buttonInner.Position = UDim2.fromScale(0.5, 0.5)
					buttonInner.Selectable = true
					buttonInner.Size = UDim2.new(1, -4, 1, -4)
					buttonInner.Image = "rbxassetid://2454009026"
					buttonInner.ImageColor3 = library.colors.bottomGradient
					local colored_buttonInner_ImageColor3 = {buttonInner, "ImageColor3", "bottomGradient"}
					colored[1 + #colored] = colored_buttonInner_ImageColor3
					button.Size = UDim2.fromOffset(textsize, 18)
					realButton.Parent = button
					offset = offset + textsize + 6
					sectionFunctions:Update()
					local presses = 0
					library.signals[1 + #library.signals] = realButton.MouseButton1Click:Connect(function()
						if lockedup then
							return
						end
						if options.Condition ~= nil and type(options.Condition) == "function" then
							local v, e = pcall(options.Condition, presses)
							if e then
								if not v then
									warn(debug.traceback(string.format("Error in button %s's Condition function: %s", buttonName, e), 2))
								end
							else
								return
							end
						end
						if not library.colorpicker and not submenuOpen then
							presses = 1 + presses
							task.spawn(callback, presses)
						end
					end)
					local imin = nil
					library.signals[1 + #library.signals] = button.MouseEnter:Connect(function()
						imin = 1
						colored_button_BackgroundColor3[3] = "main"
						colored_button_BackgroundColor3[4] = 1.5
						colored_button_ImageColor3[3] = "main"
						colored_button_ImageColor3[4] = 2.5
						tweenService:Create(button, TweenInfo.new(0.35, library.configuration.easingStyle, library.configuration.easingDirection), {
							BackgroundColor3 = darkenColor(library.colors.main, 1.5),
							ImageColor3 = darkenColor(library.colors.main, 2.5)
						}):Play()
					end)
					library.signals[1 + #library.signals] = button.MouseLeave:Connect(function()
						imin = nil
						colored_button_BackgroundColor3[3] = "topGradient"
						colored_button_BackgroundColor3[4] = nil
						colored_button_ImageColor3[3] = "bottomGradient"
						colored_button_ImageColor3[4] = nil
						tweenService:Create(button, TweenInfo.new(0.35, library.configuration.easingStyle, library.configuration.easingDirection), {
							BackgroundColor3 = library.colors.topGradient,
							ImageColor3 = library.colors.bottomGradient
						}):Play()
					end)
					local function Update()
						buttonName, callback = options.Name or buttonName, options.Callback or (warn(debug.traceback("AddButton missing callback. Name:" .. (options.Name or buttonName or "No Name"), 2)) and nil) or function()
						end
						colored_button_BackgroundColor3[3] = (imin and "main") or "topGradient"
						colored_button_BackgroundColor3[4] = (imin and 1.5) or nil
						colored_button_ImageColor3[3] = (imin and "main") or "bottomGradient"
						colored_button_ImageColor3[4] = (imin and 2.5) or nil
						colored_buttonInner_BackgroundColor3[4] = nil
						colored_buttonInner_ImageColor3[4] = nil
						colored_realButton_TextColor3[4] = nil
						if lockedup then
							colored_button_BackgroundColor3[4] = 1.25
							colored_button_ImageColor3[4] = 1.25
							colored_buttonInner_BackgroundColor3[4] = 1.25
							colored_buttonInner_ImageColor3[4] = 1.25
							colored_realButton_TextColor3[4] = 1.75
						end
						tweenService:Create(button, TweenInfo.new(0.35, library.configuration.easingStyle, library.configuration.easingDirection), {
							BackgroundColor3 = (imin and darkenColor(library.colors.main, colored_button_BackgroundColor3[4])) or darkenColor(library.colors.topGradient, colored_button_BackgroundColor3[4]),
							ImageColor3 = (imin and darkenColor(library.colors.main, colored_button_ImageColor3[4])) or darkenColor(library.colors.bottomGradient, colored_button_ImageColor3[4])
						}):Play()
						tweenService:Create(buttonInner, TweenInfo.new(0.35, library.configuration.easingStyle, library.configuration.easingDirection), {
							BackgroundColor3 = darkenColor(library.colors.topGradient, colored_buttonInner_BackgroundColor3[4]),
							ImageColor3 = darkenColor(library.colors.bottomGradient, colored_buttonInner_ImageColor3[4])
						}):Play()
						tweenService:Create(realButton, TweenInfo.new(0.35, library.configuration.easingStyle, library.configuration.easingDirection), {
							TextColor3 = darkenColor(library.colors.elementText, colored_realButton_TextColor3[4])
						}):Play()
						realButton.Text = (buttonName and tostring(buttonName)) or "???"
						return presses
					end
					Update()
					local objectdata = {
						Options = options,
						Name = buttonName,
						Flag = buttonName,
						Type = "Button",
						Parent = sectionFunctions,
						Instance = realButton,
						Press = function(...)
							if lockedup then
								return presses
							end
							if options.Condition ~= nil and type(options.Condition) == "function" then
								local v, e = pcall(options.Condition, presses)
								if e then
									if not v then
										warn(debug.traceback(string.format("Error in button %s's Condition function: %s", buttonName, e), 2))
									end
								else
									return presses
								end
							end
							local args = {...}
							local a1 = args[1]
							if a1 and type(a1) == "table" then
								table.remove(args, 1)
							end
							presses = 1 + presses
							task.spawn(callback, presses, ...)
							return presses
						end,
						RawPress = function(...)
							local args = {...}
							local a1 = args[1]
							if a1 and type(a1) == "table" then
								table.remove(args, 1)
							end
							task.spawn(callback, presses, ...)
							return presses
						end,
						Get = function()
							return callback, presses
						end,
						SetLocked = function(t, state)
							if type(t) ~= "table" then
								state = t
							end
							local last_v = lockedup
							if state == nil then
								lockedup = not lockedup
							else
								lockedup = state
							end
							if lockedup ~= last_v then
								Update()
							end
							return lockedup
						end,
						Lock = function()
							if not lockedup then
								lockedup = true
								Update()
							end
							return lockedup
						end,
						Unlock = function()
							if lockedup then
								lockedup = false
								Update()
							end
							return lockedup
						end,
						SetCondition = function(t, condition)
							if type(t) ~= "table" and condition == nil then
								condition = t
							end
							options.Condition = condition
							return condition
						end,
						Update = Update,
						SetText = function(t, str)
							if type(t) ~= "table" and str == nil then
								str = t
							end
							buttonName = str
							options.Name = str
							realButton.Text = (buttonName and tostring(buttonName)) or "???"
							return str
						end,
						SetCallback = function(t, call)
							if type(t) ~= "table" and call == nil then
								call = t
							end
							options.Callback = call
							callback = call
							return call
						end
					}
					tabFunctions.Flags[buttonName], sectionFunctions.Flags[buttonName], elements[buttonName] = objectdata, objectdata, objectdata
					buttons[1 + #buttons] = objectdata
				end
				function buttons.PressAll()
					for _, v in next, buttons do
						v.Press()
					end
				end
				function buttons.UpdateAll()
					for _, v in next, buttons do
						v.Update()
					end
				end
				if #buttons == 1 then
					for k, v in next, buttons[1] do
						if buttons[k] == nil then
							buttons[k] = v
						end
					end
				end
				return buttons
			end
			sectionFunctions.CreateButton = sectionFunctions.AddButton
			sectionFunctions.NewButton = sectionFunctions.AddButton
			sectionFunctions.Button = sectionFunctions.AddButton
			function sectionFunctions:AddTextbox(options, ...)
				options = (options and type(options) == "string" and resolvevararg("Textbox", options, ...)) or options
				local textboxName, presetValue, placeholder, callback, flagName = assert(options.Name, "Missing Name for new textbox."), options.Value, options.Placeholder, options.Callback, options.Flag or (function()
					library.unnamedtextboxes = 1 + (library.unnamedtextboxes or 0)
					return "Textbox" .. tostring(library.unnamedtextboxes)
				end)()
				if elements[flagName] ~= nil then
					warn(debug.traceback("Warning! Re-used flag '" .. flagName .. "'", 3))
				end
				local requiredtype = options.Type
				local newTextbox = Instance_new("Frame")
				local textbox = Instance_new("ImageLabel")
				local textboxInner = Instance_new("ImageLabel")
				local realTextbox = Instance_new("TextBox")
				local textboxHeadline = Instance_new("TextLabel")
				newTextbox.Name = removeSpaces((textboxName and textboxName:lower()) or "???") .. "Holder"
				newTextbox.Parent = sectionHolder
				newTextbox.BackgroundColor3 = Color3.new(1, 1, 1)
				newTextbox.BackgroundTransparency = 1
				newTextbox.Size = UDim2.new(1, 0, 0, 42)
				textbox.Name = "textbox"
				textbox.Parent = newTextbox
				textbox.Active = true
				textbox.BackgroundColor3 = library.colors.topGradient
				local colored_textbox_BackgroundColor3 = {textbox, "BackgroundColor3", "topGradient"}
				colored[1 + #colored] = colored_textbox_BackgroundColor3
				textbox.BorderColor3 = library.colors.elementBorder
				colored[1 + #colored] = {textbox, "BorderColor3", "elementBorder"}
				textbox.Position = UDim2.fromScale(0.031, 0.48)
				textbox.Selectable = true
				textbox.Size = UDim2.fromOffset(206, 18)
				textbox.Image = "rbxassetid://2454009026"
				textbox.ImageColor3 = library.colors.bottomGradient
				local colored_textbox_ImageColor3 = {textbox, "ImageColor3", "bottomGradient"}
				colored[1 + #colored] = colored_textbox_ImageColor3
				textboxInner.Name = "textboxInner"
				textboxInner.Parent = textbox
				textboxInner.Active = true
				textboxInner.AnchorPoint = Vector2.new(0.5, 0.5)
				textboxInner.BackgroundColor3 = library.colors.topGradient
				colored[1 + #colored] = {textboxInner, "BackgroundColor3", "topGradient"}
				textboxInner.BorderColor3 = library.colors.elementBorder
				colored[1 + #colored] = {textboxInner, "BorderColor3", "elementBorder"}
				textboxInner.Position = UDim2.fromScale(0.5, 0.5)
				textboxInner.Selectable = true
				textboxInner.Size = UDim2.new(1, -4, 1, -4)
				textboxInner.Image = "rbxassetid://2454009026"
				textboxInner.ImageColor3 = library.colors.bottomGradient
				colored[1 + #colored] = {textboxInner, "ImageColor3", "bottomGradient"}
				realTextbox.Name = "realTextbox"
				if options.Rich or options.RichText or options.RichTextBox then
					realTextbox.RichText = true
				end
				if options.MultiLine or options.Lines then
					realTextbox.MultiLine = true
				end
				if options.Font or options.TextFont then
					realTextbox.Font = options.Font
				end
				if options.TextScaled or options.Scaled then
					realTextbox.TextScaled = true
				end
				realTextbox.BackgroundColor3 = Color3.new(1, 1, 1)
				realTextbox.BackgroundTransparency = 1
				realTextbox.Position = UDim2.new(0.0295485705)
				realTextbox.Size = UDim2.fromScale(0.97, 1)
				realTextbox.ZIndex = 5
				realTextbox.Font = Enum.Font.Code
				realTextbox.LineHeight = 1.15
				realTextbox.Text = tostring(presetValue)
				realTextbox.TextColor3 = library.colors.otherElementText
				colored[1 + #colored] = {realTextbox, "TextColor3", "otherElementText"}
				realTextbox.TextSize = 14
				if options.ClearTextOnFocus or options.ClearText then
					realTextbox.ClearTextOnFocus = true
				else
					realTextbox.ClearTextOnFocus = false
				end
				realTextbox.PlaceholderText = (placeholder ~= nil and tostring(placeholder)) or (presetValue ~= nil and tostring(presetValue)) or ""
				realTextbox.TextXAlignment = Enum.TextXAlignment.Left
				if options.CustomProperties and type(options.CustomProperties) == "table" then
					for k, v in next, options.CustomProperties do
						local oof, e = pcall(function()
							realTextbox[k] = v
						end)
						if not oof and e then
							warn("Error setting Textbox", flagName, "|", e, debug.traceback(""))
						end
					end
				end
				realTextbox.Parent = textbox
				textboxHeadline.Name = "textboxHeadline"
				textboxHeadline.Parent = newTextbox
				textboxHeadline.Active = true
				textboxHeadline.BackgroundColor3 = Color3.new(1, 1, 1)
				textboxHeadline.BackgroundTransparency = 1
				textboxHeadline.Position = UDim2.new(0.031)
				textboxHeadline.Selectable = true
				textboxHeadline.Size = UDim2.fromOffset(206, 20)
				textboxHeadline.ZIndex = 5
				textboxHeadline.Font = Enum.Font.Code
				textboxHeadline.LineHeight = 1.15
				textboxHeadline.Text = (textboxName and tostring(textboxName)) or "???"
				textboxHeadline.TextColor3 = library.colors.elementText
				colored[1 + #colored] = {textboxHeadline, "TextColor3", "elementText"}
				textboxHeadline.TextSize = 14
				textboxHeadline.TextXAlignment = Enum.TextXAlignment.Left
				sectionFunctions:Update()
				local last_v = presetValue
				local function resolvevalue(val)
					if options.PreFormat then
						local typ = type(options.PreFormat)
						if typ == "function" then
							local x, e = pcall(options.PreFormat, val)
							if not x and e then
								warn("Error in Pre-Format (Textbox " .. flagName .. "):", e)
							else
								val = e
							end
						end
					end
					if requiredtype == "number" then
						if not options.Hex and not options.Binary and not options.Base then
							val = tonumber(val) or tonumber(val:gsub("%D", ""), 10) or 0
						else
							val = tonumber(val, (options.Hex and 16) or (options.Binary and 2) or options.Base or 10) or 0
						end
						if options.Max or options.Min then
							val = math.clamp(val, options.Min or -math.huge, options.Max or math.huge)
						end
						local decimalprecision = tonumber(options.Decimals or options.Precision or options.Precise)
						if decimalprecision then
							val = tonumber(string.format("%0." .. tostring(decimalprecision) .. "f", val))
						end
					end
					if options.PostFormat then
						local typ = type(options.PostFormat)
						if typ == "function" then
							local x, e = pcall(options.PostFormat, val)
							if not x and e then
								warn("Error in Post-Format (Textbox " .. flagName .. "):", e)
							else
								val = e
							end
						end
					end
					return (val and tonumber(val)) or val
				end
				library.signals[1 + #library.signals] = realTextbox.FocusLost:Connect(function()
					last_v = library_flags[flagName]
					local val = resolvevalue(realTextbox.Text)
					library_flags[flagName] = val
					if options.Location then
						options.Location[options.LocationFlag or flagName] = val
					end
					if callback and last_v ~= val then
						task.spawn(callback, tostring(val), last_v, realTextbox)
					end
				end)
				library.signals[1 + #library.signals] = newTextbox.MouseEnter:Connect(function()
					colored_textbox_BackgroundColor3[3] = "main"
					colored_textbox_BackgroundColor3[4] = 1.5
					colored_textbox_ImageColor3[3] = "main"
					colored_textbox_ImageColor3[4] = 2.5
					tweenService:Create(textbox, TweenInfo.new(0.35, library.configuration.easingStyle, library.configuration.easingDirection), {
						BackgroundColor3 = darkenColor(library.colors.main, 1.5),
						ImageColor3 = darkenColor(library.colors.main, 2.5)
					}):Play()
				end)
				library.signals[1 + #library.signals] = newTextbox.MouseLeave:Connect(function()
					colored_textbox_BackgroundColor3[3] = "topGradient"
					colored_textbox_BackgroundColor3[4] = nil
					colored_textbox_ImageColor3[3] = "bottomGradient"
					colored_textbox_ImageColor3[4] = nil
					tweenService:Create(textbox, TweenInfo.new(0.35, library.configuration.easingStyle, library.configuration.easingDirection), {
						BackgroundColor3 = library.colors.topGradient,
						ImageColor3 = library.colors.bottomGradient
					}):Play()
				end)
				local function set(t, str)
					if nil == str and t ~= nil then
						str = t
					end
					last_v = library_flags[flagName]
					library_flags[flagName] = str
					if options.Location then
						options.Location[options.LocationFlag or flagName] = str
					end
					local sstr = (str ~= nil and tostring(str)) or "Empty Text"
					if realTextbox.Text ~= sstr then
						realTextbox.Text = sstr
					end
					if callback and (last_v ~= str or options.AllowDuplicateCalls) then
						task.spawn(callback, str, last_v, realTextbox)
					end
					return str
				end
				if presetValue ~= nil then
					set(presetValue)
				else
					library_flags[flagName] = presetValue
					if options.Location then
						options.Location[options.LocationFlag or flagName] = presetValue
					end
				end
				local default = library_flags[flagName]
				local function update()
					textboxName, placeholder, callback = options.Name or textboxName, options.Placeholder or placeholder, options.Callback
					local str = library_flags[flagName]
					str = (str ~= nil and tostring(str)) or "Empty Text"
					if realTextbox.Text ~= str then
						realTextbox.Text = str
					end
					textboxHeadline.Text = (textboxName and tostring(textboxName)) or "???"
					return str
				end
				local objectdata = {
					Options = options,
					Name = flagName,
					Flag = flagName,
					Type = "Textbox",
					Default = default,
					Parent = sectionFunctions,
					Instance = realTextbox,
					Get = function()
						return library_flags[flagName]
					end,
					Set = set,
					Update = update,
					RawSet = function(t, str)
						if t ~= nil and str == nil then
							str = t
						end
						last_v = library_flags[flagName]
						library_flags[flagName] = str
						if options.Location then
							options.Location[options.LocationFlag or flagName] = str
						end
						update()
						return str
					end,
					Reset = function()
						return set(nil, default)
					end
				}
				tabFunctions.Flags[flagName], sectionFunctions.Flags[flagName], elements[flagName] = objectdata, objectdata, objectdata
				return objectdata
			end
			sectionFunctions.AddTextBox = sectionFunctions.AddTextbox
			sectionFunctions.NewTextBox = sectionFunctions.AddTextbox
			sectionFunctions.CreateTextBox = sectionFunctions.AddTextbox
			sectionFunctions.TextBox = sectionFunctions.AddTextbox
			sectionFunctions.NewTextbox = sectionFunctions.AddTextbox
			sectionFunctions.CreateTextbox = sectionFunctions.AddTextbox
			sectionFunctions.Textbox = sectionFunctions.AddTextbox
			sectionFunctions.Box = sectionFunctions.AddTextbox
			function sectionFunctions:AddKeybind(options, ...)
				options = (options and type(options) == "string" and resolvevararg("Keybind", options, ...)) or options
				local keybindName, presetKeybind, callback, presscallback, flag = assert(options.Name, "Missing Name for new keybind."), options.Value, options.Callback, options.Pressed, options.Flag or (function()
					library.unnamedkeybinds = 1 + (library.unnamedkeybinds or 0)
					return "Keybind" .. tostring(library.unnamedkeybinds)
				end)()
				if elements[flag] ~= nil then
					warn(debug.traceback("Warning! Re-used flag '" .. flag .. "'", 3))
				end
				library.keyHandler = keyHandler
				local keyHandler = options.KeyNames or keyHandler
				local newKeybind = Instance_new("Frame")
				local keybindHeadline = Instance_new("TextLabel")
				local keybindPositioner = Instance_new("Frame")
				local keybindList = Instance_new("UIListLayout")
				local keybindButton = Instance_new("TextButton")
				local bindedKey = presetKeybind
				local justBinded = false
				local keyName = (presetKeybind and tostring(presetKeybind):gsub("Enum.KeyCode.", "") or "")
				newKeybind.Name = "newKeybind"
				newKeybind.Parent = sectionHolder
				newKeybind.BackgroundColor3 = Color3.new(1, 1, 1)
				newKeybind.BackgroundTransparency = 1
				newKeybind.Size = UDim2.new(1, 0, 0, 19)
				keybindHeadline.Name = "keybindHeadline"
				keybindHeadline.Parent = newKeybind
				keybindHeadline.BackgroundColor3 = Color3.new(1, 1, 1)
				keybindHeadline.BackgroundTransparency = 1
				keybindHeadline.Position = UDim2.fromScale(0.031, 0.165842161)
				keybindHeadline.Size = UDim2.fromOffset(215, 12)
				keybindHeadline.Font = Enum.Font.Code
				keybindHeadline.Text = (keybindName and tostring(keybindName)) or "???"
				keybindHeadline.TextColor3 = library.colors.elementText
				colored[1 + #colored] = {keybindHeadline, "TextColor3", "elementText"}
				keybindHeadline.TextSize = 14
				keybindHeadline.TextXAlignment = Enum.TextXAlignment.Left
				keybindPositioner.Name = "keybindPositioner"
				keybindPositioner.Parent = newKeybind
				keybindPositioner.BackgroundColor3 = Color3.new(1, 1, 1)
				keybindPositioner.BackgroundTransparency = 1
				keybindPositioner.Position = UDim2.new(0.00448430516)
				keybindPositioner.Size = UDim2.fromOffset(214, 19)
				keybindList.Name = "keybindList"
				keybindList.Parent = keybindPositioner
				keybindList.FillDirection = Enum.FillDirection.Horizontal
				keybindList.HorizontalAlignment = Enum.HorizontalAlignment.Right
				keybindList.SortOrder = Enum.SortOrder.LayoutOrder
				keybindList.VerticalAlignment = Enum.VerticalAlignment.Center
				keybindButton.Name = "keybindButton"
				keybindButton.Parent = keybindPositioner
				keybindButton.Active = false
				keybindButton.BackgroundColor3 = Color3.new(1, 1, 1)
				keybindButton.BackgroundTransparency = 1
				keybindButton.Position = UDim2.fromScale(0.598130822, 0.184210524)
				keybindButton.Selectable = false
				keybindButton.Size = UDim2.fromOffset(46, 12)
				keybindButton.Font = Enum.Font.Code
				keybindButton.Text = (presetKeybind and tostring(presetKeybind):gsub("Enum.KeyCode.", "") or "[NONE]")
				keybindButton.TextColor3 = library.colors.otherElementText
				local colored_keybindButton_TextColor3 = {keybindButton, "TextColor3", "otherElementText"}
				colored[1 + #colored] = colored_keybindButton_TextColor3
				keybindButton.TextSize = 14
				keybindButton.TextXAlignment = Enum.TextXAlignment.Right
				keybindButton.Size = UDim2.fromOffset(textToSize(keybindButton).X + 4, 12)
				sectionFunctions:Update()
				local last_v = bindedKey or presetKeybind
				local function newkey()
					local old_texts = keybindButton.Text
					colored_keybindButton_TextColor3[3] = "main"
					colored_keybindButton_TextColor3[4] = nil
					tweenService:Create(keybindButton, TweenInfo.new(0.35, library.configuration.easingStyle, library.configuration.easingDirection), {
						TextColor3 = library.colors.main
					}):Play()
					if last_v then
						keybindButton.Text = "(Was " .. (last_v and tostring(last_v):gsub("Enum.KeyCode.", "") or "[NONE]") .. ") [...]"
					else
						keybindButton.Text = "[...]"
					end
					local receivingKey = nil
					receivingKey = userInputService.InputBegan:Connect(function(key)
						last_v = library_flags[flag]
						if not keyHandler.notAllowedKeys[key.KeyCode] then
							if key.KeyCode ~= Enum.KeyCode.Unknown then
								bindedKey = (key.KeyCode ~= Enum.KeyCode.Escape and key.KeyCode) or library_flags[flag]
								library_flags[flag] = bindedKey
								if options.Location then
									options.Location[options.LocationFlag or flag] = bindedKey
								end
								if bindedKey then
									keyName = keyHandler.allowedKeys[bindedKey]
									keybindButton.Text = "[" .. (keyName or bindedKey.Name or tostring(key.KeyCode):gsub("Enum.KeyCode.", "")) .. "]"
									keybindButton.Size = UDim2.fromOffset(textToSize(keybindButton).X + 4, 12)
									justBinded = true
									colored_keybindButton_TextColor3[3] = "otherElementText"
									colored_keybindButton_TextColor3[4] = nil
									tweenService:Create(keybindButton, TweenInfo.new(0.35, library.configuration.easingStyle, library.configuration.easingDirection), {
										TextColor3 = library.colors.otherElementText
									}):Play()
									receivingKey:Disconnect()
								end
								if callback and last_v ~= bindedKey then
									task.spawn(callback, bindedKey, last_v)
								end
								return
							elseif key.KeyCode == Enum.KeyCode.Unknown and not keyHandler.notAllowedMouseInputs[key.UserInputType] then
								bindedKey = key.UserInputType
								library_flags[flag] = bindedKey
								if options.Location then
									options.Location[options.LocationFlag or flag] = bindedKey
								end
								keyName = keyHandler.allowedKeys[bindedKey]
								keybindButton.Text = "[" .. (keyName or bindedKey.Name or tostring(key.KeyCode):gsub("Enum.KeyCode.", "")) .. "]"
								keybindButton.Size = UDim2.fromOffset(textToSize(keybindButton).X + 4, 12)
								justBinded = true
								colored_keybindButton_TextColor3[3] = "otherElementText"
								colored_keybindButton_TextColor3[4] = nil
								tweenService:Create(keybindButton, TweenInfo.new(0.35, library.configuration.easingStyle, library.configuration.easingDirection), {
									TextColor3 = library.colors.otherElementText
								}):Play()
								receivingKey:Disconnect()
								if callback and last_v ~= bindedKey then
									task.spawn(callback, bindedKey, last_v)
								end
								return
							end
						end
						if key.KeyCode == Enum.KeyCode.Backspace or Enum.KeyCode.Escape == key.KeyCode then
							old_texts, bindedKey = "[NONE]", nil
						end
						keybindButton.Text = old_texts
						colored_keybindButton_TextColor3[3] = "otherElementText"
						colored_keybindButton_TextColor3[4] = nil
						tweenService:Create(keybindButton, TweenInfo.new(0.35, library.configuration.easingStyle, library.configuration.easingDirection), {
							TextColor3 = library.colors.otherElementText
						}):Play()
						receivingKey:Disconnect()
						if callback and last_v ~= bindedKey then
							task.spawn(callback, bindedKey, last_v)
						end
					end)
					library.signals[1 + #library.signals] = receivingKey
				end
				library.signals[1 + #library.signals] = keybindButton.MouseButton1Click:Connect(newkey)
				library.signals[1 + #library.signals] = newKeybind.InputEnded:Connect(function(input)
					if not library.colorpicker and not submenuOpen and input.UserInputType == Enum.UserInputType.MouseButton1 then
						newkey()
					end
				end)
				if presscallback then
					library.signals[1 + #library.signals] = userInputService.InputBegan:Connect(function(key, chatting)
						if not keyHandler.notAllowedKeys[key.KeyCode] and not keyHandler.notAllowedMouseInputs[key.UserInputType] then
							if not justBinded and bindedKey == key.UserInputType or not justBinded and bindedKey == key.KeyCode and not chatting then
								if presscallback then
									task.spawn(presscallback, key, chatting)
								end
							end
							if justBinded then
								justBinded = false
							end
						end
					end)
				end
				local function set(t, key)
					if nil == key and t ~= nil then
						key = t
					end
					if key == "nil" or key == "NONE" or key == "none" then
						key = nil
					end
					last_v = library_flags[flag]
					bindedKey = key
					library_flags[flag] = key
					if options.Location then
						options.Location[options.LocationFlag or flag] = key
					end
					keyName = (key == nil and "NONE") or keyHandler.allowedKeys[key]
					keybindButton.Text = "[" .. (keyName or key.Name or tostring(key):gsub("Enum.KeyCode.", "")) .. "]"
					keybindButton.Size = UDim2.fromOffset(textToSize(keybindButton).X + 4, 12)
					justBinded = true
					colored_keybindButton_TextColor3[3] = "otherElementText"
					colored_keybindButton_TextColor3[4] = nil
					tweenService:Create(keybindButton, TweenInfo.new(0.35, library.configuration.easingStyle, library.configuration.easingDirection), {
						TextColor3 = library.colors.otherElementText
					}):Play()
					if callback and (last_v ~= key or options.AllowDuplicateCalls) then
						task.spawn(callback, key, last_v)
					end
					return key
				end
				if presetKeybind ~= nil then
					set(presetKeybind)
				else
					library_flags[flag] = bindedKey
					if options.Location then
						options.Location[options.LocationFlag or flag] = bindedKey
					end
				end
				local default = library_flags[flag]
				local function update()
					keybindName, callback, presscallback = options.Name or keybindName, options.Callback, options.Pressed
					local key = library_flags[flag]
					keyName = (key == nil and "NONE") or keyHandler.allowedKeys[key]
					keybindButton.Text = "[" .. (keyName or key.Name or tostring(key):gsub("Enum.KeyCode.", "")) .. "]"
					keybindButton.Size = UDim2.fromOffset(textToSize(keybindButton).X + 4, 12)
					colored_keybindButton_TextColor3[3] = "otherElementText"
					colored_keybindButton_TextColor3[4] = nil
					tweenService:Create(keybindButton, TweenInfo.new(0.35, library.configuration.easingStyle, library.configuration.easingDirection), {
						TextColor3 = library.colors.otherElementText
					}):Play()
					keybindHeadline.Text = (keybindName and tostring(keybindName)) or "???"
					return key
				end
				local objectdata = {
					Options = options,
					Name = flag,
					Flag = flag,
					Type = "Keybind",
					Default = default,
					Parent = sectionFunctions,
					Instance = keybindButton,
					Get = function()
						return library_flags[flag]
					end,
					Set = set,
					RawSet = function(t, key)
						if nil == key and t ~= nil then
							key = t
						end
						if key == "nil" or key == "NONE" or key == "none" then
							key = nil
						end
						last_v = library_flags[flag]
						bindedKey = key
						library_flags[flag] = key
						if options.Location then
							options.Location[options.LocationFlag or flag] = key
						end
						justBinded = true
						return key
					end,
					Update = update,
					Reset = function()
						return set(nil, default)
					end
				}
				tabFunctions.Flags[flag], sectionFunctions.Flags[flag], elements[flag] = objectdata, objectdata, objectdata
				return objectdata
			end
			sectionFunctions.NewKeybind = sectionFunctions.AddKeybind
			sectionFunctions.CreateKeybind = sectionFunctions.AddKeybind
			sectionFunctions.Keybind = sectionFunctions.AddKeybind
			sectionFunctions.Bind = sectionFunctions.AddKeybind
			function sectionFunctions:AddLabel(options, ...)
				options = (options and type(options) == "string" and resolvevararg("Label", options, ...)) or options
				local labelName, flag = options.Text or options.Value or options.Name, options.Flag or (function()
					library.unnamedlabels = 1 + (library.unnamedlabels or 0)
					return "Label" .. tostring(library.unnamedlabels)
				end)()
				if elements[flag] ~= nil then
					warn(debug.traceback("Warning! Re-used flag '" .. flag .. "'", 3))
				end
				local newLabel = Instance_new("Frame")
				local labelHeadline = Instance_new("TextLabel")
				local labelPositioner = Instance_new("Frame")
				local labelButton = Instance_new("TextButton")
				newLabel.Name = "newLabel"
				newLabel.Parent = sectionHolder
				newLabel.BackgroundColor3 = Color3.new(1, 1, 1)
				newLabel.BackgroundTransparency = 1
				newLabel.Size = UDim2.new(1, 0, 0, 19)
				labelHeadline.Name = "labelHeadline"
				labelHeadline.Parent = newLabel
				labelHeadline.BackgroundColor3 = Color3.new(1, 1, 1)
				labelHeadline.BackgroundTransparency = 1
				labelHeadline.Position = UDim2.fromScale(0.031, 0.165842161)
				labelHeadline.Size = UDim2.fromOffset(215, 12)
				labelHeadline.Font = Enum.Font.Code
				labelHeadline.Text = (labelName and tostring(labelName)) or "Empty Text"
				labelHeadline.TextColor3 = library.colors.elementText
				colored[1 + #colored] = {labelHeadline, "TextColor3", "elementText"}
				labelHeadline.TextSize = 14
				labelHeadline.TextXAlignment = Enum.TextXAlignment.Left
				labelPositioner.Name = "labelPositioner"
				labelPositioner.Parent = newLabel
				labelPositioner.BackgroundColor3 = Color3.new(1, 1, 1)
				labelPositioner.BackgroundTransparency = 1
				labelPositioner.Position = UDim2.new(0.00448430516)
				labelPositioner.Size = UDim2.fromOffset(214, 19)
				sectionFunctions:Update()
				local function set(t, str)
					if nil == str and t ~= nil then
						str = t
					end
					labelHeadline.Text = (nil ~= str and tostring(str)) or "Empty Text"
					return str
				end
				local default = labelHeadline.Text
				local objectdata = {
					Options = options,
					Name = flag,
					Flag = flag,
					Type = "Label",
					Default = default,
					Parent = sectionFunctions,
					Instance = labelHeadline,
					Get = function()
						return labelHeadline.Text, labelHeadline
					end,
					Set = set,
					RawSet = set,
					Update = function()
						return labelHeadline.Text
					end,
					Reset = function()
						return set(nil, default)
					end
				}
				tabFunctions.Flags[flag], sectionFunctions.Flags[flag], elements[flag] = objectdata, objectdata, objectdata
				return objectdata
			end
			sectionFunctions.NewLabel = sectionFunctions.AddLabel
			sectionFunctions.CreateLabel = sectionFunctions.AddLabel
			sectionFunctions.Label = sectionFunctions.AddLabel
			sectionFunctions.Text = sectionFunctions.AddLabel
			function sectionFunctions:AddSlider(options, ...)
				options = (options and type(options) == "string" and resolvevararg("Slider", options, ...)) or options
				local sliderName, maxValue, minValue, presetValue, callback, flagName = assert(options.Name, "Missing Name for new slider."), assert(options.Max, "Missing Max for new slider."), assert(options.Min, "Missing Min for new slider."), options.Value, options.Callback, options.Flag or (function()
					library.unnamedsliders = 1 + (library.unnamedsliders or 0)
					return "Slider" .. tostring(library.unnamedsliders)
				end)()
				if elements[flagName] ~= nil then
					warn(debug.traceback("Warning! Re-used flag '" .. flagName .. "'", 3))
				end
				local decimalprecision = tonumber(options.Decimals or options.Precision or options.Precise)
				if not decimalprecision and options.Max - options.Min <= 1 then
					decimalprecision = 1
				end
				if decimalprecision then
					decimalprecision = math.clamp(decimalprecision, 0, 99)
					if decimalprecision <= 0 then
						decimalprecision = nil
					end
					decimalprecision = tostring(decimalprecision)
				end
				local formattyp = options.Format and type(options.Format)
				local function resolvedisplay(val, was)
					local str = nil
					if decimalprecision then
						str = string.format("%0." .. decimalprecision .. "f", val)
					end
					str = str or tostring(val)
					if formattyp == "string" then
						return string.format(options.Format, val)
					elseif formattyp == "function" then
						local oof, g = pcall(options.Format, val, was)
						if not oof or not g then
							warn("Your format function for", sliderName, "Slider:", flagName, "has returned nothing. It should return a string to display.", debug.traceback(""))
							return "Format Function Errored"
						end
						return tostring(g)
					end
					return (sliderName or "???") .. ": " .. str
				end
				local usetextbox = options.Textbox or options.InputBox or options.CustomInput
				local newSlider = Instance_new("Frame")
				local slider = Instance_new("ImageLabel")
				local sliderInner = Instance_new("ImageLabel")
				local sliderColored = Instance_new("ImageLabel")
				local sliderHeadline = Instance_new("TextLabel")
				local startingValue = presetValue or minValue
				local sliderDragging = false
				newSlider.Name = "newSlider"
				newSlider.Parent = sectionHolder
				newSlider.BackgroundColor3 = Color3.new(1, 1, 1)
				newSlider.BackgroundTransparency = 1
				newSlider.Size = UDim2.new(1, 0, 0, 42)
				slider.Name = "slider"
				slider.Parent = newSlider
				slider.Active = true
				slider.BackgroundColor3 = library.colors.topGradient
				local colored_slider_BackgroundColor3 = {slider, "BackgroundColor3", "topGradient"}
				colored[1 + #colored] = colored_slider_BackgroundColor3
				slider.BorderColor3 = library.colors.elementBorder
				colored[1 + #colored] = {slider, "BorderColor3", "elementBorder"}
				slider.Position = UDim2.fromScale(0.031, 0.48)
				slider.Selectable = true
				slider.Size = (usetextbox and UDim2.fromOffset(156, 18)) or UDim2.fromOffset(206, 18)
				slider.Image = "rbxassetid://2454009026"
				slider.ImageColor3 = library.colors.bottomGradient
				local colored_slider_ImageColor3 = {slider, "ImageColor3", "bottomGradient"}
				colored[1 + #colored] = colored_slider_ImageColor3
				sliderInner.Name = "sliderInner"
				sliderInner.Parent = slider
				sliderInner.Active = true
				sliderInner.AnchorPoint = Vector2.new(0.5, 0.5)
				sliderInner.BackgroundColor3 = library.colors.topGradient
				colored[1 + #colored] = {sliderInner, "BackgroundColor3", "topGradient"}
				sliderInner.BorderColor3 = library.colors.elementBorder
				colored[1 + #colored] = {sliderInner, "BorderColor3", "elementBorder"}
				sliderInner.Position = UDim2.fromScale(0.5, 0.5)
				sliderInner.Selectable = true
				sliderInner.Size = UDim2.new(1, -4, 1, -4)
				sliderInner.Image = "rbxassetid://2454009026"
				sliderInner.ImageColor3 = library.colors.bottomGradient
				colored[1 + #colored] = {sliderInner, "ImageColor3", "bottomGradient"}
				sliderColored.Name = "sliderColored"
				sliderColored.Parent = sliderInner
				sliderColored.Active = true
				sliderColored.BackgroundColor3 = darkenColor(library.colors.main, 1.5)
				colored[1 + #colored] = {sliderColored, "BackgroundColor3", "main", 1.5}
				sliderColored.BorderSizePixel = 0
				sliderColored.Selectable = true
				sliderColored.Size = UDim2.fromScale(((startingValue or minValue) - minValue) / (maxValue - minValue), 1)
				sliderColored.Image = "rbxassetid://2454009026"
				sliderColored.ImageColor3 = darkenColor(library.colors.main, 2.5)
				colored[1 + #colored] = {sliderColored, "ImageColor3", "main", 2.5}
				sliderHeadline.Name = "sliderHeadline"
				sliderHeadline.Parent = newSlider
				sliderHeadline.Active = true
				sliderHeadline.BackgroundColor3 = Color3.new(1, 1, 1)
				sliderHeadline.BackgroundTransparency = 1
				sliderHeadline.Position = UDim2.new(0.031)
				sliderHeadline.Selectable = true
				sliderHeadline.Size = UDim2.fromOffset(206, 20)
				sliderHeadline.ZIndex = 5
				sliderHeadline.Font = Enum.Font.Code
				sliderHeadline.LineHeight = 1.15
				sliderHeadline.Text = resolvedisplay(startingValue)
				sliderHeadline.TextColor3 = library.colors.elementText
				colored[1 + #colored] = {sliderHeadline, "TextColor3", "elementText"}
				sliderHeadline.TextSize = 14
				sliderHeadline.TextXAlignment = Enum.TextXAlignment.Left
				local realTextbox = nil
				local function Set(t, newValue)
					if nil == newValue and t ~= nil then
						newValue = t
					end
					minValue, maxValue = options.Min, options.Max
					if newValue and (options.IllegalInput or ((not minValue or newValue >= minValue) and (not maxValue or newValue <= maxValue))) then
						local last_val = library_flags[flagName]
						library_flags[flagName] = newValue
						if options.Location then
							options.Location[options.LocationFlag or flagName] = newValue
						end
						do
							local newValue = (options.IllegalInput and math.clamp(newValue, minValue or -math.huge, maxValue or math.huge)) or newValue
							tweenService:Create(sliderColored, TweenInfo.new(0.25, library.configuration.easingStyle, library.configuration.easingDirection), {
								Size = UDim2.fromScale(((newValue or minValue) - minValue) / (maxValue - minValue), 1)
							}):Play()
						end
						sliderHeadline.Text = resolvedisplay(newValue, last_val)
						if usetextbox and realTextbox then
							realTextbox.Text = tostring(newValue)
						end
						if callback and (last_val ~= newValue or options.AllowDuplicateCalls) then
							task.spawn(callback, newValue, last_val)
						end
					end
					return newValue
				end
				if presetValue ~= nil then
					Set(presetValue)
				else
					library_flags[flagName] = startingValue
					if options.Location then
						options.Location[options.LocationFlag or flagName] = startingValue
					end
				end
				if usetextbox then
					if type(usetextbox) ~= "table" then
						usetextbox = options
					end
					local textbox = Instance_new("ImageLabel")
					local textboxInner = Instance_new("ImageLabel")
					realTextbox = Instance_new("TextBox")
					textbox.Name = "textbox"
					textbox.Parent = newSlider
					textbox.Active = true
					textbox.BackgroundColor3 = library.colors.topGradient
					local colored_textbox_BackgroundColor3 = {textbox, "BackgroundColor3", "topGradient"}
					colored[1 + #colored] = colored_textbox_BackgroundColor3
					textbox.BorderColor3 = library.colors.elementBorder
					colored[1 + #colored] = {textbox, "BorderColor3", "elementBorder"}
					textbox.Position = UDim2.new(1, -54, 0.48)
					textbox.Selectable = true
					textbox.Size = UDim2.fromOffset(43, 18)
					textbox.Image = "rbxassetid://2454009026"
					textbox.ImageColor3 = library.colors.bottomGradient
					local colored_textbox_ImageColor3 = {textbox, "ImageColor3", "bottomGradient"}
					colored[1 + #colored] = colored_textbox_ImageColor3
					textboxInner.Name = "textboxInner"
					textboxInner.Parent = textbox
					textboxInner.Active = true
					textboxInner.AnchorPoint = Vector2.new(0.5, 0.5)
					textboxInner.BackgroundColor3 = library.colors.topGradient
					colored[1 + #colored] = {textboxInner, "BackgroundColor3", "topGradient"}
					textboxInner.BorderColor3 = library.colors.elementBorder
					colored[1 + #colored] = {textboxInner, "BorderColor3", "elementBorder"}
					textboxInner.Position = UDim2.fromScale(0.5, 0.5)
					textboxInner.Selectable = true
					textboxInner.Size = UDim2.new(1, -4, 1, -4)
					textboxInner.Image = "rbxassetid://2454009026"
					textboxInner.ImageColor3 = library.colors.bottomGradient
					colored[1 + #colored] = {textboxInner, "ImageColor3", "bottomGradient"}
					realTextbox.Name = "realTextbox"
					realTextbox.Parent = textbox
					realTextbox.BackgroundColor3 = Color3.new(1, 1, 1)
					realTextbox.BackgroundTransparency = 1
					realTextbox.Position = UDim2.new(0.0295485705)
					realTextbox.Size = UDim2.fromScale(0.97, 1)
					realTextbox.ZIndex = 5
					realTextbox.ClearTextOnFocus = false
					realTextbox.Font = Enum.Font.Code
					realTextbox.LineHeight = 1.15
					realTextbox.Text = tostring(presetValue)
					realTextbox.TextColor3 = library.colors.otherElementText
					colored[1 + #colored] = {realTextbox, "TextColor3", "otherElementText"}
					realTextbox.TextSize = 14
					realTextbox.PlaceholderText = (presetValue ~= nil and tostring(presetValue)) or ""
					library.signals[1 + #library.signals] = realTextbox.FocusLost:Connect(function()
						local val = realTextbox.Text
						if usetextbox.PreFormat then
							local typ = type(usetextbox.PreFormat)
							if typ == "function" then
								local x, e = pcall(usetextbox.PreFormat, val)
								if not x and e then
									warn("Error in Pre-Format (Textbox " .. flagName .. "):", e)
								else
									val = e
								end
							end
						end
						val = (not usetextbox.Hex and not usetextbox.Binary and not usetextbox.Base and (tonumber(val) or tonumber(val:gsub("%D", ""), 10) or 0)) or tonumber(val, (usetextbox.Hex and 16) or (usetextbox.Binary and 2) or usetextbox.Base or 10) or 0
						if not options.IllegalInput and (options.Max or options.Min) then
							val = math.clamp(val, options.Min or -math.huge, options.Max or math.huge)
						end
						local decimalprecision = tonumber(options.Decimals or options.Precision or options.Precise)
						if decimalprecision then
							val = tonumber(string.format("%0." .. tostring(decimalprecision) .. "f", val))
						end
						if usetextbox.PostFormat then
							local typ = type(usetextbox.PostFormat)
							if typ == "function" then
								local x, e = pcall(usetextbox.PostFormat, val)
								if not x and e then
									warn("Error in Post-Format (Textbox " .. flagName .. "):", e)
								else
									val = e
								end
							end
						end
						Set((val and tonumber(val)) or presetValue or 0)
					end)
					library.signals[1 + #library.signals] = textbox.MouseEnter:Connect(function()
						colored_textbox_BackgroundColor3[3] = "main"
						colored_textbox_BackgroundColor3[4] = 1.5
						colored_textbox_ImageColor3[3] = "main"
						colored_textbox_ImageColor3[4] = 2.5
						tweenService:Create(textbox, TweenInfo.new(0.35, library.configuration.easingStyle, library.configuration.easingDirection), {
							BackgroundColor3 = darkenColor(library.colors.main, 1.5),
							ImageColor3 = darkenColor(library.colors.main, 2.5)
						}):Play()
					end)
					library.signals[1 + #library.signals] = textbox.MouseLeave:Connect(function()
						colored_textbox_BackgroundColor3[3] = "topGradient"
						colored_textbox_BackgroundColor3[4] = nil
						colored_textbox_ImageColor3[3] = "bottomGradient"
						colored_textbox_ImageColor3[4] = nil
						tweenService:Create(textbox, TweenInfo.new(0.35, library.configuration.easingStyle, library.configuration.easingDirection), {
							BackgroundColor3 = library.colors.topGradient,
							ImageColor3 = library.colors.bottomGradient
						}):Play()
					end)
				end
				sectionFunctions:Update()
				library.signals[1 + #library.signals] = slider.MouseEnter:Connect(function()
					colored_slider_BackgroundColor3[3] = "main"
					colored_slider_BackgroundColor3[4] = 1.5
					colored_slider_ImageColor3[3] = "main"
					colored_slider_ImageColor3[4] = 2.5
					tweenService:Create(slider, TweenInfo.new(0.35, library.configuration.easingStyle, library.configuration.easingDirection), {
						BackgroundColor3 = darkenColor(library.colors.main, 1.5),
						ImageColor3 = darkenColor(library.colors.main, 2.5)
					}):Play()
				end)
				library.signals[1 + #library.signals] = slider.MouseLeave:Connect(function()
					colored_slider_BackgroundColor3[3] = "topGradient"
					colored_slider_BackgroundColor3[4] = nil
					colored_slider_ImageColor3[3] = "bottomGradient"
					colored_slider_ImageColor3[4] = nil
					tweenService:Create(slider, TweenInfo.new(0.35, library.configuration.easingStyle, library.configuration.easingDirection), {
						BackgroundColor3 = library.colors.topGradient,
						ImageColor3 = library.colors.bottomGradient
					}):Play()
				end)
				local function sliding(input, sb, sc)
					local last_val = library_flags[flagName]
					local pos = UDim2.fromScale(math.clamp((input.Position.X - sb.AbsolutePosition.X) / sb.AbsoluteSize.X, 0, 1), 1)
					tweenService:Create(sc, TweenInfo.new(0.25, library.configuration.easingStyle, library.configuration.easingDirection), {
						Size = pos
					}):Play()
					local sliderValue = nil
					if decimalprecision then
						sliderValue = tonumber(string.format("%0." .. decimalprecision .. "f", ((pos.X.Scale * maxValue) / maxValue) * (maxValue - minValue) + minValue))
					end
					sliderValue = sliderValue or tonumber(string.format("%0.2f", (floor(((pos.X.Scale * maxValue) / maxValue) * (maxValue - minValue) + minValue))))
					library_flags[flagName] = sliderValue
					if options.Location then
						options.Location[options.LocationFlag or flagName] = sliderValue
					end
					sliderHeadline.Text = resolvedisplay(sliderValue, last_val)
					if usetextbox and realTextbox then
						realTextbox.Text = tostring(sliderValue)
					end
					if callback and last_val ~= sliderValue then
						task.spawn(callback, sliderValue, last_val)
					end
					last_val = sliderValue
				end
				library.signals[1 + #library.signals] = newSlider.InputBegan:Connect(function(input)
					if not library.colorpicker and input.UserInputType == Enum.UserInputType.MouseButton1 then
						sliderDragging = true
						isDraggingSomething = true
					end
				end)
				library.signals[1 + #library.signals] = newSlider.InputEnded:Connect(function(input)
					if not library.colorpicker and input.UserInputType == Enum.UserInputType.MouseButton1 then
						sliderDragging = false
						isDraggingSomething = false
					end
				end)
				library.signals[1 + #library.signals] = newSlider.InputBegan:Connect(function(input)
					if not library.colorpicker and not isDraggingSomething and input.UserInputType == Enum.UserInputType.MouseButton1 then
						isDraggingSomething = true
						sliding(input, sliderInner, sliderColored)
					end
				end)
				library.signals[1 + #library.signals] = userInputService.InputChanged:Connect(function(input)
					if not library.colorpicker and sliderDragging and input.UserInputType == Enum.UserInputType.MouseMovement then
						sliding(input, sliderInner, sliderColored)
					end
				end)
				local default = library_flags[flagName]
				local function Update(t, last_val)
					if last_val == nil and t ~= nil and type(t) ~= "table" then
						last_val = t
					end
					sliderName, maxValue, minValue, callback = options.Name or sliderName, options.Max or maxValue, options.Min or minValue, options.Callback
					local newValue = library_flags[flagName]
					do
						local newValue = math.clamp(newValue, options.Min or -math.huge, options.Max or math.huge)
						tweenService:Create(sliderColored, TweenInfo.new(0.25, library.configuration.easingStyle, library.configuration.easingDirection), {
							Size = UDim2.fromScale(((newValue or minValue) - minValue) / (maxValue - minValue), 1)
						}):Play()
					end
					sliderHeadline.Text = resolvedisplay(newValue, last_val)
					if usetextbox and realTextbox then
						realTextbox.Text = tostring(newValue)
					end
					return newValue
				end
				local objectdata = {
					Options = options,
					Name = flagName,
					Flag = flagName,
					Type = "Slider",
					Default = default,
					Parent = sectionFunctions,
					Instance = sliderHeadline,
					Set = Set,
					Get = function()
						return library_flags[flagName]
					end,
					SetConstraints = function(t, min, max)
						if t and type(t) ~= "table" then
							min, max = t, min
						end
						if min then
							options.Min = min
						end
						if max then
							options.Max = max
						end
						Update()
					end,
					SetMin = function(t, min)
						if min == nil and t ~= nil then
							min = t
						end
						if min and min ~= options.Min then
							options.Min = min
							Update()
						end
					end,
					SetMax = function(t, max)
						if max == nil and t ~= nil then
							max = t
						end
						if max and max ~= options.Max then
							options.Max = max
							Update()
						end
					end,
					Update = Update,
					RawSet = function(t, newValue)
						if nil == newValue and t ~= nil then
							newValue = t
						end
						local last_val = library_flags[flagName]
						library_flags[flagName] = newValue
						if options.Location then
							options.Location[options.LocationFlag or flagName] = newValue
						end
						Update(nil, last_val)
					end,
					Reset = function()
						return Set(nil, default)
					end
				}
				tabFunctions.Flags[flagName], sectionFunctions.Flags[flagName], elements[flagName] = objectdata, objectdata, objectdata
				return objectdata
			end
			sectionFunctions.NewSlider = sectionFunctions.AddSlider
			sectionFunctions.CreateSlider = sectionFunctions.AddSlider
			sectionFunctions.NumberConstraint = sectionFunctions.AddSlider
			sectionFunctions.Slider = sectionFunctions.AddSlider
			sectionFunctions.Slide = sectionFunctions.AddSlider
			function sectionFunctions:AddSearchBox(options, ...)
				options = (options and type(options) == "string" and resolvevararg("SearchBox", options, ...)) or options
				local dropdownName, listt, val, callback, flagName = assert(options.Name, "Missing Name for new searchbox."), assert(options.List, "Missing List for new searchbox."), options.Value, options.Callback, options.Flag or (function()
					library.unnamedsearchbox = 1 + (library.unnamedsearchbox or 0)
					return "SearchBox" .. tostring(library.unnamedsearchbox)
				end)()
				if elements[flagName] ~= nil then
					warn(debug.traceback("Warning! Re-used flag '" .. flagName .. "'", 3))
				end
				local newDropdown = Instance_new("Frame")
				local dropdown = Instance_new("ImageLabel")
				local dropdownInner = Instance_new("ImageLabel")
				local dropdownToggle = Instance_new("ImageButton")
				local dropdownSelection = Instance_new("TextBox")
				local dropdownHeadline = Instance_new("TextLabel")
				local dropdownHolderFrame = Instance_new("ImageLabel")
				local dropdownHolderInner = Instance_new("ImageLabel")
				local realDropdownHolder = Instance_new("ScrollingFrame")
				local realDropdownHolderList = Instance_new("UIListLayout")
				local dropdownEnabled = false
				local resolvelist = getresolver(listt, options.Filter)
				local list = resolvelist()
				local multiselect = options.MultiSelect or options.Multi or options.Multiple
				local passed_multiselect = multiselect and type(multiselect)
				local blankstring = not multiselect and (options.BlankValue or options.NoValueString or options.Nothing)
				local selectedOption = val or list[1] or blankstring
				local addcallback = options.ItemAdded or options.AddedCallback
				local delcallback = options.ItemRemoved or options.RemovedCallback
				local clrcallback = options.ItemsCleared or options.ClearedCallback
				local modcallback = options.ItemChanged or options.ChangedCallback
				if blankstring and val == nil then
					val = blankstring
				end
				if val ~= nil then
					selectedOption = val
				end
				if multiselect and (not selectedOption or type(selectedOption) ~= "table") then
					selectedOption = {}
				end
				local selectedObjects = {}
				local optionCount = 0
				newDropdown.Name = "newDropdown"
				newDropdown.Parent = sectionHolder
				newDropdown.BackgroundColor3 = Color3.new(1, 1, 1)
				newDropdown.BackgroundTransparency = 1
				newDropdown.Size = UDim2.new(1, 0, 0, 42)
				dropdown.Name = "dropdown"
				dropdown.Parent = newDropdown
				dropdown.Active = true
				dropdown.BackgroundColor3 = library.colors.topGradient
				local colored_dropdown_BackgroundColor3 = {dropdown, "BackgroundColor3", "topGradient"}
				colored[1 + #colored] = colored_dropdown_BackgroundColor3
				dropdown.BorderColor3 = library.colors.elementBorder
				colored[1 + #colored] = {dropdown, "BorderColor3", "elementBorder"}
				dropdown.Position = UDim2.fromScale(0.027, 0.45)
				dropdown.Selectable = true
				dropdown.Size = UDim2.fromOffset(206, 18)
				dropdown.Image = "rbxassetid://2454009026"
				dropdown.ImageColor3 = library.colors.bottomGradient
				local colored_dropdown_ImageColor3 = {dropdown, "ImageColor3", "bottomGradient"}
				colored[1 + #colored] = colored_dropdown_ImageColor3
				dropdownInner.Name = "dropdownInner"
				dropdownInner.Parent = dropdown
				dropdownInner.Active = true
				dropdownInner.AnchorPoint = Vector2.new(0.5, 0.5)
				dropdownInner.BackgroundColor3 = library.colors.topGradient
				colored[1 + #colored] = {dropdownInner, "BackgroundColor3", "topGradient"}
				dropdownInner.BorderColor3 = library.colors.elementBorder
				colored[1 + #colored] = {dropdownInner, "BorderColor3", "elementBorder"}
				dropdownInner.Position = UDim2.fromScale(0.5, 0.5)
				dropdownInner.Selectable = true
				dropdownInner.Size = UDim2.new(1, -4, 1, -4)
				dropdownInner.Image = "rbxassetid://2454009026"
				dropdownInner.ImageColor3 = library.colors.bottomGradient
				colored[1 + #colored] = {dropdownInner, "ImageColor3", "bottomGradient"}
				dropdownToggle.Name = "dropdownToggle"
				dropdownToggle.Parent = dropdown
				dropdownToggle.BackgroundColor3 = Color3.new(1, 1, 1)
				dropdownToggle.BackgroundTransparency = 1
				dropdownToggle.Position = UDim2.fromScale(0.9, 0.17)
				dropdownToggle.Rotation = 90
				dropdownToggle.Size = UDim2.fromOffset(12, 12)
				dropdownToggle.ZIndex = 6
				dropdownToggle.Image = "rbxassetid://71659683"
				dropdownToggle.ImageColor3 = Color3.fromRGB(171, 171, 171)
				dropdownSelection.Name = "dropdownSelection"
				dropdownSelection.Parent = dropdown
				dropdownSelection.BackgroundColor3 = Color3.new(1, 1, 1)
				dropdownSelection.BackgroundTransparency = 1
				dropdownSelection.Position = UDim2.new(0.0295485705)
				dropdownSelection.Size = UDim2.fromScale(0.85, 1)
				dropdownSelection.ZIndex = 5
				dropdownSelection.Font = Enum.Font.Code
				dropdownSelection.LineHeight = 1.15
				dropdownSelection.Text = (passed_multiselect == "string" and multiselect) or (multiselect and (blankstring or "Select Item(s)")) or (selectedOption and tostring(selectedOption)) or blankstring or "No Blank String"
				dropdownSelection.TextColor3 = library.colors.otherElementText
				colored[1 + #colored] = {dropdownSelection, "TextColor3", "otherElementText"}
				dropdownSelection.TextSize = 14
				dropdownSelection.TextXAlignment = Enum.TextXAlignment.Left
				dropdownSelection.ClearTextOnFocus = true
				dropdownHeadline.Name = "dropdownHeadline"
				dropdownHeadline.Parent = newDropdown
				dropdownHeadline.BackgroundColor3 = Color3.new(1, 1, 1)
				dropdownHeadline.BackgroundTransparency = 1
				dropdownHeadline.Position = UDim2.fromScale(0.034, 0.03)
				dropdownHeadline.Size = UDim2.fromOffset(167, 11)
				dropdownHeadline.Font = Enum.Font.Code
				dropdownHeadline.Text = (dropdownName and tostring(dropdownName)) or "???"
				dropdownHeadline.TextColor3 = library.colors.elementText
				colored[1 + #colored] = {dropdownHeadline, "TextColor3", "elementText"}
				dropdownHeadline.TextSize = 14
				dropdownHeadline.TextXAlignment = Enum.TextXAlignment.Left
				dropdownHolderFrame.Name = "dropdownHolderFrame"
				dropdownHolderFrame.Parent = newDropdown
				dropdownHolderFrame.Active = true
				dropdownHolderFrame.BackgroundColor3 = library.colors.topGradient
				colored[1 + #colored] = {dropdownHolderFrame, "BackgroundColor3", "topGradient"}
				dropdownHolderFrame.BorderColor3 = library.colors.elementBorder
				colored[1 + #colored] = {dropdownHolderFrame, "BorderColor3", "elementBorder"}
				dropdownHolderFrame.Position = UDim2.fromScale(0.025, 1.012)
				dropdownHolderFrame.Selectable = true
				dropdownHolderFrame.Size = UDim2.fromOffset(206, 22)
				dropdownHolderFrame.Visible = false
				dropdownHolderFrame.Image = "rbxassetid://2454009026"
				dropdownHolderFrame.ImageColor3 = library.colors.bottomGradient
				colored[1 + #colored] = {dropdownHolderFrame, "ImageColor3", "bottomGradient"}
				dropdownHolderInner.Name = "dropdownHolderInner"
				dropdownHolderInner.Parent = dropdownHolderFrame
				dropdownHolderInner.Active = true
				dropdownHolderInner.AnchorPoint = Vector2.new(0.5, 0.5)
				dropdownHolderInner.BackgroundColor3 = library.colors.topGradient
				colored[1 + #colored] = {dropdownHolderInner, "BackgroundColor3", "topGradient"}
				dropdownHolderInner.BorderColor3 = library.colors.elementBorder
				dropdownHolderInner.Position = UDim2.fromScale(0.5, 0.5)
				dropdownHolderInner.Selectable = true
				dropdownHolderInner.Size = UDim2.new(1, -4, 1, -4)
				dropdownHolderInner.Image = "rbxassetid://2454009026"
				dropdownHolderInner.ImageColor3 = library.colors.bottomGradient
				colored[1 + #colored] = {dropdownHolderInner, "ImageColor3", "bottomGradient"}
				realDropdownHolder.Name = "realDropdownHolder"
				realDropdownHolder.Parent = dropdownHolderInner
				realDropdownHolder.BackgroundColor3 = Color3.new(1, 1, 1)
				realDropdownHolder.BackgroundTransparency = 1
				realDropdownHolder.Selectable = false
				realDropdownHolder.Size = UDim2.fromScale(1, 1)
				realDropdownHolder.CanvasSize = UDim2.new()
				realDropdownHolder.ScrollBarThickness = 5
				realDropdownHolder.ScrollingDirection = Enum.ScrollingDirection.Y
				realDropdownHolder.AutomaticCanvasSize = Enum.AutomaticSize.Y
				realDropdownHolder.ScrollBarImageTransparency = 0.5
				realDropdownHolder.ScrollBarImageColor3 = library.colors.section
				colored[1 + #colored] = {realDropdownHolder, "ScrollBarImageColor3", "section"}
				realDropdownHolderList.Name = "realDropdownHolderList"
				realDropdownHolderList.Parent = realDropdownHolder
				realDropdownHolderList.HorizontalAlignment = Enum.HorizontalAlignment.Center
				realDropdownHolderList.SortOrder = Enum.SortOrder.LayoutOrder
				sectionFunctions:Update()
				local restorezindex = {}
				library.signals[1 + #library.signals] = newDropdown.MouseEnter:Connect(function()
					colored_dropdown_BackgroundColor3[3] = "main"
					colored_dropdown_BackgroundColor3[4] = 1.5
					colored_dropdown_ImageColor3[3] = "main"
					colored_dropdown_ImageColor3[4] = 2.5
					tweenService:Create(dropdown, TweenInfo.new(0.25, library.configuration.easingStyle, library.configuration.easingDirection), {
						BackgroundColor3 = darkenColor(library.colors.main, 1.5),
						ImageColor3 = darkenColor(library.colors.main, 2.5)
					}):Play()
				end)
				library.signals[1 + #library.signals] = newDropdown.MouseLeave:Connect(function()
					if not dropdownEnabled then
						colored_dropdown_BackgroundColor3[3] = "topGradient"
						colored_dropdown_BackgroundColor3[4] = nil
						colored_dropdown_ImageColor3[3] = "bottomGradient"
						colored_dropdown_ImageColor3[4] = nil
						tweenService:Create(dropdown, TweenInfo.new(0.25, library.configuration.easingStyle, library.configuration.easingDirection), {
							BackgroundColor3 = library.colors.topGradient,
							ImageColor3 = library.colors.bottomGradient
						}):Play()
					end
				end)
				local function UpdateDropdownHolder()
					if optionCount >= 6 then
						realDropdownHolder.CanvasSize = UDim2:fromOffset(realDropdownHolderList.AbsoluteContentSize.Y + 2)
					elseif optionCount <= 5 then
						dropdownHolderFrame.Size = UDim2.fromOffset(206, realDropdownHolderList.AbsoluteContentSize.Y + 4)
					end
				end
				local function AddOptions(optionsTable, filter)
					if options.Sort then
						local didstuff, dosort = nil, options.Sort
						if type(dosort) == "function" then
							local g, h = pcall(table.sort, optionsTable, dosort)
							if g then
								didstuff = true
							elseif h then
								warn("Error sorting list:", h, debug.traceback(""))
							end
						end
						if not didstuff then
							table.sort(optionsTable, library.defaultSort)
						end
					end
					if blankstring and (optionsTable[1] ~= blankstring or table.find(optionsTable, blankstring, 2)) then
						local exists = table.find(optionsTable, blankstring)
						if exists then
							for _ = 1, 35 do
								table.remove(optionsTable, exists)
								exists = table.find(optionsTable, blankstring)
								if not exists then
									break
								end
							end
						end
						table.insert(optionsTable, 1, blankstring)
					end
					optionCount = 0
					realDropdownHolderList.Parent = nil
					realDropdownHolder:ClearAllChildren()
					realDropdownHolderList.Parent = realDropdownHolder
					for _, v in next, optionsTable do
						if not filter or tostring(v):lower():find(dropdownSelection.Text:lower(), 1, not options.RegEx) then
							optionCount = optionCount + 1
							UpdateDropdownHolder()
							local newOption = Instance_new("ImageLabel")
							local optionButton = Instance_new("TextButton")
							if selectedOption == v then
								selectedObjects[1] = newOption
								selectedObjects[2] = optionButton
							end
							newOption.Name = "Frame"
							newOption.Parent = realDropdownHolder
							local togged = (not multiselect and selectedOption == v) or (multiselect and table.find(selectedOption, v))
							newOption.BackgroundColor3 = (togged and library.colors.selectedOption) or library.colors.topGradient
							newOption.BorderSizePixel = 0
							newOption.Size = UDim2.fromOffset(202, 18)
							newOption.Image = "rbxassetid://2454009026"
							newOption.ImageColor3 = (togged and library.colors.unselectedOption) or library.colors.bottomGradient
							local stringed = tostring(v)
							optionButton.Name = stringed
							optionButton.Parent = newOption
							optionButton.Active = true
							optionButton.AnchorPoint = Vector2.new(0.5, 0.5)
							optionButton.BackgroundColor3 = Color3.new(1, 1, 1)
							optionButton.BackgroundTransparency = 1
							optionButton.Position = UDim2.fromScale(0.5, 0.5)
							optionButton.Selectable = true
							optionButton.Size = UDim2.new(1, -10, 1)
							optionButton.ZIndex = 5
							optionButton.Font = Enum.Font.Code
							optionButton.Text = (togged and (" " .. stringed)) or stringed
							optionButton.TextColor3 = (togged and library.colors.main) or library.colors.otherElementText
							optionButton.TextSize = 14
							optionButton.TextXAlignment = Enum.TextXAlignment.Left
							library.signals[1 + #library.signals] = optionButton[(multiselect and "MouseButton1Click") or "MouseButton1Down"]:Connect(function()
								if not library.colorpicker then
									dropdownSelection.Text = (passed_multiselect == "string" and multiselect) or blankstring or "Select Item(s)"
									restorezindex[newSection] = restorezindex[newSection] or newSection.ZIndex
									restorezindex[newDropdown] = restorezindex[newDropdown] or newDropdown.ZIndex
									restorezindex[sectionHolder] = restorezindex[sectionHolder] or sectionHolder.ZIndex
									if multiselect then
										local cloned = {unpack(selectedOption)}
										local togged = table.find(selectedOption, v)
										if togged then
											table.remove(selectedOption, togged)
										else
											selectedOption[1 + #selectedOption] = v
										end
										togged = table.find(selectedOption, v)
										optionButton.Text = (togged and (" " .. stringed)) or stringed
										newOption.BackgroundColor3 = (togged and library.colors.selectedOption) or library.colors.topGradient
										newOption.ImageColor3 = (togged and library.colors.unselectedOption) or library.colors.bottomGradient
										optionButton.TextColor3 = (togged and library.colors.main) or library.colors.otherElementText
										if callback then
											task.spawn(callback, selectedOption, cloned)
										end
										if togged then
											if addcallback then
												task.spawn(addcallback, v, selectedOption)
											end
										elseif delcallback then
											task.spawn(delcallback, v, selectedOption)
										end
										if modcallback then
											task.spawn(modcallback, v, togged, selectedOption)
										end
										if #selectedOption == 0 and clrcallback then
											task.spawn(clrcallback, selectedOption, cloned)
										end
										return
									else
										dropdownSelection.Text = stringed
										if selectedOption ~= v then
											local last_v = library_flags[flagName]
											selectedObjects[1].BackgroundColor3 = library.colors.topGradient
											selectedObjects[1].ImageColor3 = library.colors.bottomGradient
											selectedObjects[2].Text = selectedObjects[2].Name
											selectedObjects[2].TextColor3 = library.colors.otherElementText
											selectedOption = v
											selectedObjects[1] = newOption
											selectedObjects[2] = optionButton
											newOption.BackgroundColor3 = library.colors.selectedOption
											newOption.ImageColor3 = library.colors.unselectedOption
											optionButton.TextColor3 = library.colors.main
											dropdownHolderFrame.Visible = false
											dropdownToggle.Rotation = 90
											dropdownEnabled = false
											newDropdown.ZIndex = 1
											colored_dropdown_BackgroundColor3[3] = "topGradient"
											colored_dropdown_BackgroundColor3[4] = nil
											colored_dropdown_ImageColor3[3] = "bottomGradient"
											colored_dropdown_ImageColor3[4] = nil
											tweenService:Create(dropdown, TweenInfo.new(0.35, library.configuration.easingStyle, library.configuration.easingDirection), {
												BackgroundColor3 = library.colors.topGradient,
												ImageColor3 = library.colors.bottomGradient
											}):Play()
											library_flags[flagName] = selectedOption
											if options.Location then
												options.Location[options.LocationFlag or flagName] = selectedOption
											end
											dropdownSelection.Text = tostring(selectedOption)
											if submenuOpen then
												submenuOpen = nil
											end
											if callback then
												task.spawn(callback, selectedOption, last_v)
											end
										else
											submenuOpen = nil
											dropdownToggle.Rotation = 90
											colored_dropdown_BackgroundColor3[3] = "topGradient"
											colored_dropdown_BackgroundColor3[4] = nil
											colored_dropdown_ImageColor3[3] = "bottomGradient"
											colored_dropdown_ImageColor3[4] = nil
											tweenService:Create(dropdown, TweenInfo.new(0.35, library.configuration.easingStyle, library.configuration.easingDirection), {
												BackgroundColor3 = library.colors.topGradient,
												ImageColor3 = library.colors.bottomGradient
											}):Play()
											dropdownHolderFrame.Visible = false
										end
									end
									for ins, z in next, restorezindex do
										ins.ZIndex = z
									end
								end
							end)
							library.signals[1 + #library.signals] = optionButton.MouseEnter:Connect(function()
								tweenService:Create(newOption, TweenInfo.new(0.35, library.configuration.easingStyle, library.configuration.easingDirection), {
									BackgroundColor3 = library.colors.hoveredOptionTop,
									ImageColor3 = library.colors.hoveredOptionBottom
								}):Play()
							end)
							library.signals[1 + #library.signals] = optionButton.MouseLeave:Connect(function()
								local togged = (not multiselect and selectedOption == v) or (multiselect and table.find(selectedOption, v))
								tweenService:Create(newOption, TweenInfo.new(0.35, library.configuration.easingStyle, library.configuration.easingDirection), {
									BackgroundColor3 = (togged and library.colors.selectedOption) or library.colors.topGradient,
									ImageColor3 = (togged and library.colors.unselectedOption) or library.colors.bottomGradient
								}):Play()
							end)
							UpdateDropdownHolder()
						end
					end
				end
				local precisionscrolling = nil
				local showing = false
				local function display(dropdownEnabled, f)
					if submenuOpen == dropdown or submenuOpen == nil then
						if dropdownEnabled then
							list = resolvelist()
							AddOptions(list, f)
							submenuOpen = dropdown
							dropdownToggle.Rotation = 270
							restorezindex[newSection] = restorezindex[newSection] or newSection.ZIndex
							restorezindex[newDropdown] = restorezindex[newDropdown] or newDropdown.ZIndex
							restorezindex[sectionHolder] = restorezindex[sectionHolder] or sectionHolder.ZIndex
							newSection.ZIndex = 50 + newSection.ZIndex
							newDropdown.ZIndex = 2
							sectionHolder.ZIndex = 2
							colored_dropdown_BackgroundColor3[3] = "main"
							colored_dropdown_BackgroundColor3[4] = 1.5
							colored_dropdown_ImageColor3[3] = "main"
							colored_dropdown_ImageColor3[4] = 2.5
							tweenService:Create(dropdown, TweenInfo.new(0.35, library.configuration.easingStyle, library.configuration.easingDirection), {
								BackgroundColor3 = darkenColor(library.colors.main, 1.5),
								ImageColor3 = darkenColor(library.colors.main, 2.5)
							}):Play()
							dropdownHolderFrame.Visible = true
							if not options.DisablePrecisionScrolling then
								local scrollrate = tonumber(options.ScrollButtonRate or options.ScrollRate) or 5
								local upkey = options.ScrollUpButton or library.scrollupbutton or shared.scrollupbutton or Enum.KeyCode.Up
								local downkey = options.ScrollDownButton or library.scrolldownbutton or shared.scrolldownbutton or Enum.KeyCode.Down
								precisionscrolling = (precisionscrolling and precisionscrolling:Disconnect() and nil) or userInputService.InputBegan:Connect(function(input)
									if input.UserInputType == Enum.UserInputType.Keyboard then
										local code = input.KeyCode
										local isup = code == upkey
										local isdown = code == downkey
										if isup or isdown then
											local txt = userInputService:GetFocusedTextBox()
											if not txt or txt == dropdownSelection then
												while wait_check() and userInputService:IsKeyDown(code) do
													realDropdownHolder.CanvasPosition = Vector2:new(math.clamp(realDropdownHolder.CanvasPosition.Y + ((isup and -scrollrate) or scrollrate), 0, realDropdownHolder.AbsoluteCanvasSize.Y))
												end
											end
										end
									end
								end)
								library.signals[1 + #library.signals] = precisionscrolling
							end
						else
							submenuOpen = nil
							dropdownToggle.Rotation = 90
							colored_dropdown_BackgroundColor3[3] = "topGradient"
							colored_dropdown_BackgroundColor3[4] = nil
							colored_dropdown_ImageColor3[3] = "bottomGradient"
							colored_dropdown_ImageColor3[4] = nil
							tweenService:Create(dropdown, TweenInfo.new(0.35, library.configuration.easingStyle, library.configuration.easingDirection), {
								BackgroundColor3 = library.colors.topGradient,
								ImageColor3 = library.colors.bottomGradient
							}):Play()
							dropdownHolderFrame.Visible = false
							for ins, z in next, restorezindex do
								ins.ZIndex = z
							end
							precisionscrolling = (precisionscrolling and precisionscrolling:Disconnect() and nil) or nil
						end
					end
					showing = dropdownEnabled
				end
				local Set = (multiselect and function(t, dat)
					if nil == dat and t ~= nil then
						dat = t
					end
					local lastv = library_flags[flagName]
					if not lastv or selectedOption ~= lastv then
						if lastv and type(lastv) == "table" then
							selectedOption = library_flags[flagName]
						else
							library_flags[flagName] = selectedOption
						end
						warn("Attempting to use new table for", flagName, " Please use :Set(), because setting it through flags table may cause errors", debug.traceback(""))
						lastv = library_flags[flagName]
					end
					local cloned = {unpack(selectedOption)}
					if not dat then
						if #selectedOption ~= 0 then
							table.clear(selectedOption)
							if callback then
								task.spawn(callback, selectedOption, cloned)
							end
						end
						return selectedOption
					elseif type(dat) ~= "table" then
						warn("Expected table for argument #1 on Set for MultiSelect searchbox. Got", dat, debug.traceback(""))
						return selectedOption
					end
					for k = table.pack(unpack(dat)).n, 1, -1 do
						if dat[k] == nil then
							table.remove(dat, k)
						end
					end
					local proceed = #cloned ~= #dat
					table.clear(selectedOption)
					for k, v in next, dat do
						selectedOption[k] = v
						if not proceed and cloned[k] ~= v then
							proceed = 1
						end
					end
					dropdownSelection.Text = (passed_multiselect == "string" and multiselect) or blankstring or "Select Item(s)"
					if proceed and callback then
						task.spawn(callback, selectedOption, cloned)
					end
					return selectedOption
				end) or function(t, str)
					if nil == str and t then
						str = t
					end
					local last_v = library_flags[flagName]
					selectedOption = str
					library_flags[flagName] = str
					if options.Location then
						options.Location[options.LocationFlag or flagName] = str
					end
					local sstr = (selectedOption and tostring(selectedOption)) or blankstring or "No Blank String"
					if dropdownSelection.Text ~= sstr then
						dropdownSelection.Text = sstr
					end
					if callback and (last_v ~= str or options.AllowDuplicateCalls) then
						task.spawn(callback, str, last_v)
					end
					return str
				end
				if val ~= nil then
					Set(val)
				else
					library_flags[flagName] = selectedOption
					if options.Location then
						options.Location[options.LocationFlag or flagName] = selectedOption
					end
				end
				library.signals[1 + #library.signals] = dropdownToggle.MouseButton1Click:Connect(function()
					showing = not showing
					display(showing)
				end)
				library.signals[1 + #library.signals] = dropdownSelection.Focused:Connect(function()
					showing = true
					display(true)
				end)
				library.signals[1 + #library.signals] = dropdownSelection:GetPropertyChangedSignal("Text"):Connect(function()
					if showing then
						display(true, #dropdownSelection.Text > 0)
					end
				end)
				if not multiselect then
					library.signals[1 + #library.signals] = dropdownSelection.FocusLost:Connect(function(b)
						if showing then
							wait()
						end
						showing = false
						display(false)
						if b then
							Set(dropdownSelection.Text)
						end
					end)
				end
				AddOptions(list)
				local default = library_flags[flagName]
				local function update()
					dropdownName, callback = options.Name or dropdownName, options.Callback
					local sstr = (passed_multiselect == "string" and multiselect) or (not multiselect and library_flags[flagName] and tostring(library_flags[flagName])) or (not multiselect and selectedOption and tostring(selectedOption)) or blankstring or "Nothing"
					if dropdownSelection.Text ~= sstr then
						dropdownSelection.Text = sstr
					end
					dropdownHeadline.Text = (dropdownName and tostring(dropdownName)) or "???"
					return sstr
				end
				local function validate(fallbackValue)
					if list and table.find(list, library_flags[flagName]) then
						update()
						return true
					end
					if fallbackValue ~= nil then
						if fallbackValue == "__DEFAULT" then
							fallbackValue = default
						end
					else
						fallbackValue = list[1]
					end
					if multiselect and type(fallbackValue) ~= "table" then
						fallbackValue = {fallbackValue}
					end
					return Set(fallbackValue)
				end
				local objectdata = {
					Options = options,
					Name = flagName,
					Flag = flagName,
					Type = "SearchBox",
					Default = default,
					Parent = sectionFunctions,
					Instance = dropdownSelection,
					Validate = validate,
					Set = Set,
					RawSet = ((multiselect and function(t, dat)
						if nil == dat and t ~= nil then
							dat = t
						end
						local lastv = library_flags[flagName]
						if not lastv or selectedOption ~= lastv then
							if lastv and type(lastv) == "table" then
								selectedOption = library_flags[flagName]
							else
								library_flags[flagName] = selectedOption
							end
							warn("Attempting to use new table for", flagName, " Please use :Set(), as setting through flags table may cause errors", debug.traceback(""))
							lastv = library_flags[flagName]
						end
						local cloned = {unpack(selectedOption)}
						if not dat then
							if #selectedOption ~= 0 then
								table.clear(selectedOption)
								if callback then
									task.spawn(callback, selectedOption, cloned)
								end
							end
							return selectedOption
						elseif type(dat) ~= "table" then
							warn("Expected table for argument #1 on Set for MultiSelect searchbox. Got", dat, debug.traceback(""))
							return selectedOption
						end
						for k = table.pack(unpack(dat)).n, 1, -1 do
							if dat[k] == nil then
								table.remove(dat, k)
							end
						end
						local proceed = #cloned ~= #dat
						table.clear(selectedOption)
						for k, v in next, dat do
							selectedOption[k] = v
							if not proceed and cloned[k] ~= v then
								proceed = 1
							end
						end
						update()
						return selectedOption
					end) or function(t, str)
						if nil == str and t then
							str = t
						end
						selectedOption = str
						library_flags[flagName] = str
						if options.Location then
							options.Location[options.LocationFlag or flagName] = str
						end
						update()
						return str
					end),
					Get = function()
						return library_flags[flagName]
					end,
					Update = update,
					Reset = function()
						return Set(nil, default)
					end
				}
				function objectdata.UpdateList(t, listt, updateValues)
					if (nil == listt and t ~= nil) or (type(t) == "table" and type(listt) ~= "table") then
						listt, updateValues = t, listt
					end
					if listt == objectdata then
						listt = nil
					end
					resolvelist = getresolver(listt or options.List, options.Filter, options.Method)
					list = resolvelist()
					if updateValues then
						validate()
					end
					if showing then
						display(false)
						display(true)
					end
					return list
				end
				tabFunctions.Flags[flagName], sectionFunctions.Flags[flagName], elements[flagName] = objectdata, objectdata, objectdata
				return objectdata
			end
			sectionFunctions.NewSearchBox = sectionFunctions.AddSearchBox
			sectionFunctions.CreateSearchBox = sectionFunctions.AddSearchBox
			sectionFunctions.SearchBox = sectionFunctions.AddSearchBox
			sectionFunctions.CreateSearchbox = sectionFunctions.AddSearchBox
			sectionFunctions.NewSearchbox = sectionFunctions.AddSearchBox
			sectionFunctions.Searchbox = sectionFunctions.AddSearchBox
			sectionFunctions.Sbox = sectionFunctions.AddSearchBox
			sectionFunctions.SBox = sectionFunctions.AddSearchBox
			if isfolder and makefolder and listfiles and readfile and writefile then
				function sectionFunctions:AddPersistence(options, ...)
					options = (options and type(options) == "string" and resolvevararg("Tab", options, ...)) or options
					local dropdownName, custom_workspace, val, persistiveflags, suffix, callback, loadcallback, savecallback, postload, postsave, flagName = assert(options.Name, "Missing Name for new persistence."), options.Workspace or library.WorkspaceName, options.Value, options.Persistive or options.Flags or "all", options.Suffix, options.Callback, options.LoadCallback, options.SaveCallback, options.PostLoadCallback, options.PostSaveCallback, options.Flag or (function()
						library.unnamedpersistence = 1 + (library.unnamedpersistence or 0)
						return "Persistence" .. tostring(library.unnamedpersistence)
					end)()
					if elements[flagName] ~= nil then
						warn(debug.traceback("Warning! Re-used flag '" .. flagName .. "'", 3))
					end
					local designerpersists = options.Desginer
					local newDropdown = Instance_new("Frame")
					local dropdown = Instance_new("ImageLabel")
					local dropdownInner = Instance_new("ImageLabel")
					local dropdownToggle = Instance_new("ImageButton")
					local dropdownSelection = Instance_new("TextBox")
					local dropdownHeadline = Instance_new("TextLabel")
					local dropdownHolderFrame = Instance_new("ImageLabel")
					local dropdownHolderInner = Instance_new("ImageLabel")
					local realDropdownHolder = Instance_new("ScrollingFrame")
					local realDropdownHolderList = Instance_new("UIListLayout")
					local dropdownEnabled = false
					if not isfolder("./Function Lib") then
						makefolder("./Function Lib")
					end
					local common_string = "./Function Lib/" .. tostring(custom_workspace or library.WorkspaceName)
					local function resolvelist(nofold)
						if custom_workspace ~= options.Workspace then
							custom_workspace = options.Workspace
							common_string = "./Function Lib/" .. tostring(custom_workspace or library.WorkspaceName)
						end
						if not isfolder or not makefolder or not listfiles then
							return {}
						end
						if not isfolder(common_string) then
							if nofold then
								return {}
							end
							makefolder(common_string)
						end
						assert(isfolder(common_string), "Couldn't create folder: " .. tostring(library.WorkspaceName or "No workspace name?"))
						local names, files = {}, listfiles(common_string)
						if #files > 0 then
							local len = #common_string + 2
							for _, f in next, files do
								names[1 + #names] = string.sub(f, len, -5)
							end
							table.sort(names)
						end
						return names
					end
					local list = resolvelist(true)
					local blankstring = options.BlankValue or options.NoValueString or options.Nothing
					local selectedObjects = {}
					local optionCount = 0
					if blankstring and val == nil then
						val = blankstring
					end
					local selectedOption = val or blankstring or list[1]
					newDropdown.Name = "newDropdown"
					newDropdown.Parent = sectionHolder
					newDropdown.BackgroundColor3 = Color3.new(1, 1, 1)
					newDropdown.BackgroundTransparency = 1
					newDropdown.Size = UDim2.new(1, 0, 0, 42)
					dropdown.Name = "dropdown"
					dropdown.Parent = newDropdown
					dropdown.Active = true
					dropdown.BackgroundColor3 = library.colors.topGradient
					local colored_dropdown_BackgroundColor3 = {dropdown, "BackgroundColor3", "topGradient"}
					colored[1 + #colored] = colored_dropdown_BackgroundColor3
					dropdown.BorderColor3 = library.colors.elementBorder
					colored[1 + #colored] = {dropdown, "BorderColor3", "elementBorder"}
					dropdown.Position = UDim2.fromScale(0.027, 0.45)
					dropdown.Selectable = true
					dropdown.Size = UDim2.fromOffset(206, 18)
					dropdown.Image = "rbxassetid://2454009026"
					dropdown.ImageColor3 = library.colors.bottomGradient
					local colored_dropdown_ImageColor3 = {dropdown, "ImageColor3", "bottomGradient"}
					colored[1 + #colored] = colored_dropdown_ImageColor3
					dropdownInner.Name = "dropdownInner"
					dropdownInner.Parent = dropdown
					dropdownInner.Active = true
					dropdownInner.AnchorPoint = Vector2.new(0.5, 0.5)
					dropdownInner.BackgroundColor3 = library.colors.topGradient
					colored[1 + #colored] = {dropdownInner, "BackgroundColor3", "topGradient"}
					dropdownInner.BorderColor3 = library.colors.elementBorder
					colored[1 + #colored] = {dropdownInner, "BorderColor3", "elementBorder"}
					dropdownInner.Position = UDim2.fromScale(0.5, 0.5)
					dropdownInner.Selectable = true
					dropdownInner.Size = UDim2.new(1, -4, 1, -4)
					dropdownInner.Image = "rbxassetid://2454009026"
					dropdownInner.ImageColor3 = library.colors.bottomGradient
					colored[1 + #colored] = {dropdownInner, "ImageColor3", "bottomGradient"}
					dropdownToggle.Name = "dropdownToggle"
					dropdownToggle.Parent = dropdown
					dropdownToggle.BackgroundColor3 = Color3.new(1, 1, 1)
					dropdownToggle.BackgroundTransparency = 1
					dropdownToggle.Position = UDim2.fromScale(0.9, 0.17)
					dropdownToggle.Rotation = 90
					dropdownToggle.Size = UDim2.fromOffset(12, 12)
					dropdownToggle.ZIndex = 2
					dropdownToggle.Image = "rbxassetid://71659683"
					dropdownToggle.ImageColor3 = Color3.fromRGB(171, 171, 171)
					dropdownSelection.Name = "dropdownSelection"
					dropdownSelection.Parent = dropdown
					dropdownSelection.BackgroundColor3 = Color3.new(1, 1, 1)
					dropdownSelection.BackgroundTransparency = 1
					dropdownSelection.Position = UDim2.new(0.0295485705)
					dropdownSelection.Size = UDim2.fromScale(0.97, 1)
					dropdownSelection.ZIndex = 5
					dropdownSelection.Font = Enum.Font.Code
					dropdownSelection.LineHeight = 1.15
					dropdownSelection.Text = (selectedOption and tostring(selectedOption)) or "nil"
					dropdownSelection.TextColor3 = library.colors.otherElementText
					colored[1 + #colored] = {dropdownSelection, "TextColor3", "otherElementText"}
					dropdownSelection.TextSize = 14
					dropdownSelection.TextXAlignment = Enum.TextXAlignment.Left
					dropdownHeadline.Name = "dropdownHeadline"
					dropdownHeadline.Parent = newDropdown
					dropdownHeadline.BackgroundColor3 = Color3.new(1, 1, 1)
					dropdownHeadline.BackgroundTransparency = 1
					dropdownHeadline.Position = UDim2.fromScale(0.034, 0.03)
					dropdownHeadline.Size = UDim2.fromOffset(167, 11)
					dropdownHeadline.Font = Enum.Font.Code
					dropdownHeadline.Text = (dropdownName and tostring(dropdownName)) or "???"
					dropdownHeadline.TextColor3 = library.colors.elementText
					colored[1 + #colored] = {dropdownHeadline, "TextColor3", "elementText"}
					dropdownHeadline.TextSize = 14
					dropdownHeadline.TextXAlignment = Enum.TextXAlignment.Left
					dropdownHolderFrame.Name = "dropdownHolderFrame"
					dropdownHolderFrame.Parent = newDropdown
					dropdownHolderFrame.Active = true
					dropdownHolderFrame.BackgroundColor3 = library.colors.topGradient
					colored[1 + #colored] = {dropdownHolderFrame, "BackgroundColor3", "topGradient"}
					dropdownHolderFrame.BorderColor3 = library.colors.elementBorder
					colored[1 + #colored] = {dropdownHolderFrame, "BorderColor3", "elementBorder"}
					dropdownHolderFrame.Position = UDim2.fromScale(0.025, 1.012)
					dropdownHolderFrame.Selectable = true
					dropdownHolderFrame.Size = UDim2.fromOffset(206, 22)
					dropdownHolderFrame.Visible = false
					dropdownHolderFrame.Image = "rbxassetid://2454009026"
					dropdownHolderFrame.ImageColor3 = library.colors.bottomGradient
					colored[1 + #colored] = {dropdownHolderFrame, "ImageColor3", "bottomGradient"}
					dropdownHolderInner.Name = "dropdownHolderInner"
					dropdownHolderInner.Parent = dropdownHolderFrame
					dropdownHolderInner.Active = true
					dropdownHolderInner.AnchorPoint = Vector2.new(0.5, 0.5)
					dropdownHolderInner.BackgroundColor3 = library.colors.topGradient
					colored[1 + #colored] = {dropdownHolderInner, "BackgroundColor3", "topGradient"}
					dropdownHolderInner.BorderColor3 = library.colors.elementBorder
					colored[1 + #colored] = {dropdownHolderInner, "BorderColor3", "elementBorder"}
					dropdownHolderInner.Position = UDim2.fromScale(0.5, 0.5)
					dropdownHolderInner.Selectable = true
					dropdownHolderInner.Size = UDim2.new(1, -4, 1, -4)
					dropdownHolderInner.Image = "rbxassetid://2454009026"
					dropdownHolderInner.ImageColor3 = library.colors.bottomGradient
					colored[1 + #colored] = {dropdownHolderInner, "ImageColor3", "bottomGradient"}
					realDropdownHolder.Name = "realDropdownHolder"
					realDropdownHolder.Parent = dropdownHolderInner
					realDropdownHolder.BackgroundColor3 = Color3.new(1, 1, 1)
					realDropdownHolder.BackgroundTransparency = 1
					realDropdownHolder.Selectable = false
					realDropdownHolder.Size = UDim2.fromScale(1, 1)
					realDropdownHolder.CanvasSize = UDim2.new()
					realDropdownHolder.ScrollBarThickness = 5
					realDropdownHolder.ScrollingDirection = Enum.ScrollingDirection.Y
					realDropdownHolder.AutomaticCanvasSize = Enum.AutomaticSize.Y
					realDropdownHolder.ScrollBarImageTransparency = 0.5
					realDropdownHolder.ScrollBarImageColor3 = library.colors.section
					colored[1 + #colored] = {realDropdownHolder, "ScrollBarImageColor3", "section"}
					realDropdownHolderList.Name = "realDropdownHolderList"
					realDropdownHolderList.Parent = realDropdownHolder
					realDropdownHolderList.HorizontalAlignment = Enum.HorizontalAlignment.Center
					realDropdownHolderList.SortOrder = Enum.SortOrder.LayoutOrder
					sectionFunctions:Update()
					library.signals[1 + #library.signals] = newDropdown.MouseEnter:Connect(function()
						colored_dropdown_BackgroundColor3[3] = "main"
						colored_dropdown_BackgroundColor3[4] = 1.5
						colored_dropdown_ImageColor3[3] = "main"
						colored_dropdown_ImageColor3[4] = 2.5
						tweenService:Create(dropdown, TweenInfo.new(0.25, library.configuration.easingStyle, library.configuration.easingDirection), {
							BackgroundColor3 = darkenColor(library.colors.main, 1.5),
							ImageColor3 = darkenColor(library.colors.main, 2.5)
						}):Play()
					end)
					library.signals[1 + #library.signals] = newDropdown.MouseLeave:Connect(function()
						if not dropdownEnabled then
							colored_dropdown_BackgroundColor3[3] = "topGradient"
							colored_dropdown_BackgroundColor3[4] = nil
							colored_dropdown_ImageColor3[3] = "bottomGradient"
							colored_dropdown_ImageColor3[4] = nil
							tweenService:Create(dropdown, TweenInfo.new(0.25, library.configuration.easingStyle, library.configuration.easingDirection), {
								BackgroundColor3 = library.colors.topGradient,
								ImageColor3 = library.colors.bottomGradient
							}):Play()
						end
					end)
					local restorezindex = {}
					local function UpdateDropdownHolder()
						if optionCount >= 6 then
							realDropdownHolder.CanvasSize = UDim2:fromOffset(realDropdownHolderList.AbsoluteContentSize.Y + 2)
						elseif optionCount <= 5 then
							dropdownHolderFrame.Size = UDim2.fromOffset(206, (realDropdownHolderList.AbsoluteContentSize.Y + 4))
						end
					end
					local function AddOptions(optionsTable, filter)
						if options.Sort then
							local didstuff, dosort = nil, options.Sort
							if type(dosort) == "function" then
								local g, h = pcall(table.sort, optionsTable, dosort)
								if g then
									didstuff = true
								elseif h then
									warn("Error sorting list:", h, debug.traceback(""))
								end
							end
							if not didstuff then
								table.sort(optionsTable, library.defaultSort)
							end
						end
						if blankstring and (optionsTable[1] ~= blankstring or table.find(optionsTable, blankstring, 2)) then
							local exists = table.find(optionsTable, blankstring)
							if exists then
								for _ = 1, 35 do
									table.remove(optionsTable, exists)
									exists = table.find(optionsTable, blankstring)
									if not exists then
										break
									end
								end
							end
							table.insert(optionsTable, 1, blankstring)
						end
						optionCount = 0
						realDropdownHolderList.Parent = nil
						realDropdownHolder:ClearAllChildren()
						realDropdownHolderList.Parent = realDropdownHolder
						for _, v in next, optionsTable do
							if not filter or tostring(v):lower():find(dropdownSelection.Text:lower(), 1, true) then
								optionCount = optionCount + 1
								UpdateDropdownHolder()
								local newOption = Instance_new("ImageLabel")
								local optionButton = Instance_new("TextButton")
								if selectedOption == v or not selectedObjects[1] or not selectedObjects[2] then
									selectedObjects[1] = newOption
									selectedObjects[2] = optionButton
								end
								newOption.Name = "Frame"
								newOption.Parent = realDropdownHolder
								newOption.BackgroundColor3 = (selectedOption == v and library.colors.selectedOption or library.colors.topGradient)
								newOption.BorderSizePixel = 0
								newOption.Size = UDim2.fromOffset(202, 18)
								newOption.Image = "rbxassetid://2454009026"
								newOption.ImageColor3 = (selectedOption == v and library.colors.unselectedOption or library.colors.bottomGradient)
								optionButton.Name = tostring(v)
								optionButton.Parent = newOption
								optionButton.AnchorPoint = Vector2.new(0.5, 0.5)
								optionButton.BackgroundColor3 = Color3.new(1, 1, 1)
								optionButton.BackgroundTransparency = 1
								optionButton.Position = UDim2.fromScale(0.5, 0.5)
								optionButton.Size = UDim2.new(1, -10, 1)
								optionButton.ZIndex = 5
								optionButton.Font = Enum.Font.Code
								optionButton.Text = (selectedOption == v and " " .. tostring(v)) or tostring(v)
								optionButton.TextColor3 = (selectedOption == v and library.colors.main or library.colors.otherElementText)
								optionButton.TextSize = 14
								optionButton.TextXAlignment = Enum.TextXAlignment.Left
								library.signals[1 + #library.signals] = optionButton.MouseButton1Down:Connect(function()
									dropdownSelection.Text = tostring(v)
									restorezindex[newSection] = restorezindex[newSection] or newSection.ZIndex
									restorezindex[newDropdown] = restorezindex[newDropdown] or newDropdown.ZIndex
									restorezindex[sectionHolder] = restorezindex[sectionHolder] or sectionHolder.ZIndex
									if selectedOption ~= v then
										local last_v = library_flags[flagName]
										selectedObjects[1].BackgroundColor3 = library.colors.topGradient
										selectedObjects[1].ImageColor3 = library.colors.bottomGradient
										selectedObjects[2].Text = selectedObjects[2].Name
										selectedObjects[2].TextColor3 = library.colors.otherElementText
										selectedOption = v
										selectedObjects[1] = newOption
										selectedObjects[2] = optionButton
										newOption.BackgroundColor3 = library.colors.selectedOption
										newOption.ImageColor3 = library.colors.unselectedOption
										optionButton.TextColor3 = library.colors.main
										dropdownHolderFrame.Visible = false
										dropdownToggle.Rotation = 90
										dropdownEnabled = false
										colored_dropdown_BackgroundColor3[3] = "topGradient"
										colored_dropdown_BackgroundColor3[4] = nil
										colored_dropdown_ImageColor3[3] = "bottomGradient"
										colored_dropdown_ImageColor3[4] = nil
										tweenService:Create(dropdown, TweenInfo.new(0.35, library.configuration.easingStyle, library.configuration.easingDirection), {
											BackgroundColor3 = library.colors.topGradient,
											ImageColor3 = library.colors.bottomGradient
										}):Play()
										library_flags[flagName] = selectedOption
										if options.Location then
											options.Location[options.LocationFlag or flagName] = selectedOption
										end
										dropdownSelection.Text = tostring(selectedOption)
										if submenuOpen then
											submenuOpen = nil
										end
										if callback then
											task.spawn(callback, selectedOption, last_v)
										end
									else
										submenuOpen = nil
										dropdownToggle.Rotation = 90
										newDropdown.ZIndex = 1
										sectionHolder.ZIndex = 1
										colored_dropdown_BackgroundColor3[3] = "topGradient"
										colored_dropdown_BackgroundColor3[4] = nil
										colored_dropdown_ImageColor3[3] = "bottomGradient"
										colored_dropdown_ImageColor3[4] = nil
										tweenService:Create(dropdown, TweenInfo.new(0.35, library.configuration.easingStyle, library.configuration.easingDirection), {
											BackgroundColor3 = library.colors.topGradient,
											ImageColor3 = library.colors.bottomGradient
										}):Play()
										dropdownHolderFrame.Visible = false
									end
									for ins, z in next, restorezindex do
										ins.ZIndex = z
									end
								end)
								library.signals[1 + #library.signals] = optionButton.MouseEnter:Connect(function()
									tweenService:Create(newOption, TweenInfo.new(0.35, library.configuration.easingStyle, library.configuration.easingDirection), {
										BackgroundColor3 = library.colors.hoveredOptionTop,
										ImageColor3 = library.colors.hoveredOptionBottom
									}):Play()
								end)
								library.signals[1 + #library.signals] = optionButton.MouseLeave:Connect(function()
									tweenService:Create(newOption, TweenInfo.new(0.35, library.configuration.easingStyle, library.configuration.easingDirection), {
										BackgroundColor3 = library.colors.unhoveredOptionTop,
										ImageColor3 = library.colors.unhoveredOptionBottom
									}):Play()
								end)
								UpdateDropdownHolder()
							end
						end
					end
					local precisionscrolling = nil
					local showing = false
					local function display(dropdownEnabled, f)
						if submenuOpen == dropdown or submenuOpen == nil then
							if dropdownEnabled then
								list = resolvelist(true)
								AddOptions(list, f)
								submenuOpen = dropdown
								restorezindex[newSection] = restorezindex[newSection] or newSection.ZIndex
								restorezindex[newDropdown] = restorezindex[newDropdown] or newDropdown.ZIndex
								restorezindex[sectionHolder] = restorezindex[sectionHolder] or sectionHolder.ZIndex
								newSection.ZIndex = 50 + newSection.ZIndex
								dropdownToggle.Rotation = 270
								newDropdown.ZIndex = 2
								sectionHolder.ZIndex = 2
								colored_dropdown_BackgroundColor3[3] = "main"
								colored_dropdown_BackgroundColor3[4] = 1.5
								colored_dropdown_ImageColor3[3] = "main"
								colored_dropdown_ImageColor3[4] = 2.5
								tweenService:Create(dropdown, TweenInfo.new(0.35, library.configuration.easingStyle, library.configuration.easingDirection), {
									BackgroundColor3 = darkenColor(library.colors.main, 1.5),
									ImageColor3 = darkenColor(library.colors.main, 2.5)
								}):Play()
								dropdownHolderFrame.Visible = true
								if not options.DisablePrecisionScrolling then
									local upkey = options.ScrollUpButton or library.scrollupbutton or shared.scrollupbutton or Enum.KeyCode.Up
									local downkey = options.ScrollDownButton or library.scrolldownbutton or shared.scrolldownbutton or Enum.KeyCode.Down
									precisionscrolling = (precisionscrolling and precisionscrolling:Disconnect() and nil) or userInputService.InputBegan:Connect(function(input)
										if input.UserInputType == Enum.UserInputType.Keyboard then
											local code = input.KeyCode
											local isup = code == upkey
											local isdown = code == downkey
											if isup or isdown then
												local txt = userInputService:GetFocusedTextBox()
												if not txt then
													while wait_check() and userInputService:IsKeyDown(code) do
														realDropdownHolder.CanvasPosition = Vector2:new(math.clamp(realDropdownHolder.CanvasPosition.Y + ((isup and -5) or 5), 0, realDropdownHolder.AbsoluteCanvasSize.Y))
													end
												end
											end
										end
									end)
									library.signals[1 + #library.signals] = precisionscrolling
								end
							else
								submenuOpen = nil
								dropdownToggle.Rotation = 90
								colored_dropdown_BackgroundColor3[3] = "topGradient"
								colored_dropdown_BackgroundColor3[4] = nil
								colored_dropdown_ImageColor3[3] = "bottomGradient"
								colored_dropdown_ImageColor3[4] = nil
								tweenService:Create(dropdown, TweenInfo.new(0.35, library.configuration.easingStyle, library.configuration.easingDirection), {
									BackgroundColor3 = library.colors.topGradient,
									ImageColor3 = library.colors.bottomGradient
								}):Play()
								dropdownHolderFrame.Visible = false
								for ins, z in next, restorezindex do
									ins.ZIndex = z
								end
								precisionscrolling = (precisionscrolling and precisionscrolling:Disconnect() and nil) or nil
							end
							showing = dropdownEnabled
						end
					end
					local last_v = nil
					local function Set(t, str)
						if nil == str and t then
							str = t
						end
						selectedOption = str
						last_v = library_flags[flagName]
						library_flags[flagName] = str
						if options.Location then
							options.Location[options.LocationFlag or flagName] = str
						end
						local sstr = (selectedOption and tostring(selectedOption)) or blankstring or "No Blank String"
						if dropdownSelection.Text ~= sstr then
							dropdownSelection.Text = sstr
						end
						if callback and (last_v ~= str or options.AllowDuplicateCalls) then
							task.spawn(callback, str, last_v)
						end
						return str
					end
					if val ~= nil then
						Set(val)
					else
						Set("Filename")
					end
					library.signals[1 + #library.signals] = dropdownSelection.Focused:Connect(function()
						showing = true
						display(true)
					end)
					library.signals[1 + #library.signals] = dropdownSelection:GetPropertyChangedSignal("Text"):Connect(function()
						if showing then
							display(true, #dropdownSelection.Text > 0)
						end
					end)
					library.signals[1 + #library.signals] = dropdownSelection.FocusLost:Connect(function(b)
						if showing then
							wait()
						end
						showing = false
						display(false)
						if b then
							Set(dropdownSelection.Text)
						end
					end)
					AddOptions(list)
					local function savestuff(s, get)
						if not s or type(s) ~= "string" then
							s = nil
						end
						local rawfile = "json__save"
						if not get then
							local filenameddst = string.gsub(s or dropdownSelection.Text or "", "%W", "")
							if #filenameddst == 0 then
								return
							end
							rawfile = string.format("%s/%s.txt", common_string, filenameddst)
						end
						if savecallback then
							local x, e = pcall(savecallback, rawfile, library_flags[flagName])
							if not x and e then
								warn("Error while calling the Pre-Save callback:", e, debug.traceback(""))
							end
						end
						local working_with = {}
						if persistiveflags == 1 or persistiveflags == true or persistiveflags == "*" then
							persistiveflags = "all"
						elseif persistiveflags == 2 then
							persistiveflags = "tab"
						elseif persistiveflags == 3 then
							persistiveflags = "section"
						end
						if persistiveflags == "all" or persistiveflags == "tab" or persistiveflags == "section" then
							for cflag, data in next, (persistiveflags == "all" and elements) or (persistiveflags == "tab" and tabFunctions.Flags) or (persistiveflags == "section" and sectionFunctions.Flags) do
								if data.Type ~= "Persistence" and (designerpersists or string.sub(cflag, 1, 11) ~= "__Designer.") then
									working_with[cflag] = data
								end
							end
						elseif type(persistiveflags) == "table" then
							if #persistiveflags > 0 then
								local inverted = persistiveflags[0] == false or persistiveflags.Inverted
								for k, cflag in next, persistiveflags do
									if k > 0 then
										local data = elements[cflag]
										if data and data.Type ~= "Persistence" and (designerpersists or string.sub(cflag, 1, 11) ~= "__Designer.") then
											working_with[cflag] = (not inverted and data) or nil
										end
									end
								end
							else
								for cflag, persists in next, elements do
									if persists and (designerpersists or string.sub(cflag, 1, 11) ~= "__Designer.") then
										local data = elements[cflag]
										if data then
											working_with[cflag] = data
										end
									end
								end
							end
						end
						local saving = {}
						for cflag in next, working_with do
							local value = library_flags[cflag]
							local good, jval = nil, nil
							if value ~= nil then
								good, jval = JSONEncode(value)
							else
								good, jval = true, "null"
							end
							if not good or (jval == "null" and value ~= nil) then
								local typ = typeof(value)
								if typ == "Color3" then
									value = (library.rainbowflags[cflag] and "rainbow") or Color3ToHex(value)
								end
								value = tostring(value)
								good, jval = JSONEncode(value)
								if not good or (jval == "null" and value ~= nil) then
									warn("Could not save value:", value, debug.traceback(""))
								end
							end
							if good and jval then
								saving[cflag] = value
							end
						end
						local ret = nil
						local good, content = JSONEncode(saving)
						if good and content then
							if not get then
								if not isfolder(common_string) then
									makefolder(common_string)
								end
								writefile(rawfile, content)
							else
								ret = content
							end
						end
						if postsave then
							local x, e = pcall(postsave, rawfile, library_flags[flagName])
							if not x and e then
								warn("Error while calling the Post-Save callback:", e, debug.traceback(""))
							end
						end
						return ret
					end
					local function loadstuff(s, jsonmode, silent)
						if not s or type(s) ~= "string" then
							s = nil
						end
						local filename = "json__load"
						if not jsonmode then
							local filenameddst = convertfilename(s or dropdownSelection.Text, nil, "")
							if #filenameddst == 0 then
								return
							end
							filename = string.format("%s/%s.txt", common_string, filenameddst)
						end
						if loadcallback then
							local x, e = pcall(loadcallback, (jsonmode and s) or filename, library_flags[flagName])
							if not x and e then
								warn("Error while calling the Pre-Load callback:", e, debug.traceback(""))
							end
						end
						if jsonmode or not isfile or isfile(filename) then
							local content = (jsonmode and s) or (not jsonmode and readfile(filename))
							if content and #content > 1 then
								local good, jcontent = JSONDecode(content)
								if good and jcontent then
									for cflag, val in next, jcontent do
										if val and type(val) == "string" and #val > 7 and #val < 64 and string.sub(val, 1, 5) == "Enum." then
											local e = string.find(val, ".", 6, true)
											if e then
												local en = Enum[string.sub(val, 6, e - 1)]
												en = en and en[string.sub(val, e + 1)]
												if en then
													val = en
												else
													warn("Tried & failed to convert '" .. val .. "' to EnumItem")
												end
											end
										end
										local data = elements[cflag]
										if data and data.Type ~= "Persistence" then
											if silent and data.RawSet then
												data:RawSet(val)
											elseif data.Set then
												data:Set(val)
											else
												library_flags[cflag] = val
											end
										end
									end
								end
							end
						end
						if postload then
							local x, e = pcall(postload, filename, library_flags[flagName])
							if not x and e then
								warn("Error while calling the Post-Load callback:", e, debug.traceback(""))
							end
						end
					end
					do
						local buttons, offset = {}, 0
						local fram = nil
						for _, options in next, {{
							Name = "Save" .. ((suffix and (" " .. tostring(suffix))) or ""),
							Callback = savestuff
							}, {
								Name = "Load" .. ((suffix and (" " .. tostring(suffix))) or ""),
								Callback = loadstuff
							}} do
							local buttonName, callback = options.Name, options.Callback
							local realButton = Instance_new("TextButton")
							realButton.Name = "realButton"
							realButton.BackgroundColor3 = Color3.new(1, 1, 1)
							realButton.BackgroundTransparency = 1
							realButton.Size = UDim2.fromScale(1, 1)
							realButton.ZIndex = 5
							realButton.Font = Enum.Font.Code
							realButton.Text = (buttonName and tostring(buttonName)) or "???"
							realButton.TextColor3 = library.colors.elementText
							colored[1 + #colored] = {realButton, "TextColor3", "elementText"}
							realButton.TextSize = 14
							local textsize = textToSize(realButton).X + 14
							if newSection.Parent.AbsoluteSize.X < offset + textsize + 8 then
								offset, fram = 0, nil
							end
							local newButton = fram or Instance_new("Frame")
							fram = newButton
							local button = Instance_new("ImageLabel")
							newButton.Name = removeSpaces((buttonName and buttonName:lower() or "???") .. "Holder")
							newButton.Parent = sectionHolder
							newButton.BackgroundColor3 = Color3.new(1, 1, 1)
							newButton.BackgroundTransparency = 1
							newButton.Size = UDim2.new(1, 0, 0, 24)
							button.Name = "button"
							button.Parent = newButton
							button.Active = true
							button.BackgroundColor3 = library.colors.topGradient
							local colored_button_BackgroundColor3 = {button, "BackgroundColor3", "topGradient"}
							colored[1 + #colored] = colored_button_BackgroundColor3
							button.BorderColor3 = library.colors.elementBorder
							colored[1 + #colored] = {button, "BorderColor3", "elementBorder"}
							button.Position = UDim2.new(0.031, offset, 0.166)
							button.Selectable = true
							button.Size = UDim2.fromOffset(28, 18)
							button.Image = "rbxassetid://2454009026"
							button.ImageColor3 = library.colors.bottomGradient
							local colored_button_ImageColor3 = {button, "ImageColor3", "bottomGradient"}
							colored[1 + #colored] = colored_button_ImageColor3
							local buttonInner = Instance_new("ImageLabel")
							buttonInner.Name = "buttonInner"
							buttonInner.Parent = button
							buttonInner.Active = true
							buttonInner.AnchorPoint = Vector2.new(0.5, 0.5)
							buttonInner.BackgroundColor3 = library.colors.topGradient
							colored[1 + #colored] = {buttonInner, "BackgroundColor3", "topGradient"}
							buttonInner.BorderColor3 = library.colors.elementBorder
							colored[1 + #colored] = {buttonInner, "BorderColor3", "elementBorder"}
							buttonInner.Position = UDim2.fromScale(0.5, 0.5)
							buttonInner.Selectable = true
							buttonInner.Size = UDim2.new(1, -4, 1, -4)
							buttonInner.Image = "rbxassetid://2454009026"
							buttonInner.ImageColor3 = library.colors.bottomGradient
							colored[1 + #colored] = {buttonInner, "ImageColor3", "bottomGradient"}
							button.Size = UDim2.fromOffset(textsize, 18)
							realButton.Parent = button
							offset = offset + textsize + 6
							sectionFunctions:Update()
							local presses = 0
							library.signals[1 + #library.signals] = realButton.MouseButton1Click:Connect(function()
								if not library.colorpicker and not submenuOpen then
									presses = 1 + presses
									task.spawn(callback, presses)
								end
							end)
							library.signals[1 + #library.signals] = button.MouseEnter:Connect(function()
								colored_button_BackgroundColor3[3] = "main"
								colored_button_BackgroundColor3[4] = 1.5
								colored_button_ImageColor3[3] = "main"
								colored_button_ImageColor3[4] = 2.5
								tweenService:Create(button, TweenInfo.new(0.35, library.configuration.easingStyle, library.configuration.easingDirection), {
									BackgroundColor3 = darkenColor(library.colors.main, 1.5),
									ImageColor3 = darkenColor(library.colors.main, 2.5)
								}):Play()
							end)
							library.signals[1 + #library.signals] = button.MouseLeave:Connect(function()
								colored_button_BackgroundColor3[3] = "topGradient"
								colored_button_BackgroundColor3[4] = nil
								colored_button_ImageColor3[3] = "bottomGradient"
								colored_button_ImageColor3[4] = nil
								tweenService:Create(button, TweenInfo.new(0.35, library.configuration.easingStyle, library.configuration.easingDirection), {
									BackgroundColor3 = library.colors.topGradient,
									ImageColor3 = library.colors.bottomGradient
								}):Play()
							end)
						end
					end
					local default = library_flags[flagName]
					local function update()
						dropdownName, custom_workspace, persistiveflags, suffix, callback, loadcallback, savecallback, postload, postsave = options.Name or dropdownName, options.Workspace or library.WorkspaceName, options.Persistive or options.Flags or "all", options.Suffix, options.Callback, options.LoadCallback, options.SaveCallback, options.PostLoadCallback, options.PostSaveCallback
						local sstr = tostring(library_flags[flagName])
						if dropdownSelection.Text ~= sstr then
							dropdownSelection.Text = sstr
						end
						dropdownHeadline.Text = (dropdownName and tostring(dropdownName)) or "???"
						return sstr
					end
					local objectdata = {
						Options = options,
						Name = flagName,
						Flag = flagName,
						Type = "Persistence",
						Default = default,
						Parent = sectionFunctions,
						Instance = dropdownSelection,
						Set = Set,
						SaveFile = function(t, str, ret)
							if t ~= nil and type(t) ~= "table" then
								str, ret = t, str
							end
							if type(str) == "string" then
								str = str:match("(.+)%..+$") or str
							end
							return savestuff(str, ret)
						end,
						LoadFile = function(t, str, jsonmode)
							if t ~= nil and type(t) ~= "table" then
								str, jsonmode = t, str
							end
							if isfile and isfile(str) then
								return loadstuff(readfile(str), true)
							elseif not jsonmode and type(str) == "string" then
								str = str:match("(.+)%..+$") or str
							end
							return loadstuff(str, jsonmode)
						end,
						LoadJSON = function(_, json)
							return loadstuff(json, true)
						end,
						LoadFileRaw = function(t, str, jsonmode)
							if t ~= nil and type(t) ~= "table" then
								str, jsonmode = t, str
							end
							if isfile and isfile(str) then
								return loadstuff(readfile(str), true, true)
							elseif not jsonmode and type(str) == "string" then
								str = str:match("(.+)%..+$") or str
							end
							return loadstuff(str, jsonmode, true)
						end,
						LoadJSONRaw = function(_, json)
							return loadstuff(json, true, true)
						end,
						GetJSON = function(t, clipboard)
							if nil == clipboard and t ~= nil then
								clipboard = t
							end
							local json = savestuff(nil, true)
							local clipfunc = (clipboard and type(clipboard) == "function" and clipboard) or setclipboard
							if clipboard and clipfunc then
								clipfunc(json)
							end
							return json
						end,
						RawSet = function(t, str)
							if nil == str and t ~= nil then
								str = t
							end
							selectedOption = str
							last_v = library_flags[flagName]
							library_flags[flagName] = str
							if options.Location then
								options.Location[options.LocationFlag or flagName] = str
							end
							update()
							return str
						end,
						Get = function()
							return library_flags[flagName]
						end,
						Update = update,
						Reset = function()
							return Set(nil, default)
						end
					}
					tabFunctions.Flags[flagName], sectionFunctions.Flags[flagName], elements[flagName] = objectdata, objectdata, objectdata
					return objectdata
				end
			else
				function sectionFunctions.AddPersistence()
					if not library.warnedpersistance then
						library.warnedpersistance = 1
						warn(debug.traceback("Persistance not supported"))
					end
					function sectionFunctions.AddPersistence()
					end
				end
			end
			sectionFunctions.NewPersistence = sectionFunctions.AddPersistence
			sectionFunctions.CreatePersistence = sectionFunctions.AddPersistence
			sectionFunctions.Persistence = sectionFunctions.AddPersistence
			sectionFunctions.CreateSaveLoad = sectionFunctions.AddPersistence
			sectionFunctions.SaveLoad = sectionFunctions.AddPersistence
			sectionFunctions.SL = sectionFunctions.AddPersistence
			function sectionFunctions:AddDropdown(options, ...)
				options = (options and type(options) == "string" and resolvevararg("Dropdown", options, ...)) or options
				local dropdownName, listt, val, callback, flagName = assert(options.Name, "Missing Name for new searchbox."), assert(options.List, "Missing List for new searchbox."), options.Value, options.Callback, options.Flag or (function()
					library.unnameddropdown = 1 + (library.unnameddropdown or 0)
					return "Dropdown" .. tostring(library.unnameddropdown)
				end)()
				if elements[flagName] ~= nil then
					warn(debug.traceback("Warning! Re-used flag '" .. flagName .. "'", 3))
				end
				local newDropdown = Instance_new("Frame")
				local dropdown = Instance_new("ImageLabel")
				local dropdownInner = Instance_new("ImageLabel")
				local dropdownToggle = Instance_new("ImageButton")
				local dropdownSelection = Instance_new("TextLabel")
				local dropdownHeadline = Instance_new("TextLabel")
				local dropdownHolderFrame = Instance_new("ImageLabel")
				local dropdownHolderInner = Instance_new("ImageLabel")
				local realDropdownHolder = Instance_new("ScrollingFrame")
				local realDropdownHolderList = Instance_new("UIListLayout")
				local dropdownEnabled = false
				local multiselect = options.MultiSelect or options.Multi or options.Multiple
				local addcallback = options.ItemAdded or options.AddedCallback
				local delcallback = options.ItemRemoved or options.RemovedCallback
				local clrcallback = options.ItemsCleared or options.ClearedCallback
				local modcallback = options.ItemChanged or options.ChangedCallback
				local blankstring = not multiselect and (options.BlankValue or options.NoValueString or options.Nothing)
				local resolvelist = getresolver(listt, options.Filter, options.Method)
				local list = resolvelist()
				local selectedOption = list[1]
				local passed_multiselect = multiselect and type(multiselect)
				if blankstring and val == nil then
					val = blankstring
				end
				if val ~= nil then
					selectedOption = val
				end
				if multiselect and (not selectedOption or type(selectedOption) ~= "table") then
					selectedOption = {}
				end
				local selectedObjects = {}
				local optionCount = 0
				newDropdown.Name = "newDropdown"
				newDropdown.Parent = sectionHolder
				newDropdown.BackgroundColor3 = Color3.new(1, 1, 1)
				newDropdown.BackgroundTransparency = 1
				newDropdown.Size = UDim2.new(1, 0, 0, 42)
				dropdown.Name = "dropdown"
				dropdown.Parent = newDropdown
				dropdown.Active = true
				dropdown.BackgroundColor3 = library.colors.topGradient
				local colored_dropdown_BackgroundColor3 = {dropdown, "BackgroundColor3", "topGradient"}
				colored[1 + #colored] = colored_dropdown_BackgroundColor3
				dropdown.BorderColor3 = library.colors.elementBorder
				colored[1 + #colored] = {dropdown, "BorderColor3", "elementBorder"}
				dropdown.Position = UDim2.fromScale(0.027, 0.45)
				dropdown.Selectable = true
				dropdown.Size = UDim2.fromOffset(206, 18)
				dropdown.Image = "rbxassetid://2454009026"
				dropdown.ImageColor3 = library.colors.bottomGradient
				local colored_dropdown_ImageColor3 = {dropdown, "ImageColor3", "bottomGradient"}
				colored[1 + #colored] = colored_dropdown_ImageColor3
				dropdownInner.Name = "dropdownInner"
				dropdownInner.Parent = dropdown
				dropdownInner.Active = true
				dropdownInner.AnchorPoint = Vector2.new(0.5, 0.5)
				dropdownInner.BackgroundColor3 = library.colors.topGradient
				colored[1 + #colored] = {dropdownInner, "BackgroundColor3", "topGradient"}
				dropdownInner.BorderColor3 = library.colors.elementBorder
				colored[1 + #colored] = {dropdownInner, "BorderColor3", "elementBorder"}
				dropdownInner.Position = UDim2.fromScale(0.5, 0.5)
				dropdownInner.Selectable = true
				dropdownInner.Size = UDim2.new(1, -4, 1, -4)
				dropdownInner.Image = "rbxassetid://2454009026"
				dropdownInner.ImageColor3 = library.colors.bottomGradient
				colored[1 + #colored] = {dropdownInner, "ImageColor3", "bottomGradient"}
				dropdownToggle.Name = "dropdownToggle"
				dropdownToggle.Parent = dropdown
				dropdownToggle.BackgroundColor3 = Color3.new(1, 1, 1)
				dropdownToggle.BackgroundTransparency = 1
				dropdownToggle.Position = UDim2.fromScale(0.9, 0.17)
				dropdownToggle.Rotation = 90
				dropdownToggle.Size = UDim2.fromOffset(12, 12)
				dropdownToggle.ZIndex = 2
				dropdownToggle.Image = "rbxassetid://71659683"
				dropdownToggle.ImageColor3 = Color3.fromRGB(171, 171, 171)
				dropdownSelection.Name = "dropdownSelection"
				dropdownSelection.Parent = dropdown
				dropdownSelection.Active = true
				dropdownSelection.BackgroundColor3 = Color3.new(1, 1, 1)
				dropdownSelection.BackgroundTransparency = 1
				dropdownSelection.Position = UDim2.new(0.0295)
				dropdownSelection.Selectable = true
				dropdownSelection.Size = UDim2.fromScale(0.97, 1)
				dropdownSelection.ZIndex = 5
				dropdownSelection.Font = Enum.Font.Code
				dropdownSelection.Text = (passed_multiselect == "string" and multiselect) or (multiselect and (blankstring or "Select Item(s)")) or (selectedOption and tostring(selectedOption)) or blankstring or "No Blank String"
				dropdownSelection.TextColor3 = library.colors.otherElementText
				colored[1 + #colored] = {dropdownSelection, "TextColor3", "otherElementText"}
				dropdownSelection.TextSize = 14
				dropdownSelection.TextXAlignment = Enum.TextXAlignment.Left
				dropdownHeadline.Name = "dropdownHeadline"
				dropdownHeadline.Parent = newDropdown
				dropdownHeadline.BackgroundColor3 = Color3.new(1, 1, 1)
				dropdownHeadline.BackgroundTransparency = 1
				dropdownHeadline.Position = UDim2.fromScale(0.034, 0.03)
				dropdownHeadline.Size = UDim2.fromOffset(167, 11)
				dropdownHeadline.Font = Enum.Font.Code
				dropdownHeadline.Text = (dropdownName and tostring(dropdownName)) or "???"
				dropdownHeadline.TextColor3 = library.colors.elementText
				colored[1 + #colored] = {dropdownHeadline, "TextColor3", "elementText"}
				dropdownHeadline.TextSize = 14
				dropdownHeadline.TextXAlignment = Enum.TextXAlignment.Left
				dropdownHolderFrame.Name = "dropdownHolderFrame"
				dropdownHolderFrame.Parent = newDropdown
				dropdownHolderFrame.Active = true
				dropdownHolderFrame.BackgroundColor3 = library.colors.topGradient
				colored[1 + #colored] = {dropdownHolderFrame, "BackgroundColor3", "topGradient"}
				dropdownHolderFrame.BorderColor3 = library.colors.elementBorder
				colored[1 + #colored] = {dropdownHolderFrame, "BorderColor3", "elementBorder"}
				dropdownHolderFrame.Position = UDim2.fromScale(0.025, 1.012)
				dropdownHolderFrame.Selectable = true
				dropdownHolderFrame.Size = UDim2.fromOffset(206, 22)
				dropdownHolderFrame.Visible = false
				dropdownHolderFrame.Image = "rbxassetid://2454009026"
				dropdownHolderFrame.ImageColor3 = library.colors.bottomGradient
				colored[1 + #colored] = {dropdownHolderFrame, "ImageColor3", "bottomGradient"}
				dropdownHolderInner.Name = "dropdownHolderInner"
				dropdownHolderInner.Parent = dropdownHolderFrame
				dropdownHolderInner.Active = true
				dropdownHolderInner.AnchorPoint = Vector2.new(0.5, 0.5)
				dropdownHolderInner.BackgroundColor3 = library.colors.topGradient
				colored[1 + #colored] = {dropdownHolderInner, "BackgroundColor3", "topGradient"}
				dropdownHolderInner.BorderColor3 = library.colors.elementBorder
				colored[1 + #colored] = {dropdownHolderInner, "BorderColor3", "elementBorder"}
				dropdownHolderInner.Position = UDim2.fromScale(0.5, 0.5)
				dropdownHolderInner.Selectable = true
				dropdownHolderInner.Size = UDim2.new(1, -4, 1, -4)
				dropdownHolderInner.Image = "rbxassetid://2454009026"
				dropdownHolderInner.ImageColor3 = library.colors.bottomGradient
				colored[1 + #colored] = {dropdownHolderInner, "ImageColor3", "bottomGradient"}
				realDropdownHolder.Name = "realDropdownHolder"
				realDropdownHolder.Parent = dropdownHolderInner
				realDropdownHolder.BackgroundColor3 = Color3.new(1, 1, 1)
				realDropdownHolder.BackgroundTransparency = 1
				realDropdownHolder.Selectable = false
				realDropdownHolder.Size = UDim2.fromScale(1, 1)
				realDropdownHolder.CanvasSize = UDim2.new()
				realDropdownHolder.ScrollBarThickness = 5
				realDropdownHolder.ScrollingDirection = Enum.ScrollingDirection.Y
				realDropdownHolder.AutomaticCanvasSize = Enum.AutomaticSize.Y
				realDropdownHolder.ScrollBarImageTransparency = 0.5
				realDropdownHolder.ScrollBarImageColor3 = library.colors.section
				colored[1 + #colored] = {realDropdownHolder, "ScrollBarImageColor3", "section"}
				realDropdownHolderList.Name = "realDropdownHolderList"
				realDropdownHolderList.Parent = realDropdownHolder
				realDropdownHolderList.HorizontalAlignment = Enum.HorizontalAlignment.Center
				realDropdownHolderList.SortOrder = Enum.SortOrder.LayoutOrder
				sectionFunctions:Update()
				local showing = false
				local function UpdateDropdownHolder()
					if optionCount >= 6 then
						realDropdownHolder.CanvasSize = UDim2:fromOffset(realDropdownHolderList.AbsoluteContentSize.Y + 2)
					elseif optionCount <= 5 then
						dropdownHolderFrame.Size = UDim2.fromOffset(206, realDropdownHolderList.AbsoluteContentSize.Y + 4)
					end
				end
				local restorezindex = {}
				local Set = (multiselect and function(t, dat)
					if nil == dat and t ~= nil then
						dat = t
					end
					local lastv = library_flags[flagName]
					if not lastv or selectedOption ~= lastv then
						if lastv and type(lastv) == "table" then
							selectedOption = library_flags[flagName]
						else
							library_flags[flagName] = selectedOption
						end
						warn("Attempting to use new table for", flagName, " Please use :Set(), as setting through flags table may cause errors", debug.traceback(""))
						lastv = library_flags[flagName]
					end
					local cloned = {unpack(selectedOption)}
					if not dat then
						if #selectedOption ~= 0 then
							table.clear(selectedOption)
							if callback then
								task.spawn(callback, selectedOption, cloned)
							end
						end
						return selectedOption
					elseif type(dat) ~= "table" then
						warn("Expected table for argument #1 on Set for MultiSelect dropdown. Got", dat, debug.traceback(""))
						return selectedOption
					end
					for k = table.pack(unpack(dat)).n, 1, -1 do
						if dat[k] == nil then
							table.remove(dat, k)
						end
					end
					local proceed = #cloned ~= #dat
					table.clear(selectedOption)
					for k, v in next, dat do
						selectedOption[k] = v
						if not proceed and cloned[k] ~= v then
							proceed = 1
						end
					end
					dropdownSelection.Text = (passed_multiselect == "string" and multiselect) or blankstring or "Select Item(s)"
					if proceed and callback then
						task.spawn(callback, selectedOption, cloned)
					end
					return selectedOption
				end) or function(t, str)
					if nil == str and t ~= nil then
						str = t
					end
					local last_v = library_flags[flagName]
					selectedOption = str
					library_flags[flagName] = str
					if options.Location then
						options.Location[options.LocationFlag or flagName] = str
					end
					local sstr = (selectedOption and tostring(selectedOption)) or blankstring or "No Blank String"
					if dropdownSelection.Text ~= sstr then
						dropdownSelection.Text = sstr
					end
					if callback and (last_v ~= str or options.AllowDuplicateCalls) then
						task.spawn(callback, str, last_v)
					end
					return str
				end
				if val ~= nil then
					Set(val)
				else
					library_flags[flagName] = selectedOption
					if options.Location then
						options.Location[options.LocationFlag or flagName] = selectedOption
					end
				end
				local function AddOptions(optionsTable)
					if options.Sort then
						local didstuff, dosort = nil, options.Sort
						if type(dosort) == "function" then
							local g, h = pcall(table.sort, optionsTable, dosort)
							if g then
								didstuff = true
							elseif h then
								warn("Error sorting list:", h, debug.traceback(""))
							end
						elseif dosort ~= 1 and dosort ~= true then
							warn("Potential mistake for passed Sort argument:", dosort, debug.traceback(""))
						end
						if not didstuff then
							table.sort(optionsTable, library.defaultSort)
						end
					end
					if blankstring and (optionsTable[1] ~= blankstring or table.find(optionsTable, blankstring, 2)) then
						local exists = table.find(optionsTable, blankstring)
						if exists then
							for _ = 1, 35 do
								table.remove(optionsTable, exists)
								exists = table.find(optionsTable, blankstring)
								if not exists then
									break
								end
							end
						end
						table.insert(optionsTable, 1, blankstring)
					end
					optionCount = 0
					realDropdownHolderList.Parent = nil
					realDropdownHolder:ClearAllChildren()
					realDropdownHolderList.Parent = realDropdownHolder
					for _, v in next, optionsTable do
						optionCount = optionCount + 1
						local newOption = Instance_new("ImageLabel")
						local optionButton = Instance_new("TextButton")
						if selectedOption == v then
							selectedObjects[1] = newOption
							selectedObjects[2] = optionButton
						end
						newOption.Name = "Frame"
						newOption.Parent = realDropdownHolder
						local togged = (not multiselect and selectedOption == v) or (multiselect and table.find(selectedOption, v))
						newOption.BackgroundColor3 = (togged and library.colors.selectedOption) or library.colors.topGradient
						newOption.BorderSizePixel = 0
						newOption.Size = UDim2.fromOffset(202, 18)
						newOption.Image = "rbxassetid://2454009026"
						newOption.ImageColor3 = (togged and library.colors.unselectedOption) or library.colors.bottomGradient
						local stringed = tostring(v)
						optionButton.Name = stringed
						optionButton.Parent = newOption
						optionButton.AnchorPoint = Vector2.new(0.5, 0.5)
						optionButton.BackgroundColor3 = Color3.new(1, 1, 1)
						optionButton.BackgroundTransparency = 1
						optionButton.Position = UDim2.fromScale(0.5, 0.5)
						optionButton.Size = UDim2.new(1, -10, 1)
						optionButton.ZIndex = 5
						optionButton.Font = Enum.Font.Code
						optionButton.Text = (togged and (" " .. stringed)) or stringed
						optionButton.TextColor3 = (togged and library.colors.main) or library.colors.otherElementText
						optionButton.TextSize = 14
						optionButton.TextXAlignment = Enum.TextXAlignment.Left
						library.signals[1 + #library.signals] = optionButton.MouseButton1Click:Connect(function()
							if not library.colorpicker then
								restorezindex[newSection] = restorezindex[newSection] or newSection.ZIndex
								restorezindex[newDropdown] = restorezindex[newDropdown] or newDropdown.ZIndex
								restorezindex[sectionHolder] = restorezindex[sectionHolder] or sectionHolder.ZIndex
								if multiselect then
									local cloned = {unpack(selectedOption)}
									local togged = table.find(selectedOption, v)
									if togged then
										table.remove(selectedOption, togged)
									else
										selectedOption[1 + #selectedOption] = v
									end
									togged = table.find(selectedOption, v)
									optionButton.Text = (togged and (" " .. stringed)) or stringed
									newOption.BackgroundColor3 = (togged and library.colors.selectedOption) or library.colors.topGradient
									newOption.ImageColor3 = (togged and library.colors.unselectedOption) or library.colors.bottomGradient
									optionButton.TextColor3 = (togged and library.colors.main) or library.colors.otherElementText
									dropdownSelection.Text = (passed_multiselect == "string" and multiselect) or blankstring or "Select(s)"
									if callback then
										task.spawn(callback, selectedOption, cloned)
									end
									if togged then
										if addcallback then
											task.spawn(addcallback, v, selectedOption)
										end
									elseif delcallback then
										task.spawn(delcallback, v, selectedOption)
									end
									if modcallback then
										task.spawn(modcallback, v, togged, selectedOption)
									end
									if #selectedOption == 0 and clrcallback then
										task.spawn(clrcallback, selectedOption, cloned)
									end
									return
								else
									if selectedOption ~= v then
										local last_v = library_flags[flagName]
										selectedObjects[1].BackgroundColor3 = library.colors.topGradient
										selectedObjects[1].ImageColor3 = library.colors.bottomGradient
										selectedObjects[2].Text = selectedObjects[2].Name
										selectedObjects[2].TextColor3 = library.colors.otherElementText
										selectedOption = v
										dropdownSelection.Text = stringed
										selectedObjects[1] = newOption
										selectedObjects[2] = optionButton
										newOption.BackgroundColor3 = library.colors.selectedOption
										newOption.ImageColor3 = library.colors.unselectedOption
										optionButton.Text = " " .. stringed
										optionButton.TextColor3 = library.colors.main
										dropdownHolderFrame.Visible = false
										dropdownToggle.Rotation = 90
										dropdownEnabled = false
										newDropdown.ZIndex = 1
										colored_dropdown_BackgroundColor3[3] = "topGradient"
										colored_dropdown_BackgroundColor3[4] = nil
										colored_dropdown_ImageColor3[3] = "bottomGradient"
										colored_dropdown_ImageColor3[4] = nil
										tweenService:Create(dropdown, TweenInfo.new(0.35, library.configuration.easingStyle, library.configuration.easingDirection), {
											BackgroundColor3 = library.colors.topGradient,
											ImageColor3 = library.colors.bottomGradient
										}):Play()
										library_flags[flagName] = selectedOption
										if options.Location then
											options.Location[options.LocationFlag or flagName] = selectedOption
										end
										submenuOpen = nil
										showing = false
										if callback then
											task.spawn(callback, selectedOption, last_v)
										end
									else
										showing = false
										submenuOpen = nil
										dropdownToggle.Rotation = 90
										newDropdown.ZIndex = 1
										sectionHolder.ZIndex = 1
										colored_dropdown_BackgroundColor3[3] = "topGradient"
										colored_dropdown_BackgroundColor3[4] = nil
										colored_dropdown_ImageColor3[3] = "bottomGradient"
										colored_dropdown_ImageColor3[4] = nil
										tweenService:Create(dropdown, TweenInfo.new(0.35, library.configuration.easingStyle, library.configuration.easingDirection), {
											BackgroundColor3 = library.colors.topGradient,
											ImageColor3 = library.colors.bottomGradient
										}):Play()
										dropdownHolderFrame.Visible = false
									end
								end
								for ins, z in next, restorezindex do
									ins.ZIndex = z
								end
							end
						end)
						library.signals[1 + #library.signals] = optionButton.MouseEnter:Connect(function()
							tweenService:Create(newOption, TweenInfo.new(0.35, library.configuration.easingStyle, library.configuration.easingDirection), {
								BackgroundColor3 = library.colors.hoveredOptionTop,
								ImageColor3 = library.colors.hoveredOptionBottom
							}):Play()
						end)
						library.signals[1 + #library.signals] = optionButton.MouseLeave:Connect(function()
							local togged = (not multiselect and selectedOption == v) or (multiselect and table.find(selectedOption, v))
							tweenService:Create(newOption, TweenInfo.new(0.35, library.configuration.easingStyle, library.configuration.easingDirection), {
								BackgroundColor3 = (togged and library.colors.selectedOption) or library.colors.topGradient,
								ImageColor3 = (togged and library.colors.unselectedOption) or library.colors.bottomGradient
							}):Play()
						end)
						UpdateDropdownHolder()
					end
				end
				local precisionscrolling = nil
				local function display(dropdownEnabled)
					list = resolvelist()
					if dropdownEnabled then
						AddOptions(list)
						submenuOpen = dropdown
						dropdownToggle.Rotation = 270
						restorezindex[newSection] = restorezindex[newSection] or newSection.ZIndex
						restorezindex[newDropdown] = restorezindex[newDropdown] or newDropdown.ZIndex
						restorezindex[sectionHolder] = restorezindex[sectionHolder] or sectionHolder.ZIndex
						newSection.ZIndex = 50 + newSection.ZIndex
						newDropdown.ZIndex = 2
						sectionHolder.ZIndex = 2
						colored_dropdown_BackgroundColor3[3] = "main"
						colored_dropdown_BackgroundColor3[4] = 1.5
						colored_dropdown_ImageColor3[3] = "main"
						colored_dropdown_ImageColor3[4] = 2.5
						tweenService:Create(dropdown, TweenInfo.new(0.35, library.configuration.easingStyle, library.configuration.easingDirection), {
							BackgroundColor3 = darkenColor(library.colors.main, 1.5),
							ImageColor3 = darkenColor(library.colors.main, 2.5)
						}):Play()
						dropdownHolderFrame.Visible = true
						if not options.DisablePrecisionScrolling then
							local upkey = options.ScrollUpButton or library.scrollupbutton or shared.scrollupbutton or Enum.KeyCode.Up
							local downkey = options.ScrollDownButton or library.scrolldownbutton or shared.scrolldownbutton or Enum.KeyCode.Down
							precisionscrolling = (precisionscrolling and precisionscrolling:Disconnect() and nil) or userInputService.InputBegan:Connect(function(input)
								if input.UserInputType == Enum.UserInputType.Keyboard then
									local code = input.KeyCode
									local isup = code == upkey
									local isdown = code == downkey
									if isup or isdown then
										local txt = userInputService:GetFocusedTextBox()
										if not txt or txt == dropdownSelection then
											while wait_check() and userInputService:IsKeyDown(code) do
												realDropdownHolder.CanvasPosition = Vector2:new(math.clamp(realDropdownHolder.CanvasPosition.Y + ((isup and -5) or 5), 0, realDropdownHolder.AbsoluteCanvasSize.Y))
											end
										end
									end
								end
							end)
							library.signals[1 + #library.signals] = precisionscrolling
						end
					else
						submenuOpen = nil
						dropdownToggle.Rotation = 90
						colored_dropdown_BackgroundColor3[3] = "topGradient"
						colored_dropdown_BackgroundColor3[4] = nil
						colored_dropdown_ImageColor3[3] = "bottomGradient"
						colored_dropdown_ImageColor3[4] = nil
						tweenService:Create(dropdown, TweenInfo.new(0.35, library.configuration.easingStyle, library.configuration.easingDirection), {
							BackgroundColor3 = library.colors.topGradient,
							ImageColor3 = library.colors.bottomGradient
						}):Play()
						dropdownHolderFrame.Visible = false
						for ins, z in next, restorezindex do
							ins.ZIndex = z
						end
						precisionscrolling = (precisionscrolling and precisionscrolling:Disconnect() and nil) or nil
					end
					if not multiselect and (not next(list) or not table.find(list, library_flags[flagName])) then
						Set(list[1])
					end
					showing = dropdownEnabled
				end
				library.signals[1 + #library.signals] = newDropdown.InputEnded:Connect(function(input)
					if not library.colorpicker and input.UserInputType == Enum.UserInputType.MouseButton1 then
						showing = not showing
						display(showing)
					end
				end)
				library.signals[1 + #library.signals] = newDropdown.MouseEnter:Connect(function()
					colored_dropdown_BackgroundColor3[3] = "main"
					colored_dropdown_BackgroundColor3[4] = 1.5
					colored_dropdown_ImageColor3[3] = "main"
					colored_dropdown_ImageColor3[4] = 2.5
					tweenService:Create(dropdown, TweenInfo.new(0.25, library.configuration.easingStyle, library.configuration.easingDirection), {
						BackgroundColor3 = darkenColor(library.colors.main, 1.5),
						ImageColor3 = darkenColor(library.colors.main, 2.5)
					}):Play()
				end)
				library.signals[1 + #library.signals] = newDropdown.MouseLeave:Connect(function()
					if not dropdownEnabled then
						colored_dropdown_BackgroundColor3[3] = "topGradient"
						colored_dropdown_BackgroundColor3[4] = nil
						colored_dropdown_ImageColor3[3] = "bottomGradient"
						colored_dropdown_ImageColor3[4] = nil
						tweenService:Create(dropdown, TweenInfo.new(0.25, library.configuration.easingStyle, library.configuration.easingDirection), {
							BackgroundColor3 = library.colors.topGradient,
							ImageColor3 = library.colors.bottomGradient
						}):Play()
					end
				end)
				library.signals[1 + #library.signals] = dropdownToggle.MouseButton1Click:Connect(function()
					if not library.colorpicker then
						showing = not showing
						display(showing)
					end
				end)
				AddOptions(list)
				local default = library_flags[flagName]
				local function update()
					dropdownName, callback = options.Name or dropdownName, options.Callback
					local sstr = (passed_multiselect == "string" and multiselect) or (library_flags[flagName] and tostring(library_flags[flagName])) or (selectedOption and tostring(selectedOption)) or blankstring or "nil"
					if dropdownSelection.Text ~= sstr then
						dropdownSelection.Text = sstr
					end
					dropdownHeadline.Text = (dropdownName and tostring(dropdownName)) or "???"
					return sstr
				end
				local function validate(fallbackValue)
					if list and table.find(list, library_flags[flagName]) then
						update()
						return true
					end
					if fallbackValue ~= nil then
						if fallbackValue == "__DEFAULT" then
							fallbackValue = fallbackValue
						end
					else
						fallbackValue = list[1]
					end
					return Set((multiselect and {fallbackValue}) or fallbackValue)
				end
				local objectdata = {
					Options = options,
					Name = flagName,
					Flag = flagName,
					Type = "Dropdown",
					Default = default,
					Parent = sectionFunctions,
					Instance = dropdownSelection,
					Get = function()
						return library_flags[flagName]
					end,
					Set = Set,
					RawSet = ((multiselect and function(t, dat)
						if nil == dat and t ~= nil then
							dat = t
						end
						local lastv = library_flags[flagName]
						if not lastv or selectedOption ~= lastv then
							if lastv and type(lastv) == "table" then
								selectedOption = library_flags[flagName]
							else
								library_flags[flagName] = selectedOption
							end
							warn("Attempting to use new table for", flagName, " Please use :Set(), as setting through flags table may cause errors", debug.traceback(""))
							lastv = library_flags[flagName]
						end
						local cloned = {unpack(selectedOption)}
						if not dat then
							if #selectedOption ~= 0 then
								table.clear(selectedOption)
							end
							return selectedOption
						elseif type(dat) ~= "table" then
							warn("Expected table for argument #1 on Set for MultiSelect dropdown. Got", dat, debug.traceback(""))
							return selectedOption
						end
						for k = table.pack(unpack(dat)).n, 1, -1 do
							if dat[k] == nil then
								table.remove(dat, k)
							end
						end
						table.clear(selectedOption)
						for k, v in next, dat do
							selectedOption[k] = v
						end
						return selectedOption
					end) or function(t, str)
						if nil == str and t ~= nil then
							str = t
						end
						selectedOption = str
						library_flags[flagName] = str
						if options.Location then
							options.Location[options.LocationFlag or flagName] = str
						end
						update()
						return str
					end),
					Update = update,
					Reset = function()
						return Set(nil, default)
					end
				}
				function objectdata.UpdateList(t, listt, updateValues)
					if (nil == listt and t ~= nil) or (type(t) == "table" and type(listt) ~= "table") then
						listt, updateValues = t, listt
					end
					if listt == objectdata then
						listt = nil
					end
					resolvelist = getresolver(listt or options.List, options.Filter, options.Method)
					list = resolvelist()
					if updateValues then
						validate()
					end
					if showing then
						display(false)
						display(true)
					end
					return list
				end
				tabFunctions.Flags[flagName], sectionFunctions.Flags[flagName], elements[flagName] = objectdata, objectdata, objectdata
				return objectdata
			end
			sectionFunctions.AddDropDown = sectionFunctions.AddDropdown
			sectionFunctions.NewDropDown = sectionFunctions.AddDropdown
			sectionFunctions.NewDropdown = sectionFunctions.AddDropdown
			sectionFunctions.CreateDropdown = sectionFunctions.AddDropdown
			sectionFunctions.CreateDropdown = sectionFunctions.AddDropdown
			sectionFunctions.DropDown = sectionFunctions.AddDropdown
			sectionFunctions.Dropdown = sectionFunctions.AddDropdown
			sectionFunctions.DD = sectionFunctions.AddDropdown
			sectionFunctions.Dd = sectionFunctions.AddDropdown
			function sectionFunctions:AddColorpicker(options, ...)
				options = (options and type(options) == "string" and resolvevararg("Colorpicker", options, ...)) or options
				if options.Random == true then
					options.Value = "random"
				elseif options.Rainbow == true then
					options.Value = "rainbow"
				end
				local colorPickerName, presetColor, callback, flagName = assert(options.Name, "Missing Name for new colorpicker."), options.Value, options.Callback, options.Flag or (function()
					library.unnamedcolorpicker = 1 + (library.unnamedcolorpicker or 0)
					return "Colorpicker" .. tostring(library.unnamedcolorpicker)
				end)()
				if elements[flagName] ~= nil then
					warn(debug.traceback("Warning! Re-used flag '" .. flagName .. "'", 3))
				end
				local designers = options.__designer
				options.__designer = nil
				local rainbowColorMode = false
				if presetColor == "random" then
					presetColor = Color3.new(math.random(), math.random(), math.random())
				elseif presetColor == "rainbow" then
					presetColor = Color3.new(1, 1, 1)
					rainbowColorMode = true
				end
				local newColorPicker = Instance_new("Frame")
				local colorPicker = Instance_new("ImageLabel")
				local colorPickerInner = Instance_new("ImageLabel")
				local colorPickerHeadline = Instance_new("TextLabel")
				local colorPickerButton = Instance_new("TextButton")
				local colorPickerHolderFrame = Instance_new("ImageLabel")
				local colorPickerHolderInner = Instance_new("ImageLabel")
				local color = Instance_new("ImageLabel")
				local selectorColor = Instance_new("Frame")
				local hue = Instance_new("ImageLabel")
				local hueGradient = Instance_new("UIGradient")
				local selectorHue = Instance_new("Frame")
				local randomColor = Instance_new("ImageLabel")
				local randomColorInner = Instance_new("ImageLabel")
				local randomColorButton = Instance_new("ImageButton")
				local hexInputBox = Instance_new("TextBox")
				local hexInput = Instance_new("ImageLabel")
				local hexInputInner = Instance_new("ImageLabel")
				local rainbow = Instance_new("ImageLabel")
				local rainbowInner = Instance_new("ImageLabel")
				local rainbowButton = Instance_new("ImageButton")
				local startingColor = presetColor or Color3.new(1, 1, 1)
				local colorPickerEnabled = false
				local colorH, colorS, colorV = 1, 1, 1
				local colorInput, hueInput = nil, nil
				local oldBackgroundColor = Color3.new()
				local oldImageColor = oldBackgroundColor
				local oldColor = oldBackgroundColor
				local rainbowColorValue = 0
				newColorPicker.Name = "newColorPicker"
				newColorPicker.Parent = sectionHolder
				newColorPicker.BackgroundColor3 = Color3.new(1, 1, 1)
				newColorPicker.BackgroundTransparency = 1
				newColorPicker.Size = UDim2.new(1, 0, 0, 19)
				colorPicker.Name = "colorPicker"
				colorPicker.Parent = newColorPicker
				colorPicker.Active = true
				colorPicker.BackgroundColor3 = library.colors.topGradient
				local colored_colorPicker_BackgroundColor3 = {colorPicker, "BackgroundColor3", "topGradient"}
				colored[1 + #colored] = colored_colorPicker_BackgroundColor3
				colorPicker.BorderColor3 = library.colors.elementBorder
				colored[1 + #colored] = {colorPicker, "BorderColor3", "elementBorder"}
				colorPicker.Position = UDim2.fromScale(0.842, 0.113)
				colorPicker.Selectable = true
				colorPicker.Size = UDim2.fromOffset(24, 12)
				colorPicker.Image = "rbxassetid://2454009026"
				colorPicker.ImageColor3 = library.colors.bottomGradient
				local colored_colorPicker_ImageColor3 = {colorPicker, "ImageColor3", "bottomGradient"}
				colored[1 + #colored] = colored_colorPicker_ImageColor3
				colorPickerInner.Name = "colorPickerInner"
				colorPickerInner.Parent = colorPicker
				colorPickerInner.Active = true
				colorPickerInner.AnchorPoint = Vector2.new(0.5, 0.5)
				colorPickerInner.BorderColor3 = library.colors.elementBorder
				colored[1 + #colored] = {colorPickerInner, "BorderColor3", "elementBorder"}
				colorPickerInner.Position = UDim2.fromScale(0.5, 0.5)
				colorPickerInner.Selectable = true
				colorPickerInner.Size = UDim2.new(1, -4, 1, -4)
				colorPickerInner.Image = "rbxassetid://2454009026"
				colorPickerInner.BackgroundColor3 = darkenColor(startingColor, 1.5)
				colorPickerInner.ImageColor3 = darkenColor(startingColor, 2.5)
				colorPickerHeadline.Name = "colorPickerHeadline"
				colorPickerHeadline.Parent = newColorPicker
				colorPickerHeadline.BackgroundColor3 = Color3.new(1, 1, 1)
				colorPickerHeadline.BackgroundTransparency = 1
				colorPickerHeadline.Position = UDim2.fromScale(0.034, 0.113)
				colorPickerHeadline.Size = UDim2.fromOffset(173, 11)
				colorPickerHeadline.Font = Enum.Font.Code
				colorPickerHeadline.Text = colorPickerName or "???"
				colorPickerHeadline.TextColor3 = library.colors.elementText
				colored[1 + #colored] = {colorPickerHeadline, "TextColor3", "elementText"}
				colorPickerHeadline.TextSize = 14
				colorPickerHeadline.TextXAlignment = Enum.TextXAlignment.Left
				colorPickerButton.Name = "colorPickerButton"
				colorPickerButton.Parent = newColorPicker
				colorPickerButton.BackgroundColor3 = Color3.new(1, 1, 1)
				colorPickerButton.BackgroundTransparency = 1
				colorPickerButton.Size = UDim2.fromScale(1, 1)
				colorPickerButton.ZIndex = 5
				colorPickerButton.Font = Enum.Font.SourceSans
				colorPickerButton.Text = ""
				colorPickerButton.TextColor3 = Color3.new()
				colorPickerButton.TextSize = 14
				colorPickerButton.TextTransparency = 1
				colorPickerButton.BorderColor3 = library.colors.elementBorder
				local colored_colorPickerButton_BorderColor3 = {colorPickerButton, "BorderColor3", "elementBorder"}
				colored[1 + #colored] = colored_colorPickerButton_BorderColor3
				local function UpdateColorPicker(force, rainbsow)
					local last_vv = library_flags[flagName]
					local newColor = force or Color3.fromHSV(colorH, colorS, colorV)
					if not force then
						colorH, colorS, colorV = newColor:ToHSV()
					end
					colorPickerInner.BackgroundColor3 = darkenColor(newColor, 1.5)
					colorPickerInner.ImageColor3 = darkenColor(newColor, 2.5)
					color.BackgroundColor3 = Color3.fromHSV(colorH, 1, 1)
					library_flags[flagName] = newColor
					if options.Location then
						options.Location[options.LocationFlag or flagName] = newColor
					end
					hexInputBox.Text = Color3ToHex(newColor)
					if force then
						color.BackgroundColor3 = force
						selectorColor.Position = UDim2.new(force and select(3, Color3.toHSV(force)))
					end
					local pos = 1 - (Color3.toHSV(newColor))
					local scalex = selectorHue.Position.X.Scale
					if scalex ~= pos and not ((pos == 0 or pos == 1) and (scalex == 1 or scalex == 0)) then
						selectorHue.Position = UDim2.new(pos)
					end
					if callback and last_vv ~= newColor then
						task.spawn(callback, newColor, last_vv, rainbsow)
					end
				end
				library.signals[1 + #library.signals] = colorPickerButton.MouseButton1Click:Connect(function()
					if submenuOpen == colorPicker or submenuOpen == nil then
						colorPickerEnabled = not colorPickerEnabled
						library.colorpicker = colorPickerEnabled
						colorPickerHolderFrame.Visible = colorPickerEnabled
						if colorPickerEnabled then
							for _, v in next, colorpickerconflicts do
								v.Visible = false
							end
							submenuOpen = colorPicker
							newColorPicker.ZIndex = 2
							newSection.ZIndex = 100 + newSection.ZIndex
							colorPickerButton.BorderColor3 = library.colors.main
							colored_colorPickerButton_BorderColor3[3] = "main"
							UpdateColorPicker()
						else
							for _, v in next, colorpickerconflicts do
								v.Visible = true
							end
							submenuOpen = nil
							newColorPicker.ZIndex = 0
							newSection.ZIndex = newSection.ZIndex - 100
							colorPickerButton.BorderColor3 = library.colors.elementBorder
							colored_colorPickerButton_BorderColor3[3] = "elementBorder"
						end
					end
				end)
				colorPickerHolderFrame.Name = "colorPickerHolderFrame"
				colorPickerHolderFrame.Parent = newColorPicker
				colorPickerHolderFrame.Active = true
				colorPickerHolderFrame.BackgroundColor3 = library.colors.topGradient
				colored[1 + #colored] = {colorPickerHolderFrame, "BackgroundColor3", "topGradient"}
				colorPickerHolderFrame.BorderColor3 = library.colors.elementBorder
				colored[1 + #colored] = {colorPickerHolderFrame, "BorderColor3", "elementBorder"}
				colorPickerHolderFrame.Selectable = true
				colorPickerHolderFrame.Position = UDim2.fromScale(0.025, 1.012)
				colorPickerHolderFrame.Size = UDim2.fromOffset(206, 250)
				if math.ceil(colorPickerHolderFrame.AbsolutePosition.Y + colorPickerHolderFrame.AbsoluteSize.Y) > floor(newTabHolder.AbsoluteSize.Y + newTabHolder.AbsolutePosition.Y) then
					colorPickerHolderFrame.Position = UDim2.new(0.025, 0, 1.012, -colorPickerHolderFrame.AbsoluteSize.Y - colorPickerButton.AbsoluteSize.Y - 2)
				end
				colorPickerHolderFrame.Visible = false
				colorPickerHolderFrame.Image = "rbxassetid://2454009026"
				colorPickerHolderFrame.ImageColor3 = library.colors.bottomGradient
				colored[1 + #colored] = {colorPickerHolderFrame, "ImageColor3", "bottomGradient"}
				colorPickerHolderInner.Name = "colorPickerHolderInner"
				colorPickerHolderInner.Parent = colorPickerHolderFrame
				colorPickerHolderInner.Active = true
				colorPickerHolderInner.AnchorPoint = Vector2.new(0.5, 0.5)
				colorPickerHolderInner.BackgroundColor3 = library.colors.topGradient
				colored[1 + #colored] = {colorPickerHolderInner, "BackgroundColor3", "topGradient"}
				colorPickerHolderInner.BorderColor3 = library.colors.elementBorder
				colored[1 + #colored] = {colorPickerHolderInner, "BorderColor3", "elementBorder"}
				colorPickerHolderInner.Position = UDim2.fromScale(0.5, 0.5)
				colorPickerHolderInner.Selectable = true
				colorPickerHolderInner.Size = UDim2.new(1, -4, 1, -4)
				colorPickerHolderInner.Image = "rbxassetid://2454009026"
				colorPickerHolderInner.ImageColor3 = library.colors.bottomGradient
				colored[1 + #colored] = {colorPickerHolderInner, "ImageColor3", "bottomGradient"}
				color.Name = "color"
				color.Parent = colorPickerHolderInner
				color.BackgroundColor3 = startingColor
				color.BorderSizePixel = 0
				color.Position = UDim2.fromOffset(5, 5)
				color.Size = UDim2.new(1, -10, 0, 192)
				color.Image = "rbxassetid://4155801252"
				selectorColor.Name = "selectorColor"
				selectorColor.Parent = color
				selectorColor.AnchorPoint = Vector2.new(0.5, 0.5)
				selectorColor.BackgroundColor3 = Color3.fromRGB(144, 144, 144)
				selectorColor.BorderColor3 = Color3.fromRGB(69, 65, 70)
				selectorColor.Position = UDim2.new(startingColor and select(3, Color3.toHSV(startingColor)))
				selectorColor.Size = UDim2.fromOffset(4, 4)
				hue.Name = "hue"
				hue.Parent = colorPickerHolderInner
				hue.BackgroundColor3 = Color3.new(1, 1, 1)
				hue.BorderSizePixel = 0
				hue.Position = UDim2.fromOffset(5, 202)
				hue.Size = UDim2.new(1, -10, 0, 14)
				hue.Image = "rbxassetid://3570695787"
				hue.ScaleType = Enum.ScaleType.Slice
				hue.SliceScale = 0.01
				hueGradient.Color = ColorSequence.new({ColorSequenceKeypoint.new(0, Color3.fromRGB(255, 0, 4)), ColorSequenceKeypoint.new(0.17, Color3.fromRGB(235, 7, 255)), ColorSequenceKeypoint.new(0.33, Color3:fromRGB(9, 189)), ColorSequenceKeypoint.new(0.5, Color3:fromRGB(193, 196)), ColorSequenceKeypoint.new(0.66, Color3:new(1)), ColorSequenceKeypoint.new(0.84, Color3.fromRGB(255, 247)), ColorSequenceKeypoint.new(1, Color3.new(1))})
				hueGradient.Name = "hueGradient"
				hueGradient.Parent = hue
				selectorHue.Name = "selectorHue"
				selectorHue.Parent = hue
				selectorHue.BackgroundColor3 = Color3:fromRGB(125, 255)
				selectorHue.BackgroundTransparency = 0.2
				selectorHue.BorderColor3 = Color3:fromRGB(84, 91)
				selectorHue.Position = UDim2.new(1 - (Color3.toHSV(startingColor)))
				selectorHue.Size = UDim2:new(2, 1)
				hexInput.Name = "hexInput"
				hexInput.Parent = colorPickerHolderInner
				hexInput.Active = true
				hexInput.BackgroundColor3 = library.colors.topGradient
				colored[1 + #colored] = {hexInput, "BackgroundColor3", "topGradient"}
				hexInput.BorderColor3 = library.colors.elementBorder
				colored[1 + #colored] = {hexInput, "BorderColor3", "elementBorder"}
				hexInput.Position = UDim2.fromOffset(5, 223)
				hexInput.Selectable = true
				hexInput.Size = UDim2.fromOffset(150, 18)
				hexInput.Image = "rbxassetid://2454009026"
				hexInput.ImageColor3 = library.colors.bottomGradient
				colored[1 + #colored] = {hexInput, "ImageColor3", "bottomGradient"}
				hexInputInner.Name = "hexInputInner"
				hexInputInner.Parent = hexInput
				hexInputInner.Active = true
				hexInputInner.AnchorPoint = Vector2.new(0.5, 0.5)
				hexInputInner.BackgroundColor3 = library.colors.topGradient
				colored[1 + #colored] = {hexInputInner, "BackgroundColor3", "topGradient"}
				hexInputInner.BorderColor3 = library.colors.elementBorder
				colored[1 + #colored] = {hexInputInner, "BorderColor3", "elementBorder"}
				hexInputInner.Position = UDim2.fromScale(0.5, 0.5)
				hexInputInner.Selectable = true
				hexInputInner.Size = UDim2.new(1, -4, 1, -4)
				hexInputInner.Image = "rbxassetid://2454009026"
				hexInputInner.ImageColor3 = library.colors.bottomGradient
				colored[1 + #colored] = {hexInputInner, "ImageColor3", "bottomGradient"}
				hexInputBox.Name = "hexInputBox"
				hexInputBox.Parent = hexInput
				hexInputBox.BackgroundColor3 = Color3.new(1, 1, 1)
				hexInputBox.BackgroundTransparency = 1
				hexInputBox.Size = UDim2.fromScale(1, 1)
				hexInputBox.ZIndex = 5
				hexInputBox.Font = Enum.Font.Code
				hexInputBox.PlaceholderText = "Hex Input"
				hexInputBox.Text = Color3ToHex(startingColor)
				hexInputBox.TextColor3 = library.colors.elementText
				colored[1 + #colored] = {hexInputBox, "TextColor3", "elementText"}
				hexInputBox.TextSize = 14
				hexInputBox.ClearTextOnFocus = false
				randomColor.Name = "randomColor"
				randomColor.Parent = colorPickerHolderInner
				randomColor.Active = true
				randomColor.BackgroundColor3 = library.colors.topGradient
				colored[1 + #colored] = {randomColor, "BackgroundColor3", "topGradient"}
				randomColor.BorderColor3 = library.colors.elementBorder
				colored[1 + #colored] = {randomColor, "BorderColor3", "elementBorder"}
				randomColor.Position = UDim2.fromOffset(158, 223)
				randomColor.Selectable = true
				randomColor.Size = UDim2.fromOffset(18, 18)
				randomColor.Image = "rbxassetid://2454009026"
				randomColor.ImageColor3 = library.colors.bottomGradient
				colored[1 + #colored] = {randomColor, "ImageColor3", "bottomGradient"}
				randomColorInner.Name = "randomColorInner"
				randomColorInner.Parent = randomColor
				randomColorInner.Active = true
				randomColorInner.AnchorPoint = Vector2.new(0.5, 0.5)
				randomColorInner.BackgroundColor3 = library.colors.topGradient
				colored[1 + #colored] = {randomColorInner, "BackgroundColor3", "topGradient"}
				randomColorInner.BorderColor3 = library.colors.elementBorder
				colored[1 + #colored] = {randomColorInner, "BorderColor3", "elementBorder"}
				randomColorInner.Position = UDim2.fromScale(0.5, 0.5)
				randomColorInner.Selectable = true
				randomColorInner.Size = UDim2.new(1, -4, 1, -4)
				randomColorInner.Image = "rbxassetid://2454009026"
				randomColorInner.ImageColor3 = library.colors.bottomGradient
				colored[1 + #colored] = {randomColorInner, "ImageColor3", "bottomGradient"}
				randomColorButton.Name = "randomColorButton"
				randomColorButton.Parent = randomColor
				randomColorButton.BackgroundColor3 = Color3.new(1, 1, 1)
				randomColorButton.BackgroundTransparency = 1
				randomColorButton.Size = UDim2.fromScale(1, 1)
				randomColorButton.ZIndex = 5
				randomColorButton.Image = "rbxassetid://7484765651"
				rainbow.Name = "rainbow"
				rainbow.Parent = colorPickerHolderInner
				rainbow.Active = true
				rainbow.BackgroundColor3 = library.colors.topGradient
				colored[1 + #colored] = {rainbow, "BackgroundColor3", "topGradient"}
				rainbow.BorderColor3 = library.colors.elementBorder
				colored[1 + #colored] = {rainbow, "BorderColor3", "elementBorder"}
				rainbow.Position = UDim2.fromOffset(158 + 18 + 4, 223)
				rainbow.Selectable = true
				rainbow.Size = UDim2.fromOffset(18, 18)
				rainbow.Image = "rbxassetid://2454009026"
				rainbow.ImageColor3 = library.colors.bottomGradient
				colored[1 + #colored] = {rainbow, "ImageColor3", "bottomGradient"}
				rainbowInner.Name = "rainbowInner"
				rainbowInner.Parent = randomColor
				rainbowInner.Active = true
				rainbowInner.AnchorPoint = Vector2.new(0.5, 0.5)
				rainbowInner.BackgroundColor3 = library.colors.topGradient
				colored[1 + #colored] = {rainbowInner, "BackgroundColor3", "topGradient"}
				rainbowInner.BorderColor3 = library.colors.elementBorder
				colored[1 + #colored] = {rainbowInner, "BorderColor3", "elementBorder"}
				rainbowInner.Position = UDim2.fromScale(0.5, 0.5)
				rainbowInner.Selectable = true
				rainbowInner.Size = UDim2.new(1, -4, 1, -4)
				rainbowInner.Image = "rbxassetid://2454009026"
				rainbowInner.ImageColor3 = library.colors.bottomGradient
				colored[1 + #colored] = {rainbowInner, "ImageColor3", "bottomGradient"}
				rainbowButton.Name = "rainbowButton"
				rainbowButton.Parent = rainbow
				rainbowButton.BackgroundColor3 = Color3.new(1, 1, 1)
				rainbowButton.BackgroundTransparency = 1
				rainbowButton.Size = UDim2.fromScale(1, 1)
				rainbowButton.ZIndex = 5
				rainbowButton.Image = "rbxassetid://7484772919"
				local indexwith = (designers and "rainbows") or "rainbowsg"
				local function setrainbow(t, rainbowColorMod)
					if nil == rainbowColorMod and t ~= nil then
						rainbowColorMod = t
					end
					if rainbowColorMod == nil or type(rainbowColorMod) ~= "boolean" then
						rainbowColorMode = not rainbowColorMode
					else
						rainbowColorMode = rainbowColorMod
					end
					if colorInput then
						colorInput = (colorInput:Disconnect() and nil) or nil
					end
					if hueInput then
						hueInput = (hueInput:Disconnect() and nil) or nil
					end
					pcall(function()
						if destroyrainbows and library.rainbows <= 0 then
							destroyrainbows = nil
						end
						if destroyrainbowsg and library.rainbowsg <= 0 then
							destroyrainbowsg = nil
						end
					end)
					if rainbowColorMode then
						pcall(function()
							if not library.rainbowflags[flagName] then
								library[indexwith] = 1 + library[indexwith]
							end
							library.rainbowflags[flagName] = true
							oldImageColor = colorPickerInner.ImageColor3
							oldBackgroundColor = colorPickerInner.BackgroundColor3
							oldColor = color.BackgroundColor3
							pcall(function()
								local common_float = 1 / 255
								while wait_check() and rainbowColorMode and (options.Value == "rainbow" or ((not designers and not destroyrainbowsg) or (designers and not destroyrainbows))) do
									rainbowColorValue = common_float + rainbowColorValue
									if rainbowColorValue > 1 then
										rainbowColorValue = 0
									end
									colorH = rainbowColorValue
									UpdateColorPicker(Color3.fromHSV(rainbowColorValue, 1, 1), true)
								end
							end)
						end)
						pcall(function()
							rainbowColorMode = nil
							if library.rainbowflags[flagName] then
								library[indexwith] = library[indexwith] - 1
							end
							library.rainbowflags[flagName] = nil
						end)
					end
					UpdateColorPicker(library_flags[flagName])
				end
				library.signals[1 + #library.signals] = randomColorButton.MouseButton1Click:Connect(function()
					if rainbowColorMode then
						setrainbow(false)
					end
					UpdateColorPicker(Color3.fromRGB(math.random(0, 255), math.random(0, 255), math.random(0, 255)))
				end)
				library.signals[1 + #library.signals] = rainbowButton.MouseButton1Click:Connect(setrainbow)
				sectionFunctions:Update()
				library.signals[1 + #library.signals] = newColorPicker.MouseEnter:Connect(function()
					tweenService:Create(colorPicker, TweenInfo.new(0.25, library.configuration.easingStyle, library.configuration.easingDirection), {
						BackgroundColor3 = darkenColor(library.colors.main, 1.5),
						ImageColor3 = darkenColor(library.colors.main, 2.5)
					}):Play()
					colored_colorPicker_BackgroundColor3[3] = "main"
					colored_colorPicker_BackgroundColor3[4] = 1.5
					colored_colorPicker_ImageColor3[3] = "main"
					colored_colorPicker_ImageColor3[4] = 2.5
				end)
				library.signals[1 + #library.signals] = newColorPicker.MouseLeave:Connect(function()
					if not colorPickerEnabled then
						tweenService:Create(colorPicker, TweenInfo.new(0.25, library.configuration.easingStyle, library.configuration.easingDirection), {
							BackgroundColor3 = library.colors.topGradient,
							ImageColor3 = library.colors.bottomGradient
						}):Play()
						colored_colorPicker_BackgroundColor3[3] = "topGradient"
						colored_colorPicker_BackgroundColor3[4] = nil
						colored_colorPicker_ImageColor3[3] = "bottomGradient"
						colored_colorPicker_ImageColor3[4] = nil
					end
				end)
				hexInputBox.FocusLost:Connect(function()
					if #hexInputBox.Text > 5 then
						local last_vv = library_flags[flagName]
						local not_fucked, clr = pcall(Color3FromHex, hexInputBox.Text)
						UpdateColorPicker((not_fucked and clr) or last_vv)
					end
				end)
				colorH = 1 - (math.clamp(selectorHue.AbsolutePosition.X - hue.AbsolutePosition.X, 0, hue.AbsoluteSize.X) / hue.AbsoluteSize.X)
				colorS = (math.clamp(selectorColor.AbsolutePosition.X - color.AbsolutePosition.X, 0, color.AbsoluteSize.X) / color.AbsoluteSize.X)
				colorV = 1 - (math.clamp(selectorColor.AbsolutePosition.Y - color.AbsolutePosition.Y, 0, color.AbsoluteSize.Y) / color.AbsoluteSize.Y)
				library.signals[1 + #library.signals] = color.InputBegan:Connect(function(input)
					if input.UserInputType == Enum.UserInputType.MouseButton1 then
						isDraggingSomething = true
						colorInput = (colorInput and colorInput:Disconnect() and nil) or runService.RenderStepped:Connect(function()
							local colorX = (math.clamp(mouse.X - color.AbsolutePosition.X, 0, color.AbsoluteSize.X) / color.AbsoluteSize.X)
							local colorY = (math.clamp(mouse.Y - color.AbsolutePosition.Y, 0, color.AbsoluteSize.Y) / color.AbsoluteSize.Y)
							selectorColor.Position = UDim2.fromScale(colorX, colorY)
							colorS = colorX
							colorV = 1 - colorY
							UpdateColorPicker()
						end)
						library.signals[1 + #library.signals] = colorInput
					end
				end)
				library.signals[1 + #library.signals] = color.InputEnded:Connect(function(input)
					if input.UserInputType == Enum.UserInputType.MouseButton1 then
						if colorInput then
							isDraggingSomething = false
							colorInput:Disconnect()
						end
					end
				end)
				library.signals[1 + #library.signals] = hue.InputBegan:Connect(function(input)
					if input.UserInputType == Enum.UserInputType.MouseButton1 then
						if hueInput then
							hueInput:Disconnect()
						end
						isDraggingSomething = true
						hueInput = runService.RenderStepped:Connect(function()
							local hueX = math.clamp(mouse.X - hue.AbsolutePosition.X, 0, hue.AbsoluteSize.X) / hue.AbsoluteSize.X
							selectorHue.Position = UDim2.new(hueX)
							colorH = 1 - hueX
							UpdateColorPicker()
						end)
						library.signals[1 + #library.signals] = hueInput
					end
				end)
				library.signals[1 + #library.signals] = hue.InputEnded:Connect(function(input)
					if hueInput and input.UserInputType == Enum.UserInputType.MouseButton1 then
						isDraggingSomething = false
						hueInput:Disconnect()
					end
				end)
				if rainbowColorMode then
					spawn(function()
						rainbowColorMode = nil
						setrainbow(true)
					end)
				end
				local function Set(t, clr)
					if clr == nil and t ~= nil then
						clr = t
					end
					if clr == "rainbow" then
						if not rainbowColorMode then
							task.spawn(setrainbow, true)
						end
						return
					elseif clr == "random" then
						clr = Color3.new(math.random(), math.random(), math.random())
					elseif type(clr) == "string" and tonumber(clr, 16) then
						clr = Color3FromHex(clr)
					end
					task.spawn(setrainbow, false)
					local last_v = library_flags[flagName]
					library_flags[flagName] = clr
					if options.Location then
						options.Location[options.LocationFlag or flagName] = clr
					end
					color.BackgroundColor3 = clr
					selectorColor.Position = UDim2.new(clr and select(3, Color3.toHSV(clr)))
					selectorHue.Position = UDim2.new(1 - (Color3.toHSV(clr)))
					colorPickerInner.BackgroundColor3 = darkenColor(clr, 1.5)
					colorPickerInner.ImageColor3 = darkenColor(clr, 2.5)
					hexInputBox.Text = Color3ToHex(clr)
					colorH, colorS, colorV = Color3.toHSV(clr)
					if callback and (last_v ~= clr or options.AllowDuplicateCalls) then
						task.spawn(callback, clr, last_v)
					end
					return clr
				end
				if presetColor ~= nil then
					Set(presetColor)
				else
					library_flags[flagName] = startingColor
					if options.Location then
						options.Location[options.LocationFlag or flagName] = startingColor
					end
				end
				local default = options.Value or startingColor or library_flags[flagName]
				local function update()
					colorPickerName, callback = options.Name or colorPickerName, options.Callback
					local clr = library_flags[flagName]
					color.BackgroundColor3 = clr
					selectorColor.Position = UDim2.new(clr and select(3, Color3.toHSV(clr)))
					selectorHue.Position = UDim2.new(1 - (Color3.toHSV(clr)))
					colorPickerInner.BackgroundColor3 = darkenColor(clr, 1.5)
					colorPickerInner.ImageColor3 = darkenColor(clr, 2.5)
					hexInputBox.Text = Color3ToHex(clr)
					colorPickerHeadline.Text = colorPickerName or "???"
					return clr
				end
				local objectdata = {
					Options = options,
					Name = flagName,
					Flag = flagName,
					Type = "Colorpicker",
					Default = default,
					Parent = sectionFunctions,
					Instance = newColorPicker,
					SetRainbow = setrainbow,
					Get = function()
						return library_flags[flagName]
					end,
					GetRainbow = function()
						return rainbowColorMode
					end,
					Set = Set,
					RawSet = function(t, clr)
						if clr == nil and t ~= nil then
							clr = t
						end
						if clr == "rainbow" then
							if not rainbowColorMode then
								task.spawn(setrainbow, true)
							end
							return clr
						elseif clr == "random" then
							clr = Color3.new(math.random(), math.random(), math.random())
						elseif clr and type(clr) == "string" and tonumber(clr, 16) then
							clr = Color3FromHex(clr)
						end
						task.spawn(setrainbow, false)
						library_flags[flagName] = clr
						if options.Location then
							options.Location[options.LocationFlag or flagName] = clr
						end
						return clr
					end,
					Update = update,
					Reset = function()
						return Set(nil, default)
					end
				}
				tabFunctions.Flags[flagName], sectionFunctions.Flags[flagName], elements[flagName] = objectdata, objectdata, objectdata
				return objectdata
			end
			sectionFunctions.AddColorPicker = sectionFunctions.AddColorpicker
			sectionFunctions.NewColorpicker = sectionFunctions.AddColorpicker
			sectionFunctions.NewColorPicker = sectionFunctions.AddColorpicker
			sectionFunctions.CreateColorPicker = sectionFunctions.AddColorpicker
			sectionFunctions.CreateColorpicker = sectionFunctions.AddColorpicker
			sectionFunctions.ColorPicker = sectionFunctions.AddColorpicker
			sectionFunctions.Colorpicker = sectionFunctions.AddColorpicker
			sectionFunctions.Cp = sectionFunctions.AddColorpicker
			sectionFunctions.CP = sectionFunctions.AddColorpicker
			function sectionFunctions:UpdateAll()
				local target = self or sectionFunctions
				if target and type(target) == "table" and target.Flags then
					for _, e in next, target.Flags do
						if e and type(e) == "table" and e.Update then
							pcall(e.Update)
						end
					end
				end
			end
			return sectionFunctions
		end
		tabFunctions.AddSection = tabFunctions.CreateSection
		tabFunctions.NewSection = tabFunctions.CreateSection
		tabFunctions.Section = tabFunctions.CreateSection
		tabFunctions.Sec = tabFunctions.CreateSection
		tabFunctions.S = tabFunctions.CreateSection
		function tabFunctions:UpdateAll()
			local target = self or tabFunctions
			if target and type(target) == "table" and target.Flags then
				for _, e in next, target.Flags do
					if e and type(e) == "table" and e.Update then
						pcall(e.Update)
					end
				end
			end
		end
		return tabFunctions
	end
	windowFunctions.AddTab = windowFunctions.CreateTab
	windowFunctions.NewTab = windowFunctions.CreateTab
	windowFunctions.Tab = windowFunctions.CreateTab
	windowFunctions.T = windowFunctions.CreateTab
	function windowFunctions:CreateDesigner(options, ...)
		options = (options and type(options) == "string" and resolvevararg("Tab", options, ...)) or options
		assert(shared.bypasstablimit or library.Designer == nil, "Designer already exists")
		options = options or {}
		options.Image = options.Image or 7483871523
		options.LastTab = true
		local designer = windowFunctions:CreateTab(options)
		local colorsection = designer:CreateSection({
			Name = "Colors"
		})
		local backgroundsection = designer:CreateSection({
			Name = "Background",
			Side = "right"
		})
		local detailssection = designer:CreateSection({
			Name = "Info"
		})
		local filessection = designer:CreateSection({
			Name = "Profiles",
			Side = "right"
		})
		local settingssection = designer:CreateSection({
			Name = "Settings",
			Side = "right"
		})
		local designerelements = {}
		library.designerelements = designerelements
		for _, v in next, {{"Main", "main"}, {"Background", "background"}, {"Outer Border", "outerBorder"}, {"Inner Border", "innerBorder"}, {"Top Gradient", "topGradient"}, {"Bottom Gradient", "bottomGradient"}, {"Section Background", "sectionBackground"}, {"Section", "section"}, {"Element Text", "elementText"}, {"Other Element Text", "otherElementText"}, {"Tab Text", "tabText"}, {"Element Border", "elementBorder"}, {"Selected Option", "selectedOption"}, {"Unselected Option", "unselectedOption"}, {"Hovered Option Top", "hoveredOptionTop"}, {"Unhovered Option Top", "unhoveredOptionTop"}, {"Hovered Option Bottom", "hoveredOptionBottom"}, {"Unhovered Option Bottom", "unhoveredOptionBottom"}} do
			local nam, codename = v[1], v[2]
			local cflag = "__Designer.Colors." .. codename
			designerelements[codename] = {
				Return = colorsection:AddColorpicker({
					Name = nam,
					Flag = cflag,
					Value = library.colors[codename],
					Callback = function(v, y)
						library.colors[codename] = v or y
					end,
					__designer = 1
				}),
				Flag = cflag
			}
		end
		local flags = {}
		local persistoptions = {
			Name = "Workspace Profile",
			Flag = "__Designer.Background.WorkspaceProfile",
			Flags = true,
			Suffix = "Config",
			Workspace = library.WorkspaceName or "Unnamed Workspace",
			Desginer = true
		}
		local daaata = {{"AddTextbox", "__Designer.Textbox.ImageAssetID", backgroundsection, {
			Name = "Image Asset ID",
			Placeholder = "rbxassetid://4427304036",
			Flag = "__Designer.Background.ImageAssetID",
			Value = "rbxassetid://4427304036",
			Callback = updatecolorsnotween
		}}, {"AddColorpicker", "__Designer.Colorpicker.ImageColor", backgroundsection, {
			Name = "Image Color",
			Flag = "__Designer.Background.ImageColor",
			Value = Color3.new(1, 1, 1),
			Callback = updatecolorsnotween,
			__designer = 1
		}}, {"AddSlider", "__Designer.Slider.ImageTransparency", backgroundsection, {
			Name = "Image Transparency",
			Flag = "__Designer.Background.ImageTransparency",
			Value = 95,
			Min = 0,
			Max = 100,
			Format = "Image Transparency: %s%%",
			Textbox = true,
			Callback = updatecolorsnotween
		}}, {"AddToggle", "__Designer.Toggle.UseBackgroundImage", backgroundsection, {
			Name = "Use Background Image",
			Flag = "__Designer.Background.UseBackgroundImage",
			Value = true,
			Callback = updatecolorsnotween
		}}, {"AddPersistence", "__Designer.Persistence.ThemeFile", filessection, {
			Name = "Theme Profile",
			Flag = "__Designer.Files.ThemeFile",
			Workspace = "Function Lib Themes",
			Flags = flags,
			Suffix = "Theme",
			Desginer = true
		}}, {"AddTextbox", "__Designer.Textbox.WorkspaceName", filessection, {
			Name = "Workspace Name",
			Value = library.WorkspaceName or "Unnamed Workspace",
			Flag = "__Designer.Files.WorkspaceFile",
			Callback = function(n, o)
				persistoptions.Workspace = n or o
			end
		}}, {"AddPersistence", "__Designer.Persistence.WorkspaceProfile", filessection, persistoptions}, {"AddButton", "__Designer.Button.TerminateGUI", settingssection, {{
			Name = "Terminate GUI",
			Callback = library.unload
		}, {
			Name = "Reset GUI",
			Callback = resetall
		}}}, {"AddKeybind", "__Designer.Keybind.ShowHideKey", settingssection, {
			Name = "Show/Hide Key",
			Location = library.configuration,
			Flag = "__Designer.Settings.ShowHideKey",
			LocationFlag = "hideKeybind",
			Value = library.configuration.hideKeybind,
			Callback = function()
				lasthidebing = os.clock()
			end
		}}}
		if setclipboard and daaata[8] then
			local common_table = daaata[8][4]
			if common_table then
				common_table[1 + #common_table] = {
					Name = "Join Discord",
					Callback = function()
						local http = game:GetService('HttpService') 
						local req =  http_request or request or HttpPost or syn.request 
						if req then
							req({
								Url = 'http://127.0.0.1:6463/rpc?v=1',
								Method = 'POST',
								Headers = {
									['Content-Type'] = 'application/json',
									Origin = 'https://discord.com'
								},
								Body = http:JSONEncode({
									cmd = 'INVITE_BROWSER',
									nonce = http:GenerateGUID(false),
									args = {code = 'uNQRZs6gzm'}
								})
							})
						end
					end
				}
				common_table = nil
			end
		end
		if options.Info then
			local typ = type(options.Info)
			if typ == "string" then
				daaata[1 + #daaata] = {"AddLabel", "__Designer.Label.Creator", detailssection, {
					Text = options.Info
				}}
			elseif typ == "table" and #options.Info > 0 then
				for _, v in next, options.Info do
					daaata[1 + #daaata] = {"AddLabel", "__Designer.Label.Creator", detailssection, {
						Text = tostring(v)
					}}
				end
			end
		end
		for _, v in next, daaata do
			designerelements[v[2]] = v[3][v[1]](v[3], v[4])
		end
		designerelements["__Designer.Textbox.WorkspaceName"]:Set(library.WorkspaceName or "Unnamed Workspace")
		for k, v in next, elements do
			if v and k and string.sub(k, 1, 11) == "__Designer." and v.Type and v.Type ~= "Persistence" then
				flags[1 + #flags] = k
			end
		end
		if library.Backdrop then
			library.Backdrop.Image = resolveid(library_flags["__Designer.Background.ImageAssetID"], "__Designer.Background.ImageAssetID") or ""
			library.Backdrop.Visible = not not library_flags["__Designer.Background.UseBackgroundImage"]
			library.Backdrop.ImageTransparency = (library_flags["__Designer.Background.ImageTransparency"] or 95) / 100
			library.Backdrop.ImageColor3 = library_flags["__Designer.Background.ImageColor"] or Color3.new(1, 1, 1)
		end
		local function setbackground(t, Asset, Transparency, Visible)
			if Visible == nil and t ~= nil and type(t) ~= "table" then
				Asset, Transparency, Visible = t, Transparency, Visible
			end
			if Visible == 0 or ((Asset == 0 or Asset == false) and Visible == nil and Transparency == nil) then
				Visible = false
			elseif Visible == 1 or ((Asset == 1 or Asset == true) and Visible == nil and Transparency == nil) then
				Visible = true
			elseif Asset == nil and Transparency == nil and Visible == nil then
				Visible = not library_flags["__Designer.Background.UseBackgroundImage"]
			end
			local temp = Asset and type(Asset)
			if Transparency == nil and Visible == nil and temp == "number" and ((Asset ~= 1 and Asset ~= 0) or (Asset > 0 and Asset <= 100)) then
				Transparency, Asset, temp = Asset, nil
			end
			if temp and ((temp == "number" and Asset > 1) or temp == "string") then
				designerelements["__Designer.Textbox.ImageAssetID"]:Set(Asset)
			end
			temp = tonumber(Transparency)
			if temp then
				designerelements["__Designer.Slider.ImageTransparency"]:Set(temp)
			end
			if Visible ~= nil then
				designerelements["__Designer.Toggle.UseBackgroundImage"]:Set(not not Visible)
			end
			return Asset, Transparency, Visible
		end
		local bk = options.Background or options.Backdrop or options.Grahpic
		if bk then
			if type(bk) == "table" then
				setbackground(bk.Asset or bk[1], bk.Transparency or bk[2], bk.Visible or bk[3])
			else
				setbackground(bk, 0, 1)
			end
		end
		library.Designer = {
			Options = options,
			Parent = windowFunctions,
			Name = "Designer",
			Flag = "Designer",
			Type = "Designer",
			Instance = designer,
			SetBackground = setbackground
		}
		local savestuff = library.elements["__Designer.Background.WorkspaceProfile"]
		if savestuff then
			library.LoadFile = savestuff.LoadFile
			library.LoadFileRaw = savestuff.LoadFileRaw
			library.LoadJSON = savestuff.LoadJSON
			library.LoadJSONRaw = savestuff.LoadJSONRaw
			library.SaveFile = savestuff.SaveFile
			library.GetJSON = savestuff.GetJSON
		end
		spawn(updatecolorsnotween)
		return library.Designer
	end
	windowFunctions.AddDesigner = windowFunctions.CreateDesigner
	windowFunctions.NewDesigner = windowFunctions.CreateDesigner
	windowFunctions.Designer = windowFunctions.CreateDesigner
	windowFunctions.D = windowFunctions.CreateDesigner
	function windowFunctions:UpdateAll()
		local target = self or windowFunctions
		if target and type(target) == "table" and target.Flags then
			for _, e in next, target.Flags do
				if e and type(e) == "table" and e.Update then
					pcall(e.Update)
				end
			end
			pcall(function()
				if library.Backdrop then
					library.Backdrop.Visible = not not library_flags["__Designer.Background.UseBackgroundImage"]
					library.Backdrop.Image = resolveid(library_flags["__Designer.Background.ImageAssetID"], "__Designer.Background.ImageAssetID") or ""
					library.Backdrop.ImageColor3 = library_flags["__Designer.Background.ImageColor"] or Color3.new(1, 1, 1)
					library.Backdrop.ImageTransparency = (library_flags["__Designer.Background.ImageTransparency"] or 95) / 100
				end
			end)
		end
	end
	library.UpdateAll = windowFunctions.UpdateAll
	if options.Themeable or options.DefaultTheme or options.Theme then
		spawn(function()
			local os_clock = os.clock
			local starttime = os_clock()
			while os_clock() - starttime < 12 do
				if homepage then
					windowFunctions.GoHome = homepage
					local x, e = pcall(homepage)
					if not x and e then
						warn("Error going to Homepage:", e)
					end
					x, e = nil
					break
				end
				task.wait()
			end
			local whatDoILookLike = options.Themeable or options.DefaultTheme or options.Theme
			windowFunctions:CreateDesigner((type(whatDoILookLike) == "table" and whatDoILookLike) or nil)
			if options.DefaultTheme or options.Theme then
				spawn(function()
					local content = options.DefaultTheme or options.Theme or options.JSON or options.ThemeJSON
					if content and type(content) == "string" and #content > 1 then
						local good, jcontent = JSONDecode(content)
						if good and jcontent then
							for cflag, val in next, jcontent do
								local data = elements[cflag]
								if data and data.Type ~= "Persistence" then
									if data.Set then
										data:Set(val)
									elseif data.RawSet then
										data:RawSet(val)
									else
										library.flags[cflag] = val
									end
								end
							end
						end
					end
				end)
			end
			os_clock, starttime = nil
		end)
	end
	return windowFunctions
end

library.NewWindow = library.CreateWindow
library.AddWindow = library.CreateWindow
library.Window = library.CreateWindow
library.W = library.CreateWindow
local Wait = library.subs.Wait
wait()
local PepsisWorld = library:CreateWindow({
    Name = 'Nasa Hub Buyer Scripts',
    Theme = {
        Image = "rbxassetid://7483871523",
        Info = "Info",
        Background = {
            Asset = "rbxassetid://5553946656"
        }
    }
})

    local GeneralTab = PepsisWorld:CreateTab({
        Name = "General"
    })
    local IslandTab = PepsisWorld:CreateTab({
        Name = "Island"
    })
    local VisualsTab = PepsisWorld:CreateTab({
        Name = "Visuals"
    })
    local MiscellaneousTab = PepsisWorld:CreateTab({
        Name = "Miscellaneous"
    })

    local Farm = GeneralTab:CreateSection({
        Name = "// Main //"
    })
    local Fighting = GeneralTab:CreateSection({
        Name = "// Fighting Style //"
    })
    local St = GeneralTab:CreateSection({
        Name = "// Setting //",
        Side = "Right"
    })
    Fighting:AddToggle({
        Name = "Auto Superhuman",
        Value = false,
        Flag = "Auto Superhuman .",
        Callback = function(value)
            _G.Auto_Superhuman=value
        end
    })
    Fighting:AddToggle({
        Name = "Auto Death Step",
        Value = false,
        Flag = "Auto Death Step .",
        Callback = function(value)
            _G.Fast_Attack=value
        end
    })
    Fighting:AddToggle({
        Name = "Auto Sharkman Karate",
        Value = false,
        Flag = "Auto Sharkman Karate .",
        Callback = function(value)
            _G.Fast_Attack=value
        end
    })
    Fighting:AddToggle({
        Name = "Auto Electric Claw",
        Value = false,
        Flag = "Auto Electric Claw .",
        Callback = function(value)
            _G.Fast_Attack=value
        end
    })
    Fighting:AddToggle({
        Name = "Auto Dragon Talon",
        Value = false,
        Flag = "Auto Dragon Talon .",
        Callback = function(value)
            _G.Fast_Attack=value
        end
    })
    Fighting:AddToggle({
        Name = "Auto Godhuman",
        Value = false,
        Flag = "Auto Godhuman .",
        Callback = function(value)
            _G.Fast_Attack=value
        end
    })
    local Mastery = GeneralTab:CreateSection({
        Name = "// Mastery //"
    })
    Mastery:AddToggle({
        Name = "Auto Farm Mastery Devil Fruits",
        Value = false,
        Flag = "Auto Farm Mastery Devil Fruits .",
        Callback = function(value)
            _G.Fast_Attack=value
        end
    })
    Mastery:AddToggle({
        Name = "Auto Farm Mastery Gun",
        Value = false,
        Flag = "AAuto Farm Mastery Gun .",
        Callback = function(value)
            _G.Fast_Attack=value
        end
    })
    Mastery:AddSlider({
        Name = "Health :",
        Flag = "Health",
        Value = 25,
        Min = 0,
        Max = 100,
        Format = function(Value)
            if Value == 0 then
                return "Health : 0%"
            else
                return "Health : " .. tostring(Value) .. "%"
            end
        end
    })
    Mastery:AddSlider({
        Name = "Distance X :",
        Flag = "Distance X",
        Value = 25,
        Min = 0,
        Max = 100,
        Format = function(Value)
            if Value == 0 then
                return "Distance X : 0%"
            else
                return "Distance X : " .. tostring(Value) .. ""
            end
        end
    })
    Mastery:AddSlider({
        Name = "Distance Y :",
        Flag = "Distance Y",
        Value = 25,
        Min = 0,
        Max = 100,
        Format = function(Value)
            if Value == 0 then
                return "Distance Y : 0%"
            else
                return "Distance Y : " .. tostring(Value) .. ""
            end
        end
    })
    Mastery:AddSlider({
        Name = "Distance Z :",
        Flag = "Distance Z",
        Value = 25,
        Min = 0,
        Max = 100,
        Format = function(Value)
            if Value == 0 then
                return "Distance Z : 0%"
            else
                return "Distance Z : " .. tostring(Value) .. ""
            end
        end
    })
    local Bosses = GeneralTab:CreateSection({
        Name = "// Bosses //"
    })
    Items = {"soon"}
    
    local Material = GeneralTab:CreateSection({
        Name = "// Material Items //"
    })
    Material:AddDropdown({
        Name = "Select Items",
        Value = false, 
        List = Items,
        Callback = function(value)
            SelectItems = value
        end
    })
    Material:AddToggle({
        Name = "Auto Farm Items",
        Value = false,
        Flag = "Auto Farm Items .",
        Callback = function(value)
            _G.Fast_Attack=value
        end
    })
    Weapon = {"Malee", "Sword", "Blox Fruit"}

    St:AddDropdown({
        Name = "Select Weapon",
        Value = false, 
        List = Weapon,
        Callback = function(value)
            SelectWeapon = value
            Select = value
        end
    })
    St:AddToggle({
        Name = "Fast Attack",
        Value = true,
        Flag = "Fast Attack .",
        Callback = function(value)
            _G.Fast_Attack=value
            _G.FastAttackNormalSpeed =value
        end
    })
    St:AddToggle({
        Name = "Auto Screen Boost",
        Value = false,
        Flag = "Auto Screen Boost .",
        Callback = function(value)
            if value == true then
                game:GetService("RunService"):Set3dRenderingEnabled(false)
                setfpscap(120)
            else
                game:GetService("RunService"):Set3dRenderingEnabled(true)
                setfpscap(360)
            end
        end
    })
    St:AddToggle({
        Name = "Enabled Bypass TP",
        Value = false,
        Flag = "Enabled Bypass TP .",
        Callback = function(value)
            _G.Bypass=value
        end
    })
    St:AddToggle({
        Name = "Auto Rejoin",
        Value = true,
        Flag = "Auto Rejoin .",
        Callback = function(value)
            _G.Fast_Attack=value
            _G.FastAttackNormalSpeed =value
        end
    })

    local usll = GeneralTab:CreateSection({
        Name = "// Ues Skill //",
        Side = "Right"
    })

    usll:AddToggle({
        Name = "Skill Z",
        Value = true,
        Flag = "Skill Z .",
        Callback = function(value)
            _G.Fast_Attack=value
        end
    })
    usll:AddToggle({
        Name = "Skill X",
        Value = true,
        Flag = "Skill X .",
        Callback = function(value)
            _G.Fast_Attack=value
        end
    })
    usll:AddToggle({
        Name = "Skill C",
        Value = true,
        Flag = "Skill C .",
        Callback = function(value)
            _G.Fast_Attack=value
        end
    })
    usll:AddToggle({
        Name = "Skill V",
        Value = true,
        Flag = "Skill V .",
        Callback = function(value)
            _G.Fast_Attack=value
        end
    })
    local usllg = GeneralTab:CreateSection({
        Name = "// Ues Skill Gun //",
        Side = "Right"
    })
    usllg:AddToggle({
        Name = "Skill Z",
        Value = true,
        Flag = "Skill Z .",
        Callback = function(value)
            _G.Fast_Attack=value
        end
    })
    usllg:AddToggle({
        Name = "Skill X",
        Value = true,
        Flag = "Skill X .",
        Callback = function(value)
            _G.Fast_Attack=value
        end
    })

    local stats = GeneralTab:CreateSection({
        Name = "// Stats //",
        Side = "Right"
    })

    Stats = {"Melee",'Defense', "Sword", "Demon Fruit"}

    stats:AddDropdown({
        Name = "Select Stats",
        Value = false,
        List = Stats,
        Callback = function(value)
            Selectstats = value
        end
    })
    task.spawn(function()
        while wait() do
            pcall(function()
                if _G.Statsup then
                    game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("AddPoint",Selectstats,20)
                end
            end)
        end
    end)
    stats:AddToggle({
        Name = "Auto Stats",
        Value = false,
        Flag = "Auto Stats .",
        Callback = function(value)
            _G.Statsup=value
        end
    })
    spawn(function()
        while wait() do
            pcall(function()
                if Select == "Melee" then
                    for i, v in pairs(game.Players.LocalPlayer.Backpack:GetChildren()) do
                        if v.ToolTip == "Melee" then
                            if game.Players.LocalPlayer.Backpack:FindFirstChild(tostring(v.Name)) then
                                SelectWeapon = v.Name
                            end
                        end
                    end
                elseif Select == "Sword" then
                    for i, v in pairs(game.Players.LocalPlayer.Backpack:GetChildren()) do
                        if v.ToolTip == "Sword" then
                            if game.Players.LocalPlayer.Backpack:FindFirstChild(tostring(v.Name)) then
                                SelectWeapon = v.Name
                            end
                        end
                    end
                elseif Select == "Blox Fruit" then
                    for i, v in pairs(game.Players.LocalPlayer.Backpack:GetChildren()) do
                        if v.ToolTip == "Blox Fruit" then
                            if game.Players.LocalPlayer.Backpack:FindFirstChild(tostring(v.Name)) then
                                SelectWeapon = v.Name
                            end
                        end
                    end
                else
                    for i, v in pairs(game.Players.LocalPlayer.Backpack:GetChildren()) do
                        if v.ToolTip == "Melee" then
                            if game.Players.LocalPlayer.Backpack:FindFirstChild(tostring(v.Name)) then
                                SelectWeapon = v.Name
                            end
                        end
                    end
                end
            end)
        end
    end)

    Farm:AddToggle({
        Name = "Auto Farm Level",
        Value = false,
        Flag = "Auto Farm Level .",
        Callback = function(value)
            _G.AutoFarmcheck = value
            if value == false then
                pcall(function()
                    q:Cancel()
                end)
            end
        end
    })
    Farm:AddToggle({
        Name = "Auto Saber",
        Value = false,
        Flag = "Auto Saber .",
        Callback = function(value)
            _G.Saber = value
            if value == false then
                pcall(function()
                    q:Cancel()
                end)
            end
        end
    })
    function isnil(thing)
        return (thing==nil)
    end
    local function round(n)
        return math.floor(tonumber(n)+0.5)
    end
    Number=math.random(1,1000000)
    task.spawn(function()
        while true do task.wait()
            for i,v in pairs(game:GetService('Players'):GetChildren())do
                if v.Name~=game:GetService('Players').LocalPlayer.Name then
                    pcall(function()
                        if not isnil(v.Character)then
                            if _G.ESPP then
                                if not isnil(v.Character.Head)and not v.Character.Head:FindFirstChild('Name'..Number)and not v.Character.Head:FindFirstChild('Name1'..Number)then
                                    local BillboardGui=Instance.new('BillboardGui',v.Character.Head)
                                    BillboardGui.Name='Name'..Number
                                    BillboardGui.ExtentsOffset=Vector3.new(0,1,0)
                                    BillboardGui.Size=UDim2.new(1,200,1,30)
                                    BillboardGui.Adornee=v.Character.Head
                                    BillboardGui.AlwaysOnTop=true
                                    local BillboardGui1=Instance.new('BillboardGui',v.Character.Head)
                                    BillboardGui1.Name='Name1'..Number
                                    BillboardGui1.ExtentsOffset=Vector3.new(0,1,0)
                                    BillboardGui1.Size=UDim2.new(1,200,1,30)
                                    BillboardGui1.Adornee=v.Character.Head
                                    BillboardGui1.AlwaysOnTop=true
                                    local TextLabel=Instance.new('TextLabel',BillboardGui)
                                    TextLabel.Font=Enum.Font.Code
                                    TextLabel.FontSize='Size14'
                                    TextLabel.TextWrapped=true
                                    TextLabel.Text=(v.Name)
                                    TextLabel.Size=UDim2.new(1,0,1,0)
                                    TextLabel.TextYAlignment='Top'
                                    TextLabel.BackgroundTransparency=1
                                    TextLabel.TextStrokeTransparency=0
                                    local TextLabel1=Instance.new('TextLabel',BillboardGui1)
                                    TextLabel1.Font=Enum.Font.Code
                                    TextLabel1.FontSize='Size14'
                                    TextLabel1.TextWrapped=true
                                    TextLabel1.Text=('\nDistance : [ '..round((game:GetService('Players').LocalPlayer.Character.Head.Position-v.Character.Head.Position).Magnitude/3)..' ]')
                                    TextLabel1.Size=UDim2.new(1,0,1,0)
                                    TextLabel1.TextYAlignment='Top'
                                    TextLabel1.BackgroundTransparency=1
                                    TextLabel1.TextStrokeTransparency=0
                                    if v.Team==game:GetService('Players').LocalPlayer.Team then
                                        TextLabel.TextColor3=Color3.new(255,255,255)
                                        TextLabel1.TextColor3=Color3.new(0,255,0)
                                    else
                                        TextLabel.TextColor3=Color3.new(255,255,255)
                                        TextLabel1.TextColor3=Color3.new(255,0,0)
                                    end
                                else
                                    v.Character.Head['Name'..Number].TextLabel.Text=(v.Name)
                                    v.Character.Head['Name1'..Number].TextLabel.Text=('\nDistance : [ '..round((game:GetService('Players').LocalPlayer.Character.Head.Position-v.Character.Head.Position).Magnitude/3)..' ]')
                                    if v.Team==game:GetService('Players').LocalPlayer.Team then
                                        TextLabel.TextColor3=Color3.new(255,255,255)
                                        TextLabel1.TextColor3=Color3.new(0,255,0)
                                    else
                                        TextLabel.TextColor3=Color3.new(255,255,255)
                                        TextLabel1.TextColor3=Color3.new(255,0,0)
                                    end
                                end
                            else
                                if v.Character.Head:FindFirstChild('Name'..Number)and v.Character.Head:FindFirstChild('Name1'..Number)then
                                    v.Character.Head:FindFirstChild('Name'..Number):Destroy()
                                    v.Character.Head:FindFirstChild('Name1'..Number):Destroy()
                                end
                            end
                        end
                    end)
                end
            end
        end
    end)
    task.spawn(function()
        while true do task.wait()
            for i,v in pairs(game:GetService("Workspace")["_WorldOrigin"].Locations:GetChildren())do
                if _G.ESPI then
                    if not v:FindFirstChild('Namei'..Number) and not v:FindFirstChild('Name1i'..Number)then
                        local BillboardGui=Instance.new('BillboardGui',v)
                        BillboardGui.Name='Namei'..Number
                        BillboardGui.ExtentsOffset=Vector3.new(0,1,0)
                        BillboardGui.Size=UDim2.new(1,200,1,30)
                        BillboardGui.Adornee=v
                        BillboardGui.AlwaysOnTop=true
                        local BillboardGui1=Instance.new('BillboardGui',v)
                        BillboardGui1.Name='Name1i'..Number
                        BillboardGui1.ExtentsOffset=Vector3.new(0,1,0)
                        BillboardGui1.Size=UDim2.new(1,200,1,30)
                        BillboardGui1.Adornee=v
                        BillboardGui1.AlwaysOnTop=true
                        local TextLabel=Instance.new('TextLabel',BillboardGui)
                        TextLabel.Font=Enum.Font.Code
                        TextLabel.FontSize='Size14'
                        TextLabel.TextWrapped=true
                        TextLabel.Text=(v.Name)
                        TextLabel.Size=UDim2.new(1,0,1,0)
                        TextLabel.TextYAlignment='Top'
                        TextLabel.BackgroundTransparency=1
                        TextLabel.TextStrokeTransparency=0
                        TextLabel.TextColor3=Color3.new(255,255,255)
                        local TextLabel1=Instance.new('TextLabel',BillboardGui1)
                        TextLabel1.Font=Enum.Font.Code
                        TextLabel1.FontSize='Size14'
                        TextLabel1.TextWrapped=true
                        TextLabel1.Text=('\nDistance : [ '..round((game:GetService('Players').LocalPlayer.Character.Head.Position-v.Position).Magnitude/3)..' ]')
                        TextLabel1.Size=UDim2.new(1,0,1,0)
                        TextLabel1.TextYAlignment='Top'
                        TextLabel1.BackgroundTransparency=1
                        TextLabel1.TextStrokeTransparency=0
                        TextLabel1.TextColor3=Color3.new(0,0,0)
                    else
                        v['Namei'..Number].TextLabel.Text=(v.Name)
                        v['Name1i'..Number].TextLabel.Text=('\nDistance : [ '..round((game:GetService('Players').LocalPlayer.Character.Head.Position-v.Position).Magnitude/3)..' ]')
                        TextLabel.TextColor3=Color3.new(255,255,255)
                        TextLabel1.TextColor3=Color3.new(0,0,0)
                    end
                else
                    if v:FindFirstChild('Namei'..Number)and v:FindFirstChild('Name1i'..Number)then
                        v:FindFirstChild('Namei'..Number):Destroy()
                        v:FindFirstChild('Name1i'..Number):Destroy()
                    end
                end
            end
        end
    end)
    local ESP = IslandTab:CreateSection({
        Name = "// ESP //",
        Side = "Right"
    })
    ESP:AddToggle({
        Name = "ESP Players",
        Value = false,
        Flag = "ESP .",
        Callback = function(value)
            _G.ESPP = value
        end
    })
    ESP:AddToggle({
        Name = "ESP Island",
        Value = false,
        Flag = "ESP .",
        Callback = function(value)
            _G.ESPI = value
        end
    })

    function UseCode(Text)
        game:GetService("ReplicatedStorage").Remotes.Redeem:InvokeServer(Text)
    end

    local Code = {"EXP_5B", "CONTROL", "UPDATE11", "XMASEXP", "1BILLION", "ShutDownFix2", "UPD14", "STRAWHATMAINE",
                "TantaiGaming", "Colosseum", "Axiore", "Sub2Daigrock", "Sky Island 3", "Sub2OfficialNoobie",
                "SUB2NOOBMASTER123", "THEGREATACE", "Fountain City", "BIGNEWS", "FUDD10", "SUB2GAMERROBOT_EXP1", "UPD15",
                "2BILLION", "UPD16", "3BVISITS", "fudd10_v2", "Starcodeheo", "Magicbus","JCWK", "Bluxxy", "Sub2Fer999",
                "Enyu_is_Pro"}
    St:AddButton({
        Name = "Redeem All Code",
        Callback = function()
            for i, v in pairs(Code) do
                UseCode(v)
            end
        end
    })
    function CheckQuest()
        local MYLEVEL = game:GetService("Players").LocalPlayer.Data.Level.Value
        if OldWolrd then
            if MYLEVEL == 1 or MYLEVEL <= 9 then
                Double_Quest=1
                Ms = "Bandit [Lv. 5]"
                NameQuest = "BanditQuest1"
                QuestLv = 1
                NameQ = "Bandit"
                CFrameQ = CFrame.new(1060.0158691406, 16.424287796021, 1547.9769287109)
                CFramePuk = CFrame.new(1073.86414, 16.2736206, 1612.17163, -0.695649207, 0, -0.718381643, 0, 1, 0,
                    0.718381643, 0, -0.695649207)
                NM = 'Windmill'
            elseif MYLEVEL == 10 or MYLEVEL <= 14 then
                Double_Quest=2
                Ms = "Monkey [Lv. 14]"
                NameQuest = "JungleQuest"
                QuestLv = 1
                NameQ = "Monkey"
                CFrameQ = CFrame.new(-1601.52808, 36.9774551, 152.812317, -0.0892550573, -7.99012057e-08, -0.996008813,
                    -4.66281733e-08, 1, -7.60429089e-08, 0.996008813, 3.96548572e-08, -0.0892550573)
                CFramePuk = CFrame.new(-1609.71216, 39.8521576, 123.384674, 0.708323717, 6.74341152e-08, 0.705887735,
                    -1.86098941e-08, 1, -7.68568071e-08, -0.705887735, 4.13030072e-08, 0.708323717)
            elseif MYLEVEL == 15 or MYLEVEL <= 29 then
                Double_Quest=3
                magbring = 240
                Ms = "Gorilla [Lv. 20]"
                NameQuest = "JungleQuest"
                QuestLv = 2
                NameQ = "Gorilla"
                CFrameQ = CFrame.new(-1600.24353, 36.8521347, 153.224792, 0.0664860159, 1.09421023e-07, -0.997787356,
                    9.55680779e-09, 1, 1.10300476e-07, 0.997787356, -1.68691017e-08, 0.0664860159)
                CFramePuk = CFrame.new(-1260.29321, 18.6214619, -398.3508, 0.816335142, 5.76316722e-07, -0.577578545,
                    8.32609999e-08, 1, 1.11549434e-06, 0.577578545, -9.58707005e-07, 0.816335142)
            elseif MYLEVEL == 30 or MYLEVEL <= 39 then
                Double_Quest=4
                Ms = "Pirate [Lv. 35]"
                NameQuest = "BuggyQuest1"
                QuestLv = 1
                NameQ = "Pirate"
                CFrameQ = CFrame.new(-1141.07483, 4.10001802, 3831.5498, 0.965929627, -0, -0.258804798, 0, 1, -0,
                    0.258804798, 0, 0.965929627)
                CFramePuk = CFrame.new(-1141.07483, 4.10001802, 3831.5498, 0.965929627, -0, -0.258804798, 0, 1, -0,
                    0.258804798, 0, 0.965929627)
            elseif MYLEVEL == 40 or MYLEVEL <= 59 then
                Double_Quest=5
                Ms = "Brute [Lv. 45]"
                NameQuest = "BuggyQuest1"
                QuestLv = 2
                NameQ = "Brute"
                CFrameQ = CFrame.new(-1141.07483, 4.10001802, 3831.5498, 0.965929627, -0, -0.258804798, 0, 1, -0,
                    0.258804798, 0, 0.965929627)
                CFramePuk = CFrame.new(-1144.44861, 90.5594559, 4307.25928, -0.998438537, 0, 0.0558618344, 0, 1, 0,
                    -0.0558618344, 0, -0.998438537)
            elseif MYLEVEL == 60 or MYLEVEL <= 74 then
                Double_Quest=6
                Ms = "Desert Bandit [Lv. 60]"
                NameQuest = "DesertQuest"
                QuestLv = 1
                NameQ = "Desert Bandit"
                CFrameQ = CFrame.new(894.488647, 5.14000702, 4392.43359, 0.819155693, -0, -0.573571265, 0, 1, -0,
                    0.573571265, 0, 0.819155693)
                CFramePuk = CFrame.new(894.488647, 5.14000702, 4392.43359, 0.819155693, -0, -0.573571265, 0, 1, -0,
                    0.573571265, 0, 0.819155693)
            elseif MYLEVEL == 75 or MYLEVEL <= 89 then
                Double_Quest=7
                Ms = "Desert Officer [Lv. 70]"
                NameQuest = "DesertQuest"
                QuestLv = 2
                NameQ = "Desert Officer"
                CFrameQ = CFrame.new(894.488647, 5.14000702, 4392.43359, 0.819155693, -0, -0.573571265, 0, 1, -0,
                    0.573571265, 0, 0.819155693)
                CFramePuk = CFrame.new(1580.03198, 4.61375761, 4366.86426)
            elseif MYLEVEL == 90 or MYLEVEL <= 99 then
                Double_Quest=8
                Ms = "Snow Bandit [Lv. 90]"
                NameQuest = "SnowQuest"
                QuestLv = 1
                NameQ = "Snow Bandit"
                CFrameQ = CFrame.new(1384.01538, 87.272789, -1296.28137, 0.462413222, -7.79864777e-08, -0.88666451,
                    -1.42050363e-08, 1, -9.53630916e-08, 0.88666451, 5.6692258e-08, 0.462413222)
                CFramePuk = CFrame.new(1372.84326, 105.990303, -1422.19507, 0.719091773, -2.12436309e-08, 0.694915235,
                    9.82151036e-08, 1, -7.10619616e-08, -0.694915235, 1.19351228e-07, 0.719091773)
            elseif MYLEVEL == 100 or MYLEVEL <= 119 then
                Double_Quest=9
                Ms = "Snowman [Lv. 100]"
                NameQuest = "SnowQuest"
                QuestLv = 2
                NameQ = "Snowman"
                CFrameQ = CFrame.new(1384.01538, 87.272789, -1296.28137, 0.462413222, -7.79864777e-08, -0.88666451,
                    -1.42050363e-08, 1, -9.53630916e-08, 0.88666451, 5.6692258e-08, 0.462413222)
                CFramePuk = CFrame.new(1220.92712, 138.011871, -1489.01208, 0.389352709, -7.53626693e-07, 0.921088696,
                    1.45705499e-07, 1, 7.56600116e-07, -0.921088696, -1.60376572e-07, 0.389352709)
            elseif MYLEVEL == 120 or MYLEVEL <= 149 then
                Double_Quest=10
                Ms = "Chief Petty Officer [Lv. 120]"
                NameQuest = "MarineQuest2"
                QuestLv = 1
                NameQ = "Chief Petty Officer"
                CFrameQ = CFrame.new(-5034.64893, 28.6520348, 4324.53369, -0.0616381466, 5.83357576e-08, 0.998098552,
                    -1.59750098e-08, 1, -5.9433436e-08, -0.998098552, -1.96080023e-08, -0.0616381466)
                CFramePuk = CFrame.new(-4863.61328, 22.6520348, 4306.39307, 0.536051273, 7.00434066e-09, -0.844185412,
                    -5.8011751e-10, 1, 7.92878918e-09, 0.844185412, -3.76051057e-09, 0.536051273)
            elseif MYLEVEL == 150 or MYLEVEL <= 174 then
                Double_Quest=11
                Ms = "Sky Bandit [Lv. 150]"
                NameQuest = "SkyQuest"
                QuestLv = 1
                NameQ = "Sky Bandit"
                CFrameQ = CFrame.new(-4843.2041, 717.669617, -2623.13159, -0.775086224, -1.6359829e-08, -0.631855488,
                    -4.10942462e-08, 1, 2.45178793e-08, 0.631855488, 4.49690951e-08, -0.775086224)
                CFramePuk = CFrame.new(-4970.74219, 294.544342, -2890.11353, -0.994874597, -8.61311165e-08, -0.101116329,
                    -9.10836278e-08, 1, 4.43614923e-08, 0.101116329, 5.33441664e-08, -0.994874597)
            elseif MYLEVEL == 175 or MYLEVEL <= 189 then
                Double_Quest=12
                Ms = "Dark Master [Lv. 175]"
                NameQuest = "SkyQuest"
                QuestLv = 2
                NameQ = "Dark Master"
                CFrameQ = CFrame.new(-4843.2041, 717.669617, -2623.13159, -0.775086224, -1.6359829e-08, -0.631855488,
                    -4.10942462e-08, 1, 2.45178793e-08, 0.631855488, 4.49690951e-08, -0.775086224)
                CFramePuk = CFrame.new(-5239.94629, 392.217102, -2208.18335, 0.969297886, -5.95604988e-09, -0.245889395,
                    3.87897714e-09, 1, -8.93151775e-09, 0.245889395, 7.70350184e-09, 0.969297886)
            elseif MYLEVEL == 190 or MYLEVEL <= 209 then
                Double_Quest=13
                Ms = "Prisoner [Lv. 190]"
                NameQuest = "PrisonerQuest"
                QuestLv = 1
                NameQ = "Prisoner"
                CFrameQ = CFrame.new(5307.95166015625, 1.6809712648391724, 475.1698913574219)
                CFramePuk = CFrame.new(5029.708984375, 68.67806243896484, 445.857177734375)
            elseif MYLEVEL == 210 or MYLEVEL <= 249 then
                Double_Quest=14
                Ms = "Dangerous Prisoner [Lv. 210]"
                NameQuest = "PrisonerQuest"
                QuestLv = 2
                NameQ = "Dangerous Prisoner"
                CFrameQ = CFrame.new(5307.95166015625, 1.6809712648391724, 475.1698913574219)
                CFramePuk = CFrame.new(5673.51758, 68.6786652, 783.757629, -0.0514698699, 7.78369369e-08, 0.998674572,
                    8.35602094e-08, 1, -7.36337e-08, -0.998674572, 7.96595359e-08, -0.0514698699)
            elseif MYLEVEL == 250 or MYLEVEL <= 299 then
                Double_Quest=15
                Ms = "Toga Warrior [Lv. 250]"
                NameQuest = "ColosseumQuest"
                QuestLv = 1
                NameQ = "Toga Warrior"
                CFrameQ = CFrame.new(-1575.72961, 7.38933659, -2983.39453, 0.52762109, -1.48187587e-06, 0.849479854,
                    2.69328297e-07, 1, 1.57716818e-06, -0.849479854, -6.0335816e-07, 0.52762109)
                CFramePuk = CFrame.new(-1819.12415, 7.28907108, -2744.02539, 0.547199547, 2.10840998e-08, -0.837002158,
                    -1.27399286e-10, 1, 2.51067309e-08, 0.837002158, -1.36317579e-08, 0.547199547)
            elseif MYLEVEL == 300 or MYLEVEL <= 324 then
                Double_Quest=16
                Ms = "Military Soldier [Lv. 300]"
                NameQuest = "MagmaQuest"
                QuestLv = 1
                NameQ = "Military Soldier"
                CFrameQ = CFrame.new(-5316.33887, 12.236989, 8517.67285, 0.499506682, -5.08374072e-08, -0.86631006,
                    -1.30872131e-08, 1, -6.62286652e-08, 0.86631006, 4.44192452e-08, 0.499506682)
                CFramePuk = CFrame.new(-5419.0752, 10.9255161, 8464.50488, -0.637788415, -4.55103836e-05, 0.770211577,
                    7.05542743e-06, 1, 6.49305366e-05, -0.770211577, 4.68461185e-05, -0.637788415)
            elseif MYLEVEL == 325 or MYLEVEL <= 374 then
                Double_Quest=17
                Ms = "Military Spy [Lv. 325]"
                NameQuest = "MagmaQuest"
                QuestLv = 2
                NameQ = "Military Spy"
                CFrameQ = CFrame.new(-5316.33887, 12.236989, 8517.67285, 0.499506682, -5.08374072e-08, -0.86631006,
                    -1.30872131e-08, 1, -6.62286652e-08, 0.86631006, 4.44192452e-08, 0.499506682)
                CFramePuk = CFrame.new(-5805.42041, 99.5276108, 8782.36719, -0.316935152, -6.4923519e-08, 0.948447227,
                    4.12987404e-08, 1, 8.2252896e-08, -0.948447227, 6.52385026e-08, -0.316935152)
            elseif MYLEVEL == 375 or MYLEVEL <= 399 then
                Double_Quest=18
                Ms = "Fishman Warrior [Lv. 375]"
                NameQuest = "FishmanQuest"
                QuestLv = 1
                NameQ = "Fishman Warrior"
                CFrameQ = CFrame.new(61122.2422, 18.4716377, 1568.84778, 0.971045971, -1.77007031e-08, 0.238892734,
                    4.80190776e-09, 1, 5.45760841e-08, -0.238892734, -5.18487475e-08, 0.971045971)
                CFramePuk = CFrame.new(60898.043, 18.4828224, 1550.9906, -0.0750192106, -4.46996573e-09, 0.997182071,
                    3.6461556e-10, 1, 4.51002746e-09, -0.997182071, 7.0192685e-10, -0.0750192106)
                    if    (_G.AutoFram )and
                    (CFrameQ.Position - game.Players.LocalPlayer.Character.HumanoidRootPart.Position).Magnitude > 3000 then
                    game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("requestEntrance",
                        Vector3.new(61163.8516, 5.43263245, 1819.78418, 1, 6.89280011e-09, 9.74497786e-14, -6.89280011e-09,
                            1, 3.38349579e-08, -9.72165599e-14, -3.38349579e-08, 1))
                end
            elseif MYLEVEL == 400 or MYLEVEL <= 449 then
                Double_Quest=19
                Ms = "Fishman Commando [Lv. 400]"
                NameQuest = "FishmanQuest"
                QuestLv = 2
                NameQ = "Fishman Commando"
                CFrameQ = CFrame.new(61122.2422, 18.4716377, 1568.84778, 0.971045971, -1.77007031e-08, 0.238892734,
                    4.80190776e-09, 1, 5.45760841e-08, -0.238892734, -5.18487475e-08, 0.971045971)
                CFramePuk = CFrame.new(61885.4063, 18.4828224, 1500.37195, 0.722261012, 4.84021889e-08, -0.691620588,
                    1.27929427e-08, 1, 8.33434299e-08, 0.691620588, -6.90435726e-08, 0.722261012)
                    if    (_G.AutoFram )and
                    (CFrameQ.Position - game.Players.LocalPlayer.Character.HumanoidRootPart.Position).Magnitude > 3000 then
                    game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("requestEntrance",
                        Vector3.new(61163.8516, 5.43263245, 1819.78418, 1, 6.89280011e-09, 9.74497786e-14, -6.89280011e-09,
                            1, 3.38349579e-08, -9.72165599e-14, -3.38349579e-08, 1))
                end
            elseif MYLEVEL == 450 or MYLEVEL <= 474 then
                Double_Quest=20
                Ms = "God's Guard [Lv. 450]"
                NameQuest = "SkyExp1Quest"
                QuestLv = 1
                NameQ = "God's Guard"
                CFrameQ = CFrame.new(-4721.28369, 845.277161, -1954.95154, -0.979754269, -1.72096932e-08, 0.200205252,
                    -2.52417198e-09, 1, 7.36076018e-08, -0.200205252, 7.16119786e-08, -0.979754269)
                CFramePuk = CFrame.new(-4630.00635, 866.902954, -1936.76331, -0.656243384, 9.12737941e-12, 0.754549265,
                    3.58402819e-09, 1, 3.10498938e-09, -0.754549265, 4.74195483e-09, -0.656243384)
                    if    (_G.AutoFram )and
                    (CFrameQ.Position - game.Players.LocalPlayer.Character.HumanoidRootPart.Position).Magnitude > 3000 then
                    game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("requestEntrance", Vector3.new(
                        -4607.82275, 872.54248, -1667.55688))
                end
            elseif MYLEVEL == 475 or MYLEVEL <= 524 then
                Double_Quest=21
                Ms = "Shanda [Lv. 475]"
                NameQuest = "SkyExp1Quest"
                QuestLv = 2
                NameQ = "Shanda"
                CFrameQ = CFrame.new(-7861.79736, 5545.49316, -379.920776, 0.504107952, -1.41941534e-08, -0.863640666,
                    -1.31181936e-08, 1, -2.40923566e-08, 0.863640666, 2.34745521e-08, 0.504107952)
                CFramePuk = CFrame.new(-7682.69775, 5607.36279, -445.691833, 0.786274791, -4.48163426e-08, -0.617877364,
                    -4.81674345e-09, 1, -7.86622607e-08, 0.617877364, 6.48263239e-08, 0.786274791)
                if    (_G.AutoFram )and
                    (CFrameQ.Position - game.Players.LocalPlayer.Character.HumanoidRootPart.Position).Magnitude > 3000 then
                    game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("requestEntrance", Vector3.new(
                        -7894.6176757813, 5547.1416015625, -380.29119873047))
                end
            elseif MYLEVEL == 525 or MYLEVEL <= 549 then
                Double_Quest=22
                Ms = "Royal Squad [Lv. 525]"
                NameQuest = "SkyExp2Quest"
                QuestLv = 1
                NameQ = "Royal Squad"
                CFrameQ = CFrame.new(-7902.23242, 5635.96387, -1411.96741, -0.0435957126, -2.13718043e-09, 0.999049246,
                    4.23562352e-10, 1, 2.15769735e-09, -0.999049246, 5.1722604e-10, -0.0435957126)
                CFramePuk = CFrame.new(-7579.42285, 5628.39111, -1540.75073, -0.0374937952, 1.17099557e-08, 0.999296963,
                    -3.30279164e-08, 1, -1.29574085e-08, -0.999296963, -3.34905081e-08, -0.0374937952)
            elseif MYLEVEL == 550 or MYLEVEL <= 624 then
                Double_Quest=23
                Ms = "Royal Soldier [Lv. 550]"
                NameQuest = "SkyExp2Quest"
                QuestLv = 2
                NameQ = "Royal Soldier"
                CFrameQ = CFrame.new(-7902.23242, 5635.96387, -1411.96741, -0.0435957126, -2.13718043e-09, 0.999049246,
                    4.23562352e-10, 1, 2.15769735e-09, -0.999049246, 5.1722604e-10, -0.0435957126)
                CFramePuk = CFrame.new(-7834.84717, 5681.36182, -1790.76782, -0.102890432, 3.28112684e-08, 0.994692683,
                    -6.45397762e-08, 1, -3.96622966e-08, -0.994692683, -6.82781121e-08, -0.102890432)
            elseif MYLEVEL == 625 or MYLEVEL <= 649 then
                Double_Quest=24
                Ms = "Galley Pirate [Lv. 625]"
                NameQuest = "FountainQuest"
                QuestLv = 1
                NameQ = "Galley Pirate"
                CFrameQ = CFrame.new(5254.52734, 38.5011368, 4049.80127, -0.0732342899, 2.23174847e-08, -0.997314751,
                    1.2052287e-07, 1, 1.35274023e-08, 0.997314751, -1.19208565e-07, -0.0732342899)
                CFramePuk = CFrame.new(5597.58936, 41.5013657, 3960.55371, -0.584786832, 4.98908861e-08, 0.811187029,
                    4.10757259e-08, 1, -3.18919575e-08, -0.811187029, 1.4670098e-08, -0.584786832)
            elseif MYLEVEL >= 650 then
                Double_Quest=25
                Ms = "Galley Captain [Lv. 650]"
                NameQuest = "FountainQuest"
                QuestLv = 2
                NameQ = "Galley Captain"
                CFrameQ = CFrame.new(5254.52734, 38.5011368, 4049.80127, -0.0732342899, 2.23174847e-08, -0.997314751,
                    1.2052287e-07, 1, 1.35274023e-08, 0.997314751, -1.19208565e-07, -0.0732342899)
                CFramePuk = CFrame.new(5705.8252, 52.241478, 4890.11035, -0.969319642, 4.40228476e-09, 0.245803744,
                    -7.88622412e-09, 1, -4.90088397e-08, -0.245803744, -4.94436954e-08, -0.969319642)
            end
        end
        if SecondSea then
            if MYLEVEL == 700 or MYLEVEL <= 724 then
                Double_Quest=1
                Ms = "Raider [Lv. 700]"
                NameQuest = "Area1Quest"
                QuestLv = 1
                NameQ = "Raider"
                CFrameQ = CFrame.new(-424.080078, 73.0055847, 1836.91589, 0.253544956, -1.42165932e-08, 0.967323601,
                    -6.00147771e-08, 1, 3.04272909e-08, -0.967323601, -6.5768397e-08, 0.253544956)
                CFramePuk = CFrame.new(-737.026123, 39.1748352, 2392.57959)
            elseif MYLEVEL == 725 or MYLEVEL <= 774 then
                Double_Quest=2
                Ms = "Mercenary [Lv. 725]"
                NameQuest = "Area1Quest"
                QuestLv = 2
                NameQ = "Mercenary"
                CFrameQ = CFrame.new(-424.080078, 73.0055847, 1836.91589, 0.253544956, -1.42165932e-08, 0.967323601,
                    -6.00147771e-08, 1, 3.04272909e-08, -0.967323601, -6.5768397e-08, 0.253544956)
                CFramePuk = CFrame.new(-938.497314, 80.9546738, 1443.98608, 0.231955677, 0, 0.972726345, -0, 1, -0,
                    -0.972726345, 0, 0.231955677)
            elseif MYLEVEL == 775 or MYLEVEL <= 874 then
                Double_Quest=3
                Ms = "Swan Pirate [Lv. 775]"
                NameQuest = "Area2Quest"
                QuestLv = 1
                NameQ = "Swan Pirate"
                CFrameQ = CFrame.new(632.698608, 73.1055908, 918.666321, -0.0319722369, 8.96074881e-10, -0.999488771,
                    1.36326533e-10, 1, 8.92172336e-10, 0.999488771, -1.07732087e-10, -0.0319722369)
                CFramePuk = CFrame.new(967.233276, 141.309494, 1210.06384, 0.999673784, 5.40161649e-09, -0.0255404469,
                    -7.62258967e-09, 1, -8.68617107e-08, 0.0255404469, 8.7028063e-08, 0.999673784)
            elseif MYLEVEL == 875 or MYLEVEL <= 899 then
                Double_Quest=4
                Ms = "Marine Lieutenant [Lv. 875]"
                NameQuest = "MarineQuest3"
                QuestLv = 1
                NameQ = "Marine Lieutenant."
                CFrameQ = CFrame.new(-2443.04639, 73.0161057, -3220.30225, -0.854058921, -6.13997599e-08, -0.520176232,
                    -1.30658604e-08, 1, -9.65840883e-08, 0.520176232, -7.56919505e-08, -0.854058921)
                CFramePuk = CFrame.new(-2967.00757, 72.9661407, -2972.7478, 0.977851391, 8.27619218e-08, -0.209300488,
                    -6.95268412e-08, 1, 7.05923142e-08, 0.209300488, -5.44767893e-08, 0.977851391)
            elseif MYLEVEL == 900 or MYLEVEL <= 949 then
                Double_Quest=5
                Ms = "Marine Captain [Lv. 900]"
                NameQuest = "MarineQuest3"
                QuestLv = 2
                NameQ = "Marine Captain"
                CFrameQ = CFrame.new(-2443.04639, 73.0161057, -3220.30225, -0.854058921, -6.13997599e-08, -0.520176232,
                    -1.30658604e-08, 1, -9.65840883e-08, 0.520176232, -7.56919505e-08, -0.854058921)
                CFramePuk = CFrame.new(-1818.36401, 93.3760834, -3203.57788, 0.315930545, 4.84752114e-08, 0.948782325,
                    1.37578589e-08, 1, -5.56731905e-08, -0.948782325, 3.06420738e-08, 0.315930545)
            elseif MYLEVEL == 950 or MYLEVEL <= 974 then
                Double_Quest=6
                Ms = "Zombie [Lv. 950]"
                NameQuest = "ZombieQuest"
                QuestLv = 1
                NameQ = "Zombie"
                CFrameQ = CFrame.new(-5492.79395, 48.5151672, -793.710571, 0.321800292, -6.24695815e-08, 0.946807742,
                    4.05616092e-08, 1, 5.21931227e-08, -0.946807742, 2.16082796e-08, 0.321800292)
                CFramePuk = CFrame.new(-5736.03516, 126.031998, -728.026184, 0.0818082988, -5.90035434e-08, 0.996648133,
                    3.5947787e-09, 1, 5.89069167e-08, -0.996648133, -1.23634614e-09, 0.0818082988)
            elseif MYLEVEL == 975 or MYLEVEL <= 999 then
                Double_Quest=7
                Ms = "Vampire [Lv. 975]"
                NameQuest = "ZombieQuest"
                QuestLv = 2
                NameQ = "Vampire"
                CFrameQ = CFrame.new(-5492.79395, 48.5151672, -793.710571, 0.321800292, -6.24695815e-08, 0.946807742,
                    4.05616092e-08, 1, 5.21931227e-08, -0.946807742, 2.16082796e-08, 0.321800292)
                CFramePuk = CFrame.new(-6028.23584, 6.40270138, -1295.4563, 0.667547405, 0, 0.744567394, -0, 1.00000012, -0,
                    -0.744567394, 0, 0.667547405)
            elseif MYLEVEL == 1000 or MYLEVEL <= 1049 then
                Double_Quest=8
                Ms = "Snow Trooper [Lv. 1000]"
                NameQuest = "SnowMountainQuest"
                QuestLv = 1
                NameQ = "Snow Trooper"
                CFrameQ = CFrame.new(605.670532, 401.422028, -5370.10107, 0.459257662, -9.56824509e-10, -0.888303101,
                    5.98925964e-10, 1, -7.67489405e-10, 0.888303101, -1.79552401e-10, 0.459257662)
                CFramePuk = CFrame.new(544.207947, 401.422028, -5309.08887, 0.503866196, -2.06684501e-08, 0.86378175,
                    1.27917943e-09, 1, 2.31816841e-08, -0.86378175, -1.05755351e-08, 0.503866196)
            elseif MYLEVEL == 1050 or MYLEVEL <= 1099 then
                Double_Quest=9
                Ms = "Winter Warrior [Lv. 1050]"
                NameQuest = "SnowMountainQuest"
                QuestLv = 2
                NameQ = "Winter Warrior"
                CFrameQ = CFrame.new(605.670532, 401.422028, -5370.10107, 0.459257662, -9.56824509e-10, -0.888303101,
                    5.98925964e-10, 1, -7.67489405e-10, 0.888303101, -1.79552401e-10, 0.459257662)
                CFramePuk = CFrame.new(1240.86279, 461.108154, -5191.104, 0.528719008, -7.18234645e-08, 0.848796904,
                    2.89169716e-10, 1, 8.44378363e-08, -0.848796904, -4.4398444e-08, 0.528719008)
            elseif MYLEVEL == 1100 or MYLEVEL <= 1124 then
                Double_Quest=10
                Ms = "Lab Subordinate [Lv. 1100]"
                NameQuest = "IceSideQuest"
                QuestLv = 1
                NameQ = "Lab Subordinate"
                CFrameQ = CFrame.new(-6060.10693, 15.9868021, -4904.7876, -0.411000341, -5.06538868e-07, 0.91163528,
                    1.26306062e-07, 1, 6.12581289e-07, -0.91163528, 3.66916197e-07, -0.411000341)
                CFramePuk = CFrame.new(-5833.63379, 48.4371948, -4510.4458, 0.0372838341, 5.56001822e-09, -0.999304712,
                    -6.95599089e-09, 1, 5.30436006e-09, 0.999304712, 6.75338763e-09, 0.0372838341)
            elseif MYLEVEL == 1125 or MYLEVEL <= 1174 then
                Double_Quest=11
                Ms = "Horned Warrior [Lv. 1125]"
                NameQuest = "IceSideQuest"
                QuestLv = 2
                NameQ = "Horned Warrior"
                CFrameQ = CFrame.new(-6060.10693, 15.9868021, -4904.7876, -0.411000341, -5.06538868e-07, 0.91163528,
                    1.26306062e-07, 1, 6.12581289e-07, -0.91163528, 3.66916197e-07, -0.411000341)
                CFramePuk = CFrame.new(-6168.15918, 42.7079964, -6020.96826, -0.744210601, 2.41774178e-09, -0.667945027,
                    -2.3336304e-09, 1, 6.21975493e-09, 0.667945027, 6.18754425e-09, -0.744210601)
            elseif MYLEVEL == 1175 or MYLEVEL <= 1199 then
                Double_Quest=12
                Ms = "Magma Ninja [Lv. 1175]"
                NameQuest = "FireSideQuest"
                QuestLv = 1
                NameQ = "Magma Ninja"
                CFrameQ = CFrame.new(-5429.68359, 15.9517593, -5296.70215, 0.919959962, -6.00166317e-08, -0.392012328,
                    2.29238974e-08, 1, -9.93018858e-08, 0.392012328, 8.23673076e-08, 0.919959962)
                CFramePuk = CFrame.new(-5404.85449, 22.8623676, -5896.09033, -0.519595861, 4.74720929e-09, 0.854412138,
                    1.52255595e-08, 1, 3.70304742e-09, -0.854412138, 1.49329917e-08, -0.519595861)
            elseif MYLEVEL == 1200 or MYLEVEL <= 1249 then
                Double_Quest=13
                Ms = "Lava Pirate [Lv. 1200]"
                NameQuest = "FireSideQuest"
                QuestLv = 2
                NameQ = "Lava Pirate"
                CFrameQ = CFrame.new(-5429.68359, 15.9517593, -5296.70215, 0.919959962, -6.00166317e-08, -0.392012328,
                    2.29238974e-08, 1, -9.93018858e-08, 0.392012328, 8.23673076e-08, 0.919959962)
                CFramePuk = CFrame.new(-5075.1958, 16.1485081, -4814.36133, -0.800640523, -1.06090866e-07, 0.599145055,
                    -6.59776447e-08, 1, 8.89041587e-08, -0.599145055, 3.16500923e-08, -0.800640523)
            elseif MYLEVEL == 1250 or MYLEVEL <= 1274 then
                Double_Quest=14
                Ms = "Ship Deckhand [Lv. 1250]"
                NameQuest = "ShipQuest1"
                QuestLv = 1
                NameQ = "Ship Deckhand"
                CFrameQ = CFrame.new(1038.67456, 125.057098, 32911.3477, 0.120709591, 5.22710089e-08, -0.992687881,
                    7.9174507e-09, 1, 5.36187876e-08, 0.992687881, -1.43318593e-08, 0.120709591)
                CFramePuk = CFrame.new(1215.14063, 125.057114, 33050.7188, 0.527230442, 2.61814961e-08, 0.849722326,
                    -5.66963045e-08, 1, 4.36674741e-09, -0.849722326, -5.04783984e-08, 0.527230442)
            elseif MYLEVEL == 1275 or MYLEVEL <= 1299 then
                Double_Quest=15
                Ms = "Ship Engineer [Lv. 1275]"
                NameQuest = "ShipQuest1"
                QuestLv = 2
                NameQ = "Ship Engineer"
                CFrameQ = CFrame.new(1038.67456, 125.057098, 32911.3477, 0.120709591, 5.22710089e-08, -0.992687881,
                    7.9174507e-09, 1, 5.36187876e-08, 0.992687881, -1.43318593e-08, 0.120709591)
                CFramePuk = CFrame.new(862.985413, 40.4428635, 32867.9492, -0.847809434, 8.49998827e-08, -0.530301034,
                    2.99658929e-08, 1, 1.1237865e-07, 0.530301034, 7.93847335e-08, -0.847809434)
            elseif MYLEVEL == 1300 or MYLEVEL <= 1324 then
                Double_Quest=16
                Ms = "Ship Steward [Lv. 1300]"
                NameQuest = "ShipQuest2"
                QuestLv = 1
                NameQ = "Ship Steward"
                CFrameQ = CFrame.new(969.268311, 125.057121, 33245.2695, -0.85863924, -4.77058464e-08, -0.512580395,
                    -1.49134394e-08, 1, -6.80880134e-08, 0.512580395, -5.08187057e-08, -0.85863924)
                CFramePuk = CFrame.new(923.611511, 129.555984, 33442.3125, 0.997516274, 9.71936913e-08, 0.0704362914,
                    -9.52239958e-08, 1, -3.13219992e-08, -0.0704362914, 2.45369804e-08, 0.997516274)
            elseif MYLEVEL == 1325 or MYLEVEL <= 1349 then
                Double_Quest=17
                Ms = "Ship Officer [Lv. 1325]"
                NameQuest = "ShipQuest2"
                QuestLv = 2
                NameQ = "Ship Officer"
                CFrameQ = CFrame.new(969.268311, 125.057121, 33245.2695, -0.85863924, -4.77058464e-08, -0.512580395,
                    -1.49134394e-08, 1, -6.80880134e-08, 0.512580395, -5.08187057e-08, -0.85863924)
                CFramePuk = CFrame.new(882.275574, 181.057739, 33354.1797, 0.845816016, -3.71928088e-08, -0.533474684,
                    1.28583932e-09, 1, -6.7679359e-08, 0.533474684, 5.65583242e-08, 0.845816016)
            elseif MYLEVEL == 1350 or MYLEVEL <= 1374 then
                Double_Quest=18
                Ms = "Arctic Warrior [Lv. 1350]"
                NameQuest = "FrostQuest"
                QuestLv = 1
                NameQ = "Arctic Warrior"
                CFrameQ = CFrame.new(5669.43506, 28.2117786, -6482.60107, 0.888092756, 1.02705066e-07, 0.459664226,
                    -6.20391774e-08, 1, -1.03572376e-07, -0.459664226, 6.34646895e-08, 0.888092756)
                CFramePuk = CFrame.new(5995.9292, 57.0727844, -6184.98926, 0.706337512, 5.23128296e-09, -0.707875192,
                    -2.2285974e-08, 1, -1.48474424e-08, 0.707875192, 2.62629936e-08, 0.706337512)
            elseif MYLEVEL == 1375 or MYLEVEL <= 1424 then
                Double_Quest=19
                Ms = "Snow Lurker [Lv. 1375]"
                NameQuest = "FrostQuest"
                QuestLv = 2
                NameQ = "Snow Lurker"
                CFrameQ = CFrame.new(5669.43506, 28.2117786, -6482.60107, 0.888092756, 1.02705066e-07, 0.459664226,
                    -6.20391774e-08, 1, -1.03572376e-07, -0.459664226, 6.34646895e-08, 0.888092756)
                CFramePuk = CFrame.new(5516.27539, 60.5209846, -6830.82764, 0.219563305, -7.8544824e-09, 0.975598276,
                    4.69439376e-09, 1, 6.99444236e-09, -0.975598276, 3.04411962e-09, 0.219563305)
            elseif MYLEVEL == 1425 or MYLEVEL <= 1449 then
                Double_Quest=20
                Ms = "Sea Soldier [Lv. 1425]"
                NameQuest = "ForgottenQuest"
                QuestLv = 1
                NameQ = "Sea Soldier"
                CFrameQ = CFrame.new(-3053.97339, 236.846283, -10146.1484, -0.999963522, -2.10707256e-08, -0.00854360498,
                    -2.09657198e-08, 1, -1.23802275e-08, 0.00854360498, -1.22006529e-08, -0.999963522)
                CFramePuk = CFrame.new(-3026.54834, 29.5403671, -9758.74316, -0.999909937, 1.71713896e-08, -0.0134194754,
                    1.68009748e-08, 1, 2.7715517e-08, 0.0134194754, 2.74875607e-08, -0.999909937)
            elseif MYLEVEL >= 1450 then
                Double_Quest=21
                Ms = "Water Fighter [Lv. 1450]"
                NameQuest = "ForgottenQuest"
                QuestLv = 2
                NameQ = "Water Fighter"
                CFrameQ = CFrame.new(-3053.97339, 236.846283, -10146.1484, -0.999963522, -2.10707256e-08, -0.00854360498,
                    -2.09657198e-08, 1, -1.23802275e-08, 0.00854360498, -1.22006529e-08, -0.999963522)
                CFramePuk = CFrame.new(-3262.00098, 298.699615, -10553.6943, -0.233570755, -4.57538185e-08, 0.972339869,
                    -5.80986068e-08, 1, 3.30992194e-08, -0.972339869, -4.87605725e-08, -0.233570755)
            end
        end
        if ThirdSea then
            if MYLEVEL == 1500 or MYLEVEL <= 1524 then
                Double_Quest=1
                Ms = "Pirate Millionaire [Lv. 1500]"
                NameQuest = "PiratePortQuest"
                QuestLv = 1
                NameQ = "Pirate Millionaire"
                CFrameQ = CFrame.new(-288.998016, 43.7932205, 5577.68994, -0.943210304, -8.05650799e-08, 0.332196265,
                    -9.89928779e-08, 1, -3.85495724e-08, -0.332196265, -6.92454165e-08, -0.943210304)
                CFramePuk = CFrame.new(-91.8906479, 75.3287811, 5647.7002, 0.571274579, 8.47636343e-08, -0.820758998,
                    -9.5655281e-08, 1, 3.66955462e-08, 0.820758998, 5.75466998e-08, 0.571274579)
            elseif MYLEVEL == 1525 or MYLEVEL <= 1574 then
                Double_Quest=2
                Ms = "Pistol Billionaire [Lv. 1525]"
                NameQuest = "PiratePortQuest"
                QuestLv = 2
                NameQ = "Pistol Billionaire"
                CFrameQ = CFrame.new(-288.998016, 43.7932205, 5577.68994, -0.943210304, -8.05650799e-08, 0.332196265,
                    -9.89928779e-08, 1, -3.85495724e-08, -0.332196265, -6.92454165e-08, -0.943210304)
                CFramePuk = CFrame.new(-740.71814, 130.458511, 5869.8623, 0.26613301, -6.96497509e-08, 0.963936329,
                    -2.79989738e-08, 1, 7.99857816e-08, -0.963936329, -4.82760854e-08, 0.26613301)
            elseif MYLEVEL == 1575 or MYLEVEL <= 1599 then
                Double_Quest=3
                Ms = "Dragon Crew Warrior [Lv. 1575]"
                NameQuest = "AmazonQuest"
                QuestLv = 1
                NameQ = "Dragon Crew Warrior"
                CFrameQ = CFrame.new(5834.86035, 51.3513641, -1103.34705, -0.919929087, 6.43650253e-08, 0.392084718,
                    7.08298344e-08, 1, 2.02354311e-09, -0.392084718, 2.96328135e-08, -0.919929087)
                CFramePuk = CFrame.new(6498.88623, 51.4962921, -1011.49811, -0.844736993, -1.62814184e-09, -0.535181701,
                    4.04657037e-08, 1, -6.69137634e-08, 0.535181701, -7.81810314e-08, -0.844736993)
            elseif MYLEVEL == 1600 or MYLEVEL <= 1624 then
                Double_Quest=4
                Ms = "Dragon Crew Archer [Lv. 1600]"
                NameQuest = "AmazonQuest"
                QuestLv = 2
                NameQ = "Dragon Crew Archer"
                CFrameQ = CFrame.new(5834.86035, 51.3513641, -1103.34705, -0.919929087, 6.43650253e-08, 0.392084718,
                    7.08298344e-08, 1, 2.02354311e-09, -0.392084718, 2.96328135e-08, -0.919929087)
                CFramePuk = CFrame.new(6608.45605, 378.396393, 235.665527, -0.647212744, -5.41171872e-08, 0.762309432,
                    -5.96274674e-08, 1, 2.0366441e-08, -0.762309432, -3.22731637e-08, -0.647212744)
            elseif MYLEVEL == 1625 or MYLEVEL <= 1649 then
                Double_Quest=5
                Ms = "Female Islander [Lv. 1625]"
                NameQuest = "AmazonQuest2"
                QuestLv = 1
                NameQ = "Female Islander"
                CFrameQ = CFrame.new(5445.11426, 601.603638, 751.129517, -0.346766561, 5.00326642e-08, -0.937951446,
                    4.48732145e-08, 1, 3.67525779e-08, 0.937951446, -2.93443314e-08, -0.346766561)
                CFramePuk = CFrame.new(4758.92871, 730.33374, 800.998047, -0.100775175, -5.07539504e-08, -0.994909227,
                    -2.28484591e-08, 1, -4.86993095e-08, 0.994909227, 1.78244619e-08, -0.100775175)
            elseif MYLEVEL == 1650 or MYLEVEL <= 1699 then
                Double_Quest=6
                Ms = "Giant Islander [Lv. 1650]"
                NameQuest = "AmazonQuest2"
                QuestLv = 2
                NameQ = "Giant Islander"
                CFrameQ = CFrame.new(5445.11426, 601.603638, 751.129517, -0.346766561, 5.00326642e-08, -0.937951446,
                    4.48732145e-08, 1, 3.67525779e-08, 0.937951446, -2.93443314e-08, -0.346766561)
                CFramePuk = CFrame.new(4736.1333, 601.373596, -123.942299, -0.651415646, 1.13692966e-08, -0.758721054,
                    1.02050288e-08, 1, 6.2230785e-09, 0.758721054, -3.6889598e-09, -0.651415646)
            elseif MYLEVEL == 1700 or MYLEVEL <= 1724 then
                Double_Quest=7
                Ms = "Marine Commodore [Lv. 1700]"
                NameQuest = "MarineTreeIsland"
                QuestLv = 1
                NameQ = "Marine Commodore"
                CFrameQ = CFrame.new(2180.83911, 28.7054462, -6739.44824, 0.977863014, 6.92042956e-09, -0.20924598,
                    -1.01339639e-08, 1, -1.42855736e-08, 0.20924598, 1.60898246e-08, 0.977863014)
                CFramePuk = CFrame.new(2447, 73.1255493, -7470, 1, 4.06989891e-08, 4.79087976e-15, -4.06989891e-08, 1,
                    2.86651343e-08, -3.62423799e-15, -2.86651343e-08, 1)
            elseif MYLEVEL == 1725 or MYLEVEL <= 1774 then
                Double_Quest=8
                Ms = "Marine Rear Admiral [Lv. 1725]"
                NameQuest = "MarineTreeIsland"
                QuestLv = 2
                NameQ = "Marine Rear Admiral"
                CFrameQ = CFrame.new(2180.83911, 28.7054462, -6739.44824, 0.977863014, 6.92042956e-09, -0.20924598,
                    -1.01339639e-08, 1, -1.42855736e-08, 0.20924598, 1.60898246e-08, 0.977863014)
                CFramePuk = CFrame.new(3660.3833, 160.524063, -6971.11328, 0.771100104, -4.33134666e-08, -0.636713922,
                    -7.22266069e-09, 1, -7.67736665e-08, 0.636713922, 6.37989501e-08, 0.771100104)
            elseif MYLEVEL == 1775 or MYLEVEL <= 1800 then
                Double_Quest=9
                Ms = "Fishman Raider [Lv. 1775]"
                NameQuest = "DeepForestIsland3"
                QuestLv = 1
                NameQ = "Fishman Raider"
                CFrameQ = CFrame.new(-10582.7578, 331.762634, -8758.56543, 0.911287963, 8.23484143e-08, -0.411769718,
                    -7.27268628e-08, 1, 3.90346848e-08, 0.411769718, -5.62511859e-09, 0.911287963)
                CFramePuk = CFrame.new(-10615.6611, 331.762634, -8446.38574, 0.30275172, -4.96152719e-09, -0.953069448,
                    -2.92618618e-09, 1, -6.13537132e-09, 0.953069448, 4.64635308e-09, 0.30275172)
            elseif MYLEVEL == 1800 or MYLEVEL <= 1824 then
                Double_Quest=10
                Ms = "Fishman Captain [Lv. 1800]"
                NameQuest = "DeepForestIsland3"
                QuestLv = 2
                NameQ = "Fishman Captain"
                CFrameQ = CFrame.new(-10582.7578, 331.762634, -8758.56543, 0.911287963, 8.23484143e-08, -0.411769718,
                    -7.27268628e-08, 1, 3.90346848e-08, 0.411769718, -5.62511859e-09, 0.911287963)
                CFramePuk = CFrame.new(-11040.3467, 331.762634, -8957.75684, -0.990780294, -5.54384094e-08, 0.135478467,
                    -4.7334634e-08, 1, 6.30372483e-08, -0.135478467, 5.60432376e-08, -0.990780294)
            elseif MYLEVEL == 1825 or MYLEVEL <= 1849 then
                Double_Quest=11
                Ms = "Forest Pirate [Lv. 1825]"
                NameQuest = "DeepForestIsland"
                QuestLv = 1
                NameQ = "Forest Pirate"
                CFrameQ = CFrame.new(-13233.2686, 332.378143, -7627.66455, -0.905921221, 2.69652856e-09, 0.423446268,
                    2.31737229e-09, 1, -1.41026579e-09, -0.423446268, -2.96307007e-10, -0.905921221)
                CFramePuk = CFrame.new(-13479, 332.378143, -7905, 1, -1.27257813e-08, 2.41825958e-15, 1.27257813e-08, 1,
                    -8.67651977e-08, -1.3141047e-15, 8.67651977e-08, 1)
            elseif MYLEVEL == 1850 or MYLEVEL <= 1899 then
                Double_Quest=12
                Ms = "Mythological Pirate [Lv. 1850]"
                NameQuest = "DeepForestIsland"
                QuestLv = 2
                NameQ = "Mythological Pirate"
                CFrameQ = CFrame.new(-13233.2686, 332.378143, -7627.66455, -0.905921221, 2.69652856e-09, 0.423446268,
                    2.31737229e-09, 1, -1.41026579e-09, -0.423446268, -2.96307007e-10, -0.905921221)
                CFramePuk = CFrame.new(-13676.1553, 469.788086, -6999.65527, 0.693832397, -2.62738986e-08, 0.720136523,
                    -4.52658462e-08, 1, 8.00970454e-08, -0.720136523, -8.8171511e-08, 0.693832397)
            elseif MYLEVEL == 1900 or MYLEVEL <= 1924 then
                Double_Quest=13
                Ms = "Jungle Pirate [Lv. 1900]"
                NameQuest = "DeepForestIsland2"
                QuestLv = 1
                NameQ = "Jungle Pirate"
                CFrameQ = CFrame.new(-12682.1279, 390.860687, -9901.89746, 0.00872628205, 1.59673574e-09, -0.999961913,
                    -5.25600941e-09, 1, 1.55092938e-09, 0.999961913, 5.2422755e-09, 0.00872628205)
                CFramePuk = CFrame.new(-12107, 331.738281, -10549, 1, -2.50327403e-09, -6.22370418e-15, 2.50327403e-09, 1,
                    8.81249651e-09, 6.20164405e-15, -8.81249651e-09, 1)
            elseif MYLEVEL == 1925 or MYLEVEL <= 1974 then
                Double_Quest=14
                Ms = "Musketeer Pirate [Lv. 1925]"
                NameQuest = "DeepForestIsland2"
                QuestLv = 2
                NameQ = "Musketeer Pirate"
                CFrameQ = CFrame.new(-12682.1279, 390.860687, -9901.89746, 0.00872628205, 1.59673574e-09, -0.999961913,
                    -5.25600941e-09, 1, 1.55092938e-09, 0.999961913, 5.2422755e-09, 0.00872628205)
                CFramePuk = CFrame.new(-13485.2305, 432.682373, -9857.01074, 0.994504631, 1.2369239e-08, -0.104692325,
                    -8.4907642e-10, 1, 1.1008283e-07, 0.104692325, -1.09388999e-07, 0.994504631)
            elseif MYLEVEL == 1975 or MYLEVEL <= 1999 then
                Double_Quest=15
                Ms = "Reborn Skeleton [Lv. 1975]"
                NameQuest = "HauntedQuest1"
                QuestLv = 1
                NameQ = "Reborn Skeleton"
                CFrameQ = CFrame.new(-9482.11035, 142.104828, 5566.32861, 0.0620567501, -4.18429273e-08, -0.998072624,
                    -3.89895867e-08, 1, -4.43479706e-08, 0.998072624, 4.1666528e-08, 0.0620567501)
                CFramePuk = CFrame.new(-8762.33496, 142.104828, 6015.7627, -0.999993861, -2.26600214e-08, 0.00350279221,
                    -2.28456738e-08, 1, -5.29611519e-08, -0.00350279221, -5.30408499e-08, -0.999993861)
            elseif MYLEVEL == 2000 or MYLEVEL <= 2024 then
                Double_Quest=16
                Ms = "Living Zombie [Lv. 2000]"
                NameQuest = "HauntedQuest1"
                QuestLv = 2
                NameQ = "Living Zombie"
                CFrameQ = CFrame.new(-9482.11035, 142.104828, 5566.32861, 0.0620567501, -4.18429273e-08, -0.998072624,
                    -3.89895867e-08, 1, -4.43479706e-08, 0.998072624, 4.1666528e-08, 0.0620567501)
                CFramePuk = CFrame.new(-10099.1494, 138.626678, 5930.86279, 0.241616711, -9.62791873e-08, -0.970371783,
                    5.61582709e-08, 1, -8.52357971e-08, 0.970371783, -3.39000081e-08, 0.241616711)
            elseif MYLEVEL == 2025 or MYLEVEL <= 2049 then
                Double_Quest=17
                Ms = "Demonic Soul [Lv. 2025]"
                NameQuest = "HauntedQuest2"
                QuestLv = 1
                NameQ = "Demonic Soul"
                CFrameQ = CFrame.new(-9514.25195, 172.104828, 6077.22998, 0.0446508788, -7.60616636e-09, 0.999002635,
                    7.97889257e-08, 1, 4.04755696e-09, -0.999002635, 7.95286255e-08, 0.0446508788)
                CFramePuk = CFrame.new(-9513.54199, 172.104828, 6143.45459, -0.777332306, -2.16450324e-08, -0.62909019,
                    -5.07872073e-08, 1, 2.83480883e-08, 0.62909019, 5.39856195e-08, -0.777332306)
            elseif MYLEVEL == 2050 or MYLEVEL <= 2074 then
                Double_Quest=18
                Ms = "Posessed Mummy [Lv. 2050]"
                NameQuest = "HauntedQuest2"
                QuestLv = 2
                NameQ = "Posessed Mummy"
                CFrameQ = CFrame.new(-9514.25195, 172.104828, 6077.22998, 0.0446508788, -7.60616636e-09, 0.999002635,
                    7.97889257e-08, 1, 4.04755696e-09, -0.999002635, 7.95286255e-08, 0.0446508788)
                CFramePuk = CFrame.new(-9580.24609, 5.79254198, 6190.47852, 0.462460369, 5.16216367e-08, -0.886639953,
                    -7.72594788e-08, 1, 1.79240605e-08, 0.886639953, 6.0212173e-08, 0.462460369)
            elseif MYLEVEL == 2075 or MYLEVEL <= 2099 then
                Double_Quest=19
                Ms = "Peanut Scout [Lv. 2075]"
                NameQuest = "NutsIslandQuest"
                QuestLv = 1
                NameQ = "Peanut Scout"
                CFrameQ = CFrame.new(-2103.18872, 38.1041794, -10193.7656, 0.7310462, 2.46138327e-08, 0.682327926,
                    -5.02823738e-09, 1, -3.06860635e-08, -0.682327926, 1.90020231e-08, 0.7310462)
                CFramePuk = CFrame.new(-2221.45996, 38.103817, -10086.0762, -0.994582355, 2.09503472e-08, 0.103951879,
                    2.41223095e-08, 1, 2.92565758e-08, -0.103951879, 3.16056337e-08, -0.994582355)
            elseif MYLEVEL == 2100 or MYLEVEL <= 2124 then
                Double_Quest=20
                Ms = "Peanut President [Lv. 2100]"
                NameQuest = "NutsIslandQuest"
                QuestLv = 2
                NameQ = "Peanut President"
                CFrameQ = CFrame.new(-2103.18872, 38.1041794, -10193.7656, 0.7310462, 2.46138327e-08, 0.682327926,
                    -5.02823738e-09, 1, -3.06860635e-08, -0.682327926, 1.90020231e-08, 0.7310462)
                CFramePuk = CFrame.new(-2171.88647, 88.2396011, -10531.9512, 0.691500723, 5.31482591e-08, -0.722375751,
                    -2.70291771e-08, 1, 4.7700329e-08, 0.722375751, -1.34595908e-08, 0.691500723)
            elseif MYLEVEL == 2125 or MYLEVEL <= 2149 then
                Double_Quest=21
                Ms = "Ice Cream Chef [Lv. 2125]"
                NameQuest = "IceCreamIslandQuest"
                QuestLv = 1
                NameQ = "Ice Cream Chef"
                CFrameQ = CFrame.new(-820.991455, 65.8195343, -10965.4316, 0.832442105, 3.44203599e-08, -0.554112017,
                    -3.14893249e-08, 1, 1.48116621e-08, 0.554112017, 5.11876364e-09, 0.832442105)
                CFramePuk = CFrame.new(-761.110657, 164.200974, -10929.7031, -0.903523564, -2.8124143e-08, 0.428538442,
                    -5.52620127e-09, 1, 5.39766987e-08, -0.428538442, 4.64010306e-08, -0.903523564)
            elseif MYLEVEL == 2150 or MYLEVEL <= 2199 then
                Double_Quest=22
                Ms = "Ice Cream Commander [Lv. 2150]"
                NameQuest = "IceCreamIslandQuest"
                QuestLv = 2
                NameQ = "Ice Cream Commander"
                CFrameQ = CFrame.new(-820.991455, 65.8195343, -10965.4316, 0.832442105, 3.44203599e-08, -0.554112017,
                    -3.14893249e-08, 1, 1.48116621e-08, 0.554112017, 5.11876364e-09, 0.832442105)
                CFramePuk = CFrame.new(-683.515137, 97.7532196, -11270.5254, -0.249526113, -3.42524373e-08, -0.968368053,
                    -4.59147245e-08, 1, -2.35401334e-08, 0.968368053, 3.85884746e-08, -0.249526113)
            elseif MYLEVEL == 2200 or MYLEVEL <= 2224 then
                Double_Quest=23
                Ms = "Cookie Crafter [Lv. 2200]"
                NameQuest = "CakeQuest1"
                QuestLv = 1
                NameQ = "Cookie Crafter"
                CFrameQ = CFrame.new(-2021.28113, 37.7982178, -12027.1602, 0.876975715, 2.42050024e-08, 0.480534643,
                    -1.83145179e-08, 1, -1.69469878e-08, -0.480534643, 6.06133632e-09, 0.876975715)
                CFramePuk = CFrame.new(-2362.1604, 37.7981148, -12116.2031, 0.428214997, 1.03298156e-07, 0.903676867,
                    -1.24923467e-08, 1, -1.08389123e-07, -0.903676867, 3.51248026e-08, 0.428214997)
            elseif MYLEVEL == 2225 or MYLEVEL <= 2249 then
                Double_Quest=24
                Ms = "Cake Guard [Lv. 2225]"
                NameQuest = "CakeQuest1"
                QuestLv = 2
                NameQ = "Cake Guard"
                CFrameQ = CFrame.new(-2021.28113, 37.7982178, -12027.1602, 0.876975715, 2.42050024e-08, 0.480534643,
                    -1.83145179e-08, 1, -1.69469878e-08, -0.480534643, 6.06133632e-09, 0.876975715)
                CFramePuk = CFrame.new(-1560.17944, 37.7981339, -12440.5781, -0.560352206, 1.90654585e-08, -0.828254402,
                    6.60573107e-08, 1, -2.16719656e-08, 0.828254402, -6.68561952e-08, -0.560352206)
            elseif MYLEVEL == 2250 or MYLEVEL <= 2274 then
                Double_Quest=25
                Ms = "Baking Staff [Lv. 2250]"
                NameQuest = "CakeQuest2"
                QuestLv = 1
                NameQ = "Baking Staff"
                CFrameQ = CFrame.new(-1929.3186, 37.7981339, -12843.3857, -0.994816065, 6.2958283e-09, 0.101690687,
                    6.02614314e-09, 1, -2.95921043e-09, -0.101690687, -2.33106734e-09, -0.994816065)
                CFramePuk = CFrame.new(-1874.04688, 74.015831, -13002.7959, 0.958144426, -9.20437699e-08, -0.286285222,
                    1.05663617e-07, 1, 3.21261275e-08, 0.286285222, -6.10314004e-08, 0.958144426)
            elseif MYLEVEL == 2275 or MYLEVEL <= 2299 then
                Double_Quest=26
                Ms = "Head Baker [Lv. 2275]"
                NameQuest = "CakeQuest2"
                QuestLv = 2
                NameQ = "Head Baker"
                CFrameQ = CFrame.new(-1929.3186, 37.7981339, -12843.3857, -0.994816065, 6.2958283e-09, 0.101690687,
                    6.02614314e-09, 1, -2.95921043e-09, -0.101690687, -2.33106734e-09, -0.994816065)
                CFramePuk = CFrame.new(-2205.25171, 108.351257, -12784.6475, 0.999649942, 1.09295986e-08, -0.0264567528,
                    -9.22357479e-09, 1, 6.46055156e-08, 0.0264567528, -6.43388702e-08, 0.999649942)
            elseif MYLEVEL == 2300 or MYLEVEL <= 2324 then
                Double_Quest=27
                Ms = "Cocoa Warrior [Lv. 2300]"
                NameQuest = "ChocQuest1"
                QuestLv = 1
                NameQ = "Cocoa Warrior"
                CFrameQ = CFrame.new(231.562515, 24.7342396, -12196.9277, 0.996608198, -4.87148775e-08, -0.0822927728,
                    4.61355079e-08, 1, -3.32453354e-08, 0.0822927728, 2.93359523e-08, 0.996608198)
                CFramePuk = CFrame.new(-26.0082874, 24.7343502, -12253.001, -0.17375651, 7.9442728e-08, 0.984788656,
                    1.18449632e-08, 1, -7.85798946e-08, -0.984788656, -1.98898231e-09, -0.17375651)
            elseif MYLEVEL == 2325 or MYLEVEL <= 2349 then
                Double_Quest=28
                Ms = "Chocolate Bar Battler [Lv. 2325]"
                NameQuest = "ChocQuest1"
                QuestLv = 2
                NameQ = "Chocolate Bar Battler"
                CFrameQ = CFrame.new(231.562515, 24.7342396, -12196.9277, 0.996608198, -4.87148775e-08, -0.0822927728,
                    4.61355079e-08, 1, -3.32453354e-08, 0.0822927728, 2.93359523e-08, 0.996608198)
                CFramePuk = CFrame.new(715.227661, 64.5699463, -12601.4971, 0.375136077, -3.84623213e-08, 0.926969767,
                    1.12107639e-08, 1, 3.69556403e-08, -0.926969767, -3.47135498e-09, 0.375136077)
            elseif MYLEVEL == 2350 or MYLEVEL <= 2374 then
                Double_Quest=29
                Ms = "Sweet Thief [Lv. 2350]"
                NameQuest = "ChocQuest2"
                QuestLv = 1
                NameQ = "Sweet Thief"
                CFrameQ = CFrame.new(147.670837, 24.7938328, -12775.2656, -0.274139136, 7.20163911e-08, -0.961690068,
                    7.48291242e-08, 1, 5.35544693e-08, 0.961690068, -5.72810492e-08, -0.274139136)
                CFramePuk = CFrame.new(59.2454491, 57.2388878, -12634.1523, 0.97673136, -3.85135479e-08, 0.214466438,
                    3.43798909e-08, 1, 2.30041923e-08, -0.214466438, -1.50955834e-08, 0.97673136)
            elseif MYLEVEL == 2375 or MYLEVEL <= 2400 then
                Double_Quest=30
                Ms = "Candy Rebel [Lv. 2375]"
                NameQuest = "ChocQuest2"
                QuestLv = 2
                NameQ = "Candy Rebel"
                CFrameQ = CFrame.new(147.670837, 24.7938328, -12775.2656, -0.274139136, 7.20163911e-08, -0.961690068,
                    7.48291242e-08, 1, 5.35544693e-08, 0.961690068, -5.72810492e-08, -0.274139136)
                CFramePuk = CFrame.new(72.7375183, 24.7938499, -12939.2383, -0.87948513, 9.16761138e-08, -0.47592634,
                    7.88268579e-08, 1, 4.69590802e-08, 0.47592634, 3.78403309e-09, -0.87948513)
            elseif MYLEVEL == 2400 or MYLEVEL <= 2425 then
                Double_Quest=31
                Ms = "Candy Pirate [Lv. 2400]"
                NameQuest = "CandyQuest1"
                QuestLv = 1
                NameQ = "Candy Pirate"
                CFrameQ = CFrame.new(-1151.48987, 16.1422901, -14445.6904, -0.316594511, -6.85698254e-08, -0.948560953, -2.05343067e-08, 1, -6.54346692e-08, 0.948560953, -1.23821675e-09, -0.316594511)
                CFramePuk = CFrame.new(-1408.46521, 16.1423531, -14552.2041, 0.90175873, -8.17216943e-08, -0.432239741, 7.81264475e-08, 1, -2.60746162e-08, 0.432239741, -1.02563433e-08, 0.90175873)
        elseif MYLEVEL >=  2426 then
                Double_Quest=32
                Ms = "Snow Demon [Lv. 2425]"
                NameQuest = "CandyQuest1"
                QuestLv = 2
                NameQ = "Snow Demon"
                CFrameQ = CFrame.new(-1151.48987, 16.1422901, -14445.6904, -0.316594511, -6.85698254e-08, -0.948560953, -2.05343067e-08, 1, -6.54346692e-08, 0.948560953, -1.23821675e-09, -0.316594511)
                CFramePuk = CFrame.new(-777.070862, 23.5809536, -14453.0078, 0.33384338, 0, -0.942628562, 0, 1, 0, 0.942628562, 0, 0.33384338)
            end
        end
    end

function Check_Double_Quest(Double_Quest)
    if OldWolrd then
        if Double_Quest==1 then
            Ms = "Bandit [Lv. 5]"
            NameQuest = "BanditQuest1"
            QuestLv = 1
            NameQ = "Bandit"
            CFrameQ = CFrame.new(1060.0158691406, 16.424287796021, 1547.9769287109)
            CFramePuk = CFrame.new(1073.86414, 16.2736206, 1612.17163, -0.695649207, 0, -0.718381643, 0, 1, 0,
                0.718381643, 0, -0.695649207)
            NM = 'Windmill'
        elseif Double_Quest==2 then
            Ms = "Monkey [Lv. 14]"
            NameQuest = "JungleQuest"
            QuestLv = 1
            NameQ = "Monkey"
            CFrameQ = CFrame.new(-1601.52808, 36.9774551, 152.812317, -0.0892550573, -7.99012057e-08, -0.996008813,
                -4.66281733e-08, 1, -7.60429089e-08, 0.996008813, 3.96548572e-08, -0.0892550573)
            CFramePuk = CFrame.new(-1609.71216, 39.8521576, 123.384674, 0.708323717, 6.74341152e-08, 0.705887735,
                -1.86098941e-08, 1, -7.68568071e-08, -0.705887735, 4.13030072e-08, 0.708323717)
        elseif Double_Quest==3 then
            magbring = 240
            Ms = "Gorilla [Lv. 20]"
            NameQuest = "JungleQuest"
            QuestLv = 2
            NameQ = "Gorilla"
            CFrameQ = CFrame.new(-1600.24353, 36.8521347, 153.224792, 0.0664860159, 1.09421023e-07, -0.997787356,
                9.55680779e-09, 1, 1.10300476e-07, 0.997787356, -1.68691017e-08, 0.0664860159)
            CFramePuk = CFrame.new(-1260.29321, 18.6214619, -398.3508, 0.816335142, 5.76316722e-07, -0.577578545,
                8.32609999e-08, 1, 1.11549434e-06, 0.577578545, -9.58707005e-07, 0.816335142)
        elseif Double_Quest==4 then
            Ms = "Pirate [Lv. 35]"
            NameQuest = "BuggyQuest1"
            QuestLv = 1
            NameQ = "Pirate"
            CFrameQ = CFrame.new(-1141.07483, 4.10001802, 3831.5498, 0.965929627, -0, -0.258804798, 0, 1, -0,
                0.258804798, 0, 0.965929627)
            CFramePuk = CFrame.new(-1141.07483, 4.10001802, 3831.5498, 0.965929627, -0, -0.258804798, 0, 1, -0,
                0.258804798, 0, 0.965929627)
        elseif Double_Quest==5 then
            Ms = "Brute [Lv. 45]"
            NameQuest = "BuggyQuest1"
            QuestLv = 2
            NameQ = "Brute"
            CFrameQ = CFrame.new(-1141.07483, 4.10001802, 3831.5498, 0.965929627, -0, -0.258804798, 0, 1, -0,
                0.258804798, 0, 0.965929627)
            CFramePuk = CFrame.new(-1144.44861, 90.5594559, 4307.25928, -0.998438537, 0, 0.0558618344, 0, 1, 0,
                -0.0558618344, 0, -0.998438537)
        elseif Double_Quest==6 then
            Ms = "Desert Bandit [Lv. 60]"
            NameQuest = "DesertQuest"
            QuestLv = 1
            NameQ = "Desert Bandit"
            CFrameQ = CFrame.new(894.488647, 5.14000702, 4392.43359, 0.819155693, -0, -0.573571265, 0, 1, -0,
                0.573571265, 0, 0.819155693)
            CFramePuk = CFrame.new(894.488647, 5.14000702, 4392.43359, 0.819155693, -0, -0.573571265, 0, 1, -0,
                0.573571265, 0, 0.819155693)
        elseif Double_Quest==7 then
            Ms = "Desert Officer [Lv. 70]"
            NameQuest = "DesertQuest"
            QuestLv = 2
            NameQ = "Desert Officer"
            CFrameQ = CFrame.new(894.488647, 5.14000702, 4392.43359, 0.819155693, -0, -0.573571265, 0, 1, -0,
                0.573571265, 0, 0.819155693)
            CFramePuk = CFrame.new(1580.03198, 4.61375761, 4366.86426)
        elseif Double_Quest==8 then
            Ms = "Snow Bandit [Lv. 90]"
            NameQuest = "SnowQuest"
            QuestLv = 1
            NameQ = "Snow Bandit"
            CFrameQ = CFrame.new(1384.01538, 87.272789, -1296.28137, 0.462413222, -7.79864777e-08, -0.88666451,
                -1.42050363e-08, 1, -9.53630916e-08, 0.88666451, 5.6692258e-08, 0.462413222)
            CFramePuk = CFrame.new(1372.84326, 105.990303, -1422.19507, 0.719091773, -2.12436309e-08, 0.694915235,
                9.82151036e-08, 1, -7.10619616e-08, -0.694915235, 1.19351228e-07, 0.719091773)
        elseif Double_Quest==9 then
            Ms = "Snowman [Lv. 100]"
            NameQuest = "SnowQuest"
            QuestLv = 2
            NameQ = "Snowman"
            CFrameQ = CFrame.new(1384.01538, 87.272789, -1296.28137, 0.462413222, -7.79864777e-08, -0.88666451,
                -1.42050363e-08, 1, -9.53630916e-08, 0.88666451, 5.6692258e-08, 0.462413222)
            CFramePuk = CFrame.new(1220.92712, 138.011871, -1489.01208, 0.389352709, -7.53626693e-07, 0.921088696,
                1.45705499e-07, 1, 7.56600116e-07, -0.921088696, -1.60376572e-07, 0.389352709)
        elseif Double_Quest==10 then
            Ms = "Chief Petty Officer [Lv. 120]"
            NameQuest = "MarineQuest2"
            QuestLv = 1
            NameQ = "Chief Petty Officer"
            CFrameQ = CFrame.new(-5034.64893, 28.6520348, 4324.53369, -0.0616381466, 5.83357576e-08, 0.998098552,
                -1.59750098e-08, 1, -5.9433436e-08, -0.998098552, -1.96080023e-08, -0.0616381466)
            CFramePuk = CFrame.new(-4863.61328, 22.6520348, 4306.39307, 0.536051273, 7.00434066e-09, -0.844185412,
                -5.8011751e-10, 1, 7.92878918e-09, 0.844185412, -3.76051057e-09, 0.536051273)
        elseif Double_Quest==11 then
            Ms = "Sky Bandit [Lv. 150]"
            NameQuest = "SkyQuest"
            QuestLv = 1
            NameQ = "Sky Bandit"
            CFrameQ = CFrame.new(-4843.2041, 717.669617, -2623.13159, -0.775086224, -1.6359829e-08, -0.631855488,
                -4.10942462e-08, 1, 2.45178793e-08, 0.631855488, 4.49690951e-08, -0.775086224)
            CFramePuk = CFrame.new(-4970.74219, 294.544342, -2890.11353, -0.994874597, -8.61311165e-08, -0.101116329,
                -9.10836278e-08, 1, 4.43614923e-08, 0.101116329, 5.33441664e-08, -0.994874597)
        elseif Double_Quest==12 then
            Ms = "Dark Master [Lv. 175]"
            NameQuest = "SkyQuest"
            QuestLv = 2
            NameQ = "Dark Master"
            CFrameQ = CFrame.new(-4843.2041, 717.669617, -2623.13159, -0.775086224, -1.6359829e-08, -0.631855488,
                -4.10942462e-08, 1, 2.45178793e-08, 0.631855488, 4.49690951e-08, -0.775086224)
            CFramePuk = CFrame.new(-5239.94629, 392.217102, -2208.18335, 0.969297886, -5.95604988e-09, -0.245889395,
                3.87897714e-09, 1, -8.93151775e-09, 0.245889395, 7.70350184e-09, 0.969297886)
        elseif Double_Quest==13 then
            Ms = "Prisoner [Lv. 190]"
            NameQuest = "PrisonerQuest"
            QuestLv = 1
            NameQ = "Prisoner"
            CFrameQ = CFrame.new(5307.95166015625, 1.6809712648391724, 475.1698913574219)
            CFramePuk = CFrame.new(5029.708984375, 68.67806243896484, 445.857177734375)
        elseif Double_Quest==14 then
            Ms = "Dangerous Prisoner [Lv. 210]"
            NameQuest = "PrisonerQuest"
            QuestLv = 2
            NameQ = "Dangerous Prisoner"
            CFrameQ = CFrame.new(5307.95166015625, 1.6809712648391724, 475.1698913574219)
            CFramePuk = CFrame.new(5673.51758, 68.6786652, 783.757629, -0.0514698699, 7.78369369e-08, 0.998674572,
                8.35602094e-08, 1, -7.36337e-08, -0.998674572, 7.96595359e-08, -0.0514698699)
        elseif Double_Quest==15 then
            Ms = "Toga Warrior [Lv. 250]"
            NameQuest = "ColosseumQuest"
            QuestLv = 1
            NameQ = "Toga Warrior"
            CFrameQ = CFrame.new(-1575.72961, 7.38933659, -2983.39453, 0.52762109, -1.48187587e-06, 0.849479854,
                2.69328297e-07, 1, 1.57716818e-06, -0.849479854, -6.0335816e-07, 0.52762109)
            CFramePuk = CFrame.new(-1819.12415, 7.28907108, -2744.02539, 0.547199547, 2.10840998e-08, -0.837002158,
                -1.27399286e-10, 1, 2.51067309e-08, 0.837002158, -1.36317579e-08, 0.547199547)
        elseif Double_Quest==16 then
            Ms = "Military Soldier [Lv. 300]"
            NameQuest = "MagmaQuest"
            QuestLv = 1
            NameQ = "Military Soldier"
            CFrameQ = CFrame.new(-5316.33887, 12.236989, 8517.67285, 0.499506682, -5.08374072e-08, -0.86631006,
                -1.30872131e-08, 1, -6.62286652e-08, 0.86631006, 4.44192452e-08, 0.499506682)
            CFramePuk = CFrame.new(-5419.0752, 10.9255161, 8464.50488, -0.637788415, -4.55103836e-05, 0.770211577,
                7.05542743e-06, 1, 6.49305366e-05, -0.770211577, 4.68461185e-05, -0.637788415)
        elseif Double_Quest==17 then
            Ms = "Military Spy [Lv. 325]"
            NameQuest = "MagmaQuest"
            QuestLv = 2
            NameQ = "Military Spy"
            CFrameQ = CFrame.new(-5316.33887, 12.236989, 8517.67285, 0.499506682, -5.08374072e-08, -0.86631006,
                -1.30872131e-08, 1, -6.62286652e-08, 0.86631006, 4.44192452e-08, 0.499506682)
            CFramePuk = CFrame.new(-5805.42041, 99.5276108, 8782.36719, -0.316935152, -6.4923519e-08, 0.948447227,
                4.12987404e-08, 1, 8.2252896e-08, -0.948447227, 6.52385026e-08, -0.316935152)
        elseif Double_Quest==18 then
            Ms = "Fishman Warrior [Lv. 375]"
            NameQuest = "FishmanQuest"
            QuestLv = 1
            NameQ = "Fishman Warrior"
            CFrameQ = CFrame.new(61122.2422, 18.4716377, 1568.84778, 0.971045971, -1.77007031e-08, 0.238892734,
                4.80190776e-09, 1, 5.45760841e-08, -0.238892734, -5.18487475e-08, 0.971045971)
            CFramePuk = CFrame.new(60898.043, 18.4828224, 1550.9906, -0.0750192106, -4.46996573e-09, 0.997182071,
                3.6461556e-10, 1, 4.51002746e-09, -0.997182071, 7.0192685e-10, -0.0750192106)
            if    (_G.AutoFram) and
                (CFrameQ.Position - game.Players.LocalPlayer.Character.HumanoidRootPart.Position).Magnitude > 3000 then
                game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("requestEntrance",
                    Vector3.new(61163.8516, 5.43263245, 1819.78418, 1, 6.89280011e-09, 9.74497786e-14, -6.89280011e-09,
                        1, 3.38349579e-08, -9.72165599e-14, -3.38349579e-08, 1))
            end
        elseif Double_Quest==19 then
            Ms = "Fishman Commando [Lv. 400]"
            NameQuest = "FishmanQuest"
            QuestLv = 2
            NameQ = "Fishman Commando"
            CFrameQ = CFrame.new(61122.2422, 18.4716377, 1568.84778, 0.971045971, -1.77007031e-08, 0.238892734,
                4.80190776e-09, 1, 5.45760841e-08, -0.238892734, -5.18487475e-08, 0.971045971)
            CFramePuk = CFrame.new(61885.4063, 18.4828224, 1500.37195, 0.722261012, 4.84021889e-08, -0.691620588,
                1.27929427e-08, 1, 8.33434299e-08, 0.691620588, -6.90435726e-08, 0.722261012)
            if    (_G.AutoFram)and
                (CFrameQ.Position - game.Players.LocalPlayer.Character.HumanoidRootPart.Position).Magnitude > 3000 then
                game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("requestEntrance",
                    Vector3.new(61163.8516, 5.43263245, 1819.78418, 1, 6.89280011e-09, 9.74497786e-14, -6.89280011e-09,
                        1, 3.38349579e-08, -9.72165599e-14, -3.38349579e-08, 1))
            end
        elseif Double_Quest==20 then
            Ms = "God's Guard [Lv. 450]"
            NameQuest = "SkyExp1Quest"
            QuestLv = 1
            NameQ = "God's Guard"
            CFrameQ = CFrame.new(-4721.28369, 845.277161, -1954.95154, -0.979754269, -1.72096932e-08, 0.200205252,
                -2.52417198e-09, 1, 7.36076018e-08, -0.200205252, 7.16119786e-08, -0.979754269)
            CFramePuk = CFrame.new(-4630.00635, 866.902954, -1936.76331, -0.656243384, 9.12737941e-12, 0.754549265,
                3.58402819e-09, 1, 3.10498938e-09, -0.754549265, 4.74195483e-09, -0.656243384)
            if    (_G.AutoFram)and
                (CFrameQ.Position - game.Players.LocalPlayer.Character.HumanoidRootPart.Position).Magnitude > 3000 then
                game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("requestEntrance", Vector3.new(
                    -4607.82275, 872.54248, -1667.55688))
            end
        elseif Double_Quest==21 then
            Ms = "Shanda [Lv. 475]"
            NameQuest = "SkyExp1Quest"
            QuestLv = 2
            NameQ = "Shanda"
            CFrameQ = CFrame.new(-7861.79736, 5545.49316, -379.920776, 0.504107952, -1.41941534e-08, -0.863640666,
                -1.31181936e-08, 1, -2.40923566e-08, 0.863640666, 2.34745521e-08, 0.504107952)
            CFramePuk = CFrame.new(-7682.69775, 5607.36279, -445.691833, 0.786274791, -4.48163426e-08, -0.617877364,
                -4.81674345e-09, 1, -7.86622607e-08, 0.617877364, 6.48263239e-08, 0.786274791)
            if    (_G.AutoFram)and
                (CFrameQ.Position - game.Players.LocalPlayer.Character.HumanoidRootPart.Position).Magnitude > 3000 then
                game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("requestEntrance", Vector3.new(
                    -7894.6176757813, 5547.1416015625, -380.29119873047))
            end
        elseif Double_Quest==22 then
            Ms = "Royal Squad [Lv. 525]"
            NameQuest = "SkyExp2Quest"
            QuestLv = 1
            NameQ = "Royal Squad"
            CFrameQ = CFrame.new(-7902.23242, 5635.96387, -1411.96741, -0.0435957126, -2.13718043e-09, 0.999049246,
                4.23562352e-10, 1, 2.15769735e-09, -0.999049246, 5.1722604e-10, -0.0435957126)
            CFramePuk = CFrame.new(-7579.42285, 5628.39111, -1540.75073, -0.0374937952, 1.17099557e-08, 0.999296963,
                -3.30279164e-08, 1, -1.29574085e-08, -0.999296963, -3.34905081e-08, -0.0374937952)
        elseif Double_Quest==23 then
            Ms = "Royal Soldier [Lv. 550]"
            NameQuest = "SkyExp2Quest"
            QuestLv = 2
            NameQ = "Royal Soldier"
            CFrameQ = CFrame.new(-7902.23242, 5635.96387, -1411.96741, -0.0435957126, -2.13718043e-09, 0.999049246,
                4.23562352e-10, 1, 2.15769735e-09, -0.999049246, 5.1722604e-10, -0.0435957126)
            CFramePuk = CFrame.new(-7834.84717, 5681.36182, -1790.76782, -0.102890432, 3.28112684e-08, 0.994692683,
                -6.45397762e-08, 1, -3.96622966e-08, -0.994692683, -6.82781121e-08, -0.102890432)
        elseif Double_Quest==24 then
            Ms = "Galley Pirate [Lv. 625]"
            NameQuest = "FountainQuest"
            QuestLv = 1
            NameQ = "Galley Pirate"
            CFrameQ = CFrame.new(5254.52734, 38.5011368, 4049.80127, -0.0732342899, 2.23174847e-08, -0.997314751,
                1.2052287e-07, 1, 1.35274023e-08, 0.997314751, -1.19208565e-07, -0.0732342899)
            CFramePuk = CFrame.new(5597.58936, 41.5013657, 3960.55371, -0.584786832, 4.98908861e-08, 0.811187029,
                4.10757259e-08, 1, -3.18919575e-08, -0.811187029, 1.4670098e-08, -0.584786832)
        elseif Double_Quest==25 then
            Ms = "Galley Captain [Lv. 650]"
            NameQuest = "FountainQuest"
            QuestLv = 2
            NameQ = "Galley Captain"
            CFrameQ = CFrame.new(5254.52734, 38.5011368, 4049.80127, -0.0732342899, 2.23174847e-08, -0.997314751,
                1.2052287e-07, 1, 1.35274023e-08, 0.997314751, -1.19208565e-07, -0.0732342899)
            CFramePuk = CFrame.new(5705.8252, 52.241478, 4890.11035, -0.969319642, 4.40228476e-09, 0.245803744,
                -7.88622412e-09, 1, -4.90088397e-08, -0.245803744, -4.94436954e-08, -0.969319642)
        end
    end
    if SecondSea then
        if Double_Quest==1 then
            Ms = "Raider [Lv. 700]"
            NameQuest = "Area1Quest"
            QuestLv = 1
            NameQ = "Raider"
            CFrameQ = CFrame.new(-424.080078, 73.0055847, 1836.91589, 0.253544956, -1.42165932e-08, 0.967323601,
                -6.00147771e-08, 1, 3.04272909e-08, -0.967323601, -6.5768397e-08, 0.253544956)
            CFramePuk = CFrame.new(-737.026123, 39.1748352, 2392.57959)
        elseif Double_Quest==2 then
            Ms = "Mercenary [Lv. 725]"
            NameQuest = "Area1Quest"
            QuestLv = 2
            NameQ = "Mercenary"
            CFrameQ = CFrame.new(-424.080078, 73.0055847, 1836.91589, 0.253544956, -1.42165932e-08, 0.967323601,
                -6.00147771e-08, 1, 3.04272909e-08, -0.967323601, -6.5768397e-08, 0.253544956)
            CFramePuk = CFrame.new(-938.497314, 80.9546738, 1443.98608, 0.231955677, 0, 0.972726345, -0, 1, -0,
                -0.972726345, 0, 0.231955677)
        elseif Double_Quest==3 then
            Ms = "Swan Pirate [Lv. 775]"
            NameQuest = "Area2Quest"
            QuestLv = 1
            NameQ = "Swan Pirate"
            CFrameQ = CFrame.new(632.698608, 73.1055908, 918.666321, -0.0319722369, 8.96074881e-10, -0.999488771,
                1.36326533e-10, 1, 8.92172336e-10, 0.999488771, -1.07732087e-10, -0.0319722369)
            CFramePuk = CFrame.new(967.233276, 141.309494, 1210.06384, 0.999673784, 5.40161649e-09, -0.0255404469,
                -7.62258967e-09, 1, -8.68617107e-08, 0.0255404469, 8.7028063e-08, 0.999673784)
        elseif Double_Quest==4 then
            Ms = "Marine Lieutenant [Lv. 875]"
            NameQuest = "MarineQuest3"
            QuestLv = 1
            NameQ = "Marine Lieutenant."
            CFrameQ = CFrame.new(-2443.04639, 73.0161057, -3220.30225, -0.854058921, -6.13997599e-08, -0.520176232,
                -1.30658604e-08, 1, -9.65840883e-08, 0.520176232, -7.56919505e-08, -0.854058921)
            CFramePuk = CFrame.new(-2967.00757, 72.9661407, -2972.7478, 0.977851391, 8.27619218e-08, -0.209300488,
                -6.95268412e-08, 1, 7.05923142e-08, 0.209300488, -5.44767893e-08, 0.977851391)
        elseif Double_Quest==5 then
            Ms = "Marine Captain [Lv. 900]"
            NameQuest = "MarineQuest3"
            QuestLv = 2
            NameQ = "Marine Captain"
            CFrameQ = CFrame.new(-2443.04639, 73.0161057, -3220.30225, -0.854058921, -6.13997599e-08, -0.520176232,
                -1.30658604e-08, 1, -9.65840883e-08, 0.520176232, -7.56919505e-08, -0.854058921)
            CFramePuk = CFrame.new(-1818.36401, 93.3760834, -3203.57788, 0.315930545, 4.84752114e-08, 0.948782325,
                1.37578589e-08, 1, -5.56731905e-08, -0.948782325, 3.06420738e-08, 0.315930545)
        elseif Double_Quest==6 then
            Ms = "Zombie [Lv. 950]"
            NameQuest = "ZombieQuest"
            QuestLv = 1
            NameQ = "Zombie"
            CFrameQ = CFrame.new(-5492.79395, 48.5151672, -793.710571, 0.321800292, -6.24695815e-08, 0.946807742,
                4.05616092e-08, 1, 5.21931227e-08, -0.946807742, 2.16082796e-08, 0.321800292)
            CFramePuk = CFrame.new(-5736.03516, 126.031998, -728.026184, 0.0818082988, -5.90035434e-08, 0.996648133,
                3.5947787e-09, 1, 5.89069167e-08, -0.996648133, -1.23634614e-09, 0.0818082988)
        elseif Double_Quest==7 then
            Ms = "Vampire [Lv. 975]"
            NameQuest = "ZombieQuest"
            QuestLv = 2
            NameQ = "Vampire"
            CFrameQ = CFrame.new(-5492.79395, 48.5151672, -793.710571, 0.321800292, -6.24695815e-08, 0.946807742,
                4.05616092e-08, 1, 5.21931227e-08, -0.946807742, 2.16082796e-08, 0.321800292)
            CFramePuk = CFrame.new(-6028.23584, 6.40270138, -1295.4563, 0.667547405, 0, 0.744567394, -0, 1.00000012, -0,
                -0.744567394, 0, 0.667547405)
        elseif Double_Quest==8 then
            Ms = "Snow Trooper [Lv. 1000]"
            NameQuest = "SnowMountainQuest"
            QuestLv = 1
            NameQ = "Snow Trooper"
            CFrameQ = CFrame.new(605.670532, 401.422028, -5370.10107, 0.459257662, -9.56824509e-10, -0.888303101,
                5.98925964e-10, 1, -7.67489405e-10, 0.888303101, -1.79552401e-10, 0.459257662)
            CFramePuk = CFrame.new(544.207947, 401.422028, -5309.08887, 0.503866196, -2.06684501e-08, 0.86378175,
                1.27917943e-09, 1, 2.31816841e-08, -0.86378175, -1.05755351e-08, 0.503866196)
        elseif Double_Quest==9 then
            Ms = "Winter Warrior [Lv. 1050]"
            NameQuest = "SnowMountainQuest"
            QuestLv = 2
            NameQ = "Winter Warrior"
            CFrameQ = CFrame.new(605.670532, 401.422028, -5370.10107, 0.459257662, -9.56824509e-10, -0.888303101,
                5.98925964e-10, 1, -7.67489405e-10, 0.888303101, -1.79552401e-10, 0.459257662)
            CFramePuk = CFrame.new(1240.86279, 461.108154, -5191.104, 0.528719008, -7.18234645e-08, 0.848796904,
                2.89169716e-10, 1, 8.44378363e-08, -0.848796904, -4.4398444e-08, 0.528719008)
        elseif Double_Quest==10 then
            Ms = "Lab Subordinate [Lv. 1100]"
            NameQuest = "IceSideQuest"
            QuestLv = 1
            NameQ = "Lab Subordinate"
            CFrameQ = CFrame.new(-6060.10693, 15.9868021, -4904.7876, -0.411000341, -5.06538868e-07, 0.91163528,
                1.26306062e-07, 1, 6.12581289e-07, -0.91163528, 3.66916197e-07, -0.411000341)
            CFramePuk = CFrame.new(-5833.63379, 48.4371948, -4510.4458, 0.0372838341, 5.56001822e-09, -0.999304712,
                -6.95599089e-09, 1, 5.30436006e-09, 0.999304712, 6.75338763e-09, 0.0372838341)
        elseif Double_Quest==11 then
            Ms = "Horned Warrior [Lv. 1125]"
            NameQuest = "IceSideQuest"
            QuestLv = 2
            NameQ = "Horned Warrior"
            CFrameQ = CFrame.new(-6060.10693, 15.9868021, -4904.7876, -0.411000341, -5.06538868e-07, 0.91163528,
                1.26306062e-07, 1, 6.12581289e-07, -0.91163528, 3.66916197e-07, -0.411000341)
            CFramePuk = CFrame.new(-6168.15918, 42.7079964, -6020.96826, -0.744210601, 2.41774178e-09, -0.667945027,
                -2.3336304e-09, 1, 6.21975493e-09, 0.667945027, 6.18754425e-09, -0.744210601)
        elseif Double_Quest==12 then
            Ms = "Magma Ninja [Lv. 1175]"
            NameQuest = "FireSideQuest"
            QuestLv = 1
            NameQ = "Magma Ninja"
            CFrameQ = CFrame.new(-5429.68359, 15.9517593, -5296.70215, 0.919959962, -6.00166317e-08, -0.392012328,
                2.29238974e-08, 1, -9.93018858e-08, 0.392012328, 8.23673076e-08, 0.919959962)
            CFramePuk = CFrame.new(-5404.85449, 22.8623676, -5896.09033, -0.519595861, 4.74720929e-09, 0.854412138,
                1.52255595e-08, 1, 3.70304742e-09, -0.854412138, 1.49329917e-08, -0.519595861)
        elseif Double_Quest==13 then
            Ms = "Lava Pirate [Lv. 1200]"
            NameQuest = "FireSideQuest"
            QuestLv = 2
            NameQ = "Lava Pirate"
            CFrameQ = CFrame.new(-5429.68359, 15.9517593, -5296.70215, 0.919959962, -6.00166317e-08, -0.392012328,
                2.29238974e-08, 1, -9.93018858e-08, 0.392012328, 8.23673076e-08, 0.919959962)
            CFramePuk = CFrame.new(-5075.1958, 16.1485081, -4814.36133, -0.800640523, -1.06090866e-07, 0.599145055,
                -6.59776447e-08, 1, 8.89041587e-08, -0.599145055, 3.16500923e-08, -0.800640523)
        elseif Double_Quest==14 then
            Ms = "Ship Deckhand [Lv. 1250]"
            NameQuest = "ShipQuest1"
            QuestLv = 1
            NameQ = "Ship Deckhand"
            CFrameQ = CFrame.new(1038.67456, 125.057098, 32911.3477, 0.120709591, 5.22710089e-08, -0.992687881,
                7.9174507e-09, 1, 5.36187876e-08, 0.992687881, -1.43318593e-08, 0.120709591)
            CFramePuk = CFrame.new(1215.14063, 125.057114, 33050.7188, 0.527230442, 2.61814961e-08, 0.849722326,
                -5.66963045e-08, 1, 4.36674741e-09, -0.849722326, -5.04783984e-08, 0.527230442)
        elseif Double_Quest==15 then
            Ms = "Ship Engineer [Lv. 1275]"
            NameQuest = "ShipQuest1"
            QuestLv = 2
            NameQ = "Ship Engineer"
            CFrameQ = CFrame.new(1038.67456, 125.057098, 32911.3477, 0.120709591, 5.22710089e-08, -0.992687881,
                7.9174507e-09, 1, 5.36187876e-08, 0.992687881, -1.43318593e-08, 0.120709591)
            CFramePuk = CFrame.new(862.985413, 40.4428635, 32867.9492, -0.847809434, 8.49998827e-08, -0.530301034,
                2.99658929e-08, 1, 1.1237865e-07, 0.530301034, 7.93847335e-08, -0.847809434)
        elseif Double_Quest==16 then
            Ms = "Ship Steward [Lv. 1300]"
            NameQuest = "ShipQuest2"
            QuestLv = 1
            NameQ = "Ship Steward"
            CFrameQ = CFrame.new(969.268311, 125.057121, 33245.2695, -0.85863924, -4.77058464e-08, -0.512580395,
                -1.49134394e-08, 1, -6.80880134e-08, 0.512580395, -5.08187057e-08, -0.85863924)
            CFramePuk = CFrame.new(923.611511, 129.555984, 33442.3125, 0.997516274, 9.71936913e-08, 0.0704362914,
                -9.52239958e-08, 1, -3.13219992e-08, -0.0704362914, 2.45369804e-08, 0.997516274)
        elseif Double_Quest==17 then
            Ms = "Ship Officer [Lv. 1325]"
            NameQuest = "ShipQuest2"
            QuestLv = 2
            NameQ = "Ship Officer"
            CFrameQ = CFrame.new(969.268311, 125.057121, 33245.2695, -0.85863924, -4.77058464e-08, -0.512580395,
                -1.49134394e-08, 1, -6.80880134e-08, 0.512580395, -5.08187057e-08, -0.85863924)
            CFramePuk = CFrame.new(882.275574, 181.057739, 33354.1797, 0.845816016, -3.71928088e-08, -0.533474684,
                1.28583932e-09, 1, -6.7679359e-08, 0.533474684, 5.65583242e-08, 0.845816016)
        elseif Double_Quest==18 then
            Ms = "Arctic Warrior [Lv. 1350]"
            NameQuest = "FrostQuest"
            QuestLv = 1
            NameQ = "Arctic Warrior"
            CFrameQ = CFrame.new(5669.43506, 28.2117786, -6482.60107, 0.888092756, 1.02705066e-07, 0.459664226,
                -6.20391774e-08, 1, -1.03572376e-07, -0.459664226, 6.34646895e-08, 0.888092756)
            CFramePuk = CFrame.new(5995.9292, 57.0727844, -6184.98926, 0.706337512, 5.23128296e-09, -0.707875192,
                -2.2285974e-08, 1, -1.48474424e-08, 0.707875192, 2.62629936e-08, 0.706337512)
        elseif Double_Quest==19 then
            Ms = "Snow Lurker [Lv. 1375]"
            NameQuest = "FrostQuest"
            QuestLv = 2
            NameQ = "Snow Lurker"
            CFrameQ = CFrame.new(5669.43506, 28.2117786, -6482.60107, 0.888092756, 1.02705066e-07, 0.459664226,
                -6.20391774e-08, 1, -1.03572376e-07, -0.459664226, 6.34646895e-08, 0.888092756)
            CFramePuk = CFrame.new(5516.27539, 60.5209846, -6830.82764, 0.219563305, -7.8544824e-09, 0.975598276,
                4.69439376e-09, 1, 6.99444236e-09, -0.975598276, 3.04411962e-09, 0.219563305)
        elseif Double_Quest==20 then
            Ms = "Sea Soldier [Lv. 1425]"
            NameQuest = "ForgottenQuest"
            QuestLv = 1
            NameQ = "Sea Soldier"
            CFrameQ = CFrame.new(-3053.97339, 236.846283, -10146.1484, -0.999963522, -2.10707256e-08, -0.00854360498,
                -2.09657198e-08, 1, -1.23802275e-08, 0.00854360498, -1.22006529e-08, -0.999963522)
            CFramePuk = CFrame.new(-3026.54834, 29.5403671, -9758.74316, -0.999909937, 1.71713896e-08, -0.0134194754,
                1.68009748e-08, 1, 2.7715517e-08, 0.0134194754, 2.74875607e-08, -0.999909937)
        elseif Double_Quest==21 then
            Ms = "Water Fighter [Lv. 1450]"
            NameQuest = "ForgottenQuest"
            QuestLv = 2
            NameQ = "Water Fighter"
            CFrameQ = CFrame.new(-3053.97339, 236.846283, -10146.1484, -0.999963522, -2.10707256e-08, -0.00854360498,
                -2.09657198e-08, 1, -1.23802275e-08, 0.00854360498, -1.22006529e-08, -0.999963522)
            CFramePuk = CFrame.new(-3262.00098, 298.699615, -10553.6943, -0.233570755, -4.57538185e-08, 0.972339869,
                -5.80986068e-08, 1, 3.30992194e-08, -0.972339869, -4.87605725e-08, -0.233570755)
        end
    end
    if ThirdSea then
        if Double_Quest==1 then
            Ms = "Pirate Millionaire [Lv. 1500]"
            NameQuest = "PiratePortQuest"
            QuestLv = 1
            NameQ = "Pirate Millionaire"
            CFrameQ = CFrame.new(-288.998016, 43.7932205, 5577.68994, -0.943210304, -8.05650799e-08, 0.332196265,
                -9.89928779e-08, 1, -3.85495724e-08, -0.332196265, -6.92454165e-08, -0.943210304)
            CFramePuk = CFrame.new(-91.8906479, 75.3287811, 5647.7002, 0.571274579, 8.47636343e-08, -0.820758998,
                -9.5655281e-08, 1, 3.66955462e-08, 0.820758998, 5.75466998e-08, 0.571274579)
        elseif Double_Quest==2 then
            Ms = "Pistol Billionaire [Lv. 1525]"
            NameQuest = "PiratePortQuest"
            QuestLv = 2
            NameQ = "Pistol Billionaire"
            CFrameQ = CFrame.new(-288.998016, 43.7932205, 5577.68994, -0.943210304, -8.05650799e-08, 0.332196265,
                -9.89928779e-08, 1, -3.85495724e-08, -0.332196265, -6.92454165e-08, -0.943210304)
            CFramePuk = CFrame.new(-740.71814, 130.458511, 5869.8623, 0.26613301, -6.96497509e-08, 0.963936329,
                -2.79989738e-08, 1, 7.99857816e-08, -0.963936329, -4.82760854e-08, 0.26613301)
        elseif Double_Quest==3 then
            Ms = "Dragon Crew Warrior [Lv. 1575]"
            NameQuest = "AmazonQuest"
            QuestLv = 1
            NameQ = "Dragon Crew Warrior"
            CFrameQ = CFrame.new(5834.86035, 51.3513641, -1103.34705, -0.919929087, 6.43650253e-08, 0.392084718,
                7.08298344e-08, 1, 2.02354311e-09, -0.392084718, 2.96328135e-08, -0.919929087)
            CFramePuk = CFrame.new(6498.88623, 51.4962921, -1011.49811, -0.844736993, -1.62814184e-09, -0.535181701,
                4.04657037e-08, 1, -6.69137634e-08, 0.535181701, -7.81810314e-08, -0.844736993)
        elseif Double_Quest==4 then
            Ms = "Dragon Crew Archer [Lv. 1600]"
            NameQuest = "AmazonQuest"
            QuestLv = 2
            NameQ = "Dragon Crew Archer"
            CFrameQ = CFrame.new(5834.86035, 51.3513641, -1103.34705, -0.919929087, 6.43650253e-08, 0.392084718,
                7.08298344e-08, 1, 2.02354311e-09, -0.392084718, 2.96328135e-08, -0.919929087)
            CFramePuk = CFrame.new(6608.45605, 378.396393, 235.665527, -0.647212744, -5.41171872e-08, 0.762309432,
                -5.96274674e-08, 1, 2.0366441e-08, -0.762309432, -3.22731637e-08, -0.647212744)
        elseif Double_Quest==5 then
            Ms = "Female Islander [Lv. 1625]"
            NameQuest = "AmazonQuest2"
            QuestLv = 1
            NameQ = "Female Islander"
            CFrameQ = CFrame.new(5445.11426, 601.603638, 751.129517, -0.346766561, 5.00326642e-08, -0.937951446,
                4.48732145e-08, 1, 3.67525779e-08, 0.937951446, -2.93443314e-08, -0.346766561)
            CFramePuk = CFrame.new(4758.92871, 730.33374, 800.998047, -0.100775175, -5.07539504e-08, -0.994909227,
                -2.28484591e-08, 1, -4.86993095e-08, 0.994909227, 1.78244619e-08, -0.100775175)
        elseif Double_Quest==6 then
            Ms = "Giant Islander [Lv. 1650]"
            NameQuest = "AmazonQuest2"
            QuestLv = 2
            NameQ = "Giant Islander"
            CFrameQ = CFrame.new(5445.11426, 601.603638, 751.129517, -0.346766561, 5.00326642e-08, -0.937951446,
                4.48732145e-08, 1, 3.67525779e-08, 0.937951446, -2.93443314e-08, -0.346766561)
            CFramePuk = CFrame.new(4736.1333, 601.373596, -123.942299, -0.651415646, 1.13692966e-08, -0.758721054,
                1.02050288e-08, 1, 6.2230785e-09, 0.758721054, -3.6889598e-09, -0.651415646)
        elseif Double_Quest==7 then
            Ms = "Marine Commodore [Lv. 1700]"
            NameQuest = "MarineTreeIsland"
            QuestLv = 1
            NameQ = "Marine Commodore"
            CFrameQ = CFrame.new(2180.83911, 28.7054462, -6739.44824, 0.977863014, 6.92042956e-09, -0.20924598,
                -1.01339639e-08, 1, -1.42855736e-08, 0.20924598, 1.60898246e-08, 0.977863014)
            CFramePuk = CFrame.new(2447, 73.1255493, -7470, 1, 4.06989891e-08, 4.79087976e-15, -4.06989891e-08, 1,
                2.86651343e-08, -3.62423799e-15, -2.86651343e-08, 1)
        elseif Double_Quest==8 then
            Ms = "Marine Rear Admiral [Lv. 1725]"
            NameQuest = "MarineTreeIsland"
            QuestLv = 2
            NameQ = "Marine Rear Admiral"
            CFrameQ = CFrame.new(2180.83911, 28.7054462, -6739.44824, 0.977863014, 6.92042956e-09, -0.20924598,
                -1.01339639e-08, 1, -1.42855736e-08, 0.20924598, 1.60898246e-08, 0.977863014)
            CFramePuk = CFrame.new(3660.3833, 160.524063, -6971.11328, 0.771100104, -4.33134666e-08, -0.636713922,
                -7.22266069e-09, 1, -7.67736665e-08, 0.636713922, 6.37989501e-08, 0.771100104)
        elseif Double_Quest==9 then
            Ms = "Fishman Raider [Lv. 1775]"
            NameQuest = "DeepForestIsland3"
            QuestLv = 1
            NameQ = "Fishman Raider"
            CFrameQ = CFrame.new(-10582.7578, 331.762634, -8758.56543, 0.911287963, 8.23484143e-08, -0.411769718,
                -7.27268628e-08, 1, 3.90346848e-08, 0.411769718, -5.62511859e-09, 0.911287963)
            CFramePuk = CFrame.new(-10615.6611, 331.762634, -8446.38574, 0.30275172, -4.96152719e-09, -0.953069448,
                -2.92618618e-09, 1, -6.13537132e-09, 0.953069448, 4.64635308e-09, 0.30275172)
        elseif Double_Quest==10 then
            Ms = "Fishman Captain [Lv. 1800]"
            NameQuest = "DeepForestIsland3"
            QuestLv = 2
            NameQ = "Fishman Captain"
            CFrameQ = CFrame.new(-10582.7578, 331.762634, -8758.56543, 0.911287963, 8.23484143e-08, -0.411769718,
                -7.27268628e-08, 1, 3.90346848e-08, 0.411769718, -5.62511859e-09, 0.911287963)
            CFramePuk = CFrame.new(-11040.3467, 331.762634, -8957.75684, -0.990780294, -5.54384094e-08, 0.135478467,
                -4.7334634e-08, 1, 6.30372483e-08, -0.135478467, 5.60432376e-08, -0.990780294)
        elseif Double_Quest==11 then
            Ms = "Forest Pirate [Lv. 1825]"
            NameQuest = "DeepForestIsland"
            QuestLv = 1
            NameQ = "Forest Pirate"
            CFrameQ = CFrame.new(-13233.2686, 332.378143, -7627.66455, -0.905921221, 2.69652856e-09, 0.423446268,
                2.31737229e-09, 1, -1.41026579e-09, -0.423446268, -2.96307007e-10, -0.905921221)
            CFramePuk = CFrame.new(-13479, 332.378143, -7905, 1, -1.27257813e-08, 2.41825958e-15, 1.27257813e-08, 1,
                -8.67651977e-08, -1.3141047e-15, 8.67651977e-08, 1)
        elseif Double_Quest==12 then
            Ms = "Mythological Pirate [Lv. 1850]"
            NameQuest = "DeepForestIsland"
            QuestLv = 2
            NameQ = "Mythological Pirate"
            CFrameQ = CFrame.new(-13233.2686, 332.378143, -7627.66455, -0.905921221, 2.69652856e-09, 0.423446268,
                2.31737229e-09, 1, -1.41026579e-09, -0.423446268, -2.96307007e-10, -0.905921221)
            CFramePuk = CFrame.new(-13676.1553, 469.788086, -6999.65527, 0.693832397, -2.62738986e-08, 0.720136523,
                -4.52658462e-08, 1, 8.00970454e-08, -0.720136523, -8.8171511e-08, 0.693832397)
        elseif Double_Quest==13 then
            Ms = "Jungle Pirate [Lv. 1900]"
            NameQuest = "DeepForestIsland2"
            QuestLv = 1
            NameQ = "Jungle Pirate"
            CFrameQ = CFrame.new(-12682.1279, 390.860687, -9901.89746, 0.00872628205, 1.59673574e-09, -0.999961913,
                -5.25600941e-09, 1, 1.55092938e-09, 0.999961913, 5.2422755e-09, 0.00872628205)
            CFramePuk = CFrame.new(-12107, 331.738281, -10549, 1, -2.50327403e-09, -6.22370418e-15, 2.50327403e-09, 1,
                8.81249651e-09, 6.20164405e-15, -8.81249651e-09, 1)
        elseif Double_Quest==14 then
            Ms = "Musketeer Pirate [Lv. 1925]"
            NameQuest = "DeepForestIsland2"
            QuestLv = 2
            NameQ = "Musketeer Pirate"
            CFrameQ = CFrame.new(-12682.1279, 390.860687, -9901.89746, 0.00872628205, 1.59673574e-09, -0.999961913,
                -5.25600941e-09, 1, 1.55092938e-09, 0.999961913, 5.2422755e-09, 0.00872628205)
            CFramePuk = CFrame.new(-13485.2305, 432.682373, -9857.01074, 0.994504631, 1.2369239e-08, -0.104692325,
                -8.4907642e-10, 1, 1.1008283e-07, 0.104692325, -1.09388999e-07, 0.994504631)
        elseif Double_Quest==15 then
            Ms = "Reborn Skeleton [Lv. 1975]"
            NameQuest = "HauntedQuest1"
            QuestLv = 1
            NameQ = "Reborn Skeleton"
            CFrameQ = CFrame.new(-9482.11035, 142.104828, 5566.32861, 0.0620567501, -4.18429273e-08, -0.998072624,
                -3.89895867e-08, 1, -4.43479706e-08, 0.998072624, 4.1666528e-08, 0.0620567501)
            CFramePuk = CFrame.new(-8762.33496, 142.104828, 6015.7627, -0.999993861, -2.26600214e-08, 0.00350279221,
                -2.28456738e-08, 1, -5.29611519e-08, -0.00350279221, -5.30408499e-08, -0.999993861)
        elseif Double_Quest==16 then
            Ms = "Living Zombie [Lv. 2000]"
            NameQuest = "HauntedQuest1"
            QuestLv = 2
            NameQ = "Living Zombie"
            CFrameQ = CFrame.new(-9482.11035, 142.104828, 5566.32861, 0.0620567501, -4.18429273e-08, -0.998072624,
                -3.89895867e-08, 1, -4.43479706e-08, 0.998072624, 4.1666528e-08, 0.0620567501)
            CFramePuk = CFrame.new(-10099.1494, 138.626678, 5930.86279, 0.241616711, -9.62791873e-08, -0.970371783,
                5.61582709e-08, 1, -8.52357971e-08, 0.970371783, -3.39000081e-08, 0.241616711)
        elseif Double_Quest==17 then
            Ms = "Demonic Soul [Lv. 2025]"
            NameQuest = "HauntedQuest2"
            QuestLv = 1
            NameQ = "Demonic Soul"
            CFrameQ = CFrame.new(-9514.25195, 172.104828, 6077.22998, 0.0446508788, -7.60616636e-09, 0.999002635,
                7.97889257e-08, 1, 4.04755696e-09, -0.999002635, 7.95286255e-08, 0.0446508788)
            CFramePuk = CFrame.new(-9513.54199, 172.104828, 6143.45459, -0.777332306, -2.16450324e-08, -0.62909019,
                -5.07872073e-08, 1, 2.83480883e-08, 0.62909019, 5.39856195e-08, -0.777332306)
        elseif Double_Quest==18 then
            Ms = "Posessed Mummy [Lv. 2050]"
            NameQuest = "HauntedQuest2"
            QuestLv = 2
            NameQ = "Posessed Mummy"
            CFrameQ = CFrame.new(-9514.25195, 172.104828, 6077.22998, 0.0446508788, -7.60616636e-09, 0.999002635,
                7.97889257e-08, 1, 4.04755696e-09, -0.999002635, 7.95286255e-08, 0.0446508788)
            CFramePuk = CFrame.new(-9580.24609, 5.79254198, 6190.47852, 0.462460369, 5.16216367e-08, -0.886639953,
                -7.72594788e-08, 1, 1.79240605e-08, 0.886639953, 6.0212173e-08, 0.462460369)
        elseif Double_Quest==19 then
            Ms = "Peanut Scout [Lv. 2075]"
            NameQuest = "NutsIslandQuest"
            QuestLv = 1
            NameQ = "Peanut Scout"
            CFrameQ = CFrame.new(-2103.18872, 38.1041794, -10193.7656, 0.7310462, 2.46138327e-08, 0.682327926,
                -5.02823738e-09, 1, -3.06860635e-08, -0.682327926, 1.90020231e-08, 0.7310462)
            CFramePuk = CFrame.new(-2221.45996, 38.103817, -10086.0762, -0.994582355, 2.09503472e-08, 0.103951879,
                2.41223095e-08, 1, 2.92565758e-08, -0.103951879, 3.16056337e-08, -0.994582355)
        elseif Double_Quest==20 then
            Ms = "Peanut President [Lv. 2100]"
            NameQuest = "NutsIslandQuest"
            QuestLv = 2
            NameQ = "Peanut President"
            CFrameQ = CFrame.new(-2103.18872, 38.1041794, -10193.7656, 0.7310462, 2.46138327e-08, 0.682327926,
                -5.02823738e-09, 1, -3.06860635e-08, -0.682327926, 1.90020231e-08, 0.7310462)
            CFramePuk = CFrame.new(-2171.88647, 88.2396011, -10531.9512, 0.691500723, 5.31482591e-08, -0.722375751,
                -2.70291771e-08, 1, 4.7700329e-08, 0.722375751, -1.34595908e-08, 0.691500723)
        elseif Double_Quest==21 then
            Ms = "Ice Cream Chef [Lv. 2125]"
            NameQuest = "IceCreamIslandQuest"
            QuestLv = 1
            NameQ = "Ice Cream Chef"
            CFrameQ = CFrame.new(-820.991455, 65.8195343, -10965.4316, 0.832442105, 3.44203599e-08, -0.554112017,
                -3.14893249e-08, 1, 1.48116621e-08, 0.554112017, 5.11876364e-09, 0.832442105)
            CFramePuk = CFrame.new(-761.110657, 164.200974, -10929.7031, -0.903523564, -2.8124143e-08, 0.428538442,
                -5.52620127e-09, 1, 5.39766987e-08, -0.428538442, 4.64010306e-08, -0.903523564)
        elseif Double_Quest==22 then
            Ms = "Ice Cream Commander [Lv. 2150]"
            NameQuest = "IceCreamIslandQuest"
            QuestLv = 2
            NameQ = "Ice Cream Commander"
            CFrameQ = CFrame.new(-820.991455, 65.8195343, -10965.4316, 0.832442105, 3.44203599e-08, -0.554112017,
                -3.14893249e-08, 1, 1.48116621e-08, 0.554112017, 5.11876364e-09, 0.832442105)
            CFramePuk = CFrame.new(-683.515137, 97.7532196, -11270.5254, -0.249526113, -3.42524373e-08, -0.968368053,
                -4.59147245e-08, 1, -2.35401334e-08, 0.968368053, 3.85884746e-08, -0.249526113)
        elseif Double_Quest==23 then
            Ms = "Cookie Crafter [Lv. 2200]"
            NameQuest = "CakeQuest1"
            QuestLv = 1
            NameQ = "Cookie Crafter"
            CFrameQ = CFrame.new(-2021.28113, 37.7982178, -12027.1602, 0.876975715, 2.42050024e-08, 0.480534643,
                -1.83145179e-08, 1, -1.69469878e-08, -0.480534643, 6.06133632e-09, 0.876975715)
            CFramePuk = CFrame.new(-2362.1604, 37.7981148, -12116.2031, 0.428214997, 1.03298156e-07, 0.903676867,
                -1.24923467e-08, 1, -1.08389123e-07, -0.903676867, 3.51248026e-08, 0.428214997)
        elseif Double_Quest==24 then
            Ms = "Cake Guard [Lv. 2225]"
            NameQuest = "CakeQuest1"
            QuestLv = 2
            NameQ = "Cake Guard"
            CFrameQ = CFrame.new(-2021.28113, 37.7982178, -12027.1602, 0.876975715, 2.42050024e-08, 0.480534643,
                -1.83145179e-08, 1, -1.69469878e-08, -0.480534643, 6.06133632e-09, 0.876975715)
            CFramePuk = CFrame.new(-1560.17944, 37.7981339, -12440.5781, -0.560352206, 1.90654585e-08, -0.828254402,
                6.60573107e-08, 1, -2.16719656e-08, 0.828254402, -6.68561952e-08, -0.560352206)
        elseif Double_Quest==25 then
            Ms = "Baking Staff [Lv. 2250]"
            NameQuest = "CakeQuest2"
            QuestLv = 1
            NameQ = "Baking Staff"
            CFrameQ = CFrame.new(-1929.3186, 37.7981339, -12843.3857, -0.994816065, 6.2958283e-09, 0.101690687,
                6.02614314e-09, 1, -2.95921043e-09, -0.101690687, -2.33106734e-09, -0.994816065)
            CFramePuk = CFrame.new(-1874.04688, 74.015831, -13002.7959, 0.958144426, -9.20437699e-08, -0.286285222,
                1.05663617e-07, 1, 3.21261275e-08, 0.286285222, -6.10314004e-08, 0.958144426)
        elseif Double_Quest==26 then
            Ms = "Head Baker [Lv. 2275]"
            NameQuest = "CakeQuest2"
            QuestLv = 2
            NameQ = "Head Baker"
            CFrameQ = CFrame.new(-1929.3186, 37.7981339, -12843.3857, -0.994816065, 6.2958283e-09, 0.101690687,
                6.02614314e-09, 1, -2.95921043e-09, -0.101690687, -2.33106734e-09, -0.994816065)
            CFramePuk = CFrame.new(-2205.25171, 108.351257, -12784.6475, 0.999649942, 1.09295986e-08, -0.0264567528,
                -9.22357479e-09, 1, 6.46055156e-08, 0.0264567528, -6.43388702e-08, 0.999649942)
        elseif Double_Quest==27 then
            Ms = "Cocoa Warrior [Lv. 2300]"
            NameQuest = "ChocQuest1"
            QuestLv = 1
            NameQ = "Cocoa Warrior"
            CFrameQ = CFrame.new(231.562515, 24.7342396, -12196.9277, 0.996608198, -4.87148775e-08, -0.0822927728,
                4.61355079e-08, 1, -3.32453354e-08, 0.0822927728, 2.93359523e-08, 0.996608198)
            CFramePuk = CFrame.new(-26.0082874, 24.7343502, -12253.001, -0.17375651, 7.9442728e-08, 0.984788656,
                1.18449632e-08, 1, -7.85798946e-08, -0.984788656, -1.98898231e-09, -0.17375651)
        elseif Double_Quest==28 then
            Ms = "Chocolate Bar Battler [Lv. 2325]"
            NameQuest = "ChocQuest1"
            QuestLv = 2
            NameQ = "Chocolate Bar Battler"
            CFrameQ = CFrame.new(231.562515, 24.7342396, -12196.9277, 0.996608198, -4.87148775e-08, -0.0822927728,
                4.61355079e-08, 1, -3.32453354e-08, 0.0822927728, 2.93359523e-08, 0.996608198)
            CFramePuk = CFrame.new(715.227661, 64.5699463, -12601.4971, 0.375136077, -3.84623213e-08, 0.926969767,
                1.12107639e-08, 1, 3.69556403e-08, -0.926969767, -3.47135498e-09, 0.375136077)
        elseif Double_Quest==29 then
            Ms = "Sweet Thief [Lv. 2350]"
            NameQuest = "ChocQuest2"
            QuestLv = 1
            NameQ = "Sweet Thief"
            CFrameQ = CFrame.new(147.670837, 24.7938328, -12775.2656, -0.274139136, 7.20163911e-08, -0.961690068,
                7.48291242e-08, 1, 5.35544693e-08, 0.961690068, -5.72810492e-08, -0.274139136)
            CFramePuk = CFrame.new(59.2454491, 57.2388878, -12634.1523, 0.97673136, -3.85135479e-08, 0.214466438,
                3.43798909e-08, 1, 2.30041923e-08, -0.214466438, -1.50955834e-08, 0.97673136)
        elseif Double_Quest==30 then
            Ms = "Candy Rebel [Lv. 2375]"
            NameQuest = "ChocQuest2"
            QuestLv = 2
            NameQ = "Candy Rebel"
            CFrameQ = CFrame.new(147.670837, 24.7938328, -12775.2656, -0.274139136, 7.20163911e-08, -0.961690068,
                7.48291242e-08, 1, 5.35544693e-08, 0.961690068, -5.72810492e-08, -0.274139136)
            CFramePuk = CFrame.new(72.7375183, 24.7938499, -12939.2383, -0.87948513, 9.16761138e-08, -0.47592634,
                7.88268579e-08, 1, 4.69590802e-08, 0.47592634, 3.78403309e-09, -0.87948513)
        elseif Double_Quest==31 then
            Ms = "Candy Pirate [Lv. 2400]"
            NameQuest = "CandyQuest1"
            QuestLv = 1
            NameQ = "Candy Pirate"
            CFrameQ = CFrame.new(-1151.48987, 16.1422901, -14445.6904, -0.316594511, -6.85698254e-08, -0.948560953, -2.05343067e-08, 1, -6.54346692e-08, 0.948560953, -1.23821675e-09, -0.316594511)
            CFramePuk = CFrame.new(-1408.46521, 16.1423531, -14552.2041, 0.90175873, -8.17216943e-08, -0.432239741, 7.81264475e-08, 1, -2.60746162e-08, 0.432239741, -1.02563433e-08, 0.90175873)
        elseif Double_Quest==32 then
            Ms = "Snow Demon [Lv. 2425]"
            NameQuest = "CandyQuest1"
            QuestLv = 2
            NameQ = "Snow Demon"
            CFrameQ = CFrame.new(-1151.48987, 16.1422901, -14445.6904, -0.316594511, -6.85698254e-08, -0.948560953, -2.05343067e-08, 1, -6.54346692e-08, 0.948560953, -1.23821675e-09, -0.316594511)
            CFramePuk = CFrame.new(-777.070862, 23.5809536, -14453.0078, 0.33384338, 0, -0.942628562, 0, 1, 0, 0.942628562, 0, 0.33384338)
        end
    end
end
function CheckBossQuest()
	if _G.SelectBoss == "Saber Expert [Lv. 200] [Boss]" then
		MsBoss = "Saber Expert [Lv. 200] [Boss]"
		NameBoss = "Saber Expert"
		CFrameBoss = CFrame.new(-1458.89502, 29.8870335, -50.633564, 0.858821094, 1.13848939e-08, 0.512275636, -4.85649254e-09, 1, -1.40823326e-08, -0.512275636, 9.6063415e-09, 0.858821094)
	elseif _G.SelectBoss == "The Saw [Lv. 100] [Boss]" then
		MsBoss = "The Saw [Lv. 100] [Boss]"
		NameBoss = "The Saw"
		CFrameBoss = CFrame.new(-683.519897, 13.8534927, 1610.87854, -0.290192783, 6.88365773e-08, 0.956968188, 6.98413629e-08, 1, -5.07531119e-08, -0.956968188, 5.21077759e-08, -0.290192783)
	elseif _G.SelectBoss== "Greybeard [Lv. 750] [Raid Boss]" then
		MsBoss = "Greybeard [Lv. 750] [Raid Boss]"
		NameBoss = "Greybeard"
		CFrameBoss = CFrame.new(-4955.72949, 80.8163834, 4305.82666, -0.433646321, -1.03394289e-08, 0.901083171, -3.0443168e-08, 1, -3.17633075e-09, -0.901083171, -2.88092288e-08, -0.433646321)
    elseif _G.SelectBoss== "The Gorilla King [Lv. 25] [Boss]" then
		MsBoss = "The Gorilla King [Lv. 25] [Boss]"
		NameBoss = "The Gorilla King"
		NameQuestBoss = "JungleQuest"
		LevelQuestBoss = 3
		CFrameQuestBoss = CFrame.new(-1604.12012, 36.8521118, 154.23732, 0.0648873374, -4.70858913e-06, -0.997892559, 1.41431883e-07, 1, -4.70933674e-06, 0.997892559, 1.64442184e-07, 0.0648873374)
		CFrameBoss = CFrame.new(-1223.52808, 6.27936459, -502.292664, 0.310949147, -5.66602516e-08, 0.950426519, -3.37275488e-08, 1, 7.06501808e-08, -0.950426519, -5.40241736e-08, 0.310949147)
	elseif _G.SelectBoss== "Bobby [Lv. 55] [Boss]" then
		MsBoss = "Bobby [Lv. 55] [Boss]"
		NameBoss = "Bobby"
		NameQuestBoss = "BuggyQuest1"
		LevelQuestBoss = 3
		CFrameQuestBoss = CFrame.new(-1139.59717, 4.75205183, 3825.16211, -0.959730506, -7.5857054e-09, 0.280922383, -4.06310328e-08, 1, -1.11807175e-07, -0.280922383, -1.18718916e-07, -0.959730506)
		CFrameBoss = CFrame.new(-1147.65173, 32.5966301, 4156.02588, 0.956680477, -1.77109952e-10, -0.29113996, 5.16530874e-10, 1, 1.08897802e-09, 0.29113996, -1.19218679e-09, 0.956680477)
	elseif _G.SelectBoss == "Yeti [Lv. 110] [Boss]" then
		MsBoss = "Yeti [Lv. 110] [Boss]"
		NameBoss = "Yeti"
		NameQuestBoss = "SnowQuest"
		LevelQuestBoss = 3
		CFrameQuestBoss = CFrame.new(1384.90247, 87.3078308, -1296.6825, 0.280209213, 2.72035177e-08, -0.959938943, -6.75690828e-08, 1, 8.6151708e-09, 0.959938943, 6.24481444e-08, 0.280209213)
		CFrameBoss = CFrame.new(1221.7356, 138.046906, -1488.84082, 0.349343032, -9.49245944e-08, 0.936994851, 6.29478194e-08, 1, 7.7838429e-08, -0.936994851, 3.17894653e-08, 0.349343032)
	elseif _G.SelectBoss== "Mob Leader [Lv. 120] [Boss]" then
		MsBoss = "Mob Leader [Lv. 120] [Boss]"
		NameBoss = "Mob Leader"
		CFrameBoss = CFrame.new(-2848.59399, 7.4272871, 5342.44043, -0.928248107, -8.7248246e-08, 0.371961564, -7.61816636e-08, 1, 4.44474857e-08, -0.371961564, 1.29216433e-08, -0.92824)
	elseif _G.SelectBoss == "Vice Admiral [Lv. 130] [Boss]" then
		MsBoss = "Vice Admiral [Lv. 130] [Boss]"
		NameBoss = "Vice Admiral"
		NameQuestBoss = "MarineQuest2"
		LevelQuestBoss = 2
		CFrameQuestBoss = CFrame.new(-5035.42285, 28.6520386, 4324.50293, -0.0611100644, -8.08395768e-08, 0.998130739, -1.57416586e-08, 1, 8.00271849e-08, -0.998130739, -1.08217701e-08, -0.0611100644)
		CFrameBoss = CFrame.new(-5078.45898, 99.6520691, 4402.1665, -0.555574954, -9.88630566e-11, 0.831466436, -6.35508286e-08, 1, -4.23449258e-08, -0.831466436, -7.63661632e-08, -0.555574954)
	elseif _G.SelectBoss == "Warden [Lv. 175] [Boss]" then
		MsBoss = "Warden [Lv. 175] [Boss]"
		NameBoss = "Warden"
		NameQuestBoss = "ImpelQuest"
		LevelQuestBoss = 1
		CFrameQuestBoss = CFrame.new(4851.35059, 5.68744135, 743.251282, -0.538484037, -6.68303741e-08, -0.842635691, 1.38001752e-08, 1, -8.81300792e-08, 0.842635691, -5.90851599e-08, -0.538484037)
		CFrameBoss = CFrame.new(5232.5625, 5.26856995, 747.506897, 0.943829298, -4.5439414e-08, 0.330433697, 3.47818627e-08, 1, 3.81658154e-08, -0.330433697, -2.45289105e-08, 0.943829298)
    elseif _G.SelectBoss== "Chief Warden [Lv. 200] [Boss]" then
		MsBoss = "Chief Warden [Lv. 200] [Boss]"
		NameBoss = "Chief Warden"
		NameQuestBoss = "ImpelQuest"
		LevelQuestBoss = 2
		CFrameQuestBoss = CFrame.new(4851.35059, 5.68744135, 743.251282, -0.538484037, -6.68303741e-08, -0.842635691, 1.38001752e-08, 1, -8.81300792e-08, 0.842635691, -5.90851599e-08, -0.538484037)
		CFrameBoss = CFrame.new(5232.5625, 5.26856995, 747.506897, 0.943829298, -4.5439414e-08, 0.330433697, 3.47818627e-08, 1, 3.81658154e-08, -0.330433697, -2.45289105e-08, 0.943829298)
	elseif _G.SelectBoss== "Swan [Lv. 225] [Boss]" then
		MsBoss = "Swan [Lv. 225] [Boss]"
		NameBoss = "Swan"
		NameQuestBoss = "ImpelQuest"
		LevelQuestBoss = 3
		CFrameQuestBoss = CFrame.new(4851.35059, 5.68744135, 743.251282, -0.538484037, -6.68303741e-08, -0.842635691, 1.38001752e-08, 1, -8.81300792e-08, 0.842635691, -5.90851599e-08, -0.538484037)
		CFrameBoss = CFrame.new(5232.5625, 5.26856995, 747.506897, 0.943829298, -4.5439414e-08, 0.330433697, 3.47818627e-08, 1, 3.81658154e-08, -0.330433697, -2.45289105e-08, 0.943829298)
	elseif _G.SelectBoss == "Magma Admiral [Lv. 350] [Boss]" then
		MsBoss = "Magma Admiral [Lv. 350] [Boss]"
		NameBoss = "Magma Admiral"
		NameQuestBoss = "MagmaQuest"
		LevelQuestBoss = 3
		CFrameQuestBoss = CFrame.new(-5317.07666, 12.2721891, 8517.41699, 0.51175487, -2.65508806e-08, -0.859131515, -3.91131572e-08, 1, -5.42026761e-08, 0.859131515, 6.13418294e-08, 0.51175487)
		CFrameBoss = CFrame.new(-5530.12646, 22.8769703, 8859.91309, 0.857838571, 2.23414389e-08, 0.513919294, 1.53689133e-08, 1, -6.91265853e-08, -0.513919294, 6.71978384e-08, 0.857838571)
	elseif _G.SelectBoss == "Fishman Lord [Lv. 425] [Boss]" then
		MsBoss = "Fishman Lord [Lv. 425] [Boss]"
		NameBoss = "Fishman Lord"
		NameQuestBoss = "FishmanQuest"
		LevelQuestBoss = 3
		CFrameQuestBoss = CFrame.new(61123.0859, 18.5066795, 1570.18018, 0.927145958, 1.0624845e-07, 0.374700129, -6.98219367e-08, 1, -1.10790765e-07, -0.374700129, 7.65569368e-08, 0.927145958)
		CFrameBoss = CFrame.new(61351.7773, 31.0306778, 1113.31409, 0.999974668, 0, -0.00714713801, 0, 1.00000012, 0, 0.00714714266, 0, 0.999974549)
        if    (_G._G.BossSelect  or  _G.AllBoss)and
                    (CFrameQuestBoss.Position - game.Players.LocalPlayer.Character.HumanoidRootPart.Position).Magnitude > 3000 then
                    game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("requestEntrance",
                        Vector3.new(61163.8516, 5.43263245, 1819.78418, 1, 6.89280011e-09, 9.74497786e-14, -6.89280011e-09,
                            1, 3.38349579e-08, -9.72165599e-14, -3.38349579e-08, 1))
                end
	elseif _G.SelectBoss == "Wysper [Lv. 500] [Boss]" then
		MsBoss = "Wysper [Lv. 500] [Boss]"
		NameBoss = "Wysper"
		NameQuestBoss = "SkyExp1Quest"
		LevelQuestBoss = 3
		CFrameQuestBoss = CFrame.new(-7862.94629, 5545.52832, -379.833954, 0.462944925, 1.45838088e-08, -0.886386991, 1.0534996e-08, 1, 2.19553424e-08, 0.886386991, -1.95022007e-08, 0.462944925)
		CFrameBoss = CFrame.new(-7925.48389, 5550.76074, -636.178345, 0.716468513, -1.22915289e-09, 0.697619379, 3.37381434e-09, 1, -1.70304748e-09, -0.697619379, 3.57381835e-09, 0.716468513)
	elseif _G.SelectBoss == "Thunder God [Lv. 575] [Boss]" then
		MsBoss = "Thunder God [Lv. 575] [Boss]"
		NameBoss = "Thunder God"
		NameQuestBoss = "SkyExp2Quest"
		LevelQuestBoss = 3
		CFrameQuestBoss = CFrame.new(-7902.78613, 5635.99902, -1411.98706, -0.0361216255, -1.16895912e-07, 0.999347389, 1.44533963e-09, 1, 1.17024491e-07, -0.999347389, 5.6715117e-09, -0.0361216255)
		CFrameBoss = CFrame.new(-7917.53613, 5616.61377, -2277.78564, 0.965189934, 4.80563429e-08, -0.261550069, -6.73089886e-08, 1, -6.46515304e-08, 0.261550069, 8.00056768e-08, 0.965189934)
	elseif _G.SelectBoss == "Cyborg [Lv. 675] [Boss]" then
		MsBoss = "Cyborg [Lv. 675] [Boss]"
		NameBoss = "Cyborg"
		NameQuestBoss = "FountainQuest"
		LevelQuestBoss = 3
		CFrameQuestBoss = CFrame.new(5253.54834, 38.5361786, 4050.45166, -0.0112687312, -9.93677887e-08, -0.999936521, 2.55291371e-10, 1, -9.93769547e-08, 0.999936521, -1.37512213e-09, -0.0112687312)
		CFrameBoss = CFrame.new(6041.82813, 52.7112198, 3907.45142, -0.563162148, 1.73805248e-09, -0.826346457, -5.94632716e-08, 1, 4.26280238e-08, 0.826346457, 7.31437524e-08, -0.563162148)
		-- New World
	elseif _G.SelectBoss== "Diamond [Lv. 750] [Boss]" then
		MsBoss = "Diamond [Lv. 750] [Boss]"
		NameBoss = "Diamond"
		NameQuestBoss = "Area1Quest"
		LevelQuestBoss = 3
		CFrameQuestBoss = CFrame.new(-424.080078, 73.0055847, 1836.91589, 0.253544956, -1.42165932e-08, 0.967323601, -6.00147771e-08, 1, 3.04272909e-08, -0.967323601, -6.5768397e-08, 0.253544956)
		CFrameBoss = CFrame.new(-1736.26587, 198.627731, -236.412857, -0.997808516, 0, -0.0661673471, 0, 1, 0, 0.0661673471, 0, -0.997808516)
	elseif _G.SelectBoss == "Jeremy [Lv. 850] [Boss]" then
		MsBoss = "Jeremy [Lv. 850] [Boss]"
		NameBoss = "Jeremy"
		NameQuestBoss = "Area2Quest"
		LevelQuestBoss = 3
		CFrameQuestBoss = CFrame.new(632.698608, 73.1055908, 918.666321, -0.0319722369, 8.96074881e-10, -0.999488771, 1.36326533e-10, 1, 8.92172336e-10, 0.999488771, -1.07732087e-10, -0.0319722369)
		CFrameBoss = CFrame.new(2203.76953, 448.966034, 752.731079, -0.0217453763, 0, -0.999763548, 0, 1, 0, 0.999763548, 0, -0.0217453763)
	elseif _G.SelectBoss == "Fajita [Lv. 925] [Boss]" then
		MsBoss = "Fajita [Lv. 925] [Boss]"
		NameBoss = "Fajita"
		NameQuestBoss = "MarineQuest3"
		LevelQuestBoss = 3
		CFrameQuestBoss = CFrame.new(-2442.65015, 73.0511475, -3219.11523, -0.873540044, 4.2329841e-08, -0.486752301, 5.64383384e-08, 1, -1.43220786e-08, 0.486752301, -3.99823996e-08, -0.873540044)
		CFrameBoss = CFrame.new(-2297.40332, 115.449463, -3946.53833, 0.961227536, -1.46645796e-09, -0.275756449, -2.3212845e-09, 1, -1.34094433e-08, 0.275756449, 1.35296352e-08, 0.961227536)
	elseif _G.SelectBoss == "Don Swan [Lv. 1000] [Boss]" then
		MsBoss = "Don Swan [Lv. 1000] [Boss]"
		NameBoss = "Don Swan"
		CFrameBoss = CFrame.new(2288.802, 15.1870775, 863.034607, 0.99974072, -8.41247214e-08, -0.0227668174, 8.4774733e-08, 1, 2.75850098e-08, 0.0227668174, -2.95079072e-08, 0.99974072)
	elseif _G.SelectBoss == "Smoke Admiral [Lv. 1150] [Boss]" then
		MsBoss = "Smoke Admiral [Lv. 1150] [Boss]"
		NameBoss = "Smoke Admiral"
		NameQuestBoss = "IceSideQuest"
		LevelQuestBoss = 3
		CFrameQuestBoss = CFrame.new(-6059.96191, 15.9868021, -4904.7373, -0.444992423, -3.0874483e-09, 0.895534337, -3.64098796e-08, 1, -1.4644522e-08, -0.895534337, -3.91229982e-08, -0.444992423)
		CFrameBoss = CFrame.new(-5115.72754, 23.7664986, -5338.2207, 0.251453817, 1.48345061e-08, -0.967869282, 4.02796978e-08, 1, 2.57916977e-08, 0.967869282, -4.54708946e-08, 0.251453817)
	elseif _G.SelectBoss== "Cursed Captain [Lv. 1325] [Raid Boss]" then
		MsBoss = "Cursed Captain [Lv. 1325] [Raid Boss]"
		NameBoss = "Cursed Captain"
		CFrameBoss = CFrame.new(916.928589, 181.092773, 33422, -0.999505103, 9.26310495e-09, 0.0314563364, 8.42916226e-09, 1, -2.6643713e-08, -0.0314563364, -2.63653774e-08, -0.999505103)
    elseif _G.SelectBoss == "Darkbeard [Lv. 1000] [Raid Boss]" then
		MsBoss = "Darkbeard [Lv. 1000] [Raid Boss]"
		NameBoss = "Darkbeard"
		CFrameBoss = CFrame.new(3876.00366, 24.6882591, -3820.21777, -0.976951957, 4.97356325e-08, 0.213458836, 4.57335361e-08, 1, -2.36868622e-08, -0.213458836, -1.33787044e-08, -0.976951957)
	elseif _G.SelectBoss == "Order [Lv. 1250] [Raid Boss]" then
		MsBoss = "Order [Lv. 1250] [Raid Boss]"
		NameBoss = "Order"
		CFrameBoss = CFrame.new(-6221.15039, 16.2351036, -5045.23584, -0.380726993, 7.41463495e-08, 0.924687505, 5.85604774e-08, 1, -5.60738549e-08, -0.924687505, 3.28013137e-08, -0.380726993)
	elseif _G.SelectBoss== "Awakened Ice Admiral [Lv. 1400] [Boss]" then
		MsBoss = "Awakened Ice Admiral [Lv. 1400] [Boss]"
		NameBoss = "Awakened Ice Admiral"
		NameQuestBoss = "FrostQuest"
		LevelQuestBoss = 3
		CFrameQuestBoss = CFrame.new(5669.33203, 28.2118053, -6481.55908, 0.921275556, -1.25320829e-08, 0.388910472, 4.72230788e-08, 1, -7.96414241e-08, -0.388910472, 9.17372489e-08, 0.921275556)
		CFrameBoss = CFrame.new(6407.33936, 340.223785, -6892.521, 0.49051559, -5.25310213e-08, -0.871432424, -2.76146022e-08, 1, -7.58250565e-08, 0.871432424, 6.12576301e-08, 0.49051559)
	elseif _G.SelectBoss== "Tide Keeper [Lv. 1475] [Boss]" then
		MsBoss = "Tide Keeper [Lv. 1475] [Boss]"
		NameBoss = "Tide Keeper"
		NameQuestBoss = "ForgottenQuest"             
		LevelQuestBoss = 3
		CFrameQuestBoss = CFrame.new(-3053.89648, 236.881363, -10148.2324, -0.985987961, -3.58504737e-09, 0.16681771, -3.07832915e-09, 1, 3.29612559e-09, -0.16681771, 2.73641976e-09, -0.985987961)
		CFrameBoss = CFrame.new(-3570.18652, 123.328949, -11555.9072, 0.465199202, -1.3857326e-08, 0.885206044, 4.0332897e-09, 1, 1.35347511e-08, -0.885206044, -2.72606271e-09, 0.465199202)
		-- Thire World
	elseif _G.SelectBoss== "Stone [Lv. 1550] [Boss]" then
		MsBoss = "Stone [Lv. 1550] [Boss]"
		NameBoss = "Stone"
		NameQuestBoss = "PiratePortQuest"             
		LevelQuestBoss = 3
		CFrameQuestBoss = CFrame.new(-290, 44, 5577)
		CFrameBoss = CFrame.new(-1085, 40, 6779)
	elseif _G.SelectBoss == "Island Empress [Lv. 1675] [Boss]" then
		MsBoss = "Island Empress [Lv. 1675] [Boss]"
		NameBoss = "Island Empress"
		NameQuestBoss = "AmazonQuest2"             
		LevelQuestBoss = 3
		CFrameQuestBoss = CFrame.new(5443, 602, 752)
		CFrameBoss = CFrame.new(5659, 602, 244)
	elseif _G.SelectBoss == "Kilo Admiral [Lv. 1750] [Boss]" then
		MsBoss = "Kilo Admiral [Lv. 1750] [Boss]"
		NameBoss = "Kilo Admiral"
		NameQuestBoss = "MarineTreeIsland"             
		LevelQuestBoss = 3
		CFrameQuestBoss = CFrame.new(2178, 29, -6737)
		CFrameBoss =CFrame.new(2846, 433, -7100)
	elseif _G.SelectBoss == "Captain Elephant [Lv. 1875] [Boss]" then
		MsBoss = "Captain Elephant [Lv. 1875] [Boss]"
		NameBoss = "Captain Elephant"
		NameQuestBoss = "DeepForestIsland"             
		LevelQuestBoss = 3
		CFrameQuestBoss = CFrame.new(-13232, 333, -7631)
		CFrameBoss = CFrame.new(-13221, 325, -8405)
	elseif _G.SelectBoss == "Beautiful Pirate [Lv. 1950] [Boss]" then
		MsBoss = "Beautiful Pirate [Lv. 1950] [Boss]"
		NameBoss = "Beautiful Pirate"
		NameQuestBoss = "DeepForestIsland2"             
		LevelQuestBoss = 3
		CFrameQuestBoss = CFrame.new(-12686, 391, -9902)
		CFrameBoss = CFrame.new(5182, 23, -20)
	elseif _G.SelectBoss== "Cake Queen [Lv. 2175] [Boss]" then
		MsBoss = "Cake Queen [Lv. 2175] [Boss]"
		NameBoss = "Cake Queen"
		NameQuestBoss = "IceCreamIslandQuest"             
		LevelQuestBoss = 3
		CFrameQuestBoss = CFrame.new(-716, 382, -11010)
		CFrameBoss = CFrame.new(-821, 66, -10965)
	elseif _G.SelectBoss== "rip_indra True Form [Lv. 5000] [Raid Boss]" then
		MsBoss = "rip_indra True Form [Lv. 5000] [Raid Boss]"
		NameBoss = "rip_indra True Form"
		CFrameBoss = CFrame.new(-5359, 424, -2735)
	elseif _G.SelectBoss == "Longma [Lv. 2000] [Boss]" then
		MsBoss = "Longma [Lv. 2000] [Boss]"
		NameBoss = "Longma"
		CFrameBoss = CFrame.new(-10248.3936, 353.79129, -9306.34473)
	elseif _G.SelectBoss == "Soul Reaper [Lv. 2100] [Raid Boss]" then
		MsBoss = "Soul Reaper [Lv. 2100] [Raid Boss]"
		NameBoss = "Soul Reaper"
		CFrameBoss = CFrame.new(-9515.62109, 315.925537, 6691.12012)
	end
end
_G.GetBoss = false
function GetBossName()
	for i,v in pairs(game.ReplicatedStorage:GetChildren()) do
		if not _G.GetBoss then
			-- World 1
			if v.Name == "The Gorilla King [Lv. 25] [Boss]" and game.Players.localPlayer.Data.Level.Value >= 20  then
                _G.SelectBoss = "The Gorilla King [Lv. 25] [Boss]"
			elseif v.Name == "Bobby [Lv. 55] [Boss]" and game.Players.localPlayer.Data.Level.Value >= 55  then
                _G.SelectBoss = "Bobby [Lv. 55] [Boss]" 
			elseif v.Name == "Yeti [Lv. 110] [Boss]" and game.Players.localPlayer.Data.Level.Value >= 105  then
                _G.SelectBoss = "Yeti [Lv. 110] [Boss]"
			elseif v.Name == "Mob Leader [Lv. 120] [Boss]"  and game.Players.localPlayer.Data.Level.Value >= 120 then
                _G.SelectBoss = "Mob Leader [Lv. 120] [Boss]"
			elseif v.Name == "Vice Admiral [Lv. 130] [Boss]"  and game.Players.localPlayer.Data.Level.Value >= 130 then
                _G.SelectBoss = "Vice Admiral [Lv. 130] [Boss]"
			elseif v.Name == "Warden [Lv. 175] [Boss]" and game.Players.localPlayer.Data.Level.Value >= 175 then
                _G.SelectBoss = "Warden [Lv. 175] [Boss]"
			elseif v.Name == "Saber Expert [Lv. 200] [Boss]" and game.Workspace.Map.Jungle.Final.Part.Transparency == 1 then
				_G.SelectBoss = "Saber Expert [Lv. 200] [Boss]"
			elseif v.Name == "Chief Warden [Lv. 200] [Boss]"  and game.Players.localPlayer.Data.Level.Value >= 200 then
                _G.SelectBoss = "Chief Warden [Lv. 200] [Boss]"
			elseif v.Name == "Swan [Lv. 225] [Boss]"  and game.Players.localPlayer.Data.Level.Value >= 250 then
                _G.SelectBoss = "Swan [Lv. 225] [Boss]"
			elseif v.Name == "Magma Admiral [Lv. 350] [Boss]" and game.Players.localPlayer.Data.Level.Value >= 350  then
                _G.SelectBoss = "Magma Admiral [Lv. 350] [Boss]"
			elseif v.Name == "Fishman Lord [Lv. 425] [Boss]" and game.Players.localPlayer.Data.Level.Value >= 425  then
                _G.SelectBoss = "Fishman Lord [Lv. 425] [Boss]"
			elseif v.Name == "Wysper [Lv. 500] [Boss]" and game.Players.localPlayer.Data.Level.Value >= 500 then
                _G.SelectBoss = "Wysper [Lv. 500] [Boss]"
			elseif v.Name == "Thunder God [Lv. 575] [Boss]"  and game.Players.localPlayer.Data.Level.Value >= 575 then
                _G.SelectBoss = "Thunder God [Lv. 575] [Boss]"
			elseif v.Name == "Cyborg [Lv. 675] [Boss]" and game.Players.localPlayer.Data.Level.Value >= 675 then
                _G.SelectBoss = "Cyborg [Lv. 675] [Boss]"
				-- World2
			elseif v.Name == "Diamond [Lv. 750] [Boss]" and game.Players.localPlayer.Data.Level.Value >= 750 then
                _G.SelectBoss = "Diamond [Lv. 750] [Boss]"
			elseif v.Name == "Jeremy [Lv. 850] [Boss]" and game.Players.localPlayer.Data.Level.Value >= 850 then
                _G.SelectBoss = "Jeremy [Lv. 850] [Boss]"
			elseif v.Name == "Fajita [Lv. 925] [Boss]" and game.Players.localPlayer.Data.Level.Value >= 925  then
                _G.SelectBoss = "Fajita [Lv. 925] [Boss]"
			elseif v.Name == "Don Swan [Lv. 1000] [Boss]" and game.Players.localPlayer.Data.Level.Value >= 1000 and game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("TalkTrevor","1") == 0 then
                _G.SelectBoss = "Don Swan [Lv. 1000] [Boss]" 
			elseif v.Name == "Smoke Admiral [Lv. 1150] [Boss]" and game.Players.localPlayer.Data.Level.Value >= 1150 then
                _G.SelectBoss = "Smoke Admiral [Lv. 1150] [Boss]"
			elseif v.Name == "Cursed Captain [Lv. 1325] [Raid Boss]" and game.Players.localPlayer.Data.Level.Value >= 1325 then
                _G.SelectBoss = "Cursed Captain [Lv. 1325] [Raid Boss]"
			elseif v.Name == "Awakened Ice Admiral [Lv. 1400] [Boss]" and game.Players.localPlayer.Data.Level.Value >= 1400  then
                _G.SelectBoss = "Awakened Ice Admiral [Lv. 1400] [Boss]"
			elseif v.Name == "Tide Keeper [Lv. 1475] [Boss]" and game.Players.localPlayer.Data.Level.Value >= 1475  then
                _G.SelectBoss = "Tide Keeper [Lv. 1475] [Boss]"
				-- World3
			elseif v.Name == "Stone [Lv. 1550] [Boss]" and game.Players.localPlayer.Data.Level.Value >= 1550 then
                _G.SelectBoss = "Stone [Lv. 1550] [Boss]"
			elseif v.Name == "Island Empress [Lv. 1675] [Boss]" and game.Players.localPlayer.Data.Level.Value >= 1675 then
				_G.SelectBoss = "Island Empress [Lv. 1675] [Boss]"
			elseif v.Name == "Kilo Admiral [Lv. 1750] [Boss]" and game.Players.localPlayer.Data.Level.Value >= 1750 then
				_G.SelectBoss = "Kilo Admiral [Lv. 1750] [Boss]"
			elseif v.Name == "Captain Elephant [Lv. 1875] [Boss]" and game.Players.localPlayer.Data.Level.Value >= 1875 then
				_G.SelectBoss = "Captain Elephant [Lv. 1875] [Boss]"
			elseif v.Name == "Beautiful Pirate [Lv. 1950] [Boss]" and game.Players.localPlayer.Data.Level.Value >= 1950 then
				_G.SelectBoss = "Beautiful Pirate [Lv. 1950] [Boss]"
			elseif v.Name == "Cake Queen [Lv. 2175] [Boss]" and game.Players.localPlayer.Data.Level.Value >= 2175 then
				_G.SelectBoss = "Cake Queen [Lv. 2175] [Boss]"
			end 
		end 
	end
end
task.spawn(function()
	while wait() do
		if _G.AllBoss then
			GetBossName()
		end
	end
end)

    function itemequip(ToolSe)
        if game.Players.LocalPlayer.Backpack:FindFirstChild(ToolSe) then
            tool = game.Players.LocalPlayer.Backpack:FindFirstChild(ToolSe)
            wait(.1)
            game.Players.LocalPlayer.Character.Humanoid:EquipTool(tool)
        end
    end
    getgenv().Combat_Weapons_PVP=function(U,Y)
        task.spawn(function()
            for i,v in pairs(game.Players.LocalPlayer.Backpack:GetChildren()) do
                if v.ToolTip == U and v:IsA('Tool') then
                    local ToolHumanoid=game.Players.LocalPlayer.Backpack:FindFirstChild(v.Name) 
                    game.Players.LocalPlayer.Character.Humanoid:EquipTool(ToolHumanoid) 
                end
            end
            wait(2)
            for i,v in pairs(game.Players.LocalPlayer.Backpack:GetChildren()) do
                if v.ToolTip == Y and v:IsA('Tool') then
                    local ToolHumanoid=game.Players.LocalPlayer.Backpack:FindFirstChild(v.Name) 
                    game.Players.LocalPlayer.Character.Humanoid:EquipTool(ToolHumanoid) 
                end
            end
        end)
    end

    task.spawn(function()
        while wait() do 
            AttackRandomType = math.random(1,5)
            wait(0.5)
        end
    end)

    function Com(com,...)
        local Remote = game:GetService('ReplicatedStorage').Remotes:FindFirstChild("Comm"..com)
        if Remote:IsA("RemoteEvent") then
            Remote:FireServer(...)
        elseif Remote:IsA("RemoteFunction") then
            Remote:InvokeServer(...)
        end
    end
    getgenv().Island=function(Island)
        local RealtargetPos = {Island}
        local targetPos = RealtargetPos[1]
        local RealTarget
        if type(targetPos) == "vector" then
            RealTarget = targetPos
        elseif type(targetPos) == "userdata" then
            RealTarget = targetPos.Position
        elseif type(targetPos) == "number" then
            RealTarget = CFrame.new(unpack(RealtargetPos))
            RealTarget = RealTarget.Position
        end
        local ReturnValue
        local CheckInOut = math.huge;
        if game.Players.LocalPlayer.Team then
            for i,v in pairs(game.Workspace._WorldOrigin.PlayerSpawns:FindFirstChild(tostring(game.Players.LocalPlayer.Team)):GetChildren()) do 
                local ReMagnitude = (RealTarget - v:GetModelCFrame().Position).Magnitude;
                if ReMagnitude < CheckInOut then
                    CheckInOut = ReMagnitude;
                    ReturnValue = v.Name
                end
            end
            if ReturnValue then
                return ReturnValue
            end 
        end
    end
    Speed_Tween=360
    getgenv().Tween_To_Target=function(Target)
        if _G.Bypass then
        local Target_Position={Target}
        local Value_Target=Target_Position[1]
        local RealTarget
        if type(Value_Target)=='vector'then
            RealTarget=CFrame.new(Value_Target)
        elseif type(Value_Target)=='userdata'then
            RealTarget=Value_Target
        elseif type(Value_Target)=='number'then
            RealTarget=CFrame.new(unpack(RealTarget))
        end
        if game.Players.LocalPlayer.Character:WaitForChild('Humanoid').Health == 0 then if q then q:Cancel() end repeat wait() until game.Players.LocalPlayer.Character:WaitForChild('Humanoid').Health > 0; wait(0.2) end
        local Distance=(RealTarget.Position-game:GetService("Players").LocalPlayer.Character:WaitForChild("HumanoidRootPart").Position).Magnitude      
        if Distance>3000 then
            pcall(function()
                fkwarp=false
                if game:GetService("Players")["LocalPlayer"].Data:FindFirstChild("SpawnPoint").Value==tostring(getgenv().Island(RealTarget))then 
                    wait(.1)
                    Com("F_","TeleportToSpawn")
                elseif game:GetService('Players')['LocalPlayer'].Data:FindFirstChild('LastSpawnPoint').Value==tostring(getgenv().Island(RealTarget))then
                    game:GetService('Players').LocalPlayer.Character:WaitForChild('Humanoid'):ChangeState(15)
                    wait(0.1)
                    repeat wait()until game:GetService('Players').LocalPlayer.Character:WaitForChild('Humanoid').Health>0
                else
                    if game:GetService('Players').LocalPlayer.Character:WaitForChild('Humanoid').Health>0 then
                        if fkwarp==false then
                            game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame=RealTarget
                        end
                        fkwarp=true
                    end
                    wait(.08)
                    game:GetService('Players').LocalPlayer.Character:WaitForChild('Humanoid'):ChangeState(15)
                    repeat wait() until game:GetService('Players').LocalPlayer.Character:WaitForChild('Humanoid').Health>0
                    wait(.1)
                    Com("F_","SetSpawnPoint")
                end
                wait(0.2)
                return
            end)
        end
        if game:GetService('Players').LocalPlayer:DistanceFromCharacter(Target.Position)<=250 then
            game:GetService('Players').LocalPlayer.Character.HumanoidRootPart.CFrame=Target
        elseif not game.Players.LocalPlayer.Character:FindFirstChild('Root')then
            local K=Instance.new('Part',game.Players.LocalPlayer.Character)
            K.Size=Vector3.new(1,0.5,1)
            K.Name='Root'
            K.Anchored=true
            K.Transparency=1
            K.CanCollide=false
            K.CFrame=game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame*CFrame.new(0,20,0)
        end
        local z=game:service('TweenService')
        local B=TweenInfo.new((RealTarget.Position-game.Players.LocalPlayer.Character.Root.Position).Magnitude/Speed_Tween,Enum.EasingStyle.Linear)
        local S,g=pcall(function()
            local q=z:Create(game.Players.LocalPlayer.Character.Root,B,{CFrame=RealTarget})
            q:Play()
        end)
        if not S then
            return g
        end
        game.Players.LocalPlayer.Character.Root.CFrame=game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame
        if S and game.Players.LocalPlayer.Character:FindFirstChild('Root')then
            pcall(function()
                if(game.Players.LocalPlayer.Character.HumanoidRootPart.Position-Target.Position).Magnitude>=20 then
                    spawn(function()
                        pcall(function()
                            if(game.Players.LocalPlayer.Character.Root.Position-game.Players.LocalPlayer.Character.HumanoidRootPart.Position).Magnitude>150 then
                                game.Players.LocalPlayer.Character.Root.CFrame = game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame
                            else 
                                game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame=game.Players.LocalPlayer.Character.Root.CFrame
                            end
                        end)
                    end)
                elseif(game.Players.LocalPlayer.Character.HumanoidRootPart.Position-Target.Position).Magnitude>=10 and(game.Players.LocalPlayer.Character.HumanoidRootPart.Position-Target.Position).Magnitude<20 then
                    game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame=Target
                elseif(game.Players.LocalPlayer.Character.HumanoidRootPart.Position-Target.Position).Magnitude<10 then
                    game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame=Target
                end
            end)
        end
    else
        if game:GetService("Players").LocalPlayer:DistanceFromCharacter(Target.Position) <= 250 then 
            game:GetService("Players").LocalPlayer.Character.HumanoidRootPart.CFrame = Target
        elseif not game.Players.LocalPlayer.Character:FindFirstChild("Root")then 
            local K = Instance.new("Part",game.Players.LocalPlayer.Character)
            K.Size = Vector3.new(1,0.5,1)
            K.Name = "Root"
            K.Anchored = true
            K.Transparency = 1
            K.CanCollide = false
            K.CFrame = game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame * CFrame.new(0,20,0)
        end
        local U = (game.Players.LocalPlayer.Character.HumanoidRootPart.Position-Target.Position).Magnitude
        local z = game:service("TweenService")
        local B = TweenInfo.new((Target.Position-game.Players.LocalPlayer.Character.Root.Position).Magnitude/385,Enum.EasingStyle.Linear)
        local S,g = pcall(function()
        local q = z:Create(game.Players.LocalPlayer.Character.Root,B,{CFrame = Target})
        q:Play()
    end)
    if not S then 
        return g
    end
    game.Players.LocalPlayer.Character.Root.CFrame = game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame
        if S and game.Players.LocalPlayer.Character:FindFirstChild("Root") then 
            pcall(function()
                if (game.Players.LocalPlayer.Character.HumanoidRootPart.Position-Target.Position).Magnitude >= 20 then 
                    spawn(function()
                        pcall(function()
                            if (game.Players.LocalPlayer.Character.Root.Position-game.Players.LocalPlayer.Character.HumanoidRootPart.Position).Magnitude > 150 then 
                                game.Players.LocalPlayer.Character.Root.CFrame = game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame
                            else 
                                game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame=game.Players.LocalPlayer.Character.Root.CFrame
                            end
                        end)
                    end)
                elseif (game.Players.LocalPlayer.Character.HumanoidRootPart.Position-Target.Position).Magnitude >= 10 and(game.Players.LocalPlayer.Character.HumanoidRootPart.Position-Target.Position).Magnitude < 20 then 
                    game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = Target
                elseif (game.Players.LocalPlayer.Character.HumanoidRootPart.Position-Target.Position).Magnitude < 10 then 
                    game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = Target
                end
            end)
        end
    end
    end
    getgenv().Increase_Speed_Tween_Farm=function(T,P)
        task.spawn(function()
            for i,v in pairs(game:GetService('Workspace').Enemies:GetChildren())do
                if v.Name==tostring(P.Name)and(v.HumanoidRootPart.Position-T.Position).Magnitude<300 then
                    D=(v.HumanoidRootPart.Position-T.Position).Magnitude
                    if D<800 then
                        Speed_Tween=500
                    end
                end
            end
        end)
    end
    task.spawn(function()
        while task.wait() do 
            if  _G.AutoFarmcheck then 
                if _G.AutoShanda  then
                    _G.FastFram = true
                    _G.Kill_Player = false
                    _G.AutoFram = false
                    _G.DoubleQuest = false
                elseif not _G.AutoShanda and _G.AutoFramPly then
                    _G.FastFram = false
                    _G.Kill_Player = true
                    _G.AutoFram = false
                    _G.DoubleQuest = false
                elseif _G.AutoShanda and not _G.AutoFramPly then
                    game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("AbandonQuest")
                elseif not _G.AutoShanda and not _G.AutoFramPly then
                    _G.FastFram = false
                    
                    _G.AutoFram = true
                    _G.DoubleQuest = true
                end
            end
        end
    end)




    task.spawn(function()
        while wait() do
            if  _G.AutoFarmcheck then 
                    Playersv = #game:GetService("Players"):GetPlayers()
                    LVA = game:GetService("Players").LocalPlayer.Data.Level.Value
                    if LVA == 1 or LVA <= 19 then
                        _G.AutoFramPly = false
                        _G.AutoShanda = false
                    elseif LVA == 20 or LVA <= 65 then
                        _G.AutoFramPly = false
                        _G.AutoShanda = true         
                    elseif LVA >= 66 and Playersv >= 6 then
                        if game.Players.LocalPlayer.PlayerGui.Main.Quest.Visible == false then
                            if string.find(game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("PlayerHunter"), "I don't have anything") then
                                _G.AutoFramPly = false
                                _G.AutoShanda = false
                            else
                                _G.AutoFramPly = true
                                _G.AutoShanda = false
                            end
                        end
                    elseif LVA >= 66 and Playersv <= 5 then
                        _G.AutoFramPly = false
                        _G.AutoShanda = false
                    
                    elseif LVA >= 700 then
                        _G.AutoFramPly = false
                        _G.AutoShanda = false
                    end              
            else
                _G.Kill_Player = false
                _G.FastFram = false    
                _G.AutoFram = false
                _G.DoubleQuest = false
            end
        end
    end)

    local CameraShaker = require(game.ReplicatedStorage.Util.CameraShaker)
    spawn(function()
        while task.wait() do
            if _G.Kill_Player and _G.AutoFramPly  then
                pcall(function()
                    quest_title = game:GetService("Players").LocalPlayer.PlayerGui.Main.Quest.Container.QuestTitle.Title.Text
                    if string.find(quest_title, "Defeat") and string.find(quest_title, "(0/1)") then
                        local Player = string.split(quest_title, " ")[2]
                        local PlayerLevel = tonumber(game.Players[Player].Data.Level.Value)
                        if game:GetService("Workspace").Characters:FindFirstChild(Player) then
                            if PlayerLevel >= 20 and PlayerLevel <= (game.Players.LocalPlayer.Data.Level.Value + 400) then
                                for i, v in pairs(game:GetService("Workspace").Characters:GetChildren()) do
                                    if v.Name == tostring(Player) and v:FindFirstChild("Humanoid") and v.Humanoid.Health > 0 and
                                        v.Parent then
                                        if (game.Players.LocalPlayer.Character.HumanoidRootPart.Position -  v.HumanoidRootPart.Position).Magnitude <= 2100 or (v.HumanoidRootPart.Position -game.Players.LocalPlayer.Character.HumanoidRootPart.Position).Magnitude <= 2100 then                
                                            repeat task.wait(.1)
                                                if (game.Players.LocalPlayer.Character.HumanoidRootPart.Position - v.HumanoidRootPart.Position).Magnitude <= 45 or (v.HumanoidRootPart.Position - game.Players.LocalPlayer.Character.HumanoidRootPart.Position).Magnitude <= 45 then
                                                    getgenv().Combat_Weapons_PVP('Melee','Sword')
                                                    if not game.Players.LocalPlayer.Character:FindFirstChild('HasBuso') then
                                                        game.ReplicatedStorage.Remotes.CommF_:InvokeServer('Buso')
                                                    end

                                                    if game:GetService("Players")["LocalPlayer"].PlayerGui.Main.PvpDisabled.Visible == false then
                                                        v.HumanoidRootPart.Size = Vector3.new(50, 50, 50)
                                                        v.HumanoidRootPart.Transparency = 1
                                                        FastAttackk = true
                                                        if AttackRandomType == 1 then
                                                            getgenv().Tween_To_Target(v.HumanoidRootPart.CFrame * CFrame.new(0, 20, 1))
                                                        elseif AttackRandomType == 2 then
                                                            getgenv().Tween_To_Target(v.HumanoidRootPart.CFrame * CFrame.new(0, 1, 20))
                                                        elseif AttackRandomType == 3 then
                                                            getgenv().Tween_To_Target(v.HumanoidRootPart.CFrame * CFrame.new(1, 1, -20))
                                                        elseif AttackRandomType == 4 then
                                                            getgenv().Tween_To_Target(v.HumanoidRootPart.CFrame * CFrame.new(20, 1, 0))
                                                        elseif AttackRandomType == 5 then
                                                            
                                                        end
                                                        if game.Players.LocalPlayer.Character:FindFirstChild("Black Leg") and
                                                            game.Players.LocalPlayer.Character:FindFirstChild("Black Leg")
                                                                .Level.Value >= 150 then
                                                            game:service('VirtualInputManager'):SendKeyEvent(true, "V",
                                                                false, game)
                                                            game:service('VirtualInputManager'):SendKeyEvent(false, "V",
                                                                false, game)
                                                        end
                                                        game:service('VirtualInputManager'):SendKeyEvent(true, "Z", false,
                                                            game)
                                                        game:service('VirtualInputManager'):SendKeyEvent(false, "Z", false,
                                                            game)
                                                        wait()
                                                        game:service('VirtualInputManager'):SendKeyEvent(true, "X", false,
                                                            game)
                                                        game:service('VirtualInputManager'):SendKeyEvent(false, "X", false,
                                                            game)
                                                        wait(.1)
                                                        game:GetService 'VirtualUser':CaptureController()
                                                        game:GetService 'VirtualUser':Button1Down(Vector2.new(1280, 672))
                                                        Attack()
                                                        wait(0.1)
                                                        Boost()
                                                        sethiddenproperty(game.Players.LocalPlayer, "SimulationRadius",
                                                            math.huge)
                                                    else
                                                        repeat
                                                            wait()
                                                            game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer(
                                                                "EnablePvp")
                                                        until game:GetService("Players")["LocalPlayer"].PlayerGui.Main
                                                            .PvpDisabled.Visible == false
                                                    end
                                                else
                                                    getgenv().Tween_To_Target(v.HumanoidRootPart.CFrame * CFrame.new(30, 5, 0))
                                                end

                                            until not _G.Kill_Player or v.Humanoid.Health <= 0 or not v.Parent or
                                                game.Players.LocalPlayer.PlayerGui.Main.Quest.Visible == false or
                                                not _G.AutoFarmcheck
                                            game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("AbandonQuest")
                                            FastAttackk = false
                                        else
                                            getgenv().Tween_To_Target(v.HumanoidRootPart.CFrame)
                                        end
                                    end
                                end
                            else
                                game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("AbandonQuest")
                            end
                        else
                            game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("AbandonQuest")
                        end
                    else
                        game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("AbandonQuest")
                    end
                end)
            end
        end
    end)
    task.spawn(function()
        while wait() do
            if _G.AllBoss then
                pcall(function()
                    CheckBossQuest()
                    if MsBoss == "Soul Reaper [Lv. 2100] [Raid Boss]" or MsBoss == "Longma [Lv. 2000] [Boss]" or MsBoss == "Don Swan [Lv. 1000] [Boss]" or MsBoss == "Cursed Captain [Lv. 1325] [Raid Boss]" or MsBoss == "Order [Lv. 1250] [Raid Boss]" or MsBoss == "rip_indra True Form [Lv. 5000] [Raid Boss]" then
                        if game:GetService("ReplicatedStorage"):FindFirstChild(MsBoss) or game:GetService("Workspace").Enemies:FindFirstChild(MsBoss) then
                            if game:GetService("Workspace").Enemies:FindFirstChild(MsBoss) then
                                for i,v in pairs(game:GetService("Workspace").Enemies:GetChildren()) do
                                    if v.Name == MsBoss then
                                        repeat wait()
                                            _G.GetBoss = true
                     
                                                if not game.Players.LocalPlayer.Character:FindFirstChild("HasBuso") then
                                                    game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("Buso")
                                                end
                                 
                                     
                                                wait()
                                                itemequip(SelectWeapon) 

                                            StartMagnet = true
                                            FastAttack = true
                                            getgenv().Tween_To_Target(v.HumanoidRootPart.CFrame * CFrame.new(1,30,0))
                                            PosMon = v.HumanoidRootPart.CFrame
                                            v.HumanoidRootPart.Size = Vector3.new(60,60,60)
                                            v.Humanoid.JumpPower = 0
                                            v.Humanoid.WalkSpeed = 0
                                            v.HumanoidRootPart.CanCollide = false
                                            v.Humanoid:ChangeState(11)
                                        until _G.AllBoss == false or not v.Parent or v.Humanoid.Health <= 0
                                        _G.GetBoss = false
                                    end
                                end
                            else
                                _G.GetBoss = true
                                getgenv().Tween_To_Target(CFrameBoss)
                            end
                        else
                            _G.GetBoss = false
                        end
                    else
                        if _G.AllBoss then
                            CheckBossQuest()
                            if not string.find(game:GetService("Players").LocalPlayer.PlayerGui.Main.Quest.Container.QuestTitle.Title.Text, NameBoss) then
                                game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("AbandonQuest")
                            end
                            if game:GetService("Players").LocalPlayer.PlayerGui.Main.Quest.Visible == false then
                                _G.GetBoss = true
                                repeat wait() getgenv().Tween_To_Target(CFrameQuestBoss) until (CFrameQuestBoss.Position - game:GetService("Players").LocalPlayer.Character.HumanoidRootPart.Position).Magnitude <= 3 or not _G.AllBoss
                                if (CFrameQuestBoss.Position - game.Players.LocalPlayer.Character.HumanoidRootPart.Position).Magnitude <= 4 then
                                    wait(1.1)
                                    game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("StartQuest", NameQuestBoss, LevelQuestBoss)
                                end
                            elseif game:GetService("Players").LocalPlayer.PlayerGui.Main.Quest.Visible == true then
                                if game:GetService("ReplicatedStorage"):FindFirstChild(MsBoss) or game:GetService("Workspace").Enemies:FindFirstChild(MsBoss) then
                                    if game:GetService("Workspace").Enemies:FindFirstChild(MsBoss) then
                                        for i,v in pairs(game:GetService("Workspace").Enemies:GetChildren()) do
                                            if v.Name == MsBoss then
                                                repeat wait()
                                                    _G.GetBoss = true
                                                    if string.find(game:GetService("Players").LocalPlayer.PlayerGui.Main.Quest.Container.QuestTitle.Title.Text, NameBoss) then
                                                    
                                                            if not game.Players.LocalPlayer.Character:FindFirstChild("HasBuso") then
                                                                game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("Buso")
                                                            end
                                                 
                                                    
                                                            wait()
                                                            itemequip(SelectWeapon) 
                                                  
                                                        StartMagnet = true
                                                        FastAttack = true
                                                        getgenv().Tween_To_Target(v.HumanoidRootPart.CFrame * CFrame.new(1,30,0))
                                                        PosMon = v.HumanoidRootPart.CFrame
                                                        v.HumanoidRootPart.Size = Vector3.new(60,60,60)
                                                        v.Humanoid.JumpPower = 0
                                                        v.Humanoid.WalkSpeed = 0
                                                        v.HumanoidRootPart.CanCollide = false
                                                        v.Humanoid:ChangeState(11)								
                                                    else
                                                        game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("AbandonQuest")
                                                    end
                                                until _G.AllBoss == false or not v.Parent or v.Humanoid.Health <= 0
                                                _G.GetBoss = false
                                            end
                                        end
                                    else
                                        _G.GetBoss = true
                                        getgenv().Tween_To_Target(CFrameBoss)
                                    end
                                else
                                    _G.GetBoss = false
                                end
                            end
                        end
                    end
                end)
            end
        end
    end)
    task.spawn(function()
        while wait() do
            if _G.BossSelect then
                pcall(function()
                    CheckBossQuest()
                    if MsBoss == "Soul Reaper [Lv. 2100] [Raid Boss]" or MsBoss == "Longma [Lv. 2000] [Boss]" or MsBoss == "Don Swan [Lv. 1000] [Boss]" or MsBoss == "Cursed Captain [Lv. 1325] [Raid Boss]" or MsBoss == "Order [Lv. 1250] [Raid Boss]" or MsBoss == "rip_indra True Form [Lv. 5000] [Raid Boss]" then
                        if game:GetService("Workspace").Enemies:FindFirstChild(MsBoss) then
                            for i,v in pairs(game:GetService("Workspace").Enemies:GetChildren()) do
                                if v.Name == MsBoss then
                                    repeat wait()
                                    
                                            if not game.Players.LocalPlayer.Character:FindFirstChild("HasBuso") then
                                                game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("Buso")
                                            end
                                   

                                            wait()
                                            itemequip(SelectWeapon) 
                               
                                        StartMagnet = true
                                        FastAttack = true
                                        getgenv().Tween_To_Target(v.HumanoidRootPart.CFrame * CFrame.new(1,30,0))
                                        PosMon = v.HumanoidRootPart.CFrame
                                        v.HumanoidRootPart.Size = Vector3.new(60,60,60)
                                        v.Humanoid.JumpPower = 0
                                        v.Humanoid.WalkSpeed = 0
                                        v.HumanoidRootPart.CanCollide = false
                                        v.Humanoid:ChangeState(11)
                                    until _G.BossSelect == false or not v.Parent or v.Humanoid.Health <= 0
                                end
                            end
                        else
                            getgenv().Tween_To_Target(CFrameBoss)
                        end
                    else
                        if _G.BossSelect then
                            CheckBossQuest()
                            if not string.find(game:GetService("Players").LocalPlayer.PlayerGui.Main.Quest.Container.QuestTitle.Title.Text, NameBoss) then
                                game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("AbandonQuest")
                            end
                            if game:GetService("Players").LocalPlayer.PlayerGui.Main.Quest.Visible == false then
                                repeat wait() getgenv().Tween_To_Target(CFrameQuestBoss) until (CFrameQuestBoss.Position - game:GetService("Players").LocalPlayer.Character.HumanoidRootPart.Position).Magnitude <= 3 or not _G.BossSelect
                                if (CFrameQuestBoss.Position - game.Players.LocalPlayer.Character.HumanoidRootPart.Position).Magnitude <= 4 then
                                    wait(1.1)
                                    game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("StartQuest", NameQuestBoss, LevelQuestBoss)
                                end
                            elseif game:GetService("Players").LocalPlayer.PlayerGui.Main.Quest.Visible == true then
                                if game:GetService("Workspace").Enemies:FindFirstChild(MsBoss) then
                                    for i,v in pairs(game:GetService("Workspace").Enemies:GetChildren()) do
                                        if v.Name == MsBoss then
                                            repeat wait()
                                                if string.find(game:GetService("Players").LocalPlayer.PlayerGui.Main.Quest.Container.QuestTitle.Title.Text, NameBoss) then
                                            
                                                        if not game.Players.LocalPlayer.Character:FindFirstChild("HasBuso") then
                                                            game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("Buso")
                                                        end
                                              
                                              
                                                        wait()
                                                        itemequip(SelectWeapon) 
                                         
                                                    StartMagnet = true
                                                    FastAttack = true
                                                    getgenv().Tween_To_Target(v.HumanoidRootPart.CFrame * CFrame.new(1,30,0))
                                                    PosMon = v.HumanoidRootPart.CFrame
                                                    v.HumanoidRootPart.Size = Vector3.new(60,60,60)
                                                    v.Humanoid.JumpPower = 0
                                                    v.Humanoid.WalkSpeed = 0
                                                    v.HumanoidRootPart.CanCollide = false
                                                    v.Humanoid:ChangeState(11)								
                                                else
                                                    game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("AbandonQuest")
                                                end
                                            until _G.BossSelect == false or not v.Parent or v.Humanoid.Health <= 0
                                        end
                                    end
                                else
                                    getgenv().Tween_To_Target(CFrameBoss)
                                end
                            end
                        end
                    end
                end)
            end
        end
    end)
    local BossTable = {}
    for i, v in pairs(game:GetService("ReplicatedStorage"):GetChildren()) do
        if string.find(v.Name, "Boss") then
            if v.Name == "Ice Admiral [Lv. 700] [Boss]" then
    
            else
                table.insert(BossTable, v.Name)
            end
        end
    end
    local Boss_Dropdown =  Bosses:AddDropdown({
            Name = "Select Boss",
            Value = false, 
            List = BossTable,
            Callback = function(value)
                _G.SelectBoss = value
            end
        })
        Bosses:AddToggle({
            Name = "Auto Farm Boss",
            Value = false,
            Flag = "Auto Farm Boss .",
            Callback = function(value)
                _G.BossSelect= value
            end
        })
      
        Bosses:AddToggle({
            Name = "Auto Farm Boss All",
            Value = false,
            Flag = "Auto Farm Boss .",
            Callback = function(value)
                _G.AllBoss = value
                _G.GetBoss = false
                MsBoss = ""
            end
        })
    
        Bosses:AddToggle({
            Name = "Auto Farm Boss Hop",
            Value = false,
            Flag = "Auto Farm Boss Hop .",
            Callback = function(value)
            end
        })
        task.spawn(function()
            while task.wait() do
                table.clear(BossTable)
                for i, v in pairs(game:GetService("ReplicatedStorage"):GetChildren()) do
                    if string.find(v.Name, "Boss") then
                        if v.Name == "Ice Admiral [Lv. 700] [Boss]" then
    
                        else
                            table.insert(BossTable, v.Name)
                        end
                    end
                end
            end
        end)
    local CameraShaker = require(game.ReplicatedStorage.Util.CameraShaker)
    spawn(function()
        while wait() do
            if _G.AutoFram  and _G.DoubleQuest and Double_Quest_Farm then
                pcall(function()         
                    
                        if not string.find(game:GetService("Players").LocalPlayer.PlayerGui.Main.Quest.Container.QuestTitle.Title.Text, NameQ) then
                            StartMagnet = false
                            game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("AbandonQuest")
                        end
                        if game:GetService("Players").LocalPlayer.PlayerGui.Main.Quest.Visible == false then
                            StartMagnet = false
                            
                            repeat wait() 
                                if (CFrameQ.Position - game:GetService("Players").LocalPlayer.Character.HumanoidRootPart.Position).Magnitude >= 2200 then
                                    getgenv().Tween_To_Target(CFrameQ)   
                                else
                                    getgenv().Tween_To_Target(CFrameQ)  
                                end
                            until (CFrameQ.Position - game:GetService("Players").LocalPlayer.Character.HumanoidRootPart.Position).Magnitude <= 3 or not _G.AutoFram 
                            if (CFrameQ.Position - game:GetService("Players").LocalPlayer.Character.HumanoidRootPart.Position).Magnitude <= 3 then
                                wait(0.5)
                                game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("StartQuest",NameQuest,QuestLv)
                                    
                                    game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("StartQuest",NameQuest,QuestLv)            
                            end
                        elseif game:GetService("Players").LocalPlayer.PlayerGui.Main.Quest.Visible == true then
                           
                            if game:GetService("Workspace").Enemies:FindFirstChild(Ms) then
                                for i,v in pairs(game:GetService("Workspace").Enemies:GetChildren()) do
                                    if v:FindFirstChild("HumanoidRootPart") and v:FindFirstChild("Humanoid") and v.Humanoid.Health > 0 then
                                        if v.Name == Ms then
                                            repeat wait(_G.Fast_Delay)
                                                
                                                if string.find(game:GetService("Players").LocalPlayer.PlayerGui.Main.Quest.Container.QuestTitle.Title.Text, NameQ) then
                                                    if not game.Players.LocalPlayer.Character:FindFirstChild('HasBuso') then
                                                        game.ReplicatedStorage.Remotes.CommF_:InvokeServer('Buso')
                                                    end
                                                    itemequip(SelectWeapon) 
                                                    StartMagnet = true               
                                                    getgenv().Increase_Speed_Tween_Farm(v.HumanoidRootPart.CFrame,v)
                                                    getgenv().Tween_To_Target(v.HumanoidRootPart.CFrame * CFrame.new(0, 35, 1))
                                                    PosMon = v.HumanoidRootPart.CFrame
                                                    v.HumanoidRootPart.Size = Vector3.new(60,60,60)
                                                    v.HumanoidRootPart.CanCaillde = false  
                                                
                                                else
                                                    StartMagnet = false
                                                    game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("AbandonQuest")
                                                end
                                            until not _G.AutoFram   or v.Humanoid.Health <= 0 or not v.Parent or game:GetService("Players").LocalPlayer.PlayerGui.Main.Quest.Visible == false or not _G.AutoFarmcheck
                                            Speed_Tween=360
                                        end
                                    end
                                end
                            else
                                StartMagnet = false
                                if game:GetService("ReplicatedStorage"):FindFirstChild(Ms) then
                                    getgenv().Tween_To_Target(game:GetService("ReplicatedStorage"):FindFirstChild(Ms).HumanoidRootPart.CFrame)
                                else	
                                    if AttackRandomType == 1 then
                                        getgenv().Tween_To_Target(CFramePuk * CFrame.new(0, 20, 200))
                                    elseif AttackRandomType == 2 then
                                        getgenv().Tween_To_Target(CFramePuk * CFrame.new(-200, 20, 0))
                                    elseif AttackRandomType == 3 then
                                        getgenv().Tween_To_Target(CFramePuk * CFrame.new(0, 20, -200))
                                    elseif AttackRandomType == 4 then
                                        getgenv().Tween_To_Target(CFramePuk * CFrame.new(100, 20, 0))
                                    elseif AttackRandomType == 5 then
                                        getgenv().Tween_To_Target(CFramePuk * CFrame.new(0, 20, -200))
                                    end
                                end
                            end
                        end
                    end)
                end    
            end
        end)

        function CheckNotifyComplete()
            for i, v in pairs(game:GetService("Players")["LocalPlayer"].PlayerGui:FindFirstChild("Notifications"):GetChildren()) do
                if v.Name == "NotificationTemplate" then
                    if string.lower(v.Text):find("quest completed") then
                        pcall(function()
                            v:Destroy()
                        end)
                        return true
                    end
                end
            end
            return false
        end
        
        local NoLoopDuplicate = false
        local SubQuest = false
        local oldmob = Ms
        local oldcheckquest = NameQ
        
        task.spawn(function()
            while wait() do
                pcall(function()
                    if _G.AutoFram then
                        if _G.DoubleQuest then 
                            if SubQuest == true then 
                                if Double_Quest then 
                                    if tonumber(Double_Quest-1) ~= 0 then 
                                        Check_Double_Quest(tonumber(Double_Quest-1))
                                    end
                                end
                            else
                                CheckQuest()
                                oldmob = Ms
                                oldcheckquest = NameQ
                                spawn(function()
                                    pcall(function()
                                        if NoLoopDuplicate == false then 
                                            if CheckNotifyComplete() and _G.AutoFram then
                                                NoLoopDuplicate = true 
                                                while wait() do
                                                    SubQuest = true
                                                    if CheckNotifyComplete() or _G.AutoFram == false then
                                                        break;
                                                    end
                                                end
                                                SubQuest = false
                                                NoLoopDuplicate = false
                                            end
                                        end
                                    end)
                                end)
                                if SubQuest == true then  
                                    if Double_Quest then 
                                        if tonumber(Double_Quest-1) ~= 0 then 
                                            Check_Double_Quest(tonumber(Double_Quest-1))
                                        end
                                    end
                                end
                            end
                        else
                            CheckQuest()
                        end
                        Double_Quest_Farm=true
                    end
                end)
            end
        end)
        task.spawn(function()
            while wait() do
                pcall(function()
                    if _G.AutoFram and _G.Saber then
                        Auto_Farm_Level=true
                        else
                            Auto_Farm_Level=false
                    end
                end)
            end
        end)
        task.spawn(function()
            while wait() do
                pcall(function()
                    if _G.Saber and game.Players.LocalPlayer.Data.Level.Value >= 200 and not game:GetService("Players").LocalPlayer.Backpack:FindFirstChild("Saber") and not game.Players.LocalPlayer.Character:FindFirstChild("Saber") then
                        if Auto_Farm_Level then
                            _G.AutoFram = false
                        end
                        if game:GetService("Workspace").Map.Jungle.Final.Part.Transparency == 0 then
                            if game:GetService("Workspace").Map.Jungle.QuestPlates.Door.Transparency == 0 then
                                if (CFrame.new(-1612.55884, 36.9774132, 148.719543, 0.37091279, 3.0717151e-09, -0.928667724, 3.97099491e-08, 1, 1.91679348e-08, 0.928667724, -4.39869794e-08, 0.37091279).Position - game.Players.LocalPlayer.Character.HumanoidRootPart.Position).Magnitude <= 100 then
                                    getgenv().Tween_To_Target(game:GetService("Players").LocalPlayer.Character.HumanoidRootPart.CFrame)
                                    wait(1)
                                    game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = game:GetService("Workspace").Map.Jungle.QuestPlates.Plate1.Button.CFrame
                                    wait(1)
                                    game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = game:GetService("Workspace").Map.Jungle.QuestPlates.Plate2.Button.CFrame
                                    wait(1)
                                    game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = game:GetService("Workspace").Map.Jungle.QuestPlates.Plate3.Button.CFrame
                                    wait(1)
                                    game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = game:GetService("Workspace").Map.Jungle.QuestPlates.Plate4.Button.CFrame
                                    wait(1)
                                    game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = game:GetService("Workspace").Map.Jungle.QuestPlates.Plate5.Button.CFrame
                                    wait(1) 
                                else
                                    getgenv().Tween_To_Target(CFrame.new(-1612.55884, 36.9774132, 148.719543, 0.37091279, 3.0717151e-09, -0.928667724, 3.97099491e-08, 1, 1.91679348e-08, 0.928667724, -4.39869794e-08, 0.37091279))
                                end
                            else
                                if game:GetService("Workspace").Map.Desert.Burn.Part.Transparency == 0 then
                                    if game:GetService("Players").LocalPlayer.Backpack:FindFirstChild("Torch") or game.Players.LocalPlayer.Character:FindFirstChild("Torch") then
                                        itemequip("Torch")
                                        getgenv().Tween_To_Target(CFrame.new(1114.61475, 5.04679728, 4350.22803, -0.648466587, -1.28799094e-09, 0.761243105, -5.70652914e-10, 1, 1.20584542e-09, -0.761243105, 3.47544882e-10, -0.648466587))
                                    else
                                        getgenv().Tween_To_Target(CFrame.new(-1610.00757, 11.5049858, 164.001587, 0.984807551, -0.167722285, -0.0449818149, 0.17364943, 0.951244235, 0.254912198, 3.42372805e-05, -0.258850515, 0.965917408))                 
                                    end
                                else
                                    if game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("ProQuestProgress","SickMan") ~= 0 then
                                        game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("ProQuestProgress","GetCup")
                                        wait(0.5)
                                        itemequip("Cup")
                                        wait(0.5)
                                        game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("ProQuestProgress","FillCup",game:GetService("Players").LocalPlayer.Character.Cup)
                                        wait(0)
                                        game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("ProQuestProgress","SickMan") 
                                    else
                                        if game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("ProQuestProgress","RichSon") == nil then
                                            game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("ProQuestProgress","RichSon")
                                        elseif  game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("ProQuestProgress","RichSon") == 0 then
                                            if game:GetService("Workspace").Enemies:FindFirstChild("Mob Leader [Lv. 120] [Boss]") or game:GetService("ReplicatedStorage"):FindFirstChild("Mob Leader [Lv. 120] [Boss]") then
                                                getgenv().Tween_To_Target(CFrame.new(-2967.59521, -4.91089821, 5328.70703, 0.342208564, -0.0227849055, 0.939347804, 0.0251603816, 0.999569714, 0.0150796166, -0.939287126, 0.0184739735, 0.342634559))
                                                for i,v in pairs(game:GetService("Workspace").Enemies:GetChildren()) do
                                                    if v.Name == "Mob Leader [Lv. 120] [Boss]" then
                                                        repeat wait()
                                                            StartMagnet = true
                                                            FastAttack = true
                                                
                                                                if not game.Players.LocalPlayer.Character:FindFirstChild("HasBuso") then
                                                                    game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("Buso")
                                                                end
                                                         
                                                            if not game.Players.LocalPlayer.Character:FindFirstChild(SelectWeapon) then
                                                                wait()
                                                                itemequip(SelectWeapon)
                                                            end
                                                            getgenv().Tween_To_Target(v.HumanoidRootPart.CFrame * CFrame.new(0,0,0))
                                                            PosMon = v.HumanoidRootPart.CFrame
                                         
                                                                game:GetService'VirtualUser':CaptureController()
                                                                game:GetService'VirtualUser':Button1Down(Vector2.new(1280, 672))
                                             
                                                            v.HumanoidRootPart.Size = Vector3.new(60,60,60)

                                                                v.HumanoidRootPart.Transparency = 1
                                                            v.Humanoid.JumpPower = 0
                                                            v.Humanoid.WalkSpeed = 0
                                                            v.HumanoidRootPart.CanCollide = false
                                                            v.Humanoid:ChangeState(11)
                                                        until v.Humanoid.Health <= 0 or _G.Saber == false
                                                    end
                                                end
                                            end
                                        elseif game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("ProQuestProgress","RichSon") == 1 then
                                            game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("ProQuestProgress","RichSon")
                                            wait(0.5)
                                            itemequip("Relic")
                                            wait(0.5)
                                            getgenv().Tween_To_Target(CFrame.new(-1404.91504, 29.9773273, 3.80598116, 0.876514494, 5.66906877e-09, 0.481375456, 2.53851997e-08, 1, -5.79995607e-08, -0.481375456, 6.30572643e-08, 0.876514494))
                                        end
                                    end
                                end
                            end
                        else
                            if game:GetService("Workspace").Enemies:FindFirstChild("Saber Expert [Lv. 200] [Boss]") or game:GetService("ReplicatedStorage"):FindFirstChild("Saber Expert [Lv. 200] [Boss]") then
                                getgenv().Tween_To_Target(CFrame.new(-1401.85046, 29.9773273, 8.81916237, 0.85820812, 8.76083845e-08, 0.513301849, -8.55007443e-08, 1, -2.77243419e-08, -0.513301849, -2.00944328e-08, 0.85820812))
                                for i,v in pairs(game:GetService("Workspace").Enemies:GetChildren()) do
                                    if v.Name == "Saber Expert [Lv. 200] [Boss]" then
                                        repeat wait()
                                            StartMagnet = true
                                            FastAttack = true
                                   
                                                if not game.Players.LocalPlayer.Character:FindFirstChild("HasBuso") then
                                                    game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("Buso")
                                                end
                                         
                                            if not game.Players.LocalPlayer.Character:FindFirstChild(SelectWeapon) then
                                                wait()
                                                itemequip(SelectWeapon)
                                            end
                                            getgenv().Tween_To_Target(v.HumanoidRootPart.CFrame * CFrame.new(0,0,0))
                                            PosMon = v.HumanoidRootPart.CFrame
                                    
                                                game:GetService'VirtualUser':CaptureController()
                                                game:GetService'VirtualUser':Button1Down(Vector2.new(1280, 672))
                                         
                                            v.HumanoidRootPart.Size = Vector3.new(60,60,60)
                                                v.HumanoidRootPart.Transparency = 1
                                            v.Humanoid.JumpPower = 0
                                            v.Humanoid.WalkSpeed = 0
                                            v.HumanoidRootPart.CanCollide = false
                                            v.Humanoid:ChangeState(11)
                                            game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("SetSpawnPoint")
                                        until v.Humanoid.Health <= 0 or _G.Saber == false
                                        if v.Humanoid.Health <= 0 then
                                            game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("ProQuestProgress","PlaceRelic")
                                        end
                                        _G.AutoFram = true
                                    end
                                end
                            end
                        end
                    end
                end)
            end
        end)
        spawn(function()
            while wait() do
                if _G.FastFram   then
                    pcall(function()
                        if game:GetService("Workspace").Enemies:FindFirstChild('Shanda [Lv. 475]') then
                            for i, v in pairs(game:GetService("Workspace").Enemies:GetChildren()) do
                                if v.Name == 'Shanda [Lv. 475]' then
                                    repeat wait( 0.2)
                                        if not game.Players.LocalPlayer.Character:FindFirstChild('HasBuso') then
                                            game.ReplicatedStorage.Remotes.CommF_:InvokeServer('Buso')
                                        end
                                        itemequip(SelectWeapon)
                                        getgenv().Increase_Speed_Tween_Farm(v.HumanoidRootPart.CFrame,v)
                                        getgenv().Tween_To_Target(v.HumanoidRootPart.CFrame * CFrame.new(0, 20, 0))
                                        v.HumanoidRootPart.Size = Vector3.new(60, 60, 60)
                                        v.Humanoid.JumpPower = 0
                                        StartMagnetFast = true
                                        v.Humanoid.WalkSpeed = 0
                                        PosMon =  v.HumanoidRootPart.CFrame 
                                        v.HumanoidRootPart.CanCollide = false
                                        v.Humanoid:ChangeState(11)
                                        sethiddenproperty(game.Players.LocalPlayer, "SimulationRadius", math.huge)
                                    until _G.FastFram == false or v.Humanoid.Health <= 0 or not _G.AutoFarmcheck
                                    StartMagnetFast = false
                                    Speed_Tween=360
                                end
                            end
                        else
                            cfs = CFrame.new(-7682.69775, 5607.36279, -445.691833, 0.786274791, -4.48163426e-08, -0.617877364,
                                -4.81674345e-09, 1, -7.86622607e-08, 0.617877364, 6.48263239e-08, 0.786274791)
                            if (game.Players.LocalPlayer.Character.HumanoidRootPart.Position - cfs.Position).Magnitude <= 500 then
                                getgenv().Tween_To_Target(cfs)
                            else
                                wait(.6)
                                game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("requestEntrance", Vector3.new(
                                    -7894.6176757813, 5547.1416015625, -380.29119873047))
                            end
                        end
                    end)
                end
            end
        end)
        

        spawn(function()
            game:GetService("RunService").Heartbeat:Connect(function() 
                pcall(function()
                        for i,v in pairs(game:GetService("Workspace").Enemies:GetChildren()) do
                            if  StartMagnetFast and  (v.HumanoidRootPart.Position - PosMon.Position).magnitude <= 350 then
                                v.HumanoidRootPart.CFrame = PosMon
                                v.HumanoidRootPart.CanCollide = false
                                v.HumanoidRootPart.Size = Vector3.new(50,50,50)
                                if v.Humanoid:FindFirstChild("Animator") then
                                    v.Humanoid.Animator:Destroy()
                                end
                                sethiddenproperty(game.Players.LocalPlayer, "SimulationRadius",  math.huge)
                            end
                        end
                end)
            end)
        end)


        spawn(function()
            game:GetService("RunService").Heartbeat:Connect(function() 
                pcall(function()
                    for i,v in pairs(game:GetService("Workspace").Enemies:GetChildren()) do
                        if   _G.AutoFram  and StartMagnet and v.Name == Ms and (v.HumanoidRootPart.Position - PosMon.Position).Magnitude <= 350 then
                            v.HumanoidRootPart.CFrame = PosMon
                            v.HumanoidRootPart.CanCollide = false
                            v.HumanoidRootPart.Size = Vector3.new(50,50,50)
                            if v.Humanoid:FindFirstChild("Animator") then
                                v.Humanoid.Animator:Destroy()
                            end
                            sethiddenproperty(game.Players.LocalPlayer, "SimulationRadius",  math.huge)
                        end
                    end
                end)
            end)
        end)

        spawn(function()
            pcall(function()
                game:GetService("RunService").Stepped:Connect(function()
                    if _G.AutoFarmcheck or _G.Start or _G.BossSelect or _G.AllBoss then
                        if not game.Players.LocalPlayer.Character.HumanoidRootPart:FindFirstChild("BodyClip") then
                            local Noclip = Instance.new("BodyVelocity")
                            Noclip.Name = "BodyClip"
                            Noclip.Parent = game.Players.LocalPlayer.Character.HumanoidRootPart
                            Noclip.MaxForce = Vector3.new(100000,100000,100000)
                            Noclip.Velocity = Vector3.new(0,0,0)
                        end
                    else	
                        if game.Players.LocalPlayer.Character.HumanoidRootPart:FindFirstChild("BodyClip") then
                            game.Players.LocalPlayer.Character.HumanoidRootPart:FindFirstChild("BodyClip"):Destroy()
                        end
                    end
                end)
            end)
        end)
        
        spawn(function()
            pcall(function()
                game:GetService("RunService").Stepped:Connect(function()
                    if _G.AutoFarmcheck or _G.Start or _G.BossSelect or _G.AllBoss then
                        for _, v in pairs(game.Players.LocalPlayer.Character:GetDescendants()) do
                            if v:IsA("BasePart") then
                                v.CanCollide = false    
                            end
                        end
                    end
                end)
            end)
        end)


        spawn(function()
            while wait(.25) do
                if _G.Auto_Superhuman or _G.Auto_Fully_Superhuman and game.Players.LocalPlayer:FindFirstChild("WeaponAssetCache") then 
                    pcall(function()
                        if game:GetService("Players").LocalPlayer.Data.Beli.Value >= 500000 and (game.Players.LocalPlayer.Character:FindFirstChild("Combat") or game.Players.LocalPlayer.Backpack:FindFirstChild("Combat")) then
                            SelectWeapon = "Combat"
                            local args = {
                                [1] = "BuyElectro"
                            }
                            game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer(unpack(args))
                        end   
                        if game.Players.LocalPlayer.Character:FindFirstChild("Superhuman") or game.Players.LocalPlayer.Backpack:FindFirstChild("Superhuman") then
                            SelectWeapon = "Superhuman"
                        end  
                        if game.Players.LocalPlayer.Backpack:FindFirstChild("Black Leg") and game.Players.LocalPlayer.Backpack:FindFirstChild("Black Leg").Level.Value <= 299  then
                            SelectWeapon = "Black Leg"
                        end
                        if game.Players.LocalPlayer.Backpack:FindFirstChild("Electro") and game.Players.LocalPlayer.Backpack:FindFirstChild("Electro").Level.Value <= 299  then
                            SelectWeapon = "Electro"
                        end
                        if game.Players.LocalPlayer.Backpack:FindFirstChild("Fishman Karate") and game.Players.LocalPlayer.Backpack:FindFirstChild("Fishman Karate").Level.Value <= 299  then
                            SelectWeapon = "Fishman Karate"
                        end
                        if game.Players.LocalPlayer.Backpack:FindFirstChild("Dragon Claw") and game.Players.LocalPlayer.Backpack:FindFirstChild("Dragon Claw").Level.Value <= 299  then
                            SelectWeapon= "Dragon Claw"
                        end
                        if game.Players.LocalPlayer.Backpack:FindFirstChild("Black Leg") and game.Players.LocalPlayer.Backpack:FindFirstChild("Black Leg").Level.Value >= 300  then
                            local args = {
                                [1] = "BuyFishmanKarate"
                            }
                            game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer(unpack(args))
                        end
                        if game.Players.LocalPlayer.Character:FindFirstChild("Black Leg") and game.Players.LocalPlayer.Character:FindFirstChild("Black Leg").Level.Value >= 300  then
                            local args = {
                                [1] = "BuyFishmanKarate"
                            }
                            game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer(unpack(args))
                        end
                        if game.Players.LocalPlayer.Character:FindFirstChild("Electro") and game.Players.LocalPlayer.Character:FindFirstChild("Electro").Level.Value >= 300  then
                            local args = {
                                [1] = "BuyBlackLeg"
                            }
                            game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer(unpack(args))
                        end
                        if game.Players.LocalPlayer.Backpack:FindFirstChild("Fishman Karate") and game.Players.LocalPlayer.Backpack:FindFirstChild("Fishman Karate").Level.Value >= 300  then
                            if _G.Auto_Fully_Superhuman and game.Players.LocalPlayer.Data.Fragments.Value < 1500 then
                                if game.Players.LocalPlayer.Data.Level.Value > 1100 then
                                    _G.Select_Dungeon = "Flame"
                                    _G.Auto_Buy_Chips_Dungeon = true
                                    _G.Auto_Start_Dungeon = true
                                    _G.Auto_Next_Island = true
                                    _G.Kill_Aura = true
                                end
                            else
                                _G.Auto_Buy_Chips_Dungeon = false
                                _G.Auto_Start_Dungeon = false
                                _G.Auto_Next_Island = false
                                _G.Kill_Aura = false
                                local args = {
                                    [1] = "BlackbeardReward",
                                    [2] = "DragonClaw",
                                    [3] = "2"
                                }
                                game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer(unpack(args))
                            end
                        end
                        if game.Players.LocalPlayer.Character:FindFirstChild("Fishman Karate") and game.Players.LocalPlayer.Character:FindFirstChild("Fishman Karate").Level.Value >= 300  then
                            if _G.Auto_Fully_Superhuman and game.Players.LocalPlayer.Data.Fragments.Value < 1500 then
                                if game.Players.LocalPlayer.Data.Level.Value > 1100 then
                                    _G.Select_Dungeon = "Flame"
                                    _G.Auto_Buy_Chips_Dungeon = true
                                    _G.Auto_Start_Dungeon = true
                                    _G.Auto_Next_Island = true
                                    _G.Kill_Aura = true
                                end
                            else
                                _G.Auto_Buy_Chips_Dungeon = false
                                _G.Auto_Start_Dungeon = false
                                _G.Auto_Next_Island = false
                                _G.Kill_Aura = false
                                local args = {
                                    [1] = "BlackbeardReward",
                                    [2] = "DragonClaw",
                                    [3] = "2"
                                }
                                game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer(unpack(args))
                            end
                        end
                        if game.Players.LocalPlayer.Backpack:FindFirstChild("Dragon Claw") and game.Players.LocalPlayer.Backpack:FindFirstChild("Dragon Claw").Level.Value >= 300  then
                            local args = {
                                [1] = "BuySuperhuman"
                            }
                            game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer(unpack(args))
                        end
                        if game.Players.LocalPlayer.Character:FindFirstChild("Dragon Claw") and game.Players.LocalPlayer.Character:FindFirstChild("Dragon Claw").Level.Value >= 300  then
                            local args = {
                                [1] = "BuySuperhuman"
                            }
                            game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer(unpack(args))
                        end 
                    end)
                end
            end
        end)
        local plr = game.Players.LocalPlayer
        local CbFw = getupvalues(require(plr.PlayerScripts.CombatFramework))
        local CbFw2 = CbFw[2]
    
        function GetCurrentBlade() 
            local p13 = CbFw2.activeController
            local ret = p13.blades[1]
            if not ret then return end
            while ret.Parent~=game.Players.LocalPlayer.Character do ret=ret.Parent end
            return ret
        end
        local CameraShaker = require(game.ReplicatedStorage.Util.CameraShaker)
        for i,v in pairs(getreg()) do
            if typeof(v) == "function" and getfenv(v).script == game:GetService("Players").LocalPlayer.PlayerScripts.CombatFramework then
                for x,w in pairs(debug.getupvalues(v)) do
                    if typeof(w) == "table" then
                        task.spawn(function()
                            game:GetService("RunService").RenderStepped:Connect(function()
                                if _G.Fast_Attack then
                                    pcall(function()
                                        CameraShaker:Stop()
                                        w.activeController.increment = 10
                                        w.activeController.timeToNextAttack = -(math.huge^math.huge^math.huge)
                                        w.activeController.attacking = false
                                        w.activeController.timeToNextBlock = 0
                                        w.activeController.blocking = false                            
                                        w.activeController.hitboxMagnitude = 50
                                        w.activeController.humanoid.AutoRotate = true
                                        w.activeController.focusStart = 0
                                    end)
                                end
                            end)
                        end)
                    end
                end
            end
        end
        local SeraphFrame = debug.getupvalues(require(game:GetService("Players").LocalPlayer.PlayerScripts:WaitForChild("CombatFramework")))[2]
        local VirtualUser = game:GetService('VirtualUser')
        local RigControllerR = debug.getupvalues(require(game:GetService("Players").LocalPlayer.PlayerScripts.CombatFramework.RigController))[2]
        local Client = game:GetService("Players").LocalPlayer
        local DMG = require(Client.PlayerScripts.CombatFramework.Particle.Damage)
        function SeraphFuckWeapon() 
            local p13 = SeraphFrame.activeController
            local wea = p13.blades[1]
            if not wea then return end
            while wea.Parent~=game.Players.LocalPlayer.Character do wea=wea.Parent end
            return wea
        end
        function getHits(Size)
            local Hits = {}
            local Enemies = workspace.Enemies:GetChildren()
            local Characters = workspace.Characters:GetChildren()
            for i=1,#Enemies do local v = Enemies[i]
                local Human = v:FindFirstChildOfClass("Humanoid")
                if Human and Human.RootPart and Human.Health > 0 and game.Players.LocalPlayer:DistanceFromCharacter(Human.RootPart.Position) < Size+5 then
                    table.insert(Hits,Human.RootPart)
                end
            end
            for i=1,#Characters do local v = Characters[i]
                if v ~= game.Players.LocalPlayer.Character then
                    local Human = v:FindFirstChildOfClass("Humanoid")
                    if Human and Human.RootPart and Human.Health > 0 and game.Players.LocalPlayer:DistanceFromCharacter(Human.RootPart.Position) < Size+5 then
                        table.insert(Hits,Human.RootPart)
                    end
                end
            end
            return Hits
        end
        task.spawn(
            function()
            while wait(0) do
                if  _G.FastAttackNormalSpeed then
                    if SeraphFrame.activeController then
                        SeraphFrame.activeController.timeToNextAttack = 0
                        SeraphFrame.activeController.focusStart = 0
                        SeraphFrame.activeController.hitboxMagnitude = 40
                        SeraphFrame.activeController.humanoid.AutoRotate = true
                        SeraphFrame.activeController.increment = 1 + 1 / 1
                    end
                end
            end
        end)
        function Boost()
            spawn(function()
            game:GetService("ReplicatedStorage").RigControllerEvent:FireServer("weaponChange",tostring(SeraphFuckWeapon()))
            end)
        end
        function Unboost()
            spawn(function()
                game:GetService("ReplicatedStorage").RigControllerEvent:FireServer("unequipWeapon",tostring(SeraphFuckWeapon()))
            end)
        end
        local cdnormal = 0
        local Animation = Instance.new("Animation")
        local CooldownFastAttack = 0
        Attack = function()
            local ac = SeraphFrame.activeController
            if ac and ac.equipped then
                task.spawn(
                    function()
                    if tick() - cdnormal > 0.5 then
                        ac:attack()
                        cdnormal = tick()
                    else
                         Animation.AnimationId = ac.anims.basic[2]
                        ac.humanoid:LoadAnimation(Animation):Play(2, 2)
                        game:GetService("ReplicatedStorage").RigControllerEvent:FireServer("hit", getHits(120), 2, "")
                    end
                end)
            end
        end
        b = tick()
        spawn(function()
            while task.wait(0) do
                if  _G.FastAttackNormalSpeed then
                    if b - tick() > 0.75 then
                        wait(.2)
                        b = tick()
                    end
                    pcall(function()
                        for i, v in pairs(game.Workspace.Enemies:GetChildren()) do
                            if v.Humanoid.Health > 0 then
                                if (v.HumanoidRootPart.Position - game.Players.LocalPlayer.Character.HumanoidRootPart.Position).Magnitude <= 40 then
                                    Attack()
                                    wait(0)
                                    Boost()
                                end
                            end
                        end
                    end)
                end
            end
        end)
        k = tick()
        spawn(function()
            while wait(0) do
                if  _G.FastAttackNormalSpeed then
                    if k - tick() > 0.75 then
                        wait(0)
                        k = tick()
                    end
                    pcall(function()
                        for i, v in pairs(game.Workspace.Enemies:GetChildren()) do
                            if v.Humanoid.Health > 0 then
                                if (v.HumanoidRootPart.Position - game.Players.LocalPlayer.Character.HumanoidRootPart.Position).Magnitude <= 40 then
                                wait(0)
                                Unboost()
                                end
                            end
                        end
                    end)
                end
            end
        end)
        local Client = game.Players.LocalPlayer
        local STOP = require(Client.PlayerScripts.CombatFramework.Particle)
        local STOPRL = require(game:GetService("ReplicatedStorage").CombatFramework.RigLib)
        task.spawn(function()
            while task.wait() do
                pcall(function()
                    if not shared.orl then shared.orl = STOPRL.wrapAttackAnimationAsync end
                    if not shared.cpc then shared.cpc = STOP.play end
                        STOPRL.wrapAttackAnimationAsync = function(a,b,c,d,func)
                        local Hits = STOPRL.getBladeHits(b,c,d)
                        if Hits then
                            if _G.Fast_Attack then
                                STOP.play = function() end
                                a:Play(0.01,0.01,0.01)
                                func(Hits)
                                STOP.play = shared.cpc
                                a:Play()
                            end
                        end
                    end
                end)
            end
        end)
            if _G.Kill_Player then
                local Fast = getupvalues(require(game:GetService("Players").LocalPlayer.PlayerScripts.CombatFramework))
                local Lop = Fast[2]
                Lop.activeController.timeToNextAttack = (-math.huge^math.huge*math.huge)
                Lop.activeController.attacking = false
                Lop.activeController.timeToNextBlock = 0
                Lop.activeController.humanoid.AutoRotate = 80
                Lop.activeController.increment = 3
                Lop.activeController.blocking = false
                Lop.activeController.hitboxMagnitude = 80
                Attack()
                wait(0.1)
                Boost()
            end
  
        local Tp = IslandTab:CreateSection({
            Name = "// Island //"
        })

        if OldWolrd then
            Island = {
                "Colosseum",
                "Desert",
                "Snow Island",
                "Magma",
                "Pirate Village",
                "Prison",
                "Snow Island",
                "MarineFord",
                "Sky  1",
                "Sky  2",
                "Fountain City",
                }
       
        end

        Tp:AddDropdown({
            Name = "Select Island",
            Flag = "Select_Island",
            List = Island,
            Value = _G.Select ,
            Callback = function(value)
                _G.Select = value
            end
        })
        
        Tp:AddToggle({
            Name = "Teleport",
            Flag = "Teleport",
            Value = _G.Start,
            Callback = function(value)
                _G.Start = value    
                if _G.Start == true then
                    repeat wait()
                        if _G.Select == "Colosseum" then
                            getgenv().Tween_To_Target(CFrame.new(-1496.73206, 7.38933802, -2928.0437, -0.876864791, 1.27515394e-08, -0.48073712, 2.64718789e-08, 1, -2.17597513e-08, 0.48073712, -3.18063726e-08, -0.876864791))
                        elseif _G.Select == "Desert" then
                            getgenv().Tween_To_Target(CFrame.new(943.7542724609375, 6.601687908172607, 4233.7216796875))
                        elseif _G.Select == "Snow Island" then
                            getgenv().Tween_To_Target(CFrame.new(1152.290771484375, 7.303403377532959, -1202.771240234375))
                        elseif _G.Select == "Magma" then
                            getgenv().Tween_To_Target(CFrame.new(-5224.455078125, 8.623546600341797, 8434.7080078125))
                        elseif _G.Select == "Pirate Village" then 
                            getgenv().Tween_To_Target(CFrame.new(-1159.470947265625, 4.752050399780273, 3817.74951171875))
                        elseif _G.Select == "Prison"  then
                            getgenv().Tween_To_Target(CFrame.new(4850.544921875, 5.652063846588135, 735.5812377929688))
                        elseif _G.Select == "Sky  1"  then
                            getgenv().Tween_To_Target(CFrame.new(-4868.55029296875, 717.7359619140625, -2576.03466796875))
                        elseif _G.Select == "Sky  2" then
                            game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("requestEntrance",Vector3.new(-4607.82275, 872.54248, -1667.55688))
                        elseif _G.Select == "Fountain City" then
                            getgenv().Tween_To_Target(CFrame.new(5127.1284179688, 59.501365661621, 4105.4458007813))
                        elseif _G.Select == "MarineFord" then
                            getgenv().Tween_To_Target(CFrame.new(-4887.47998046875, 22.65203285217285, 4250.78271484375))
                        end
                    until not _G.Start
                end
                q:Cancel()
            end
        })
return library, library_flags, library.subs
