# Komendy do Gita

1\. Sprawdzenie statusu plików\
`git status`

2\. Tworzenie repozytorium
1. Inicjalizacja repozytorium w bieżącym folderze\
`git init`
2. Zdalne łączenie repozytorium\
`git remote add origin <link>`
3. Zmiana nazwy gałęzi na main\
`git branch -M main`

3\. Proces dodawania plików do repozytorium
1. Sprawdzenie statusu plików\
`git status`
2. Inicjalizacja plików/pliku\
`git add .` lub `git add <nazwa pliku>`
3. Zapis zmian, dodanie commita\
`git commit -m "<text>"`
4. Wysłanie plików na main\
`git push -u origin main`

4\. Ignorowanie (nie dodawanie do repozytorium) określonego pliku\
`echo "<nazwa pliku>" >> .gitignore`