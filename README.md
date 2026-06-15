# lab-perevalova-6sns-stomatology-clinics-2026

Песочница: **https://perevalova-6sns-stomatology-clinics-2026.lab.6-sense.pro/**

Рейтинг стоматологий Москвы 2026: выручка, отзывы на картах, цены с сайтов.

## Source of truth

Рабочий файл в workspace: `../dashboard_stomatology_V2.html`  
Сборка данных: `../build_dashboard_stageB.py` → `patch_dashboard_data()`

## Деплой

```powershell
cd "d:\Incoming\Cursor\Dashboards\Stomatology_clinics"
.\deploy\sync_lab_public.ps1
cd deploy\lab-perevalova-6sns-stomatology-clinics-2026
git add public/
git -c user.name="NP-6Sns" -c user.email="perevalova@6-sense.pro" commit -m "Deploy: stomatology dashboard"
git push origin main
```

Push в `main` → GitHub Actions → lab-сервер (~15 с).

Подробно: `STOMATOLOGY_DEPLOY.md` в корне workspace.
