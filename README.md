# new-project

Навчальний репозиторій для завдання **PROM-42164**: створення Git-репозиторію, робота в гілці `development` та об'єднання змін у `main`.

## Передумови

Встановіть Git і GitHub CLI (`gh`), увійдіть у свій обліковий запис:

```bash
gh auth login
```

Перевірте ім'я та email автора комітів:

```bash
git config user.name
git config user.email
```

Якщо вони не задані, налаштуйте свої значення через `git config --global user.name` та `git config --global user.email`.

## Покрокова інструкція

Виконуйте ці кроки для нового проєкту, у каталозі, де ще немає `new-project`.

### 1. Створіть каталог

```bash
mkdir new-project
```

### 2. Перейдіть у нього

```bash
cd new-project
```

### 3. Ініціалізуйте Git з основною гілкою main

```bash
git init -b main
```

Локальний Git-репозиторій не має налаштування public/private. Публічність задається на GitHub під час публікації нижче.

### 4. Створіть README з початковим текстом

```bash
printf '# new-project\n\nНавчальний репозиторій для завдання PROM-42164.\n' > README.md
```

### 5. Додайте файл до staging area

```bash
git add README.md
```

### 6. Створіть початковий коміт

```bash
git commit -m "init"
```

### 7. Створіть development та перейдіть до неї

```bash
git switch -c development
git branch --show-current
```

Остання команда повинна вивести `development`.

### 8. Додайте інструкцію до README

Відкрийте `README.md` у текстовому редакторі та додайте покрокову інструкцію зі створення репозиторію, комітів, гілок, злиття й публікації (як у цьому файлі). Збережіть файл, перевірте зміни та підготуйте їх до коміту:

```bash
git diff -- README.md
git add README.md
```

### 9. Зробіть Smart Commit

```bash
git commit -m "PROM-42164 #comment Add step-by-step Git repository and development branch instructions"
```

Формат: `ISSUE_KEY #comment текст коментаря`. Це коректний синтаксис Smart Commit. Для фактичного додавання коментаря до Jira потрібні інтеграція GitHub із Jira, увімкнені Smart Commits, відповідні права та email автора коміту, що відповідає користувачу Jira. Сам Git-коміт працює і без інтеграції.

Документація: [Atlassian Smart Commit commands](https://support.atlassian.com/jira-software-cloud/docs/process-issues-with-smart-commits/#Smart-Commit-commands).

### 10. Об'єднайте development у main

```bash
git switch main
git merge --no-ff --no-commit development
```

`--no-ff` забезпечує окремий merge-коміт, а `--no-commit` дозволяє перевірити результат перед його створенням.

### 11. Перевірте результат перед фінальним комітом

```bash
git status
git diff --cached --check
git diff --cached -- README.md
```

На цьому етапі злиття підготовлено, але ще не закомічено. Переконайтеся, що немає конфліктів і README містить інструкцію.

### 12. Закомітьте злиття та перевірте чистоту робочого каталогу

```bash
git commit -m "Merge development into main for PROM-42164"
git status
git log --oneline --graph --all
```

Очікуваний фінальний статус: `nothing to commit, working tree clean`.

## Публікація на GitHub

Створіть новий **публічний** репозиторій у своєму акаунті та відправте обидві гілки:

```bash
gh repo create new-project --public --source=. --remote=origin --push
git push -u origin development
git fetch origin
git status -sb
git branch -vv
```

Назва `new-project` повинна бути вільною у вашому GitHub-акаунті. Основна гілка — `main`; гілка `development` залишається доступною після злиття.

Для перевірки синхронізації такі команди мають завершитися без виводу:

```bash
git diff main origin/main
git diff development origin/development
```

## Результат для здачі

Після успішної публікації відкрийте `README.md` у гілці `main` на GitHub та скопіюйте адресу:

```text
https://github.com/<your-github-login>/new-project/blob/main/README.md
```

Саме це посилання потрібно вставити у відповідь на завдання Prometheus.
