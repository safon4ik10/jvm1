```
public class JvmComprehension {
    public static void main(String[] args) {
        int i = 1;                      // 1
        Object o = new Object();        // 2
        Integer ii = 2;                 // 3
        printAll(o, i, ii);             // 4
        System.out.println("finished"); // 7
    }

    private static void printAll(Object o, int i, Integer ii) {
        Integer uselessVar = 700;                   // 5
        System.out.println(o.toString() + i + ii);  // 6
    }
}
```

# Class loader: 
В Application ClassLoader будет передан в загрузку JvmComprehension, который в свою очередь делегирует это в Platfomr ClassLoader и далее в Bootstrap ClassLoader, данный класс должен быть загружен из Application ClassLoader, 
так же при инициализации будут проинциализированны статические методы
Далее информация о классе JvmComprehension подгрузится в метаспейс (его имя, и методы)

# Описание
В момент вызовы метода main будет создан фрейм в Stack memmory
1) Затем в этот фрейм загрузится перменная i
2) В heap будет загружен объект new Object(), а в фрейм main ссылка на объект Object
3) Я тут не совсем уверен, но попытаюсь предположить, что ссылка на объект будет храниться в фрейме main, значение в heap
4) Будет создан еще один фрейм для printAll, ссылки на объекты (Integer, Object) подгрузятся в фрейм printAll и будут ссылаться на те же объекты, примитив int i будет храниться в фрейме
5) Ссылка на объект будет храниться в фрейме printAll, значение в heap
6) Создастся фрейм в котором будет храниться ссылка на o и ii, i будет храниться в фрейме
7) Создастся фрейм в котором будет храниться временная? ссылка на строковую перменную, объект которой будет лежать в heap 

# GC 
В коде нет циклов и долгой работы программы, GC будет вызыван один раз в момент завершения программы.
