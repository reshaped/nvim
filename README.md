# nvim

A single-file Neovim configuration for C, C++, Go, Python and Rust, based heavily on [kickstart.nvim](https://github.com/nvim-lua/kickstart.nvim).

It needs Neovim 0.12 or later, tree-sitter-cli 0.26.1 or later, and a C compiler.

## Install

Clone it to Neovim's config directory:

```sh
git clone https://github.com/reshaped/nvim ~/.config/nvim
```

On macOS:

```sh
brew install neovim tree-sitter-cli ripgrep go node rust
```

On Ubuntu 26.04, apt's Neovim (0.11.6) and tree-sitter-cli (0.25.9) are too old. Install Neovim from the [official release](https://github.com/neovim/neovim/releases/latest), and keep `~/.local/bin` ahead of `/usr/bin` in `PATH`:

```sh
v=v0.12.6
curl -fLO https://github.com/neovim/neovim/releases/download/$v/nvim-linux-x86_64.tar.gz
mkdir -p ~/.local/opt/neovim/$v ~/.local/bin
tar -xzf nvim-linux-x86_64.tar.gz -C ~/.local/opt/neovim/$v --strip-components=1
ln -sfn ~/.local/opt/neovim/$v ~/.local/opt/neovim/current
ln -sfn ~/.local/opt/neovim/current/bin/nvim ~/.local/bin/nvim
```

The Neovim PPA has no 26.04 build. If you added it, remove it before `apt update`:

```sh
sudo rm /etc/apt/sources.list.d/neovim-ppa-ubuntu-stable-resolute.sources
```

Then install the rest, with `xclip` in place of `wl-clipboard` on X11:

```sh
sudo apt install git curl unzip build-essential clang ripgrep nodejs npm golang-go rustc cargo rust-src wl-clipboard
```

Start Neovim, run `:MasonInstall tree-sitter-cli`, and restart it to build the parsers.

Language servers install themselves on first start, and `:Mason` lists them. `:checkhealth nvim-treesitter mason vim.lsp vim.provider telescope` checks the rest.

## Usage

The leader key is Space.

| Keys | Action |
|---|---|
| `<leader>f` | Find files |
| `<leader>g` | Grep the project |
| `<leader>b` | Switch buffers |
| `<leader>/` | Search the buffer |
| `<leader>r` | Run the file |
| `<leader>s` | Replace the word under the cursor |
| `<leader>q` | List diagnostics |

`<leader>r` saves the file and runs it in a terminal split: C and C++ with clang, Go with `go run`, Python with uv or else python3, and Rust with cargo in a Cargo project or else rustc. Saving formats C, C++, Go, Python and Rust through their language servers.

Over SSH, yanks reach your local clipboard through the terminal (OSC 52), and `p` pastes the last yank. In tmux, that needs `set -g set-clipboard on`.

`:Typr` opens typing practice, and `:TyprStats` shows how it's going.

## License

MIT. See [LICENSE](LICENSE), which keeps kickstart.nvim's notice.
