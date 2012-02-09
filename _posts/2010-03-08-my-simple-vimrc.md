---
title: My simple .vimrc
layout: post
category : configuration
tags : [vim, editor]
---
{% include JB/setup %}

Nothing special, but i think that my _Dropbox_ isn’t the right place where write it!!!

    set number
    set noerrorbells
    set softtabstop=4
    set expandtab
    set shiftwidth=4
    set autoindent
    set wrap
    syntax on
    colorscheme evening
    set diffopt=filler,iwhite
    vmap ,px !xmllint --format -<CR>
