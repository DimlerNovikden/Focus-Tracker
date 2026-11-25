# Сайт политики конфиденциальности

Содержимое этой папки публикуется на GitHub Pages. Есть важная особенность:
**политика может лежать по любому пути, а `app-ads.txt` — только в корне домена.**
Рекламные сети (Яндекс, Google) ищут файл строго по адресу `https://<домен>/app-ads.txt`,
поэтому одного репозитория `Focus-Tracker` для него недостаточно.

## Схема публикации

| Что | Репозиторий | Файлы | Адрес |
| --- | --- | --- | --- |
| Политика | `Focus-Tracker` (project pages) | `index.html`, `privacy-policy.html`, `.nojekyll` | `https://dimlernovikden.github.io/Focus-Tracker/` |
| `app-ads.txt` | `DimlerNovikden.github.io` (user pages) | `app-ads.txt` (+ опционально `index.html` с редиректом) | `https://dimlernovikden.github.io/app-ads.txt` |

Исходники лежат в этой папке; `app-ads.txt` отсюда копируется в корневой репозиторий
`DimlerNovikden.github.io` без изменений.

> Альтернатива: если у вас есть свой домен (например, `focus-app.ru`), положите оба файла
> в его корень. Тогда политика будет на `https://focus-app.ru/`, а `app-ads.txt` —
> на `https://focus-app.ru/app-ads.txt`. Это самый простой вариант с точки зрения правил
> рекламных сетей.

## 1. Репозиторий политики (`Focus-Tracker`)

1. Создайте на GitHub **публичный** репозиторий `Focus-Tracker`.
   Важно: на 25.11.2026 аккаунт `https://github.com/DimlerNovikden` отвечает 404 — его нужно
   создать или уточнить правильный логин. Если логин другой, замените `dimlernovikden`
   в `index.html`, `PRIVACY_POLICY.md` и `src/core/privacy.ts`.
2. Скопируйте в корень репозитория `index.html`, `privacy-policy.html` и `.nojekyll`.
3. Выполните:
   ```powershell
   git init
   git add index.html privacy-policy.html .nojekyll
   git commit -m "Add privacy policy"
   git branch -M main
   git remote add origin https://github.com/DimlerNovikden/Focus-Tracker.git
   git push -u origin main
   ```
4. **Settings → Pages → Source: Deploy from a branch → main / (root) → Save**.
5. Проверьте `https://dimlernovikden.github.io/Focus-Tracker/`.

## 2. Корневой репозиторий для `app-ads.txt` (`DimlerNovikden.github.io`)

1. Создайте **публичный** репозиторий с именем `DimlerNovikden.github.io`
   (имя должно совпадать с логином — это user pages, они отдаются из корня домена).
2. Скопируйте туда `app-ads.txt` из этой папки.
3. Запушьте в ветку `main`:
   ```powershell
   git init
   git add app-ads.txt
   git commit -m "Add app-ads.txt"
   git branch -M main
   git remote add origin https://github.com/DimlerNovikden/DimlerNovikden.github.io.git
   git push -u origin main
   ```
4. **Settings → Pages** для этого репозитория обычно уже включены; если нет —
   включите `main / (root)`.
5. Проверьте `https://dimlernovikden.github.io/app-ads.txt`.

Опционально положите в этот же корень `index.html` с редиректом на политику, чтобы
корень домена не отдавал 404:

```html
<!DOCTYPE html>
<html lang="ru">
<head>
  <meta charset="UTF-8">
  <meta http-equiv="refresh" content="0; url=https://dimlernovikden.github.io/Focus-Tracker/">
  <title>Политика конфиденциальности</title>
</head>
<body>
  <p><a href="https://dimlernovikden.github.io/Focus-Tracker/">Политика конфиденциальности</a></p>
</body>
</html>
```

## Проверка после публикации

```powershell
# Политика: 200 + HTML с заголовком
curl.exe -s -o NUL -w "%{http_code}`n" https://dimlernovikden.github.io/Focus-Tracker/

# app-ads.txt: 200, text/plain, первая строка e-planning.net
curl.exe -sI https://dimlernovikden.github.io/app-ads.txt
curl.exe -s https://dimlernovikden.github.io/app-ads.txt | Select-Object -First 3
```

В карточке приложения в Google Play / App Store укажите сайт `https://dimlernovikden.github.io/`
(или свой домен) — именно из этого домена краулер будет брать `/app-ads.txt`. Для RuStore
подтверждение владения идёт кодом, сайт не обязателен.

## Что заменить перед публикацией

- [ ] Логин GitHub и имя репозитория, если они отличаются от `DimlerNovikden` / `Focus-Tracker`.
- [ ] Дату вступления в силу (сейчас 25.11.2026) — в `index.html`, `PRIVACY_POLICY.md`,
      `src/core/privacy.ts`.
- [ ] Email `chertchertila@vk.com`, если он изменится.
- [ ] `app-ads.txt` — актуальная выгрузка из кабинета РСЯ (170 строк, `yandex.com ... DIRECT`).
- [ ] `PRIVACY_POLICY_URL` и `APP_ADS_TXT_URL` в `src/core/privacy.ts` — после публикации
      убедитесь, что оба адреса открываются.

## Юридическая оговорка

Текст политики — рабочий черновик, подготовленный по фактическому составу приложения
(Яндекс Мобильная Реклама, только Android, без аналитики и платежей). Перед публикацией
его должен проверить юрист: это юридически значимый документ.
