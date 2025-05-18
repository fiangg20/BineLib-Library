# BineLib Documentation

---

## **Overview**
**BineLib** is a Roblox Lua UI library designed to create customizable and interactive user interfaces. Developed by luauruler26, it offers features such as draggable/resizable windows, theme customization, blur effects, and a variety of pre-built components (buttons, sliders, dropdowns, etc.). The library supports both dark and light themes and includes dynamic animations.

---

## **Installation**
1. Include the library in your script:
   ```lua
   local Library = loadstring(game:HttpGet("https://glot.io/snippets/h76idkfka7/raw/tria.ts"))()
   ```

---

## **Core Components & Methods (source.lua)**

### **1. Window Initialization**
Create a main window to host UI elements:
```lua
local Window = Library:CreateWindow({
    Title = "Window Title",      -- Window title
    Theme = "Dark",              -- Theme mode ("Dark", "Light", or custom)
    Size = UDim2.fromOffset(500, 400), -- Window size
    Transparency = 0.2,          -- UI transparency (0-1)
    Blurring = true,             -- Enable/disable background blur
    MinimizeKeybind = Enum.KeyCode.LeftAlt, -- Keybind to toggle visibility
})
```

### **2. UI Components**
#### **Tabs and Sections**
- **Add Tab Sections**: Organize tabs into groups.
  ```lua
  Window:AddTabSection({
      Name = "Section Name", -- Section title
      Order = 1,             -- Layout order
  })
  ```
- **Add Tabs**: Create tabs within sections.
  ```lua
  local Tab = Window:AddTab({
      Title = "Tab Title",   -- Tab name
      Section = "Section Name", -- Parent section
      Icon = "rbxassetid://11963373994" -- Optional icon
  })
  ```

#### **Non-Interactable Elements**
- **Paragraph**: Display text.
  ```lua
  Window:AddParagraph({
      Title = "Header",           -- Title text
      Description = "Description",-- Body text
      Tab = Tab,                  -- Parent tab
  })
  ```

#### **Interactable Elements**
- **Button**: Execute a callback on click.
  ```lua
  Window:AddButton({
      Title = "Button",           -- Button label
      Description = "Description",-- Tooltip text
      Tab = Tab,                  -- Parent tab
      Callback = function()       -- Action on click
          print("Button clicked!")
      end,
  })
  ```
- **Slider**: Adjust numerical values.
  ```lua
  Window:AddSlider({
      Title = "Slider",           -- Slider label
      Description = "Adjust value", 
      Tab = Tab,
      MaxValue = 100,             -- Maximum value
      AllowDecimals = false,      -- Enable decimal inputs
      Callback = function(Value)  -- Returns current value
          print(Value)
      end,
  })
  ```
- **Toggle**: Switch between states.
  ```lua
  Window:AddToggle({
      Title = "Toggle",           -- Toggle label
      Description = "Enable/disable",
      Default = false,            -- Initial state
      Tab = Tab,
      Callback = function(State)  -- Returns boolean
          print(State)
      end,
  })
  ```

#### **Advanced Components**
- **Dropdown**: Select from a list of options.
  ```lua
  Window:AddDropdown({
      Title = "Dropdown",         -- Dropdown label
      Description = "Choose an option",
      Tab = Tab,
      Options = {                 -- Key-value pairs
          ["Option 1"] = "Value1",
          ["Option 2"] = "Value2",
      },
      Callback = function(SelectedValue)
          print(SelectedValue)
      end,
  })
  ```
- **Keybind**: Set custom keybinds.
  ```lua
  Window:AddKeybind({
      Title = "Keybind",           -- Keybind label
      Description = "Set a key",
      Tab = Tab,
      Callback = function(Key)     -- Returns Enum.KeyCode
          print(Key)
      end,
  })
  ```

---

## **Example Usage (example.lua)**

### **1. Theme Configuration**
Define and apply themes:
```lua
local Themes = {
    Dark = { ... }, -- Primary, Secondary, Text, etc.
    Light = { ... },
    Void = { ... },
}
Window:SetTheme(Themes.Dark) -- Apply a theme
```

### **2. Notification System**
Display temporary alerts:
```lua
Window:Notify({
    Title = "Notification",       -- Notification header
    Description = "Message text", -- Body text
    Duration = 5,                 -- Display time (seconds)
})
```

### **3. Settings Tab**
Configure UI behavior:
```lua
-- Keybind customization
Window:AddKeybind({
    Title = "Minimize Keybind",
    Description = "Set the toggle keybind",
    Tab = SettingsTab,
    Callback = function(Key)
        Window:SetSetting("Keybind", Key) -- Update keybind
    end,
})

-- Transparency adjustment
Window:AddSlider({
    Title = "UI Transparency",
    Description = "Adjust UI opacity",
    Tab = SettingsTab,
    MaxValue = 1,
    AllowDecimals = true,
    Callback = function(Value)
        Window:SetSetting("Transparency", Value)
    end,
})
```

---

## **Additional Features**
- **Drag & Resize**: Windows are draggable and resizable by default.
- **Blur Effect**: Enable with `Blurring = true` during window creation.
- **Dynamic Themes**: Modify colors using `Window:SetTheme(CustomThemeTable)`.

---

## **Notes**
- Ensure Roblox graphics settings are set to **Level 8 or higher** for blur effects.
- Use `Window:SetSetting("Size", UDim2.new(...))` to dynamically adjust window size.
