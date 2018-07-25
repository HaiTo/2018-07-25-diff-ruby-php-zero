## Rubyist dive to PHP
### Rubyist の車窓から

---
## ~~Rubyist dive to PHP~~
### Rubyist の車窓から

---

## $ diff ruby php //-> ?0
### Rubyist の車窓から

面白いスライドが作れなかったので  
当たり障りないdiffの話をします  

---

## About me

Name: HaiTo  
2014/5 : HaiTo.join(Sansan, state: :intern)  
2015/4 : HaiTo.change(state: :employee)  
2017/1 : HaiTo.change(job: MoneyForward)  
2018/6 : HaiTo->changeJob(Mercari)  
  
Hobby: Game (League of Legends)  
  
PHP勉強会初参加ですん  
  
---

## Rubyist からみたPHP初歩編
```ruby
receiver.method(args)
Klass.new(args)
```

```php
$receiver->method(args)
new Klass(args)
```
@[1, 3]
@[2, 4]

Ruby は `new` すらClassClassのメソッドなので  
```ruby
klass = [HaiTo, Linux].sample
klass.new #=> HaiTo.new or Linux.new になる
```
という感じでFactoryとかを作るのがお手軽  

---

## Rubyist からみたPHP初歩編
```ruby
a = [1,2,3]
a.map{|i| i*2 } #=> [2,4,6]
```

```php
$a = [1,2,3];
$res = [];
foreach($a as $i) { $res[] = $i * 2 } // $res => [2,4,6]
```
@[1, 3, 4]
@[2, 5]
`array_map` は無名関数を配列数分生成するのでパフォーマンス的に弱いらしいのでこっち  

---

## Rubyist からみたPHP初歩編
```ruby
module M
  def say; puts 'hi'; end
end
class K
  include M
end
K.new.say #=> 'hi'
```

```php
trait M {
  public function say(){ print('hi'.PHP_EOL); }
}
class K {
  use M;
}
(new K())->say() #=> 'hi'
```
@[1-3, 8-10]
@[4-6, 11-13]
@[7, 14]

---

# そんなかわらんやんけ！
# やったー！

---
## Rubyist からみたPHP虚空編
```ruby
1 + 2 #=> 3
1.+(2) #=> 3 
# つまり 1->+(2)
```
1はリテラルながらもIntegerClassのInstanceで、 + もただのメソッド(語弊がある)  
Rubyの世界ではほぼ全てがObjectなので、よりOOPを強く意識することになる。  
> そしてOOPとは何かを人は永遠に問い続けることになるのだ  

---
## Rubyist からみたPHP黒魔術編
```ruby
class Numeric
  def to_s; 'デレデレデェェェン'; end
end
puits 1.to_s #=> デレデレデェェェン
```
PHPでも php extentions をいれるとできるが、それ不要でほぼ全てのクラスを再定義できる  
ActiveSupport/core-extがさいつよの例。書き心地がとても良くなる  

---

## AS/core-extの黒魔術たち

```ruby
hs = {name: 'haito', age: :secret}
hs.to_query #=> "name=haito&age=secret"

str = 'haito'.inquiry
str #=> 'haito'
str.linux? #=> false
str.haito? #=> true

[1,2].many? #=> true
[1,2].many?(&:odd?) #=> false
[1].many? #=> false
```

特にStringとかArray、Hashに対する拡張がエグい数ある  
一度慣れるとRubyで用意されているメソッドなのかRailsが拡張しているのか考えなくなる  

---

## 強力なClosureがほしいって話
```ruby
# def file.open(path, mode)
#   f = self._open(path, mode)
#   yield f if block_given?
#   self.close
# end
File.open(path, 'a') {|f| f.write('hello') }
```

`{...}` の中が `yield` の箇所で実行される。このBlock(≒無名関数||Closure)がRubyでは強力  
軽いし、簡単だし、なによりとても利便性が高い
```ruby
# Configuration pattern 
Airbrake.configure do |config|
  config.api_key = 'your_key_here'
end
```

---

## キーワード引数がほしいって話
```ruby
def func(name:, age:, options: {})
  self.update(
    name: name, age: age+10, options: options.slice(:hoge, :huga)
  )
end
func(age: 10, name: 'HaiTo')
```
順序考慮不要の引数。 `:` の後にデフォルト値も書けて、書くと `not required` になる  
phpだと `$options['age']` みたいに受け取るしかなくて明示性が低くて辛い。  
わりと普通にほしい。  
> DataTypeを作るとかもあるけど……Airbrake.configure do |config|
  config.api_key = 'your_key_here'
end

---

## おわりに
- そんなRubyもPHPも違いがない。表面的には書き心地の問題があるがその程度。重篤ではない。
- ただPHPはTypeDeclarationがある！やった！
- RubyもPHPもLightweightLanguageとしてGoとかRustとは違った美味しさで戦っていこう
- つまりPHPが書けるならRubyも書けるのでそこは実際には障壁にならなさそう
- つまりRubyistも採用できるぞ！やったね！


