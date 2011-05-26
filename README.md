What is this?
==================================
Generate tags file for puppet's external DSL.
I use Vim, but probablly work in Emacs.

Currentry, only `class` and `define` are suported(=jump-able).

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
underlinetag
----------------------------------
To highlight jump-able keyword in Vim, use underlinetag vim plugin.

* [ underlinetag ]( http://www.vim.org/scripts/script.php?script_id=3494 )


vim-localrc
----------------------------------
When you use tags file which is based on relative path, fixing Vim's current directory(`:pwd`) 
to directory( where you generate tags on ) is very important to let vim find the proper file.

Also,it is important to let Vim know the word such like `apache::mod_ssl` as one non-spearated keyword. 

To fix Vim's current directory to manifest's top directory.
install vim-localrc

* [ vim-localrc ]( http://www.vim.org/scripts/script.php?script_id=3393 )

then

    cd /etc/puppet/manifests
    puppet-tags > tags
    cat <<'EOS'> .local.vimrc
    lcd <sfile>:h
    set isk+=:,-
    EOS

isk is `iskeyword`. Including ':' is important, which is name space sparator.
