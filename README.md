1. Опишите кратко, как вы поняли: в чем основное отличие полной (аппаратной) виртуализации, паравиртуализации и виртуализации на основе ОС.

Ответ:

Аппаратная виртуализация включает в себя установку гипервизора или диспетчера виртуальных машин (VMM). Именно они создают уровень абстракции между программным обеспечением и непосредственным «железом». После установки гипервизора программное обеспечение полагается на виртуальные представления вычислительных компонентов — то есть, к примеру, на виртуальные CPU вместо физических

Виртуализация на основе ОС могут использовать все ресурсы хостовй машины ( доступновсе железо ),
так же используют общие динамические библиотеки, общие страницы  памяти на хостовой машине, что может экономить ресурсы.
При этом контейнер и хостовая машина должны быть на одинаковом ядре (в базовом понимании).

При Паравирутализации, госетвая ОС используют только собственные ресурсы выделенные гипервизором.
Другими словами: при паравиртуализации имеется слой Гипервизора (отвечающий за разделение ресурсов)в хостовой машине, о
существляющих взаимодействия гостевой ос и железа
в контейнерной релиазаии, контейнер обращается  без явного слоя гипервизора в ОС, разделение ресурсов осуществляется на уровне ОС.  

2. Выберите один из вариантов использования организации физических серверов, в зависимости от условий использования.

Организация серверов:

- физические сервера,
- паравиртуализация,
- виртуализация уровня ОС.

Условия использования:

- Высоконагруженная база данных, чувствительная к отказу.
- Различные web-приложения.
- Windows системы для использования бухгалтерским отделом.
- Системы, выполняющие высокопроизводительные расчеты на GPU.

Опишите, почему вы выбрали к каждому целевому использованию такую организацию.

Ответ:

Высоконагруженная база данных, чувствительная к отказу
    Физический сервер 
        требуется более высокая производительность, аппаратное размещение дает более высокий отклик, 
        и сокращает точки отказа в виде гипервизора хостовой машны.
        хотя возможно (и используется) использование полной  аппаратной виртуализации при использовании 
        кластеризации для повышения доступности (такиесервера БД имеются у нас организации)
         
Различные Java-приложения
    Виртуализация уровня ОС (контейнеры)
        Требуется меньше ресурсов, выше скорость масштабирования при необходимости расширения. 
        нет жестких требований к аппаратнымм ресурсам, требет меньше ресурсов на администрирование

Windows системы для использования Бухгалтерским отделом
    Паравиртуализация 
        эффективнее делать бэкаприрование -  клонирование всей вирт. машины, 
        возможность расширени ресурсов на уровне вирт. машины. 
        нет критичных требований к доступу к аппаратной составляющей сервера.
        
Системы, выполняющие высокопроизводительные расчеты на GPU
    Физические сервера 
        как мне кажется, для аппаратнх расчетов требуется максимальный доступ к аппаратным ресурсам,
        который физический сервер даетболее эффективно, и а в 2х других, доступ осуществляется черех хостовую ОС 

3. Выберите подходящую систему управления виртуализацией для предложенного сценария. Детально опишите ваш выбор.

Сценарии:

- 100 виртуальных машин на базе Linux и Windows, общие задачи, нет особых требований. Преимущественно Windows based инфраструктура, требуется реализация программных балансировщиков нагрузки, репликации данных и автоматизированного механизма создания резервных копий.
- Требуется наиболее производительное бесплатное open source решение для виртуализации небольшой (20-30 серверов) инфраструктуры на базе Linux и Windows виртуальных машин.
- Необходимо бесплатное, максимально совместимое и производительное решение для виртуализации Windows инфраструктуры.
- Необходимо рабочее окружение для тестирования программного продукта на нескольких дистрибутивах Linux.

Ответ:
- Необходимо рабочее окружение для тестирования программного продукта на нескольких дистрибутивах Linux.
Например Docker
Позволяет создавать контейнеры, автоматизировать их запуск и развертывание, управляет жизненным циклом. Он позволяет запускать множество контейнеров на одной хост-машине.
Контейнеры позволяют отделить приложение от инфраструктуры: разработчикам не нужно задумываться, в каком окружении будет работать их приложение, будут ли там нужные настройки и зависимости. Они просто создают приложение, упаковывают все зависимости и настройки в единый образ. Затем этот образ можно запускать на других системах, не беспокоясь, что приложение не запустится.

4. Опишите возможные проблемы и недостатки гетерогенной среды виртуализации (использования нескольких систем управления виртуализацией одновременно) и что необходимо сделать для минимизации этих рисков и проблем. Если бы у вас был выбор, то создавали бы вы гетерогенную среду или нет? Мотивируйте ваш ответ примерами.

Ответ:

Проблемы гетерогенной среды:

- содержать несколко команд администрирования/сопровождения для разных систем (кдровые издержки)
- гораздо ниже масштабируемость, придется масштабировать 2(или более) системы, 
- сложность при выделении и управлении ресурсами
- финансовые затраты, так как необходимо содержать несколько систем одновременно (если считать платные версии)
- проблемы миграции между разными системами, + полное дублирование всей инфраструктуры под 2(или более) системы виртуализации
- если бой и тест в разных системах, то отлавливать "баги" сложнее
      
Без опыта, крайне сложно сказать как минимизировать , но можно предположить:
 - распределить системы по совместимости, например, Hyper-V для всей Windows инфраструктуры и VMWare для остальных. 
 - обучить команду сопровождения работе с обоими системами, для взаимозаменяемости (достаточно спорный вариант, но применяемый)
 - дальше затрудняюсь без практического опыта, что-то сказать (нескольких лекций явно недостаточно)
Предположу что выбрал бы одну систему, так как инфраструктурно и кадрово содержать такую куда практичнее,но есть нюансы в используемых задачах, возможно чисто техниески может потребоваться и разные системы. 
Без комплектсного видения очень сложно сказать.
Но при развернтой инраструктуре на Windows, использование других продуктов, и серверов на Windows,то логичнее использовать Hyper-V для подобного решения, и не плодить зоопарка систем. 
Так же Hyper-V имеет в том числе практически полноценное бесплатное решение.
