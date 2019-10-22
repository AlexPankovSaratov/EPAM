
public class Main {
    public static void main(String[] args) {
        //Добый день =) Для каждого метода сделал свою функцию.
        //Для проверки в методе main вызываю их последовательно и результат принтую.
        //В 5 задании использую самописный класс стэка "Dynamic_stack"
        int[] nums = new int[] { 10, 5, 3, 8, 2 };
        int[] result = Task1_ArraySorting(nums);
        System.out.println("Результат 1 задания :");
        for(int i = 0; i < result.length; i ++)
            System.out.println("Array element = " + result[i]);
        int x = 5;
        System.out.println("");
        System.out.println("Результат 2 задания :");
        if (Task2_Search(x, result)) {
            System.out.println("Task2_Search = " + x);
        }else{
            System.out.println("Данного значения нет в массиве = " + x);
        }
        System.out.println("");
        System.out.println("Результат 3 задания :");
        System.out.println(Task3_UniqueWords("один два три четыри два четыри пять"));
        System.out.println("");
        System.out.println("Результат 4 задания :");
        Task4_factorial(25);
        System.out.println("");
        System.out.println("Результат 5 задания :");
        String BracketSequence = "([()]){()}";
        if ( Task5_CorrectBracketSequence(BracketSequence)){
            System.out.println("Скобочная последовательность " + BracketSequence + " - Правильная");
        }else  System.out.println("Скобочная последовательность " + BracketSequence + " - Не правильная");
    }
    //Задание 1. Сортировка массива.
    public static int[] Task1_ArraySorting(int arr[]) {
        int tempValue;
        for (int i = 0; i < arr.length - 1; i++) {
            for (int j = i+1; j <= arr.length - 1 ; j++)
                if (arr[j] < arr[i]){
                    tempValue = arr[i];
                    arr[i] = arr[j];
                    arr[j] = tempValue;
                }
        }
        return arr;
    }
    //Задание 2. Поиск значение в отсортированном массиве.
    public static boolean Task2_Search(int x, int arr[]){
        boolean result = false;
        int firstvalue = arr[0];
        int lastvalue = arr[arr.length-1];
        if ((firstvalue < x && x < lastvalue) || (firstvalue > x && x > lastvalue)){
            for (int i = 0 ; i <= arr.length-1 ; i++){
                if (arr[i] == x) result = true;
            }
        }
        return result;
    }
    //Задание 3 Возвращает только те слова, которые встречаются в ней только один
    //раз.
    public static String Task3_UniqueWords(String x){
        String [] ArrayString = x.split(" ");
        String result = "";
        //Если нельзя использовать split и регулярные выражения то можно бежать по Char'ам
        // и формировать массив через substring по индексам пробелов
        for (int i = 0; i <= ArrayString.length-1; i++){
            int coincidence = 0;
            for (int j = 0; j <= ArrayString.length-1; j++){
                if (ArrayString[i].equals(ArrayString[j])) coincidence ++;
            }
            if (coincidence == 1) {
                if (result == "")result = result + ArrayString[i];
                else result = result + " " + ArrayString[i];
            }
        }
        return result;
    }
    //Задание 4 Вычисление Факториала (Так же можно вычислить его с помощью рекурсии, время не стал тратить)
    public static void Task4_factorial(int x){
        long result = 1;
        for (int i = 1; i <= x; i ++){
            result = result*i;
        }
        System.out.println("Факториал " + x + " = " + result);
    }
    //Задание 5  Правильная скобочная последовательность (Так же можно использовать в данном заданий класс Stack)
    // Но я использовал свой класс Dynamic_stack.
    public static boolean Task5_CorrectBracketSequence(String x){
        Dynamic_stack Stack = new Dynamic_stack(x.length());
        for(int i = 0 ; i <= x.length()-1; i++) {
            char temp = x.charAt(i);
            if (temp == '(' || temp == '[' || temp == '{') {
                Stack.AddInStack(temp);
            }else{
                if (temp == ')') {
                    if(!(Stack.getLastValue()  == '(')) return false;
                }
                if (temp == ']') {
                    if(!(Stack.getLastValue()  == '[')) return false;
                }
                if (temp == '}') {
                    if(!(Stack.getLastValue()  == '{')) return false;
                }
            }
        }
        return true;
    }
}
