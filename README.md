### DroppingLib
A lightweight GUI library for Roblox with a modern design, animations, and customizable components.  

---

#### **Features**  
- Title bar with dynamic dropdown toggle  
- Smooth animations (rotation and dropdown expansion)  
- Prebuilt components: **Button**, **Toggle**, **Dropdown Menu**  
- Extensible architecture for adding custom components  

---

#### **Installation**  
1. Create a `ModuleScript` in Roblox Studio.  
2. Paste the loader into the module.  
3. Require the module in your script:  
   ```lua
   local Library = loadstring(game:HttpGet("https://raw.githubusercontent.com/fiangg20/droppinglib/refs/head/main/source"))()
   ```

---

### **API Reference**  

#### `Library.Create() -> GUI`  
Initializes the GUI window. 

### **`SetTitle(text: string)`**  
Updates the title bar text.  

**Parameters:**  
- `text` (string): New title text  

**Example:**  
```lua
MyGUI.SetTitle("New Title")
```

**Returns:**  
- A table with:  
  - `ScreenGui`: The root GUI object (parent this to `PlayerGui`).  
  - Methods: `CreateButton`, `CreateToggle`, `AddDropdownItem`.  

**Example:**  
```lua
local MyGUI = Library.Create()
MyGUI.ScreenGui.Parent = game.Players.LocalPlayer:WaitForChild("PlayerGui")
```

---

#### **`CreateButton(props: table) -> TextButton`**  
Adds a button to the title bar.  

**Parameters:**  
- `props` (table):  
  - `Text` (string): Button label.  
  - `Callback` (function): Fires when clicked.  

**Example:**  
```lua
MyGUI.CreateButton({
    Text = "Click Me",
    Callback = function()
        print("Button clicked!")
    end
})
```

---

#### **`CreateToggle(props: table) -> TextButton`**  
Adds a toggle switch to the title bar.  

**Parameters:**  
- `props` (table):  
  - `Text` (string): Toggle label.  
  - `Callback` (function): Fires on toggle (returns `state: boolean`).  

**Example:**  
```lua
MyGUI.CreateToggle({
    Text = "Enable",
    Callback = function(state)
        print("Toggle state:", state)
    end
})
```

---

#### **`AddDropdownItem(item: table)`**  
Adds an item to the dropdown menu.  

**Parameters:**  
- `item` (table):  
  - `Text` (string): Item label.  
  - `Callback` (function): Fires when the item is clicked.  

**Example:**  
```lua
MyGUI.AddDropdownItem({
    Text = "Option 1",
    Callback = function()
        print("Option 1 selected!")
    end
})
```

---

### **Dropdown Behavior**  
- Click the **`^`** button on the title bar to toggle the dropdown.  
- The caret rotates `180°` when opened.  
- Dropdown height animates smoothly between `0` and `200` pixels.  

---

### **Customization Tips**  
1. **Colors**: Modify `BackgroundColor3` properties in the code.  
2. **Positioning**: Adjust `MainWindow.Position` or use `AnchorPoint`.  
3. **Dropdown Size**: Change the `200` in `UDim2.new(1, 0, 0, 200)` (line 59).  

---

### **Full Example**  
```lua
local Library = require(path.to.module)

local GUI = Library.Create()
GUI.ScreenGui.Parent = game.Players.LocalPlayer.PlayerGui

-- Add a button
GUI.CreateButton({
    Text = "Hello",
    Callback = function()
        print("Hello world!")
    end
})

-- Add a toggle
GUI.CreateToggle({
    Text = "Lights",
    Callback = function(state)
        print("Lights:", state and "ON" or "OFF")
    end
})

-- Add dropdown items
GUI.AddDropdownItem({ Text = "Option 1", Callback = function() print("1") end })
GUI.AddDropdownItem({ Text = "Option 2", Callback = function() print("2") end })
```

---

### **Notes**  
- Uses Roblox’s `TweenService` for animations.  
- Extend the library by adding methods like `CreateSlider` or `CreateInput` (follow the pattern in `CreateButton`).  
