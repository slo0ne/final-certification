
import json
import os
from datetime import datetime

DATA_FILE = "data.json"

def load_data():
    """Загружает данные из JSON-файла"""
    if not os.path.exists(DATA_FILE):
        return []
    with open(DATA_FILE, "r", encoding="utf-8") as f:
        return json.load(f)

def save_data(entries):
    """Сохраняет данные в JSON-файл"""
    with open(DATA_FILE, "w", encoding="utf-8") as f:
        json.dump(entries, f, ensure_ascii=False, indent=2)

def add_entry():
    """Добавляет новую запись о погоде"""
    print("\n--- Добавление записи ---")
    
    while True:
        date = input("Введите дату (ГГГГ-ММ-ДД): ")
        try:
            datetime.strptime(date, "%Y-%m-%d")
            break
        except ValueError:
            print("Ошибка: неверный формат даты. Используйте ГГГГ-ММ-ДД")
    
    while True:
        try:
            temp = float(input("Введите температуру: "))
            break
        except ValueError:
            print("Ошибка: введите число")
    
    description = input("Введите описание погоды: ")
    
    while True:
        rain = input("Осадки (да/нет): ").lower()
        if rain in ["да", "нет", "yes", "no"]:
            rain_yes = rain in ["да", "yes"]
            break
        print("Ошибка: введите 'да' или 'нет'")
    
    entry = {
        "date": date,
        "temperature": temp,
        "description": description,
        "rain": rain_yes
    }
    
    entries = load_data()
    entries.append(entry)
    save_data(entries)
    
    print("➤ Запись добавлена!")

def show_all():
    """Показывает все записи"""
    entries = load_data()
    
    if not entries:
        print("\nНет сохранённых записей.")
        return
    
    print("\n--- Все записи ---")
    for entry in entries:
        rain_str = "Есть осадки" if entry["rain"] else "Нет осадков"
        print(f"{entry['date']} | {entry['temperature']}°C | {entry['description']} | {rain_str}")

def filter_by_date():
    """Фильтрует записи по дате"""
    date = input("\nВведите дату для фильтрации (ГГГГ-ММ-ДД): ")
    entries = load_data()
    
    filtered = [e for e in entries if e["date"] == date]
    
    if not filtered:
        print(f"Записей на дату {date} не найдено.")
    else:
        print(f"\n--- Записи на {date} ---")
        for entry in filtered:
            rain_str = "Осадки есть" if entry["rain"] else "Осадков нет"
            print(f"{entry['temperature']}°C | {entry['description']} | {rain_str}")

def filter_by_temp():
    """Фильтрует записи по температуре > 20°C"""
    entries = load_data()
    
    filtered = [e for e in entries if e["temperature"] > 20]
    
    if not filtered:
        print("\nЗаписей с температурой > 20°C не найдено.")
    else:
        print("\n--- Записи с температурой > 20°C ---")
        for entry in filtered:
            rain_str = "Осадки есть" if entry["rain"] else "Осадков нет"
            print(f"{entry['date']} | {entry['temperature']}°C | {entry['description']} | {rain_str}")

def main():
    """Главное меню программы"""
    while True:
        print("\n" + "=" * 40)
        print("         WEATHER DIARY")
        print("=" * 40)
        print("1 — Добавить запись")
        print("2 — Показать все записи")
        print("3 — Фильтровать по дате")
        print("4 — Показать записи с температурой > 20°C")
        print("5 — Выйти")
        print("-" * 40)
        
        choice = input("Выберите пункт: ")
        
        if choice == "1":
            add_entry()
        elif choice == "2":
            show_all()
        elif choice == "3":
            filter_by_date()
        elif choice == "4":
            filter_by_temp()
        elif choice == "5":
            print("\nДо свидания!")
            break
        else:
            print("Ошибка: неверный пункт меню. Попробуйте снова.")

if __name__ == "__main__":
    main()