# Распознавание марки и модели машины по фото
Задача: по фото определить марку и модель машины.

Используемый датасет: [VMMRdb](http://vmmrdb.cecsresearch.org/)

Ввиду отсутствия возможности обучать модель используя мощные ресурсы, обучение было проведено для распознавания трех классов: Ford Explorer, Honda Civic и Nissan Altima (папки с изображениями в new_dataset). Эту же модель можно использовать и для обучения на большем количестве классов.

# Использование проекта: 

  1) В файле config.py указать путь до папки-датасета. В эту папку поместить папки с фотографиями (1 папка - 1 класс).
  2) Установить зависимости исполнив команду ``` pip3 install -r requirements.txt ```
  3) Сделать препроцессинг датасета, исполнив команду ``` python3 main.py -p ```
  4) Чтобы запустить обучение, нужно исполнить команду ``` python3 main.py -t ```. Количество эпох и параметры SGD можно изменять в файле config.py
  5) Чтобы предсказать класс картинки, нужно исполнить команду ``` python3 main.py -i image_path/image.jpg ```. Здесь для предсказания будет использоваться параметры обученной модели из папки ``` results/resnet152/resnet152.pt ```
  
# Процесс обучения:
После обучения строятся графики loss и accuracy для тренировочной и валидационной выборки. Найти их можно в ``` results/resnet152/resnet152_graph.png ```. Полученные параметры модели можно скачать по ссылке [resnet152.pt](https://drive.google.com/file/d/1z8rokHI-2jjN9obpa9ZQ4Hgg-QwkjP2I/)
В папке ``` web_images ``` лежат картинки, которые я скачал из выдачи Яндекса по запросу соответсвующих моделей машин.
В ноутбуке ``` test_sample.py.ipynb ``` показываются предсказания модели на этих картинках.

Используемая модель - ResNet 152. При первом ее обучении я столкнулся с тем, что loss на валидационной выборке ведет себя неадекватно. 
После этого я добавил аугментацию (отражение по горизонтали и изменение яркости/гаммы картинки) и обучение пошло хорошо (можно посмотреть на графике).