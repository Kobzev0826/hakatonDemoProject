# hakatonDemoProject
## team: three silent men 
Королев Артем Олегович  
Кобзев Владимир Анатольевич  
Бараев Дамир Рустамович 

### Описание проблемы
Возникновение ошибки обусловлено отсутсвием синзронизации кода и БД. 
Если посмотреть на Breakpoint идущей с проектом в репозитории ( HakatonEntityRepository) то можно увидеть следующую картину:  
При первых нескольких обращениях Boolean existsHakatonEntityByName(String name); возвращало значение false по этому происходила запись id
и возникала ошибка, когда спустя какое то время БД помещала первое присланое значение, а для второго значения срабатывало условие на запрет одинаковых идентификаторов 
### Вариант решения
Решение лежит в плоскости синхронизации 
наш вариант: 
добавление ReentrantLock в DomainServiceImpl метод saveHakatonEntity  

### P.S.
не стоит добавлять в распостраняемые файлы данные для доступа к БД. Предоставляемые данные, с разрешениями для пользователя давали возможность снять ограничение на запрет одинаковых значений, а так же изменять БД.  
По этому один из вариантов решения может быть в изменении политики БД)
