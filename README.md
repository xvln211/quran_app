<!DOCTYPE html>
<html lang="ru">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>القرآن</title>
    <style>
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
            font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
        }

        body {
            background: linear-gradient(135deg, var(--bg-color-1), var(--bg-color-2));
            color: #fff;
            min-height: 100vh;
            perspective: 1000px;
            overflow-x: hidden;
            transition: all 0.8s ease;
        }

        .container {
            max-width: 1200px;
            margin: 0 auto;
            padding: 20px;
            transform-style: preserve-3d;
        }

        header {
            text-align: center;
            margin-bottom: 30px;
            transform: translateZ(20px);
        }

        h1 {
            font-size: 3.5rem;
            margin-bottom: 10px;
            text-shadow: 0 0 10px var(--neon-color), 0 0 20px var(--neon-color), 0 0 30px var(--neon-color);
            color: var(--neon-color);
            transition: all 0.8s ease;
        }

        .surah-info {
            text-align: center;
            margin-bottom: 20px;
            padding: 20px;
            background: rgba(255, 255, 255, 0.05);
            border-radius: 15px;
            border: 1px solid var(--neon-border);
            box-shadow: 0 0 15px var(--neon-glow);
        }

        .surah-name-arabic {
            font-size: 2.2rem;
            color: var(--neon-color);
            margin-bottom: 10px;
            font-family: 'Traditional Arabic', 'Times New Roman', serif;
            text-shadow: 0 0 10px var(--neon-glow);
        }

        .surah-name-russian {
            font-size: 1.3rem;
            color: #d0d0f0;
            margin-bottom: 5px;
        }

        .surah-name-tajik {
            font-size: 1.3rem;
            color: #d0d0f0;
            margin-bottom: 10px;
        }

        .ayah-number {
            font-size: 1.1rem;
            color: #a0a0e0;
            font-style: italic;
        }

        .search-container {
            display: flex;
            justify-content: center;
            margin-bottom: 30px;
            transform: translateZ(30px);
        }

        .search-box {
            display: flex;
            width: 100%;
            max-width: 500px;
            box-shadow: 0 0 15px var(--neon-glow);
            border-radius: 50px;
            overflow: hidden;
            background: rgba(255, 255, 255, 0.1);
            backdrop-filter: blur(10px);
            transition: all 0.8s ease;
        }

        input {
            flex: 1;
            padding: 15px 20px;
            border: none;
            background: transparent;
            color: white;
            font-size: 1.1rem;
            outline: none;
        }

        input::placeholder {
            color: #a0a0e0;
        }

        button {
            padding: 15px 25px;
            background: var(--neon-color);
            border: none;
            color: white;
            cursor: pointer;
            font-size: 1.1rem;
            transition: all 0.3s ease;
        }

        button:hover {
            background: var(--neon-hover);
            box-shadow: 0 0 15px var(--neon-glow);
        }

        .content {
            display: flex;
            flex-wrap: wrap;
            gap: 30px;
            justify-content: center;
            transform-style: preserve-3d;
        }

        .card {
            background: rgba(255, 255, 255, 0.05);
            border-radius: 15px;
            padding: 25px;
            width: 100%;
            max-width: 600px;
            box-shadow: 0 10px 25px rgba(0, 0, 0, 0.3);
            backdrop-filter: blur(10px);
            border: 1px solid var(--neon-border);
            transform: translateZ(10px);
            transition: transform 0.3s ease, box-shadow 0.3s ease;
        }

        .card:hover {
            transform: translateZ(20px);
            box-shadow: 0 15px 35px var(--neon-glow);
        }

        .card-title {
            font-size: 1.5rem;
            margin-bottom: 20px;
            color: var(--neon-color);
            text-align: center;
            border-bottom: 1px solid var(--neon-border);
            padding-bottom: 10px;
            transition: all 0.8s ease;
        }

        .arabic-text {
            font-size: 2rem;
            text-align: right;
            line-height: 1.8;
            margin-bottom: 20px;
            color: #f0f0f0;
            font-family: 'Traditional Arabic', 'Times New Roman', serif;
        }

        .translation {
            font-size: 1.1rem;
            line-height: 1.6;
            margin-bottom: 20px;
            color: #d0d0f0;
        }

        .audio-player {
            width: 100%;
            margin-top: 20px;
            border-radius: 10px;
            overflow: hidden;
        }

        .audio-controls {
            display: flex;
            justify-content: center;
            margin-top: 15px;
        }

        .audio-btn {
            padding: 12px 25px;
            background: var(--btn-bg);
            border: 2px solid var(--neon-color);
            border-radius: 25px;
            color: white;
            cursor: pointer;
            font-size: 1rem;
            transition: all 0.3s ease;
            min-width: 150px;
        }

        .audio-btn:hover {
            background: var(--neon-color);
            box-shadow: 0 0 15px var(--neon-glow);
            transform: translateY(-2px);
        }

        .audio-btn.active {
            background: var(--neon-color);
            box-shadow: 0 0 20px var(--neon-glow);
        }

        .loading {
            text-align: center;
            font-size: 1.2rem;
            color: var(--neon-color);
            margin: 20px 0;
        }

        .error {
            text-align: center;
            font-size: 1.2rem;
            color: #ff6b6b;
            margin: 20px 0;
        }

        .info {
            text-align: center;
            margin-top: 20px;
            color: #a0a0e0;
            font-size: 0.9rem;
        }

        .navigation {
            display: flex;
            justify-content: center;
            gap: 20px;
            margin-top: 30px;
            transform: translateZ(20px);
        }

        .nav-button {
            padding: 12px 25px;
            background: var(--btn-bg);
            border: 2px solid var(--neon-color);
            border-radius: 25px;
            color: white;
            cursor: pointer;
            font-size: 1rem;
            transition: all 0.3s ease;
            min-width: 120px;
        }

        .nav-button:hover {
            background: var(--neon-color);
            box-shadow: 0 0 15px var(--neon-glow);
            transform: translateY(-2px);
        }

        .nav-button:disabled {
            opacity: 0.5;
            cursor: not-allowed;
            transform: none;
        }

        .nav-button:disabled:hover {
            background: var(--btn-bg);
            box-shadow: none;
        }

        @media (max-width: 768px) {
            .content {
                flex-direction: column;
                align-items: center;
            }
            
            .card {
                width: 100%;
            }
            
            h1 {
                font-size: 2.5rem;
            }
            
            .surah-name-arabic {
                font-size: 1.8rem;
            }
            
            .arabic-text {
                font-size: 1.6rem;
            }
            
            .navigation {
                flex-direction: column;
                align-items: center;
            }
            
            .nav-button {
                width: 200px;
            }
            
            .audio-btn {
                width: 200px;
            }
        }
    </style>
