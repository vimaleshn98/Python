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
4) pyenv install 3.7.6
5) pyenv --versions
   this will system pyhton version and new added pyhton version
   so 
6) make new version of python as default python version
   pyenv shell 3.7.6
7) python --version
