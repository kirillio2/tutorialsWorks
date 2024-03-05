Инкапсуляция: 

Существует чтобы защитить свойства класса, их нельзя использовать вне класса, 
можно только в самом классе

class Eat{
    private $name;
    private $type;

    
    public function getName($name){
      return $this->name;
    }
    
    public function getType($type){
      return $this->type;
    }
    
    
    public function setName($name){
      $this->name = $name;
    }
    
    public function setType($type){
      $this->type = $type;
    }
}



Наследование - это механизм, позволяющий новым классам (подклассам или дочерним классам) наследовать свойства и методы уже существующего класса (родительского класса или суперкласса). Подкласс может расширить или переопределить функциональность родительского класса по своему усмотрению.



class Animal {
    protected $name;
    protected $sound;
    
    public function __construct($name, $sound) {
        $this->name = $name;
        $this->sound = $sound;
    }
    
    protected function makeSound() {
        return $this->sound;
    }
    
    public function getInfo() {
        return "This is {$this->name}. It makes " . $this->makeSound() . " sound.";
    }
}

// Дочерний класс, наследующий Animal
class Dog extends Animal {
    public function __construct($name) {
        parent::__construct($name, "bark");
    }
    
    public function wagTail() {
        return "{$this->name} is wagging its tail.";
    }
}

// Дочерний класс, наследующий Animal
class Cat extends Animal {
    public function __construct($name) {
        parent::__construct($name, "meow");
    }
    
    public function purr() {
        return "{$this->name} is purring.";
    }
}

// Использование классов
$dog = new Dog("Buddy");
$cat = new Cat("Whiskers");

echo $dog->getInfo() . "<br>"; // This is Buddy. It makes bark sound.
echo $dog->wagTail() . "<br>"; // Buddy is wagging its tail.

echo $cat->getInfo() . "<br>"; // This is Whiskers. It makes meow sound.
echo $cat->purr() . "<br>"; // Whiskers is purring.




Полимарфизм - означает способность объекта использовать методы с одинаковыми именами, но с различной реализацией, в зависимости от его типа или контекста, в котором он используется. Это позволяет объектам различных классов реализовывать один и тот же интерфейс (например, методы с одинаковыми именами), но с различной логикой выполнения, что улучшает гибкость и переиспользуемость кода.


// Родительский класс
class Shape {
    protected $name;
    
    public function __construct($name) {
        $this->name = $name;
    }
    
    public function getArea() {
        // Базовая реализация для получения площади
        return 0;
    }
}

// Дочерний класс - круг
class Circle extends Shape {
    protected $radius;
    
    public function __construct($name, $radius) {
        parent::__construct($name);
        $this->radius = $radius;
    }
    
    public function getArea() {
        // Переопределение метода для круга
        return pi() * pow($this->radius, 2);
    }
}

// Дочерний класс - прямоугольник
class Rectangle extends Shape {
    protected $width;
    protected $height;
    
    public function __construct($name, $width, $height) {
        parent::__construct($name);
        $this->width = $width;
        $this->height = $height;
    }
    
    public function getArea() {
        // Переопределение метода для прямоугольника
        return $this->width * $this->height;
    }
}

// Использование полиморфизма
$circle = new Circle("Круг", 5);
$rectangle = new Rectangle("Прямоугольник", 4, 6);

// Получение площади для разных фигур
echo "{$circle->name} имеет площадь {$circle->getArea()} <br>"; // Круг имеет площадь 78.539816339745
echo "{$rectangle->name} имеет площадь {$rectangle->getArea()} <br>"; // Прямоугольник имеет площадь 24