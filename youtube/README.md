# Вставка видео с YouTube используя iFrame - The right way:

Видео: [YouTube](https://www.youtube.com/watch?v=4JS70KB9GS0&t)

Автор: [Вадим Макеев](https://www.youtube.com/channel/UCaTfYudJUVA8cV_But8KZVQ)

## Проблема

При вставке iframe видео с youtube на сайт каждый iframe подгружает свои скрипты (даже если iframe уже есть на странице) и начинает предварительную загрузку видео, что может плохо сказаться на времени загрузки сайта и собственно сожрать много трафика (не забудем, что пользователь может пользоваться смарфтоном в данный момент)

## Решение

Для этого нам необходим контейнер слещующего вида, учитывая "доступность" и вариант отключения JavaScript.

> **Принцип работы:** если отключен JavaScript у нас даное решение остаеться в виде блока с ссылкой, при клике на которую мы переходим на видео в YouTube и можем его просмотреть. Если же JS включен, то данная конструкция при клике на кнопку "Play" данный блок преобразуеться в iframe и автоматически воспроизводит видео, что позволяет активировать их по одному.

```html
<div class="video">
  <a class="video__link" href="https://youtu.be/{video_ID}">
    <picture>
      <source
        srcset="https://i.ytimg.com/vi_webp/{video_ID}/maxresdefault.webp"
        type="image/webp"
      />
      <img
        class="video__media"
        src="https://i.ytimg.com/vi/{video_ID}/maxresdefault.jpg"
        alt="Не забываем прописать alt"
      />
    </picture>
  </a>
  <button class="video__button" type="button" aria-label="Запустить видео">
    <svg width="68" height="48" viewBox="0 0 68 48">
      <path
        class="video__button-shape"
        d="M66.52,7.74c-0.78-2.93-2.49-5.41-5.42-6.19C55.79,.13,34,0,34,0S12.21,.13,6.9,1.55 C3.97,2.33,2.27,4.81,1.48,7.74C0.06,13.05,0,24,0,24s0.06,10.95,1.48,16.26c0.78,2.93,2.49,5.41,5.42,6.19 C12.21,47.87,34,48,34,48s21.79-0.13,27.1-1.55c2.93-0.78,4.64-3.26,5.42-6.19C67.94,34.95,68,24,68,24S67.94,13.05,66.52,7.74z"
      ></path>
      <path class="video__button-icon" d="M 45,24 27,14 27,34"></path>
    </svg>
  </button>
</div>
```

> Не забываем импортировать CSS стили и JavaScript в проект.

### Где взять плейсхолдер видео YouTube? [StackOverflow](https://stackoverflow.com/questions/2068344/how-do-i-get-a-youtube-video-thumbnail-from-the-youtube-api/2068371#2068371)

> Обратите внимание, что Standard resolution **(sddefault)** и Maximum resolution **(maxresdefault)** не всегда могут быть доступны!

#### Default

> https://img.youtube.com/vi/insert_youtube_video_id_here/default.jpg

#### High quality

> https://img.youtube.com/vi/insert_youtube_video_id_here/hqdefault.jpg

#### Medium quality

> https://img.youtube.com/vi/insert_youtube_video_id_here/mqdefault.jpg

#### Standard resolution

> https://img.youtube.com/vi/insert_youtube_video_id_here/sddefault.jpg

#### Maximum resolution

> https://img.youtube.com/vi/insert_youtube_video_id_here/maxresdefault.jpg

#### Форматы

Изображения могут быть доступны в форматах: **jpg, webp**.

> В стилях используем подход адаптивных изображений от Netflix. Размеры самого блока в пропорции 16:9.
> Для преобразования этой конструкции в iframe используем JS, который указан в этой папке.

## Сниппеты

- [VS Code](/vscode-snippet.json);
