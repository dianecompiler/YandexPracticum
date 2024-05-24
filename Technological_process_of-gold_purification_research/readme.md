# Исследование технологического процесса очистки золота

### Задача
Нужно подготовить прототип модели машинного обучения для компании, которая разрабатывает решения для эффективной работы промышленных предприятий.

Модель должна предсказать коэффициент восстановления золота из золотосодержащей руды. Следует использовать данные с параметрами добычи и очистки. 

Модель поможет оптимизировать производство, чтобы не запускать предприятие с убыточными характеристиками.

Нам необходимо:

1. Подготовить данные;
2. Провести исследовательский анализ данных;
3. Построить и обучить модель.
   
## Этапы исследования
**1. Подготовка данных.**

    1.1. Открытие файлов и их изучение.
    1.2. Проверка правильности рассчета эффективности обогащения. Вычисление эффективности на обучающей выборке для признака rougher.output.recovery. Поиск MAE между нашими расчётами и значением признака.
    1.3. Анализ признаков, недоступных в тестовой выборке.
    1.4. Предобработка данных.
    
**2. Анализ данных.**

    2.1. Поиск и устранение аномалий.
    2.2. Исследование изменения концентрации элементов на каждом этапе.
    2.3. Анализ распределения размеров гранул на обучающей и тестовой выборках.
    2.4. Исследование суммарных концентраций.
    
**3. Построение модели.**

    3.1. Написание функции для вычисления итогового sMAPE.
    3.2. Обучение и проверка разных моделей.

**4. Выводы.**
    
## Выводы
В ходе исследования была проделана следующая работа:
- Мы проверили формулу вычисления эффективности обогащения, среднее абсолютное отклонение получилось очень низким. Значит расчеты верны.
- Выяснили, что в тестовую выборку не попали признаки с этапом final и типами параметра output и calculation. Это связано с тем, что тестовая выборка имитирует работу модели в реальных условиях протекания технологического процесса, и целевая метрика вычисляется только в работающей системе. В обучающей выборке есть все данные, т.к. целевой признак вычисляется по историческим данным.
- Провели предобработку данных: устранили пропуски, убедились в отсутствии дубликатов, устранили аномальные значения.
- Исследовали изменение концентрации элементов на каждом этапе: концентрация золота после каждого этапа увеличивается, концентрация серебра увеличивается после флотации, а затем уменьшается на последующих этапах, концентрация свинца немного увеличивается.
- Проанализировали распределения размеров гранул на обучающей и тестовой выборках, они оказались очень похожи.
- Исследовали суммарную концентрацию металлов: она растет с каждым этапом.
- Для вычисления итогового sMAPE мы написали функцию.
- Обучили и проверили модель линейной регресси, случайного леса и дерево решений. Лучший результат показала модель линейной регрессии, итоговая sMAPE на обучающей выборке составила 5.64. На тестовых данных итоговая sMAPE составила 6.24.
- Константная модель показала итоговое sMAPE 7.77. Т.е. результат тестирования нашей модели на тествой выборке лучше, чем результат константной модели.