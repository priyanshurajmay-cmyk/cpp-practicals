# cpp-practicals
# C++ Practical Lab Solutions

---

# 1. Sum of First n Terms Using Command Line Argument

```cpp
#include <iostream>
#include <cstdlib>
using namespace std;

int main(int argc, char* argv[])
{
    int n;

    if (argc > 1)
        n = atoi(argv[1]);
    else
    {
        cout << "Enter value of n: ";
        cin >> n;
    }

    int sum = 0;

    for (int i = 1; i <= n; i++)
        sum += i;

    cout << "Sum = " << sum;

    return 0;
}
```

---

# 2. Remove Duplicates from an Array

```cpp
#include <iostream>
using namespace std;

int main()
{
    int n;
    cout << "Enter size of array: ";
    cin >> n;

    int arr[100];

    cout << "Enter elements:\n";
    for (int i = 0; i < n; i++)
        cin >> arr[i];

    cout << "Array after removing duplicates:\n";

    for (int i = 0; i < n; i++)
    {
        bool duplicate = false;

        for (int j = 0; j < i; j++)
        {
            if (arr[i] == arr[j])
            {
                duplicate = true;
                break;
            }
        }

        if (!duplicate)
            cout << arr[i] << " ";
    }

    return 0;
}
```

---

# 3. Count Occurrences of Alphabets Using Command Line Arguments

```cpp
#include <iostream>
#include <cctype>
using namespace std;

int main(int argc, char* argv[])
{
    int count[26] = {0};

    for (int i = 1; i < argc; i++)
    {
        char* str = argv[i];

        while (*str)
        {
            if (isalpha(*str))
            {
                char ch = tolower(*str);
                count[ch - 'a']++;
            }
            str++;
        }
    }

    cout << "Alphabet Occurrences:\n";

    for (int i = 0; i < 26; i++)
    {
        cout << char(i + 'a') << " : " << count[i] << endl;
    }

    return 0;
}
```

---

# 4. Menu Driven String Manipulation Program

```cpp
#include <iostream>
using namespace std;

int length(char str[])
{
    int len = 0;
    while (str[len] != '\0')
        len++;
    return len;
}

void concatenate(char s1[], char s2[])
{
    int i = length(s1);
    int j = 0;

    while (s2[j] != '\0')
    {
        s1[i] = s2[j];
        i++;
        j++;
    }

    s1[i] = '\0';

    cout << "Concatenated String: " << s1 << endl;
}

void compare(char s1[], char s2[])
{
    int i = 0;

    while (s1[i] == s2[i] && s1[i] != '\0' && s2[i] != '\0')
        i++;

    if (s1[i] == s2[i])
        cout << "Strings are Equal\n";
    else
        cout << "Strings are Not Equal\n";
}

void uppercase(char str[])
{
    int i = 0;

    while (str[i] != '\0')
    {
        if (str[i] >= 'a' && str[i] <= 'z')
            str[i] = str[i] - 32;
        i++;
    }

    cout << "Uppercase String: " << str << endl;
}

void reverse(char str[])
{
    int len = length(str);

    cout << "Reversed String: ";

    for (int i = len - 1; i >= 0; i--)
        cout << str[i];

    cout << endl;
}

void insertString(char mainStr[], char insertStr[], int pos)
{
    int lenMain = length(mainStr);
    int lenInsert = length(insertStr);

    for (int i = lenMain; i >= pos; i--)
        mainStr[i + lenInsert] = mainStr[i];

    for (int i = 0; i < lenInsert; i++)
        mainStr[pos + i] = insertStr[i];

    cout << "Updated String: " << mainStr << endl;
}

int main()
{
    char str1[200], str2[100];
    int choice;

    do
    {
        cout << "\n1. Show Address of Each Character";
        cout << "\n2. Concatenate Strings";
        cout << "\n3. Compare Strings";
        cout << "\n4. Length of String";
        cout << "\n5. Convert to Uppercase";
        cout << "\n6. Reverse String";
        cout << "\n7. Insert String";
        cout << "\n8. Exit";
        cout << "\nEnter Choice: ";
        cin >> choice;

        switch (choice)
        {
        case 1:
            cout << "Enter String: ";
            cin >> str1;

            for (int i = 0; str1[i] != '\0'; i++)
                cout << str1[i] << " : " << (void*)&str1[i] << endl;
            break;

        case 2:
            cout << "Enter First String: ";
            cin >> str1;
            cout << "Enter Second String: ";
            cin >> str2;
            concatenate(str1, str2);
            break;

        case 3:
            cout << "Enter First String: ";
            cin >> str1;
            cout << "Enter Second String: ";
            cin >> str2;
            compare(str1, str2);
            break;

        case 4:
            cout << "Enter String: ";
            cin >> str1;
            cout << "Length = " << length(str1) << endl;
            break;

        case 5:
            cout << "Enter String: ";
            cin >> str1;
            uppercase(str1);
            break;

        case 6:
            cout << "Enter String: ";
            cin >> str1;
            reverse(str1);
            break;

        case 7:
            int pos;
            cout << "Enter Main String: ";
            cin >> str1;
            cout << "Enter String to Insert: ";
            cin >> str2;
            cout << "Enter Position: ";
            cin >> pos;
            insertString(str1, str2, pos);
            break;
        }

    } while (choice != 8);

    return 0;
}
```

