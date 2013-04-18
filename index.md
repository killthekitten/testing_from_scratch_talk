# rspec_rescue_mission

!SLIDE

# Спасение утопающих

## Покрываем тестами взрослый Ruby on Rails проект

!SLIDE

# @killthekitten
## Николай Шебанов

!SLIDE bottom-left

# Тесты естественны для RoR
}}} images/railsguides.png

!SLIDE

# И тем не менее...

!SLIDE left

}}} images/patsan.png

!SLIDE

# Зачем?
## ...нужны тесты, если можно и без них

!SLIDE bottom-left

# Тесты экономят $$$
}}} images/bablo.jpg

!SLIDE

# Тогда почему их нет?
## (тестов)

!SLIDE left

# Тестов нет потому, что:

1. "Есть задачи поважнее"
1. Мешают на стадии прототипа
1. Команда не имеет опыта тестирования
1. ...

!SLIDE left

# Как результат, с каждым новым релизом:

1. Больнее выкатывать релиз
1. Дольше разрабатывать новые фичи
1. Труднее рефакторить
1. Тесты откладываются в самый дальний ящик

!SLIDE bottom-left

# Бизнес теряет деньги

}}} images/success.png

!SLIDE bottom-right

# Программист теряет работу

}}} images/success2.jpg

!SLIDE top-left

# Надо спасать ситуацию

}}} images/rescue.jpg

!SLIDE left

# Работа над ошибками

+ Спеки - не доп. задача, спеки - часть задачи
+ Долго пишет спеки тот, кто делает это плохо
+ "Потом допишу" Driven Development
+ Нужно менять воркфлоу

!SLIDE left

# Фигакс-фигакс и в продакшн
+ Читаем условия задачи
+ Коммитим решение
+ ...
+ PROFIT

!SLIDE left

# Делаем по науке
+ Читаем условия задачи
+ **Пишем тесты**
+ Коммитим **протестированное** решение
+ **Code Review + CI Server**
+ ...
+ PROFIT

!SLIDE

# Инструментарий

``` ruby
group :test, :development do
  gem 'factory_girl'
  gem 'factory_girl_rails'
  gem 'rspec-rails'
  #gem 'capybara'
  #gem 'capybara-webkit'
  gem 'rr'
  gem 'simplecov', require: false
  gem 'shoulda'
  gem 'webmock'
  gem 'simplecov', require: false
end

group :development do
  gem 'guard-rspec'
  gem 'terminal-notifier-guard'
end
```

!SLIDE

# simplecov

``` ruby
if ENV['RCOV']
  require 'simplecov'
  SimpleCov.start
end
```

!SLIDE

}}} images/simplecov.png

!SLIDE

# Спасибо!
## Вопросы?
## @killthekitten, [http://killthekitten.github.io/testing_from_scratch_talk/](http://killtekitten.github.io/testing_from_scratch_talk/)

!NOTES

 * a note
