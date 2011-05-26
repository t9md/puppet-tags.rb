これは何？
==================================
Puppet の 外部 DSL( マニフェスト記述言語 )のタグジャンプ用の tags  ファイルを生成します。
私は Vim を使用していますが、Emacs でも機能すると思います。

現在は、`class`, `define` のみ対応しています。

使い方
==================================

    t410 % puppet-tags.rb -h    

     puppet-tags.rb [-f] [DIR]
     
        -f : fullpath
        DIR: if omitted current directory is used

    t410 % puppet-tags.rb > tags
    t410 % 

その他の設定
==================================
underlinetag
----------------------------------
どのキーワードがジャンプできるかを知りたければ、 *underlinetag* プラグインを試してみて下さい。

* [ underlinetag ]( http://www.vim.org/scripts/script.php?script_id=3494 )


vim-localrc
----------------------------------
相対パスでファイルパスが書かれている tags ファイルを使用する場合、Vim のカレントディレクトリ(`:pwd`) 
を tags ファイルを生成した時の、ディレクトリに固定する事が重要です。

また、`apache::mod_ssl` のようなコロン(:)を含むクラス名、define名をひとかたまりのキーワードとして Vim に
認識させる必要があります。

Puppet のマニフェストのトップディレクトリに  Vim のカレントディレクトリを固定したい場合、
*vim-localrc* プラグインを試してみて下さい。

* [ vim-localrc ]( http://www.vim.org/scripts/script.php?script_id=3393 )

下記の設定をします。

    cd /etc/puppet/manifests
    puppet-tags > tags
    cat <<'EOS'> .local.vimrc
    lcd <sfile>:h
    set isk+=:,-
    EOS

上記の、isk は `iskeyword`の略で、puppet の ネームスペースセパレータである `:` をキーワードに含めるように 
しています。これにより、`apache::mod_ssl` のような `:` コロンを含む `class`, `define` でも一つのキーワード 
として処理可能、つまりジャンプの単位として扱ってくれるようになります。
