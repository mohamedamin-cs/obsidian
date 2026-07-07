

# 🟦 **What Is Lua?**

Lua is a lightweight, fast, and easy-to-learn scripting language commonly used in:

- game development (Roblox, WoW addons, CryEngine, etc.)
    
- embedded systems
    
- extending applications
    

It has simple syntax and is great for beginners.

---

# 🟢 **1. Printing to the Screen**

```lua
print("Hello, world!")
```

---

# 🟢 **2. Variables**

Lua is dynamically typed (no need to declare a type).

```lua
name = "Alice"
age = 20
pi = 3.14
```

### Nil

`nil` means “no value”.

```lua
x = nil  -- removes the variable
```

---

# 🟢 **3. Comments**

```lua
-- This is a single-line comment

--[[
This is a
multi-line comment
]]
```

---

# 🟢 **4. Basic Data Types**

Lua has:

- **nil**
    
- **boolean** (`true`, `false`)
    
- **number** (float/double)
    
- **string**
    
- **table** (the most important type!)
    
- **function**
    

---

# 🟢 **5. Strings**

```lua
greet = "Hello"
print(greet .. " world")  -- .. concatenates strings
```

---

# 🟢 **6. Arithmetic**

```lua
a = 10
b = 3
print(a + b)
print(a - b)
print(a * b)
print(a / b)
print(a % b)
```

---

# 🟢 **7. Conditionals**

```lua
x = 5

if x > 10 then
    print("Greater")
elseif x == 10 then
    print("Equal")
else
    print("Less")
end
```

---

# 🟢 **8. Loops**

### While loop

```lua
i = 1
while i <= 5 do
    print(i)
    i = i + 1
end
```

### For loop

```lua
for i = 1, 5 do
    print(i)
end
```

Reverse:

```lua
for i = 5, 1, -1 do
    print(i)
end
```

---

# 🟢 **9. Tables (Lua’s main data structure!)**

Tables can act as:

- **arrays**
    
- **dictionaries**
    
- **objects**
    

### Array-like table

```lua
fruits = {"apple", "banana", "pear"}

print(fruits[1]) -- apple  (Lua arrays start at 1)
```

### Dictionary-like table

```lua
player = {
    name = "Alex",
    score = 100
}

print(player["name"])
print(player.score)   -- same as above
```

---

# 🟢 **10. Functions**

```lua
function add(a, b)
    return a + b
end

print(add(3, 4))
```

Anonymous function:

```lua
hello = function()
    print("Hi!")
end
```

---

# 🟢 **11. Metatables** (advanced but core to Lua)

Lua uses **metatables** to simulate classes, operator overloading, inheritance, etc.  
Simplified example:

```lua
mt = {
    __add = function(a, b)
        return a.value + b.value
    end
}

A = {value = 10}
B = {value = 20}

setmetatable(A, mt)
setmetatable(B, mt)

print(A + B) -- 30
```

---

# 🟢 **12. Modules**

Lua 5.1 style:

```lua
local module = {}

function module.hello()
    print("Hello from module!")
end

return module
```
