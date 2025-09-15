
# Детекция объектов с дрона

Проект для обучения модели YOLO для детекции объектов с высоты птичьего полета.

## 🚀 Возможности

- Детекция транспортных средств с дрона
- Обучение на кастомном датасете
- Интеграция с системами навигации дронов
- Поддержка различных версий YOLO

## 📦 Установка

1. Клонируйте репозиторий:
```bash
git clone <your-repo-url>
cd drone-object-detection
```

2. Создайте виртуальное окружение и установите зависимости:
```bash
python -m venv venv
source venv/bin/activate  # Linux/Mac
# или
venv\Scripts\activate     # Windows

pip install -r requirements.txt
```

## 📁 Структура проекта

```
drone-object-detection/
├── dataset/
│   ├── images/
│   │   ├── train/
│   │   ├── val/
│   │   └── test/
│   └── labels/
│       ├── train/
│       ├── val/
│       └── test/
├── model.ipynb 
├── models/
│   └── (здесь будут сохранены обученные модели)
├── requirements.txt
├── README.md
└── .gitignore
```

## 🏃‍♂️ Быстрый старт

1. Подготовьте данные в формате YOLO:
   - Разместите изображения в `dataset/images/[train,val,test]`
   - Разместите аннотации в `dataset/labels/[train,val,test]`

2. Настройте конфигурацию в `data.yaml`:
```yaml
train: dataset/images/train
val: dataset/images/val
test: dataset/images/test

nc: 1  # количество классов
names: ['small-vehicle']  # имена классов
```

3. Запустите ноутбук:
```bash
model.ipynb
```


## 🧠 Обучение модели

Для обучения используется YOLOv8 с возможностью выбора различных размеров моделей (n, s, m, l, x):

```python
from ultralytics import YOLO

# Загрузка модели
model = YOLO('yolov11n.pt')  # nano version

# Обучение
results = model.train(
    data='data.yaml',
    epochs=100,
    imgsz=640,
    batch=16,
    device='cuda'  # или 'cpu'
)
```

## 📊 Датсет

Текущий датасет содержит:
- 7 изображений для обучения
- 3 изображения для валидации
- Класс: small-vehicle (малые транспортные средства)

Аннотации в формате YOLO:
```
class_id center_x center_y width height
```