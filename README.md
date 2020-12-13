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

 p1 =Post.objects.get(text_title="Bad weather")
 p2 =Post.objects.get(text_title="Exchange rates by currency")
 p3 =Post.objects.get(text_title="New president")
 c1 =Category.objects.get(category_name ='Sport')
 c2 =Category.objects.get(category_name ='Politics')
 c3 =Category.objects.get(category_name ='Weather')
 c4 =Category.objects.get(category_name ='Economics')
 p1._category.add(c3,c1)
 p2._category.add(c4)
 p3._category.add(c2)
 
Создать как минимум 4 комментария к разным объектам модели Post (в каждом объекте должен быть как минимум один комментарий):

Comment.objects.create(user = User.objects.get(username= 'Dima'), post = Post.objects.get(text_title="Bad weather"), comment = 'good')
Comment.objects.create(user = User.objects.get(username= 'Wasja'), post = Post.objects.get(text_title="Bad weather"), comment = 'so so')
Comment.objects.create(user = User.objects.get(username= 'Wasja'), post = Post.objects.get(text_title="Exchange rates by currency"), comment = 'so bad news')
Comment.objects.create(user = User.objects.get(username= 'Wasja'), post = Post.objects.get(text_title="New president"), comment = 'Maybe it will be better')

Применяя функции like() и dislike() к статьям/новостям и комментариям, скорректировать рейтинги этих объектов:

Post.objects.get(text_title="Bad weather").like()
Post.objects.get(text_title="Bad weather").like()
Post.objects.get(text_title="Bad weather").like()
Post.objects.get(text_title="Bad weather").like()
Post.objects.get(text_title="Bad weather").dislike()

Post.objects.get(text_title="Exchange rates by currency").like()
Post.objects.get(text_title="Exchange rates by currency").like()
Post.objects.get(text_title="Exchange rates by currency").like()
Post.objects.get(text_title="Exchange rates by currency").like()

Post.objects.get(text_title="New president").like()
Post.objects.get(text_title="New president").like()
Post.objects.get(text_title="New president").dislike()
Post.objects.get(text_title="New president").dislike()

Comment.objects.get(comment = 'good').like()
Comment.objects.get(comment = 'good').like()
Comment.objects.get(comment = 'good').like()
Comment.objects.get(comment ='so so').like()
Comment.objects.get(comment ='so so').like()
Comment.objects.get(comment ='so so').like()
Comment.objects.get(comment ='so bad news').like()
Comment.objects.get(comment ='so bad news').like()
Comment.objects.get(comment ='so bad news').like()
Comment.objects.get(comment ='so bad news').dislike()
Comment.objects.get(comment ='Maybe it will be better').like()

Обновить рейтинги пользователей:
Author.objects.get(author= User.objects.get(username ='Dima')).update_rating()
Author.objects.get(author= User.objects.get(username ='Wasja')).update_rating()

Вывести username и рейтинг лучшего пользователя (применяя сортировку и возвращая поля первого объекта):
top_author = Author.objects.all().order_by('-author_rating').values('author', 'author_rating')[0]
top_author['author'] = Author.objects.all().order_by('-author_rating').author.username
print(top)

Вывести дату добавления, username автора, рейтинг, заголовок и превью лучшей статьи, основываясь на лайках/дислайках к этой статье:
top_post = Post.objects.all().order_by('-article_rating').values("datetime", 'author', 'article_rating', 'text_title')[0]
top_post["datetime"] = top_post["datetime"].strftime("%A, %d. %B %Y %I:%M%p")
top_post['author'] = Post.objects.all().order_by('-article_rating')[0].author.author.username
top_post['превью'] = Post.objects.all().order_by('-article_rating')[0].preview()
print(top_post)

Вывести все комментарии (дата, пользователь, рейтинг, текст) к этой статье:

 all_comms = Comment.objects.filter(post =Post.objects.get(text_title="Bad weather")).values('datetime', 'user', 'comment_rating', 'comment')
 for com in all_comms:
     com['datetime'] = com['datetime'].strftime("%A, %d. %B %Y %I:%M%p")
     com['user'] = Author.objects.get(author = com['user']).author.username
 print(all_comms)