---

# 5. Merge Two Ordered Arrays

```cpp
#include <iostream>
using namespace std;

int main()
{
    int n1, n2;

    cout << "Enter size of first array: ";
    cin >> n1;

    int a[100];

    cout << "Enter elements in sorted order:\n";
    for (int i = 0; i < n1; i++)
        cin >> a[i];

    cout << "Enter size of second array: ";
    cin >> n2;

    int b[100];

    cout << "Enter elements in sorted order:\n";
    for (int i = 0; i < n2; i++)
        cin >> b[i];

    int c[200];
    int i = 0, j = 0, k = 0;

    while (i < n1 && j < n2)
    {
        if (a[i] < b[j])
            c[k++] = a[i++];
        else
            c[k++] = b[j++];
    }

    while (i < n1)
        c[k++] = a[i++];

    while (j < n2)
        c[k++] = b[j++];

    cout << "Merged Array:\n";

    for (int x = 0; x < k; x++)
        cout << c[x] << " ";

    return 0;
}
```

---

# 6a. Binary Search Using Recursion

```cpp
#include <iostream>
using namespace std;

int binarySearch(int arr[], int low, int high, int key)
{
    if (low > high)
        return -1;

    int mid = (low + high) / 2;

    if (arr[mid] == key)
        return mid;

    if (key < arr[mid])
        return binarySearch(arr, low, mid - 1, key);

    return binarySearch(arr, mid + 1, high, key);
}

int main()
{
    int n;
    cin >> n;

    int arr[100];

    for (int i = 0; i < n; i++)
        cin >> arr[i];

    int key;
    cin >> key;

    int result = binarySearch(arr, 0, n - 1, key);

    if (result == -1)
        cout << "Element Not Found";
    else
        cout << "Element Found at Index " << result;

    return 0;
}
```

---

# 6b. Binary Search Without Recursion

```cpp
#include <iostream>
using namespace std;

int main()
{
    int n;
    cin >> n;

    int arr[100];

    for (int i = 0; i < n; i++)
        cin >> arr[i];

    int key;
    cin >> key;

    int low = 0, high = n - 1;
    int found = -1;

    while (low <= high)
    {
        int mid = (low + high) / 2;

        if (arr[mid] == key)
        {
            found = mid;
            break;
        }
        else if (key < arr[mid])
            high = mid - 1;
        else
            low = mid + 1;
    }

    if (found == -1)
        cout << "Element Not Found";
    else
        cout << "Element Found at Index " << found;

    return 0;
}
```

---

# 7a. GCD Using Recursion

```cpp
#include <iostream>
using namespace std;

int gcd(int a, int b)
{
    if (b == 0)
        return a;

    return gcd(b, a % b);
}

int main()
{
    int a, b;
    cin >> a >> b;

    cout << "GCD = " << gcd(a, b);

    return 0;
}
```

---

# 7b. GCD Without Recursion

```cpp
#include <iostream>
using namespace std;

int main()
{
    int a, b;
    cin >> a >> b;

    while (b != 0)
    {
        int temp = b;
        b = a % b;
        a = temp;
    }

    cout << "GCD = " << a;

    return 0;
}
```

---

# 8. Matrix Class Operations

```cpp
#include <iostream>
using namespace std;

class Matrix
{
    int a[10][10], r, c;

public:
    void input()
    {
        cout << "Enter rows and columns: ";
        cin >> r >> c;

        cout << "Enter elements:\n";

        for (int i = 0; i < r; i++)
            for (int j = 0; j < c; j++)
                cin >> a[i][j];
    }

    void display()
    {
        for (int i = 0; i < r; i++)
        {
            for (int j = 0; j < c; j++)
                cout << a[i][j] << " ";

            cout << endl;
        }
    }

    Matrix add(Matrix m)
    {
        if (r != m.r || c != m.c)
            throw "Addition not possible";

        Matrix temp;
        temp.r = r;
        temp.c = c;

        for (int i = 0; i < r; i++)
            for (int j = 0; j < c; j++)
                temp.a[i][j] = a[i][j] + m.a[i][j];

        return temp;
    }

    Matrix multiply(Matrix m)
    {
        if (c != m.r)
            throw "Multiplication not possible";

        Matrix temp;
        temp.r = r;
        temp.c = m.c;

        for (int i = 0; i < temp.r; i++)
        {
            for (int j = 0; j < temp.c; j++)
            {
                temp.a[i][j] = 0;

                for (int k = 0; k < c; k++)
                    temp.a[i][j] += a[i][k] * m.a[k][j];
            }
        }

        return temp;
    }

    void transpose()
    {
        for (int i = 0; i < c; i++)
        {
            for (int j = 0; j < r; j++)
                cout << a[j][i] << " ";

            cout << endl;
        }
    }
};

int main()
{
    Matrix m1, m2, result;

    try
    {
        cout << "Enter First Matrix:\n";
        m1.input();

        cout << "Enter Second Matrix:\n";
        m2.input();

        cout << "Sum:\n";
        result = m1.add(m2);
        result.display();

        cout << "Product:\n";
        result = m1.multiply(m2);
        result.display();

        cout << "Transpose of First Matrix:\n";
        m1.transpose();
    }
    catch (const char* msg)
    {
        cout << msg << endl;
    }

    return 0;
}
```

