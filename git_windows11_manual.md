### Инструкция по установке git в Windows 11

Я не особо приветствую Windows, особенно последние их релизы, но у меня возникла необходимость использовать git для загрузки своих инструкций к себе в GitHub. Вообще git очень разнообразно можно использовать. Git клиенты с графикой сторонние я не хочу использовать, мне достаточно консоли. Вот собственно сама инструкция по установке и базовой настройке:

1. Щелкаем правой кнопкой на меню пуск и выбираем WindowsPowerShell(администратор), можно конечно через Win+R и командой.
2. Вводим `winget install Git.Git`
3. После того как консоль попросит подтвердить установку, подтверждаем
4. Перезапускаем PowerShell, так как после установки он еще не понимает, что ему уже доступна команда git
5. После перезапуска проверяем что git встал командой `git --version`, в терминале появится текущая версия git
6. Создаем репозиторий в GitHub, через сайт [GitHub](https://github.com/), соответственно если у вас нет аккаунта, то сначала создаем там аккаунт
6. Возвращаемся в терминал и вводим `git config --global user.name "вводим имя пользователя с GitHub"` ("" - оставляем обязательно)
7. Вводим `git config --global user.email "вводим свой e-mail"` ("" - оставляем обязательно)
8. Теперь идем в ту папку на диске, где хотим работать с созданным репозиторием, в моем случае вводим в терминале `cd 'C:\Users\sergey\Documents\'`
9. Клонируем репозиторий `git clone https://github.com/texport/manuals.git`
10. Переходим в созданную папку при клонировании репозитория `cd manuals`
11. Добавляем в папку manuals, то что хотим отправить в репозиторий, в моем случае я добавил эту инструкцию скопировав ее, ввожу команду в терминал `cp C:\Users\sergey\Documents\git_windows11_manual.md C:\Users\sergey\Documents\manuals\`
12. Фиксируем изменения командой в терминале `git add --all`
13. Отправляем внесенные изменения `git push`

