Адаптация под Яндекс Игры
=========================

Что уже подключено:

1. SDK Яндекс Игр подключён в index.html:
   https://yandex.ru/games/sdk/v2

2. В js/yandex-games.js создан безопасный мост YGBridge.
   Если игра запущена локально и SDK нет — всё работает в локальном режиме.

3. Облачные сохранения:
   - локально игра сохраняется в localStorage;
   - в Яндекс Играх дополнительно сохраняется через player.setData;
   - ключ сохранения: igorek-save.

4. Leaderboard по кубкам:
   - technical name лидерборда: cups;
   - в кабинете Яндекс Игр нужно создать лидерборд с technical name cups;
   - игра отправляет туда количество кубков игрока;
   - если API лидерборда недоступен, показывается тестовый топ.

5. Язык игры:
   - язык берётся через Yandex Games SDK: ysdk.environment.i18n.lang;
   - логика находится в js/yandex-games.js: YGBridge.detectLanguage();
   - игра применяет язык в js/game.js через applyGameLanguage();
   - сейчас поддерживается русский интерфейс, поэтому неподдержанные языки приводятся к ru.

6. LoadingAPI:
   - после инициализации SDK вызывается ysdk.features.LoadingAPI.ready().

7. Rewarded video уже интегрировано в 4 точки игры:
   - главная: x2 монеты на 60 секунд;
   - главная: +50000 монет, сумма умножается от общей статистики;
   - магазин: бесплатный Nikke Box;
   - магазин: бесплатный Card Pack.

   В локальном режиме без SDK награда выдаётся сразу для теста.
   В Яндекс Играх награда выдаётся только через callback onRewarded.

8. В YGBridge есть функции:
   - showFullscreenAd()
   - showRewardedAd(onReward, onClose, onError)

Что нужно сделать в кабинете Яндекс Игр перед релизом:

1. Создать Leaderboard:
   Technical name: cups
   Тип: Numeric / больше — лучше.

2. Проверить, что сохранения игрока разрешены.

3. Проверить rewarded video в черновике Яндекс Игр.

4. Загрузить игру как ZIP/архив с файлами проекта.

5. Если нужны звуки — положить WAV в папку sounds/ по именам из sounds/README.txt.

Важные файлы:
- index.html
- style.css
- js/game.js
- js/yandex-games.js
- data/faq.json
- assets/
- sounds/
