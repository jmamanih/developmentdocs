# Install Sublime Text
## Version 3, Buil 3126
## On OS X

## Activate Licence
1. Install Program & Exit from it
2. Run Porgram & Click Help->Enter license
3. Copy/Paste Serial & click activate
4. That's It ! Enjoy

Licence:

```
óñ BEGIN LICENSE óñ
Wixel
Single User License
EA7E-848235
103D2969 8700C7ED 8173CF61 537000C0
EB3C7ECB 5E750F17 6B42B67C A190090B
7669164F C6F371A8 5A1D88D5 BDD0DA70
C065892B 7CC1BB2B 1C8B8C7C F08E7789
7C2A5241 35F86328 4C8F70D9 C023D7C2
11245C36 59A730DB 72BDB9A7 D5B20304
90E90E72 9F08CA25 73F49C20 179D938E
5BC8BEDA 13457A69 39E6265F 233767F9
óó END LICENSE óó

```

## Enable Menu Options
### View Side Bar

    Menu View, Side Bar, Show Open Files

### Add Folder to Project

    Menu Project, Add Folder to Project, Select Folder

## Install Package Control
goto URL: https://packagecontrol.io/installation

copy text

```
import urllib.request,os,hashlib; h = 'df21e130d211cfc94d9b0905775a7c0f' + '1e3d39e33b79698005270310898eea76'; pf = 'Package Control.sublime-package'; ipp = sublime.installed_packages_path(); urllib.request.install_opener( urllib.request.build_opener( urllib.request.ProxyHandler()) ); by = urllib.request.urlopen( 'http://packagecontrol.io/' + pf.replace(' ', '%20')).read(); dh = hashlib.sha256(by).hexdigest(); print('Error validating download (got %s instead of %s), please try manual install' % (dh, h)) if dh != h else open(os.path.join( ipp, pf), 'wb' ).write(by)
```
    Menu –> View -> Show console -> paste text

    Verify press to Cmd + Shift + p

## Install Packages

    Cmd+Shift+p -> Type "Install Package", Enter -> type "package name to install"

## Remove Packages

    Cmd+Shift+P -> Type "Remove Package", Enter -> type "package name to remove"

## Packages for Sublime Text

### A File Icon
    
    Press cmd + shift + p, Type "Install package", "A File Icon"

### Auto Filename

    Install Package, Auto Filename

### Seti UI (Improve Interface)

Install Package, Seti-UI
Copy text

```js
{
  "theme": "Seti.sublime-theme",

  "caret_extra_width": 2,                 //  to have a wider/thicker caret
  "caret_extra_bottom": 3,                //  to make the caret = to the line height (the theme currently support 0,3,5)
  "caret_extra_top": 3,

  "overlay_scroll_bars": "enabled",       //  to show scrollbars only when scrolling
  "highlight_line": true,                 //  to highlight the current line
}
```

    Sublime-Text Menu, Preferences, Settings, In to file preferences.sublime-setting--User, Reapply the settings by pasting the text

### One Dark Scheme Theme

    Press cmd + shift + p, Type "Install package", "One Dark Color Scheme"
    Sublime-Text Menu, Preferences, Color Scheme, One Dark Color Scheme, One Dark select (Atom theme default)

### Matherial Theme

[Source URL Material Theme](https://github.com/equinusocio/material-theme)

    Press cmd + shift + p to open the command palette.
    Type "install package" and press enter. Then search for "Material Theme"

    You can also manually activate this theme by adding these lines to your user settings (Preferences > Settings - User):

#### Active Theme Material

    Press cmd + shift + p, Type "Active Theme", Select "Material-Theme-Darker"

    You can also manually activate this theme by adding these lines to your user settings (Preferences > Settings - User):

```sh 
"color_scheme": "Packages/Material Theme/schemes/Material-Theme.tmTheme",
"theme": "Material-Theme.sublime-theme",
```

#### Configuration

Recommended settings
Menu Sublime-Text, Preferences > Settings, Edit the 'Preferences.sublime-setting--User' file adding the following lines

```sh
"always_show_minimap_viewport" : true,
"bold_folder_labels"           : true,
"font_options"                 : [ "gray_antialias", "subpixel_antialias" ],    // On retina Mac & Windows
"indent_guide_options"         : [ "draw_normal", "draw_active" ],   // Highlight active indent
"line_padding_bottom"          : 3,
"line_padding_top"             : 3,
"overlay_scroll_bars"          : "enabled",

```

### Markdown HighLighting

Press cmd + shift + p, Type "MarkdownHighlighting", close all file markdown format, open file to view effects

### Haroopad as publisher and markdown viewer
    Install Haroopad Markdown
    Select “Package Control: Install Package” from the Command Palette (super+shift+p)
    Find “Haroopad Markdown” and select
    Select Menu, Tool, Open width Haroopad

### Emmet (Automatic creation of html tags)  

Installation and Use

    Press cmd + shift + p to open the command palette.
    Type "install package" and press enter, then search for "Emmet".
    Test, example write ! Crtl+E

### JavascripNext - ES6 Systax

Installation and Use
    
    Press cmd + shift + p to open the command palette, Type "install package" and press enter, then search for "JavascriptNext"

    To set this as your default JavaScript syntax, open a javascript file, then select View -> Syntax -> Open all with current extension as... -> JavaScriptNext-ES6 Syntax -> JavaScript Next.
    

### Sublime Terminal
Shortcuts and menu entries for opening a terminal at the current file, or the current root project folder in **Sublime Text**.

Installation

    Press cmd + shift + p to open the command palette.
    Type "install package" and press enter, then search for "Terminal"

Usage

    Open Terminal at File Press cmd+shift+t
    Open Terminal at Project Folder Press cmd+alt+shift+t on OS X

Package Settings

The default settings can be viewed by accessing the *Preferences > Package Settings > Terminal > Settings – Default* 

Edit file to iTerm2 terminal OS X:

```js
{
  "terminal": "iTerm2-v3.sh",
  "parameters": ["--open-in-tab"]
}
```

### Sidebar Enhancements

Installation and Use
    
    Press cmd + shift + p to open the command palette, Type "install package" and press enter, then search for "Sidebar Enhancements".
    Right click on a file in the menu panel
    
### Find Selected

Installation 
    
    Press cmd + shift + p to open the command palette, Type "install package" and press enter, then search for "FindSelected".
Usage
    
    f3 - find_selected_next - If selected find next occurrence, if not then find last search term. 
    shift+f3 - find_selected_previous - If selected find prev occurence, if not then find previous last search term. ctrl+f3 - find_selected_next - If selected find next occurrence, if not then find clipboard. 
    ctrl+shift+f3 - find_selected_previous

Configuration

    Right click on a file in the menu panel

### Set syntax view

Cmd+Shift+P, type: set syntax: MultiMarkdown, Intro

### Install TypeScript syntax
Cmd+Shift+P, Install Package, TypeSript Select,
Open file.ts, Cmd+Shift+P, Set syntax: TypeScript, Intro
