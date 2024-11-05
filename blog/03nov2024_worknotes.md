3 ноября 2024

# Разбираюсь почему скомпилился проект

## Лог Движка

[UE5.4 Compile log history.txt](<additional/UE5.4 Compile log history.txt>)

Это файлик в который я скидывал логи неудавшихся компиляций. + последняя удавшаяся.

в этом логе помню меня привлекла эта строчка: 

```
2>Unable to build while Live Coding is active. Exit the editor and game, or press Ctrl+Alt+F11 if iterating on code in the editor or game
```

после чего я и закрыл движок. Нажал `Build`. Скомпилилось. Вникать не стал) было поздно и лень) 

Но надо будет снова найти где там настраивается `Live Coding`. Раз пытался искать, ведь в `4.27` он был на виду и тогда это была экспериментальная фича. Помню пользовался ей.

## Лог студии

После запуска инсталлера Visual Studio в режиме восстановить все удалилось и инсталлер выдал это:

[dd_setup_20241101224852_errors.log](additional/dd_setup_20241101224852_errors.log)

в файле вижу эту строчку: 

```
Журнал
        C:\Users\Dmitry Borisov\AppData\Local\Temp\dd_setup_20241101224852_588_UnrealEngineV1.log
```

и вот этот файл: [dd_setup_20241101224852_588_UnrealEngineV1.log](additional/dd_setup_20241101224852_588_UnrealEngineV1.log)

Чего там я могу понять пока не знаю. Читать/понимать это трудно. Может когда-нибудь.

