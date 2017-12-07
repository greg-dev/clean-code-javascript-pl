Original Repository: [ryanmcdermott/clean-code-javascript](https://github.com/ryanmcdermott/clean-code-javascript)

# Czysty kod JavaScript

## Spis treści
  1. [Wprowadzenie](#wprowadzenie)
  2. [Zmienne](#zmienne)
  3. [Funkcje](#funkcje)
  4. [Obiekty i struktury danych](#obiekty-i-struktury-danych)
  5. [Klasy](#klasy)
  6. [SOLID](#solid)
  7. [Testowanie](#testowanie)
  8. [Współbieżność](#współbieżność)
  9. [Obsługa błędów](#obsługa-błędów)
  10. [Formatowanie](#formatowanie)
  11. [Komentarze](#komentarze)
  12. [Tłumaczenie](#tłumaczenie)

<!--
## Introduction
![Humorous image of software quality estimation as a count of how many expletives
you shout when reading code](http://www.osnews.com/images/comics/wtfm.jpg)

Software engineering principles, from Robert C. Martin's book
[*Clean Code*](https://www.amazon.com/Clean-Code-Handbook-Software-Craftsmanship/dp/0132350882),
adapted for JavaScript. This is not a style guide. It's a guide to producing
[readable, reusable, and refactorable](https://github.com/ryanmcdermott/3rs-of-software-architecture) software in JavaScript.

Not every principle herein has to be strictly followed, and even fewer will be
universally agreed upon. These are guidelines and nothing more, but they are
ones codified over many years of collective experience by the authors of
*Clean Code*.

Our craft of software engineering is just a bit over 50 years old, and we are
still learning a lot. When software architecture is as old as architecture
itself, maybe then we will have harder rules to follow. For now, let these
guidelines serve as a touchstone by which to assess the quality of the
JavaScript code that you and your team produce.

One more thing: knowing these won't immediately make you a better software
developer, and working with them for many years doesn't mean you won't make
mistakes. Every piece of code starts as a first draft, like wet clay getting
shaped into its final form. Finally, we chisel away the imperfections when
we review it with our peers. Don't beat yourself up for first drafts that need
improvement. Beat up the code instead!
-->
## Wprowadzenie
![Humorystyczny obrazek przedstawiający ocenę jakości oprogramowania za pomocą ilości przekleństw
wykrzyczanych podczas czytania kodu](http://www.osnews.com/images/comics/wtfm.jpg)

Zasady inżynierii oprogramowania z książki Roberta C. Martina
[*Czysty kod*](https://www.amazon.com/Clean-Code-Handbook-Software-Craftsmanship/dp/0132350882),
dostosowane do języka JavaScript. Nie są to wytyczne dotyczące stylu. To wytyczne do tworzenia
[czytelnego, prostego w refaktoryzacji i wielokrotnym użyciu](https://github.com/ryanmcdermott/3rs-of-software-architecture)
oprogramowania w języku JavaScript.

Nie każda z podanych tu zasad musi być ściśle przestrzegana i nie wszystkie z nich będą
powszechnie przyjęte. To nic więcej, niż wskazówki zebrane dzięki wieloletniemu 
doświadczeniu autorów *Czystego kodu*.

Inżynieria oprogramowania ma trochę ponad 50 lat i nadal wiele się uczymy.
Gdy architektura oprogramowania będzie tak stara, jak sama architektura,
wtedy może będziemy mieli trudniejsze zasady do przestrzegania. Na razie niech te
wytyczne służą jako podstawa do oceny jakości kodu JavaScript, który Ty i Twój zespół tworzycie.

Jeszcze jedno: poznanie zasad nie zrobi z Ciebie lepszego programisty w mgnieniu oka,
a wieloletnia praca zgodnie z nimi nie sprawi, że przestaniesz popełniać błędy.
Każdy kawałek kodu zaczyna się od wstępnego szkicu i jest jak mokra glina formowana
do ostatecznego kształtu. Wreszcie niczym rzeźbiarz dłutem usuwamy wszelkie niedoskonałości
podczas przeglądu kodu wspólnie z kolegami. Nie zadręczaj się wstępnymi szkicami wymagającymi poprawek.
Zamiast tego męcz kod!

<!--
## **Variables**
### Use meaningful and pronounceable variable names
-->
## **Zmienne**
### Używaj znaczących i wymawialnych nazw zmiennych

**Źle:**
```javascript
const yyyymmdstr = moment().format('YYYY/MM/DD');
```

**Dobrze:**
```javascript
const currentDate = moment().format('YYYY/MM/DD');
```
**[⬆ powrót na początek](#spis-treści)**

<!--
### Use the same vocabulary for the same type of variable
-->
### Używaj tego samego słownictwa dla tego samego rodzaju danych

**Źle:**
```javascript
getUserInfo();
getClientData();
getCustomerRecord();
```

**Dobrze:**
```javascript
getUser();
```
**[⬆ powrót na początek](#spis-treści)**

<!--
### Use searchable names
We will read more code than we will ever write. It's important that the code we
do write is readable and searchable. By *not* naming variables that end up
being meaningful for understanding our program, we hurt our readers.
Make your names searchable. Tools like
[buddy.js](https://github.com/danielstjules/buddy.js) and
[ESLint](https://github.com/eslint/eslint/blob/660e0918933e6e7fede26bc675a0763a6b357c94/docs/rules/no-magic-numbers.md)
can help identify unnamed constants.
-->
### Używaj odnajdywalnych nazw
Będziemy czytać więcej kodu, niż kiedykolwiek napiszemy. Ważne jest, aby nasz kod
był czytelny i przeszukiwalny. *Nie* nazywając zmiennych, mających znaczenie
dla zrozumienia naszego programu, krzywdzimy czytających.
Spraw, by Twoje nazwy były odnajdywalne. Narzędzia takie jak
[buddy.js](https://github.com/danielstjules/buddy.js) i
[ESLint](https://github.com/eslint/eslint/blob/660e0918933e6e7fede26bc675a0763a6b357c94/docs/rules/no-magic-numbers.md)
mogą pomóc zidentyfikować nienazwane stałe.

**Źle:**
```javascript
// Czym do diaska jest 86400000?
setTimeout(blastOff, 86400000);

```

**Dobrze:**
```javascript
// Zadeklaruj ją jako nazwaną stałą, używając wielkich liter.
const MILLISECONDS_IN_A_DAY = 86400000;

setTimeout(blastOff, MILLISECONDS_IN_A_DAY);

```
**[⬆ powrót na początek](#spis-treści)**

<!--
### Use explanatory variables
-->
### Używaj zmiennych wyjaśniających

**Źle:**
```javascript
const address = 'One Infinite Loop, Cupertino 95014';
const cityZipCodeRegex = /^[^,\\]+[,\\\s]+(.+?)\s*(\d{5})?$/;
saveCityZipCode(address.match(cityZipCodeRegex)[1], address.match(cityZipCodeRegex)[2]);
```

**Dobrze:**
```javascript
const address = 'One Infinite Loop, Cupertino 95014';
const cityZipCodeRegex = /^[^,\\]+[,\\\s]+(.+?)\s*(\d{5})?$/;
const [, city, zipCode] = address.match(cityZipCodeRegex) || [];
saveCityZipCode(city, zipCode);
```
**[⬆ powrót na początek](#spis-treści)**

<!--
### Avoid Mental Mapping
Explicit is better than implicit.
-->
### Unikaj map mentalnych
Jasne jest lepsze niż niejasne.

**Źle:**
```javascript
const locations = ['Austin', 'New York', 'San Francisco'];
locations.forEach((l) => {
  doStuff();
  doSomeOtherStuff();
  // ...
  // ...
  // ...
  // Czekaj, czym było `l`?
  dispatch(l);
});
```

**Dobrze:**
```javascript
const locations = ['Austin', 'New York', 'San Francisco'];
locations.forEach((location) => {
  doStuff();
  doSomeOtherStuff();
  // ...
  // ...
  // ...
  dispatch(location);
});
```
**[⬆ powrót na początek](#spis-treści)**

<!--
### Don't add unneeded context
If your class/object name tells you something, don't repeat that in your
variable name.
-->
### Nie dodawaj niepotrzebnego kontekstu
Jeśli nazwa Twojej klasy/obiektu coś mówi, nie powtarzaj tego w nazwie zmiennej.

**Źle:**
```javascript
const Car = {
  carMake: 'Honda',
  carModel: 'Accord',
  carColor: 'Blue'
};

function paintCar(car) {
  car.carColor = 'Red';
}
```

**Dobrze:**
```javascript
const Car = {
  make: 'Honda',
  model: 'Accord',
  color: 'Blue'
};

function paintCar(car) {
  car.color = 'Red';
}
```
**[⬆ powrót na początek](#spis-treści)**

<!--
### Use default arguments instead of short circuiting or conditionals
Default arguments are often cleaner than short circuiting. Be aware that if you
use them, your function will only provide default values for `undefined`
arguments. Other "falsy" values such as `''`, `""`, `false`, `null`, `0`, and
`NaN`, will not be replaced by a default value.
-->
### Używaj domyślnych wartości argumentów zamiast wykonań warunkowych lub warunków
Domyślne wartości argumentów są zwykle jaśniejsze niż wykonania warunkowe. Pamiętaj, że jeśli
ich użyjesz, Twoja funkcja dostarczy domyślne wartości tylko dla argumentów niezdefiniowanych (`undefined`). Inne "fałszywe" wartości, takie jak `''`, `""`, `false`, `null`, `0` i
`NaN`, nie będą zastąpione wartością domyślną.

**Źle:**
```javascript
function createMicrobrewery(name) {
  const breweryName = name || 'Hipster Brew Co.';
  // ...
}

```

**Dobrze:**
```javascript
function createMicrobrewery(breweryName = 'Hipster Brew Co.') {
  // ...
}

```
**[⬆ powrót na początek](#spis-treści)**

<!--
## **Functions**
### Function arguments (2 or fewer ideally)
Limiting the amount of function parameters is incredibly important because it
makes testing your function easier. Having more than three leads to a
combinatorial explosion where you have to test tons of different cases with
each separate argument.

One or two arguments is the ideal case, and three should be avoided if possible.
Anything more than that should be consolidated. Usually, if you have
more than two arguments then your function is trying to do too much. In cases
where it's not, most of the time a higher-level object will suffice as an
argument.

Since JavaScript allows you to make objects on the fly, without a lot of class
boilerplate, you can use an object if you are finding yourself needing a
lot of arguments.

To make it obvious what properties the function expects, you can use the ES2015/ES6
destructuring syntax. This has a few advantages:

1. When someone looks at the function signature, it's immediately clear what
properties are being used.
2. Destructuring also clones the specified primitive values of the argument
object passed into the function. This can help prevent side effects. Note:
objects and arrays that are destructured from the argument object are NOT
cloned.
3. Linters can warn you about unused properties, which would be impossible
without destructuring.
-->
## **Funkcje**
### Parametry funkcji (najlepiej 2 lub mniej)
Ograniczanie ilości parametrów funkcji jest niezwykle ważne, gdyż czyni
testowanie Twojej funkcji prostszym. Mając więcej niż trzy, prowadzisz do
eksplozji kombinatorycznej, w której musisz przetestować masę różnych przypadków
osobno z każdym kolejnym parametrem.

Najlepiej, jeśli jest jeden lub dwa parametry, trzy powinny być już w miarę możliwości unikane.
Większa ilość powinna być skonsolidowana. Zwykle, gdy masz
więcej niż dwa parametry, Twoja funkcja próbuje zrobić za dużo. W przypadkach,
gdy tak nie jest, zazwyczaj obiekt wyższego rzędu będzie wystarczającym
parametrem.

Jako że JavaScript pozwala tworzyć obiekty w locie i bez konieczności użycia kodu
związanego z klasami, zawsze możesz użyć obiektu, gdy czujesz, że potrzebujesz
dużo parametrów.

Aby było oczywistym, jakich parametrów oczekuje funkcja, możesz użyć destrukturyzacji
wprowadzonej w wersji ES2015/ES6. Ma to kilka zalet:

1. Gdy ktoś popatrzy na sygnaturę funkcji, od razu będzie mieć jasność, jakie
właściwości będą wykorzystywane.
2. Destrukturyzacja klonuje określone prymitywne wartości argumentów obiektu
przekazywanego do funkcji. Może to pomóc w uniknięciu efektów ubocznych. Uwaga:
obiekty i tablice będące wynikiem destrukturyzacji argumentów obiektu NIE będą
klonowane.
3. Lintery mogą ostrzec Cię przed nieużywanymi zmiennymi, co będzie niemożliwe
bez destrukturyzacji.

**Źle:**
```javascript
function createMenu(title, body, buttonText, cancellable) {
  // ...
}
```

**Dobrze:**
```javascript
function createMenu({ title, body, buttonText, cancellable }) {
  // ...
}

createMenu({
  title: 'Foo',
  body: 'Bar',
  buttonText: 'Baz',
  cancellable: true
});
```
**[⬆ powrót na początek](#spis-treści)**


<!--
### Functions should do one thing
This is by far the most important rule in software engineering. When functions
do more than one thing, they are harder to compose, test, and reason about.
When you can isolate a function to just one action, they can be refactored
easily and your code will read much cleaner. If you take nothing else away from
this guide other than this, you'll be ahead of many developers.
-->
### Funkcja powinna wykonywać tylko jedno zadanie
Jest to zdecydowanie najważniejsza zasada w inżynierii oprogramowania. Gdy funkcje
wykonują więcej niż jedno zadanie, są trudniejsze w kompozycji, testowaniu i zrozumieniu.
Jeśli możesz ograniczyć działanie funkcji do tylko jednego zadania, będzie ona
prostsza w refaktoryzacji, a Twój kod czytelniejszy. Nawet jeśli nie wyniesiesz
z tego przewodnika nic więcej poza tym, to i tak będziesz do przodu w stosunku do wielu deweloperów.

**Źle:**
```javascript
function emailClients(clients) {
  clients.forEach((client) => {
    const clientRecord = database.lookup(client);
    if (clientRecord.isActive()) {
      email(client);
    }
  });
}
```

**Dobrze:**
```javascript
function emailActiveClients(clients) {
  clients
    .filter(isActiveClient)
    .forEach(email);
}

function isActiveClient(client) {
  const clientRecord = database.lookup(client);
  return clientRecord.isActive();
}
```
**[⬆ powrót na początek](#spis-treści)**

<!--
### Function names should say what they do
-->
### Nazwy funkcji powinny mówić co one robią

**Źle:**
```javascript
function addToDate(date, month) {
  // ...
}

const date = new Date();

// Z nazwy funkcji trudno wywnioskować, co jest dodawane
addToDate(date, 1);
```

**Dobrze:**
```javascript
function addMonthToDate(month, date) {
  // ...
}

const date = new Date();
addMonthToDate(1, date);
```
**[⬆ powrót na początek](#spis-treści)**

<!--
### Functions should only be one level of abstraction
When you have more than one level of abstraction your function is usually
doing too much. Splitting up functions leads to reusability and easier
testing.
-->
### Funkcje powinny być tylko jednym poziomem abstrakcji
Gdy masz więcej niż jeden poziom abstrakcji, Twoja funkcja zwykle robi za dużo.
Podzielenie funkcji umożliwi wielokrotne użycie kodu i ułatwi jego testowanie.

**Źle:**
```javascript
function parseBetterJSAlternative(code) {
  const REGEXES = [
    // ...
  ];

  const statements = code.split(' ');
  const tokens = [];
  REGEXES.forEach((REGEX) => {
    statements.forEach((statement) => {
      // ...
    });
  });

  const ast = [];
  tokens.forEach((token) => {
    // lex...
  });

  ast.forEach((node) => {
    // parse...
  });
}
```

**Dobrze:**
```javascript
function tokenize(code) {
  const REGEXES = [
    // ...
  ];

  const statements = code.split(' ');
  const tokens = [];
  REGEXES.forEach((REGEX) => {
    statements.forEach((statement) => {
      tokens.push( /* ... */ );
    });
  });

  return tokens;
}

function lexer(tokens) {
  const ast = [];
  tokens.forEach((token) => {
    ast.push( /* ... */ );
  });

  return ast;
}

function parseBetterJSAlternative(code) {
  const tokens = tokenize(code);
  const ast = lexer(tokens);
  ast.forEach((node) => {
    // parse...
  });
}
```
**[⬆ powrót na początek](#spis-treści)**

<!--
### Remove duplicate code
Do your absolute best to avoid duplicate code. Duplicate code is bad because it
means that there's more than one place to alter something if you need to change
some logic.

Imagine if you run a restaurant and you keep track of your inventory: all your
tomatoes, onions, garlic, spices, etc. If you have multiple lists that
you keep this on, then all have to be updated when you serve a dish with
tomatoes in them. If you only have one list, there's only one place to update!

Oftentimes you have duplicate code because you have two or more slightly
different things, that share a lot in common, but their differences force you
to have two or more separate functions that do much of the same things. Removing
duplicate code means creating an abstraction that can handle this set of
different things with just one function/module/class.

Getting the abstraction right is critical, that's why you should follow the
SOLID principles laid out in the *Classes* section. Bad abstractions can be
worse than duplicate code, so be careful! Having said this, if you can make
a good abstraction, do it! Don't repeat yourself, otherwise you'll find yourself
updating multiple places anytime you want to change one thing.
-->
### Usuń powielony kod
Rób wszystko, co tylko możesz, aby uniknąć powielania kodu. Powielony kod jest zły,
gdyż oznacza, że jest więcej niż jedno miejsce do zmodyfikowania, gdy potrzebujesz zmienić
trochę logiki.

Wyobraź sobie, że prowadzisz restaurację i sprawujesz nadzór nad swoimi zapasami:
wszystkie pomidory, cebule, czosnek, przyprawy itd. Jeśli masz je spisane w wielu miejscach,
to wszystkie z nich muszą zostać uaktualnione, gdy serwujesz danie
z pomidorami. Mając jedną listę, do uaktualnienia jest tylko jedno miejsce!

Częstokroć powielasz kod, gdyż musisz rozwiązać dwa lub więcej nieznacznie różnych problemów,
mających ze sobą wiele wspólnego, a ich różnice wymuszają na Tobie posiadanie
dwóch lub więcej oddzielnych funkcji robiących wiele tego samego. Usunięcie
powielonego kodu oznacza utworzenie abstrakcji, mogącej obsłużyć ten zestaw
różnych problemów za pomocą tylko jednej funkcji/modułu/klasy.

Poprawne użycie abstrakcji jest istotne, dlatego też powinieneś przestrzegać
zasad SOLID, znajdujących się w rozdziale *Klasy*. Zła abstrakcja może być
gorsza, niż powielony kod, bądź więc ostrożny! Jeśli możesz zastosować
dobrą abstrakcję, zrób to! Nie powtarzaj się, w przeciwnym razie skończysz
uaktualniając wiele miejsc za każdym razem, gdy chcesz zmienić jedną rzecz.

**Źle:**
```javascript
function showDeveloperList(developers) {
  developers.forEach((developer) => {
    const expectedSalary = developer.calculateExpectedSalary();
    const experience = developer.getExperience();
    const githubLink = developer.getGithubLink();
    const data = {
      expectedSalary,
      experience,
      githubLink
    };

    render(data);
  });
}

function showManagerList(managers) {
  managers.forEach((manager) => {
    const expectedSalary = manager.calculateExpectedSalary();
    const experience = manager.getExperience();
    const portfolio = manager.getMBAProjects();
    const data = {
      expectedSalary,
      experience,
      portfolio
    };

    render(data);
  });
}
```

**Dobrze:**
```javascript
function showEmployeeList(employees) {
  employees.forEach((employee) => {
    const expectedSalary = employee.calculateExpectedSalary();
    const experience = employee.getExperience();

    const data = {
      expectedSalary,
      experience
    };

    switch (employee.type) {
      case 'manager':
        data.portfolio = employee.getMBAProjects();
        break;
      case 'developer':
        data.githubLink = employee.getGithubLink();
        break;
    }

    render(data);
  });
}
```
**[⬆ powrót na początek](#spis-treści)**

<!--
### Set default objects with Object.assign
-->
### Ustawiaj domyślne obiekty używając Object.assign

**Źle:**
```javascript
const menuConfig = {
  title: null,
  body: 'Bar',
  buttonText: null,
  cancellable: true
};

function createMenu(config) {
  config.title = config.title || 'Foo';
  config.body = config.body || 'Bar';
  config.buttonText = config.buttonText || 'Baz';
  config.cancellable = config.cancellable !== undefined ? config.cancellable : true;
}

createMenu(menuConfig);
```

**Dobrze:**
```javascript
const menuConfig = {
  title: 'Order',
  // Użytkownik nie uwzględnił klucza 'body'
  buttonText: 'Send',
  cancellable: true
};

function createMenu(config) {
  config = Object.assign({
    title: 'Foo',
    body: 'Bar',
    buttonText: 'Baz',
    cancellable: true
  }, config);

  // config ma teraz wartość: {title: "Order", body: "Bar", buttonText: "Send", cancellable: true}
  // ...
}

createMenu(menuConfig);
```
**[⬆ powrót na początek](#spis-treści)**


<!--
### Don't use flags as function parameters
Flags tell your user that this function does more than one thing. Functions should do one thing. Split out your functions if they are following different code paths based on a boolean.
-->
### Nie używaj flag jako argumentów funkcji
Flagi mówią użytkownikowi, że dana funkcja robi więcej niż jedną rzecz. Funkcje powinny robić jedną rzecz. Rozdziel swoje funkcje, jeśli ich kod podąża innymi ścieżkami zależnie od zmiennej boolowskiej.

**Źle:**
```javascript
function createFile(name, temp) {
  if (temp) {
    fs.create(`./temp/${name}`);
  } else {
    fs.create(name);
  }
}
```

**Dobrze:**
```javascript
function createFile(name) {
  fs.create(name);
}

function createTempFile(name) {
  createFile(`./temp/${name}`);
}
```
**[⬆ powrót na początek](#spis-treści)**

<!--
### Avoid Side Effects (part 1)
A function produces a side effect if it does anything other than take a value in
and return another value or values. A side effect could be writing to a file,
modifying some global variable, or accidentally wiring all your money to a
stranger.

Now, you do need to have side effects in a program on occasion. Like the previous
example, you might need to write to a file. What you want to do is to
centralize where you are doing this. Don't have several functions and classes
that write to a particular file. Have one service that does it. One and only one.

The main point is to avoid common pitfalls like sharing state between objects
without any structure, using mutable data types that can be written to by anything,
and not centralizing where your side effects occur. If you can do this, you will
be happier than the vast majority of other programmers.
-->
### Unikaj skutków ubocznych (część 1)
Funkcja daje skutki uboczne, gdy robi cokolwiek innego niż pobranie jednej wartości
i zwrócenie innej lub innych. Skutkiem ubocznym może być zapis do pliku,
zmodyfikowanie jakiejś zmiennej globalnej, lub też przypadkowe przelanie wszystkich
Twoich pieniędzy nieznajomemu.

Czasem potrzebujesz skutków ubocznych w programie. Jak w poprzednim przykładzie
możesz potrzebować zapisu do pliku. Tym, co chcesz zrobić, jest znalezienie jednego miejsca,
gdzie go umieścisz. Nie miej kilku funkcji i klas, które zapisują do poszczególnych plików.
Miej jedną usługę, która to robi. Jedną i tylko jedną.

Główną kwestią jest unikanie powszechnych pułapek, takich jak dzielenie stanu między obiektami
bez jakiejkolwiek struktury, użycie mutowalnych typów danych, które mogą być nadpisane przez cokolwiek
i nieokreślenie jednego miejsca dającego skutki uboczne. Jeśli możesz to zrobić, będziesz szczęśliwszy,
niż zdecydowana większość programistów.

**Źle:**
```javascript
// Globalna zmienna po której następuja funkcja, która się do niej odnosi
// Jeśli będziemy mieć kolejną funckję używającą tej nazwy, teraz będzie ona tablicą i może spowodować błąd.
let name = 'Ryan McDermott';

function splitIntoFirstAndLastName() {
  name = name.split(' ');
}

splitIntoFirstAndLastName();

console.log(name); // ['Ryan', 'McDermott'];
```

**Dobrze:**
```javascript
function splitIntoFirstAndLastName(name) {
  return name.split(' ');
}

const name = 'Ryan McDermott';
const newName = splitIntoFirstAndLastName(name);

console.log(name); // 'Ryan McDermott';
console.log(newName); // ['Ryan', 'McDermott'];
```
**[⬆ powrót na początek](#spis-treści)**

<!--
### Avoid Side Effects (part 2)
In JavaScript, primitives are passed by value and objects/arrays are passed by
reference. In the case of objects and arrays, if your function makes a change
in a shopping cart array, for example, by adding an item to purchase,
then any other function that uses that `cart` array will be affected by this
addition. That may be great, however it can be bad too. Let's imagine a bad
situation:

The user clicks the "Purchase", button which calls a `purchase` function that
spawns a network request and sends the `cart` array to the server. Because
of a bad network connection, the `purchase` function has to keep retrying the
request. Now, what if in the meantime the user accidentally clicks "Add to Cart"
button on an item they don't actually want before the network request begins?
If that happens and the network request begins, then that purchase function
will send the accidentally added item because it has a reference to a shopping
cart array that the `addItemToCart` function modified by adding an unwanted
item.

A great solution would be for the `addItemToCart` to always clone the `cart`,
edit it, and return the clone. This ensures that no other functions that are
holding onto a reference of the shopping cart will be affected by any changes.

Two caveats to mention to this approach:
  1. There might be cases where you actually want to modify the input object,
but when you adopt this programming practice you will find that those cases
are pretty rare. Most things can be refactored to have no side effects!

  2. Cloning big objects can be very expensive in terms of performance. Luckily,
this isn't a big issue in practice because there are
[great libraries](https://facebook.github.io/immutable-js/) that allow
this kind of programming approach to be fast and not as memory intensive as
it would be for you to manually clone objects and arrays.
-->
### Unikaj skutków ubocznych (część 2)
W języku JavaScript typy proste przekazywane są przez wartość, a obiekty/tablice przez
referencję. W przypadku obiektów i tablic, jeśli funkcja dokona zmiany
w tablicy koszyka z zakupami, na przykład przez dodanie produktu,
to inna funkcja używająca tej tablicy koszka `cart` będzie tą zmianą dotknięta.
Może to być dobre, jednak może też być i złe. Wyobraź sobie złą sytuację:

Użytkownik klika przycisk "Kup" wywołujący funkcję `purchase`, która tworzy
żądanie i wysyła tablicę `cart` do serwera. Z powodu
słabego połączenia sieciowego, funkcja `purchase` musi powtarzać żądanie.
Co jeśli w międzyczasie użytkownik przypadkowo kliknie przycisk "Dodaj do koszyka"
na produkcie, który nie był dodany wcześniej?
Jeśli tak się wydarzy i żądanie zostanie wysłane, wtedy funkcja kupująca
wyśle przypadkowo dodany produkt, gdyż posiada ona referencję do tablicy koszyka
zakupów zmodyfikowaną przez funkcję `addItemToCart` poprzez dodanie niechcianego
produktu.

Świetnym rozwiązaniem byłoby, aby `addItemToCart` zawsze klonowała `cart`,
edytowała i zwracała sklonowaną tablicę. To zapewnia, że żadna inna funkcja
przechowująca referencję do koszyka zakupów będzie dotknięta jakąkolwiek zmianą.

Dwa zastrzeżenia do tego podejścia:
  1. Mogą występować przypadki, w których rzeczywiście chcesz zmodyfikować wejściowy obiekt,
ale gdy zaczniesz stosować tę praktykę w programowaniu, przekonasz się, że są one
dość rzadkie. Większość może być zrefaktoryzowana bez skutków ubocznych!

  2. Klonowanie dużych obiektów może być kosztowne pod względem wydajności. Na szczęście
w praktyce nie jest to duży problem, gdyż mamy
[świetne biblioteki](https://facebook.github.io/immutable-js/) pozwalające
takiemu podejściu do programowania być szybkim i nieobciążającym pamięci aż tak,
jak by to było w przypadku ręcznego klonowania obiektów i tablic.

**Źle:**
```javascript
const addItemToCart = (cart, item) => {
  cart.push({ item, date: Date.now() });
};
```

**Dobrze:**
```javascript
const addItemToCart = (cart, item) => {
  return [...cart, { item, date: Date.now() }];
};
```

**[⬆ powrót na początek](#spis-treści)**

<!--
### Don't write to global functions
Polluting globals is a bad practice in JavaScript because you could clash with another
library and the user of your API would be none-the-wiser until they get an
exception in production. Let's think about an example: what if you wanted to
extend JavaScript's native Array method to have a `diff` method that could
show the difference between two arrays? You could write your new function
to the `Array.prototype`, but it could clash with another library that tried
to do the same thing. What if that other library was just using `diff` to find
the difference between the first and last elements of an array? This is why it
would be much better to just use ES2015/ES6 classes and simply extend the `Array` global.
-->
### Nie pisz do funkcji globalnych
Zanieczyszczanie globalnej przestrzeni jest złą praktyką w języku JavaScript,
gdyż możesz kolidować z inną biblioteką i użytkownik Twojego API może być niczego nieświadomym, dopóki wyjątek nie pojawi się na produkcji. Pomyślmy o takim przykładzie:
co jeśli chciałbyś rozszerzyć natywny obiekt Array, aby miał metodę `diff`, która
może pokazać różnicę między dwiema tablicami? Mógłbyś przypisać swoją nową funkcję
do `Array.prototype`, ale może to kolidować z inną biblioteką, która próbowała
zrobić to samo. Co jeśli inna biblioteka używała `diff` do znalezienia
różnicy między pierwszym i ostatnim elementem tablicy? Właśnie dlatego
byłoby dużo lepiej używać po prostu klas wprowadzonych w wersji ES2015/ES6
i zwyczajnie rozszerzyć globalną `Array`.

**Źle:**
```javascript
Array.prototype.diff = function diff(comparisonArray) {
  const hash = new Set(comparisonArray);
  return this.filter(elem => !hash.has(elem));
};
```

**Dobrze:**
```javascript
class SuperArray extends Array {
  diff(comparisonArray) {
    const hash = new Set(comparisonArray);
    return this.filter(elem => !hash.has(elem));
  }
}
```
**[⬆ powrót na początek](#spis-treści)**

<!--
### Favor functional programming over imperative programming
JavaScript isn't a functional language in the way that Haskell is, but it has
a functional flavor to it. Functional languages can be cleaner and easier to test.
Favor this style of programming when you can.
-->
### Przedkładaj programowanie funkcyjne nad programowanie imperatywne
JavaScript nie jest językiem funkcyjnym w takim stopniu, jak Haskell, ale zawiera trochę
funkcyjnego aromatu. Języki funkcyjne mogą być czystsze i prostsze w testowaniu.
Preferuj ten styl programowania, kiedy tylko możesz.

**Źle:**
```javascript
const programmerOutput = [
  {
    name: 'Uncle Bobby',
    linesOfCode: 500
  }, {
    name: 'Suzie Q',
    linesOfCode: 1500
  }, {
    name: 'Jimmy Gosling',
    linesOfCode: 150
  }, {
    name: 'Gracie Hopper',
    linesOfCode: 1000
  }
];

let totalOutput = 0;

for (let i = 0; i < programmerOutput.length; i++) {
  totalOutput += programmerOutput[i].linesOfCode;
}
```

**Dobrze:**
```javascript
const programmerOutput = [
  {
    name: 'Uncle Bobby',
    linesOfCode: 500
  }, {
    name: 'Suzie Q',
    linesOfCode: 1500
  }, {
    name: 'Jimmy Gosling',
    linesOfCode: 150
  }, {
    name: 'Gracie Hopper',
    linesOfCode: 1000
  }
];

const totalOutput = programmerOutput
  .map(output => output.linesOfCode)
  .reduce((totalLines, lines) => totalLines + lines);
```
**[⬆ powrót na początek](#spis-treści)**

<!--
### Encapsulate conditionals
-->
### Stosuj hermetyzację warunków

**Źle:**
```javascript
if (fsm.state === 'fetching' && isEmpty(listNode)) {
  // ...
}
```

**Dobrze:**
```javascript
function shouldShowSpinner(fsm, listNode) {
  return fsm.state === 'fetching' && isEmpty(listNode);
}

if (shouldShowSpinner(fsmInstance, listNodeInstance)) {
  // ...
}
```
**[⬆ powrót na początek](#spis-treści)**

<!--
### Avoid negative conditionals
-->
### Unikaj negowania warunków

**Źle:**
```javascript
function isDOMNodeNotPresent(node) {
  // ...
}

if (!isDOMNodeNotPresent(node)) {
  // ...
}
```

**Dobrze:**
```javascript
function isDOMNodePresent(node) {
  // ...
}

if (isDOMNodePresent(node)) {
  // ...
}
```
**[⬆ powrót na początek](#spis-treści)**

<!--
### Avoid conditionals
This seems like an impossible task. Upon first hearing this, most people say,
"how am I supposed to do anything without an `if` statement?" The answer is that
you can use polymorphism to achieve the same task in many cases. The second
question is usually, "well that's great but why would I want to do that?" The
answer is a previous clean code concept we learned: a function should only do
one thing. When you have classes and functions that have `if` statements, you
are telling your user that your function does more than one thing. Remember,
just do one thing.
-->
### Unikaj warunków
Wydaje się to być zadaniem niewykonalnym. Większość ludzi słysząc to pierwszy raz, powie:
"Jak mam zrobić cokolwiek bez instrukcji `if`?" Odpowiedzią jest, że
możesz użyć polimorfizmu, aby osiągnąć to samo w wielu przypadkach. Drugim
pytaniem jest zwykle: "Dobrze, to świetnie, ale dlaczego chciałbym to zrobić?"
Odpowiedzią jest poprzednio poznana koncepcja czystego kodu: funkcja powinna robić
tylko jedną rzecz. Gdy masz klasy i funkcje zawierające instrukcje `if`,
mówisz użytkownikowi, że Twoja funkcja robi więcej, niż jedną rzecz. Pamiętaj,
rób po prostu jedną rzecz.

**Źle:**
```javascript
class Airplane {
  // ...
  getCruisingAltitude() {
    switch (this.type) {
      case '777':
        return this.getMaxAltitude() - this.getPassengerCount();
      case 'Air Force One':
        return this.getMaxAltitude();
      case 'Cessna':
        return this.getMaxAltitude() - this.getFuelExpenditure();
    }
  }
}
```

**Dobrze:**
```javascript
class Airplane {
  // ...
}

class Boeing777 extends Airplane {
  // ...
  getCruisingAltitude() {
    return this.getMaxAltitude() - this.getPassengerCount();
  }
}

class AirForceOne extends Airplane {
  // ...
  getCruisingAltitude() {
    return this.getMaxAltitude();
  }
}

class Cessna extends Airplane {
  // ...
  getCruisingAltitude() {
    return this.getMaxAltitude() - this.getFuelExpenditure();
  }
}
```
**[⬆ powrót na początek](#spis-treści)**

<!--
### Avoid type-checking (part 1)
JavaScript is untyped, which means your functions can take any type of argument.
Sometimes you are bitten by this freedom and it becomes tempting to do
type-checking in your functions. There are many ways to avoid having to do this.
The first thing to consider is consistent APIs.
-->
### Unikaj sprawdzania typów (część 1)
JavaScript jest typowany dynamicznie, co oznacza, że Twoje funkcje mogą przyjmować argumenty dowolnego typu.
Czasami ta wolność jest uciążliwa i sprawdzanie typów w Twoich funkcjach
okazuje się kuszące. Jest wiele sposobów, aby tego uniknąć.
Pierwszym jest rozważenie zwartych API.

**Źle:**
```javascript
function travelToTexas(vehicle) {
  if (vehicle instanceof Bicycle) {
    vehicle.pedal(this.currentLocation, new Location('texas'));
  } else if (vehicle instanceof Car) {
    vehicle.drive(this.currentLocation, new Location('texas'));
  }
}
```

**Dobrze:**
```javascript
function travelToTexas(vehicle) {
  vehicle.move(this.currentLocation, new Location('texas'));
}
```
**[⬆ powrót na początek](#spis-treści)**

<!--
### Avoid type-checking (part 2)
If you are working with basic primitive values like strings and integers,
and you can't use polymorphism but you still feel the need to type-check,
you should consider using TypeScript. It is an excellent alternative to normal
JavaScript, as it provides you with static typing on top of standard JavaScript
syntax. The problem with manually type-checking normal JavaScript is that
doing it well requires so much extra verbiage that the faux "type-safety" you get
doesn't make up for the lost readability. Keep your JavaScript clean, write
good tests, and have good code reviews. Otherwise, do all of that but with
TypeScript (which, like I said, is a great alternative!).
-->
### Unikaj sprawdzania typów (część 2)
Jeśli pracujesz z podstawowymi wartościami jak ciągi znaków i tablice
i nie możesz użyć polimorfizmu, a nadal czujesz potrzebę sprawdzania typów,
powinieneś rozważyć użycie języka TypeScript. Jest on świetną alternatywą dla normalnego
języka JavaScript, gdyż dostarcza statycznego typowania do jego standardowej składni.
Problemem z ręcznym sprawdzaniem typów w normalnym JavaScript jest to, że używanie go
poprawnie wymaga na tyle dużo dodatkowej rozwlekłości, iż otrzymane sztuczne bezpieczeństwo typologiczne
nie wynagradza utraty czytelności. Utrzymuj Twój JavaScript czystym, pisz
dobre testy i miej dobre przeglądy kodu. W przeciwnym razie rób wszystko to samo,
ale używając TypeScript (który, jak powiedziałem, jest świetną alternatywą!).

**Źle:**
```javascript
function combine(val1, val2) {
  if (typeof val1 === 'number' && typeof val2 === 'number' ||
      typeof val1 === 'string' && typeof val2 === 'string') {
    return val1 + val2;
  }

  throw new Error('Must be of type String or Number');
}
```

**Dobrze:**
```javascript
function combine(val1, val2) {
  return val1 + val2;
}
```
**[⬆ powrót na początek](#spis-treści)**

<!--
### Don't over-optimize
Modern browsers do a lot of optimization under-the-hood at runtime. A lot of
times, if you are optimizing then you are just wasting your time. [There are good
resources](https://github.com/petkaantonov/bluebird/wiki/Optimization-killers)
for seeing where optimization is lacking. Target those in the meantime, until
they are fixed if they can be.
-->
### Nie optymalizuj nadmiernie
Nowoczesne przeglądarki w czasie wykonania dokonują wielu optymalizacji "pod maską".
Często gdy optymalizujesz, po prostu tracisz swój czas.
[Tu są dobre źródła](https://github.com/petkaantonov/bluebird/wiki/Optimization-killers)
pokazująca niedostatki optymalizacji. Postaw je sobie za cel w międzyczasie, dopóki nie będą
poprawione, jeśli mogą być.

**Źle:**
```javascript

// W starych przeglądarkach każda iteracja z niebuforowanym `list.length` byłaby kosztowna
// w związku z ponownym obliczeniem `list.length`. W nowoczesnych przeglądarkach jest to zoptymalizowane.
for (let i = 0, len = list.length; i < len; i++) {
  // ...
}
```

**Dobrze:**
```javascript
for (let i = 0; i < list.length; i++) {
  // ...
}
```
**[⬆ powrót na początek](#spis-treści)**

<!--
### Remove dead code
Dead code is just as bad as duplicate code. There's no reason to keep it in
your codebase. If it's not being called, get rid of it! It will still be safe
in your version history if you still need it.
-->
### Usuwaj martwy kod
Martwy kod jest po prostu tak samo zły, jak powielony kod. Nie ma powodu, aby go trzymać.
Jeśli nie będzie wywoływany, pozbądź się go! Będzie nadal bezpieczny
w historii Twojego systemu wersjonowania, jeśli ciągle go potrzebujesz.

**Źle:**
```javascript
function oldRequestModule(url) {
  // ...
}

function newRequestModule(url) {
  // ...
}

const req = newRequestModule;
inventoryTracker('apples', req, 'www.inventory-awesome.io');

```

**Dobrze:**
```javascript
function newRequestModule(url) {
  // ...
}

const req = newRequestModule;
inventoryTracker('apples', req, 'www.inventory-awesome.io');
```
**[⬆ powrót na początek](#spis-treści)**

<!--
## **Objects and Data Structures**
### Use getters and setters
Using getters and setters to access data on objects could be better than simply
looking for a property on an object. "Why?" you might ask. Well, here's an
unorganized list of reasons why:

* When you want to do more beyond getting an object property, you don't have
to look up and change every accessor in your codebase.
* Makes adding validation simple when doing a `set`.
* Encapsulates the internal representation.
* Easy to add logging and error handling when getting and setting.
* You can lazy load your object's properties, let's say getting it from a
server.
-->
## **Obiekty i struktury danych**
### Używaj getterów i setterów
Używanie getterów i setterów, aby uzyskać dostęp do danych obiektów, może być lepsze, niż zwykłe
sprawdzanie właściwości obiektu. Możesz spytać: "Dlaczego?". Hmmm... oto niektóre
z powodów:

* Jeśli chcesz robić coś ponad pobieranie właściwości obiektu, nie musisz
sprawdzać i zmieniać każdego akcesora w swoim kodzie.
* Dodanie walidacji jest proste podczas wykonywania `set`.
* Hermetyzuje wewnętrzną reprezentację.
* Łatwo dodać logowanie i obsługę błędów podczas pobierania i ustawiania.
* Możesz zastosować leniwe ładowanie właściwości Twojego obiektu, przykładowo, pobierając je
z serwera.

**Źle:**
```javascript
function makeBankAccount() {
  // ...

  return {
    balance: 0,
    // ...
  };
}

const account = makeBankAccount();
account.balance = 100;
```

**Dobrze:**
```javascript
function makeBankAccount() {
  // ta jest prywatna
  let balance = 0;

  // "getter" udostępniony publicznie przez zwrócenie obiektu poniżej
  function getBalance() {
    return balance;
  }

  // "setter" udostępniony publicznie przez zwrócenie obiektu poniżej
  function setBalance(amount) {
    // ... walidacja przed uaktualnieniem zmiennej "balance"
    balance = amount;
  }

  return {
    // ...
    getBalance,
    setBalance,
  };
}

const account = makeBankAccount();
account.setBalance(100);
```
**[⬆ powrót na początek](#spis-treści)**


<!--
### Make objects have private members
This can be accomplished through closures (for ES5 and below).
-->
### Używaj prywatnych właściwości i metod obiektów
Można to osiągnąć dzięki domknięciom (dla wersji ES5 i niższych).

**Źle:**
```javascript

const Employee = function(name) {
  this.name = name;
};

Employee.prototype.getName = function getName() {
  return this.name;
};

const employee = new Employee('John Doe');
console.log(`Employee name: ${employee.getName()}`); // Employee name: John Doe
delete employee.name;
console.log(`Employee name: ${employee.getName()}`); // Employee name: undefined
```

**Dobrze:**
```javascript
function makeEmployee(name) {
  return {
    getName() {
      return name;
    },
  };
}

const employee = makeEmployee('John Doe');
console.log(`Employee name: ${employee.getName()}`); // Employee name: John Doe
delete employee.name;
console.log(`Employee name: ${employee.getName()}`); // Employee name: John Doe
```
**[⬆ powrót na początek](#spis-treści)**


<!--
## **Classes**
### Prefer ES2015/ES6 classes over ES5 plain functions
It's very difficult to get readable class inheritance, construction, and method
definitions for classical ES5 classes. If you need inheritance (and be aware
that you might not), then prefer ES2015/ES6 classes. However, prefer small functions over
classes until you find yourself needing larger and more complex objects.
-->
## **Klasy**
### Przedkładaj klasy wprowadzone w ES2015/ES6 ponad proste funkcje jak w ES5
Trudno uzyskać czytelne dziedziczenie, konstrukcję i definicje metod
klasycznymi technikami dostępnymi w ES5. Gdy potrzebujesz dziedziczenia (a bądź świadom,
że może nie musisz), wykorzystuj klasy wprowadzone w ES2015/ES6. Niemniej jednak przedkładaj małe funkcje ponad
klasy, dopóki nie będziesz potrzebował większych i bardziej złożonych obiektów.

**Źle:**
```javascript
const Animal = function(age) {
  if (!(this instanceof Animal)) {
    throw new Error('Instantiate Animal with `new`');
  }

  this.age = age;
};

Animal.prototype.move = function move() {};

const Mammal = function(age, furColor) {
  if (!(this instanceof Mammal)) {
    throw new Error('Instantiate Mammal with `new`');
  }

  Animal.call(this, age);
  this.furColor = furColor;
};

Mammal.prototype = Object.create(Animal.prototype);
Mammal.prototype.constructor = Mammal;
Mammal.prototype.liveBirth = function liveBirth() {};

const Human = function(age, furColor, languageSpoken) {
  if (!(this instanceof Human)) {
    throw new Error('Instantiate Human with `new`');
  }

  Mammal.call(this, age, furColor);
  this.languageSpoken = languageSpoken;
};

Human.prototype = Object.create(Mammal.prototype);
Human.prototype.constructor = Human;
Human.prototype.speak = function speak() {};
```

**Dobrze:**
```javascript
class Animal {
  constructor(age) {
    this.age = age;
  }

  move() { /* ... */ }
}

class Mammal extends Animal {
  constructor(age, furColor) {
    super(age);
    this.furColor = furColor;
  }

  liveBirth() { /* ... */ }
}

class Human extends Mammal {
  constructor(age, furColor, languageSpoken) {
    super(age, furColor);
    this.languageSpoken = languageSpoken;
  }

  speak() { /* ... */ }
}
```
**[⬆ powrót na początek](#spis-treści)**


<!--
### Use method chaining
This pattern is very useful in JavaScript and you see it in many libraries such
as jQuery and Lodash. It allows your code to be expressive, and less verbose.
For that reason, I say, use method chaining and take a look at how clean your code
will be. In your class functions, simply return `this` at the end of every function,
and you can chain further class methods onto it.
-->
### Wykorzystuj łańcuchowanie metod
Wzorzec ten jest bardzo przydatny w języku JavaScript i widać to w wielu bibliotekach takich jak
jQuery i Lodash. Pozwala on uzyskać kod ekspresywny i mniej rozwlekły.
W związku z tym mówię - użyj łańcuchowania metod i popatrz, jak czysty będzie Twój kod.
W funkcjach Twoich klas zwyczajnie zwracaj `this` na końcu każdej funkcji
i będziesz mógł doczepić do nich (jak ogniwa łańcucha) inne metody klasy.

**Źle:**
```javascript
class Car {
  constructor(make, model, color) {
    this.make = make;
    this.model = model;
    this.color = color;
  }

  setMake(make) {
    this.make = make;
  }

  setModel(model) {
    this.model = model;
  }

  setColor(color) {
    this.color = color;
  }

  save() {
    console.log(this.make, this.model, this.color);
  }
}

const car = new Car('Ford','F-150','red');
car.setColor('pink');
car.save();
```

**Dobrze:**
```javascript
class Car {
  constructor(make, model, color) {
    this.make = make;
    this.model = model;
    this.color = color;
  }

  setMake(make) {
    this.make = make;
    // ZAUWAŻ: Zwracamy this dla łańcuchowania
    return this;
  }

  setModel(model) {
    this.model = model;
    // ZAUWAŻ: Zwracamy this dla łańcuchowania
    return this;
  }

  setColor(color) {
    this.color = color;
    // ZAUWAŻ: Zwracamy this dla łańcuchowania
    return this;
  }

  save() {
    console.log(this.make, this.model, this.color);
    // ZAUWAŻ: Zwracamy this dla łańcuchowania
    return this;
  }
}

const car = new Car('Ford','F-150','red')
  .setColor('pink')
  .save();
```
**[⬆ powrót na początek](#spis-treści)**

<!--
### Prefer composition over inheritance
As stated famously in [*Design Patterns*](https://en.wikipedia.org/wiki/Design_Patterns) by the Gang of Four,
you should prefer composition over inheritance where you can. There are lots of
good reasons to use inheritance and lots of good reasons to use composition.
The main point for this maxim is that if your mind instinctively goes for
inheritance, try to think if composition could model your problem better. In some
cases it can.

You might be wondering then, "when should I use inheritance?" It
depends on your problem at hand, but this is a decent list of when inheritance
makes more sense than composition:

1. Your inheritance represents an "is-a" relationship and not a "has-a"
relationship (Human->Animal vs. User->UserDetails).
2. You can reuse code from the base classes (Humans can move like all animals).
3. You want to make global changes to derived classes by changing a base class.
(Change the caloric expenditure of all animals when they move).
-->
### Przedkładaj kompozycję ponad dziedziczenie
Jak stwierdzono głośno we [*Wzorcach projektowych*](https://en.wikipedia.org/wiki/Design_Patterns) Bandy Czterech,
powinieneś przedkładać kompozycję ponad dziedziczenie tam, gdzie tylko możesz. Jest wiele
dobrych powodów, aby używać dziedziczenia i wiele dobrych powodów, aby używać kompozycji.
Głównym punktem tej maksymy jest, aby gdy w myślach instynktownie skłaniasz się
ku dziedziczeniu, próbować zastanowić się, czy kompozycja może odwzorować problem lepiej.
W niektórych przypadkach może.

Możesz się zastanawiać: "kiedy powinienem użyć dziedziczenia?". To zależy
od Twojego problemu, ale tu jest skromna lista przypadków, gdy dziedziczenie
ma więcej sensu niż kompozycja:

1. Twoje dziedziczenie reprezentuje relację "x-jest-y" a nie "x-posiada-y"
(Człowiek->Zwierzę kontra Użytkownik->SzczegółyUżytkownika).
2. Możesz wykorzystać ponownie kod ze zbioru swoich klas (ludzie mogą poruszać się jak wszystkie zwierzęta).
3. Chcesz dokonać globalnych zmian w klasach pochodnych zmieniając klasę podstawową
(zmienić zużycie kalorii podczas poruszania dla wszystkich zwierząt).

**Źle:**
```javascript
class Employee {
  constructor(name, email) {
    this.name = name;
    this.email = email;
  }

  // ...
}

// Źle, gdyż Pracownicy "posiadają" dane podatkowe. DanePodatkowePracownika nie są typem Pracownika
class EmployeeTaxData extends Employee {
  constructor(ssn, salary) {
    super();
    this.ssn = ssn;
    this.salary = salary;
  }

  // ...
}
```

**Dobrze:**
```javascript
class EmployeeTaxData {
  constructor(ssn, salary) {
    this.ssn = ssn;
    this.salary = salary;
  }

  // ...
}

class Employee {
  constructor(name, email) {
    this.name = name;
    this.email = email;
  }

  setTaxData(ssn, salary) {
    this.taxData = new EmployeeTaxData(ssn, salary);
  }
  // ...
}
```
**[⬆ powrót na początek](#spis-treści)**

## **SOLID**
<!--
### Single Responsibility Principle (SRP)
As stated in Clean Code, "There should never be more than one reason for a class
to change". It's tempting to jam-pack a class with a lot of functionality, like
when you can only take one suitcase on your flight. The issue with this is
that your class won't be conceptually cohesive and it will give it many reasons
to change. Minimizing the amount of times you need to change a class is important.
It's important because if too much functionality is in one class and you modify
a piece of it, it can be difficult to understand how that will affect other
dependent modules in your codebase.
-->
### Zasada jednej odpowiedzialności (SRP)
Jak stwierdzono w Czystym Kodzie, "Nigdy nie powinno być więcej niż jednego powodu do modyfikacji klasy". Kuszącym jest zapakowanie w klasę wielu funkcjonalności, tak jak wtedy,
gdy możesz zabrać tylko jedną walizkę podczas lotu. Problemem jest tutaj to,
że Twoja klasa nie będzie koncepcyjnie spójna i da jej to wiele powodów
do zmian. Minimalizacja ilości sytuacji, w których musisz zmienić klasę, jest istotna.
Jest istotna, gdyż jeśli jedna klasa zawiera zbyt dużo funkcjonalności i modyfikujesz
część z nich, może stać się trudnym do zrozumienia, jak wpłynie to na inne
zależne moduły w Twoim kodzie.

**Źle:**
```javascript
class UserSettings {
  constructor(user) {
    this.user = user;
  }

  changeSettings(settings) {
    if (this.verifyCredentials()) {
      // ...
    }
  }

  verifyCredentials() {
    // ...
  }
}
```

**Dobrze:**
```javascript
class UserAuth {
  constructor(user) {
    this.user = user;
  }

  verifyCredentials() {
    // ...
  }
}


class UserSettings {
  constructor(user) {
    this.user = user;
    this.auth = new UserAuth(user);
  }

  changeSettings(settings) {
    if (this.auth.verifyCredentials()) {
      // ...
    }
  }
}
```
**[⬆ powrót na początek](#spis-treści)**

<!--
### Open/Closed Principle (OCP)
As stated by Bertrand Meyer, "software entities (classes, modules, functions,
etc.) should be open for extension, but closed for modification." What does that
mean though? This principle basically states that you should allow users to
add new functionalities without changing existing code.
-->
### Zasada otwarte-zamknięte (OCP)
Jak stwierdził Bertrand Meyer, "Encje (klasy, moduły, funkcje itd.)
powinny być otwarte na rozszerzenie, ale zamknięte na modyfikacje". Co więc
to oznacza? Ta zasada po prostu stwierdza, że powinieneś umożliwić użytkownikom
dodanie nowych funkcjonalności bez zmiany istniejącego kodu.

**Źle:**
```javascript
class AjaxAdapter extends Adapter {
  constructor() {
    super();
    this.name = 'ajaxAdapter';
  }
}

class NodeAdapter extends Adapter {
  constructor() {
    super();
    this.name = 'nodeAdapter';
  }
}

class HttpRequester {
  constructor(adapter) {
    this.adapter = adapter;
  }

  fetch(url) {
    if (this.adapter.name === 'ajaxAdapter') {
      return makeAjaxCall(url).then((response) => {
        // przekształć odpowiedź i zwróć
      });
    } else if (this.adapter.name === 'httpNodeAdapter') {
      return makeHttpCall(url).then((response) => {
        // przekształć odpowiedź i zwróć
      });
    }
  }
}

function makeAjaxCall(url) {
  // żądanie i zwrócenie obietnicy
}

function makeHttpCall(url) {
  // żądanie i zwrócenie obietnicy
}
```

**Dobrze:**
```javascript
class AjaxAdapter extends Adapter {
  constructor() {
    super();
    this.name = 'ajaxAdapter';
  }

  request(url) {
    // żądanie i zwrócenie obietnicy
  }
}

class NodeAdapter extends Adapter {
  constructor() {
    super();
    this.name = 'nodeAdapter';
  }

  request(url) {
    // żądanie i zwrócenie obietnicy
  }
}

class HttpRequester {
  constructor(adapter) {
    this.adapter = adapter;
  }

  fetch(url) {
    return this.adapter.request(url).then((response) => {
      // przekształć odpowiedź i zwróć
    });
  }
}
```
**[⬆ powrót na początek](#spis-treści)**

<!--
### Liskov Substitution Principle (LSP)
This is a scary term for a very simple concept. It's formally defined as "If S
is a subtype of T, then objects of type T may be replaced with objects of type S
(i.e., objects of type S may substitute objects of type T) without altering any
of the desirable properties of that program (correctness, task performed,
etc.)." That's an even scarier definition.

The best explanation for this is if you have a parent class and a child class,
then the base class and child class can be used interchangeably without getting
incorrect results. This might still be confusing, so let's take a look at the
classic Square-Rectangle example. Mathematically, a square is a rectangle, but
if you model it using the "is-a" relationship via inheritance, you quickly
get into trouble.
-->
### Zasada podstawienia Liskov (LSP)
Jest to przerażająca nazwa dla bardzo prostego pojęcia. Jest formalnie zdefiniowana jako "Jeśli S
jest podtypem T, wtedy obiekty typu T mogą być wymienione z obiektami typu S
(np. obiekty typu S mogą zastąpić obiekty typu T) bez zmieniania żadnych
pożądanych właściwości tego programu (poprawność, zadanie wykonane
itd.)". To jeszcze bardziej przerażająca definicja.

Najlepszym wyjaśnieniem tego będzie, jeśli masz klasę bazową i klasę potomną,
wtedy klasy bazowa i potomna mogą zostać użyte wymiennie bez otrzymania
niepoprawnych wyników. Może to być nadal pogmatwane, spójrzmy więc na
klasyczny przykład: Kwadrat-Prostokąt. Matematycznie kwadrat jest prostokątem, ale
jeśli modelujesz to używając relacji "x-jest-y" przez dziedziczenie, szybko
wpadniesz w kłopoty.

**Źle:**
```javascript
class Rectangle {
  constructor() {
    this.width = 0;
    this.height = 0;
  }

  setColor(color) {
    // ...
  }

  render(area) {
    // ...
  }

  setWidth(width) {
    this.width = width;
  }

  setHeight(height) {
    this.height = height;
  }

  getArea() {
    return this.width * this.height;
  }
}

class Square extends Rectangle {
  setWidth(width) {
    this.width = width;
    this.height = width;
  }

  setHeight(height) {
    this.width = height;
    this.height = height;
  }
}

function renderLargeRectangles(rectangles) {
  rectangles.forEach((rectangle) => {
    rectangle.setWidth(4);
    rectangle.setHeight(5);
    const area = rectangle.getArea(); // ŹLE: Zwraca 25 dla Kwadratu. Powinno być 20
    rectangle.render(area);
  });
}

const rectangles = [new Rectangle(), new Rectangle(), new Square()];
renderLargeRectangles(rectangles);
```

**Dobrze:**
```javascript
class Shape {
  setColor(color) {
    // ...
  }

  render(area) {
    // ...
  }
}

class Rectangle extends Shape {
  constructor(width, height) {
    super();
    this.width = width;
    this.height = height;
  }

  getArea() {
    return this.width * this.height;
  }
}

class Square extends Shape {
  constructor(length) {
    super();
    this.length = length;
  }

  getArea() {
    return this.length * this.length;
  }
}

function renderLargeShapes(shapes) {
  shapes.forEach((shape) => {
    const area = shape.getArea();
    shape.render(area);
  });
}

const shapes = [new Rectangle(4, 5), new Rectangle(4, 5), new Square(5)];
renderLargeShapes(shapes);
```
**[⬆ powrót na początek](#spis-treści)**

<!--
### Interface Segregation Principle (ISP)
JavaScript doesn't have interfaces so this principle doesn't apply as strictly
as others. However, it's important and relevant even with JavaScript's lack of
type system.

ISP states that "Clients should not be forced to depend upon interfaces that
they do not use." Interfaces are implicit contracts in JavaScript because of
duck typing.

A good example to look at that demonstrates this principle in JavaScript is for
classes that require large settings objects. Not requiring clients to setup
huge amounts of options is beneficial, because most of the time they won't need
all of the settings. Making them optional helps prevent having a
"fat interface".
-->
### Zasada segregacji interfejsów (ISP)
JavaScript nie posiada interfejsów, więc ta zasada nie ma tu tak restrykcyjnego zastosowania,
jak pozostałe. Mimo tego jest ważna i istotna nawet przy braku typowania w JavaScript.

ISP stwierdza, że "Na klientach nie powinna być wymuszana zależność od interfejsów,
których oni nie używają". Interfejsy w JavaScript są niejawnymi kontraktami przez
kacze typowanie.

Dobrym przykładem demonstrującym tę zasadę w JavaScript są klasy,
które wymagają dużych obiektów z opcjami. Nie wymaganie od klientów instalowania
ogromnych ilości ustawień jest korzystne, gdyż przez większość czasu nie będą oni potrzebować
wszystkich tych ustawień. Uczynienie ich opcjonalnymi pomoże zapobiec otrzymaniu
"grubego interfejsu".

**Źle:**
```javascript
class DOMTraverser {
  constructor(settings) {
    this.settings = settings;
    this.setup();
  }

  setup() {
    this.rootNode = this.settings.rootNode;
    this.animationModule.setup();
  }

  traverse() {
    // ...
  }
}

const $ = new DOMTraverser({
  rootNode: document.getElementsByTagName('body'),
  animationModule() {} // W większości przypadków nie będziemy musieli animować podczas trawersowania.
  // ...
});

```

**Dobrze:**
```javascript
class DOMTraverser {
  constructor(settings) {
    this.settings = settings;
    this.options = settings.options;
    this.setup();
  }

  setup() {
    this.rootNode = this.settings.rootNode;
    this.setupOptions();
  }

  setupOptions() {
    if (this.options.animationModule) {
      // ...
    }
  }

  traverse() {
    // ...
  }
}

const $ = new DOMTraverser({
  rootNode: document.getElementsByTagName('body'),
  options: {
    animationModule() {}
  }
});
```
**[⬆ powrót na początek](#spis-treści)**

<!--
### Dependency Inversion Principle (DIP)
This principle states two essential things:
1. High-level modules should not depend on low-level modules. Both should
depend on abstractions.
2. Abstractions should not depend upon details. Details should depend on
abstractions.

This can be hard to understand at first, but if you've worked with AngularJS,
you've seen an implementation of this principle in the form of Dependency
Injection (DI). While they are not identical concepts, DIP keeps high-level
modules from knowing the details of its low-level modules and setting them up.
It can accomplish this through DI. A huge benefit of this is that it reduces
the coupling between modules. Coupling is a very bad development pattern because
it makes your code hard to refactor.

As stated previously, JavaScript doesn't have interfaces so the abstractions
that are depended upon are implicit contracts. That is to say, the methods
and properties that an object/class exposes to another object/class. In the
example below, the implicit contract is that any Request module for an
`InventoryTracker` will have a `requestItems` method.
-->
### Zasada odwrócenia zależności (DIP)
Ta zasada określa dwie istotne rzeczy:
1. Wysokopoziomowe moduły nie powinny zależeć od modułów niskopoziomowych. Jedne i drugie
powinny zależeć od abstrakcji.
2. Abstrakcje nie powinny zależeć od szczegółów. Szczegóły powinny zależeć
od abstrakcji.

Z początku może to być trudne do zrozumienia, ale jeśli pracowałeś z AngularJS,
widziałeś implementację tej zasady w formie Wstrzykiwania zależności (DI).
Podczas gdy nie są one identycznymi pojęciami, Zasada odwrócenia zależności trzyma wysokopoziomowe
moduły z dala od wiedzy na temat szczegółów ich niskopoziomowych modułów i ich ustawiania.
Może to być osiągnięte dzięki Wstrzykiwaniu zależności. Ogromną korzyścią jest, iż redukuje to
zależności między modułami. Zależność jest bardzo złym wzorcem, gdyż
czyni Twój kod trudniejszym do zrefaktoryzowania.

Jak wcześniej zaznaczono, JavaScript nie posiada interfejsów, więc abstrakcje
będące zależnymi, są niejawnymi kontraktami. Oznacza to metody
i właściwości, które obiekt/klasa wystawia dla innego obiektu/klasy.
W przykładzie poniżej niejawnym kontraktem jest to, że dowolny moduł Request dla
`InventoryTracker` będzie posiadał metodę `requestItems`.

**Źle:**
```javascript
class InventoryRequester {
  constructor() {
    this.REQ_METHODS = ['HTTP'];
  }

  requestItem(item) {
    // ...
  }
}

class InventoryTracker {
  constructor(items) {
    this.items = items;

    // ŹLE: Utworzyliśmy zależność od specyficznej implementacji żądania.
    // Powinniśmy po prostu uczynić requestItems zależnym od metody: `request`
    this.requester = new InventoryRequester();
  }

  requestItems() {
    this.items.forEach((item) => {
      this.requester.requestItem(item);
    });
  }
}

const inventoryTracker = new InventoryTracker(['apples', 'bananas']);
inventoryTracker.requestItems();
```

**Dobrze:**
```javascript
class InventoryTracker {
  constructor(items, requester) {
    this.items = items;
    this.requester = requester;
  }

  requestItems() {
    this.items.forEach((item) => {
      this.requester.requestItem(item);
    });
  }
}

class InventoryRequesterV1 {
  constructor() {
    this.REQ_METHODS = ['HTTP'];
  }

  requestItem(item) {
    // ...
  }
}

class InventoryRequesterV2 {
  constructor() {
    this.REQ_METHODS = ['WS'];
  }

  requestItem(item) {
    // ...
  }
}

// Przez skonstruowanie naszych zależności na zewnątrz i wstrzyknięcie ich, możemy łatwo
// zastąpić nasz moduł żądania nowym, fantazyjnym, używającym WebSockets.
const inventoryTracker = new InventoryTracker(['apples', 'bananas'], new InventoryRequesterV2());
inventoryTracker.requestItems();
```
**[⬆ powrót na początek](#spis-treści)**

<!--
## **Testing**
Testing is more important than shipping. If you have no tests or an
inadequate amount, then every time you ship code you won't be sure that you
didn't break anything. Deciding on what constitutes an adequate amount is up
to your team, but having 100% coverage (all statements and branches) is how
you achieve very high confidence and developer peace of mind. This means that
in addition to having a great testing framework, you also need to use a
[good coverage tool](http://gotwarlost.github.io/istanbul/).

There's no excuse to not write tests. There are [plenty of good JS test frameworks](http://jstherightway.org/#testing-tools), so find one that your team prefers.
When you find one that works for your team, then aim to always write tests
for every new feature/module you introduce. If your preferred method is
Test Driven Development (TDD), that is great, but the main point is to just
make sure you are reaching your coverage goals before launching any feature,
or refactoring an existing one.
-->
## **Testowanie**
Testowanie jest ważniejsze niż dostarczanie. Jeśli nie masz testów albo jest ich
nieodpowiednia ilość, to za każdym razem dostarczając swój kod, nie będziesz pewnym,
że czegoś nie popsułeś. Decyzja o tym, jaka ilość testów jest odpowiednia, należy
do Twojego zespołu, ale pokrycie w 100% (wszystkie instrukcje i gałęzie) jest tym,
co pozwoli osiągnąć wysoką pewność i święty spokój dewelopera. Oznacza to, że
jako dodatek do posiadanego świetnego frameworka do testowania, musisz jeszcze użyć
[dobrego narzędzia pokrycia](http://gotwarlost.github.io/istanbul/).

Nie ma usprawiedliwienia dla niepisania testów. Jest [mnóstwo dobrych frameworków testowych] (http://jstherightway.org/#testing-tools), znajdź więc ten, który Twój zespół preferuje.
Kiedy go znajdziesz, wtedy postaw sobie za cel, aby zawsze pisać testy
dla każdej nowej funkcjonalności/modułu, który wprowadzasz. Jeśli preferowaną przez Ciebie metodą jest
Test Driven Development (TDD), to świetnie, ale istotą jest po prostu
upewnienie się, że osiągasz swoje cele dotyczące pokrycia przed wypuszczeniem jakiejkolwiek funkcjonalności
albo refaktoryzacji już istniejącej.

<!--
### Single concept per test
-->
### Pojedynczy pomysł na test

**Źle:**
```javascript
import assert from 'assert';

describe('MakeMomentJSGreatAgain', () => {
  it('handles date boundaries', () => {
    let date;

    date = new MakeMomentJSGreatAgain('1/1/2015');
    date.addDays(30);
    assert.equal('1/31/2015', date);

    date = new MakeMomentJSGreatAgain('2/1/2016');
    date.addDays(28);
    assert.equal('02/29/2016', date);

    date = new MakeMomentJSGreatAgain('2/1/2015');
    date.addDays(28);
    assert.equal('03/01/2015', date);
  });
});
```

**Dobrze:**
```javascript
import assert from 'assert';

describe('MakeMomentJSGreatAgain', () => {
  it('handles 30-day months', () => {
    const date = new MakeMomentJSGreatAgain('1/1/2015');
    date.addDays(30);
    assert.equal('1/31/2015', date);
  });

  it('handles leap year', () => {
    const date = new MakeMomentJSGreatAgain('2/1/2016');
    date.addDays(28);
    assert.equal('02/29/2016', date);
  });

  it('handles non-leap year', () => {
    const date = new MakeMomentJSGreatAgain('2/1/2015');
    date.addDays(28);
    assert.equal('03/01/2015', date);
  });
});
```
**[⬆ powrót na początek](#spis-treści)**

<!--
## **Concurrency**
### Use Promises, not callbacks
Callbacks aren't clean, and they cause excessive amounts of nesting. With ES2015/ES6,
Promises are a built-in global type. Use them!
-->
## **Współbieżność**
### Używaj Obietnic, a nie wywołań zwrotnych
Wywołania zwrotne nie są czyste i powodują nadmierne ilości zagnieżdżeń.
W ES2015/ES6 Obietnice są wbudowanym, globalnym typem. Używaj ich!

**Źle:**
```javascript
import { get } from 'request';
import { writeFile } from 'fs';

get('https://en.wikipedia.org/wiki/Robert_Cecil_Martin', (requestErr, response) => {
  if (requestErr) {
    console.error(requestErr);
  } else {
    writeFile('article.html', response.body, (writeErr) => {
      if (writeErr) {
        console.error(writeErr);
      } else {
        console.log('File written');
      }
    });
  }
});

```

**Dobrze:**
```javascript
import { get } from 'request';
import { writeFile } from 'fs';

get('https://en.wikipedia.org/wiki/Robert_Cecil_Martin')
  .then((response) => {
    return writeFile('article.html', response);
  })
  .then(() => {
    console.log('File written');
  })
  .catch((err) => {
    console.error(err);
  });

```
**[⬆ powrót na początek](#spis-treści)**

<!--
### Async/Await are even cleaner than Promises
Promises are a very clean alternative to callbacks, but ES2017/ES8 brings async and await
which offer an even cleaner solution. All you need is a function that is prefixed
in an `async` keyword, and then you can write your logic imperatively without
a `then` chain of functions. Use this if you can take advantage of ES2017/ES8 features
today!
-->
### Async/Await są jeszcze bardziej czyste niż Obietnice
Obietnice są bardzo czystą alternatywą dla wywołań zwrotnych, ale ES2017/ES8
wprowadza async i await, które oferują jeszcze czystsze rozwiązanie.
Wszystkim, czego potrzebujesz, jest funkcja poprzedzona słowem kluczowym
`async` i wtedy możesz pisać swoją logikę imperatywnie bez łańcucha funkcji
z `then`. Używaj tego, jeśli możesz skorzystać z funkcjonalności ES2017/ES8 już dziś!

**Źle:**
```javascript
import { get } from 'request-promise';
import { writeFile } from 'fs-promise';

get('https://en.wikipedia.org/wiki/Robert_Cecil_Martin')
  .then((response) => {
    return writeFile('article.html', response);
  })
  .then(() => {
    console.log('File written');
  })
  .catch((err) => {
    console.error(err);
  });

```

**Dobrze:**
```javascript
import { get } from 'request-promise';
import { writeFile } from 'fs-promise';

async function getCleanCodeArticle() {
  try {
    const response = await get('https://en.wikipedia.org/wiki/Robert_Cecil_Martin');
    await writeFile('article.html', response);
    console.log('File written');
  } catch(err) {
    console.error(err);
  }
}
```
**[⬆ powrót na początek](#spis-treści)**

<!--
## **Error Handling**
Thrown errors are a good thing! They mean the runtime has successfully
identified when something in your program has gone wrong and it's letting
you know by stopping function execution on the current stack, killing the
process (in Node), and notifying you in the console with a stack trace.

### Don't ignore caught errors
Doing nothing with a caught error doesn't give you the ability to ever fix
or react to said error. Logging the error to the console (`console.log`)
isn't much better as often times it can get lost in a sea of things printed
to the console. If you wrap any bit of code in a `try/catch` it means you
think an error may occur there and therefore you should have a plan,
or create a code path, for when it occurs.
-->
## **Obsługa błędów**
Wyrzucane błędy są czymś dobrym! Oznaczają, że w czasie wykonania zostało poprawnie
zidentyfikowane coś, co poszło źle w Twoim programie i daje Ci znać, aby
zatrzymać wykonywanie funkcji na obecnym stosie, zamknąć proces (w Node)
i poinformować Cię w konsoli ze śladem stosu.

### Nie ignoruj przechwyconych błędów
Nie zrobienie niczego z przechwyconym błędem nie daje Ci możliwości naprawienia
albo zareagowania na ten błąd. Logowanie błędu do konsoli (`console.log`)
nie jest dużo lepsze, gdyż może on zaginąć w morzu rzeczy informacji do konsoli.
Jeśli zawrzesz jakikolwiek kawałek kodu w bloku `try/catch`, oznacza to, że
myślisz o błędzie mogącym tam wystąpić i w związku z tym powinieneś mieć plan
albo utworzyć ścieżkę kodu do miejsca, w którym wystąpi.

**Źle:**
```javascript
try {
  functionThatMightThrow();
} catch (error) {
  console.log(error);
}
```

**Dobrze:**
```javascript
try {
  functionThatMightThrow();
} catch (error) {
  // Jedna z opcji (głośniejsza niż console.log):
  console.error(error);
  // Inna opcja:
  notifyUserOfError(error);
  // Inna opcja:
  reportErrorToService(error);
  // ALBO zastosuj wszystkie trzy!
}
```

<!--
### Don't ignore rejected promises
For the same reason you shouldn't ignore caught errors
from `try/catch`.
-->
### Nie ignoruj odrzuconych obietnic
Z tych samych powodów, dla których nie powinieneś ignorować przechwyconych błędów
w `try/catch`.

**Źle:**
```javascript
getdata()
  .then((data) => {
    functionThatMightThrow(data);
  })
  .catch((error) => {
    console.log(error);
  });
```

**Dobrze:**
```javascript
getdata()
  .then((data) => {
    functionThatMightThrow(data);
  })
  .catch((error) => {
    // Jedna z opcji (głośniejsza niż console.log):
    console.error(error);
    // Inna opcja:
    notifyUserOfError(error);
    // Inna opcja:
    reportErrorToService(error);
    // ALBO zastosuj wszystkie trzy!
  });
```

**[⬆ powrót na początek](#spis-treści)**

<!--
## **Formatting**
Formatting is subjective. Like many rules herein, there is no hard and fast
rule that you must follow. The main point is DO NOT ARGUE over formatting.
There are [tons of tools](http://standardjs.com/rules.html) to automate this.
Use one! It's a waste of time and money for engineers to argue over formatting.

For things that don't fall under the purview of automatic formatting
(indentation, tabs vs. spaces, double vs. single quotes, etc.) look here
for some guidance.

### Use consistent capitalization
JavaScript is untyped, so capitalization tells you a lot about your variables,
functions, etc. These rules are subjective, so your team can choose whatever
they want. The point is, no matter what you all choose, just be consistent.
-->
## **Formatowanie**
Formatowanie jest subiektywne. Jak w wielu innych tu przypadkach, nie ma sztywnej i szybkiej
zasady, którą musisz przyjąć. Najważniejsze, abyś NIE SPIERAŁ SIĘ o formatowanie.
Są [tony narzędzi](http://standardjs.com/rules.html), by to zautomatyzować.
Użyj jednego! Spieranie się o formatowanie jest stratą czasu i pieniędzy
dla inżynierów.

W sprawach, które nie są objęte automatycznym formatowaniem
(wcięcia, tabulacje kontra spacje, podwójne kontra pojedyncze cudzysłowy itd.) zaglądnij tu
po trochę wskazówek.

### Używaj wielkich liter konsekwentnie
JavaScript jest typowany dynamicznie, więc wielkie litery powiedzą Ci dużo o Twoich
zmiennych, funkcjach itd. Te zasady są subiektywne, więc Twój zespół może wybrać
cokolwiek chce. Chodzi o to, żebyś bez względu na to, co wybierzecie, był konsekwentnym.

**Źle:**
```javascript
const DAYS_IN_WEEK = 7;
const daysInMonth = 30;

const songs = ['Back In Black', 'Stairway to Heaven', 'Hey Jude'];
const Artists = ['ACDC', 'Led Zeppelin', 'The Beatles'];

function eraseDatabase() {}
function restore_database() {}

class animal {}
class Alpaca {}
```

**Dobrze:**
```javascript
const DAYS_IN_WEEK = 7;
const DAYS_IN_MONTH = 30;

const SONGS = ['Back In Black', 'Stairway to Heaven', 'Hey Jude'];
const ARTISTS = ['ACDC', 'Led Zeppelin', 'The Beatles'];

function eraseDatabase() {}
function restoreDatabase() {}

class Animal {}
class Alpaca {}
```
**[⬆ powrót na początek](#spis-treści)**


<!--
### Function callers and callees should be close
If a function calls another, keep those functions vertically close in the source
file. Ideally, keep the caller right above the callee. We tend to read code from
top-to-bottom, like a newspaper. Because of this, make your code read that way.
-->
### Wywołanie funkcji i wywołana funkcja powinny być blisko siebie
Jeśli funkcja wywołuje inną, trzymaj te funkcje wertykalnie blisko w pliku źródłowym.
Najlepiej umieść wywołanie zaraz powyżej wywołanej. Mamy tendencję do czytania kodu
z góry na dół jak gazetę. Dlatego też spraw, aby Twój kod był czytany w ten sposób.

**Źle:**
```javascript
class PerformanceReview {
  constructor(employee) {
    this.employee = employee;
  }

  lookupPeers() {
    return db.lookup(this.employee, 'peers');
  }

  lookupManager() {
    return db.lookup(this.employee, 'manager');
  }

  getPeerReviews() {
    const peers = this.lookupPeers();
    // ...
  }

  perfReview() {
    this.getPeerReviews();
    this.getManagerReview();
    this.getSelfReview();
  }

  getManagerReview() {
    const manager = this.lookupManager();
  }

  getSelfReview() {
    // ...
  }
}

const review = new PerformanceReview(employee);
review.perfReview();
```

**Dobrze:**
```javascript
class PerformanceReview {
  constructor(employee) {
    this.employee = employee;
  }

  perfReview() {
    this.getPeerReviews();
    this.getManagerReview();
    this.getSelfReview();
  }

  getPeerReviews() {
    const peers = this.lookupPeers();
    // ...
  }

  lookupPeers() {
    return db.lookup(this.employee, 'peers');
  }

  getManagerReview() {
    const manager = this.lookupManager();
  }

  lookupManager() {
    return db.lookup(this.employee, 'manager');
  }

  getSelfReview() {
    // ...
  }
}

const review = new PerformanceReview(employee);
review.perfReview();
```

**[⬆ powrót na początek](#spis-treści)**

<!--
## **Comments**
### Only comment things that have business logic complexity.
Comments are an apology, not a requirement. Good code *mostly* documents itself.
-->
## **Komentarze**
### Komentuj tylko rzeczy mające złożoną logikę biznesową.
Komentarze są przeprosinami, nie wymogiem. Dobry kod *przeważnie* dokumentuje się sam.

**Źle:**
```javascript
function hashIt(data) {
  // Hash
  let hash = 0;

  // Długość łańcucha znaków
  const length = data.length;

  // Pętla po literach w zmiennej data
  for (let i = 0; i < length; i++) {
    // Pobierz kod litery.
    const char = data.charCodeAt(i);
    // Utwórz hash
    hash = ((hash << 5) - hash) + char;
    // Przekonwertuj na liczbę 32-bitową
    hash &= hash;
  }
}
```

**Dobrze:**
```javascript

function hashIt(data) {
  let hash = 0;
  const length = data.length;

  for (let i = 0; i < length; i++) {
    const char = data.charCodeAt(i);
    hash = ((hash << 5) - hash) + char;

    // Przekonwertuj na liczbę 32-bitową
    hash &= hash;
  }
}

```
**[⬆ powrót na początek](#spis-treści)**

<!--
### Don't leave commented out code in your codebase
Version control exists for a reason. Leave old code in your history.
-->
### Nie pozostawiaj zakomentowanego kodu
Kontrola wersji istnieje nie bez powodu. Pozostaw stary kod w Twojej historii.

**Źle:**
```javascript
doStuff();
// doOtherStuff();
// doSomeMoreStuff();
// doSoMuchStuff();
```

**Dobrze:**
```javascript
doStuff();
```
**[⬆ powrót na początek](#spis-treści)**

<!--
### Don't have journal comments
Remember, use version control! There's no need for dead code, commented code,
and especially journal comments. Use `git log` to get history!
-->
### Nie twórz komentarzy-dziennika.
Pamiętaj, używaj kontroli wersji! Nie jest potrzebny martwy kod, zakomentowany kod
i przede wszystkim komentarze będące dziennikiem. Używaj `git log`, by sprawdzić historię!

**Źle:**
```javascript
/**
 * 2016-12-20: Usunąłem monady, nie rozumiałem ich (RM)
 * 2016-10-01: Ulepszyłem użycie specjalnych monad (JP)
 * 2016-02-03: Usunąłem sprawdzanie typów (LI)
 * 2015-03-14: Dodałem funkcję combine ze sprawdzaniem typów (JR)
 */
function combine(a, b) {
  return a + b;
}
```

**Dobrze:**
```javascript
function combine(a, b) {
  return a + b;
}
```
**[⬆ powrót na początek](#spis-treści)**

<!--
### Avoid positional markers
They usually just add noise. Let the functions and variable names along with the
proper indentation and formatting give the visual structure to your code.
-->
### Unikaj markerów pozycyjnych
Zwykle dodają one tylko szum. Pozwól funkcjom i nazwom zmiennych wraz z poprawnymi
wcięciami i formatowaniem dać wizualną strukturę Twojemu kodowi.

**Źle:**
```javascript
////////////////////////////////////////////////////////////////////////////////
// Scope Model Instantiation
////////////////////////////////////////////////////////////////////////////////
$scope.model = {
  menu: 'foo',
  nav: 'bar'
};

////////////////////////////////////////////////////////////////////////////////
// Action setup
////////////////////////////////////////////////////////////////////////////////
const actions = function() {
  // ...
};
```

**Dobrze:**
```javascript
$scope.model = {
  menu: 'foo',
  nav: 'bar'
};

const actions = function() {
  // ...
};
```
**[⬆ powrót na początek](#spis-treści)**

<!--
## Translation

This is also available in other languages:
-->
## Tłumaczenie

Ten dokument dostępny jest również w innych językach:

  - ![br](https://raw.githubusercontent.com/gosquared/flags/master/flags/flags/shiny/24/Brazil.png) **Brazilian Portuguese**: [fesnt/clean-code-javascript](https://github.com/fesnt/clean-code-javascript)
  - ![es](https://raw.githubusercontent.com/gosquared/flags/master/flags/flags/shiny/24/Uruguay.png) **Spanish**: [andersontr15/clean-code-javascript](https://github.com/andersontr15/clean-code-javascript-es)
  - ![cn](https://raw.githubusercontent.com/gosquared/flags/master/flags/flags/shiny/24/China.png) **Chinese**:
    - [alivebao/clean-code-js](https://github.com/alivebao/clean-code-js)
    - [beginor/clean-code-javascript](https://github.com/beginor/clean-code-javascript)
  - ![de](https://raw.githubusercontent.com/gosquared/flags/master/flags/flags/shiny/24/Germany.png) **German**: [marcbruederlin/clean-code-javascript](https://github.com/marcbruederlin/clean-code-javascript)
  - ![kr](https://raw.githubusercontent.com/gosquared/flags/master/flags/flags/shiny/24/South-Korea.png) **Korean**: [qkraudghgh/clean-code-javascript-ko](https://github.com/qkraudghgh/clean-code-javascript-ko)
  - ![pl](https://raw.githubusercontent.com/gosquared/flags/master/flags/flags/shiny/24/Poland.png) **Polish**: [greg-dev/clean-code-javascript-pl](https://github.com/greg-dev/clean-code-javascript-pl)
  - ![ru](https://raw.githubusercontent.com/gosquared/flags/master/flags/flags/shiny/24/Russia.png) **Russian**:
    - [BoryaMogila/clean-code-javascript-ru/](https://github.com/BoryaMogila/clean-code-javascript-ru/)
    - [maksugr/clean-code-javascript](https://github.com/maksugr/clean-code-javascript)
  - ![vi](https://raw.githubusercontent.com/gosquared/flags/master/flags/flags/shiny/24/Vietnam.png) **Vietnamese**: [hienvd/clean-code-javascript/](https://github.com/hienvd/clean-code-javascript/)
  - ![ja](https://raw.githubusercontent.com/gosquared/flags/master/flags/flags/shiny/24/Japan.png) **Japanese**: [mitsuruog/clean-code-javascript/](https://github.com/mitsuruog/clean-code-javascript/)
  - ![id](https://raw.githubusercontent.com/gosquared/flags/master/flags/flags/shiny/24/Indonesia.png) **Indonesia**:
  [andirkh/clean-code-javascript/](https://github.com/andirkh/clean-code-javascript/)

**[⬆ powrót na początek](#spis-treści)**
