# Nisttell

**Ni**ni + Gho**stt**y + Fuzz**el**

## Introduction

This is two simple python scripts that handle open ghostty windows using the capabilities of the Niri window manager to mimic the functionality of the tmux-sessionizer. This allows the user to create new sessions and hop between without tmux solving the rendering problems it introduces in ghostty.

## Installation

1. Install ghostty, niri, python, fuzzel or fzf from your package manager.
2. Clone the repository and cd into the repo folder.
3. Make the two scripts executable

```bash
chmod +x nisttell
chmod +x nisttell-switcher
```

4. In your ghostty config make sure that single instance is disabled
```ini
gtk-single-instance = false
```

5. On your niri configurations 'config.kdl'
    i. If you want to use fuzzel:
    ```kdl
        Mod+apostrophe { spawn "~/<NISTTELL_DIR>/nisttell";}
        Mod+semicolon { spawn "~/<NISTELL_DIR>/nisttell-switcher";}
    ```
    ii. If you want to use the fzf:
    ```kdl
        Mod+apostrophe { spawn-sh "ghostty --title=session.manager -e bash -c ~/<NISTTELL_DIR>/nisttell";}
        Mod+semicolon { spawn-sh "ghostty --title=session.switcher -e bash -c ~/<NISTELL_DIR>/nisttell-switcher";}
    ```
        - You can also make this floating by setting a window rule for the windows that have title with "session."

        ```kdl
        window-rule {
            match title="^session\\."
            open-floating true
        }
        ```

## How this works

This used the tab column displays capabilites of the niri window manager.
1. You select a project from your folder.
2. A new ghostty window is spawned in the working directory you selected and with a title `ghostty.project_name` that will be used to swtich between the windows.
3. Niri will activate tab mode in the ghostty column if not already activated.
4. The new ghostty window that has spawned will be consumed into the column.
5. Niri will focus the new ghostty window.
