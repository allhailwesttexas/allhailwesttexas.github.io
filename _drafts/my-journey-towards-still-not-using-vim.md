My journey towards still not using vim on a large Python project. 

I don't really want it to be an IDE but I want to be able to write code for the project in Vim. If I need an interactive debugger I will probably stick with PyCharm.

- Neovim is out now. I don't really know what kind of upsides I get versus using plain Vim, but it seems like the future. I install Neovim. It is surprisingly fiddly if you want to avoid the snap store, which I do.

- OK, let's find the best code intellisense thing. Since my last vim adventure there's been some developments. There's `coc.nvim` which is a "batteries included" implementation of the [Language Server Protocl]() or LSP.
- There's a variety of plugin managers

- OK, let's get some sort of "go to file" working. I've been hearing about [fzf]() so I look into that. It comes with a vim plugin! Perfect. My project is very large
so it takes a few seconds to load all the files, but in practice it doesn't matter since I can start typing for what I want to find straight away anyway. But it annoys me
enough that I start wondering about ignoring files in the output, and it turns out you can swap the searcher to [ripgrep]() and it will ignore files in `.gitignore` by default.
Easy! Now my search window is very fast and I am happy.
