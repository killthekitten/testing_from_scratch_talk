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

# Средняя температура по больнице

## Команда должна иметь примеры написания (всяких) спек

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

# Что тестируем?
## Helpers + Controllers + Models

!SLIDE

# Request Specs
## Очень эффективные, но медленные и проблемные
### Лучше иметь специально обученного человека

!SLIDE

# JS Testing
## Аналогично, эффективные и проблемные

!SLIDE left

# specs/models

* стейт машины
* валидации
  * should be_valid
  * should have(n).errors_on
  * match error message
* константы
* shoulda

!SLIDE

# specs/models/concerns

```ruby
require 'spec_helper'

class HasMatcher::Test
  include ActiveModel::Model
  include ActiveModel::Validations
  include HasMatcher

  attr_accessor :matcher_text
end

describe HasMatcher do
...
```
!SLIDE left

# specs/controllers

## Плюсы
+ максимально простые и эффективные
+ однотипные
+ прикрывают большое количество тылов: создание объекта, отображение, права доступа и т.п.
+ есть сессия и вьюха

!SLIDE left

# specs/controllers

## Минусы
- нет редиректов
- ничего не знают о JS
- ничего не знают о кнопках

!SLIDE

# specs/mailers

!SLIDE

# spec/models/helpers

+ Большое покрытие вьюхи
- Скорее всего, надо покрывать много условий

!SLIDE

# ability_spec.rb

!SLIDE

# Сторонние сервисы, API, OAuth

+ Искать стабы в README
+ webmock

!SLIDE

# Mailers, Async Workers

!SLIDE

# FactoryGirl

!SLIDE

# FactoryGirl
## Тоже нужно тестить

```ruby
# spec/factories_spec.rb

FactoryGirl.factories.map(&:name).each do |factory_name|
  describe "The #{factory_name} factory" do
    it 'is valid' do
      build(factory_name).should be_valid
    end
  end
end
```

```ruby
# Rakefile

desc 'Run factory specs.'
RSpec::Core::RakeTask.new(:factory_specs) do |t|
  t.pattern = './spec/factories_spec.rb'
end

task spec: :factory_specs
```

!SLIDE

# RSpec

+ let/set, ленивая загрузка
+ стабы, моки
+ spec_helper
+ синтаксический сахар
+ ссылка на документашку

!SLIDE

# RR

```ruby
# Flexmock
flexmock(User).should_receive(:find).with('42').and_return(jane)
# RSpec
User.should_receive(:find).with('42').and_return(jane)
# Mocha
User.expects(:find).with('42').returns { jane }
# rspec-mocks (using return value blocks)
User.should_receive(:find).with('42') { jane }
# RR
mock(User).find('42') { jane }
```

!SLIDE left

# Самостоятельное изучение для коллег

* codeschool.com/courses/rails-testing-for-zombies
* codeschool.com/courses/testing-with-rspec
* betterspecs.org (github.com/andreareginato/betterspecs/issues/20)
* betterspecs.org/#resources

!SLIDE left

# Займемся списыванием

* github.com/rails/rails
* github.com/gitlabhq/gitlabhq
* github.com/infews/keydown
* github.com/spree/spree
* github.com/errbit/errbit
* Любой большой опенсорс тоже подойдет

!SLIDE

# Спасибо!
## Вопросы?
## @killthekitten, [http://killthekitten.ru/testing_from_scratch_talk/](http://killtekitten.ru/testing_from_scratch_talk/)
