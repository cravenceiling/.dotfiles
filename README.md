# .dotfiles

My personal configuration files, managed with [GNU Stow](https://www.gnu.org/software/stow/).

Everything tracked lives under `home/`, mirroring the layout of `$HOME`.
Running `./dot stow` symlinks those files into place, so editing
`~/.config/nvim/init.lua` is the same as editing
`~/.dotfiles/home/.config/nvim/init.lua`.

## Layout

```
.dotfiles/
├── dot                 # tiny CLI wrapper around stow
└── home/               # symlinked into ~ (the "stow package")
    └── .config/
        ├── nvim/       # Neovim config
        └── ghostty/    # Ghostty terminal config
```

## Install on a new machine

```sh
# 1. Install prerequisites
sudo pacman -S stow            # or: brew install stow

# 2. Clone
git clone git@github.com:<you>/.dotfiles.git ~/.dotfiles
cd ~/.dotfiles

# 3. Symlink everything into place
./dot stow
```

If a config already exists as a *real* file/dir (e.g. you already have
`~/.config/nvim`), Stow will refuse to overwrite it. Either move the old one
aside, or absorb it into the repo:

```sh
./dot adopt        # moves existing files into home/ and replaces them with symlinks
git diff           # review what was absorbed before committing
```

## Day-to-day

Edit files anywhere they appear in `~` — they're symlinks back to this repo —
then commit and push from `~/.dotfiles`. New configs go under `home/`,
followed by `./dot stow` to link them.
