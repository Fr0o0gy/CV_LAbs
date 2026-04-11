# 4 лабораторная работа 
## Сверточные нейронные сети
План:
1) Немного теории
2) Реализация на практике

Рассмотрим самую банальную сверточную сеть

вопрос КАК?

<img width="1297" height="999" alt="изображение" src="https://github.com/user-attachments/assets/ffe395c9-2138-480e-bc96-bf55bab320cc" />

Чаще всего мы видим какие-нибудь такие картинки
<img width="1467" height="1023" alt="изображение" src="https://github.com/user-attachments/assets/6f6daba4-76db-4075-b9c2-dfd31efe17ff" />

Итак возьмем чб изображение цифры от 0 до 9 размерностью 28 на 28 пикселей. Каждый пиксель, имеющий значение от 0 до 255 это входной нейрон сети 

<img width="1544" height="1002" alt="изображение" src="https://github.com/user-attachments/assets/5e5b947d-e2d9-4bd8-9f24-aa6c00f6b837" />

само число называется активацией

<img width="635" height="280" alt="изображение" src="https://github.com/user-attachments/assets/72e2180b-f5f7-466a-9de1-99073714a8a9" />

Таким образом на вход мы получаем 784 нейрона, а на выходе 10

<img width="815" height="613" alt="изображение" src="https://github.com/user-attachments/assets/aa9014a2-6ab6-4ea9-b1c5-a2bdaa1d4d6c" />

Эта сеть имеет 4 слоя. И каждый имеет нейроны, шаблон активаций одного слоя приводит к активации конкретных неронов следующего слоя нейронов и так до финального слоя. Но что скрыто внутри?

<img width="1061" height="1024" alt="изображение" src="https://github.com/user-attachments/assets/2c378380-5eec-4d6f-bd5c-9eb2fa28b795" />

Внутри у нас есть какие-то параметры. Первым параметром являются веса, значения которые умножаются на нейроны

<img width="1175" height="132" alt="изображение" src="https://github.com/user-attachments/assets/af5131a0-27bf-4954-90a8-e9f03c1de1ee" />

Представим веса в другом формате на изображении для визуализации, зеленый цвет положительные веса, а красным обозначим отрицательные

<img width="400" height="409" alt="изображение" src="https://github.com/user-attachments/assets/bd8c527f-ba98-4f67-b029-2e1677d33fc5" />

Если мы занулим веса везде, кроме какой-нибудь интересующей нас области, тогда получение взвещенной суммы пикселей сведется к сумме пикселей только в интересующей нас области

<img width="419" height="418" alt="изображение" src="https://github.com/user-attachments/assets/c4659018-db25-455d-8c86-14d2889f6342" />

Эта сумма может быть любой, но это нас не устраивает (каждый предыдущий слой будет сильнее влять на предыдущий + смягчение турбо градиентов и т.д.). Поэтому нормализуем данные от 0 до 1 (или от -1 до 1). Для этого и нужна функция 

<img width="1785" height="451" alt="изображение" src="https://github.com/user-attachments/assets/f2170570-3e98-4767-965b-5bb30f578113" />

Обычно эта функция называется сигмоидой или логистической кривой

<img width="1715" height="953" alt="изображение" src="https://github.com/user-attachments/assets/2074ceb3-4ccf-4c63-8e89-6d998ce18d6e" />

Таким образом активация нейрона это мера того насколько положительна взвешенная сумма

<img width="1829" height="1007" alt="изображение" src="https://github.com/user-attachments/assets/ecec091c-bf46-4453-a1c3-74d17396bda2" />

Но может быть, мы хотим чтобы нейрон возбуждался не от просто положительного значения, а от какого-то значения, тогда мы вводим смещение (bias)

<img width="1274" height="140" alt="изображение" src="https://github.com/user-attachments/assets/59084778-8c91-4637-9b0a-fe248f803171" />

Это только для одного нейрона, а так как неронов у нас 784 в первом слое, по 16 в скрытых слоях и 10 в выходном слое, получим следующее 

<img width="690" height="548" alt="изображение" src="https://github.com/user-attachments/assets/b6811ff8-90ba-4853-b6fb-c4c44c16d008" />

Таким образом мы получили 13к ручек для настройки работы сети. То есть обучение - это поиск корректных настроек этих ручек.

Запишем громоздкие выражения более компактно 

<img width="1186" height="710" alt="изображение" src="https://github.com/user-attachments/assets/e696801d-c033-4dd6-b451-70a96b1981ff" />

Таким образом получим функцию ошибки от 13к переменных. И обучение нейронной сети, это по сути нахождение минимума этой функции

<img width="1382" height="935" alt="изображение" src="https://github.com/user-attachments/assets/5238c407-c823-4e14-bf1b-67885dde6b47" />

А как собственно померить эту ошибку? Так как мы определяем цифру, то на выходном слое мы должны получить один возбужденный нейрон со значением 1 и остальные с нулями. ДЛя этого зададим квадрат разницы между желаемым и действительным.

