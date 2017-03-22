+++
date = "2017-03-19T21:00:09-04:00"
draft = false
title = "16.04 and vscode"
tags = ["ubuntu","16.04","vscode"]

comments = false
share = false
menu = "main"
+++

Things you forget when you setup your virtual machine.

VSCode doesn't like to work over remote X. [You have to call](https://github.com/Microsoft/vscode/issues/3451):

~~~~
sed -i 's/BIG-REQUESTS/_IG-REQUESTS/' /usr/lib/x86_64-linux-gnu/libxcb.so.1
~~~~

