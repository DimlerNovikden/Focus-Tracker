# Сайт политики конфиденциальности

Опубликовано 25.11.2026 на GitHub Pages.

| Что | Адрес | Статус |
| --- | --- | --- |
| Политика (основная) | https://dimlernovikden.github.io/Focus-Tracker/ | 200 |
| Политика (корень домена) | https://dimlernovikden.github.io/ | 200 |
| `app-ads.txt` | https://dimlernovikden.github.io/app-ads.txt | 200, `text/plain` |

## Как устроено

- Репозиторий `DimlerNovikden/Focus-Tracker` (public) — страница политики:
  `index.html`, `privacy-policy.html`, `PRIVACY_POLICY.md`, `README.md`, `.nojekyll`.
- Репозиторий `DimlerNovikden/DimlerNovikden.github.io` (public, user pages) —
  `app-ads.txt` в корне домена и копия `index.html`.
- `app-ads.txt` обязан лежать именно в корне `https://dimlernovikden.github.io/`,
  иначе краулеры Яндекса и Google его не найдут. Путь `/Focus-Tracker/app-ads.txt`
  для этого не подходит.

## Обновление

1. Правите `index.html` / `PRIVACY_POLICY.md` в этой папке.
2. Загружаете изменённые файлы в `Focus-Tracker` (Add file → Upload files) и,
   если менялась политика, копируете `index.html` в `DimlerNovikden.github.io`.
3. Обновляете `app-ads.txt`, если в кабинете РСЯ изменился список продавцов.
4. Проверяете:

```powershell
curl.exe -s -o NUL -w "policy=%{http_code}`n" https://dimlernovikden.github.io/Focus-Tracker/
curl.exe -s -o NUL -w "root=%{http_code}`n" https://dimlernovikden.github.io/
curl.exe -sI https://dimlernovikden.github.io/app-ads.txt
```

## Что осталось за человеком

- Юридическая проверка текста политики (черновик составлен по фактическому
  составу приложения: Яндекс Мобильная Реклама, только Android, без аналитики
  и платежей).
- Указать `https://dimlernovikden.github.io/Focus-Tracker/` в Google Play Console,
  RuStore и App Store Connect.
- Пересобрать APK после утверждения политики и проверить кнопку на экране
  «О приложении».
