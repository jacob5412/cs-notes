# Homebrew

* Homebrew is a free and open-source software package management system that simplifies the installation of software on Apple's macOS operating system and Linux.
* `brew` prefers pre-compiled binaries but will compile from source in some cases.


## Installation

1. Install Xcode Tools:		

    ```zsh
    xcode-select —install
    ```

2. Install Homebrew

    ```zsh
    ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"
    ```

## Cask

`brew cask` is an extension to `brew` that allows management of graphical applications through the Cask project.

1. Install Cask		

    ```zsh
    brew install cask
    ```

2. List apps:

    ```zsh	
    brew search --casks
    ```

3. Search apps:

    ```zsh
    brew search (discord)
    ```

4. Install:

    ```zsh
    brew cask install (discord)
    ```

5. Update:

    ```zsh
    brew cask upgrade
    ```

6. Help:

    ```zsh
    brew cask help
    ```

## Examples

### Htop

```
//Install htop:				brew install htop
Run:						sudo htop
```

### Speedtest

```zsh
//Install Speedtest			brew install speedtest-cli
Run:						speedtest-cli
```

### Youtube-DL

```zsh
//Install youtube-dl:		brew install youtube-dl
//Install ffmpeg:			brew install youtube-dl ffmpeg
Download highest-res vid:	youtube-dl -f bestvideo+bestaudio ‘link’
Help:						youtube-dl --help
```

### ImageMagick

```zsh
//Install ImageMagick:		brew install imagemagick
Add border (sample):		convert testing.png -border 1x1 -bordercolor black result.png
Resize (sample):			convert testing.png -resize 1920 (or x1080) example.png
Add effect (sample):		convert testing.png -charcoal 2 example.png
Change multiple (sample):	for file in *.png; do convert $file -resize 1920 small-$file; done
Help:						convert help
```

## References

1. [Snazzy Labs](https://youtu.be/Ym2pxzWpTNw)
2. [Cask vs Formula](https://apple.stackexchange.com/questions/125468/what-is-the-difference-between-brew-and-brew-cask)