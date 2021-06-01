# Що таке Angular?
Angular - написаний на TypeScript front-end фреймворк з відкритим кодом. Як платформа, Angular включає:

- Структура на основі компонентів для побудови масштабованих веб-додатків
- Колекція добре інтегрованих бібліотек, що охоплюють широкий спектр функцій, включаючи маршрутизацію, управління формами, зв'язок клієнт-сервер, тощо
- Набір інструментів розробника, які допоможуть вам розробити, побудувати, протестувати та оновити ваш код

За допомогою Angular ви використовуєте платформу, яка може масштабуватися від проектів одного розробника до додатків на рівень підприємств. Angular призначений для максимально спрощення оновлення, тому ви можете скористатися перевагами останніх розробок з мінімальними зусиллями. Найкраще з усього є те, що екосистема Angular складається з різноманітної групи з понад 1,7 мільйона розробників, авторів бібліотек та творців контенту.

# Додатки Angular: Основи
## Компоненти
Компоненти - це будівельні блоки, які складають додаток. Компонент включає клас TypeScript із декоратором @Component (), шаблоном HTML та стилями. Декоратор @Component () визначає таку інформацію, що стосується конкретної Angular інформації:

- **Селектор CSS** визначає як компонент використовується в шаблоні. Елементи HTML у вашому шаблоні, які відповідають цьому селектору, стають екземплярами компонента.
- **Шаблон HTML** вказує Angular як відображати компонент.
- Необов’язковий **набір стилів CSS** визначає вигляд елементів HTML шаблону.

Далі наведено мінімальний кутовий компонент.

```
import { Component } from '@angular/core';

@Component({
  selector: 'hello-world',
  template: `
    <h2>Hello World</h2>
    <p>This is my first component!</p>
    `,
})
export class HelloWorldComponent {
  // The code in this class drives the component's behavior.
}
```
Щоб використати цей компонент, впишіть в шаблоні:
```
<hello-world></hello-world>
```
Коли Angular відображає цей компонент, отриманий DOM виглядає так:
```
<hello-world>
    <h2>Hello World</h2>
    <p>This is my first component!</p>
</hello-world>
```
Модель компонентів Angular пропонує потужну інкапсуляцію та інтуїтивно зрозумілу структуру додатків. Компоненти також полегшують програму для модульного тестування та можуть покращити загальну читабельність вашого коду.

