# Neovim Config

A clean Neovim setup with LSP, autocompletion, and fuzzy finding. Requires **Neovim 0.11+**.

## Prerequisites

```bash
brew install neovim ripgrep fd
```

- **ripgrep** and **fd** are needed by Telescope for live grep and file finding.
- **Node.js** is needed for the TypeScript and Pyright language servers.

## Install

Back up any existing config, then symlink or copy:

```bash
# Back up existing config
mv ~/.config/nvim ~/.config/nvim.bak

# Option 1: Symlink (recommended — edits stay in the repo)
ln -s ~/nvim-config ~/.config/nvim

# Option 2: Copy
cp -r nvim-config ~/.config/nvim
```

On first launch, lazy.nvim will auto-bootstrap and install all plugins. Mason will install the configured LSP servers (lua_ls, ts_ls, pyright).

To install treesitter parsers, run inside Neovim:

```
:TSInstall bash c html css javascript typescript json lua markdown python yaml
```

## What's Included

| Category | Plugins |
|---|---|
| Plugin manager | lazy.nvim |
| Theme | Catppuccin Mocha |
| LSP | nvim-lspconfig + mason.nvim (lua_ls, ts_ls, pyright) |
| Completion | nvim-cmp (LSP, snippets, paths, buffer) |
| Snippets | LuaSnip + friendly-snippets |
| Syntax | nvim-treesitter |
| Fuzzy finder | Telescope + fzf-native |
| Status line | lualine.nvim |
| Git | gitsigns.nvim |
| Editing | nvim-surround, nvim-autopairs, Comment.nvim |
| UI | indent-blankline, which-key, fidget.nvim |

## Key Bindings

Leader key is **Space**.

### General

| Keys | Action |
|---|---|
| `<Space>r` | Save and run current file (Python, JS, TS, Lua, Bash) |
| `<Space>q` | Open diagnostics quickfix list |
| `Esc` | Clear search highlight |
| `Ctrl+h/j/k/l` | Navigate between splits |
| `q` | Close the run-output terminal split |

### Finding (Telescope)

| Keys | Action |
|---|---|
| `<Space>ff` | Find files |
| `<Space>fg` | Live grep |
| `<Space>fb` | Find buffers |
| `<Space>fh` | Find help tags |
| `<Space>fd` | Find diagnostics |
| `<Space>fr` | Resume last search |
| `<Space>fw` | Grep word under cursor |
| `<Space>f.` | Recent files |

### LSP (active when a language server attaches)

| Keys | Action |
|---|---|
| `gd` | Go to definition |
| `gr` | Go to references |
| `gI` | Go to implementation |
| `gy` | Go to type definition |
| `gD` | Go to declaration |
| `K` | Hover documentation |
| `<Space>rn` | Rename symbol |
| `<Space>ca` | Code action |
| `<Space>ds` | Document symbols |
| `<Space>ws` | Workspace symbols |
| `<Space>th` | Toggle inlay hints |

### Completion (in insert mode)

| Keys | Action |
|---|---|
| `Tab` | Accept completion / jump to next snippet field |
| `Shift+Tab` | Jump to previous snippet field |
| `Ctrl+n` / `Ctrl+p` | Next / previous item |
| `Ctrl+Space` | Trigger completion |
| `Ctrl+b` / `Ctrl+f` | Scroll docs |

### Editing

| Keys | Action |
|---|---|
| `gcc` | Toggle line comment |
| `gc` (visual) | Toggle comment on selection |
| `ys{motion}{char}` | Add surround (e.g. `ysiw"` to surround word with quotes) |
| `ds{char}` | Delete surround |
| `cs{old}{new}` | Change surround |

## Adding More Language Servers

Open Neovim and run `:Mason` to browse available servers. Install one with `:MasonInstall <name>`.

Then add it to `lua/plugins/lsp.lua`:

```lua
vim.lsp.config("new_server", { capabilities = capabilities })
vim.lsp.enable({ "lua_ls", "ts_ls", "pyright", "new_server" })
```

## File Structure

```
init.lua                    -- Core options, keymaps, lazy.nvim bootstrap
lua/plugins/
  colorscheme.lua           -- Catppuccin theme
  completion.lua            -- nvim-cmp + LuaSnip
  lsp.lua                   -- LSP, Mason, keymaps
  telescope.lua             -- Fuzzy finder
  treesitter.lua            -- Syntax highlighting
  ui.lua                    -- Statusline, git signs, indent guides, etc.
```
