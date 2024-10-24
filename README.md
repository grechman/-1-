## Отчет по лабораторной работе № 1

#### № группы: `ПМ-2401`

#### Выполнил: `Гречков Максим Дмитриевич`

#### Вариант: `9`

### Cодержание:

- [Постановка задачи](#1-постановка-задачи)
- [Входные и выходные данные](#2-входные-и-выходные-данные)
- [Выбор структуры данных](#3-выбор-структуры-данных)
- [Алгоритм](#4-алгоритм)
- [Программа](#5-программа)
- [Анализ правильности решения](#6-анализ-правильности-решения)

### 1. Постановка задачи

> Программа получает на вход 4 числа A, B, C и D не пресыщающих по модулю 10<sup>9</sup>. Нужно выяснить, из скольки чисел
> составить строго возрастающюю последовательность. Если это все числа, то вывести "для всех чисел"
Данную задачу можно разделить на 2 подзадачи: сортировка и сравнение попарно чисел.

- Для 1 подзадачи нужно:
    1. `Ввести данные с клавиатуры и проверить их на различия`
- Для 2 подзадачи нужно:
    1. `Сравниваем числа и убираем счетчик, если они совпали`


### 2. Входные и выходные данные

#### Данные на вход

На вход программа должна получать 4 числа, при этом в условии сказано, что они натуральные, а значит будем использовать `Integer`. Граница таких чисел <= 10<sup>9</sup>

|             | Тип                | min значение    | max значение   |
|-------------|--------------------|-----------------|----------------|
| A (Число 1) | Натуральное  число | -10<sup>9</sup> | 10<sup>9</sup> |
| B (Число 2) | Натуральное  число | -10<sup>9</sup> | 10<sup>9</sup> |
| C (Число 3) | Натуральное  число | -10<sup>9</sup> | 10<sup>9</sup> |
| D (Число 4) | Натуральное  число | -10<sup>9</sup> | 10<sup>9</sup> |

#### Данные на выход

Программа должна вывести количество кубиков, которые можно поставить друг на друга и все ли кубы попали под условие.
Значит выходными данными будет строка с сообщением и натуральное число

|         | Тип               | min значение | max значение   |
|---------|-------------------|--------------|----------------|
| Число 1 | Натуральное число | 0            | 10<sup>9</sup> |
| Строка 1| Строка            |       -      |       -        |

### 3. Выбор структуры данных

Программа получает 4 натуральных числа, поэтому будем работать с типом данных `int`. 
|                 | название переменной | Тип (в Java)         | 
|---------------|--------------------------|----------------------|
| A (Число 1) | `A`                       | `int`|
| B (Число 2) | `B`                       | `int`|
| C (Число 3) | `C`                       | `int`|
| D (Число 4) | `D`                       | `int`|

Для вывода результата необязательно его хранить в отдельной переменной.

### 4. Алгоритм

#### Алгоритм выполнения программы:

1. **Ввод данных:**  
   Программа вводит 4 переменные типа int.

2. **Сравнение чисел:**  
   Программа сравнивает соседние элементы. Если они равны, то уменьшается счетчик.

3. **Вывод результата:**  
   На экран выводится количество кубиков в башне и сообщение, задействованы ли все кубики.

#### Блок-схема

```mermaid
graph TD
    A[Start] --> B[Initialize Scanner and PrintStream]
    B --> C[Read A, B, C, D]
    C --> D[Initialize count = 4]
    D --> E{if (A == B)}
    E -->|Yes| F[count--]
    E -->|No| G{if (A == C)}
    G -->|Yes| H[count--]
    G -->|No| I{if (A == D)}
    I -->|Yes| J[count--]
    I -->|No| K{if (B == C)}
    K -->|Yes| L{if (A != B)}
    L -->|Yes| M[count--]
    L -->|No| N{if (B == D)}
    K -->|No| N
    N -->|Yes| O{if (A != B)}
    O -->|Yes| P[count--]
    O -->|No| Q{if (C == D)}
    N -->|No| Q
    Q -->|Yes| R{if (A != C)}
    R -->|Yes| S[count--]
    R -->|No| T[Print "Количество квадратов:" + count]
    Q -->|No| T
    T --> U{if (count == 4)}
    U -->|Yes| V[Print "Все квадраты можно расположить"]
    U -->|No| W[End]
    V --> W

```

### 5. Программа

```java
package com.company;


import java.io.PrintStream;
import java.util.Scanner;
public class Main {
    // Объявляем объект класса Scanner для ввода данных
    public static Scanner in = new Scanner(System.in);
    // Объявляем объект класса PrintStream для вывода данных
    public static PrintStream out = System.out;

    public static void main(String[] args) {
        // Sample input values
        int A = in.nextInt();
        int B = in.nextInt();
        int C = in.nextInt();
        int D = in.nextInt();

        int count = 4; // We can always place at least one square

        // Check if we can place 2 squares
        if (A == B)
            count--;
        if (A == C)
            count--;
        if (A == D)
            count--;
        if (B == C)
            if (A != B)
                count--;
        if (B == D)
            if (A != B)
                count--;
        if (C == D)
            if (A != C)
                count--;

        out.println("Количество квадратов: " + count);
	if (count == 4)
            out.println("Все квадраты можно расположить");
    }
}

```

### 6. Анализ правильности решения

Программа работает корректно на всем множестве решений с учетом ограничений.

1. Тест на `разные`:

    - **Input**:
        ```
        1 2 3 4
        ```

    - **Output**:
        ```
        Количество квадратов: 4
	Все квадраты можно расположить
        ```

2. Тест на `одинаковые` :

    - **Input**:
        ```
        1 1 1 1
        ```

    - **Output**:
        ```
        Количество квадратов: 1
        ```

3. Тест на ограничение задачи:

    - **Input**:
        ```
        10000000 1000 1000 10
        ```

    - **Output**:
        ```
        Количество квадратов: 3
        ```