Для отримання додаткової інформації про те, що можна робити з компонентами, див. розділ [Components](https://angular.io/guide/component-overview).

## Шаблони
Кожен компонент має HTML-шаблон, який декларує спосіб відображення цього компонента. Ви визначаєте цей шаблон або вбудовано, або шляхом шляху до файлу.

Angular розширює HTML додатковим синтаксисом, який дозволяє вставляти динамічні значення з вашого компонента. Angular автоматично оновлює відтворений DOM, коли змінюється стан вашого компонента. Однією із програм цієї функції є вставка динамічного тексту, як показано в наступному прикладі.
``` 
<p>{{ message }}</p>
```
Значення повідомлення надходить із класу компонентів:
``` 
import { Component } from '@angular/core';

@Component ({
  selector: 'hello-world-interpolation',
  templateUrl: './hello-world-interpolation.component.html'
})
export class HelloWorldInterpolationComponent {
    message = 'Hello, World!';
}
```
Коли програма завантажує компонент та його шаблон, користувач бачить таке:
``` 
<p>Hello, World!</p>
```
Зверніть увагу на використання подвійних фігурних дужок - вони доручають Angular інтерполювати вміст усередині них.

Angular також підтримує прив'язку властивостей, щоб допомогти вам встановити значення для властивостей та атрибутів елементів HTML і передати значення логіці презентації вашого додатка.
``` 
<p [id]="sayHelloId" [style.color]="fontColor">You can set my color in the component!</p>
```
Зверніть увагу на використання квадратних дужок - цей синтаксис вказує на те, що ви прив’язуєте властивість або атрибут до значення в класі компонента.

Ви також можете оголосити слухачам подій слухати та реагувати на дії користувача, такі як натискання клавіш, рухи миші, клацання та дотики. Ви оголошуєте прослуховувач подій, вказуючи в дужках назву події:
``` 
<button (click)="sayMessage()" [disabled]="canClick">Trigger alert message</button>
```
Попередній приклад викликає метод, який визначено в класі компонентів:
``` 
sayMessage() {
    alert(this.message);
}
```
Нижче наведено приклад інтерполяції та прив’язок у шаблоні Angular:
``` 
import { Component } from '@angular/core';

@Component ({
  selector: 'hello-world-bindings',
  templateUrl: './hello-world-bindings.component.html'
})
export class HelloWorldBindingsComponent {
    fontColor = 'blue';
    sayHelloId = 1;
    canClick = false;
    message = 'Hello, World';
    sayMessage() {
        alert(this.message);
    }
}
```
Ви можете додати додаткову функціональність до своїх шаблонів за допомогою [директив](https://angular.io/guide/built-in-directives). Найпопулярнішими директивами Angular є `*ngIf` та `*ngFor`. Ви можете використовувати директиви для виконання різноманітних завдань, таких як динамічне змінення структури DOM. А також ви можете створити власні власні директиви, щоб створити чудовий досвід користування.

Наступний код є прикладом директиви `*ngIf`.
```
import { Component } from '@angular/core';

@Component({
    selector: 'hello-world-ngif',
    templateUrl: './hello-world-ngif.component.html'
  })
export class HelloWorldNgIfComponent {
  message = 'I\'m read only!';
  canEdit = false;

  onEditClick() {
    this.canEdit = !this.canEdit;
    if (this.canEdit) {
      this.message = 'You can edit me!';
    } else {
      this.message = 'I\'m read only!';
    }
  }
}
```
Декларативні шаблони Angular дозволяють чітко відокремити логіку програми від її презентації. Шаблони базуються на стандартному HTML, тому їх легко створювати, підтримувати та оновлювати.

Щоб отримати докладнішу інформацію про те, що можна робити з шаблонами, див. розділ [Templates](https://angular.io/guide/template-syntax).

## Ведення залежності
Введення залежностей дозволяє оголосити залежності класів TypeScript, не дбаючи про їх створення. Натомість Angular обробляє інстанцію замість вас. Цей шаблон дизайну дозволяє писати більш перевірений та гнучкий код. Незважаючи на те, що розуміння введення залежності не є критичним для початку використання Angular, ми настійно рекомендуємо це як найкращу практику, і багато аспектів Angular певною мірою цим користуються.

Щоб проілюструвати, як працює введення залежностей, розглянемо наступний приклад. Перший файл, `logger.service.ts`, визначає клас `Logger`. Цей клас містить функцію `writeCount`, яка реєструє номер на консолі.
```
import { Injectable } from '@angular/core';

@Injectable({providedIn: 'root'})
export class Logger {
  writeCount(count: number) {
    console.warn(count);
  }
}
```
Далі файл `hello-world-di.component.ts` визначає компонент Angular. Цей компонент містить кнопку, яка використовує функцію `writeCount` класу `Logger`. Щоб отримати доступ до цієї функції, `Logger` служба  вводиться в клас `HelloWorldDI`, додаючи `private logger: Logger` до конструктора.
```
import { Component } from '@angular/core';
import { Logger } from '../logger.service';

@Component({
  selector: 'hello-world-di',
  templateUrl: './hello-world-di.component.html'
})
export class HelloWorldDependencyInjectionComponent  {
  count = 0;

  constructor(private logger: Logger) {
  }

  onLogMe() {
    this.logger.writeCount(this.count);
    this.count++;
  }
}
```
Для отримання додаткової інформації про введення залежності та Angular див. розділ  [Dependency injection in Angular](https://angular.io/guide/dependency-injection).

# Angular CLI
CLI Angular - це найшвидший, найпростіший і рекомендований спосіб розробки програм Angular. Angular CLI полегшує ряд завдань. Ось кілька прикладів:


|ng build      |Компілює програму Angular у вихідний каталог. |
| :------------- |:------------------| 
| **ng serve**  | **Створює та обслуговує вашу програму, відновлюючи зміни файлів.**|
| **ng generate**  | **Створює або модифікує файли на основі схеми.**|
| **ng test**   | **Запускає модульні тести за даним проектом.**|
| **ng e2e**  | **Створює та обслуговує програму Angular, а потім запускає наскрізні тести.**|

Ви знайдете Angular CLI цінним інструментом для розробки своїх додатків.

Для отримання додаткової інформації про кутовий CLI див. розділ [CLI Reference](https://angular.io/cli).

# Початок роботи c Angular
Для роботи з Angular необхідно встановити сервер Node.js і пакетний менеджер npm, якщо вони відсутні на робочій машині. Для установки можна використовувати [програму установки Node.js](https://nodejs.org/uk/).

![Node.js](C:\Users\Lumen\Documents\GitHub\Angular\node.jpg)

 Разом з сервером вона також встановить і npm. При цьому особливого якогось знання для роботи з NodeJS і npm не потрібно.

Установка Typescript
Для установки Typescript відкриємо консоль/командний рядок і виконаємо в ній наступну команду: 
```
npm install typescript --save-dev
```

# Установка Angular CLI
Для компіляції додатка ми будемо використовувати інфраструктуру Angular CLI. Angular CLI спрощує створення додатка, його компіляцію. Angular CLI поширюється як пакет npm, тому для його використання його необхідно спочатку встановити.

Для установки Angular CLI відкриємо консоль/командний рядок і виконаємо в ній наступну команду: `npm install -g @angular/cli`

Дана команда встановить пакет @angular/cli в якості глобального модуля, тому в подальшому при створенні новий проектів Angular його не буде потрібно встановлювати заново.

Ту ж команду можна використовувати для оновлення Angluar CLI при виході нової версії фреймворка. Перевірити версію CLI можна в командному рядку/консолі за допомогою команди: `ng version`

# Створення нового проекту:
Angular CLI дозволяє легко створити проект командою: `ng new *Назва проекту*`. Команда запитує інформацію про функції, які потрібно включити в початковий проект програми. Прийміть значення за замовчуванням, натиснувши клавішу Enter або Return. Інтерфейс CLI Angular встановлює необхідні пакети Angular npm та інші залежності. Це може зайняти кілька хвилин.

Запуск проекту
Перейдіть до каталогу робочої області та запустіть програму.

1. `cd *Назва проекту*`
1. `ng serve --open`

Команда ng serve створює додаток, запускає сервер розробки, переглядає вихідні файли та відновлює додаток під час внесення змін до цих файлів. Прапор `--open` відкриває браузер до http://localhost:4200/.

## Перший додаток на Angular
Створимо на жорсткому диску папку програми. Шлях вона буде називатися `purchaseApp`. У цій папці створимо новий файл `package.json` наступного змісту:
```
{
  "name": "helloapp",
  "version": "1.0.0",
  "description": "First Angular 7 Project",
  "author": "Eugene Popov <metanit.com>",
  "scripts": {
    "dev": "webpack-dev-server --hot --open",
    "build": "webpack"
  },
  "dependencies": {
    "@angular/common": "~7.0.0",
    "@angular/compiler": "~7.0.0",
    "@angular/core": "~7.0.0",
    "@angular/forms": "~7.0.0",
    "@angular/platform-browser": "~7.0.0",
    "@angular/platform-browser-dynamic": "~7.0.0",
    "@angular/router": "~7.0.0",
    "core-js": "^2.5.7",
    "rxjs": "^6.3.3",
    "zone.js": "^0.8.26"
  },
  "devDependencies": {
    "@types/node": "^10.12.0",
    "typescript": "^3.0.0",
    "webpack": "^4.21.0",
    "webpack-cli": "^3.1.2",
    "webpack-dev-server": "^3.1.9",
    "angular2-template-loader": "^0.6.2",
    "awesome-typescript-loader": "^5.2.1",
    "uglifyjs-webpack-plugin": "^2.0.0"
  }
}
```
Також додамо в папку проекту новий файл `tsconfig.json`:
```
{
  "compilerOptions": {
    "target": "es5",
    "module": "es2015",
    "moduleResolution": "node",
    "sourceMap": true,
    "emitDecoratorMetadata": true,
    "experimentalDecorators": true,
    "lib": ["es2015", "dom"],
    "noImplicitAny": true,
    "suppressImplicitAnyIndexErrors": true,
    "typeRoots": ["node_modules/@types/"]
  },
  "exclude": ["node_modules"]
}
```
Файл `package.json` встановлює пакети і залежності, які будуть використовуватися проектом.

Файл `tsconfig.json` встановлює конфігурацію для компілятора TypeScript.

Для складання проекту будемо використовувати збирач Webpack, тому також визначимо в папці проекту файл `webpack.config.js`:
```
var path = require('path')
var webpack = require('webpack')
var UglifyJSPlugin = require('uglifyjs-webpack-plugin') // плагин минимизации
module.exports = {
  entry: {
    polyfills: './src/polyfills.ts',
    app: './src/main.ts',
  },
  output: {
    path: path.resolve(__dirname, './public'), // путь к каталогу выходных файлов — папка public
    publicPath: '/public/',
    filename: '[name].js', // название создаваемого файла
  },
  resolve: {
    extensions: ['.ts', '.js'],
  },
  module: {
    rules: [
      //загрузчик для ts
      {
        test: /\.ts$/, // определяем тип файлов
        use: [
          {
            loader: 'awesome-typescript-loader',
            options: {
              configFileName: path.resolve(
                __dirname,
                'tsconfig.json'
              ),
            },
          },
          'angular2-template-loader',
        ],
      },
    ],
  },
  plugins: [
    new webpack.ContextReplacementPlugin(
      /angular(\\|\/)core/,
      path.resolve(__dirname, 'src'), // каталог с исходными файлами
      {} // карта маршрутов
    ),
    new UglifyJSPlugin(),
  ],
}
```
Після створення цих трьох файлів в папці проекту відкриємо командний рядок (термінал) і перейдемо в ній до папки проекту за допомогою команди `cd`:
```
C:\WINDOWS\system32>cd C:\angular2\purchaseApp
```
І потім виконаємо команду `npm install`, яка встановить всі необхідні модулі:
```
C:\angular2\purchaseApp>npm install
```
Після виконання цієї команди в папці проекту повинна з'явитися підпапка `node_modules`, яка містить всі використовувані залежно та пакети.

Потім створимо в папці проекту каталог `src`, а в цьому каталозі визначимо папку `app`.

В каталог `src / app` додамо новий файл, який назвемо `app.component.ts` і який буде мати наступний код:
```
import { Component } from '@angular/core'

class Item {
  purchase: string
  done: boolean
  price: number

  constructor(purchase: string, price: number) {
    this.purchase = purchase
    this.price = price
    this.done = false
  }
}

@Component({
  selector: 'purchase-app',
  template: `
    <div class="page-header">
      <h1>Список покупок</h1>
    </div>
    <div class="panel">
      <div class="form-inline">
        <div class="form-group">
          <div class="col-md-8">
            <input
              class="form-control"
              [(ngModel)]="text"
              placeholder="Название"
            />
          </div>
        </div>
        <div class="form-group">
          <div class="col-md-6">
            <input
              type="number"
              class="form-control"
              [(ngModel)]="price"
              placeholder="Цена"
            />
          </div>
        </div>
        <div class="form-group">
          <div class="col-md-offset-2 col-md-8">
            <button
              class="btn btn-default"
              (click)="addItem(text, price)"
            >
              Добавить
            </button>
          </div>
        </div>
      </div>
      <table class="table table-striped">
        <thead>
          <tr>
            <th>Предмет</th>
            <th>Цена</th>
            <th>Куплено</th>
          </tr>
        </thead>
        <tbody>
          <tr *ngFor="let item of items">
            <td>{{ item.purchase }}</td>
            <td>{{ item.price }}</td>
            <td>
              <input
                type="checkbox"
                [(ngModel)]="item.done"
              />
            </td>
          </tr>
        </tbody>
      </table>
    </div>
  `,
})
export class AppComponent {
  items: Item[] = [
    { purchase: 'Хлеб', done: false, price: 15.9 },
    { purchase: 'Масло', done: false, price: 60 },
    { purchase: 'Картофель', done: true, price: 22.6 },
    { purchase: 'Сыр', done: false, price: 310 },
  ]
  addItem(text: string, price: number): void {
    if (text == null || text.trim() == '' || price == null)
      return
    this.items.push(new Item(text, price))
  }
}
```
Першим рядком тут імпортується функціональність компонента з `@ angular / core`.

Для роботи нам буде потрібно допоміжний клас `Item`. Цей клас містить три поля: `purchase` (назва покупки), `done` (чи зроблена покупка) і `price` (її ціна).

У самому класі компонента визначається початковий список покупок, який буде виводитися на сторінку:
```
items: Item[] =
    [
        { purchase: "Хлеб", done: false, price: 15.9 },
        { purchase: "Масло", done: false, price: 60 },
        { purchase: "Картофель", done: true, price: 22.6 },
        { purchase: "Сыр", done: false, price:310 }
    ];
```
І також в класі визначено метод додавання в цей список:
```
addItem(text: string, price: number): void {

    if(text==null || text.trim()=="" || price==null)
        return;
    this.items.push(new Item(text, price));
}
```
Для виведення покупок тут визначено великий шаблон. 

У самому шаблоні для виведення даних з масиву items в таблицю передбачена директива:
```
*ngFor="let item of items"
```
Крім того, зверху від таблиці розташована форма для введення нового об'єкта `Item`. А до натискання кнопки прив'язаний метод `addItem ()` компонента.

Щоб задіяти цей компонент, додамо в каталог `src / app` файл модуля `app.module.ts`:
```
import { NgModule } from '@angular/core'
import { BrowserModule } from '@angular/platform-browser'
import { FormsModule } from '@angular/forms'
import { AppComponent } from './app.component'
@NgModule({
  imports: [BrowserModule, FormsModule],
  declarations: [AppComponent],
  bootstrap: [AppComponent],
})
export class AppModule {}
```
Рівнем вище в каталозі src визначимо файл main.ts для запуску проекту:
```
import { platformBrowserDynamic } from '@angular/platform-browser-dynamic'
import { AppModule } from './app/app.module'
const platform = platformBrowserDynamic()
platform.bootstrapModule(AppModule)
```
Також в каталозі `src` визначимо файл `polyfills.ts`, який необхідний для запуску програми:
```
import 'core-js/es6'
// для поддержки Reflect Api
import 'core-js/es7/reflect'
// zone используется angular
import 'zone.js/dist/zone'
```
В кінці визначимо головну сторінку `index.html` в кореневій папці проекту:
```
<!DOCTYPE html>
<html>
  <head>
    <meta charset="utf-8" />
    <title>Приложение покупок</title>
    <meta
      name="viewport"
      content="width=device-width, initial-scale=1"
    />
    <link
      rel="stylesheet"
      href="https://maxcdn.bootstrapcdn.com/bootstrap/3.3.2/css/bootstrap.min.css"
    />
  </head>
  <body>
    <purchase-app>Загрузка...</purchase-app>
    <script src="public/polyfills.js"></script>
    <script src="public/app.js"></script>
  </body>
</html>
```
В результаті у нас вийде наступна структура проекту:

![Структура](C:\Users\Lumen\Documents\GitHub\Angular\purchaseApp\first-app-1.png)

Запустимо проект. Для цього в командному рядку (терміналі) перейдемо до папки проекту і потім виконаємо команду 'npm run dev':
```
C:\angular2\purchaseApp>npm run dev
```

![Додаток](C:\Users\Lumen\Documents\GitHub\Angular\purchaseApp\first-app-2.png)

Готово!

### Виконала: Долготьор Алевтина 

### Група: ІО-92