# functions

در C، توابع (Functions) به صورت بلوک‌هایی از کد هستند که یک وظیفه خاص را انجام می‌دهند. توابع به شما این امکان را می‌دهند که کد را به بخش‌های کوچکتر تقسیم کرده و هر بخش را به صورت جداگانه اجرا کنید. این امر به بهبود خوانایی کد، تدوین مجدد (refactoring) و استفادهٔ مجدد کد کمک می‌کند.

یک تابع در C معمولاً شامل موارد زیر است:

تعریف تابع (Function Declaration): به طور کلی نوع بازگشتی تابع و نام آن تعریف می‌شود. مثلاً: int add(int a, int b);

تعریف تابع (Function Definition): بدنه‌ی تابع که شامل دستورات مربوط به انجام وظیفه تابع است. مثال:

```c
int add(int a, int b) {
    return a + b;
}
```
صدا زدن تابع (Function Call): در بخش اصلی برنامه یا در دیگر توابع، می‌توانید یک تابع را فراخوانی کنید. مثال:
```c
int result = add(5, 3);
```


رشته‌ها در C به صورت آرایه‌های از نوع کاراکتر تعریف می‌شوند. یک رشته نهایی با اتمام یک کاراکتر نال ('\0') ختم می‌شود. این کاراکتر نال نشان‌دهنده پایان رشته است. برای کار با رشته‌ها، از توابع مختلفی چون strlen (برای اندازه‌ی رشته) و strcpy (برای کپی کردن رشته) استفاده می‌شود. همچنین، می‌توان از عملگرهای رشته‌ای مانند اتصال (strcat) و مقایسه (strcmp) نیز استفاده کرد.



```c
#include <stdio.h>
#include <string.h>

int main() {
    char hello[] = "Hello";
    char world[] = " World";

    // اندازه‌ی رشته
    int len = strlen(hello);

    // کپی کردن رشته
    char copy[20];
    strcpy(copy, hello);

    // اتصال دو رشته
    strcat(copy, world);

    // مقایسه دو رشته
    int result = strcmp(hello, world);

    printf("Length: %d\n", len);
    printf("Copy: %s\n", copy);
    printf("Comparison result: %d\n", result);

    return 0;
}
```
در C، می‌توانید از تابع scanf برای ورود رشته از ورودی استفاده کنید. برای این کار، می‌توانید یک فرمت خوانش رشته (%s) را به scanf ارائه دهید. در زیر یک مثال ساده آورده شده است:
```c
#include <stdio.h>

int main() {
    char inputString[50]; // تعریف یک آرایه برای ذخیره رشته ورودی

    printf("Enter a string: ");
    scanf("%s", inputString);

    printf("You entered: %s\n", inputString);

    return 0;
}
```

از تابع getchar می‌توانید برای خواندن یک کاراکتر از ورودی استفاده کنید. برای خواندن یک رشته کامل از ورودی، می‌توانید از یک حلقه استفاده کنید تا تا زمانی که Enter (جداکننده خط) فشرده نشود، کاراکترها را بخوانید.
```c
#include <stdio.h>

int main() {
    char inputString[50]; // تعریف یک آرایه برای ذخیره رشته ورودی
    int index = 0;
    char c;

    printf("Enter a string: ");

    // خواندن کاراکترها تا زمانی که Enter فشرده نشود
    while ((c = getchar()) != '\n' && index < 49) {
        inputString[index] = c;
        index++;
    }

    inputString[index] = '\0'; // اضافه کردن کاراکتر پایان رشته

    printf("You entered: %s\n", inputString);

    return 0;
}
```
تابع برای تبدیل حروف به حروف کوچک یا بزرگ:
```c
void toLowerCase(char str[]) {
    for (int i = 0; str[i] != '\0'; i++) {
        if (str[i] >= 'A' && str[i] <= 'Z') {
            str[i] += ('a' - 'A'); // تبدیل به حرف کوچک
        }
    }
}
```

تابع برای محاسبه تعداد تکرار یک کاراکتر در یک رشته:
```c
int countOccurrences(char str[], char target) {
    int count = 0;
    for (int i = 0; str[i] != '\0'; i++) {
        if (str[i] == target) {
            count++;
        }
    }
    return count;
}
```

تابع برای محاسبه تعداد کلمات در یک رشته:
```c
int countWords(char str[]) {
    int count = 0;
    int i = 0;

    while (str[i] != '\0') {
        // اگر کاراکتر جاری یک فاصله یا کاراکتر جدید خط باشد، یک کلمه جدید شروع شده است
        if (str[i] == ' ' || str[i] == '\n' || str[i] == '\t') {
            count++;
        }
        i++;
    }

    return count + 1; // تعداد کلمات برابر با تعداد فاصله‌ها + 1
}
```



تابع برای چک کردن اعداد اول:
```c
#include <stdbool.h>

bool isPrime(int num) {
    if (num <= 1) {
        return false;
    }

    for (int i = 2; i * i <= num; i++) {
        if (num % i == 0) {
            return false;
        }
    }

    return true;
}
```

تابع برای مرتب‌سازی آرایه با الگوریتم Bubble Sort:
```c
void bubbleSort(int arr[], int size) {
    for (int i = 0; i < size - 1; i++) {
        for (int j = 0; j < size - i - 1; j++) {
            if (arr[j] > arr[j + 1]) {
                // مقایسه و جابجایی اعضا
                int temp = arr[j];
                arr[j] = arr[j + 1];
                arr[j + 1] = temp;
            }
        }
    }
}
```





