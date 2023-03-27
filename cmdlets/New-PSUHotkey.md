---
external help file: Universal.Cmdlets.dll-Help.xml
Module Name: Universal
online version: https://go.microsoft.com/fwlink/?LinkID=217032
schema: 2.0.0
---

# New-PSUHotkey

## SYNOPSIS
Creates a desktop hotkey to invoke a script.

## SYNTAX

```
New-PSUHotkey [-Script] <Script> [-Credential <Variable>] [-Environment <String>]
 [-ModifierKeys <ModifierKeys>] -Keys <Keys> [-ComputerName <String>] [-AppToken <String>]
 [-UseDefaultCredentials] [-Integrated] [<CommonParameters>]
```

## DESCRIPTION
Creates a desktop hotkey to invoke a script. This cmdlet is only supported in Desktop Mode.

## EXAMPLES

### Example 1
```powershell
PS C:\> New-PSUHotkey -Script 'MyScript1.ps1' -Keys 'I' -ModifierKeys 'Ctrl'
```

Creates a Ctrl+I hotkey that will invoke the MyScript1.ps1 script. 

## PARAMETERS

### -AppToken
Not Supported

```yaml
Type: String
Parameter Sets: (All)
Aliases:

Required: False
Position: Named
Default value: None
Accept pipeline input: False
Accept wildcard characters: False
```

### -ComputerName
Not Supported

```yaml
Type: String
Parameter Sets: (All)
Aliases: Uri

Required: False
Position: Named
Default value: None
Accept pipeline input: False
Accept wildcard characters: False
```

### -Credential
The credential variable to use when running the script. 

```yaml
Type: Variable
Parameter Sets: (All)
Aliases:

Required: False
Position: Named
Default value: None
Accept pipeline input: False
Accept wildcard characters: False
```

### -Environment
The environment to use when running the script. 

```yaml
Type: String
Parameter Sets: (All)
Aliases:

Required: False
Position: Named
Default value: None
Accept pipeline input: False
Accept wildcard characters: False
```

### -Integrated
Not Supported

```yaml
Type: SwitchParameter
Parameter Sets: (All)
Aliases:

Required: False
Position: Named
Default value: None
Accept pipeline input: False
Accept wildcard characters: False
```

### -Keys
The key to use for the hotkey. 

```yaml
Type: Keys
Parameter Sets: (All)
Aliases:
Accepted values: None, LButton, RButton, Cancel, MButton, XButton1, XButton2, Back, Tab, LineFeed, Clear, Enter, Return, ShiftKey, ControlKey, Menu, Pause, CapsLock, Capital, HangulMode, HanguelMode, KanaMode, JunjaMode, FinalMode, KanjiMode, HanjaMode, Escape, IMEConvert, IMENonconvert, IMEAccept, IMEAceept, IMEModeChange, Space, Prior, PageUp, PageDown, Next, End, Home, Left, Up, Right, Down, Select, Print, Execute, Snapshot, PrintScreen, Insert, Delete, Help, D0, D1, D2, D3, D4, D5, D6, D7, D8, D9, A, B, C, D, E, F, G, H, I, J, K, L, M, N, O, P, Q, R, S, T, U, V, W, X, Y, Z, LWin, RWin, Apps, Sleep, NumPad0, NumPad1, NumPad2, NumPad3, NumPad4, NumPad5, NumPad6, NumPad7, NumPad8, NumPad9, Multiply, Add, Separator, Subtract, Decimal, Divide, F1, F2, F3, F4, F5, F6, F7, F8, F9, F10, F11, F12, F13, F14, F15, F16, F17, F18, F19, F20, F21, F22, F23, F24, NumLock, Scroll, LShiftKey, RShiftKey, LControlKey, RControlKey, LMenu, RMenu, BrowserBack, BrowserForward, BrowserRefresh, BrowserStop, BrowserSearch, BrowserFavorites, BrowserHome, VolumeMute, VolumeDown, VolumeUp, MediaNextTrack, MediaPreviousTrack, MediaStop, MediaPlayPause, LaunchMail, SelectMedia, LaunchApplication1, LaunchApplication2, Oem1, OemSemicolon, Oemplus, Oemcomma, OemMinus, OemPeriod, OemQuestion, Oem2, Oem3, Oemtilde, OemOpenBrackets, Oem4, Oem5, OemPipe, Oem6, OemCloseBrackets, Oem7, OemQuotes, Oem8, OemBackslash, Oem102, ProcessKey, Packet, Attn, Crsel, Exsel, EraseEof, Play, Zoom, NoName, Pa1, OemClear, KeyCode, Shift, Control, Alt, Modifiers

Required: True
Position: Named
Default value: None
Accept pipeline input: False
Accept wildcard characters: False
```

### -ModifierKeys
The modifier keys to use for the hotkey.

```yaml
Type: ModifierKeys
Parameter Sets: (All)
Aliases:
Accepted values: None, Alt, Ctrl, Shift, Win

Required: False
Position: Named
Default value: None
Accept pipeline input: False
Accept wildcard characters: False
```

### -Script
The script to invoke. 

```yaml
Type: Script
Parameter Sets: (All)
Aliases:

Required: True
Position: 1
Default value: None
Accept pipeline input: True (ByValue)
Accept wildcard characters: False
```

### -UseDefaultCredentials
Not supported

```yaml
Type: SwitchParameter
Parameter Sets: (All)
Aliases:

Required: False
Position: Named
Default value: None
Accept pipeline input: False
Accept wildcard characters: False
```

### CommonParameters
This cmdlet supports the common parameters: -Debug, -ErrorAction, -ErrorVariable, -InformationAction, -InformationVariable, -OutVariable, -OutBuffer, -PipelineVariable, -Verbose, -WarningAction, and -WarningVariable. For more information, see [about_CommonParameters](http://go.microsoft.com/fwlink/?LinkID=113216).

## INPUTS

### PowerShellUniversal.Script

## OUTPUTS

### System.Object
## NOTES

## RELATED LINKS
