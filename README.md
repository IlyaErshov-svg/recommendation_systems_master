# Настройка окружения для аналитики данных с Conda

Это руководство поможет вам настроить базовое окружение для аналитики данных в Jupyter Notebook с использованием Conda.

## Шаг 1: Установка Miniconda

Miniconda - это легковесная версия Anaconda, которая включает в себя Conda, Python и необходимые пакеты.

### Установка через Homebrew (для macOS)
```bash
brew install --cask miniconda
```

### Инициализация Conda
После установки необходимо инициализировать Conda для вашей оболочки:
```bash
conda init "$(basename "${SHELL}")"
```

### Перезапуск оболочки
Для применения изменений закройте и откройте терминал заново или выполните:
```bash
source ~/.zshrc  # для zsh
# или
source ~/.bashrc  # для bash
```

### Проверка установки
```bash
conda --version
```

### Принятие условий использования (Terms of Service)
При первом использовании conda необходимо принять условия использования для каналов Anaconda:
```bash
conda tos accept --override-channels --channel https://repo.anaconda.com/pkgs/main
conda tos accept --override-channels --channel https://repo.anaconda.com/pkgs/r
```

## Шаг 2: Создание окружения для аналитики данных

Создаем новое окружение с Python 3.11:
```bash
conda create -n data_analysis python=3.11 -y
```

## Шаг 3: Установка необходимых пакетов

Активируем окружение:
```bash
conda activate data_analysis
```

Устанавливаем основные пакеты для аналитики данных:
```bash
conda install pandas numpy matplotlib seaborn jupyter -y
```

Дополнительные полезные пакеты:
```bash
conda install scikit-learn plotly dash -y
```

## Шаг 4: Запуск Jupyter Notebook

### Вариант 1: Запуск в браузере
После активации окружения запускаем Jupyter:
```bash
jupyter notebook
```

### Вариант 2: Работа в VS Code (рекомендуется)
VS Code имеет встроенную поддержку Jupyter ноутбуков:

1. Установите необходимые расширения VS Code:
   - Python
   - Jupyter

2. Выберите правильное окружение:
   - Откройте палитру команд (Cmd+Shift+P)
   - Выберите "Python: Select Interpreter"
   - Укажите путь к окружению data_analysis

   Чтобы найти точный путь к Python в вашем окружении, выполните в терминале:
   ```bash
   conda activate data_analysis
   which python
   ```
   
   В вашем случае путь: `/opt/homebrew/Caskroom/miniconda/base/envs/data_analysis/bin/python`

3. Откройте `.ipynb` файл в VS Code и работайте с ним напрямую

Преимущества работы в VS Code:
- Интеграция с Git
- Удобный отладчик
- Автодополнение кода
- Встроенный терминал
- Поддержка множества расширений

## Шаг 5: Проверка работы окружения

Создайте новый ноутбук и выполните следующий код для проверки:

```python
import pandas as pd
import numpy as np
import matplotlib.pyplot as plt
import seaborn as sns

print("Версия pandas:", pd.__version__)
print("Версия numpy:", np.__version__)
print("Версия matplotlib:", plt.matplotlib.__version__)
print("Версия seaborn:", sns.__version__)

# Создаем тестовые данные
data = pd.DataFrame({
    'x': np.random.randn(100),
    'y': np.random.randn(100)
})

# Строим простой график
plt.figure(figsize=(10, 6))
plt.scatter(data['x'], data['y'])
plt.title('Тестовый график')
plt.show()
```

## Полезные команды Conda

### Управление окружениями
- Список всех окружений: `conda env list`
- Активация окружения: `conda activate data_analysis`
- Деактивация окружения: `conda deactivate`
- Удаление окружения: `conda env remove -n data_analysis`

### Управление пакетами
- Список установленных пакетов: `conda list`
- Установка пакета: `conda install package_name`
- Обновление пакета: `conda update package_name`
- Удаление пакета: `conda remove package_name`

### Экспорт и импорт окружений
- Экспорт окружения в файл: `conda env export > environment.yml`
- Создание окружения из файла: `conda env create -f environment.yml`

## Рекомендации

1. Всегда создавайте отдельное окружение для каждого проекта
2. Используйте `conda env export` для сохранения зависимостей проекта
3. Регулярно обновляйте пакеты для получения последних исправлений и улучшений
4. Для сложных проектов рассмотрите использование `requirements.txt` вместе с `environment.yml`

## Шаг 6: Настройка Git и связь с GitHub

### Инициализация Git репозитория
```bash
git init
```

### Настройка пользователя Git (если еще не настроено)
```bash
git config --global user.name "Ваше имя"
git config --global user.email "ваш.email@example.com"
```

### Связывание с удаленным репозиторием GitHub
1. Создайте пустой репозиторий на GitHub
2. Скопируйте URL репозитория (например: `https://github.com/username/repository-name.git`)
3. Свяжите локальный репозиторий с удаленным:
```bash
git remote add origin https://github.com/username/repository-name.git
git branch -M main
```

### Добавление файлов и первый коммит
```bash
git add .
git commit -m "Initial commit: Настройка окружения для аналитики данных"
git push -u origin main
```

### Полезные команды Git
- `git status` - проверить статус файлов
- `git add .` - добавить все изменения в индекс
- `git commit -m "Сообщение"` - создать коммит с сообщением
- `git push` - отправить изменения в удаленный репозиторий
- `git pull` - получить изменения из удаленного репозитория

## Следующие шаги

После настройки базового окружения вы можете:
- Изучить основы работы с pandas для анализа данных
- Научиться создавать визуализации с помощью matplotlib и seaborn
- Освоить машинное обучение с scikit-learn
- Создавать интерактивные дашборды с Dash