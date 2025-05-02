import os
import zipfile

project_name = "buhuchet-online"
os.makedirs(project_name, exist_ok=True)

files = {
    "index.html": '''<!DOCTYPE html>
<html lang="ru">
<head>
  <meta charset="UTF-8">
  <title>Академия Бухгалтерии Онлайн</title>
  <link rel="stylesheet" href="style.css">
</head>
<body>
  <header>
    <h1>Академия Бухгалтерии Онлайн</h1>
    <nav>
      <a href="index.html">Главная</a>
      <a href="courses.html">Курсы</a>
    </nav>
  </header>
  <main>
    <section class="hero">
      <h2>Онлайн-обучение бухгалтерии для всех</h2>
      <p>Практические курсы для начинающих и опытных специалистов.</p>
      <a href="courses.html" class="btn">Посмотреть курсы</a>
    </section>
  </main>
  <footer>
    <p>&copy; 2025 Академия Бухгалтерии</p>
  </footer>
</body>
</html>''',

    "courses.html": '''<!DOCTYPE html>
<html lang="ru">
<head>
  <meta charset="UTF-8">
  <title>Курсы по бухгалтерии</title>
  <link rel="stylesheet" href="style.css">
</head>
<body>
  <header>
    <h1>Курсы по бухгалтерии</h1>
    <nav>
      <a href="index.html">Главная</a>
      <a href="courses.html">Курсы</a>
    </nav>
  </header>
  <main>
    <section>
      <h2>Бухгалтерский учет с нуля</h2>
      <p>Изучите основы бухучета, двойную запись, счета и проводки.</p>
    </section>
    <section>
      <h2>1С: Бухгалтерия</h2>
      <p>Освойте работу в 1С:Бухгалтерия 8.3 — от документов до отчетности.</p>
    </section>
    <section>
      <h2>Налогообложение для малого бизнеса</h2>
      <p>Упрощенка, ОСНО, налоги ИП и ООО — просто и доступно.</p>
    </section>
  </main>
  <footer>
    <p>&copy; 2025 Академия Бухгалтерии</p>
  </footer>
</body>
</html>''',

    "style.css": '''body {
  font-family: 'Segoe UI', sans-serif;
  background-color: #f9f9f9;
  color: #333;
  margin: 0;
  padding: 0;
}
header {
  background-color: #2c3e50;
  color: white;
  padding: 20px;
  text-align: center;
}
nav a {
  margin: 0 10px;
  color: white;
  text-decoration: none;
}
.hero {
  background-color: #ecf0f1;
  padding: 50px;
  text-align: center;
}
.btn {
  background-color: #2980b9;
  color: white;
  padding: 10px 20px;
  text-decoration: none;
  border-radius: 4px;
}
footer {
  background-color: #ddd;
  text-align: center;
  padding: 15px;
}
'''
}

# Создание файлов
for filename, content in files.items():
    with open(os.path.join(project_name, filename), 'w', encoding='utf-8') as f:
        f.write(content.strip())

# Создание архива
zip_path = f"{project_name}.zip"
with zipfile.ZipFile(zip_path, 'w') as zipf:
    for root, _, filenames in os.walk(project_name):
        for filename in filenames:
            full_path = os.path.join(root, filename)
            arcname = os.path.relpath(full_path, project_name)
            zipf.write(full_path, arcname)

print(f"Сайт упакован в архив: {zip_path}")
