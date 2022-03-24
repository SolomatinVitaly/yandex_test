<p>Решение тестового задания от техгруппы поддержки Медиасервисов на Junior-разработчика
<p>Для корректной работы в первом задании в папке со скриптом должен быть скачан исходный файл</p>

##***Техзадание:***

### Задание 1
Есть набор данных о стоимости недвижимости в Великобритании - .csv файл (скачать можно по ссылке
https://disk.yandex.ru/d/ZTnv3LiUeqEK5A, описание столбцов тут https://www.gov.uk/guidance/about-the-price-paid-data)
нужно написать программу, которая сформирует файл, в котором будет перечислена вся недвижимость, проданная больше 1-го раза.
Программа должна потреблять как можно меньше вычислительных ресурсов. Рассмотреть случаи экономии памяти и процессорного времени.


### Задание 2
Есть процесс, который запускается каждый раз, когда сотрудник поддержки нажимает кнопку, чтобы взять обращение пользователя в работу. Работа процесса описывается функцией (язык программирования groovy):
defset_assignee(login) // логин сотрудника поддержки
{
	// request_data - интерфейс управления БД. Считать, что не может исполняться несколько операций с БД параллельно
	requests = request_data.get_all() // получаем все обращения пользователей из БД
	request = requests.groupBy{
		it.id
	}.collect{ key, value ->
		value.max{ it.version }
	}.findAll{ req ->
		req.status == 'opened'&&
		req.state == 'ready'
	}.max{
		it.priority
	}
	if (request == null)
		returnnull
	
	request.state = 'inprogress'
	request.assignee = login
	request.version += 1
	request_data.upload(request) // загружаем новую версию обращения в БД (старая не удаляется)
	returnrequest
}

Функция возвращает системе обращение пользователя. Это обращение попадает в работу сотруднику поддержки.
Случилась ошибка: одно и то же обращение пользователя попало в работу 2-м сотрудникам поддержки. Измените код так, чтобы этого больше не повторилось.


### Задание 3
Написать программу, которая шлёт в некоторый канал в Телеграмме последнюю новость с сайта https://vc.ru
Условие: в коде не должно быть токенов.

Для всех 3 задач
Разрешённые языки программирования:
С/С++
Java
Groovy
Python



