# Starship to improve Bash 

Starship's installation and configuration for Bash

![](header.png)

## Installation


```sh
sh -c "$(curl -fsSL https://starship.rs/install.sh)"

# ~/.bashrc

---
eval "$(starship init bash)"
export LC_ALL="en_US.UTF-8"
---

mkdir -p ~/.config && touch ~/.config/starship.toml


# Inserts a blank line between shell prompts
add_newline = true

# Replace the "❯" symbol in the prompt with "➜"
[character]                            # The name of the module we are configuring is "character"
success_symbol = "[➜](bold green)"     # The "success_symbol" segment is being set to "➜" with the color "bold green"

# Disable the package module, hiding it from the prompt completely
[package]
disabled = true
```

## Condifuration and Customization

```sh
sudo pacman -S noto-fonts-emoji

```

```sh
---> /etc/fonts/local.conf

<?xml version="1.0"?>
<!DOCTYPE fontconfig SYSTEM "fonts.dtd">
<fontconfig>
 <alias>
   <family>sans-serif</family>
   <prefer>
     <family>Noto Sans</family>
     <family>Noto Color Emoji</family>
     <family>Noto Emoji</family>
     <family>DejaVu Sans</family>
   </prefer> 
 </alias>

 <alias>
   <family>serif</family>
   <prefer>
     <family>Noto Serif</family>
     <family>Noto Color Emoji</family>
     <family>Noto Emoji</family>
     <family>DejaVu Serif</family>
   </prefer>
 </alias>

 <alias>
  <family>monospace</family>
  <prefer>
    <family>Noto Mono</family>
    <family>Noto Color Emoji</family>
    <family>Noto Emoji</family>
   </prefer>
 </alias>
</fontconfig>
```

```sh
git clone https://github.com/ryanoasis/nerd-fonts
cd nerd-fonts
sudo ./install.sh
```

## Meta

Simone Arena – [@the_lello](https://twitter.com/the_lello) – lellothegreat@protonmail.ch


