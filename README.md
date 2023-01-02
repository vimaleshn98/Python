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
5) pyenv versions
   this will system pyhton version and new added pyhton version
   so 
6) make new version of python as default python version
   pyenv shell 3.7.6
    ![image](https://user-images.githubusercontent.com/52690867/210213837-1ef3b170-94c5-485d-9011-e0db34cce970.png)

7) python --version
8)  best practise to upgrade pip also
    ``` pip3.7 install --upgrade pip ```
9) if VS code using install python extensions
