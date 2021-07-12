# Инструкция по созданию SSH-ключей с примерами (для macOS)

С 13 августа 2021 г. больше не будут работать пароли учетных записей при аутентификации операций Git на GitHub.com.

Поэтому, как один из вариантов, можно создать и использовать ключ  SSH.

Об этом может напомнить и VSCode:

![предупреждение vscode про ключи](/pictures/ssh/Untitled.png)


Инструкция по созданию находится здесь - [https://docs.github.com/en/github/authenticating-to-github/connecting-to-github-with-ssh/generating-a-new-ssh-key-and-adding-it-to-the-ssh-agent#generating-a-new-ssh-key](https://docs.github.com/en/github/authenticating-to-github/connecting-to-github-with-ssh/generating-a-new-ssh-key-and-adding-it-to-the-ssh-agent#generating-a-new-ssh-key)

Сначала можно проверить был ли такой ключ создан раннее: вводим команду ls ~/.ssh, если не находит - ключей нет.


**Создание SSH-ключа**

Вводим в терминал команду ssh-keygen -t ed25519 -C “your_email@example.com”, подставляя свой адрес. Это создает новый ключ ssh, используя предоставленный адрес электронной почты в качестве метки.

![screenshot](/pictures/ssh/Untitled-1.png)

Когда  будет предложено «Введите файл для сохранения ключа», необходимо нажать Enter. Это принимает расположение файла по умолчанию.

![screenshot](/pictures/ssh/Untitled-2.png)

В командной строке можно ввести дополнительную безопасную парольную фразу. Если не добавлять - нажать Enter.

![screenshot](/pictures/ssh/Untitled-3.png)

Ключ создался.

**Добавление SSH-ключа в ssh-agent**

Запускаем ssh-agent в фоновом режиме командой eval "$(ssh-agent -s)”.

![screenshot](/pictures/ssh/Untitled-4.png)

Если используется macOS Sierra 10.12.2 или новее, то нужно будет изменить свой ~/.ssh/config файл, чтобы ключи автоматически загружались в ssh-agent и сохранялись парольные фразы в связке ключей.

Сначала необходимо проверить, существует ли файл в расположении по умолчанию командой open ~/.ssh/config.

![screenshot](/pictures/ssh/Untitled-5.png)

Если файл не существует, необходимо его создать командой touch ~/.ssh/config.

![screenshot](/pictures/ssh/Untitled-6.png)

Далее снова открываем файл командой open ~/.ssh/config, затем необходимо его изменить, чтобы он содержал следующие строки.

![screenshot](/pictures/ssh/Untitled-7.png)

Если кодовую фразу к ключу не добавлять, то строку  UseKeychain следует удалить.

Далее необходимо добавить закрытый ключ SSH к ssh-agent и сохранить парольную фразу в цепочке для ключей командой ssh-add -K ~/.ssh/id_ed25519. Если парольной фразы нет, то команду -К нужно удалить.

![screenshot](/pictures/ssh/Untitled-8.png)

**Добавление SSH-ключа в учетную запись на GitHub**

Инструкция: [https://docs.github.com/en/github/authenticating-to-github/connecting-to-github-with-ssh/adding-a-new-ssh-key-to-your-github-account](https://docs.github.com/en/github/authenticating-to-github/connecting-to-github-with-ssh/adding-a-new-ssh-key-to-your-github-account)

Скопировать открытый ключ SSH в буфер обмена командой pbcopy < ~/.ssh/id_ed25519.pub.

![screenshot](/pictures/ssh/Untitled-9.png)

Зайти в свой профиль на GitHub -> Настройки -> SSH и GPG ключи -> Новый ключ SSH -> В поле Заголовок добавить описание, в поле Ключ вставить скопированный ключ. Возможно, понадобится ввести свой пароль от GitHub.

Далее в Терминале ввести команду ssh -T [git@github.com](mailto:git@github.com) и после ввести Yes.

![screenshot](/pictures/ssh/Untitled-10.png)

![screenshot](/pictures/ssh/Untitled-11.png)

**Переключение с HTTPS на SSH**

Чтобы использовать ключ вместо логина и пароля (юзернейм), необходимо переключить удаленные URL-адреса с HTTPS на SSH. Инструкция: [https://docs.github.com/en/get-started/getting-started-with-git/managing-remote-repositories#switching-remote-urls-from-https-to-ssh](https://docs.github.com/en/get-started/getting-started-with-git/managing-remote-repositories#switching-remote-urls-from-https-to-ssh)

В терминале открываем папку своего проекта и командой git remote -v перечисляем репозитории.

![screenshot](/pictures/ssh/Untitled-12.png)

Изменяем URL-адрес с HTTPS на SSH с помощью команды git remote set-url origin git@github.com:USERNAME/REPOSITORY.git (заменяем https:// на git@).

![screenshot](/pictures/ssh/Untitled-13.png)

Проверяем, что получилось командой git remote -v.

![screenshot](/pictures/ssh/Untitled-14.png)
