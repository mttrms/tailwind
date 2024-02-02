# Next.js/Tailwind Starter Template
Base repo taken from https://github.com/timlrx/tailwind-nextjs-starter-blog

Note: I have not used this repo outside of this testing, I just pulled a random tailwind/react project down. My example was using Remix Stacks like the [Blue Stack](https://github.com/remix-run/blues-stack) but that requires a bit more setup.

## Purpose
Example repository and setup instructions to reproduce protected folders interfering with tailwindcss autocompletion in Neovim on Linux.

## Requirements
Taken from [LazyVim](https://www.lazyvim.org/)
- Neovim >= 0.9.0 (needs to be built with LuaJIT)
- Git >= 2.19.0 (for partial clones support)
- a C compiler for `nvim-treesitter`
- Ubuntu 22 (likely other linux distros. I've only tested this on a dedicated Linux box as well as WSL w/ Windows)

## LazyVim setup
Taken from [LazyVim Installation](https://www.lazyvim.org/installation)

Backup current files:
```
# required
mv ~/.config/nvim{,.bak}

# optional but recommended
mv ~/.local/share/nvim{,.bak}
mv ~/.local/state/nvim{,.bak}
mv ~/.cache/nvim{,.bak}
```

Clone the starter.
`git clone https://github.com/LazyVim/starter ~/.config/nvim`

Launch Neovim with `nvim`

Launch `Mason` with `:Mason`

Install `tailwindcss` LSP (scroll to tailwind, type `i`)

## Reproduction Steps
1. Start `nvim`
2. Open `Main.tsx` 
3. Verify that when editing a `className` you see Tailwind auto completions
4. Exit `nvim`
5. `sudo mkdir test-dir`
6. `sudo chmod 222 test-dir`
7. start `nvim`
8. Open `Main.tsx`
9. Note that you no longer have Tailwind auto completions when editing `className` prop
10. Exit `nvim`, `sudo chmod 777 test-dir`, try step 8 again and you will see auto completions working as expected

You can also write some Javascript at the bottom of the file and see JS autocompletions work as expected regardless of the protected directory.

I tested this just by adding this to the bottom of the file:
```
const someVar = 'testing';
someVar. // then inspecting autocompletion popup
```