<img width="1153" height="923" alt="изображение" src="https://github.com/user-attachments/assets/32d545aa-214f-4f5a-90b2-0e853521d705" />

Чем ближе сеть к истине, тем меньше ошибка и наоборот. 

<img width="898" height="789" alt="изображение" src="https://github.com/user-attachments/assets/774d64a9-cc79-40a4-b168-e83df9a4955c" />

Но в тупую смотреть на ошибки и ждать чего-то не рационально. Нужно показать куда двигаться, для этого и есть градиентный спуск. тоесть чем круче наклон функции ошибки тем быстре мы попаде к локальному минимуму, раскидаем на условной функции ошибки стартовую точки

<img width="1734" height="894" alt="изображение" src="https://github.com/user-attachments/assets/f289d161-acd0-413e-882b-d3b0d618e65f" />

Получим следующее

<img width="1730" height="869" alt="изображение" src="https://github.com/user-attachments/assets/af900b26-f61e-44f6-9ebc-183b905a871d" />

Рассмотрим сеть определенную 3 весами и 3 нейронами

<img width="1223" height="452" alt="изображение" src="https://github.com/user-attachments/assets/8f0eac74-2e4b-4ad0-bbcb-18cef92e539c" />

Рассмотрим связь между 2 последними нейронами. Обозначим их следующим образом

<img width="1826" height="974" alt="изображение" src="https://github.com/user-attachments/assets/d47be9e6-12b6-4cec-aed8-ba1ec00fe5c6" />

Выведем зависимость ошибки от входного веса
<img width="770" height="187" alt="изображение" src="https://github.com/user-attachments/assets/47d633d9-f37b-4c6e-a7e8-63c847d9eabf" />

Вычислим производные

<img width="625" height="558" alt="изображение" src="https://github.com/user-attachments/assets/046fd3c5-8936-4492-9bb3-2987cc315ae8" />

Тогда вся производная примет вид

<img width="776" height="507" alt="изображение" src="https://github.com/user-attachments/assets/68b8ec04-675d-4571-af62-f824cd95f9d9" />

Но не стоит забывать, что это только один компонент из градиента ошибки по отношению ко всем весам и смещениеям

<img width="417" height="718" alt="изображение" src="https://github.com/user-attachments/assets/fcbff9d1-65af-484c-9d5b-c83e097b324c" />

Взяв градиент по смещению, взяв производную (производная Z равна единице) получим такую формулу

<img width="1640" height="216" alt="изображение" src="https://github.com/user-attachments/assets/69fc9643-3996-4d58-9b7d-b9d496d212af" />

Для сетей имеющих больше нейронов в слое, сильно ничего не меняется, просто добавляется индекс

<img width="1108" height="592" alt="изображение" src="https://github.com/user-attachments/assets/43895c70-3360-4115-a40e-3ee13e459c4d" />

Тогда уравнение Z примет следующий вид
<img width="1108" height="592" alt="изображение" src="https://github.com/user-attachments/assets/dd007d6d-201a-468a-9c68-7a16e6da112b" />

И в итоге

<img width="1862" height="928" alt="изображение" src="https://github.com/user-attachments/assets/9f7e6d0e-a4aa-405c-8a90-05969a74db1e" />

Теперь пойдем от ошибки к началу тогда взятые производные будут накапливаться (то есть мы накидываем выражения друг на друга, а не пытаемся из менить все целиком)

Рассмотрим схемки описывающие работу нейронных сетей.

<img width="1260" height="625" alt="изображение" src="https://github.com/user-attachments/assets/d1f958f1-b8ed-47b6-bc0b-b61353c01e0a" />

Фильтр (ядро свертки) имеет ту же глубину, что и входное изображение (3 канала RGB). Он сканирует изображение с шагом 1, перемножая свои веса с соответствующими пикселями и суммируя результат. Так мы получаем карту активаций (28×28×1), где высокие значения означают, что в данном участке изображения присутствует паттерн, похожий на фильтр.

Зачем это надо?  
Уменьшается размерность (с 32×32×3 до 28×28×6), но информация не теряется, а наоборот — становится более «понятной» для следующих слоев.  
Свертка инвариантна к сдвигу: если признак чуть сместится, он все равно активирует тот же фильтр.
Веса фильтров обучаются (а не задаются вручную), поэтому сеть сама находит оптимальные признаки для своей задачи.  

<img width="685" height="333" alt="изображение" src="https://github.com/user-attachments/assets/247c982f-727e-4c86-9921-f2023b546ad9" />

Далее применяем пулинг (Слой агрегирования для уменьшения размерности)

<img width="1192" height="783" alt="изображение" src="https://github.com/user-attachments/assets/9935a545-d101-439c-a2ed-5f34a514b287" />

Итак, пулиннг имеет следущие свойства

