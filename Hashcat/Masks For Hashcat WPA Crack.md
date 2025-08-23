[wiki / mask attack - hashcat.net](https://hashcat.net/wiki/doku.php?id=mask_attack)

## Charsets
### Built-in charsets
```
?l = abcdefghijklmnopqrstuvwxyz
?u = ABCDEFGHIJKLMNOPQRSTUVWXYZ
?d = 0123456789
?h = 0123456789abcdef
?H = 0123456789ABCDEF
?s = «space»!"#$%&'()*+,-./:;<=>?@[\]^_`{|}~
?a = ?l?u?d?s
?b = 0x00 - 0xff
```
### Custom charsets
All hashcat versions have four commandline-parameters to configure four custom charsets.
```
--custom-charset1=CS
--custom-charset2=CS
--custom-charset3=CS
--custom-charset4=CS
```
These commandline-parameters have four analogue shortcuts called -1, -2, -3 and -4. You can specify the chars directly on the command line or use a so-called hashcat charset file (plain text file with .hcchr extension which contains the chars/digits to be used on the 1st line of the file). See examples below:

#### Examples
The following commands all define the same custom charset that consists of the chars “abcdefghijklmnopqrstuvwxyz0123456789” (aka “lalpha-numeric”):
```
-1 abcdefghijklmnopqrstuvwxyz0123456789
-1 abcdefghijklmnopqrstuvwxyz?d
-1 ?l0123456789
-1 ?l?d
-1 loweralpha_numeric.hcchr # file that contains all digits + chars (abcdefghijklmnopqrstuvwxyz0123456789)
```

