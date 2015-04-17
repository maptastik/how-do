# Remove artifact from right-click menu

Sometimes in Windows 7 - and apparently in all Windows OSes since 2000 - there's the possibility that after you've selected something from the right-click menu, the thing you selected will hang around as the top-most layer on the screen. How to fix this ([source](http://superuser.com/questions/57016/menu-select-item-stuck-on-screen-after-context-or-command-menu-has-closed)).

1. Go to the Start menu and search "Run".
2. Select the Run program
3. The Run program will open up. There's only the one field to type in. In that field type `tskill dwm`
4. Click "OK"

This should refresh the screen and get rid of the artifact.