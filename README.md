<h1 align="center">Otter</h1>

<div align="center">
	An animation module for Roblox interface, with Signals, Motors, and Springs.
</div>

<div>&nbsp;</div>

## Installation

### Method 1: Model File (Roblox Studio)
* Download the `rbxm` model file attached to the latest release from the [GitHub releases page](https://github.com/azumanga/Otter/releases).
* Insert the model into Studio into a place like `ReplicatedStorage`

### Method 2: Filesystem
* Copy the `src` directory into your codebase
* Rename the folder to `Otter`
* Use a plugin like [Rojo](https://github.com/LPGhatguy/rojo) to sync the files into a place

## [Documentation](https://roblox.github.io/otter)
For a detailed guide and examples, check out [the official Otter documentation](https://roblox.github.io/otter).

```lua
--[[
    This code demonstrates Otter capabiltiies.
    It makes a frame that will follow the mouse.
    Make sure to have Otter in ReplicatedStorage!
]]
local ReplicatedStorage = game:GetService("ReplicatedStorage")
local Players = game:GetService("Players")

local Otter = require(ReplicatedStorage.Otter)

local localPlayer = Players.LocalPlayer
local mouse = localPlayer:GetMouse()

local container = Instance.new("ScreenGui")
container.ResetOnSpawn = false
container.Parent = localPlayer:WaitForChild("PlayerGui")

local frame = Instance.new("Frame")
frame.AnchorPoint = Vector2.new(1, 1)
frame.Size = UDim2.new(0, 20, 0, 20)
frame.BorderSizePixel = 0
frame.BackgroundColor3 = Color3.fromRGB(255, 255, 255)
frame.Parent = container

local positionMotor = Otter.createGroupMotor({
    x = 0,
    y = 0,
})

positionMotor:onStep(function(values)
    frame.Position = UDim2.new(0, values.x, 0, values.y)
end)

local function updateMotor()
    positionMotor:setGoal({
        x = Otter.spring(mouse.X),
        y = Otter.spring(mouse.Y),
    })
end

updateMotor()
mouse.Move:Connect(updateMotor)
```

## License
This package uses the MIT License. You may find it by viewing the LICENSE file in the repository.
(I am not sure what license Otter actually uses)
