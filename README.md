```markdown
# 🧠 Modern Vim Setup for Python Development



This repo includes a plug-and-play `.vimrc` configuration designed for Python development and productivity.


## ✨ Features

- 🐍 Enhanced Python syntax & REPL integration
- 🚀 Productivity tools like commenting, repeating, surrounding
- 🔍 Fuzzy file search with FZF
- 📁 File explorer (NERDTree)
- 🎨 Onedark theme + airline status bar
- 🧠 Git integration + GitHub Copilot AI suggestions

---

## 🛠️ Installation Guide

## 🍺 Install Homebrew (macOS)

First, make sure you have [Homebrew](https://brew.sh/) installed. It's the de facto package manager for macOS.

Open Terminal and run:

```sh
/bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"

### 1. Install Vim or Neovim

**Vim:**

```bash
# Debian/Ubuntu
sudo apt install vim

# macOS (with Homebrew)
brew install vim
```

**Neovim(Only if You want to be fancy):**

```bash
# Debian/Ubuntu
sudo apt install neovim

# macOS
brew install neovim
```

---

### 2. Install vim-plug

**For Vim:**

```bash
curl -fLo ~/.vim/autoload/plug.vim --create-dirs \
  https://raw.githubusercontent.com/junegunn/vim-plug/master/plug.vim
```

**For Neovim:**

```bash
curl -fLo ~/.local/share/nvim/site/autoload/plug.vim --create-dirs \
  https://raw.githubusercontent.com/junegunn/vim-plug/master/plug.vim
```

---

### 3. Create `.vimrc` or `init.vim`

**Vim users:**

```bash
nano ~/.vimrc
```

**Neovim users:**

```bash
mkdir -p ~/.config/nvim
nano ~/.config/nvim/init.vim
```

Paste the following content inside:

```vim
call plug#begin('~/.vim/plugged')

" --- 🐍 Python Development ---
Plug 'vim-python/python-syntax'
Plug 'jmcantrell/vim-virtualenv'
Plug 'jpalardy/vim-slime'

" --- 🚀 Productivity Tools ---
Plug 'tpope/vim-surround'
Plug 'tpope/vim-commentary'
Plug 'tpope/vim-repeat'
Plug 'neoclide/coc.nvim', {'branch': 'release'}

" --- 🔍 Fuzzy Finder + Navigation ---
Plug 'junegunn/fzf', { 'do': { -> fzf#install() } }
Plug 'junegunn/fzf.vim'
Plug 'easymotion/vim-easymotion'

" --- 📁 File Tree Explorer ---
Plug 'preservim/nerdtree'

" --- 🎨 UI and Aesthetic ---
Plug 'vim-airline/vim-airline'
Plug 'vim-airline/vim-airline-themes'
Plug 'joshdick/onedark.vim'
Plug 'jiangmiao/auto-pairs'

" --- 🏁 Startup Screen ---
Plug 'mhinz/vim-startify'

" --- 🧠 Git + AI ---
Plug 'tpope/vim-fugitive'
Plug 'github/copilot.vim'

call plug#end()

syntax on
filetype plugin indent on

set expandtab
set shiftwidth=4
set tabstop=4
set softtabstop=4
set clipboard=unnamedplus
set number

" ALE Python settings (requires ALE plugin separately)
let g:ale_linters = {'python': ['flake8', 'mypy']}
let g:ale_fixers = {'python': ['black']}
let g:ale_fix_on_save = 1

colorscheme onedark

" --- Slime config for REPL ---
let g:slime_target = "tmux"
let g:slime_python_ipython = 1
let g:slime_dont_ask_default = 1
xmap <leader>ss <Plug>SlimeRegionSend
nmap <leader>ss <Plug>SlimeParagraphSend

" NERDTree
nnoremap <C-n> :NERDTreeToggle<CR>

" CoC autocomplete
inoremap <silent><expr> <C-space> coc#refresh()
autocmd CursorHoldI * silent call CocActionAsync('showSignatureHelp')
inoremap <silent><expr> <C-j> pumvisible() ? coc#_select_confirm() : "\<C-j>"
inoremap <silent><expr> <C-p> pumvisible() ? "\<C-p>" : "\<C-p>"
inoremap <silent><expr> <C-Space> coc#refresh()
```

---

### 4. Open Vim and Install Plugins

Launch Vim and run:

```vim
:PlugInstall
```

This will install all the plugins listed.

---

### 5. 🧪 Python Linting & Formatting (Optional but Recommended)

Install required tools globally or in a virtual environment:

```bash
pip install flake8 mypy black virtualenv
```

---

## 🧠 Usage Tips

| Feature            | Command / Shortcut           |
| ------------------ | ---------------------------- |
| Toggle File Tree   | `<Ctrl> + n`                 |
| Open FZF Files     | `:Files`                     |
| Send code to REPL  | Visual select + `<leader>ss` |
| Git status         | `:G` or `:Gstatus`           |
| Start screen       | Launch Vim (Startify loads)  |
| Copilot trigger    | Usually auto, or `<C-Space>` |
| Completion nav     | `<C-j>` / `<C-p>`            |

---

## 🔌 Optional Plugin: ALE

If you want to use **ALE** for linting instead of CoC:

```vim
Plug 'dense-analysis/ale'
```

---

## 💬 Final Notes

- Works with both Vim and Neovim
- Make sure to install `fzf` binary if using `fzf.vim`:
  
```bash
brew install fzf     # macOS
sudo apt install fzf # Linux
```

---

Happy Vimming! ⚡
```
