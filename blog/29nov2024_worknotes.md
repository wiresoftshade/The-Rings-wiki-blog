# Научился резервировать git репозиторий в папку на свой комп

Чтобы сделать резервную копию git репозитория у себя на компьютере:

- сделать клон репозитория с опцией `--mirror`
    - либо выполнить `fetch all` в SmartGit(предположительно)
- забрать все объекты LFS

## 1. Сделать клон репозитория с опцией `--mirror`

- To perform a mirror clone, use the `git clone` command with the `--mirror` option.

```
git clone --mirror https://github.com/EXAMPLE-USER/REPOSITORY.git
```

Я исспользую SmartGit и я не делал этот пункт. Он, вроде бы сам забирает всегда полную версию репозитория. Либо я чего-то не понял, но у меня сработало. Я смог потом забирать другие ветки, которые не были в списки `local`, а были только в `origin`.

Думаю все получилось потому что я выполнял команду `fetch all` в SmartGit

При клонировании репозитория в SmartGit можно отметить опцию `Include Submodules` — SmartGit автоматически подгрузит все модули. Если отметить опцию `Fetch all Heads and Tags`, то SmartGit после создания папки проекта скачает все ветки и теги для данного репозитория.

## 2. Забрать все объекты LFS

- If the repository includes Git Large File Storage objects, pull in the objects. For more details on Git Large File Storage and how to install it, see "[About Git Large File Storage](https://docs.github.com/en/repositories/working-with-files/managing-large-files/about-git-large-file-storage)."

```    
git lfs fetch --all
```

Эту команду я выполнял и он заметно подгрузид объекты LFS и написал сколько.

Использованные ссылки: https://docs.github.com/en/repositories/archiving-a-github-repository/backing-up-a-repository


