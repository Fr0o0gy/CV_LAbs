# Лабораторные работы по компьютерному зрению

## 3 Лабораторная работа

**Путинцев Кирилл, группа 8Е21**

### Работа с видеопотоком

Сначала разберемся в задачами видеонаблюдения, а потом рассмотрим выполненную лабораторную работу

Задачи видеонаблюдения
<img width="1051" height="711" alt="изображение" src="https://github.com/user-attachments/assets/67c7c363-9aee-44f8-89f4-3f26b6df672e" />

Какие проблемы с этим связаны?

<img width="1661" height="405" alt="изображение" src="https://github.com/user-attachments/assets/5e507abd-1bdf-4838-80a9-a5c69d49432c" />

А как будем оценивать?

<img width="1679" height="805" alt="изображение" src="https://github.com/user-attachments/assets/68a7331d-afdc-4f61-972c-ac9a08ceafc1" />

В рамках лабораторной работы мы имеем задачу слежения за мышкой. Рассмотрим пример с аналогичным видео. Мы имеем ряд допущений

<img width="907" height="573" alt="изображение" src="https://github.com/user-attachments/assets/2a1945cb-af5f-499b-a86f-b8632b0c73f8" />

Разработаем алгоритм

<img width="1465" height="821" alt="изображение" src="https://github.com/user-attachments/assets/9a560c82-a919-4847-a47a-b0897ebd5258" />

После, с помощью первых моментов определим центр масс изображения. Тем самым получив центр масс оставшейся мышки.

Дальше остается только соединить центры масс покадрово отфильтровав выбросы. Так мы получим траекторию. И для наглядности соеденим центры масс каждого изображения с исходным изображением.

Теперь глянем как это выглядит в моем исполнении

<img width="814" height="678" alt="изображение" src="https://github.com/user-attachments/assets/32c032d1-436b-4690-9245-59a175155324" />

<img width="587" height="221" alt="изображение" src="https://github.com/user-attachments/assets/318e64e9-7279-48bd-8a93-521467cf8d14" />

<img width="611" height="461" alt="изображение" src="https://github.com/user-attachments/assets/d7fb78a4-1758-4d6e-9b42-365dac2b48b1" />

Фон

<img width="618" height="296" alt="изображение" src="https://github.com/user-attachments/assets/18f8780b-9a88-4ea0-8d0b-28f83306ed7a" />


<img width="578" height="470" alt="изображение" src="https://github.com/user-attachments/assets/b0df97ee-5f44-46d2-853c-ab18d20e902a" />

Сравнение

<img width="739" height="302" alt="изображение" src="https://github.com/user-attachments/assets/759d9401-b18b-4c98-b01d-61e664a3a416" />

Результат вычитания

<img width="555" height="421" alt="изображение" src="https://github.com/user-attachments/assets/1e5c1341-13b1-463e-90ae-16bac4c3cba7" />

Результат работы после морфологической операции закрытия (эрозия + делатация) + бинаризация

<img width="537" height="408" alt="изображение" src="https://github.com/user-attachments/assets/04b9b898-0a8d-4dfd-b4d5-c127c4a3a329" />

Перезапусти и вставь картинку с центром масс
<img width="590" height="487" alt="изображение" src="https://github.com/user-attachments/assets/36005745-75f3-43a4-aa60-663604e99fb4" />

И финальная траектория
<img width="589" height="443" alt="изображение" src="https://github.com/user-attachments/assets/2ac0db06-9bf7-4f56-8ebf-581d809a7667" />

