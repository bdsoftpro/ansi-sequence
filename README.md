```The operating system may transform some keystrokes into unicode strings, such as for an input method editor or other configured shortcuts. In these instances, it is acceptable to deviate from these specifications.

Normally, these send these codes for these keystrokes. Note that no distinction is made between enter on the numeric keypad and the "regular" enter key. Other keystrokes not listed here should follow the rules at http://www.leonerd.org.uk/hacks/fixterms/. Meta is used here to refer to a platform-defined modifier key, such as Alt or Option.

Keystrokes encoding a Unicode character where neither Control nor Meta is pressed simply send the unicode character. If Meta is used to access the input method editor, Meta should be ignored.

There are various special cases for certain keys. This table gives the expected behavior for a conforming client, which supercedes the preceding rules:

Modifier               a         h          i          m          space       backspace       tab       enter      up        esc
-----------------------------------------------------------------------------------------------------------------------------------------------
None                   a         h          i          m          0x20        0x7f            0x9       0xd        CSI A     0x1b                                                            
Shift                  A         H          I          M          CSI 32;2u   CSI 127;2u      CSI Z     CSI 13;2u  CSI 1;2A  CSI 27;2u                                                        
Control                0x1       0x8        CSI 105;5u CSI 109;5u 0x0         CSI 127;5u      CSI 9;5u  CSI 13;5u  CSI 1;5A  CSI 27;5u                                                                            
Control+Shift          CSI 65;5u CSI 74;5u  CSI 73;5u  CSI 77;5u  CSI 32;6u   CSI 127;6u      CSI 1;6Z  CSI 13;6u  CSI 1;6A  CSI 27;6u                                                                                 
Meta                   0x1b a    0x1b h     0x1b i     0x1b m     0x1b 0x20   ???             0x1b 0x9  0x1b 0xd   CSI 1;3A  0x1b 0x1b  (WTF)                                                                           
Meta+Shift             0x1b A    0x1B H     0x1b I     0x1b M     CSI 32;4u   CSI 127;4u      CSI 1;4Z  CSI 13;4u  CSI 1;4A  CSI 27;4u                                                                                 
Meta+Control           0x1b 0x1  0x1b 0x8   CSI 105;7u CSI 109;7u 0x1b 0x0    CSI 3;7~        CSI 9;7u  CSI 13;7u  CSI 1;7A  CSI 27;7u                                                                                   
Meta+Control+Shift     CSI 65;7u CSI 72;7u  CSI 73;7u  CSI 77;7u  CSI 32;8u   CSI 127;8u      CSI 1;8Z  CSI 13;8u  CSI 1;8A  CSI 27;8u


Special keys like function keys and navigation keys use their own CSI codes. The codes will include a modifier, built using this table:

Shift   1
Meta    2
Ctrl    4

Add 1 to the bitmask of modifiers above to get the CSI `[modifier]` paraemter. For example, Meta+Shift would have a modifier of 4. The `[modifier]` parameter may be omitted from sequences below if it would be 1. When multiple forms are specified, any is valid.
These special keys use codes as follows:

Key          Form 1               Form 2
--------------------------------------------------
Insert       CSI 2;[modifier] ~ 
Delete       CSI 3;[modifier] ~ 
Page Up      CSI 5;[modifier] ~ 
Page Down    CSI 6;[modifier] ~ 
Home         CSI 7;[modifier] ~   CSI [modifeir];H
End          CSI 8;[modifier] ~   CSI [modifeir];F
F1           CSI 11;[modifier] ~  CSI [modifier];P
F2           CSI 12;[modifier] ~  CSI [modifier];Q
F3           CSI 13;[modifier] ~  CSI [modifier];R
F4           CSI 14;[modifier] ~  CSI [modifier];S
F5           CSI 15;[modifier] ~
F6           CSI 17;[modifier] ~
F7           CSI 18;[modifier] ~
F8           CSI 19;[modifier] ~
F9           CSI 20;[modifier] ~
F10          CSI 21;[modifier] ~
F11          CSI 23;[modifier] ~
F12          CSI 24;[modifier] ~
Up           CSI 1;[modifier] A
Down         CSI 1;[modifier] B
Right        CSI 1;[modifier] C
Left         CSI 1;[modifier] D

In application cursor mode (DECCKM), use these codes instead when no modifier is pressed:

Up           ESC O A
Down         ESC O B
Right        ESC O C
Left         ESC O D
Home         ESC O H
End          ESC O F

In application keypad mode (DECNKM), use these codes for keys on the numeric keypad:

Keypad Enter      ESC O M   CSI 1;[modifier] M 
Keypad Multiply   ESC O j   CSI 1;[modifier] j 
Keypad Plus       ESC O k   CSI 1;[modifier] k 
Keypad Minus      ESC O m   CSI 1;[modifier] m 
Keypad Decimal    ESC O n   CSI 1;[modifier] n 
Keypad Divide     ESC O o   CSI 1;[modifier] o 
Keypad 0          ESC O p   CSI 1;[modifier] p 
Keypad 1          ESC O q   CSI 1;[modifier] q 
Keypad 2          ESC O r   CSI 1;[modifier] r 
Keypad 3          ESC O s   CSI 1;[modifier] s 
Keypad 4          ESC O t   CSI 1;[modifier] t 
Keypad 5          ESC O u   CSI 1;[modifier] u 
Keypad 6          ESC O v   CSI 1;[modifier] v 
Keypad 7          ESC O w   CSI 1;[modifier] w 
Keypad 8          ESC O x   CSI 1;[modifier] x 
Keypad 9          ESC O y   CSI 1;[modifier] y 
Keypad Equals     ESC O X   CSI 1;[modifier] X 

When not in application keypad mode, these keys behave like their non-keypad equivalents.

Optionally, applications may choose to send these codes for certain control+key combos when Meta is not pressed:

Key     Code
------------
2       0x0
\       0x1c
]       0x1d
6       0x1e
_       0x1f
?       0x7f
```
