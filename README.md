What is this?
==================================
generate tags file for puppet's external DSL tags file
I use Vim, but probablly work in Emacs.

Usage
==================================

    t410 % puppet-tags.rb -h    

     puppet-tags.rb [-f] [DIR]
     
        -f : fullpath
        DIR: if omitted current directory is used

    t410 % puppet-tags.rb > tags
    t410 % 

Other Configuration
==================================
To highlight jump-able keyword in Vim, use underlinetag vim plugin.

<http://www.vim.org/scripts/script.php?script_id=3494>

To Vim's current directory to manifest's top directory.
install vim-localrc
<http://www.vim.org/scripts/script.php?script_id=3393>

then

    cd /etc/puppet/manifests
    puppet-tags > tags
    cat <<'EOS'> .local.vimrc
    lcd <sfile>:h
    set isk+=:,-
    EOS

isk is `iskeyword`. Including ':' is important, which is name space sparator.
