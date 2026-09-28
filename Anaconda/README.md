# Komendy do Anacondy

1\. Tworzenie nowego środowiska ('y' - potwierdzenie instalacji):\
`conda create -n nazwa_środowiska python=3.12`

2\. Instalacja ipykernel:\
`pip install ipykernel`

3\. Aktywowanie danego środowiska:\
`conda activate nazwa_środowiska`

4\. Lista środowisk:\
`conda info --envs`

5\. Dodanie kernela do środowiska:\
`python -m ipykernel install --user --name=nazwa_środowiska --display-name="Wyświetlana nazwa"`

6\. Usunięcie kernela z jupytera:\
`jupyter kernelspec uninstall nazwa_kernela`

7\. Sprawdź listę kerneli:\
`jupyter kernelspec list`

8\. Usunięcie danego środowiska:\
`conda env remove -n nazwa_środowiska`

