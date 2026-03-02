# WinApiGdi32

`WinApiGdi32` is a C# .NET Framework (4.8) class library providing a comprehensive set of P/Invoke wrappers for native Windows API functions, primarily focusing on `gdi32.dll` and `user32.dll`.

This library simplifies working with native Windows contexts such as GDI graphics, simulating input, managing windows, and accessing system parameters, directly from your managed C# applications.

## Features

- **GDI Graphics (`gdi32.dll`)**: Create Device Contexts (DCs), draw shapes (Lines, Rectangles, Ellipses, Pies), perform region filling, manage Bitmaps / DIBs, and execute complex Blitting operations such as `BitBlt`, `StretchBlt`, `PlgBlt`, and `PatBlt`.
- **Input Simulation (`user32.dll`)**: Send keyboard and mouse inputs programmatically using `SendInput`, `GetCursorPos`, `SetCursorPos`, and `mouse_event`. Includes definitions for complete virtual key codes and input types constraints.
- **Window Management (`user32.dll`)**: Easily interact with the Windows desktop using `FindWindow`, `FindWindowEx`, `SendMessage`, `GetWindow`, and `MoveWindow`.
- **System Settings**: Retrieve or apply system preferences, such as setting the desktop wallpaper using `SystemParametersInfo` flag `SPI_SETDESKWALLPAPER`.
- **Structures & Enums defined**: Pre-configured Win32 structures such as `RECT`, `POINT`, `BITMAPINFO`, `RGBQUAD`, `INPUT`, `KEYBDINPUT`, and Enums matching Raster operations (`Rop`, `TernaryRasterOperations`) and event flags.

## Usage

Include the library in your project by referencing the compiled `.dll` or adding the project directly to your solution.

All native interactions are implemented as static methods inside the `WinApiGdi32.WinGdi32` class.

### Example: Finding a Window & Getting its Device Context

```csharp
using WinApiGdi32;
using System;

IntPtr hWnd = WinGdi32.FindWindow(null, "Untitled - Notepad");
if (hWnd != IntPtr.Zero)
{
    // Retrieve the Device Context for the window
    IntPtr hdc = WinGdi32.GetWindowDC(hWnd);
    
    // Draw a rectangle
    WinGdi32.Rectangle(hdc, 10, 10, 100, 100);
    
    // Always remember to release the DC when finished
    WinGdi32.ReleaseDC(hWnd, hdc);
}
```

### Example: Simulating a Mouse Click

```csharp
using WinApiGdi32;

// Set cursor to a specific screen location
WinGdi32.SetCursorPos(500, 500);

// Simulate a left mouse down and mouse up
WinGdi32.mouse_event((uint)WinGdi32.MouseEventFlags.LEFTDOWN, 0, 0, 0, UIntPtr.Zero);
WinGdi32.mouse_event((uint)WinGdi32.MouseEventFlags.LEFTUP, 0, 0, 0, UIntPtr.Zero);
```

## Requirements

- **.NET Framework**: v4.8
- **OS**: Windows (Relies on native Win32 APIs like `gdi32.dll` and `user32.dll`)

## License

This project is open-source and free to be used and modified according to your own needs.