</head>
<body>
    <div class="container">
        <header>
            <h1>القرآن</h1>
        </header>
        
        <div class="surah-info">
            <div class="surah-name-arabic" id="surah-name-arabic">سورة الفاتحة</div>
            <div class="surah-name-russian" id="surah-name-russian">Сура Аль-Фатиха</div>
            <div class="surah-name-tajik" id="surah-name-tajik">Сураи Фотиҳа</div>
            <div class="ayah-number" id="ayah-number">Аят 1</div>
        </div>
        
        <div class="search-container">
            <div class="search-box">
                <input type="text" id="search-input" placeholder="Введите номер аята (например: 17:32)">
                <button id="search-button">Поиск</button>
            </div>
        </div>
        
        <div class="content">
            <div class="card">
                <div class="card-title">Арабский текст</div>
                <div id="arabic-text" class="arabic-text"></div>
                <div class="audio-player">
                    <audio id="audio-player" controls style="width: 100%;">
                        Ваш браузер не поддерживает аудио элементы.
                    </audio>
                </div>
                <div class="audio-controls">
                    <button id="repeat-btn" class="audio-btn">🔁 Повторить аят</button>
                </div>
            </div>
            
            <div class="card">
                <div class="card-title">Перевод на русский</div>
                <div id="russian-translation" class="translation"></div>
            </div>
            
            <div class="card">
                <div class="card-title">Перевод на таджикский</div>
                <div id="tajik-translation" class="translation"></div>
            </div>
        </div>
        
        <div class="navigation">
            <button id="prev-button" class="nav-button">← Предыдущий аят</button>
            <button id="next-button" class="nav-button">Следующий аят →</button>
        </div>
        
        <div class="info">
            Для поиска введите номер суры и аята в формате "сура:аят" (например: 1:5)
        </div>
    </div>

    <script>
        document.addEventListener('DOMContentLoaded', function() {
            const searchInput = document.getElementById('search-input');
            const searchButton = document.getElementById('search-button');
            const arabicText = document.getElementById('arabic-text');
            const russianTranslation = document.getElementById('russian-translation');
            const tajikTranslation = document.getElementById('tajik-translation');
            const audioPlayer = document.getElementById('audio-player');
            const prevButton = document.getElementById('prev-button');
            const nextButton = document.getElementById('next-button');
            const repeatBtn = document.getElementById('repeat-btn');
            const surahNameArabic = document.getElementById('surah-name-arabic');
            const surahNameRussian = document.getElementById('surah-name-russian');
            const surahNameTajik = document.getElementById('surah-name-tajik');
            const ayahNumber = document.getElementById('ayah-number');

            let currentSurah = 1;
            let currentAyah = 1;
            let isRepeatMode = false;

            // Полная база данных всех 114 сур Корана на арабском, русском и таджикском
            const surahNames = {
                1: { arabic: "سورة الفاتحة", russian: "Сура Аль-Фатиха", tajik: "Сураи Фотиҳа" },
                2: { arabic: "سورة البقرة", russian: "Сура Аль-Бакара", tajik: "Сураи Бақара" },
                3: { arabic: "سورة آل عمران", russian: "Сура Али Имран", tajik: "Сураи Оли Имрон" },
                4: { arabic: "سورة النساء", russian: "Сура Ан-Ниса", tajik: "Сураи Нисо" },
                5: { arabic: "سورة المائدة", russian: "Сура Аль-Маида", tajik: "Сураи Моида" },
                6: { arabic: "سورة الأنعام", russian: "Сура Аль-Анам", tajik: "Сураи Анъом" },
                7: { arabic: "سورة الأعراف", russian: "Сура Аль-Араф", tajik: "Сураи Аъроф" },
                8: { arabic: "سورة الأنفال", russian: "Сура Аль-Анфаль", tajik: "Сураи Анфол" },
                9: { arabic: "سورة التوبة", russian: "Сура Ат-Тауба", tajik: "Сураи Тавба" },
                10: { arabic: "سورة يونس", russian: "Сура Юнус", tajik: "Сураи Юнус" },
                11: { arabic: "سورة هود", russian: "Сура Худ", tajik: "Сураи Ҳуд" },
                12: { arabic: "سورة يوسف", russian: "Сура Юсуф", tajik: "Сураи Юсуф" },
                13: { arabic: "سورة الرعد", russian: "Сура Ар-Рад", tajik: "Сураи Раъд" },
                14: { arabic: "سورة إبراهيم", russian: "Сура Ибрахим", tajik: "Сураи Иброҳим" },
                15: { arabic: "سورة الحجر", russian: "Сура Аль-Хиджр", tajik: "Сураи Ҳиҷр" },
                16: { arabic: "سورة النحل", russian: "Сура Ан-Нахль", tajik: "Сураи Наҳл" },
                17: { arabic: "سورة الإسراء", russian: "Сура Аль-Исра", tajik: "Сураи Исро" },
                18: { arabic: "سورة الكهف", russian: "Сура Аль-Кахф", tajik: "Сураи Каҳф" },
                19: { arabic: "سورة مريم", russian: "Сура Марьям", tajik: "Сураи Марям" },
                20: { arabic: "سورة طه", russian: "Сура Та Ха", tajik: "Сураи То Ҳо" },
                21: { arabic: "سورة الأنبياء", russian: "Сура Аль-Анбия", tajik: "Сураи Анбиё" },
                22: { arabic: "سورة الحج", russian: "Сура Аль-Хадж", tajik: "Сураи Ҳаҷ" },
                23: { arabic: "سورة المؤمنون", russian: "Сура Аль-Муминун", tajik: "Сураи Муминун" },
                24: { arabic: "سورة النور", russian: "Сура Ан-Нур", tajik: "Сураи Нур" },
                25: { arabic: "سورة الفرقان", russian: "Сура Аль-Фуркан", tajik: "Сураи Фурқон" },
                26: { arabic: "سورة الشعراء", russian: "Сура Аш-Шуара", tajik: "Сураи Шуаро" },
                27: { arabic: "سورة النمل", russian: "Сура Ан-Намль", tajik: "Сураи Намл" },
                28: { arabic: "سورة القصص", russian: "Сура Аль-Касас", tajik: "Сураи Қасас" },
                29: { arabic: "سورة العنكبوت", russian: "Сура Аль-Анкабут", tajik: "Сураи Анкабут" },
                30: { arabic: "سورة الروم", russian: "Сура Ар-Рум", tajik: "Сураи Рум" },
                31: { arabic: "سورة لقمان", russian: "Сура Лукман", tajik: "Сураи Луқмон" },
                32: { arabic: "سورة السجدة", russian: "Сура Ас-Саджда", tajik: "Сураи Саҷда" },
                33: { arabic: "سورة الأحزاب", russian: "Сура Аль-Ахзаб", tajik: "Сураи Аҳзоб" },
                34: { arabic: "سورة سبأ", russian: "Сура Саба", tajik: "Сураи Саба" },
                35: { arabic: "سورة فاطر", russian: "Сура Фатыр", tajik: "Сураи Фотир" },
                36: { arabic: "سورة يس", russian: "Сура Йа Син", tajik: "Сураи Ясин" },
                37: { arabic: "سورة الصافات", russian: "Сура Ас-Саффат", tajik: "Сураи Соффат" },
                38: { arabic: "سورة ص", russian: "Сура Сад", tajik: "Сураи Сод" },
                39: { arabic: "سورة الزمر", russian: "Сура Аз-Зумар", tajik: "Сураи Зумар" },
                40: { arabic: "سورة غافر", russian: "Сура Гафир", tajik: "Сураи Ғофир" },
                41: { arabic: "سورة فصلت", russian: "Сура Фуссилят", tajik: "Сураи Фуссилат" },
                42: { arabic: "سورة الشورى", russian: "Сура Аш-Шура", tajik: "Сураи Шуро" },
                43: { arabic: "سورة الزخرف", russian: "Сура Аз-Зухруф", tajik: "Сураи Зухруф" },
                44: { arabic: "سورة الدخان", russian: "Сура Ад-Духан", tajik: "Сураи Духон" },
                45: { arabic: "سورة الجاثية", russian: "Сура Аль-Джасия", tajik: "Сураи Ҷосия" },
                46: { arabic: "سورة الأحقاف", russian: "Сура Аль-Ахкаф", tajik: "Сураи Аҳқоф" },
                47: { arabic: "سورة محمد", russian: "Сура Мухаммад", tajik: "Сураи Муҳаммад" },
                48: { arabic: "سورة الفتح", russian: "Сура Аль-Фатх", tajik: "Сураи Фатҳ" },
                49: { arabic: "سورة الحجرات", russian: "Сура Аль-Худжурат", tajik: "Сураи Ҳуҷурот" },
                50: { arabic: "سورة ق", russian: "Сура Каф", tajik: "Сураи Қоф" },
                51: { arabic: "سورة الذاريات", russian: "Сура Аз-Зарият", tajik: "Сураи Зориёт" },
                52: { arabic: "سورة الطور", russian: "Сура Ат-Тур", tajik: "Сураи Тур" },
                53: { arabic: "سورة النجم", russian: "Сура Ан-Наджм", tajik: "Сураи Наҷм" },
                54: { arabic: "سورة القمر", russian: "Сура Аль-Камар", tajik: "Сураи Қамар" },
                55: { arabic: "سورة الرحمن", russian: "Сура Ар-Рахман", tajik: "Сураи Раҳмон" },
                56: { arabic: "سورة الواقعة", russian: "Сура Аль-Вакиа", tajik: "Сураи Воқеа" },
                57: { arabic: "سورة الحديد", russian: "Сура Аль-Хадид", tajik: "Сураи Ҳадид" },
                58: { arabic: "سورة المجادلة", russian: "Сура Аль-Муджадиля", tajik: "Сураи Муҷодала" },
                59: { arabic: "سورة الحشر", russian: "Сура Аль-Хашр", tajik: "Сураи Ҳашр" },
                60: { arabic: "سورة الممتحنة", russian: "Сура Аль-Мумтахана", tajik: "Сураи Мумтаҳана" },
                61: { arabic: "سورة الصف", russian: "Сура Ас-Сафф", tajik: "Сураи Сафф" },
                62: { arabic: "سورة الجمعة", russian: "Сура Аль-Джумуа", tajik: "Сураи Ҷумъа" },
                63: { arabic: "سورة المنافقون", russian: "Сура Аль-Мунафикун", tajik: "Сураи Мунофиқун" },
                64: { arabic: "سورة التغابن", russian: "Сура Ат-Тагабун", tajik: "Сураи Тағобун" },
                65: { arabic: "سورة الطلاق", russian: "Сура Ат-Таляк", tajik: "Сураи Талоқ" },
                66: { arabic: "سورة التحريم", russian: "Сура Ат-Тахрим", tajik: "Сураи Таҳрим" },
                67: { arabic: "سورة الملك", russian: "Сура Аль-Мульк", tajik: "Сураи Мулк" },
                68: { arabic: "سورة القلم", russian: "Сура Аль-Калям", tajik: "Сураи Қалам" },
                69: { arabic: "سورة الحاقة", russian: "Сура Аль-Хакка", tajik: "Сураи Ҳоққа" },
                70: { arabic: "سورة المعارج", russian: "Сура Аль-Мааридж", tajik: "Сураи Маориҷ" },
                71: { arabic: "سورة نوح", russian: "Сура Нух", tajik: "Сураи Нуҳ" },
                72: { arabic: "سورة الجن", russian: "Сура Аль-Джинн", tajik: "Сураи Ҷин" },
                73: { arabic: "سورة المزمل", russian: "Сура Аль-Муззаммиль", tajik: "Сураи Муззаммил" },
                74: { arabic: "سورة المدثر", russian: "Сура Аль-Муддассир", tajik: "Сураи Муддассир" },
                75: { arabic: "سورة القيامة", russian: "Сура Аль-Кийама", tajik: "Сураи Қиёмат" },
                76: { arabic: "سورة الإنسان", russian: "Сура Аль-Инсан", tajik: "Сураи Инсон" },
                77: { arabic: "سورة المرسلات", russian: "Сура Аль-Мурсалят", tajik: "Сураи Мурсалот" },
                78: { arabic: "سورة النبأ", russian: "Сура Ан-Наба", tajik: "Сураи Наба" },
                79: { arabic: "سورة النازعات", russian: "Сура Ан-Назиат", tajik: "Сураи Нозиот" },
                80: { arabic: "سورة عبس", russian: "Сура Абаса", tajik: "Сураи Абаса" },
                81: { arabic: "سورة التكوير", russian: "Сура Ат-Таквир", tajik: "Сураи Таквир" },
                82: { arabic: "سورة الانفطار", russian: "Сура Аль-Инфитар", tajik: "Сураи Инфитор" },
                83: { arabic: "سورة المطففين", russian: "Сура Аль-Мутаффифин", tajik: "Сураи Мутаффифин" },
                84: { arabic: "سورة الانشقاق", russian: "Сура Аль-Иншикак", tajik: "Сураи Иншиқоқ" },
                85: { arabic: "سورة البروج", russian: "Сура Аль-Бурудж", tajik: "Сураи Бурӯҷ" },
                86: { arabic: "سورة الطارق", russian: "Сура Ат-Тарик", tajik: "Сураи Ториқ" },
                87: { arabic: "سورة الأعلى", russian: "Сура Аль-Аля", tajik: "Сураи Аъло" },
                88: { arabic: "سورة الغاشية", russian: "Сура Аль-Гашия", tajik: "Сураи Ғошия" },
                89: { arabic: "سورة الفجر", russian: "Сура Аль-Фаджр", tajik: "Сураи Фаҷр" },
                90: { arabic: "سورة البلد", russian: "Сура Аль-Баляд", tajik: "Сураи Баляд" },
                91: { arabic: "سورة الشمس", russian: "Сура Аш-Шамс", tajik: "Сураи Шамс" },
                92: { arabic: "سورة الليل", russian: "Сура Аль-Ляйль", tajik: "Сураи Лайл" },
                93: { arabic: "سورة الضحى", russian: "Сура Ад-Духа", tajik: "Сураи Зуҳо" },
                94: { arabic: "سورة الشرح", russian: "Сура Аш-Шарх", tajik: "Сураи Шарҳ" },
                95: { arabic: "سورة التين", russian: "Сура Ат-Тин", tajik: "Сураи Тин" },
                96: { arabic: "سورة العلق", russian: "Сура Аль-Аляк", tajik: "Сураи Алақ" },
                97: { arabic: "سورة القدر", russian: "Сура Аль-Кадр", tajik: "Сураи Қадр" },
                98: { arabic: "سورة البينة", russian: "Сура Аль-Баййина", tajik: "Сураи Байина" },
                99: { arabic: "سورة الزلزلة", russian: "Сура Аз-Зальзаля", tajik: "Сураи Зилзол" },
                100: { arabic: "سورة العاديات", russian: "Сура Аль-Адия", tajik: "Сураи Одиёт" },
                101: { arabic: "سورة القارعة", russian: "Сура Аль-Кариа", tajik: "Сураи Қориа" },
                102: { arabic: "سورة التكاثر", russian: "Сура Ат-Такасур", tajik: "Сураи Такасур" },
                103: { arabic: "سورة العصر", russian: "Сура Аль-Аср", tajik: "Сураи Аср" },
                104: { arabic: "سورة الهمزة", russian: "Сура Аль-Хумаза", tajik: "Сураи Ҳумаза" },
                105: { arabic: "سورة الفيل", russian: "Сура Аль-Филь", tajik: "Сураи Фил" },
                106: { arabic: "سورة قريش", russian: "Сура Курайш", tajik: "Сураи Қурайш" },
                107: { arabic: "سورة الماعون", russian: "Сура Аль-Маун", tajik: "Сураи Маъун" },
                108: { arabic: "سورة الكوثر", russian: "Сура Аль-Каусар", tajik: "Сураи Кавсар" },
                109: { arabic: "سورة الكافرون", russian: "Сура Аль-Кафирун", tajik: "Сураи Кофирун" },
                110: { arabic: "سورة النصر", russian: "Сура Ан-Наср", tajik: "Сураи Наср" },
                111: { arabic: "سورة المسد", russian: "Сура Аль-Масад", tajik: "Сураи Масад" },
                112: { arabic: "سورة الإخلاص", russian: "Сура Аль-Ихлас", tajik: "Сураи Ихлос" },
                113: { arabic: "سورة الفلق", russian: "Сура Аль-Фаляк", tajik: "Сураи Фалақ" },
                114: { arabic: "سورة الناس", russian: "Сура Ан-Нас", tajik: "Сураи Нас" }
            };

            // Функция для обновления информации о суре
            function updateSurahInfo(surah, ayah) {
                const surahInfo = surahNames[surah];
                if (surahInfo) {
                    surahNameArabic.textContent = surahInfo.arabic;
                    surahNameRussian.textContent = surahInfo.russian;
                    surahNameTajik.textContent = surahInfo.tajik;
                } else {
                    surahNameArabic.textContent = `سورة ${surah}`;
                    surahNameRussian.textContent = `Сура ${surah}`;
                    surahNameTajik.textContent = `Сураи ${surah}`;
                }
                ayahNumber.textContent = `Аят ${ayah}`;
            }

            // Палитра неоновых цветов для каждого аята
            const neonColors = [
                // Синие оттенки
                {
                    neon: '#00a8ff',
                    hover: '#0097e6',
                    glow: 'rgba(0, 168, 255, 0.7)',
                    border: 'rgba(0, 168, 255, 0.3)',
                    bg1: '#0c0c2e',
                    bg2: '#1a1a3e',
                    btnBg: 'rgba(0, 168, 255, 0.2)'
                },
                // Фиолетовые оттенки
                {
                    neon: '#9c27b0',
                    hover: '#8e24aa',
                    glow: 'rgba(156, 39, 176, 0.7)',
                    border: 'rgba(156, 39, 176, 0.3)',
                    bg1: '#1a0b2e',
                    bg2: '#2d1b3e',
                    btnBg: 'rgba(156, 39, 176, 0.2)'
                },
                // Зеленые оттенки
                {
                    neon: '#4caf50',
                    hover: '#45a049',
                    glow: 'rgba(76, 175, 80, 0.7)',
                    border: 'rgba(76, 175, 80, 0.3)',
                    bg1: '#0c2e0c',
                    bg2: '#1a3e1a',
                    btnBg: 'rgba(76, 175, 80, 0.2)'
                },
                // Розовые оттенки
                {
                    neon: '#e91e63',
                    hover: '#d81b60',
                    glow: 'rgba(233, 30, 99, 0.7)',
                    border: 'rgba(233, 30, 99, 0.3)',
                    bg1: '#2e0c1a',
                    bg2: '#3e1a2a',
                    btnBg: 'rgba(233, 30, 99, 0.2)'
                },
                // Оранжевые оттенки
                {
                    neon: '#ff9800',
                    hover: '#f57c00',
                    glow: 'rgba(255, 152, 0, 0.7)',
                    border: 'rgba(255, 152, 0, 0.3)',
                    bg1: '#2e1c0c',
                    bg2: '#3e2a1a',
                    btnBg: 'rgba(255, 152, 0, 0.2)'
                },
                // Бирюзовые оттенки
                {
                    neon: '#00bcd4',
                    hover: '#00acc1',
                    glow: 'rgba(0, 188, 212, 0.7)',
                    border: 'rgba(0, 188, 212, 0.3)',
                    bg1: '#0c2e2e',
                    bg2: '#1a3e3e',
                    btnBg: 'rgba(0, 188, 212, 0.2)'
                },
                // Желтые оттенки
                {
                    neon: '#ffeb3b',
                    hover: '#fdd835',
                    glow: 'rgba(255, 235, 59, 0.7)',
                    border: 'rgba(255, 235, 59, 0.3)',
                    bg1: '#2e2e0c',
                    bg2: '#3e3e1a',
                    btnBg: 'rgba(255, 235, 59, 0.2)'
                },
                // Красные оттенки
                {
                    neon: '#f44336',
                    hover: '#e53935',
                    glow: 'rgba(244, 67, 54, 0.7)',
                    border: 'rgba(244, 67, 54, 0.3)',
                    bg1: '#2e0c0c',
                    bg2: '#3e1a1a',
                    btnBg: 'rgba(244, 67, 54, 0.2)'
                }
            ];

            // Функция для получения цвета на основе номера аята
            function getColorForAyah(surah, ayah) {
                const index = (surah + ayah) % neonColors.length;
                return neonColors[index];
            }

            // Функция для применения цветовой схемы
            function applyColorScheme(colorScheme) {
                const root = document.documentElement;
                root.style.setProperty('--neon-color', colorScheme.neon);
                root.style.setProperty('--neon-hover', colorScheme.hover);
                root.style.setProperty('--neon-glow', colorScheme.glow);
                root.style.setProperty('--neon-border', colorScheme.border);
                root.style.setProperty('--bg-color-1', colorScheme.bg1);
                root.style.setProperty('--bg-color-2', colorScheme.bg2);
                root.style.setProperty('--btn-bg', colorScheme.btnBg);
            }

            // Информация о количестве аятов в сурах (полная база для всех 114 сур)
            const surahInfo = {
                1: 7, 2: 286, 3: 200, 4: 176, 5: 120, 6: 165, 7: 206, 8: 75, 9: 129, 10: 109,
                11: 123, 12: 111, 13: 43, 14: 52, 15: 99, 16: 128, 17: 111, 18: 110, 19: 98, 20: 135,
                21: 112, 22: 78, 23: 118, 24: 64, 25: 77, 26: 227, 27: 93, 28: 88, 29: 69, 30: 60,
                31: 34, 32: 30, 33: 73, 34: 54, 35: 45, 36: 83, 37: 182, 38: 88, 39: 75, 40: 85,
                41: 54, 42: 53, 43: 89, 44: 59, 45: 37, 46: 35, 47: 38, 48: 29, 49: 18, 50: 45,
                51: 60, 52: 49, 53: 62, 54: 55, 55: 78, 56: 96, 57: 29, 58: 22, 59: 24, 60: 13,
                61: 14, 62: 11, 63: 11, 64: 18, 65: 12, 66: 12, 67: 30, 68: 52, 69: 52, 70: 44,
                71: 28, 72: 28, 73: 20, 74: 56, 75: 40, 76: 31, 77: 50, 78: 40, 79: 46, 80: 42,
                81: 29, 82: 19, 83: 36, 84: 25, 85: 22, 86: 17, 87: 19, 88: 26, 89: 30, 90: 20,
                91: 15, 92: 21, 93: 11, 94: 8, 95: 8, 96: 19, 97: 5, 98: 8, 99: 8, 100: 11,
                101: 11, 102: 8, 103: 3, 104: 9, 105: 5, 106: 4, 107: 7, 108: 3, 109: 6, 110: 3,
                111: 5, 112: 4, 113: 5, 114: 6
            };

            // Функция для получения идентификатора таджикского перевода
            async function getTajikEdition() {
                try {
                    const response = await fetch('https://api.alquran.cloud/v1/edition/language/tg');
                    const data = await response.json();
                    
                    if (data.data && data.data.length > 0) {
                        return data.data[0].identifier;
                    } else {
                        return 'en.asad';
                    }
                } catch (error) {
                    console.error('Ошибка получения таджикского перевода:', error);
                    return 'en.asad';
                }
            }

            // Функция для обновления состояния кнопок навигации
            function updateNavigationButtons() {
                prevButton.disabled = currentSurah === 1 && currentAyah === 1;
                const maxAyahs = surahInfo[currentSurah] || 286;
                nextButton.disabled = currentAyah >= maxAyahs && currentSurah >= 114;
            }

            // Функция для загрузки данных аята
            async function loadAyah(surah, ayah) {
                try {
                    // Обновляем информацию о суре
                    updateSurahInfo(surah, ayah);
                    
                    // Применяем цветовую схему для этого аята
                    const colorScheme = getColorForAyah(surah, ayah);
                    applyColorScheme(colorScheme);
                    
                    // Показать состояние загрузки
                    arabicText.innerHTML = '<div class="loading">Загрузка арабского текста...</div>';
                    russianTranslation.innerHTML = '<div class="loading">Загрузка перевода на русский...</div>';
                    tajikTranslation.innerHTML = '<div class="loading">Загрузка перевода на таджикский...</div>';
                    
                    // Обновляем текущие значения
                    currentSurah = surah;
                    currentAyah = ayah;
                    
                    // Обновляем состояние кнопок
                    updateNavigationButtons();
                    
                    // Загрузка арабского текста и аудио от alafasy
                    const arabicResponse = await fetch(`https://api.alquran.cloud/v1/ayah/${surah}:${ayah}/ar.alafasy`);
                    const arabicData = await arabicResponse.json();
                    
                    if (arabicData.code === 200) {
                        arabicText.textContent = arabicData.data.text;
                        audioPlayer.src = arabicData.data.audio;
                        
                        setTimeout(() => {
                            audioPlayer.play().catch(e => console.log('Автовоспроизведение заблокировано'));
                        }, 500);
                    } else {
                        arabicText.innerHTML = '<div class="error">Ошибка загрузки арабского текста</div>';
                    }
                    
                    // Загрузка перевода на русский
                    const russianResponse = await fetch(`https://api.alquran.cloud/v1/ayah/${surah}:${ayah}/ru.kuliev`);
                    const russianData = await russianResponse.json();
                    
                    if (russianData.code === 200) {
                        russianTranslation.textContent = russianData.data.text;
                    } else {
                        russianTranslation.innerHTML = '<div class="error">Ошибка загрузки перевода на русский</div>';
                    }
                    
                    // Получаем идентификатор таджикского перевода и загружаем его
                    const tajikEdition = await getTajikEdition();
                    const tajikResponse = await fetch(`https://api.alquran.cloud/v1/ayah/${surah}:${ayah}/${tajikEdition}`);
                    const tajikData = await tajikResponse.json();
                    
                    if (tajikData.code === 200) {
                        tajikTranslation.textContent = tajikData.data.text;
                    } else {
                        tajikTranslation.innerHTML = '<div class="error">Ошибка загрузки перевода на таджикский</div>';
                    }
                    
                } catch (error) {
                    console.error('Ошибка загрузки данных:', error);
                    arabicText.innerHTML = '<div class="error">Ошибка загрузки данных. Проверьте подключение к интернету.</div>';
                    russianTranslation.innerHTML = '';
                    tajikTranslation.innerHTML = '';
                }
            }

            // Функция для перехода к предыдущему аяту
            function goToPreviousAyah() {
                if (currentAyah > 1) {
                    loadAyah(currentSurah, currentAyah - 1);
                } else if (currentSurah > 1) {
                    const prevSurah = currentSurah - 1;
                    const prevSurahAyahs = surahInfo[prevSurah] || 286;
                    loadAyah(prevSurah, prevSurahAyahs);
                }
            }

            // Функция для перехода к следующему аяту
            function goToNextAyah() {
                const maxAyahs = surahInfo[currentSurah] || 286;
                
                if (currentAyah < maxAyahs) {
                    loadAyah(currentSurah, currentAyah + 1);
                } else if (currentSurah < 114) {
                    loadAyah(currentSurah + 1, 1);
                }
            }

            // Обработчик окончания воспроизведения аудио
            audioPlayer.addEventListener('ended', function() {
                if (isRepeatMode) {
                    audioPlayer.currentTime = 0;
                    audioPlayer.play();
                }
            });

            // Обработчик кнопки повтора
            repeatBtn.addEventListener('click', function() {
                isRepeatMode = !isRepeatMode;
                repeatBtn.classList.toggle('active', isRepeatMode);
                repeatBtn.innerHTML = isRepeatMode ? '🔁 Повтор включен' : '🔁 Повторить аят';
                
                if (isRepeatMode) {
                    audioPlayer.currentTime = 0;
                    audioPlayer.play();
                }
            });

            // Обработчик нажатия кнопки поиска
            searchButton.addEventListener('click', function() {
                const input = searchInput.value.trim();
                if (input) {
                    const parts = input.split(':');
                    if (parts.length === 2) {
                        const surah = parseInt(parts[0]);
                        const ayah = parseInt(parts[1]);
                        
                        if (!isNaN(surah) && !isNaN(ayah) && surah > 0 && ayah > 0) {
                            loadAyah(surah, ayah);
                        } else {
                            alert('Пожалуйста, введите корректный номер суры и аята (например: 17:32)');
                        }
                    } else {
                        alert('Пожалуйста, используйте формат "сура:аят" (например: 17:32)');
                    }
                } else {
                    alert('Пожалуйста, введите номер аята для поиска');
                }
            });

            // Обработчик нажатия Enter в поле ввода
            searchInput.addEventListener('keypress', function(e) {
                if (e.key === 'Enter') {
                    searchButton.click();
                }
            });

            // Обработчики для кнопок навигации
            prevButton.addEventListener('click', goToPreviousAyah);
            nextButton.addEventListener('click', goToNextAyah);

            // Загрузить пример аята при загрузке страницы
            loadAyah(1, 1);
        });
    </script>
</body>
</html>
