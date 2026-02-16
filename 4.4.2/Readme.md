# 🛠 Compile old D2 tools with Visual Studio 2010 Express

`allegro-4.4.2-msvc-10.0.7z`  Extract it somewhere safe (e.g. `C:\Libraries\allegro-4.4.2`).

----------

# 2️⃣ Create the Project in Visual Studio

----------
## 🆕 Create New Project

1.  Open **Microsoft Visual C++ 2010 Express**
2.  Click **New Project**
3.  Select:
    -   Win32        
    -   Win32 Console Application
4.  Click **OK**

## 🧙 Win32 Application Wizard
1.  Click **Next**    
2.  Under **Additional Options**, check:   
`☑ Empty Project` 
3.  Click **Finish**
    
You should now see:
Solution Explorer
 ├── Header Files
 └── Source Files

----------

# 3️⃣ Add win_ds1edit Source Files
1.  Open the extracted win_ds1edit source folder
2.  Drag all `.h` files into:  `Header Files` 
3.  Drag all `.c` files into:   `Source Files` 
4. Repeat for all files inside the `mpq` subdirectory

----------

# 4️⃣ Link the Allegro Library

⚠️ Important: Click on the **Project Name** (not the Solution!) before opening properties.
Go to: `Project → Properties` 
All following steps happen under: `Configuration  Properties` 

## 🧩 Step 1 — Add Include Directory
`C/C++ → General → Additional  Include  Directories` 
Add: `<PathToAllegro>\include\` 
Example: `C:\Libraries\allegro-4.4.2\include\` 

## 📚 Step 2 — Add Library Directory
`Linker → General → Additional  Library  Directories` 
Add: `<PathToAllegro>\lib\` 

## 🔗 Step 3 — Add Library File
`Linker → Input → Additional Dependencies` 
Add: `allegro-4.4.2-monolith-md.lib` 
Click OK.

----------

# 5️⃣ Build the Project

Go to: `Build → Build Solution` 
If everything is correct, you should see:
`========== Rebuild All: 1 succeeded, 0 failed, 0 skipped ==========` 
Your executable will be located in: `<ProjectFolder>\Debug\` 

----------

# 📦 ADDITIONAL - Adding an External Static Library (General Guide)
This section explains how to add **any external `.lib` + `.h` library** to a Visual C++ 2010 Express project.
This expands the Allegro example and applies to any static library.

----------

## ❓ Why “Add Reference” Doesn’t Work
The **References tab** only works for projects inside the same solution. External libraries must be added manually.

----------

## ✅ Correct Way to Add a Static Library

### 1️⃣ Open Project Properties
Right-click your project → **Properties**

### 2️⃣ Add Header Path
`Configuration  Properties → C/C++ → General → Additional  Include  Directories` 
Add the folder containing your `.h` file.
Example: `C:\Libraries\MyLib\include\` 

### 3️⃣ Add Library Path
`Configuration  Properties → Linker → General → Additional  Library  Directories` 
Add the folder containing your `.lib` file.
Example: `C:\Libraries\MyLib\lib\` 

### 4️⃣ Add the .lib File Name
`Configuration  Properties → Linker → Input → Additional  Dependencies` 
Add: `MyLibrary.lib` 

----------

## 💡 Alternative Method
You can also add the library manually via: `Linker → Command Line` 
And append: `MyLibrary.lib` 
But using **Additional Dependencies** is cleaner.

----------

## 🧠 Using the Library in Code
After configuration, simply include the header: `#include  "MyLibrary.h"` 
You can now call its functions normally.

----------

# 🧩 Troubleshooting
### ❌ Unresolved External Symbol
Most common causes:
-   `.lib` not added under Additional Dependencies
-   Wrong architecture (x86 vs x64 mismatch)
-   Library compiled with different runtime (/MD vs /MT)

----------

### ❌ Cannot Open Include File
Check:
-   Include directory path is correct
-   Header file exists
-   Path matches configuration (Debug/Release)

----------

# 🏆 Credits
-   **Paul Siramy** — Author of win_ds1edit
-   **Tom Amigo** — MPQ sample console app code

----------

# 📎 Notes
-   VC++ 2010 works on Windows 10
-   Web installer often fails — use ISO
-   No additional service packs required
-   Modern Visual Studio versions may not compile this project easily
