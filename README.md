## Инструкция по запуску демки по распознаванию лиц на raspberry pi
### Необходимые компоненты
1. OS - Raspbian Buster
2. Python >= 3.4
3. Cmake
4. Установленный openvino версии 2020.4 для raspbian.
5. Intel Neural Compute Stick 2
6. Веб-камера
7. Библиотеки для питона (помимо тех, что устанавливаются с openvino):
    1. PyQt5
    2. Pandas
    3. Numpy
    4. Scipy
    5. opencv-python

#### Ссылки на необходимые компоненты
OS: https://www.raspberrypi.org/downloads/raspberry-pi-os/    
OPENVINO: https://download.01.org/opencv/2020/openvinotoolkit/2020.4/l_openvino_toolkit_runtime_raspbian_p_2020.4.287.tgz
#### Установка Cmake
```
sudo apt install cmake
```
#### Установка openvino

##### Установка кратко:
Загрузка openvino и установка переменных среды (запись в ./bashrc для удобства)
```
sudo mkdir -p /opt/intel/openvino
cd /opt/intel/openvino
wget https://download.01.org/opencv/2020/openvinotoolkit/2020.4/l_openvino_toolkit_runtime_raspbian_p_2020.4.287.tgz
tar -xf  l_openvino_toolkit_runtime_raspbian_raspbian_p_2020.4.287.tgz --strip 1 -C /opt/intel/openvino

source /opt/intel/openvino/bin/setupvars.sh
echo "source /opt/intel/openvino/bin/setupvars.sh" >> ~/.bashrc
```

Установка зависимостей openvino

```
cd /opt/intel/openvino/install_dependencies/
sudo ./install_openvino_dependencies.sh
```

Добавление USB правил для NSC2
```
sudo usermod -a -G users "$(whoami)"
sh /opt/intel/openvino/install_dependencies/install_NCS_udev_rules.sh
```

Ссылка на гайд по установке: https://docs.openvinotoolkit.org/latest/openvino_docs_install_guides_installing_openvino_raspbian.html

#### Установка необходимых библиотек для питона

```
pip install --upgrade pip
pip install numpy
pip install PyQt5
pip install pandas
pip install scipy
pip install opencv-python

```
### Запуск демки

Демка находится в папке FacialRecognition.
Для её запуска необходимо запустить start.sh, с подключенной к RPI веб-камерой и NCS2.
В этом файле описаны параметры с которыми запускается файл face_recognition_demo.py. (Список параметров есть в FacialRecognition/README.md)

```
# В папке FacialRecognition

chmod +x start.sh
./start.sh

```

Добавление лиц пользователей для распознавания осуществляется в папку /face pics
Имена пользователей - названия изображений с расширением .jpg
Результат распознавания лиц записывается в таблицу faces_detected.csv

Оригинальный репозиторий - https://github.com/aguazul/FacialRecognition