<img width="818" height="527" alt="изображение" src="https://github.com/user-attachments/assets/c9124fc2-a36e-4d51-82e7-904e54111efb" />

Рассмотрим несколько примеров

<img width="1649" height="752" alt="изображение" src="https://github.com/user-attachments/assets/2a9c09e0-0c0c-4528-8493-ca08ff8eadf5" />

VGG

<img width="673" height="357" alt="изображение" src="https://github.com/user-attachments/assets/c454840c-dedf-42fc-9fea-c136cbae4afe" />

GoogleNet

<img width="1273" height="857" alt="изображение" src="https://github.com/user-attachments/assets/948ee39b-0112-4b76-9c79-e249bf4d8fc5" />

ResNett

<img width="1290" height="817" alt="изображение" src="https://github.com/user-attachments/assets/0dd03cce-d469-41d6-87bf-820046687a0a" />

Также можно использовать свертку 1 на 1 для получения карт активаций той же размерности

<img width="673" height="217" alt="изображение" src="https://github.com/user-attachments/assets/bbc3dcf4-f5c6-470f-b0a8-6d91dcae95a6" />

Чуваки начали применять перенос весов для решения проблемы затухания градиента

<img width="1260" height="628" alt="изображение" src="https://github.com/user-attachments/assets/cdc1a06b-3d66-47d3-8e37-04a57b54a8a9" />

<img width="1762" height="801" alt="изображение" src="https://github.com/user-attachments/assets/3eb12797-732d-46ba-9227-af8cc9d06891" />

Yolo (you only look once)

<img width="1722" height="704" alt="изображение" src="https://github.com/user-attachments/assets/dd5e4611-32b9-4902-8fc0-51550669c8c9" />

<img width="1358" height="826" alt="изображение" src="https://github.com/user-attachments/assets/9561ea29-3919-4800-9159-ded1b2cc2b4d" />

<img width="1368" height="710" alt="изображение" src="https://github.com/user-attachments/assets/487381a7-def4-47ef-8b03-008134d10228" />

Теперь глянем мою работу

Нашел датасет английских букв (1 буква записана в ячейку 1х785)  
Изображение 28х28 и 1 метка  
Загрузил его


<img width="647" height="403" alt="изображение" src="https://github.com/user-attachments/assets/a8a07959-42dc-455a-aa43-d14d2c1efb97" />

Глянул сколькр примеров каждой буквы

<img width="333" height="540" alt="изображение" src="https://github.com/user-attachments/assets/2a49c520-869d-4670-a85d-f04a69692033" />

Посмотрел вообще как они записаны

<img width="813" height="413" alt="изображение" src="https://github.com/user-attachments/assets/88334988-6b02-4405-8acb-2a0e87294c75" />

Нормализовал и подготовил данные

<img width="222" height="52" alt="изображение" src="https://github.com/user-attachments/assets/9655e1e8-41ee-4dcc-877f-48235f44e0a7" />

На всякий еще раз
Conv + pooling извлекают локальные примитивы (края,текстуры,простые формы)  
Flatten меняет формат с 3д на 1д  
Dense(128) Извлекает глобальные комбинации (там вертикальные линии, горизонтальные,круги)  
Dense(26) Классифицирует класс (1 из 26)  
<img width="538" height="469" alt="изображение" src="https://github.com/user-attachments/assets/ec474d8b-6c81-4911-b755-95df1c5bcc5b" />

Батч - кол-во итераций через которые обновляются веса ( мб Эпоха = Все элементы выборки / размер батча)  
Эпоха - Количество полных проходов по всему обучающему набору данных  
Validation_split - количество от обучающих данный для проверки на сколько хорошо работает модель (валидации, то есть она не учится а только проверяет себя)  
Verbose - Что будем выводить (0 - ничего, 1 - Прогресс-бар, потери, точность, 2 - Только значения)  
<img width="1092" height="389" alt="изображение" src="https://github.com/user-attachments/assets/ac4561e4-fe44-4a70-8fd1-164e8957cc30" />

X_test --- тестовые изображения  
y_test --- равильные метки для тестовых изображений

ПОлучили точность
<img width="302" height="33" alt="изображение" src="https://github.com/user-attachments/assets/797202fc-2469-45ae-9c23-45e9f6fe5196" />

Выведем графики
<img width="795" height="260" alt="изображение" src="https://github.com/user-attachments/assets/b019254a-93ae-4125-a847-14bc2a9c30b5" />

На всякий приведем пример предсказаний
<img width="432" height="229" alt="изображение" src="https://github.com/user-attachments/assets/0b835e30-df07-4413-99a2-056090317d30" />

Ну и для оценки выведим матрицы корреляции
<img width="890" height="831" alt="изображение" src="https://github.com/user-attachments/assets/cc5d2952-c129-485b-844e-a22d75dd36cb" />

<img width="876" height="828" alt="изображение" src="https://github.com/user-attachments/assets/dbe48091-034d-4901-8d05-0906ab8328d7" />
