# HW5 Aksenov Yaroslav

[Ссылка на ноутбук](https://colab.research.google.com/drive/1n8qeBdDAoR9SDIJjg4ZI9uOu4HRI9Y83?usp=sharing)

# Нормализация
Использовался метод TPM, где длина транскрипции была убрана, так как она нам неизвестна, получилась следующая формула:

<img src="https://render.githubusercontent.com/render/math?math={\Large TPM_i = \frac{q_i}{\sum q_j} \cdot 10^6}#gh-light-mode-only">
<img src="https://render.githubusercontent.com/render/math?math={\Large \color{white}TPM_i = \frac{q_i}{\sum q_j} \cdot 10^6}#gh-dark-mode-only">

<img src="https://render.githubusercontent.com/render/math?math={q_i}#gh-light-mode-only"> <img src="https://render.githubusercontent.com/render/math?math={\color{white} q_i}#gh-dark-mode-only"> - риды попавшие на транскрипцию </br>
<img src="https://render.githubusercontent.com/render/math?math={l_i}#gh-light-mode-only">


# Полученные графики

![](/images/heatmap.png)
На графике видим 5 кластеров.
![](images/PCA.png)
Разбили на группы cTEC, mTEC-III, mTEC-IV, mTEC-I, mTEC-II понизили размерность данных.
![](images/UMAP.png)
