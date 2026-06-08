# QuranApp-audio

Отдельный репозиторий для MP3 и манифеста прослушивания. **Не смешивать с QuranAppWebsite** (лендинг на GitHub Pages).

## Структура

```
QuranApp-audio/
  listening-manifest.v2.json   # манифест (обновляется скриптом из QuranApp)
  tafsir_saadi/
    001.mp3
    048.mp3
    002_001-011.mp3
    ...
  translation/                 # опционально, для будущего CDN перевода
    001.mp3
```

## Первичная настройка

1. Создайте публичный репозиторий `QuranApp-audio` на GitHub.
2. Скопируйте MP3 из локального архива тафсира в `tafsir_saadi/`.
3. В корне QuranApp сгенерируйте манифест:

```bash
npm run build:listening-manifest -- --from-dir "C:/path/to/tafsir_saadi"
```

Или без архива (CDN URL для всех 114 сур, файлы должны быть в репо):

```bash
npm run build:listening-manifest -- --fill-cdn-gaps
```

4. Скопируйте содержимое папки `audio-repo/` (манифест + `tafsir_saadi/`) в новый репо.
5. Закоммитьте, запушьте, создайте тег:

```bash
git tag v1.0.0
git push origin v1.0.0
```

## URL после публикации

- Манифест: `https://cdn.jsdelivr.net/gh/mansurkhatuev-coder/QuranApp-audio@v1.0.0/listening-manifest.v2.json`
- Аудио: `https://cdn.jsdelivr.net/gh/mansurkhatuev-coder/QuranApp-audio@v1.0.0/tafsir_saadi/048.mp3`

Обновление: новый тег (`v1.0.1`) + обновить `LISTENING_AUDIO_GITHUB_TAG` в `constants/listening-audio.ts`.

## Офлайн-пак (этап 2)

Позже: GitHub Release `tafsir_saadi-v1.zip` для скачивания в настройках приложения.

## Лимиты

- Рекомендуемый размер репо до ~1 GB.
- Файлы до 100 MB каждый.
- Не использовать Git LFS для стриминга (лимит bandwidth на free).
