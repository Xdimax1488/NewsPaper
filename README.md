Создать двух пользователей (с помощью метода User.objects.create_user):

user1 = User.objects.create(username = 'Dima')
user2 = User.objects.create(username = 'Wasja')

Создать два объекта модели Author, связанные с пользователями:

Author.objects.create(author = User.objects.get(username = 'Dima'))
Author.objects.create(author = User.objects.get(username = 'Wasja'))

Добавить 4 категории в модель Category:
 
Category.objects.create(category_name = 'Sport')
Category.objects.create(category_name = 'Politics')
Category.objects.create(category_name = 'Weather')
Category.objects.create(category_name = 'Economics')

Добавить 2 статьи и 1 новость:

Post.objects.create(author= Author.objects.get(author = User.objects.get(username= 'Dima')),title = Post.article, text_title='Bad weather',text_news = 'some text')
Post.objects.create(author= Author.objects.get(author = User.objects.get(username= 'Dima')),title = Post.news, text_title='Exchange rates by currency',text_news = 'some text')
Post.objects.create(author= Author.objects.get(author = User.objects.get(username= 'Wasja')),title = Post.article, text_title='New president',text_news = 'some text')

Присвоить им категории (как минимум в одной статье/новости должно быть не меньше 2 категорий):

 p1 =Post.objects.filter(text_title="Bad weather")
 p2 =Post.objects.filter(text_title="Exchange rates by currency")
 p3 =Post.objects.filter(text_title="New president")
 c1 =Category.objects.get(category_name ='Sport')
 c2 =Category.objects.get(category_name ='Politics')
 c3 =Category.objects.get(category_name ='Weather')
 c4 =Category.objects.get(category_name ='Economics')
 p1._category.add(c3,c1)
 p2._category.add(c4)
 p3._category.add(c2)
 
Создать как минимум 4 комментария к разным объектам модели Post (в каждом объекте должен быть как минимум один комментарий):







