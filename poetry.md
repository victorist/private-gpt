# Установка Poetry
```
curl -sSL https://install.python-poetry.org | python3 -
```

После установки...

To get started you need Poetry's bin directory (/Users/victoristratov/.local/bin) in your `PATH`
environment variable.

Add `export PATH="/Users/victoristratov/.local/bin:$PATH"` to your shell configuration file `.zshrc`.

Alternatively, you can call Poetry explicitly with `/Users/victoristratov/.local/bin/poetry`.

You can test that everything is set up by executing:

`poetry --version`


# Включите завершение табуляции для Bash, Fish или Zsh
**Help:**
  
  One can generate a completion script for `poetry` that is compatible with a given shell. The script is output on `stdout` allowing one to re-direct the output to the file of their choosing. Where you place the file will depend on which shell, and which operating system you are using. Your particular configuration may also determine where these scripts need to be placed.
  
  Here are some common set ups for the three supported shells under Unix and similar operating systems (such as GNU/Linux).
  
  *BASH:*
  
  Completion files are commonly stored in `/etc/bash_completion.d/`
  
  Run the command:
  
  `poetry completions bash > /etc/bash_completion.d/poetry.bash-completion`
  
  This installs the completion script. You may have to log out and log back in to your shell session for the changes to take effect.
  
  *FISH:*
  
  Fish completion files are commonly stored in`$HOME/.config/fish/completions`
  
  Run the command:
  
  `poetry completions fish > ~/.config/fish/completions/poetry.fish`
  
  This installs the completion script. You may have to log out and log back in to your shell session for the changes to take effect.
  
  *ZSH:*
  
  ZSH completions are commonly stored in any directory listed in your `$fpath` variable. To use these completions, you must either add the generated script to one of those directories, or add your own to this list.
  
  Adding a custom directory is often the safest best if you're unsure of which directory to use. First create the directory, for this example we'll create a hidden directory inside our `$HOME` directory
  
  `mkdir ~/.zfunc`
  
  Then add the following lines to your `.zshrc` just before `compinit`
  
  `fpath+=~/.zfunc`
  
  Now you can install the completions script using the following command
  
  `poetry completions zsh > ~/.zfunc/_poetry`
  
  You must then either log out and log back in, or simply run
  
  `exec zsh`

  Затем вы необходимо добавить следующие строки в `~/.zshrc`, если они еще не существуют:
  


  
  For the new completions to take affect.
  
  _CUSTOM LOCATIONS:_
  
  Alternatively, you could save these files to the place of your choosing, such as a custom directory inside your $HOME. Doing so will require you to add the proper directives, such as `source`ing inside your login script. Consult your shells documentation for how to add such directives.