# lab-perevalova-6sns-stomatology-clinics-2026

Песочница (после настройки infra):  
**https://perevalova-6sns-stomatology-clinics-2026.lab.6-sense.pro/**

Рейтинг стоматологий Москвы 2026: выручка, отзывы на картах, цены с сайтов.

## Source of truth

- `Stomatology_clinics/dashboard_stomatology_V2.html`
- Сборка данных: `build_dashboard_stageB.py` → `patch_dashboard_data()`
- Деплой: `dashboard_stomatology_V2.html` + `assets/` → `public/` → push `main`

Обновление перед push:

```powershell
cd "d:\Incoming\Cursor\Dashboards\Stomatology_clinics"
python apply_manual_price_corrections.py
python -c "from pathlib import Path; import pandas as pd; from build_dashboard_stageB import prepare_frame, build_payload, patch_dashboard_data, SOURCE_XLSX; df=prepare_frame(pd.read_excel(SOURCE_XLSX, header=2)); patch_dashboard_data(Path('dashboard_stomatology_V2.html'), build_payload(df))"
Copy-Item dashboard_stomatology_V2.html deploy\lab-perevalova-6sns-stomatology-clinics-2026\public\index.html -Force
Copy-Item assets\* deploy\lab-perevalova-6sns-stomatology-clinics-2026\public\assets\ -Force
# В index.html для песочницы: canonical/og:url → lab.6-sense.pro (см. скрипт в deploy/)
```

## Настройка (один раз, владелец org / infra)

1. `lab-add-project.sh <login> perevalova-6sns-stomatology-clinics-2026` (как для yt-analytics).
2. Создать в org `NP-6Sns` репозиторий из `lab-template` с этим именем.
3. Secrets (как у yt-analytics-04-2026, другой `DEPLOY_PATH`):
   - `DEPLOY_SSH_KEY`, `DEPLOY_HOST`, `DEPLOY_USER`
   - `DEPLOY_PATH` → `/home/lab_<login>/sites/perevalova-6sns-stomatology-clinics-2026/public/`

Без шага 1 URL с этим именем **не появится** — это не настраивается только из git.
