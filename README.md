# Python
Python learning
Prepare setup
1) sudo yum install openssl-devel -y
2) curl http://pyenv.run | bash
3) add env variable to bashrc
    ```
    export PYENV_ROOT="$HOME/.pyenv"
    command -v pyenv >/dev/null || export PATH="$PYENV_ROOT/bin:$PATH"
    eval "$(pyenv init -)"
    eval "$(pyenv virtualenv-init -)"
    ```
