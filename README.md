# docs
полезное
#
Создание и настройка ssh ключей
1. Запустите Git Bash и введите
ssh-keygen -t rsa -C "your@email.ru"
2. На вопрос “Enter file in which to save the key” введите id_rsa и нажмите “Enter”
3. Далее введите любой пароль, и подтвердите его (лучше пропустить, потому что каждый раз при соединении с github, придется вводить его)
4. Скопируйте созданные в директории пользователя файлы “id_rsa” и “id_rsa.pub” в папку c:\Documents and Settings\Username\.ssh (XP) или c:\Users\Username\.ssh (Vista). При необходимости создайте эту папку с помощью команды
mkgir ".ssh"
в консоли Windows
5. Откройте страницу настроек Вашего аккаунта github https://github.com/account
6. Добавьте содержимое публичного ключа из файла “id_rsa.pub”, воспользовавшись ссылкой “add public key” в разделе “SSH Public Keys”
7. Проверьте работоспособность ключа, введя в Git Bash:
ssh git@github.com
# git
Сбросить историю
Создаем заново
git init
git commit...
git remote add origin git://github.com/paulboone/ticgit.git
git push origin master -f


# pip wheel
полезное
#
https://dizballanze.com/ru/python-wheels-dlia-bystroi-ustanovki-zavisimostei/
pip freeze > 1.txt

pip install -U pip
pip install wheel
mkdir wheels
pip wheel -w wheels/ -r 1.txt --pre --allow-all-external

pip install --no-index -f wheels/ -r 1.txt

# conda env
conda create -n mlenv
conda activate mlenv 
conda list
conda install jupyter
jupyter notebook

conda deactivate
conda env list
conda env remove -n mlenv
  








@REM Copyright (C) 2012 Anaconda, Inc
@REM SPDX-License-Identifier: BSD-3-Clause
@REM Test first character and last character of %1 to see if first character is a "
@REM   but the last character isn't.
@REM This was a bug as described in https://github.com/ContinuumIO/menuinst/issues/60
@REM When Anaconda Prompt has the form
@REM   %windir%\system32\cmd.exe "/K" "C:\Users\builder\Miniconda3\Scripts\activate.bat" "C:\Users\builder\Miniconda3"
@REM Rather than the correct
@REM    %windir%\system32\cmd.exe /K ""C:\Users\builder\Miniconda3\Scripts\activate.bat" "C:\Users\builder\Miniconda3""
@REM this solution taken from https://stackoverflow.com/a/31359867
@set "_args1=%1"
@set _args1_first=%_args1:~0,1%
@set _args1_last=%_args1:~-1%
@set _args1_first=%_args1_first:"=+%
@set _args1_last=%_args1_last:"=+%
@set _args1=

@if "%_args1_first%"=="+" if NOT "%_args1_last%"=="+" (
    @CALL "%~dp0..\condabin\conda.bat" activate
    @GOTO :End
)

@REM This may work if there are spaces in anything in %*
@CALL "%~dp0..\condabin\conda.bat" activate %*

:End
@set _args1_first=
@set _args1_last=
