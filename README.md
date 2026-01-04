# Neovim config

Personal Neovim setup built around `lazy.nvim`, LSP, Treesitter, Telescope, and a small set of quality-of-life plugins.

Leader key: `<Space>`

## Requirements

- Neovim `0.11+` (this config uses `vim.lsp.config`)
- `git`
- A Nerd Font (icons)
- Optional but recommended:
	- `make` (builds `telescope-fzf-native` and LuaSnip’s optional regexp engine)
	- Node.js (for many LSP servers/tools like `tsserver`, `prettier`, `eslint`)

## Install

1. Back up your current config:

	 ```sh
	 mv ~/.config/nvim ~/.config/nvim.bak
	 ```

2. Clone this repo:

	 ```sh
	 git clone <YOUR_REPO_URL> ~/.config/nvim
	 ```

3. Start Neovim:

	 ```sh
	 nvim
	 ```

On first launch, `lazy.nvim` bootstraps automatically and installs plugins.

## What’s included

### Core

- Sensible defaults: relative numbers, 2-space indentation, system clipboard, split behavior, no swapfile
- `jk` to exit insert mode

### LSP

- LSP keymaps attached per-buffer via `LspAttach`
- Servers installed via Mason (`mason-lspconfig`):
	- `pyright`, `ts_ls`, `html`, `cssls`, `tailwindcss`, `svelte`, `lua_ls`, `graphql`, `emmet_ls`, `prismals`, `eslint`
- Extra server tweaks in `after/lsp/*` for:
	- `eslint` (filetypes)
	- `svelte` (notify TS/JS changes on save)
	- `graphql` / `emmet_ls` (filetypes)

### Formatting

- `conform.nvim` format-on-save (with LSP fallback)
- Formatters by filetype:
	- JS/TS/JSON/YAML/Markdown/GraphQL/etc: `prettier`
	- Lua: `stylua`
	- Python: `ruff`
	- Shell: `shfmt`

### Linting

- `nvim-lint` wired to run on `BufEnter`, `BufWritePost`, `InsertLeave`
- Python: `ruff`
- Avoids duplicate diagnostics if Ruff is attached as an LSP client

### Navigation & UI

- `telescope.nvim` (+ `telescope-fzf-native`)
- `nvim-tree` file explorer
- `trouble.nvim` diagnostics/quickfix UI (Telescope integration)
- `gitsigns.nvim` hunk actions + blame
- `lualine.nvim` statusline
- `bufferline.nvim` in tab mode
- `alpha-nvim` dashboard
- `which-key.nvim` keymap discoverability
- `indent-blankline.nvim` indentation guides
- `dressing.nvim` improved UI prompts/select

### Editing helpers

- `nvim-cmp` + `LuaSnip` + `friendly-snippets` + `lspkind`
- `nvim-autopairs` integrated with completion
- Treesitter textobjects (custom captures for JS/TS in `after/queries/ecma/textobjects.scm`)
- `substitute.nvim` for quick operator/line substitutions
- `nvim-surround`
- `vim-maximizer`
- `todo-comments.nvim` (+ Telescope picker + Trouble source)

## Keymaps

### General

- Insert: `jk` → escape
- `<leader>nh` → clear search highlights
- `<leader>+` / `<leader>-` → increment/decrement number

### Windows / tabs

- `<leader>sv` / `<leader>sh` → vertical/horizontal split
- `<leader>se` → equalize splits
- `<leader>sx` → close split
- `<leader>sm` → maximize/minimize split

- `<leader>to` / `<leader>tx` → new/close tab
- `<leader>tn` / `<leader>tp` → next/prev tab
- `<leader>tf` → open current buffer in new tab

### Telescope

- `<leader>ff` → find files
- `<leader>fr` → recent files
- `<leader>fs` → live grep
- `<leader>fc` → grep word under cursor
- `<leader>ft` → TODOs (Telescope)
- `<leader>fk` → keymaps

Inside Telescope (insert mode):

- `<C-j>` / `<C-k>` → move selection
- `<C-q>` → send to quickfix and open Trouble
- `<C-t>` → open results in Trouble

### File explorer (nvim-tree)

- `<leader>ee` → toggle tree
- `<leader>ef` → locate current file in tree
- `<leader>ec` → collapse
- `<leader>er` → refresh

### LSP (buffer-local)

- `gd` → definition
- `gD` → declaration
- `gr` → references (Telescope)
- `gi` → implementations (Telescope)
- `gt` → type definitions (Telescope)
- `K` → hover docs
- `<leader>rn` → rename
- `<leader>ca` → code action (normal/visual)
- `<leader>d` → line diagnostics float
- `<leader>D` → buffer diagnostics (Telescope)
- `[d` / `]d` → prev/next diagnostic
- `<leader>rs` → restart LSP

### Formatting / linting

- `<leader>mp` → format file / selection
- `<leader>l` → lint current file

### Git

- `<leader>lg` → LazyGit

Gitsigns:

- `[h` / `]h` → prev/next hunk
- `<leader>hs` / `<leader>hr` → stage/reset hunk (normal/visual)
- `<leader>hS` / `<leader>hR` → stage/reset buffer
- `<leader>hu` → undo stage hunk
- `<leader>hp` → preview hunk
- `<leader>hb` / `<leader>hB` → blame line / toggle blame
- `<leader>hd` / `<leader>hD` → diff this / diff vs `~`

### Trouble

- `<leader>xw` → workspace diagnostics
- `<leader>xd` → document diagnostics
- `<leader>xq` → quickfix list
- `<leader>xl` → location list
- `<leader>xt` → TODOs

### Sessions

- `<leader>wr` → restore session for cwd
- `<leader>ws` → save session for cwd

### Substitute

- `<leader>r` → substitute with motion
- `<leader>rr` → substitute line
- `<leader>R` → substitute to end of line
- Visual: `<leader>r` → substitute selection

### TODO comments

- `[t` / `]t` → prev/next todo

### Treesitter textobjects

Custom selects/moves/swaps are defined in the Treesitter textobjects plugin config and `after/queries/ecma/textobjects.scm`.

## Updating

- Update plugins: `:Lazy update`
- Update Treesitter parsers: `:TSUpdate`
- Update Mason tools/servers: `:Mason` (then update/install)

## Layout

- `init.lua` loads core, plugins, and LSP keymaps/diagnostics.
- `lua/rene/core/*` editor options + general keymaps.
- `lua/rene/lazy.lua` lazy.nvim bootstrap + plugin imports.
- `lua/rene/plugins/*` plugin specs/config.
- `lua/rene/plugins/lsp/*` Mason + LSP capabilities integration.
- `after/lsp/*` per-server overrides.
- `after/queries/*` custom Treesitter queries.

## Notes

- AI plugin config exists but is currently commented out in `lua/rene/plugins/ai.lua`.