---

# 9. Inheritance and Runtime Polymorphism

```cpp
#include <iostream>
using namespace std;

class Person
{
protected:
    string name;

public:
    void getName()
    {
        cout << "Enter Name: ";
        cin >> name;
    }

    virtual void display()
    {
        cout << "Name: " << name << endl;
    }
};

class Student : public Person
{
    string course;
    int marks, year;

public:
    void getData()
    {
        getName();

        cout << "Enter Course: ";
        cin >> course;

        cout << "Enter Marks: ";
        cin >> marks;

        cout << "Enter Year: ";
        cin >> year;
    }

    void display()
    {
        cout << "Student Details\n";
        cout << "Name: " << name << endl;
        cout << "Course: " << course << endl;
        cout << "Marks: " << marks << endl;
        cout << "Year: " << year << endl;
    }
};

class Employee : public Person
{
    string department;
    int salary;

public:
    void getData()
    {
        getName();

        cout << "Enter Department: ";
        cin >> department;

        cout << "Enter Salary: ";
        cin >> salary;
    }

    void display()
    {
        cout << "Employee Details\n";
        cout << "Name: " << name << endl;
        cout << "Department: " << department << endl;
        cout << "Salary: " << salary << endl;
    }
};

int main()
{
    Person* p;

    Student s;
    s.getData();

    Employee e;
    e.getData();

    p = &s;
    p->display();

    p = &e;
    p->display();

    return 0;
}
```

---

# 10. Triangle Class with Exception Handling

```cpp
#include <iostream>
#include <cmath>
using namespace std;

class Triangle
{
    float a, b, c;

public:
    Triangle(float x, float y, float z)
    {
        if (x <= 0 || y <= 0 || z <= 0)
            throw "Sides must be greater than 0";

        if ((x + y <= z) || (x + z <= y) || (y + z <= x))
            throw "Invalid Triangle";

        a = x;
        b = y;
        c = z;
    }

    float area()
    {
        float s = (a + b + c) / 2;
        return sqrt(s * (s - a) * (s - b) * (s - c));
    }

    float area(float base, float height)
    {
        return 0.5 * base * height;
    }
};

int main()
{
    try
    {
        Triangle t(3, 4, 5);

        cout << "Area using Heron's Formula: " << t.area() << endl;

        cout << "Area of Right Angled Triangle: " << t.area(3, 4);
    }
    catch (const char* msg)
    {
        cout << msg;
    }

    return 0;
}
```

---

# 11. Store and Retrieve Student Records from File

```cpp
#include <iostream>
#include <fstream>
using namespace std;

class Student
{
public:
    int roll;
    char name[50];
    char className[20];
    int year;
    float marks;

    void input()
    {
        cout << "Enter Roll No: ";
        cin >> roll;

        cout << "Enter Name: ";
        cin >> name;

        cout << "Enter Class: ";
        cin >> className;

        cout << "Enter Year: ";
        cin >> year;

        cout << "Enter Marks: ";
        cin >> marks;
    }

    void display()
    {
        cout << roll << " " << name << " " << className
             << " " << year << " " << marks << endl;
    }
};

int main()
{
    Student s;

    ofstream fout("students.txt");

    for (int i = 0; i < 5; i++)
    {
        s.input();

        fout << s.roll << " "
             << s.name << " "
             << s.className << " "
             << s.year << " "
             << s.marks << endl;
    }

    fout.close();

    ifstream fin("students.txt");

    cout << "\nStudent Records:\n";

    while (fin >> s.roll >> s.name >> s.className >> s.year >> s.marks)
    {
        s.display();
    }

    fin.close();

    return 0;
}
```

---

# 12. Copy File After Removing Whitespaces

```cpp
#include <iostream>
#include <fstream>
using namespace std;

int main()
{
    ifstream fin("input.txt");
    ofstream fout("output.txt");

    char ch;

    while (fin.get(ch))
    {
        if (ch != ' ' && ch != '\n' && ch != '\t')
            fout.put(ch);
    }

    fin.close();
    fout.close();

    cout << "Contents copied successfully without whitespaces.";

    return 0;
}
```
